---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verbindung mit RStudio
topic: connect
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 2%

---


# Verbindung mit RStudio

In diesem Dokument werden die Schritte zum Verbinden von R Studio mit dem Adobe Experience Platform Abfrage Service beschrieben.

Nach der Installation von RStudio müssen Sie zunächst auf dem angezeigten *Konsolenbildschirm* Ihr R-Skript für die Verwendung von PostgreSQL vorbereiten.

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

Nachdem Sie Ihr R-Skript für die Verwendung von PostgreSQL vorbereitet haben, können Sie jetzt RStudio mit dem Abfrage Service verbinden, indem Sie den PostgreSQL-Treiber laden.

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
| `{HOST_NUMBER` und `{PORT_NUMBER}` | Der Host-Endpunkt und sein Anschluss für den Abfrage-Dienst. |
| `{USERNAME}` und `{PASSWORD}` | Die Anmeldeinformationen, die verwendet werden. Der Benutzername hat die Form `ORG_ID@AdobeOrg`. |

>[!NOTE] Weitere Informationen zum Auffinden der Anmeldeinformationen für Datenbankname, Host, Anschluss und Anmeldung finden Sie auf der Seite [Anmeldeinformationen auf der Plattform](https://platform.adobe.com/query/configuration). Melden Sie sich zur Suche nach Ihren Anmeldeinformationen bei Platform an, klicken Sie auf **Abfragen** und dann auf **Anmeldeinformationen**.

## Nächste Schritte

Nachdem Sie nun eine Verbindung zum Abfrage Service hergestellt haben, können Sie Abfragen schreiben, um SQL-Anweisungen auszuführen und zu bearbeiten. Beispielsweise können Sie Abfragen `dbGetQuery(con, sql)` ausführen, bei denen die SQL-Abfrage ausgeführt werden `sql` soll.

Die folgende Abfrage verwendet einen Datensatz, der [ExperienceEvents](../creating-queries/experience-event-queries.md) enthält, und erstellt ein Histogramm der Ansichten einer Website, je nach Bildschirmhöhe des Geräts.

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

Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Handbuch [laufender Abfragen](../creating-queries/creating-queries.md).