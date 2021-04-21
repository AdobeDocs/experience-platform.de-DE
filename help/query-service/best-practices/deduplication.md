---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Dienst;Abfrage-Dienst;Daten-Deduplizierung-Duplikate;Deduplizierung-Duplikate
solution: Experience Platform
title: Data Deduplizierung-Duplikate im Abfrage-Dienst
topic-legacy: queries
type: Tutorial
description: In diesem Dokument werden Beispiele für die Unter-Auswahl- und vollständige Abfrage von Beispielen für die Deduplizierung von drei gängigen Anwendungsfällen erläutert. Erlebnis-Ereignis, Käufe und Metriken.
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# Data Deduplizierung-Duplikate in [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] unterstützt Data Deduplizierung-Duplikate. Das Deduplizierung-Duplikate von Daten kann ausgeführt werden, wenn eine ganze Zeile aus einer Berechnung entfernt oder ein bestimmter Feldsatz ignoriert werden muss, da nur ein Teil der Daten in der Zeile Duplikat-Informationen ist.

Deduplizierung-Duplikate umfasst in der Regel die Verwendung der Funktion `ROW_NUMBER()` für eine ID (oder mehrere IDs) über einen bestimmten Zeitraum hinweg, wodurch ein neues Feld zurückgegeben wird, das die Anzahl der Erkennung eines Duplikats darstellt. Die Zeit wird häufig mithilfe des Felds [!DNL Experience Data Model] (XDM) `timestamp` dargestellt.

Wenn der Wert von `ROW_NUMBER()` `1` ist, bezieht er sich auf die ursprüngliche Instanz. Im Allgemeinen ist dies die Instanz, die Sie verwenden möchten. Dies erfolgt meist innerhalb einer Unterauswahl, bei der das Deduplizierung-Duplikate in einer höheren Ebene (`SELECT`) ausgeführt wird, wie bei einer Aggregat-Zählung.

Anwendungsfälle von Deduplizierung-Duplikaten können entweder global sein oder auf eine einzelne Benutzer- oder Endbenutzer-ID innerhalb des `identityMap` beschränkt sein.

In diesem Dokument wird erläutert, wie Deduplizierung-Duplikate in drei gängigen Anwendungsfällen durchgeführt wird: Erlebnis-Ereignis, Käufe und Metriken.

Zu jedem Deduplizierung-Duplikate gehören Scope, Window-Key, ein Überblick über die SQL-Abfrage.

## Experience Ereignisses {#experience-events}

Bei Duplikat Experience Ereignisses sollten Sie die gesamte Zeile ignorieren.

>[!CAUTION]
>
>Für viele Datensätze in [!DNL Experience Platform], einschließlich der vom Adobe Analytics Data Connector erstellten, wurde bereits ein Deduplizierung-Duplikate auf Erlebnis-Ereignis-Ebene angewendet. Daher ist eine erneute Anwendung dieser Deduplizierung-Duplikate-Ebene nicht erforderlich und wird Ihre Abfrage verlangsamen.
>
>Es ist wichtig, die Quelle Ihrer Datensätze zu verstehen und zu wissen, ob Deduplizierung-Duplikate auf Erlebnis-Ereignis-Ebene bereits angewendet wurde. Bei allen Streaming-Datensätzen (z. B. von Adobe Target) müssen Sie **ein Deduplizierung-Duplikate auf Erlebnis-Ereignis-Ebene anwenden, da diese Datenquellen &quot;mindestens einmal&quot;Semantik haben.**

**Bereich:** Global

**Fensterschlüssel:** `id`

### Deduplizierung-Duplikate-Beispiel

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

Wenn Sie Duplikat-Käufe haben, möchten Sie wahrscheinlich den Großteil der Experience Ereignis-Zeile behalten, jedoch die mit dem Kauf verknüpften Felder ignorieren (z. B. die Metrik `commerce.orders`). Käufe enthalten ein spezielles Feld für die Kauf-ID, das `commerce.order.purchaseID` lautet.

**Bereich:** Besucher

**Window key:** identityMap[$NAMENSRAUM].id &amp; commerce.order.purchaseID

### Deduplizierung-Duplikate-Beispiel

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

### Vollständiges Beispiel

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

Wenn Sie eine Metrik verwenden, die die optionale eindeutige ID verwendet, und ein Duplikat dieser ID angezeigt wird, sollten Sie diesen Metrikwert ignorieren und den Rest des Experience Ereignisses beibehalten.

In XDM verwenden fast alle Metriken den Datentyp `Measure`, der ein optionales Feld `id` enthält, das Sie zum Deduplizierung-Duplikate verwenden können.

**Bereich:** Besucher

**Window key:** identityMap[$NAMENSRAUM].id &amp; id of Measurement-Objekt

### Deduplizierung-Duplikate-Beispiel

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

In diesem Dokument werden die Ausführung von Data Deduplizierung-Duplikate im Abfrage Service sowie Beispiele für das Data Deduplizierung-Duplikate beschrieben. Weitere Best Practices beim Schreiben von Abfragen mit dem Abfrage Service finden Sie im Handbuch [Abfragen schreiben](./writing-queries.md).
