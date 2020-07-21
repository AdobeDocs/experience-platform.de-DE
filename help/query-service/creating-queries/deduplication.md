---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Data Deduplizierung-Duplikate
topic: queries
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---


# Data Deduplizierung-Duplikate in [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] unterstützt Data Deduplizierung-Duplikate, wenn möglicherweise eine ganze Zeile aus einer Berechnung entfernt oder ein bestimmter Feldsatz ignoriert werden muss, da nur ein Teil der Daten in der Zeile ein Duplikat ist. Das gängige Deduplizierung-Duplikate besteht darin, die `ROW_NUMBER()` Funktion über ein Fenster hinweg für eine ID oder mehrere IDs über einen bestimmten Zeitraum hinweg (unter Verwendung des [!DNL Experience Data Model] (XDM-) `timestamp` Felds) zu verwenden, um ein neues Feld zurückzugeben, das die Anzahl der erkannten Duplikat angibt. Ist dieser Wert `1`der Wert, bezieht sich dies auf die ursprüngliche Instanz und in den meisten Fällen auf die Instanz, die Sie verwenden möchten, wobei jede andere Instanz ignoriert wird. Dies erfolgt meist innerhalb einer Unterauswahl, bei der das Deduplizierung-Duplikate in einer höheren Ebene wie der Durchführung einer Aggregat-Anzahl durchgeführt wird. `SELECT`

## Anwendungsbeispiele

Einige Anwendungsfälle für Deduplizierung-Duplikate sind im gesamten Datumsbereich global und einige sind auf eine einzige Besucher- oder Endbenutzer-ID innerhalb der `identityMap`beschränkt.

In diesem Dokument werden Beispiele für die Unterauswahl und die vollständige Abfrage von Beispielen für die Deduplizierung von drei gängigen Anwendungsfällen erläutert:
- [ExperienceEvents](#experienceevents)
- [Käufe](#purchases)
- [Metriken](#metrics)

### ExperienceEvents {#experienceevents}

Bei Duplikat ExperienceEvents sollten Sie die gesamte Zeile ignorieren.

>[!CAUTION]
>
>Für viele DataSets in [!DNL Experience Platform], einschließlich der vom Adobe Analytics Data Connector erstellten, wurde bereits ein Deduplizierung-Duplikate auf ExperienceEvent-Ebene angewendet. Daher ist eine erneute Anwendung dieser Deduplizierung-Duplikate-Ebene nicht erforderlich und wird Ihre Abfrage verlangsamen. Es ist wichtig, die Quelle Ihrer DataSets zu verstehen und zu wissen, ob Deduplizierung-Duplikate auf ExperienceEvent-Ebene bereits angewendet wurde. Für alle Streaming-DataSets (z. B. solche aus Adobe Target) müssen Sie Deduplizierung-Duplikate auf ExperienceEvent-Ebene anwenden, da diese Datenquellen eine Semantik von &quot;mindestens einmal&quot;aufweisen.

**Anwendungsbereich:** Global

**Fensterschlüssel:** id

#### Unterauswahl

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

#### Vollständiges Beispiel

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

### Käufe {#purchases}

Wenn Sie Duplikat-Käufe haben, möchten Sie wahrscheinlich den Großteil der ExperienceEvent-Zeile behalten, jedoch die mit dem Kauf verknüpften Felder (z. B. die `commerce.orders` Metrik) ignorieren. Für Käufe gibt es ein spezielles Feld für die Kauf-ID. Dieses Feld ist `commerce.order.purchaseID`vorhanden.

**Anwendungsbereich:** Besucher

**Fensterschlüssel:** identityMap[$NAMENSRAUM].id &amp; commerce.order.purchaseID

#### Unterauswahl

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

#### Vollständiges Beispiel

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

### Metriken {#metrics}

Wenn Sie eine Metrik verwenden, die die optionale eindeutige ID verwendet, und ein Duplikat dieser ID angezeigt wird, sollten Sie diesen Metrikwert ignorieren und den Rest des ExperienceEvent beibehalten. In XDM verwenden fast alle Metriken den `Measure` Datentyp, der ein optionales `id` Feld enthält, das Sie zum Deduplizierung-Duplikate verwenden können.

**Anwendungsbereich:** Besucher

**Fensterschlüssel:** identityMap[$NAMENSRAUM].id &amp; id des Measure-Objekts

#### Unterauswahl

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

#### Vollständiges Beispiel

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
