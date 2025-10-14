---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;Looker;Looker;Verbindung zum Abfrage-Service;
solution: Experience Platform
title: Verbinden von Looker mit dem Abfrage-Service
description: In diesem Dokument werden die Schritte zum Verbinden von Looker mit dem Abfrage-Service von Adobe Experience Platform erläutert.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 5%

---

# Verbinden von [!DNL Looker] mit dem Abfrage-Service

In diesem Dokument werden die Schritte zum Verbinden von [!DNL Looker] mit Adobe Experience Platform [!DNL Query Service] beschrieben.

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL Looker] haben und mit dem Navigieren in der zugehörigen Benutzeroberfläche vertraut sind. Weitere Informationen zu [!DNL Looker] finden Sie in der [offiziellen [!DNL Looker] Dokumentation](https://docs.looker.com/).

## Erstellen einer neuen Datenbankverbindung {#create-connection}

Wählen Sie nach der Anmeldung bei [!DNL Looker] die Option **[!DNL Admin]** und dann **[!DNL Connections]** aus. Die Seite [!DNL Connections] wird geöffnet. Wählen Sie auf der [!DNL Connections] Seite **[!DNL Add Connection]** aus.

Geben Sie hier die Details für die unten aufgeführten Verbindungseinstellungen ein. In der offiziellen Looker-Dokumentation finden [&#x200B; Anweisungen zum Erstellen einer neuen Datenbankverbindung und Beschreibungen der verfügbaren Eigenschaften](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** Der Name Ihrer Verbindung.
- **[!DNL Dialect]:** Der Dialekt, der für die SQL-Datenbank verwendet wird. [!DNL Query Service] verwendet **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** Der Host-Endpunkt und dessen Port für [!DNL Query Service].
- **[!DNL Database]:** Die zu verwendende Datenbank.
- **[!DNL Username and Password]:** Die Anmeldedaten, die verwendet werden. Der Benutzername hat die Form `ORG_ID@AdobeOrg`.
- **SSL**: Aktivieren Sie SSL, um eine sichere Verbindung über das Netzwerk sicherzustellen.

Um die zum Verbinden von Looker mit dem Abfrage-Service erforderlichen Anmeldeinformationen zu finden, melden Sie sich bei der Experience Platform-Benutzeroberfläche an und wählen Sie **[!UICONTROL Abfragen]** im linken Navigationsbereich aus, gefolgt von **[!UICONTROL Anmeldeinformationen]**. Weitere Informationen zum Auffinden der Anmeldeinformationen **host**, **port**, **database**, **username** und **password** finden Sie im Handbuch [credentials](../ui/credentials.md).

![Die Seite mit den Anmeldeinformationen des Arbeitsbereichs &quot;Experience Platform-Abfragen“ mit hervorgehobenen Anmeldeinformationen und den ablaufenden Anmeldeinformationen.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] bietet auch nicht ablaufende Anmeldeinformationen, um eine einmalige Einrichtung mit Drittanbieter-Clients zu ermöglichen. Siehe die Dokumentation für [vollständige Anweisungen zum Generieren und Verwenden nicht ablaufender Anmeldeinformationen](../ui/credentials.md#non-expiring-credentials). Es ist notwendig, diesen Prozess abzuschließen, wenn Sie Looker als einmaliges Setup verbinden möchten. Die erfassten `credential`- und `technicalAccountId`-Werte umfassen den Wert für den Looker-`password`.

Weitere Informationen zur SSL-Unterstützung für Drittanbieterverbindungen in Adobe Experience Platform finden Sie in der [[!DNL Query Service] SSL-Dokumentation](./ssl-modes.md). In diesem Dokument erfahren Sie, wie Sie eine Verbindung mit `verify-full` SSL-Modus herstellen.

Nachdem Sie Ihre Verbindungsdetails eingegeben haben, wählen Sie **[!DNL Test These Settings]** aus, um sicherzustellen, dass Ihre Anmeldeinformationen ordnungsgemäß funktionieren. Weitere Informationen zum [&#x200B; Ihrer Verbindungseinstellungen finden &#x200B;](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) in der offiziellen Looker-Dokumentation. Bei erfolgreicher Verbindung wird eine Meldung auf dem Bildschirm angezeigt, die Sie darauf hinweist, dass Sie eine Verbindung herstellen können. Nachdem Ihre Verbindung erfolgreich hergestellt wurde, wählen Sie **[!DNL Add Connection]** aus, um Ihre Verbindung zu erstellen.

## Nächste Schritte

Nachdem Sie sich mit [!DNL Query Service] verbunden haben, können Sie [!DNL Looker] verwenden, um Abfragen zu schreiben. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
