---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Power BI; Power BI; Verbindung mit Query Service
solution: Experience Platform
title: Power BI zu Query Service verbinden
description: In diesem Dokument werden die Schritte zum Verbinden von Power BI mit Adobe Experience Platform Query Service erläutert.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 1%

---

# Verbinden [!DNL Power BI] zu Query Service

In diesem Dokument werden die Schritte zum Verbinden von [!DNL Power BI] Desktop mit Adobe Experience Platform Query Service.

## Erste Schritte

Für dieses Handbuch benötigen Sie bereits Zugriff auf [!DNL Power BI] -Desktop-Programm verwenden und mit dem Navigieren in der -Benutzeroberfläche vertraut sind. Zum Herunterladen [!DNL Power BI] Desktop oder weitere Informationen finden Sie unter [offiziell [!DNL Power BI] Dokumentation](https://docs.microsoft.com/de-de/power-bi/).

>[!IMPORTANT]
>
> Die [!DNL Power BI] Desktop-Programm **only** auf Windows-Geräten verfügbar.

So erwerben Sie die erforderlichen Anmeldeinformationen zum Herstellen einer Verbindung [!DNL Power BI] zur Experience Platform benötigen Sie Zugriff auf den Arbeitsbereich Abfragen in der Platform-Benutzeroberfläche. Wenden Sie sich an Ihren IMS-Organisationsadministrator, wenn Sie derzeit keinen Zugriff auf den Arbeitsbereich &quot;Abfragen&quot;haben.

Nach der Installation [!DNL Power BI], müssen Sie `Npgsql`, ein .NET-Treiberpaket für PostgreSQL. Weitere Informationen zu Npgsql finden Sie im [Npgsql-Dokumentation](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Sie müssen Version 4.0.10 oder niedriger herunterladen, da neuere Versionen zu Fehlern führen.

Unter &quot;[!DNL Npgsql GAC Installation]&quot;Wählen Sie im Bildschirm für die benutzerdefinierte Einrichtung die Option **[!DNL Will be installed on local hard drive]**.

Um sicherzustellen, dass Npgsql ordnungsgemäß installiert wurde, starten Sie den Computer neu, bevor Sie mit den nächsten Schritten fortfahren.

## Verbinden [!DNL Power BI] zu Query Service {#connect-power-bi}

Verbindung herstellen [!DNL Power BI] zu Query Service, öffnen Sie [!DNL Power BI] und wählen Sie **[!DNL Get Data]** im oberen Menüband.

![Die [!DNL Power BI] Registerkarte &quot;Dashboard-Startseite&quot;mit hervorgehobenen Daten abrufen.](../images/clients/power-bi/open-power-bi.png)

Eingabe &quot;[!DNL PostgreSQL]&quot; in der Suchleiste, um die Liste der Datenquellen einzuschränken. Wählen Sie unter den angezeigten Ergebnissen die Option **[!DNL PostgreSQL database]**, gefolgt von **[!DNL Connect]**.

![Dialogfeld &quot;Daten abrufen&quot;mit [!DNL PostgreSQL] Datenbank und Verbindung hervorgehoben.](../images/clients/power-bi/get-data.png)

Die [!DNL PostgreSQL] Datenbankdialogfeld angezeigt, in dem Werte für Ihren Server und Ihre Datenbank angefordert werden. Diese Werte werden aus Ihren Adobe Experience Platform-Anmeldedaten übernommen. Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei der Platform-Benutzeroberfläche an und wählen Sie **[!UICONTROL Abfragen]** aus der linken Navigation, gefolgt von **[!UICONTROL Anmeldeinformationen]**. Weitere Informationen zum Auffinden Ihres Datenbanknamens, Hosts, Ports und Ihrer Anmeldedaten finden Sie in der [Handbuch zu Anmeldeinformationen](../ui/credentials.md).

![Der Arbeitsbereich &quot;Experience Platform Queries&quot;mit den Registerkarten &quot;Anmeldeinformationen&quot;und &quot;Ablaufberechtigungen&quot;wurde hervorgehoben.](../images/clients/power-bi/query-service-credentials-page.png)

Für **[!DNL Server]** Geben Sie in Power BI den Wert für den Host im Abschnitt Query Service-Anmeldedaten ein. Für die Produktion fügen Sie Port hinzu `:80` an das Ende der Host-Zeichenfolge. Beispiel: `made-up.platform-query.adobe.io:80`.

Die **[!DNL Database]** -Feld kann entweder &quot;all&quot;oder ein Datensatz-Tabellenname sein. Beispiel: `prod:all`.

>[!IMPORTANT]
>
>Verschachtelte Datenstrukturen in BI-Tools von Drittanbietern können reduziert werden, um ihre Benutzerfreundlichkeit zu verbessern und den erforderlichen Arbeitsaufwand zum Abrufen, Analysieren, Transformieren und Berichten von Daten zu reduzieren. Weitere Informationen finden Sie in der Dokumentation unter[`FLATTEN` Funktion](../best-practices/flatten-nested-data.md) Anweisungen zum Aktivieren dieser Einstellung beim Herstellen einer Verbindung zu einer Datenbank.

![Die [!DNL Power BI] Dashboard mit markierten Eingabe-Feldern für Server und Datenbank.](../images/clients/power-bi/postgresql-database-dialog.png)

### Data Connectivity-Modus

Als Nächstes können Sie Ihre **[!DNL Data Connectivity mode]**. Auswählen **[!DNL Import]** gefolgt von **[!DNL OK]** , um eine Liste aller verfügbaren Tabellen anzuzeigen, oder wählen Sie **[!DNL DirectQuery]** , um die Datenquelle direkt abzufragen, ohne Daten direkt in zu importieren oder zu kopieren [!DNL Power BI].

Weitere Informationen finden Sie unter **[!DNL Import]** -Modus, lesen Sie bitte den Abschnitt unter [Tabellen importieren](#import). Weitere Informationen finden Sie unter **[!DNL DirectQuery]** -Modus, lesen Sie bitte den Abschnitt unter [Datensatz ohne Datenimport abfragen](#direct-query).

Auswählen **[!DNL OK]** nach Bestätigung Ihrer Datenbankdetails.

![Die [!DNL PostgreSQL] Datenbankdialogfeld mit hervorgehobenem Data Connectivity-Modus.](../images/clients/power-bi/connectivity-mode.png)

### Authentifizierung

Eine Eingabeaufforderung mit der Aufforderung, Ihren Benutzernamen, Ihr Kennwort und Ihre Anwendungseinstellungen anzufordern, wird angezeigt. Der Benutzername in diesem Fall ist Ihre Organisations-ID und das Kennwort Ihr Authentifizierungstoken. Beide finden Sie auf der Seite mit den Anmeldedaten für Query Service .

Füllen Sie diese Details aus und wählen Sie dann **[!DNL Connect]** , um mit dem nächsten Schritt fortzufahren.

![Das Datenbankdialogfeld mit dem Dropdown-Menü Benutzername, Kennwort und Anwendungseinstellungen wurde hervorgehoben.](../images/clients/power-bi/import-mode.png)

## Importieren einer Tabelle {#import}

Durch Auswahl der **[!DNL Import]** [!DNL Data Connectivity mode], wird der vollständige Datensatz importiert, sodass Sie die ausgewählten Tabellen und Spalten im [!DNL Power BI] Desktop-Applikation unverändert.

>[!IMPORTANT]
>
>Um Datenänderungen zu sehen, die seit dem ersten Import aufgetreten sind, müssen Sie die Daten in [!DNL Power BI] , indem Sie den vollständigen Datensatz erneut importieren.

Um eine Tabelle zu importieren, geben Sie die Server- und Datenbankdetails ein [wie oben beschrieben](#connect-power-bi) und wählen Sie die **[!DNL Import]** [!DNL Data Connectivity mode], gefolgt von **[!DNL OK]**. Ein Dialogfeld mit einer Liste aller verfügbaren Tabellen wird angezeigt. Wählen Sie die Tabelle aus, deren Vorschau Sie anzeigen möchten, gefolgt von **[!DNL Load]** , um den Datensatz in den Power BI zu bringen.

![Das Dialogfeld Navigator mit einer Tabelle und hervorgehobenem Ladevorgang.](../images/clients/power-bi/preview-table.png)

Die Tabelle wird jetzt in [!DNL Power BI].

![Die [!DNL Power BI] Dashboard mit Anweisungen zum Erstellen benutzerdefinierter Visualisierungen hervorgehoben.](../images/clients/power-bi/import-table.png)

### Importieren von Tabellen mit benutzerdefiniertem SQL

[!DNL Power BI] und anderen Drittanbieter-Tools wie Tableau erlauben es Benutzern derzeit nicht, verschachtelte Objekte wie XDM-Objekte in Platform zu importieren. Um dies zu berücksichtigen, [!DNL Power BI] ermöglicht Ihnen die Verwendung von benutzerdefiniertem SQL, um auf diese verschachtelten Felder zuzugreifen und eine reduzierte Ansicht der Daten zu erstellen. [!DNL Power BI] lädt dann diese reduzierte Ansicht der zuvor verschachtelten Daten als normale Tabelle.

Aus dem [!DNL PostgreSQL] Datenbank-Popover, auswählen **[!DNL Advanced options]** , um eine benutzerdefinierte SQL-Abfrage in die **[!DNL SQL statement]** Abschnitt. Diese benutzerdefinierte Abfrage sollte verwendet werden, um Ihre JSON-Name-Wert-Paare in ein Tabellenformat zu reduzieren.

![Die [!DNL PostgreSQL] Datenbankdialogfeld mit den erweiterten Optionen für den Datenkonnektivitätsmodus hervorgehoben. Diese ermöglichen die Erstellung einer benutzerdefinierten SQL-Anweisung.](../images/clients/power-bi/custom-sql-statement.png)

Nachdem Sie Ihre benutzerdefinierte Abfrage eingegeben haben, wählen Sie **[!DNL OK]** , um mit der Verbindung Ihrer Datenbank fortzufahren. Siehe [Authentifizierung](#authentication) weiter oben für Anleitungen zum Verbinden einer Datenbank aus diesem Teil des Workflows.

Nach Abschluss der Authentifizierung wird eine Vorschau der reduzierten Daten im [!DNL Power BI] Desktop-Dashboard als Tabelle. Der Server- und Datenbankname werden oben im Dialogfeld aufgeführt. Auswählen **[!DNL Load]** , um den Importvorgang abzuschließen.

![Eine Visualisierung einer reduzierten, importierten Tabelle im [!DNL Power BI] Dashboard.](../images/clients/power-bi/imported-table-preview.png)

Die Visualisierungen können jetzt über das [!DNL Power BI] Desktop-Programm.

## Datensatz ohne Datenimport abfragen {#direct-query}

Die **[!DNL DirectQuery]** [!DNL Data Connectivity mode] fragt die Datenquelle direkt ab, ohne Daten in die [!DNL Power BI] Desktop. Mit diesem Verbindungsmodus können Sie alle Visualisierungen mit aktuellen Daten über die Benutzeroberfläche aktualisieren. Die zum Erstellen oder Aktualisieren der Visualisierung erforderliche Zeit hängt jedoch von der Leistung der zugrunde liegenden Datenquelle ab.

So verwenden Sie [!DNL Data Connectivity mode], wählen Sie die **[!DNL DirectQuery]** umschalten **[!DNL Advanced options]** , um eine benutzerdefinierte SQL-Abfrage in die **[!DNL SQL statement]** Abschnitt. Stellen Sie sicher, dass **[!DNL Include relationship columns]** ausgewählt ist. Nachdem Sie die Abfrage abgeschlossen haben, wählen Sie **[!DNL OK]** , um fortzufahren.

![Die [!DNL PostgreSQL] Datenbankdialogfeld mit den Einstellungen, die für die Verwendung des Data Connectivity-Modus erforderlich sind, hervorgehoben.](../images/clients/power-bi/direct-query-mode.png)

Eine Vorschau Ihrer Abfrage wird angezeigt. Auswählen **[!DNL Load]** um die Ergebnisse der Abfrage anzuzeigen.

![Eine Vorschau der tabellarischen Ergebnisse aus der Beispielabfrage.](../images/clients/power-bi/preview-direct-query.png)

## Nächste Schritte

Durch Lesen dieses Dokuments sollten Sie jetzt verstehen, wie Sie eine Verbindung zum [!DNL Power BI] Desktop-Programm und die verschiedenen verfügbaren Datenverbindungsmodi. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Abschnitt [Anleitung zur Ausführung von Abfragen](../best-practices/writing-queries.md).
