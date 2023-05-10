---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; Query Service; RStudio; Studio; Verbindung mit Query Service;
solution: Experience Platform
title: RStudio mit Query Service verbinden
description: In diesem Dokument werden die Schritte zum Verbinden von R Studio mit Adobe Experience Platform Query Service beschrieben.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 15%

---

# Verbinden von [!DNL RStudio] mit dem Abfrage-Service

In diesem Dokument werden die Schritte zum Verbinden von [!DNL RStudio] mit Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> [!DNL RStudio] wurde jetzt umbenannt als [!DNL Posit]. [!DNL RStudio] -Produkte wurden in [!DNL Posit Connect], [!DNL Posit Workbench], [!DNL Posit Package] Manager, [!DNL Posit Cloud]und [!DNL Posit Academy].
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL RStudio] und sind mit der Verwendung vertraut. Weitere Informationen [!DNL RStudio] finden Sie im Abschnitt [offiziell [!DNL RStudio] Dokumentation](https://rstudio.com/products/rstudio/).
> 
> Zusätzlich zur Verwendung von [!DNL RStudio] Mit Query Service müssen Sie die [!DNL PostgreSQL] JDBC 4.2-Treiber. Sie können den JDBC-Treiber von der [[!DNL PostgreSQL] offizielle Site](https://jdbc.postgresql.org/download/).

## Erstellen Sie eine [!DNL Query Service] Verbindung in [!DNL RStudio] Benutzeroberfläche

Nach der Installation [!DNL RStudio]müssen Sie das RJDBC-Paket installieren. Anleitung zum [Datenbank über die Befehlszeile verbinden](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r) finden Sie in der offiziellen Posit-Dokumentation.

Bei Verwendung von Mac OS können Sie **[!UICONTROL Instrumente]** aus der Menüleiste, gefolgt von **[!UICONTROL Pakete installieren]** aus dem Dropdown-Menü aus. Alternativ können Sie die **[!DNL Packages]** in der RStudio-Benutzeroberfläche ein und wählen Sie **[!DNL Install]**.

Ein Popup wird angezeigt, in dem die **[!DNL Install Packages]** angezeigt. Stellen Sie sicher, dass **[!DNL Repository (CRAN)]** für die **[!DNL Install from]** Abschnitt. Der Wert für **[!DNL Packages]** sollte `RJDBC`. Sichern **[!DNL Install dependencies]** ausgewählt ist. Nachdem Sie bestätigt haben, dass alle Werte korrekt sind, wählen Sie **[!DNL Install]** um die Pakete zu installieren. Nachdem das RJDBC-Paket installiert wurde, starten Sie es neu. [!DNL RStudio] , um den Installationsprozess abzuschließen.

Nachher [!DNL RStudio] neu gestartet wurde, können Sie jetzt eine Verbindung zu Query Service herstellen. Wählen Sie die **[!DNL RJDBC]** -Paket im **[!DNL Packages]** und geben Sie den folgenden Befehl in die Konsole ein:

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Wo `{PATH TO THE POSTGRESQL JDBC JAR}` stellt den Pfad zum [!DNL PostgreSQL] JDBC JAR, das auf Ihrem Computer installiert wurde.

Jetzt können Sie Ihre Verbindung zu Query Service erstellen. Geben Sie den folgenden Befehl in die Konsole ein:

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>Siehe [[!DNL Query Service] SSL-Dokumentation](./ssl-modes.md) Erfahren Sie mehr über die SSL-Unterstützung für Drittanbieterverbindungen zu Adobe Experience Platform Query Service und über die Verbindung mit `verify-full` SSL-Modus.

Weiterführende Informationen dazu, wie Sie Datenbanknamen, Hosts, Ports und Anmeldeinformationen finden können, stehen im [Handbuch zu Anmeldeinformationen](../ui/credentials.md). Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei [!DNL Platform], wählen Sie **[!UICONTROL Abfragen]**, gefolgt von **[!UICONTROL Anmeldeinformationen]**.

Eine Meldung in der Konsolenausgabe bestätigt die Verbindung zu Query Service.

## Schreiben von Abfragen

Nachdem Sie sich mit [!DNL Query Service], können Sie Abfragen schreiben, um SQL-Anweisungen auszuführen und zu bearbeiten. Beispielsweise können Sie `dbGetQuery(con, sql)` zum Durchführen von Abfragen verwenden, bei denen `sql` die SQL-Abfrage ist, die Sie ausführen möchten.

Die folgende Abfrage verwendet einen Datensatz mit [Erlebnisereignisse](../../xdm/classes/experienceevent.md) und erstellt ein Histogramm mit Seitenansichten einer Website, je nach Bildschirmhöhe des Geräts.

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
