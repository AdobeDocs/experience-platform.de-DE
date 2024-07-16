---
keywords: Experience Platform;home;popular topics;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: Verbinden von Looker mit Query Service
description: In diesem Dokument werden die Schritte zum Verbinden von Looker mit dem Adobe Experience Platform Query Service beschrieben.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 5%

---

# Verbinden von [!DNL Looker] mit dem Abfrage-Service

In diesem Dokument werden die Schritte zum Verbinden von [!DNL Looker] mit Adobe Experience Platform [!DNL Query Service] beschrieben.

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL Looker] haben und mit der Navigation in der Benutzeroberfläche vertraut sind. Weitere Informationen zu [!DNL Looker] finden Sie in der [offiziellen [!DNL Looker] Dokumentation](https://docs.looker.com/).

## Neue Datenbankverbindung erstellen {#create-connection}

Nachdem Sie sich bei [!DNL Looker] angemeldet haben, wählen Sie **[!DNL Admin]**, gefolgt von **[!DNL Connections]**. Die Seite [!DNL Connections] wird geöffnet. Wählen Sie auf der Seite [!DNL Connections] die Option **[!DNL Add Connection]** aus.

Geben Sie hier die Details für die unten aufgeführten Verbindungsparameter ein. Anweisungen zum Erstellen einer neuen Datenbankverbindung und Beschreibungen der verfügbaren Eigenschaften finden Sie in der offiziellen Dokumentation zu Looker](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).[

- **[!DNL Name]:** Der Name Ihrer Verbindung.
- **[!DNL Dialect]:** Das für die SQL-Datenbank verwendete Dialogfeld. [!DNL Query Service] verwendet **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** Der Host-Endpunkt und sein Port für [!DNL Query Service].
- **[!DNL Database]:** Die Datenbank, die verwendet wird.
- **[!DNL Username and Password]:** Die Anmeldeinformationen, die verwendet werden. Der Benutzername hat die Form &quot;`ORG_ID@AdobeOrg`&quot;.
- **SSL**: Aktivieren Sie SSL, um eine sichere Verbindung im Netzwerk sicherzustellen.

Um die Anmeldeinformationen zu finden, die zum Verbinden von Looker mit Query Service erforderlich sind, melden Sie sich bei der Platform-Benutzeroberfläche an und wählen Sie im linken Navigationsbereich **[!UICONTROL Abfragen]** , gefolgt von **[!UICONTROL Anmeldeinformationen]**. Weitere Informationen zum Auffinden Ihrer Anmeldedaten für **host**, **port**, **database**, **username** und **password** finden Sie im [Benutzerhandbuch](../ui/credentials.md).

![Die Seite &quot;Anmeldeinformationen&quot;im Arbeitsbereich &quot;Experience Platform-Abfragen&quot;mit Anmeldeinformationen und Kennungen zum Ablauf der Anmeldedaten sind hervorgehoben.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] bietet auch nicht ablaufende Anmeldeinformationen, um eine einmalige Einrichtung mit Clients von Drittanbietern zu ermöglichen. Eine vollständige Anleitung zum Generieren und Verwenden von nicht ablaufenden Anmeldedaten finden Sie in der Dokumentation für [. ](../ui/credentials.md#non-expiring-credentials) Dieser Vorgang muss abgeschlossen werden, wenn Sie Looker als einmaliges Setup verbinden möchten. Die erworbenen Werte `credential` und `technicalAccountId` bilden den Wert für den Parameter Looker `password` .

Informationen zur SSL-Unterstützung für Drittanbieterverbindungen in Adobe Experience Platform finden Sie in der [[!DNL Query Service] SSL-Dokumentation](./ssl-modes.md). Dieses Dokument enthält Anweisungen zum Herstellen einer Verbindung mit dem SSL-Modus &quot;`verify-full`&quot;.

Nachdem Sie Ihre Verbindungsdetails eingegeben haben, wählen Sie **[!DNL Test These Settings]** aus, um sicherzustellen, dass Ihre Anmeldedaten ordnungsgemäß funktionieren. Weitere Informationen zu [Testen Ihrer Verbindungseinstellungen](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) finden Sie in der offiziellen Dokumentation zu Looker. Bei erfolgreicher Verbindung wird auf dem Bildschirm eine Meldung angezeigt, die angibt, dass Sie eine Verbindung herstellen können. Nachdem die Verbindung erfolgreich hergestellt wurde, wählen Sie **[!DNL Add Connection]** aus, um Ihre Verbindung zu erstellen.

## Nächste Schritte

Nachdem Sie sich mit [!DNL Query Service] angemeldet haben, können Sie mit [!DNL Looker] Abfragen schreiben. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
