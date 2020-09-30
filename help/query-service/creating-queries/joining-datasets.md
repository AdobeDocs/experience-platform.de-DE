---
keywords: Experience Platform;home;popular topics;query service;Query service;joining datasets;joining dataset;
solution: Experience Platform
title: Datensätze verknüpfen
topic: queries
type: Tutorial
description: Durch Verknüpfung von Datensätzen können Sie Daten aus anderen Datensätzen in Ihre Abfrage aufnehmen. In diesem Beispiel wird ein benutzerdefinierter Betriebssystemdataset verwendet, um die operationSystemID dem Wert des Betriebssystems zuzuordnen.
translation-type: tm+mt
source-git-commit: 37356db1666b0c800119b1e254940ad72550848a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 80%

---


# Datensätze verknüpfen

Durch Verknüpfung von Datensätzen können Sie Daten aus anderen Datensätzen in Ihre Abfrage aufnehmen. In diesem Beispiel wird ein benutzerdefinierter Betriebssystemdatensatz verwendet, um die `operatingsystemID` dem Wert `operatingsystem` zuzuordnen.

Datensätze:
- your_analytics_table
- custom_operating_system_lookup

Erstellen Sie eine `SELECT`-Anweisung für die 50 wichtigsten Betriebssysteme nach Anzahl der Seitenansichten.

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= ('2018-01-01') AND TIMESTAMP <= ('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

![Bild](../images/queries/joining-datasets/select-operating-systems.png)