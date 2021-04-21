---
keywords: Experience Platform;Home;beliebte Themen;Abfrage-Dienst;Abfrage-Dienst;RStudio;Studio;Verbindung mit Abfrage-Dienst;
solution: Experience Platform
title: Verbinden von RStudio mit dem Abfrage-Dienst
topic-legacy: connect
description: In diesem Dokument werden die Schritte zum Verbinden von R Studio mit Adobe Experience Platform Query Service beschrieben.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 18%

---

# Verbinden Sie [!DNL RStudio] mit dem Abfrage-Dienst

Dieses Dokument führt Sie durch die Schritte zum Verbinden von [!DNL RStudio] mit Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Dieses Handbuch setzt voraus, dass Sie bereits Zugriff auf [!DNL RStudio] haben und mit dessen Verwendung vertraut sind. Weitere Informationen zu [!DNL RStudio] finden Sie in der [offiziellen  [!DNL RStudio] Dokumentation](https://rstudio.com/products/rstudio/).
> 
> Außerdem müssen Sie den PostgreSQL JDBC 4.2-Treiber installieren, um RStudio mit Abfrage Service zu verwenden. Sie können den JDBC-Treiber von der [offiziellen PostgreSQL-Site](https://jdbc.postgresql.org/download.html) herunterladen.

## [!DNL Query Service]-Verbindung in der [!DNL RStudio]-Schnittstelle erstellen

Nach der Installation von [!DNL RStudio] müssen Sie das RJDBC-Paket installieren. Wechseln Sie zum Bereich **[!DNL Packages]** und wählen Sie **[!DNL Install]**.

![](../images/clients/rstudio/install-package.png)

Es wird ein Popup mit dem Bildschirm **[!DNL Install Packages]** angezeigt. Stellen Sie sicher, dass **[!DNL Repository (CRAN)]** für den Abschnitt **[!DNL Install from]** ausgewählt ist. Der Wert für **[!DNL Packages]** sollte `RJDBC` sein. Stellen Sie sicher, dass **[!DNL Install dependencies]** ausgewählt ist. Nachdem Sie bestätigt haben, dass alle Werte korrekt sind, wählen Sie **[!DNL Install]** aus, um die Pakete zu installieren.

![](../images/clients/rstudio/install-jrdbc.png)

Nachdem das RJDBC-Paket installiert wurde, starten Sie RStudio neu, um den Installationsprozess abzuschließen.

Nach dem Neustart von RStudio können Sie nun eine Verbindung zum Abfrage Service herstellen. Wählen Sie im Bereich **[!DNL Packages]** das **[!DNL RJDBC]**-Paket aus und geben Sie den folgenden Befehl in die Konsole ein:

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Dabei stellt {PATH TO THE POSTGRESQL JDBC JAR} den Pfad zur PostgreSQL JDBC JAR dar, die auf Ihrem Computer installiert wurde.

Sie können jetzt Ihre Verbindung mit dem Abfrage Service herstellen, indem Sie den folgenden Befehl in der Konsole eingeben:

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!NOTE]
>
> Weiterführende Informationen zum Finden Ihres Datenbanknamens, Hosts, Ports und Ihrer Anmeldedaten finden Sie auf der Seite [Anmeldedaten in Platform](https://platform.adobe.com/query/configuration). Melden Sie sich zur Suche nach Ihren Anmeldeinformationen bei [!DNL Platform] an, wählen Sie **[!UICONTROL Abfragen]** und anschließend **[!UICONTROL Anmeldeinformationen]**.

![](../images/clients/rstudio/connection-rjdbc.png)

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
