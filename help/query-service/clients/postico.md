---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;postico;Postico;Verbindung mit Abfrage-Service;
solution: Experience Platform
title: Verbinden von Postico mit dem Abfrage-Service
description: Dieses Dokument enthält den Link zur Installation des Backup-Clients Postico für den Abfrage-Service von Adobe Experience Platform.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 4%

---

# Verbinden von [!DNL Postico] mit dem Abfrage-Service (Mac)

In diesem Dokument werden die Schritte zum Verbinden von [!DNL Postico] mit Adobe Experience Platform [!DNL Query Service] beschrieben.

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL Postico] haben und mit dem Navigieren in der zugehörigen Benutzeroberfläche vertraut sind. Weitere Informationen zu [!DNL Postico] finden Sie in der [offiziellen [!DNL Postico] Dokumentation](https://eggerapps.at/postico/docs).
> 
> Darüber hinaus ist [!DNL Postico] **nur** auf macOS-Geräten verfügbar.

Um [!DNL Postico] mit dem Abfrage-Service zu verbinden, öffnen Sie [!DNL Postico] und wählen Sie **[!DNL New Favorite]**. Das Dialogfeld für Verbindungseinstellungen wird angezeigt. Hier können Sie Parameterwerte eingeben, um eine Verbindung mit Adobe Experience Platform herzustellen. Geben Sie die unten aufgeführten Verbindungseinstellungen ein. Anleitungen zum [Verbinden mit einem PostgreSQL Server mit Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) finden Sie auch auf der offiziellen Postico-Website.

| Verbindungsparameter | Beschreibung |
|---|---|
| **[!DNL Host]:** | Der Hostname des PostgreSQL-Servers. |
| **[!DNL Port]:** | Der Port für [!DNL Query Service]. Sie müssen Port **80** oder **5432** verwenden, um eine Verbindung mit [!DNL Query Service] herzustellen. |
| **[!DNL User]** | Erstellen Sie einen Namen für Ihre spezifische Verbindung. Lassen Sie das Feld leer, um Ihren Mac-Anmeldenamen zu verwenden. |
| **[!DNL Password]** | Diese alphanumerische Zeichenfolge ist Ihre Experience Platform **[!UICONTROL Kennwort]**-Berechtigung. Wenn Sie nicht ablaufende Anmeldeinformationen verwenden möchten, ist dieser Wert die verketteten Argumente aus der `technicalAccountID` und der in die JSON-Konfigurationsdatei heruntergeladenen `credential`. Das Kennwort hat folgende Form: {technicalAccountId}:{credential}. Die JSON-Konfigurationsdatei für nicht ablaufende Anmeldeinformationen ist ein einmaliger Download während ihrer Initialisierung, von dem Adobe keine Kopie speichert. |
| **[!DNL Database]** | Verwenden Sie Ihren Experience Platform **[!UICONTROL Datenbank]** Berechtigungswert: `prod:all`. |

Weiterführende Informationen dazu, wie Sie Datenbanknamen, Hosts, Ports und Anmeldeinformationen finden können, finden Sie im [ zu Anmeldeinformationen ](../ui/credentials.md). Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei [!DNL Experience Platform] an und wählen Sie **[!UICONTROL Abfragen]** gefolgt von **[!UICONTROL Anmeldeinformationen]**.

Nachdem Sie Ihre Anmeldeinformationen eingefügt haben, wählen Sie **[!DNL Connect]** aus, um eine Verbindung mit dem Abfrage-Service herzustellen.

Nachdem Sie eine Verbindung zu Experience Platform hergestellt haben, können Sie eine Liste aller Beziehungen anzeigen, die zuvor mit dem Abfrage-Service hergestellt wurden.

## SQL-Anweisungen erstellen

Um eine neue SQL-Abfrage zu erstellen, wählen Sie in der Seitenleiste **[!DNL SQL Query]** aus. Alternativ können Sie den Tastaturbefehl (⇧⌘T) verwenden, um zur Abfrageansicht zu navigieren, und die Abfrage eingeben, die Sie ausführen möchten. Wenn Sie fertig sind, wählen Sie **[!DNL Execute Statement]** aus, um die Abfrage auszuführen. Es wird eine Tabelle mit den Ergebnissen der abgeschlossenen Abfrageausführung angezeigt.

In der offiziellen Postico-Dokumentation finden Sie weitere Informationen zur [Verwendung der Abfrageansicht](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## Nächste Schritte

Nachdem Sie sich mit [!DNL Query Service] verbunden haben, können Sie [!DNL Postico] verwenden, um Abfragen zu schreiben. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
