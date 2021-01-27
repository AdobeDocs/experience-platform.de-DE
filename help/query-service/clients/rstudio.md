---
keywords: Experience Platform;home;popular topics;Query service;query service;RStudio;rstudio;connect to query service;
solution: Experience Platform
title: Mit RStudio verbinden
topic: connect
description: In diesem Dokument werden die Schritte zum Verbinden von R Studio mit Adobe Experience Platform Query Service beschrieben.
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 64%

---


# Verbinden mit [!DNL RStudio]

Dieses Dokument führt Sie durch die Schritte zum Verbinden von R Studio mit Adobe Experience Platform [!DNL Query Service].

Nach der Installation von [!DNL RStudio] müssen Sie zunächst auf dem Bildschirm *Console* Ihren R-Skript für die Verwendung von [!DNL PostgreSQL] vorbereiten.

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

Nachdem Sie Ihr R-Skript für die Verwendung von [!DNL PostgreSQL] vorbereitet haben, können Sie [!DNL RStudio] jetzt [!DNL Query Service] durch Laden des [!DNL PostgreSQL]-Treibers verbinden.

```r
drv <- dbDriver("PostgreSQL")
con <- dbConnect(drv, 
 dbname = "{DATABASE_NAME}",
 host="{HOST_NUMBER}",
 port={PORT_NUMBER},
 user="{USERNAME}",
 password="{PASSWORD}")
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{DATABASE_NAME}` | Der Name der zu verwendenden Datenbank. |
| `{HOST_NUMBER` und `{PORT_NUMBER}` | Der Host-Endpunkt und sein Port für Query Service. |
| `{USERNAME}` und `{PASSWORD}` | Die Anmeldedaten, die verwendet werden sollen. Der Benutzername hat die Form `ORG_ID@AdobeOrg`. |

>[!NOTE]
>
> Weiterführende Informationen zum Finden Ihres Datenbanknamens, Hosts, Ports und Ihrer Anmeldedaten finden Sie auf der Seite [Anmeldedaten in Platform](https://platform.adobe.com/query/configuration). Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei [!DNL Platform] an, klicken Sie auf **[!UICONTROL Abfragen]** und dann auf **[!UICONTROL Anmeldeinformationen]**.

## Nächste Schritte

Nachdem Sie eine Verbindung zu [!DNL Query Service] hergestellt haben, können Sie Abfragen schreiben, um SQL-Anweisungen auszuführen und zu bearbeiten. Beispielsweise können Sie `dbGetQuery(con, sql)` zum Durchführen von Abfragen verwenden, bei denen `sql` die SQL-Abfrage ist, die Sie ausführen möchten.

Folgende Abfrage nutzt einen Datensatz, der [ExperienceEvents](../best-practices/experience-event-queries.md) enthält, und erstellt ein Histogramm mit Seitenansichten einer Website, je nach Bildschirmhöhe des jeweiligen Geräts.

```sql
df_pageviews <- dbGetQuery(con,
"SELECT t.range AS buckets, 
 Count(*) AS pageviews 
FROM (SELECT CASE 
 WHEN device.screenheight BETWEEN 0 AND 99 THEN '0 - 99' 
 WHEN device.screenheight BETWEEN 100 AND 199 THEN '100-199' 
 WHEN device.screenheight BETWEEN 200 AND 299 THEN '200-299' 
 WHEN device.screenheight BETWEEN 300 AND 399 THEN '300-399' 
 WHEN device.screenheight BETWEEN 400 AND 499 THEN '400-499' 
 WHEN device.screenheight BETWEEN 500 AND 599 THEN '500-599' 
 ELSE '600-699' 
 end AS range 
 FROM aa_post_vals_3) t 
GROUP BY t.range 
ORDER BY buckets 
LIMIT 1000000")
```

Eine erfolgreiche Antwort gibt die Ergebnisse der Abfrage zurück:

```r
df_pageviews
 buckets pageviews
1 0 - 99 198985
2 500-599 67138
3 300-399 2147
4 200-299 354
5 400-499 6947
6 100-199 4415
7 600-699 3097040
```

Weiterführende Informationen zum Verfassen und Ausführen von Abfragen finden Sie im [Handbuch zum Ausführen von Abfragen](../best-practices/writing-queries.md).