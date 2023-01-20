---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Power BI; Power BI; Verbindung mit Query Service
solution: Experience Platform
title: Power BI zu Query Service verbinden
description: In diesem Dokument werden die Schritte zum Verbinden von Power BI mit Adobe Experience Platform Query Service erläutert.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 1%

---

# Verbinden [!DNL Power BI] zu Query Service

In diesem Dokument werden die Schritte zum Verbinden von [!DNL Power BI] Desktop mit Adobe Experience Platform Query Service.

## Erste Schritte

Für dieses Handbuch benötigen Sie bereits Zugriff auf [!DNL Power BI] -Desktop-Programm verwenden und mit dem Navigieren in der -Benutzeroberfläche vertraut sind. Zum Herunterladen [!DNL Power BI] Desktop oder weitere Informationen finden Sie unter [offiziell [!DNL Power BI] Dokumentation](https://docs.microsoft.com/de-de/power-bi/).

>[!IMPORTANT]
>
> Die [!DNL Power BI] Desktop-Programm **only** auf Windows-Geräten verfügbar.

So erwerben Sie die erforderlichen Anmeldeinformationen zum Herstellen einer Verbindung [!DNL Power BI] zur Experience Platform benötigen Sie Zugriff auf den Arbeitsbereich Abfragen in der Platform-Benutzeroberfläche. Wenden Sie sich an Ihren Organisationsadministrator, wenn Sie derzeit keinen Zugriff auf den Arbeitsbereich &quot;Abfragen&quot;haben.

Nach der Installation [!DNL Power BI], müssen Sie `Npgsql`, ein .NET-Treiberpaket für PostgreSQL. Weitere Informationen zu Npgsql finden Sie im [Npgsql-Dokumentation](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Sie müssen Version 4.0.10 oder niedriger herunterladen, da neuere Versionen zu Fehlern führen.

Unter &quot;[!DNL Npgsql GAC Installation]&quot;Wählen Sie im Bildschirm für die benutzerdefinierte Einrichtung die Option **[!DNL Will be installed on local hard drive]**.

Um sicherzustellen, dass Npgsql ordnungsgemäß installiert wurde, starten Sie den Computer neu, bevor Sie mit den nächsten Schritten fortfahren.

## Verbinden [!DNL Power BI] zu Query Service {#connect-power-bi}

Verbindung herstellen [!DNL Power BI] zu Query Service, öffnen Sie [!DNL Power BI] und wählen Sie **[!DNL Get Data]** im oberen Menüband. Geben Sie als Nächstes &quot;[!DNL PostgreSQL]&quot; in der Suchleiste, um die Liste der Datenquellen einzuschränken. Wählen Sie aus den angezeigten Ergebnissen die Option **[!DNL PostgreSQL database]**, gefolgt von **[!DNL Connect]**.

Die [!DNL PostgreSQL] Datenbankdialogfeld angezeigt, in dem Werte für Ihren Server und Ihre Datenbank angefordert werden. Zusätzliche Anweisungen zum [Verbindung zu einer PostgreSQL-Datenbank über Power Query Desktop herstellen](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) ist im Offiziellen Dokument [!DNL PowerBI] Dokumentation.

Diese erforderlichen Werte werden aus Ihren Adobe Experience Platform-Anmeldedaten übernommen. Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei der Platform-Benutzeroberfläche an und wählen Sie **[!UICONTROL Abfragen]** aus der linken Navigation, gefolgt von **[!UICONTROL Anmeldeinformationen]**. Weitere Informationen zum Auffinden Ihres Datenbanknamens, Hosts, Ports und Ihrer Anmeldedaten finden Sie in der [Handbuch zu Anmeldeinformationen](../ui/credentials.md).

![Der Arbeitsbereich &quot;Experience Platform Queries&quot;mit den Registerkarten &quot;Anmeldeinformationen&quot;und &quot;Ablaufberechtigungen&quot;wurde hervorgehoben.](../images/clients/power-bi/query-service-credentials-page.png)

Im **[!DNL Server]** des [!DNL PostgreSQL database] eingeben, geben Sie den Wert für den Host ein, der in Query Service gefunden wird. [!UICONTROL Anmeldeinformationen] Abschnitt. Für die Produktion fügen Sie Port hinzu `:80` an das Ende der Host-Zeichenfolge. Beispiel: `made-up.platform-query.adobe.io:80`.

Die **[!DNL Database]** -Feld kann entweder &quot;all&quot;oder ein Datensatz-Tabellenname sein. Beispiel: `prod:all`.

>[!IMPORTANT]
>
>Verschachtelte Datenstrukturen in BI-Tools von Drittanbietern können reduziert werden, um ihre Benutzerfreundlichkeit zu verbessern und den erforderlichen Arbeitsaufwand zum Abrufen, Analysieren, Transformieren und Berichten von Daten zu reduzieren. Weitere Informationen finden Sie in der Dokumentation unter[`FLATTEN` Funktion](../essential-concepts/flatten-nested-data.md) Anweisungen zum Aktivieren dieser Einstellung beim Herstellen einer Verbindung zu einer Datenbank.

### Data Connectivity-Modus {#data-connectivity-mode}

Als Nächstes können Sie Ihre **[!DNL Data Connectivity mode]**. Im [!DNL PostgreSQL database] Dialogfeld auswählen **[!DNL Import]** gefolgt von **[!DNL OK]** , um eine Liste aller verfügbaren Tabellen anzuzeigen, oder wählen Sie **[!DNL DirectQuery]** , um die Datenquelle direkt abzufragen, ohne Daten direkt in zu importieren oder zu kopieren [!DNL Power BI].

Weitere Informationen zum **[!DNL Import]** -Modus, lesen Sie bitte den Abschnitt unter [Tabellen importieren](#import). Weitere Informationen finden Sie unter **[!DNL DirectQuery]** -Modus, lesen Sie bitte den Abschnitt unter [Datensatz ohne Datenimport abfragen](#direct-query).

Auswählen **[!DNL OK]** nach Bestätigung Ihrer Datenbankdetails.

### Authentifizierung {#authentication}

Nachdem Sie den Datenkonnektivitätsmodus bestätigt haben, wird eine Eingabeaufforderung angezeigt, in der Sie nach Ihrem Benutzernamen, Kennwort und den Anwendungseinstellungen gefragt werden. Der Benutzername in diesem Fall ist Ihre Organisations-ID und das Kennwort Ihr Authentifizierungstoken. Beide finden Sie auf der Seite mit den Anmeldedaten für Query Service .

Füllen Sie diese Details aus und wählen Sie dann **[!DNL Connect]** , um mit dem nächsten Schritt fortzufahren.

## Importieren einer Tabelle {#import}

Durch Auswahl der **[!DNL Import]** [!DNL Data Connectivity mode], wird der vollständige Datensatz importiert, sodass Sie die ausgewählten Tabellen und Spalten im [!DNL Power BI] Desktop-Applikation unverändert.

>[!IMPORTANT]
>
>Um Datenänderungen zu sehen, die seit dem ersten Import aufgetreten sind, müssen Sie die Daten in [!DNL Power BI] , indem Sie den vollständigen Datensatz erneut importieren.

Um eine Tabelle zu importieren, geben Sie die Server- und Datenbankdetails ein [wie oben beschrieben](#connect-power-bi) und wählen Sie die **[!DNL Import]** [!DNL Data Connectivity mode], gefolgt von **[!DNL OK]**. Die [!DNL Navigator] angezeigt und zeigt eine Liste aller verfügbaren Tabellen an. Wählen Sie die Tabelle aus, deren Vorschau Sie anzeigen möchten, gefolgt von **[!DNL Load]** , um den Datensatz in den Power BI zu bringen. Die Tabelle wird jetzt in [!DNL Power BI].

[Allgemeine Informationen zum Herstellen einer Verbindung zu Daten auf dem PowerBi-Desktop](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) App finden Sie in der offiziellen Dokumentation.

### Importieren von Tabellen mit benutzerdefiniertem SQL

[!DNL Power BI] und anderen Drittanbieter-Tools wie [!DNL Tableau] erlauben es Benutzern derzeit nicht, verschachtelte Objekte wie XDM-Objekte in Platform zu importieren. Um dies zu berücksichtigen, [!DNL Power BI] ermöglicht Ihnen die Verwendung von benutzerdefiniertem SQL, um auf diese verschachtelten Felder zuzugreifen und eine reduzierte Ansicht der Daten zu erstellen. [!DNL Power BI] lädt dann diese reduzierte Ansicht der zuvor verschachtelten Daten als normale Tabelle.

Aus dem [!DNL PostgreSQL database] Dialogfeld auswählen **[!DNL Advanced options]** , um eine benutzerdefinierte SQL-Abfrage in die **[!DNL SQL statement]** Abschnitt. Diese benutzerdefinierte Abfrage sollte verwendet werden, um Ihre JSON-Name-Wert-Paare in ein Tabellenformat zu reduzieren. Die offizielle Dokumentation enthält auch Informationen zur [PowerBI mit einer SQL-Anweisung in den erweiterten Optionen verbinden](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options).

Nachdem Sie Ihre benutzerdefinierte Abfrage eingegeben haben, wählen Sie **[!DNL OK]** , um mit der Verbindung Ihrer Datenbank fortzufahren. Siehe [Authentifizierung](#authentication) weiter oben für Anleitungen zum Verbinden einer Datenbank aus diesem Teil des Workflows.

Nach Abschluss der Authentifizierung wird eine Vorschau der reduzierten Daten im [!DNL Power BI] Desktop-Dashboard als Tabelle. Der Server- und Datenbankname werden oben im Dialogfeld aufgeführt. Auswählen **[!DNL Load]** , um den Importvorgang abzuschließen.

Die Visualisierungen können jetzt über das [!DNL Power BI] Desktop-Programm.

## Datensatz ohne Datenimport abfragen {#direct-query}

Die **[!DNL DirectQuery]** [!DNL Data Connectivity mode] fragt die Datenquelle direkt ab, ohne Daten in die [!DNL Power BI] Desktop. Mit diesem Verbindungsmodus können Sie alle Visualisierungen mit aktuellen Daten über die Benutzeroberfläche aktualisieren. Die zum Erstellen oder Aktualisieren der Visualisierung erforderliche Zeit hängt jedoch von der Leistung der zugrunde liegenden Datenquelle ab.

Weitere Informationen über [die Verwendung [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery) sowie eine umfassende Diskussion über die [Konnektivitätsoptionen, Anwendungsfälle und Einschränkungen](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about) ist im Offiziellen Dokument [!DNL PowerBI] Dokumentation.

So verwenden Sie [!DNL Data Connectivity mode], wählen Sie die **[!DNL DirectQuery]** umschalten **[!DNL Advanced options]** , um eine benutzerdefinierte SQL-Abfrage in die **[!DNL SQL statement]** Abschnitt. Stellen Sie sicher, dass **[!DNL Include relationship columns]** ausgewählt ist. Nachdem Sie die Abfrage abgeschlossen haben, wählen Sie **[!DNL OK]** , um fortzufahren.

Eine Vorschau Ihrer Abfrage wird angezeigt. Auswählen **[!DNL Load]** um die Ergebnisse der Abfrage anzuzeigen.

## Nächste Schritte

Durch Lesen dieses Dokuments sollten Sie jetzt verstehen, wie Sie eine Verbindung zum [!DNL Power BI] Desktop-Programm und die verschiedenen verfügbaren Datenverbindungsmodi. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Abschnitt [Anleitung zur Ausführung von Abfragen](../best-practices/writing-queries.md).
