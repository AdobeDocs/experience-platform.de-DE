---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; Query Service; postico; Postico; Verbindung mit Query Service
solution: Experience Platform
title: Verbindung mit Query Service
description: Dieses Dokument enthält den Link zur Installation des Backup-Clients Postico für Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 8%

---

# Verbinden [!DNL Postico] zu Query Service (Mac)

In diesem Dokument werden die Schritte zum Verbinden von [!DNL Postico] mit Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL Postico] und sind mit dem Navigieren in der Benutzeroberfläche vertraut. Weitere Informationen [!DNL Postico] finden Sie im Abschnitt [offiziell [!DNL Postico] Dokumentation](https://eggerapps.at/postico/docs).
> 
> Zusätzlich [!DNL Postico] is **only** auf macOS-Geräten verfügbar.

Verbindung herstellen [!DNL Postico] zu Query Service, öffnen Sie [!DNL Postico] und wählen Sie **[!DNL New Favorite]**. Das Dialogfeld für Verbindungseinstellungen wird angezeigt. Von hier aus können Sie Parameterwerte eingeben, um eine Verbindung mit Adobe Experience Platform herzustellen. Geben Sie die unten aufgeführten Verbindungsparameter ein. Anleitung zum [Verbindung zu einem PostgreSQL-Server mit Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) sind auch auf der offiziellen Postico-Website verfügbar.

| Verbindungsparameter | Beschreibung |
|---|---|
| **[!DNL Host]:** | Der Hostname des PostgreSQL-Servers. |
| **[!DNL Port]:** | Der Port für [!DNL Query Service]. Sie müssen Port verwenden **80** oder **5432** zur Verbindung mit [!DNL Query Service]. |
| **[!DNL User]** | Erstellen Sie einen Namen für Ihre spezifische Verbindung. Lassen Sie das Feld leer, um Ihren Mac-Anmeldenamen zu verwenden. |
| **[!DNL Password]** | Diese alphanumerische Zeichenfolge ist Ihre Experience Platform **[!UICONTROL Passwort]** Berechtigung. Wenn Sie nicht ablaufende Anmeldeinformationen verwenden möchten, ist dieser Wert die verketteten Argumente aus dem `technicalAccountID` und `credential` in die JSON-Konfigurationsdatei heruntergeladen wurde. Der Kennwortwert hat folgende Form: {technicalAccountId}:{credential}. Die JSON-Konfigurationsdatei für nicht ablaufende Anmeldeinformationen ist ein einmaliger Download während der Initialisierung, von dem die Adobe keine Kopie aufbewahrt. |
| **[!DNL Database]** | Verwenden Ihrer Experience Platform **[!UICONTROL Datenbank]** credential value: `prod:all`. |

Weiterführende Informationen dazu, wie Sie Datenbanknamen, Hosts, Ports und Anmeldeinformationen finden können, stehen im [Handbuch zu Anmeldeinformationen](../ui/credentials.md). Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei [!DNL Platform], wählen Sie **[!UICONTROL Abfragen]**, gefolgt von **[!UICONTROL Anmeldeinformationen]**.

Nachdem Sie Ihre Anmeldedaten eingefügt haben, wählen Sie **[!DNL Connect]** , um eine Verbindung mit Query Service herzustellen.

Nach der Verbindung mit Platform können Sie eine Liste aller zuvor mit Query Service vorgenommenen Relationen anzeigen.

## SQL-Anweisungen erstellen

Um eine neue SQL-Abfrage zu erstellen, wählen Sie **[!DNL SQL Query]** über die Seitenleiste aus. Verwenden Sie alternativ den Tastaturbefehl (⇧ ⌘ T), um zur Abfrageansicht zu navigieren und die Abfrage einzugeben, die Sie ausführen möchten. Wenn Sie fertig sind, wählen Sie **[!DNL Execute Statement]** , um die Abfrage auszuführen. Eine Tabelle mit den Ergebnissen Ihrer abgeschlossenen Abfrage-Ausführung wird angezeigt.

Weitere Informationen zu [mit der Abfrageansicht](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## Nächste Schritte

Jetzt, da Sie mit [!DNL Query Service]können Sie [!DNL Postico] , um Abfragen zu schreiben. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
