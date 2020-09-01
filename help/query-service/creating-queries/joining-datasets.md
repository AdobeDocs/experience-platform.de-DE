---
keywords: Experience Platform;home;popular topics;query service;Query service;joining datasets;joining dataset;
solution: Experience Platform
title: Datensätze verknüpfen
topic: queries
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 100%

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
WHERE _ACP_YEAR=2018 
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

![Bild](../images/queries/joining-datasets/select-operating-systems.png)