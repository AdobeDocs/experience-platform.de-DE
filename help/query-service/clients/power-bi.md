---
keywords: Experience Platform;Home;beliebte Themen;Abfrage-Dienst;Abfrage-Dienst;Power BI;Power-bi;Verbindung zum Abfrage-Dienst herstellen
solution: Experience Platform
title: Power BI mit dem Abfrage-Dienst verbinden
topic-legacy: connect
description: Dieses Dokument führt Sie durch die Schritte, um Power BI mit dem Adobe Experience Platform Abfrage Service zu verbinden.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 5%

---

# Verbinden Sie [!DNL Power BI] mit dem Abfrage Service (PC)

In diesem Dokument werden die Schritte zur Verbindung von Power BI mit dem Adobe Experience Platform Abfrage Service beschrieben.

>[!NOTE]
>
> Dieses Handbuch setzt voraus, dass Sie bereits Zugriff auf [!DNL Power BI] haben und mit der Navigation in der Oberfläche vertraut sind. Weitere Informationen zu [!DNL Power BI] finden Sie in der [offiziellen  [!DNL Power BI] Dokumentation](https://docs.looker.com/).
>
> Zusätzlich ist Power BI **nur** auf Windows-Geräten verfügbar.

Nach der Installation von Power BI müssen Sie `Npgsql`, ein .NET-Treiberpaket für PostgreSQL, installieren. Weitere Informationen zu Npgsql finden Sie in der [Npgsql Dokumentation](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Sie müssen Version 4.0.10 oder niedriger herunterladen, da neuere Versionen zu Fehlern führen.

Wählen Sie im benutzerdefinierten Setup-Bildschirm unter &quot;[!DNL Npgsql GAC Installation]&quot;**[!DNL Will be installed on local hard drive]**.

Um sicherzustellen, dass npgsql ordnungsgemäß installiert wurde, starten Sie den Computer neu, bevor Sie mit den nächsten Schritten fortfahren.

## Verbinden Sie [!DNL Power BI] mit [!DNL Query Service]

Um [!DNL Power BI] mit [!DNL Query Service] zu verbinden, öffnen Sie [!DNL Power BI] und wählen Sie **[!DNL Get Data]** in der oberen Menüleiste aus.

![](../images/clients/power-bi/open-power-bi.png)

Wählen Sie **[!DNL PostgreSQL database]**, gefolgt von **[!DNL Connect]**.

![](../images/clients/power-bi/get-data.png)

Sie können jetzt Werte für den Server und die Datenbank eingeben.  Weiterführende Informationen zum Finden Ihres Datenbanknamens, Hosts, Ports und Ihrer Anmeldedaten finden Sie auf der Seite [Anmeldedaten in Platform](https://platform.adobe.com/query/configuration). Melden Sie sich zur Suche nach Ihren Anmeldeinformationen bei [!DNL Platform] an, wählen Sie **[!UICONTROL Abfragen]** und anschließend **[!UICONTROL Anmeldeinformationen]**.

**[!DNL Server]** ist der Host, der unter den Verbindungsdetails gefunden wird. Bei der Produktion fügen Sie Anschluss `:80` am Ende der Hostzeichenfolge hinzu. **[!DNL Database]** kann entweder &quot;all&quot;oder ein Dataset-Tabellenname sein.

Zusätzlich können Sie **[!DNL Data Connectivity mode]** auswählen. Wählen Sie **[!DNL Import]** aus, um eine Liste aller verfügbaren Tabellen anzuzeigen, oder wählen Sie **[!DNL DirectQuery]**, um eine Abfrage direkt zu erstellen.

Weitere Informationen zum **[!DNL Import]**-Modus finden Sie im Abschnitt [Anzeigen einer Vorschau und Importieren einer Tabelle](#preview). Weitere Informationen zum **[!DNL DirectQuery]**-Modus finden Sie im Abschnitt [SQL-Anweisungen erstellen](#create). Wählen Sie **[!DNL OK]** aus, nachdem Sie die Datenbankdetails bestätigt haben.

![](../images/clients/power-bi/connectivity-mode.png)

Es wird eine Eingabeaufforderung zum Benutzernamen, Kennwort und Anwendungseinstellungen angezeigt. Füllen Sie diese Details aus und wählen Sie dann **[!DNL Connect]** aus, um mit dem nächsten Schritt fortzufahren.

![](../images/clients/power-bi/import-mode.png)

## Vorschau und Importieren einer Tabelle {#preview}

Wenn Sie den Modus **[!DNL Import]** ausgewählt haben, wird ein Dialogfeld mit einer Liste aller verfügbaren Tabellen angezeigt. Wählen Sie die zu Vorschau Tabelle aus, gefolgt von **[!DNL Load]**, um den Datensatz in [!DNL Power BI] zu laden.

![](../images/clients/power-bi/preview-table.png)

Die Tabelle wird jetzt in den Power BI importiert.

![](../images/clients/power-bi/import-table.png)

## SQL-Anweisungen {#create} erstellen

Wenn Sie den Modus **[!DNL DirectQuery]** ausgewählt haben, müssen Sie den Abschnitt Erweiterte Optionen mit der SQL-Abfrage ausfüllen, die Sie erstellen möchten.

Fügen Sie unter **[!DNL SQL statement]** die SQL-Abfrage ein, die Sie erstellen möchten. Stellen Sie sicher, dass das Kontrollkästchen **[!DNL Include relationship columns]** aktiviert ist. Nachdem Sie Ihre Abfrage geschrieben haben, wählen Sie **[!DNL OK]** aus, um fortzufahren.

![](../images/clients/power-bi/direct-query-mode.png)

Eine Vorschau Ihrer Abfrage wird angezeigt. Wählen Sie **[!DNL Load]** aus, um die Ergebnisse der Abfrage anzuzeigen.

![](../images/clients/power-bi/preview-direct-query.png)

## Nächste Schritte

Nachdem Sie eine Verbindung mit [!DNL Query Service] hergestellt haben, können Sie [!DNL Power BI] verwenden, um Abfragen zu schreiben. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Leitfaden zu [laufenden Abfragen](../best-practices/writing-queries.md).
