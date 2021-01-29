---
keywords: Experience Platform;home;popular topics;tableau;Tableau;query service;Query service;connect to query service;
solution: Experience Platform
title: Verbinden mit Tableau
topic: connect
description: Dieses Dokument führt Sie durch die Schritte, um Tableau mit dem Adobe Experience Platform Abfrage Service zu verbinden.
translation-type: tm+mt
source-git-commit: eac93f3465fa6ce4af7a6aa783cf5f8fb4ac9b9b
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 14%

---


# [!DNL Tableau]

Dieses Dokument beschreibt die Schritte zum Verbinden von Tableau mit Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Dieses Handbuch setzt voraus, dass Sie bereits Zugriff auf [!DNL Tableau] haben und mit der Navigation in der Oberfläche vertraut sind. Weitere Informationen zu [!DNL Tableau] finden Sie in der [offiziellen  [!DNL Tableau] Dokumentation](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

## [!DNL Tableau] mit Plattform verbinden

Um [!DNL Tableau] mit [!DNL Query Service] zu verbinden, öffnen Sie [!DNL Tableau] und wählen Sie im Abschnitt **[!DNL To a Server]** **[!DNL More]**, gefolgt von **[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

Sie können jetzt Werte eingeben, um eine Verbindung mit Adobe Experience Platform herzustellen.  Weiterführende Informationen zum Finden Ihres Datenbanknamens, Hosts, Ports und Ihrer Anmeldedaten finden Sie auf der Seite [Anmeldedaten in Platform](https://platform.adobe.com/query/configuration). Melden Sie sich zur Suche nach Ihren Anmeldeinformationen bei [!DNL Platform] an, wählen Sie **[!UICONTROL Abfragen]** und anschließend **[!UICONTROL Anmeldeinformationen]**.

Vergewissern Sie sich, dass Sie das Feld **[!UICONTROL SSL Erforderlich]** markiert haben, bevor Sie versuchen, eine Verbindung herzustellen.

Nachdem Sie alle Ihre Anmeldedaten eingegeben haben, wählen Sie **[!DNL Sign In]** aus, um fortzufahren.

![](../images/clients/tableau/sign-in.png)

Sie haben jetzt eine Verbindung zu Adobe Experience Platform hergestellt, wobei eine Liste der Tabellen auf der Seite angezeigt wird.

![](../images/clients/tableau/connected.png)

## Nächste Schritte

Nachdem Sie eine Verbindung mit [!DNL Query Service] hergestellt haben, können Sie [!DNL Tableau] verwenden, um Abfragen zu schreiben. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Leitfaden zu [laufenden Abfragen](../best-practices/writing-queries.md).