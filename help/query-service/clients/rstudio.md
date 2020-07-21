---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mit RStudio verbinden
topic: connect
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 61%

---


# Connect with [!DNL RStudio]

This document walks through the steps for connecting R Studio with Adobe Experience Platform [!DNL Query Service].

After installing [!DNL RStudio], on the *Console* screen that appears, you will first need to prepare your R script to use [!DNL PostgreSQL].

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

Once you have prepared your R script to use [!DNL PostgreSQL], you can now connect [!DNL RStudio] to [!DNL Query Service] by loading the [!DNL PostgreSQL] driver.

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
>Weiterführende Informationen zum Finden Ihres Datenbanknamens, Hosts, Ports und Ihrer Anmeldedaten finden Sie auf der Seite [Anmeldedaten in Platform](https://platform.adobe.com/query/configuration). To find your credentials, log in to [!DNL Platform], click **[!UICONTROL Queries]**, then click **[!UICONTROL Credentials]**.

## Nächste Schritte

Now that you have connected to [!DNL Query Service], you can write queries to execute and edit SQL statements. Beispielsweise können Sie `dbGetQuery(con, sql)` zum Durchführen von Abfragen verwenden, bei denen `sql` die SQL-Abfrage ist, die Sie ausführen möchten.

Folgende Abfrage nutzt einen Datensatz, der [ExperienceEvents](../creating-queries/experience-event-queries.md) enthält, und erstellt ein Histogramm mit Seitenansichten einer Website, je nach Bildschirmhöhe des jeweiligen Geräts.

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

Weiterführende Informationen zum Verfassen und Ausführen von Abfragen finden Sie im [Handbuch zum Ausführen von Abfragen](../creating-queries/creating-queries.md).