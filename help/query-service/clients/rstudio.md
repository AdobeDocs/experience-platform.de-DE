---
keywords: Experience Platform;Home;beliebte Themen;Abfrage-Dienst;Abfrage-Dienst;RStudio;Studio;Verbindung mit Abfrage-Dienst;
solution: Experience Platform
title: Verbinden von RStudio mit dem Abfrage-Dienst
topic: connect
description: In diesem Dokument werden die Schritte zum Verbinden von R Studio mit Adobe Experience Platform Query Service beschrieben.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 36%

---


# Verbinden Sie [!DNL RStudio] mit dem Abfrage-Dienst

Dieses Dokument führt Sie durch die Schritte zum Verbinden von [!DNL RStudio] mit Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Dieses Handbuch setzt voraus, dass Sie bereits Zugriff auf [!DNL RStudio] haben und mit dessen Verwendung vertraut sind. Weitere Informationen zu [!DNL RStudio] finden Sie in der [offiziellen  [!DNL RStudio] Dokumentation](https://rstudio.com/products/rstudio/).

## [!DNL Query Service]-Verbindung in der [!DNL RStudio]-Schnittstelle erstellen

Nach der Installation von [!DNL RStudio] müssen Sie auf dem Bildschirm **[!DNL Console]**, der angezeigt wird, zunächst Ihr R-Skript für die Verwendung von [!DNL PostgreSQL] vorbereiten.

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
> Weiterführende Informationen zum Finden Ihres Datenbanknamens, Hosts, Ports und Ihrer Anmeldedaten finden Sie auf der Seite [Anmeldedaten in Platform](https://platform.adobe.com/query/configuration). Melden Sie sich zur Suche nach Ihren Anmeldeinformationen bei [!DNL Platform] an, wählen Sie **[!UICONTROL Abfragen]** und anschließend **[!UICONTROL Anmeldeinformationen]**.

## Schreiben von Abfragen

Nachdem Sie eine Verbindung zu [!DNL Query Service] hergestellt haben, können Sie Abfragen schreiben, um SQL-Anweisungen auszuführen und zu bearbeiten. Beispielsweise können Sie `dbGetQuery(con, sql)` zum Durchführen von Abfragen verwenden, bei denen `sql` die SQL-Abfrage ist, die Sie ausführen möchten.

Die folgende Abfrage verwendet einen Datensatz, der [Erlebnis-Ereignis](../best-practices/experience-event-queries.md) enthält, und erstellt ein Histogramm der Ansichten einer Website, je nach Bildschirmhöhe des Geräts.

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

## Nächste Schritte

Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Leitfaden zu [laufenden Abfragen](../best-practices/writing-queries.md).