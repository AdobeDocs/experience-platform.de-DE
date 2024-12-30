---
keywords: Experience Platform;Startseite;beliebte Themen;query service;Abfrage-Service;Power BI;power bi;Verbindung mit Abfrage-Service;
solution: Experience Platform
title: Verbinden von Power BI mit dem Abfrage-Service
description: In diesem Dokument werden die Schritte zum Verbinden von Power BI mit Abfrage-Service von Adobe Experience Platform beschrieben.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 2b76b99d1e22d75faf8d758edd6cf08acdec7c21
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 96%

---

# Verbinden von [!DNL Power BI] mit dem Abfrage-Service

In diesem Dokument werden die Schritte zum Verbinden von [!DNL Power BI] Desktop mit dem Abfrage-Service von Adobe Experience Platform beschrieben.

## Erste Schritte

Für dieses Handbuch müssen Sie bereits Zugriff auf die [!DNL Power BI] Desktop-App haben und mit dem Navigieren in der zugehörigen Benutzeroberfläche vertraut sein. Informationen zum Herunterladen von [!DNL Power BI] Desktop oder weitere Details finden Sie in der [offiziellen [!DNL Power BI] -Dokumentation](https://docs.microsoft.com/de-de/power-bi/).

>[!IMPORTANT]
>
> Die [!DNL Power BI] Desktop-Anwendung ist **nur** auf Windows-Geräten verfügbar.

Um die erforderlichen Anmeldedaten zum Verbinden von [!DNL Power BI] mit Experience Platform zu erhalten, benötigen Sie Zugriff auf den Arbeitsbereich „Abfragen“ in der Platform-Benutzeroberfläche. Bitte wenden Sie sich an die Administratorin oder den Administrator Ihrer Organisation, wenn Sie derzeit keinen Zugriff auf den Arbeitsbereich „Abfragen“ haben.

## Verbinden von [!DNL Power BI] mit dem Abfrage-Service {#connect-power-bi}

Um [!DNL Power BI] mit dem Abfrage-Service zu verbinden, öffnen Sie [!DNL Power BI] und wählen Sie im oberen Menüband die Option **[!DNL Get Data]** aus. Geben Sie als Nächstes „[!DNL PostgreSQL]“ in der Suchleiste ein, um die Liste der Datenquellen einzugrenzen. Wählen Sie aus den angezeigten Ergebnissen die Option **[!DNL PostgreSQL database]** und dann **[!DNL Connect]** aus.

Das [!DNL PostgreSQL]-Datenbankdialogfeld wird angezeigt, über das Werte für Ihren Server und Ihre Datenbank angefordert werden. Zusätzliche Anweisungen zum [Verbinden mit einer PostgreSQL-Datenbank über Power Query Desktop](https://learn.microsoft.com/de-de/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) finden Sie in der offiziellen [!DNL PowerBI]-Dokumentation.

Diese erforderlichen Werte werden aus Ihren Adobe Experience Platform-Anmeldedaten übernommen. Um Ihre Anmeldedaten zu finden, melden Sie sich bei der Platform-Benutzeroberfläche an und wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Abfragen]** und dann **[!UICONTROL Anmeldedaten]** aus. Weiterführende Informationen dazu, wie Sie Datenbanknamen, Hosts, Ports und Anmeldedaten finden können, stehen im [Handbuch zu Anmeldedaten](../ui/credentials.md).

>[!IMPORTANT]
>
>Als Power BI- oder Tableau-Anwender können Sie Customer Journey Analytics über die Registerkarte Anmeldeinformationen des Abfrage-Service mit Ihren BI-Tools verbinden. Anleitungen zum Verbinden (Verbinden [ BI-Tools mit dem Customer Journey Analytics) finden Sie in der Dokumentation ](../ui/credentials.md#connect-to-customer-journey-analytics) Anmeldedaten .

![Der Experience Platform-Arbeitsbereich „Abfragen“, auf dem die Registerkarte „Anmeldedaten“ und Anmeldedaten mit ihrem Ablaufdatum hervorgehoben sind.](../images/clients/power-bi/query-service-credentials-page.png)

Geben Sie in das Feld **[!DNL Server]** des Dialogfelds [!DNL PostgreSQL database] den Wert für den Host ein, der im Abschnitt [!UICONTROL Anmeldedaten] für den Abfrage-Service zu finden ist. Für die Produktion fügen Sie Port `:80` dem Ende der Host-Zeichenfolge hinzu. Beispiel: `made-up.platform-query.adobe.io:80`.

Das Feld **[!DNL Database]** kann entweder auf „alle“ oder einen Datensatz-Tabellennamen lauten. Beispiel: `prod:all`.

>[!IMPORTANT]
>
>Verschachtelte Datenstrukturen in BI-Tools von Drittanbietern können vereinfacht werden, um ihre Benutzerfreundlichkeit zu verbessern und den erforderlichen Arbeitsaufwand beim Abrufen, Analysieren, Transformieren und Berichten von Daten zu reduzieren. Anweisungen zum Aktivieren dieser Einstellung beim Herstellen einer Verbindung zu einer Datenbank finden Sie in der Dokumentation zur Funktion [`FLATTEN`](../key-concepts/flatten-nested-data.md).

### Datenkonnektivitätsmodus {#data-connectivity-mode}

Als Nächstes können Sie Ihren **[!DNL Data Connectivity mode]** auswählen. Wählen Sie im Dialogfeld [!DNL PostgreSQL database] die Option **[!DNL Import]** und dann **[!DNL OK]** aus, um eine Liste aller verfügbaren Tabellen anzuzeigen, oder wählen Sie **[!DNL DirectQuery]** aus, um die Datenquelle direkt abzufragen, ohne Daten direkt nach [!DNL Power BI] zu importieren oder zu kopieren.

Weitere Informationen zum **[!DNL Import]**-Modus finden Sie im Abschnitt zum [Importieren von Tabellen](#import). Weitere Informationen zum **[!DNL DirectQuery]**-Modus finden Sie im Abschnitt zum [Abfragen eines Datensatzes ohne Datenimport](#direct-query).

Wählen Sie nach Bestätigung Ihrer Datenbankdetails **[!DNL OK]** aus.

### Authentifizierung {#authentication}

Nachdem Sie den Datenkonnektivitätsmodus bestätigt haben, wird eine Eingabeaufforderung angezeigt, in der Sie nach Ihrem Benutzernamen, Kennwort und den Anwendungseinstellungen gefragt werden. Der Benutzername in diesem Fall ist Ihre Organisations-ID und das Kennwort Ihr Authentifizierungs-Token. Beide Informationen finden Sie auf der Seite mit den Anmeldedaten des Abfrage-Service.

Füllen Sie diese Details aus und wählen Sie dann **[!DNL Connect]** aus, um mit dem nächsten Schritt fortzufahren.

## Importieren einer Tabelle {#import}

Durch Auswahl von **[!DNL Import]** [!DNL Data Connectivity mode] wird der vollständige Datensatz importiert, sodass Sie die ausgewählten Tabellen und Spalten in der [!DNL Power BI] Desktop-Anwendung wie vorliegend nutzen können.

>[!IMPORTANT]
>
>Um Datenänderungen zu sehen, die seit dem ersten Import aufgetreten sind, müssen Sie die Daten in [!DNL Power BI] aktualisieren, indem Sie den vollständigen Datensatz erneut importieren.

Um eine Tabelle zu importieren, geben Sie die Server- und Datenbankdetails [wie oben beschrieben](#connect-power-bi) ein und wählen Sie **[!DNL Import]** [!DNL Data Connectivity mode] und dann **[!DNL OK]** aus. Das Dialogfeld [!DNL Navigator] wird mit einer Liste aller verfügbaren Tabellen angezeigt. Wählen Sie die Tabelle aus, deren Vorschau Sie anzeigen möchten, und dann **[!DNL Load]**, um den Datensatz in Power BI zu importieren. Die Tabelle wird jetzt in [!DNL Power BI] importiert.

[Allgemeine Informationen zum Verbinden mit Daten in der PowerBi Desktop](https://learn.microsoft.com/de-de/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data)-App finden Sie in der offiziellen Dokumentation.

### Importieren von Tabellen mit benutzerdefinierten SQL-Abfragen

[!DNL Power BI] und andere Drittanbieter-Tools wie [!DNL Tableau] erlauben es Benutzenden derzeit nicht, verschachtelte Objekte wie XDM-Objekte in Platform zu importieren. Deshalb ermöglicht Ihnen [!DNL Power BI] die Verwendung von benutzerdefinierten SQL-Abfragen, um auf diese verschachtelten Felder zuzugreifen und eine reduzierte Ansicht der Daten zu erstellen. [!DNL Power BI] lädt dann diese reduzierte Ansicht der zuvor verschachtelten Daten als normale Tabelle.

Wählen Sie im Dialogfeld [!DNL PostgreSQL database] die Option **[!DNL Advanced options]** aus, um eine benutzerdefinierte SQL-Abfrage im Abschnitt **[!DNL SQL statement]** einzugeben. Diese benutzerdefinierte Abfrage sollte verwendet werden, um Ihre JSON-Name-Wert-Paare in ein Tabellenformat zu reduzieren. Die offizielle Dokumentation enthält auch Informationen zum [Verbinden von PowerBI mit einer SQL-Anweisung in den erweiterten Optionen](https://learn.microsoft.com/de-de/power-query/connectors/postgresql#connect-using-advanced-options).

Nachdem Sie Ihre benutzerdefinierte Abfrage eingegeben haben, wählen Sie **[!DNL OK]** aus, um mit der Verbindung Ihrer Datenbank fortzufahren. Anleitungen zum Verbinden einer Datenbank aus diesem Teil des Workflows finden Sie weiter oben im Abschnitt [Authentifizierung](#authentication).

Nach Abschluss der Authentifizierung wird eine Vorschau der reduzierten Daten im [!DNL Power BI] Desktop-Dashboard als Tabelle angezeigt. Der Server- und Datenbankname werden oben im Dialogfeld aufgeführt. Wählen Sie **[!DNL Load]** aus, um den Importvorgang abzuschließen.

Die Visualisierungen können jetzt über die [!DNL Power BI] Desktop-App bearbeitet und exportiert werden.

## Abfragen von Datensätzen ohne Datenimport {#direct-query}

Der **[!DNL DirectQuery]** [!DNL Data Connectivity mode] fragt die Datenquelle direkt ab, ohne Daten nach [!DNL Power BI] Desktop zu importieren oder zu kopieren. Mit diesem Verbindungsmodus können Sie alle Visualisierungen mit aktuellen Daten über die Benutzeroberfläche aktualisieren. Die zum Erstellen oder Aktualisieren der Visualisierung erforderliche Zeit hängt jedoch von der Performance der zugrunde liegenden Datenquelle ab.

Weitere Informationen über [die Verwendung von [!DNL DirectQuery]](https://learn.microsoft.com/de-de/power-bi/connect-data/desktop-use-directquery) sowie eine umfassende Erörterung der zugehörigen [Konnektivitätsoptionen, Anwendungsfälle und Einschränkungen](https://learn.microsoft.com/de-de/power-bi/connect-data/desktop-directquery-about) finden Sie in der offiziellen [!DNL PowerBI]-Dokumentation.

Um diesen [!DNL Data Connectivity mode] zu verwenden, wählen Sie den **[!DNL DirectQuery]**-Umschalter und dann **[!DNL Advanced options]** aus, um eine benutzerdefinierte SQL-Abfrage im Abschnitt **[!DNL SQL statement]** einzugeben. Stellen Sie sicher, dass **[!DNL Include relationship columns]** ausgewählt ist. Nachdem Sie die Abfrage abgeschlossen haben, wählen Sie **[!DNL OK]** aus, um fortzufahren.

Eine Vorschau Ihrer Abfrage wird angezeigt. Wählen Sie **[!DNL Load]** aus, um die Ergebnisse der Abfrage anzuzeigen.

## Nächste Schritte

Durch Lesen dieses Dokuments sollten Sie jetzt verstehen, wie Sie eine Verbindung zur [!DNL Power BI] Desktop-App und zu den verschiedenen verfügbaren Datenverbindungsmodi herstellen können. Weiterführende Informationen zum Schreiben und Ausführen von Abfragen finden Sie in der [Anleitung zur Ausführung von Abfragen](../best-practices/writing-queries.md).
