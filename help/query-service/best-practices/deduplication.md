---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Datendeduplizierung; Deduplizierung;
solution: Experience Platform
title: Datendeduplizierung in Query Service
topic-legacy: queries
type: Tutorial
description: In diesem Dokument werden Beispiele für die Unter-Auswahl und vollständige Beispielabfrage zur Deduplizierung von drei gängigen Anwendungsfällen, Erlebnisereignisse, Käufe und Metriken, vorgestellt.
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: b140037ed5f055a8e7c583540910cc6b18bbf0bd
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# Datendeduplizierung in [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] unterstützt die Datendeduplizierung. Eine Datendeduplizierung kann durchgeführt werden, wenn eine ganze Zeile aus einer Berechnung entfernt oder ein bestimmter Satz von Feldern ignoriert werden muss, da nur ein Teil der Daten in der Zeile doppelte Informationen enthält.

Die Deduplizierung umfasst in der Regel die Verwendung der `ROW_NUMBER()` -Funktion in einem Fenster für eine ID (oder ein Paar von IDs) über einen bestimmten Zeitraum hinweg, die ein neues Feld zurückgibt, das die Anzahl der erkannten Duplikate darstellt. Die Zeit wird häufig durch die Verwendung der [!DNL Experience Data Model] (XDM) `timestamp` -Feld.

Wenn der Wert der `ROW_NUMBER()` is `1`, bezieht er sich auf die ursprüngliche Instanz. Im Allgemeinen ist dies die Instanz, die Sie verwenden möchten. Dies erfolgt meist innerhalb einer Unterauswahl, bei der die Deduplizierung auf einer höheren Ebene erfolgt `SELECT` z. B. Aggregat-Zählung.

Anwendungsfälle für die Deduplizierung können entweder global sein oder auf eine einzelne Benutzer- oder Endbenutzer-ID innerhalb der `identityMap`.

In diesem Dokument wird die Deduplizierung für drei gängige Anwendungsfälle beschrieben: Erlebnisereignisse, Käufe und Metriken.

Zu jedem Beispiel gehören der Perimeter, der Fensterschlüssel, ein Entwurf der Deduplizierungsmethode sowie die vollständige SQL-Abfrage.

## Erlebnisereignisse {#experience-events}

Bei doppelten Erlebnisereignissen sollten Sie wahrscheinlich die gesamte Zeile ignorieren.

>[!CAUTION]
>
>Viele Datensätze in [!DNL Experience Platform], einschließlich der vom Adobe Analytics Data Connector erstellten, bereits eine Deduplizierung auf Erlebnisebene angewendet. Daher ist eine erneute Anwendung dieser Deduplizierungsstufe nicht erforderlich und verlangsamt Ihre Abfrage.
>
>Es ist wichtig, die Quelle Ihrer Datensätze zu verstehen und zu wissen, ob die Deduplizierung auf Erlebnis-Ereignis-Ebene bereits angewendet wurde. Für alle gestreamten Datensätze (z. B. solche aus Adobe Target) müssen Sie **will** muss eine Deduplizierung auf Erlebnis-Event-Ebene anwenden, da diese Datenquellen &quot;mindestens einmal&quot;Semantik haben.

**Umfang:** Global

**Window key:** `id`

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

Wenn Sie doppelte Käufe haben, sollten Sie den Großteil der [!DNL Experience Event] Zeile, aber die mit dem Kauf verbundenen Felder ignorieren (z. B. die `commerce.orders` Metrik). Käufe enthalten ein spezielles Feld für die Kauf-ID, d. h. `commerce.order.purchaseID`.

Es wird empfohlen, `purchaseID` im Besucherbereich, da dies das standardmäßige semantische Feld für Kauf-IDs in XDM ist. Der Besucherbereich wird zum Entfernen doppelter Kaufdaten empfohlen, da die Abfrage schneller ist als der globale Bereich. Es ist unwahrscheinlich, dass eine Kauf-ID über mehrere Besucher-IDs hinweg dupliziert wird.

**Umfang:** Besucher

**Window key:** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

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
>In einigen Fällen, in denen die ursprünglichen Analytics-Daten doppelte Kauf-IDs über Besucher-IDs hinweg enthalten, müssen Sie **kann** müssen die Kauf-ID-Duplikatzählung für alle Besucher ausführen. Wenn die Kauf-ID nicht vorhanden ist, müssen Sie bei dieser Methode eine Bedingung einbeziehen, die stattdessen die Ereignis-ID verwendet, um die Abfrage so schnell wie möglich zu halten.

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

Wenn Sie eine Metrik haben, die die optionale eindeutige ID verwendet, und ein Duplikat dieser ID angezeigt wird, sollten Sie diesen Metrikwert ignorieren und den Rest des Erlebnisereignisses beibehalten.

In XDM verwenden fast alle Metriken die `Measure` Datentyp mit einem optionalen `id` -Feld, das Sie für die Deduplizierung verwenden können.

**Umfang:** Besucher

**Window key:** identityMap[$NAMESPACE].id und id des Measurement-Objekts

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

In diesem Dokument wurde beschrieben, wie Daten in Query Service dedupliziert werden können, sowie Beispiele für die Deduplizierung von Daten. Weitere Best Practices beim Schreiben von Abfragen mit Query Service finden Sie im Abschnitt [Anleitung zum Schreiben von Abfragen](./writing-queries.md).
