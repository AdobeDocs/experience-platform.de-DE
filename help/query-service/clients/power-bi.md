---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Power BI; Power BI; Verbindung mit Query Service
solution: Experience Platform
title: Power BI zu Query Service verbinden
topic-legacy: connect
description: In diesem Dokument werden die Schritte zum Verbinden von Power BI mit Adobe Experience Platform Query Service erläutert.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 2109abd02b9c6c321c21a8fe3826509d22b1c2e2
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 6%

---

# Verbinden von [!DNL Power BI] mit Query Service (PC)

In diesem Dokument werden die Schritte zum Verbinden von Power BI mit Adobe Experience Platform Query Service beschrieben.

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL Power BI] haben und mit der Navigation in der Benutzeroberfläche vertraut sind. Weitere Informationen zu [!DNL Power BI] finden Sie in der [offiziellen [!DNL Power BI] Dokumentation](https://docs.microsoft.com/de-de/power-bi/).
>
> Außerdem ist der Power BI **nur** auf Windows-Geräten verfügbar.

Nach der Installation von Power BI müssen Sie `Npgsql` installieren, ein .NET-Treiberpaket für PostgreSQL. Weitere Informationen zu Npgsql finden Sie in der [Npgsql-Dokumentation](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Sie müssen Version 4.0.10 oder niedriger herunterladen, da neuere Versionen zu Fehlern führen.

Wählen Sie unter &quot;[!DNL Npgsql GAC Installation]&quot;auf dem benutzerdefinierten Setup-Bildschirm **[!DNL Will be installed on local hard drive]** aus.

Um sicherzustellen, dass npgsql ordnungsgemäß installiert ist, starten Sie den Computer neu, bevor Sie mit den nächsten Schritten fortfahren.

## Verbinden Sie [!DNL Power BI] mit [!DNL Query Service]

Um [!DNL Power BI] mit [!DNL Query Service] zu verbinden, öffnen Sie [!DNL Power BI] und wählen Sie **[!DNL Get Data]** im oberen Menüband aus.

![](../images/clients/power-bi/open-power-bi.png)

Wählen Sie **[!DNL PostgreSQL database]**, gefolgt von **[!DNL Connect]**.

![](../images/clients/power-bi/get-data.png)

Sie können jetzt Werte für den Server und die Datenbank eingeben.  Weiterführende Informationen zum Finden Ihres Datenbanknamens, Hosts, Ports und Ihrer Anmeldedaten finden Sie auf der Seite [Anmeldedaten in Platform](https://platform.adobe.com/query/configuration). Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei [!DNL Platform] an, wählen Sie **[!UICONTROL Abfragen]**, gefolgt von **[!UICONTROL Anmeldeinformationen]**.

**[!DNL Server]** ist der Host, der unter den Verbindungsdetails gefunden wird. Fügen Sie für die Produktion Port `:80` am Ende der Host-Zeichenfolge hinzu. **[!DNL Database]** kann entweder &quot;all&quot;oder ein Datensatztabellenname sein.

Zusätzlich können Sie **[!DNL Data Connectivity mode]** auswählen. Wählen Sie **[!DNL Import]** aus, um eine Liste aller verfügbaren Tabellen anzuzeigen, oder wählen Sie **[!DNL DirectQuery]** aus, um direkt eine Abfrage zu erstellen.

Weitere Informationen zum Modus **[!DNL Import]** finden Sie im Abschnitt [Vorschau und Import einer Tabelle](#preview). Weitere Informationen zum Modus **[!DNL DirectQuery]** finden Sie im Abschnitt [Erstellen von SQL-Anweisungen](#create). Wählen Sie **[!DNL OK]** aus, nachdem Sie Ihre Datenbankdetails bestätigt haben.

![](../images/clients/power-bi/connectivity-mode.png)

Eine Eingabeaufforderung mit der Aufforderung, Ihren Benutzernamen, Ihr Kennwort und Ihre Anwendungseinstellungen anzufordern, wird angezeigt. Füllen Sie diese Details aus und wählen Sie dann **[!DNL Connect]** aus, um mit dem nächsten Schritt fortzufahren.

![](../images/clients/power-bi/import-mode.png)

## Vorschau erstellen und Tabelle importieren {#preview}

Wenn Sie den Modus **[!DNL Import]** ausgewählt haben, wird ein Dialogfeld mit einer Liste aller verfügbaren Tabellen angezeigt. Wählen Sie die Tabelle aus, die Sie in der Vorschau anzeigen möchten, gefolgt von **[!DNL Load]**, um den Datensatz in [!DNL Power BI] zu bringen.

![](../images/clients/power-bi/preview-table.png)

Der Tisch ist jetzt in den Power BI importiert.

![](../images/clients/power-bi/import-table.png)

## SQL-Anweisungen erstellen {#create}

Wenn Sie den Modus **[!DNL DirectQuery]** ausgewählt haben, müssen Sie den Abschnitt Erweiterte Optionen mit der SQL-Abfrage ausfüllen, die Sie erstellen möchten.

Fügen Sie unter **[!DNL SQL statement]** die SQL-Abfrage ein, die Sie erstellen möchten. Stellen Sie sicher, dass das Kontrollkästchen **[!DNL Include relationship columns]** aktiviert ist. Nachdem Sie Ihre Abfrage geschrieben haben, wählen Sie **[!DNL OK]** aus, um fortzufahren.

![](../images/clients/power-bi/direct-query-mode.png)

Eine Vorschau Ihrer Abfrage wird angezeigt. Wählen Sie **[!DNL Load]** aus, um die Ergebnisse der Abfrage anzuzeigen.

![](../images/clients/power-bi/preview-direct-query.png)

## Nächste Schritte

Nachdem Sie sich mit [!DNL Query Service] angemeldet haben, können Sie [!DNL Power BI] verwenden, um Abfragen zu schreiben. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Handbuch zu [laufenden Abfragen](../best-practices/writing-queries.md).
