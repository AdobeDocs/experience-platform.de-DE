---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; Query Service; postico; Postico; Verbindung mit Query Service
solution: Experience Platform
title: Verbindung mit Query Service
topic-legacy: connect
description: Dieses Dokument enthält den Link zur Installation des Backup-Clients Postico für Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 7%

---

# Verbinden von [!DNL Postico] mit Query Service (Mac)

In diesem Dokument werden die Schritte zum Verbinden von [!DNL Postico] mit Adobe Experience Platform [!DNL Query Service] beschrieben.

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL Postico] haben und mit der Navigation in der Benutzeroberfläche vertraut sind. Weitere Informationen zu [!DNL Postico] finden Sie in der [offiziellen [!DNL Postico] Dokumentation](https://eggerapps.at/postico/docs).
> 
> Außerdem ist [!DNL Postico] **nur** auf macOS-Geräten verfügbar.

Um [!DNL Postico] mit Query Service zu verbinden, öffnen Sie [!DNL Postico] und wählen Sie **[!DNL New Favorite]** aus.

![](../images/clients/postico/open-postico.png)

Sie können jetzt Werte eingeben, um eine Verbindung mit Adobe Experience Platform herzustellen.

Weitere Informationen zum Auffinden Ihrer Datenbanknamen, Host-, Port- und Anmeldedaten finden Sie im Handbuch [Anmeldeinformationen](../ui/credentials.md). Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei [!DNL Platform] an, wählen Sie **[!UICONTROL Abfragen]**, gefolgt von **[!UICONTROL Anmeldeinformationen]**.

Nachdem Sie Ihre Anmeldedaten eingefügt haben, wählen Sie **[!DNL Connect]** aus, um eine Verbindung mit Query Service herzustellen.

![](../images/clients/postico/authentication-details.png)

Nach der Verbindung mit Platform können Sie eine Liste aller zuvor mit Query Service vorgenommenen Relationen anzeigen.

![](../images/clients/postico/show-queries.png)

## SQL-Anweisungen erstellen

Um eine neue SQL-Abfrage zu erstellen, wählen Sie &quot;SQL-Abfrage&quot;aus und öffnen Sie sie.

![](../images/clients/postico/create-query.png)

Es wird ein Feld angezeigt, in das Sie die auszuführende Abfrage eingeben können. Wenn Sie fertig sind, wählen Sie **[!DNL Execute Statement]** aus, um die Abfrage auszuführen.

![](../images/clients/postico/run-statement.png)

Es wird eine Tabelle mit den Ergebnissen Ihrer abgeschlossenen Abfrage-Ausführung angezeigt.

![](../images/clients/postico/query-results.png)

## Nächste Schritte

Nachdem Sie sich mit [!DNL Query Service] angemeldet haben, können Sie [!DNL Postico] verwenden, um Abfragen zu schreiben. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
