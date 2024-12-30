---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;RStudio;rstudio;mit Abfrage-Service verbinden;
solution: Experience Platform
title: RStudio mit dem Abfrage-Service verbinden
description: In diesem Dokument werden die Schritte zum Verbinden von R Studio mit Adobe Experience Platform Query Service beschrieben.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 11%

---

# Verbinden von [!DNL RStudio] mit dem Abfrage-Service

In diesem Dokument werden die Schritte zum Verbinden von [!DNL RStudio] mit Adobe Experience Platform [!DNL Query Service] erläutert.

>[!NOTE]
>
> [!DNL RStudio] wurde jetzt in [!DNL Posit] umbenannt. [!DNL RStudio] Produkte wurden in [!DNL Posit Connect], [!DNL Posit Workbench], [!DNL Posit Package] Manager, [!DNL Posit Cloud] und [!DNL Posit Academy] umbenannt.
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL RStudio] haben und mit dessen Verwendung vertraut sind. Weitere Informationen zu [!DNL RStudio] finden Sie in der [offiziellen [!DNL RStudio] Dokumentation](https://rstudio.com/products/rstudio/).
> 
> Um [!DNL RStudio] mit dem Abfrage-Service verwenden zu können, müssen Sie außerdem den [!DNL PostgreSQL] JDBC 4.2-Treiber installieren. Sie können den JDBC-Treiber von der [[!DNL PostgreSQL] offiziellen Website) ](https://jdbc.postgresql.org/download/).

## Erstellen einer [!DNL Query Service] Verbindung in der [!DNL RStudio]

Nach der Installation von [!DNL RStudio] müssen Sie das RJDBC-Paket installieren. Eine Anleitung zum &quot;[ einer Datenbank über die Befehlszeile](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r) finden Sie in der offiziellen POSIT-Dokumentation.

Wenn Sie ein Mac-Betriebssystem verwenden, können Sie **[!UICONTROL Tools]** in der Menüleiste und anschließend **[!UICONTROL Pakete installieren]** aus dem Dropdown-Menü auswählen. Wählen Sie alternativ die Registerkarte **[!DNL Packages]** in der RStudio-Benutzeroberfläche aus und klicken Sie auf **[!DNL Install]**.

Ein Popup-Fenster mit dem **[!DNL Install Packages]** wird angezeigt. Stellen Sie sicher, dass **[!DNL Repository (CRAN)]** für den Abschnitt **[!DNL Install from]** ausgewählt ist. Der Wert für **[!DNL Packages]** sollte `RJDBC` sein. Stellen Sie sicher, dass **[!DNL Install dependencies]** ausgewählt ist. Nachdem Sie bestätigt haben, dass alle Werte korrekt sind, wählen Sie **[!DNL Install]** aus, um die Pakete zu installieren. Nachdem das RJDBC-Paket installiert wurde, starten Sie [!DNL RStudio] neu, um den Installationsprozess abzuschließen.

Nachdem [!DNL RStudio] neu gestartet wurde, können Sie jetzt eine Verbindung zum Abfrage-Service herstellen. Wählen Sie das **[!DNL RJDBC]** im Bereich **[!DNL Packages]** aus und geben Sie den folgenden Befehl in die Konsole ein:

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Dabei entspricht `{PATH TO THE POSTGRESQL JDBC JAR}` dem Pfad zur [!DNL PostgreSQL] JDBC-JAR-Datei, die auf Ihrem Computer installiert wurde.

Jetzt können Sie Ihre Verbindung zum Abfrage-Service erstellen. Geben Sie den folgenden Befehl in die Konsole ein:

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>In der [[!DNL Query Service] SSL-](./ssl-modes.md) erfahren Sie mehr über die SSL-Unterstützung für Drittanbieterverbindungen zum Abfrage-Service von Adobe Experience Platform und darüber, wie Sie eine Verbindung mit `verify-full` SSL-Modus herstellen.

Weiterführende Informationen dazu, wie Sie Datenbanknamen, Hosts, Ports und Anmeldeinformationen finden können, finden Sie im [ zu Anmeldeinformationen ](../ui/credentials.md). Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei [!DNL Platform] an und wählen Sie **[!UICONTROL Abfragen]** gefolgt von **[!UICONTROL Anmeldeinformationen]**.

Eine Meldung in der Konsolenausgabe bestätigt die Verbindung zum Abfrage-Service.

## Schreiben von Abfragen

Nachdem Sie nun eine Verbindung zu [!DNL Query Service] hergestellt haben, können Sie Abfragen schreiben, um SQL-Anweisungen auszuführen und zu bearbeiten. Beispielsweise können Sie `dbGetQuery(con, sql)` zum Durchführen von Abfragen verwenden, bei denen `sql` die SQL-Abfrage ist, die Sie ausführen möchten.

Die folgende Abfrage verwendet einen Datensatz mit [Erlebnisereignissen](../../xdm/classes/experienceevent.md) und erstellt ein Histogramm der Seitenansichten einer Website basierend auf der Bildschirmhöhe des Geräts.

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

Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Handbuch unter [Ausführen von Abfragen](../best-practices/writing-queries.md).
