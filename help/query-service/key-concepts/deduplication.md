---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;Datendeduplizierung;Deduplizierung;
solution: Experience Platform
title: Datendeduplizierung in Abfrage-Service
type: Tutorial
description: 'In diesem Dokument werden Beispiele für Unterauswahlen und vollständige Abfragen zur Deduplizierung von drei gängigen Anwendungsfällen beschrieben: Erlebnisereignisse, Käufe und Metriken.'
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 100%

---

# Datendeduplizierung in [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] unterstützt die Duplizierung von Daten. Daten können dedupliziert werden, wenn eine ganze Zeile aus einer Berechnung entfernt oder ein bestimmter Satz von Feldern ignoriert werden muss, da nur ein Teil der Daten in der Zeile doppelte Informationen enthält.

Die Deduplizierung umfasst in der Regel die Verwendung der Funktion `ROW_NUMBER()` in einem Fenster für eine ID (oder ein ID-Paar) über einen bestimmten Zeitraum hinweg, die ein neues Feld mit der Anzahl der erkannten Duplikate zurückgibt. Die Zeit wird häufig durch die Verwendung des Felds [!DNL Experience Data Model] (XDM) `timestamp` dargestellt.

Ein `ROW_NUMBER()`-Wert von `1` bezieht sich auf die ursprüngliche Instanz. Im Allgemeinen ist dies die Instanz, die verwendet werden soll. Dies geschieht meist innerhalb einer Unterauswahl, bei der die Deduplizierung in einer höheren `SELECT`-Anweisung erfolgt, wie z. B. einer Aggregatzählung.

Anwendungsfälle für die Deduplizierung können entweder global sein oder auf eine einzelne Benutzer- oder Endbenutzer-ID innerhalb von `identityMap` beschränkt sein.

In diesem Dokument wird die Deduplizierung für drei gängige Anwendungsfälle beschrieben: Erlebnisereignisse, Käufe und Metriken.

Zu jedem Beispiel gehören der Bereich, der Fensterschlüssel, eine Beschreibung der Deduplizierungsmethode sowie die vollständige SQL-Abfrage.

## Erlebnisereignisse {#experience-events}

Bei doppelten Erlebnisereignissen soll wahrscheinlich die gesamte Zeile ignoriert werden.

>[!CAUTION]
>
>Bei vielen Datensätzen in [!DNL Experience Platform], einschließlich der vom Adobe Analytics Data Connector erstellten, wurde bereits eine Deduplizierung auf Erlebnisereignis-Ebene angewendet. Daher ist eine erneute Anwendung dieser Deduplizierungsstufe nicht erforderlich und verlangsamt Ihre Abfrage.
>
>Es ist wichtig, die Quelle Ihrer Datensätze zu verstehen und zu wissen, ob die Deduplizierung auf Erlebnisereignis-Ebene bereits angewendet wurde. Für gestreamte Datensätze (z. B. solche aus Adobe Target) **müssen** Sie eine Deduplizierung auf Erlebnisereignis-Ebene anwenden, da diese Datenquellen eine „mindestens einmal“-Semantik aufweisen.

**Bereich:** Global

**Fensterschlüssel:** `id`

### Beispiel einer Deduplizierung

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

### Vollständiges Beispiel

```sql
SELECT COUNT(*) AS num_events FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num
  FROM experience_events
) WHERE id_dup_num = 1
```

## Käufe {#purchases}

Bei doppelten Käufen soll der Großteil der Zeile [!DNL Experience Event] wahrscheinlich beibehalten, aber die mit dem Kauf verbundenen Felder (z. B. die Metrik `commerce.orders`) ignoriert werden. Käufe enthalten ein spezielles Feld für die Kauf-ID: `commerce.order.purchaseID`.

Es wird empfohlen, `purchaseID` im Besucherbereich zu verwenden, da dies das standardmäßige semantische Feld für Kauf-IDs in XDM ist. Der Besucherbereich wird zum Entfernen doppelter Kaufdaten empfohlen, da die Abfrage schneller ist als der globale Bereich. Es ist unwahrscheinlich, dass eine Kauf-ID über mehrere Besucher-IDs hinweg dupliziert wird.

**Bereich:** Besuchende

**Fensterschlüssel:** identityMap[$NAMESPACE].id und commerce.order.purchaseID

### Beispiel einer Deduplizierung

```sql
SELECT *,
  IF(LENGTH(commerce.`order`.purchaseID) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, commerce.`order`.purchaseID
            ORDER BY timestamp ASC
      ),
    1) AS purchaseID_dup_num
FROM experience_events
```

>[!NOTE]
>
>In einigen Fällen, in denen die ursprünglichen Analytics-Daten doppelte Kauf-IDs über Besucher-IDs hinweg enthalten, müssen Sie **gegebenenfalls** die Kauf-ID-Duplikatszählung für alle Besuchenden ausführen. Wenn die Kauf-ID nicht vorhanden ist, müssen Sie bei dieser Methode eine Bedingung einschließen, die stattdessen die Ereignis-ID verwendet, um eine möglichst schnelle Abfrage sicherzustellen.

### Vollständiges Beispiel

Im folgenden Beispiel wird eine Bedingungsklausel verwendet, um die Ereignis-ID zu verwenden, falls die Kauf-ID nicht vorhanden ist.

```sql
SELECT SUM(commerce.purchases.value) AS num_purchases FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(commerce.`order`.purchaseID) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, commerce.order.purchaseID
              ORDER BY timestamp ASC
        ),
      1) AS purchaseID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND purchaseID_dup_num = 1
```

## Metriken {#metrics}

Bei einer Metrik, die die optionale eindeutige ID verwendet, und ein Duplikat dieser ID auftaucht, soll dieser Metrikwert wahrscheinlich ignoriert und der Rest des Erlebnisereignisses beibehalten werden.

In XDM verwenden fast alle Metriken den Datentyp `Measure` mit einem optionalen `id`-Feld, das Sie für die Deduplizierung verwenden können.

**Bereich:** Besuchende

**Fensterschlüssel:** identityMap[$NAMESPACE].id und ID des Maßnahmen-Objekts

### Beispiel einer Deduplizierung

```sql
SELECT *,
  IF(LENGTH(application.launches.id) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
            ORDER BY timestamp ASC
      ),
    1) AS launchesID_dup_num
FROM experience_events
```

### Vollständiges Beispiel

```sql
SELECT SUM(application.launches.value) AS num_launches FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(application.launches.id) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
              ORDER BY timestamp ASC
        ),
      1) AS launchesID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND launchesID_dup_num = 1
```

## Nächste Schritte

In diesem Dokument wurden Beispiele für die Datendeduplizierung und die Durchführung einer Datendeduplizierung im Abfrage-Service beschrieben. Weitere Best Practices beim Schreiben von Abfragen mit Abfrage-Service finden Sie im [Handbuch zum Schreiben von Abfragen](../best-practices/writing-queries.md).
