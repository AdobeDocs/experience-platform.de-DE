---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zusammenfügen von Datensätzen
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 3%

---


# Zusammenfügen von Datensätzen

Durch die Verknüpfung von Datensätzen können Sie Daten aus anderen Datensätzen in Ihre Abfrage aufnehmen. In diesem Beispiel wird ein benutzerdefinierter Betriebssystemdataset verwendet, um den Wert `operatingsystemID` dem `operatingsystem` Wert zuzuordnen.

Datensätze:
- your_analytics_table
- custom_operating_system_lookup

Erstellen Sie eine `SELECT` Anweisung für die 50 wichtigsten Betriebssysteme nach Anzahl der Ansichten.

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