---
keywords: Experience Platform;home;popular topics;Query service;query service;postico;Postico;connect to query service
solution: Experience Platform
title: Verbindung mit Query Service
description: Dieses Dokument enthält den Link zur Installation des Backup-Clients Postico für Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 4%

---

# Verbinden von [!DNL Postico] mit Query Service (Mac)

In diesem Dokument werden die Schritte zum Verbinden von [!DNL Postico] mit Adobe Experience Platform [!DNL Query Service] beschrieben.

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL Postico] haben und mit der Navigation in der Benutzeroberfläche vertraut sind. Weitere Informationen zu [!DNL Postico] finden Sie in der [offiziellen [!DNL Postico] Dokumentation](https://eggerapps.at/postico/docs).
> 
> Außerdem ist [!DNL Postico] **nur** auf macOS-Geräten verfügbar.

Um [!DNL Postico] mit Query Service zu verbinden, öffnen Sie [!DNL Postico] und wählen Sie **[!DNL New Favorite]** aus. Das Dialogfeld für Verbindungseinstellungen wird angezeigt. Von hier aus können Sie Parameterwerte eingeben, um eine Verbindung mit Adobe Experience Platform herzustellen. Geben Sie die unten aufgeführten Verbindungsparameter ein. Anweisungen zum Herstellen einer Verbindung mit einem PostgreSQL-Server mit Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) finden Sie auch auf der offiziellen Postico-Website.[

| Verbindungsparameter | Beschreibung |
|---|---|
| **[!DNL Host]:** | Der Hostname des PostgreSQL-Servers. |
| **[!DNL Port]:** | Der Port für [!DNL Query Service]. Sie müssen den Port **80** oder **5432** verwenden, um eine Verbindung mit [!DNL Query Service] herzustellen. |
| **[!DNL User]** | Erstellen Sie einen Namen für Ihre spezifische Verbindung. Lassen Sie das Feld leer, um Ihren Mac-Anmeldenamen zu verwenden. |
| **[!DNL Password]** | Diese alphanumerische Zeichenfolge ist Ihre Experience Platform **[!UICONTROL Kennwort]**-Berechtigung. Wenn Sie nicht ablaufende Anmeldeinformationen verwenden möchten, ist dieser Wert die verketteten Argumente aus den `technicalAccountID` und den `credential`, die in der JSON-Konfigurationsdatei heruntergeladen wurden. Der Kennwortwert hat das folgende Format: {technicalAccountId}:{credential}. Die JSON-Konfigurationsdatei für nicht ablaufende Anmeldeinformationen ist ein einmaliger Download während der Initialisierung, von dem Adobe keine Kopie aufbewahrt. |
| **[!DNL Database]** | Verwenden Sie Ihren Experience Platform **[!UICONTROL Database]**-Berechtigungswert: `prod:all`. |

Weitere Informationen zum Auffinden Ihrer Datenbanknamen, Host-, Port- und Anmeldedaten finden Sie im [Handbuch zu Anmeldeinformationen](../ui/credentials.md). Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei [!DNL Platform] an, wählen Sie dann **[!UICONTROL Abfragen]**, gefolgt von **[!UICONTROL Anmeldeinformationen]**.

Wählen Sie nach dem Einfügen Ihrer Anmeldedaten **[!DNL Connect]** aus, um eine Verbindung mit Query Service herzustellen.

Nach der Verbindung mit Platform können Sie eine Liste aller zuvor mit Query Service vorgenommenen Relationen anzeigen.

## SQL-Anweisungen erstellen

Um eine neue SQL-Abfrage zu erstellen, wählen Sie in der Seitenleiste die Option **[!DNL SQL Query]** aus. Verwenden Sie alternativ den Tastaturbefehl (⇧ ⌘ T), um zur Abfrageansicht zu navigieren und die Abfrage einzugeben, die Sie ausführen möchten. Wählen Sie abschließend **[!DNL Execute Statement]** aus, um die Abfrage auszuführen. Eine Tabelle mit den Ergebnissen Ihrer abgeschlossenen Abfrage-Ausführung wird angezeigt.

Weitere Informationen zu [Verwendung der Abfrageansicht](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html) finden Sie in der offiziellen Postico-Dokumentation .

## Nächste Schritte

Nachdem Sie sich mit [!DNL Query Service] angemeldet haben, können Sie mit [!DNL Postico] Abfragen schreiben. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
