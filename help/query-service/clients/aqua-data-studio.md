---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;Aqua Data Studio;Aqua Data Studio;Verbinden mit dem Abfrage-Service;
solution: Experience Platform
title: Verbinden von Aqua Data Studio mit dem Abfrage-Service
description: In diesem Dokument werden die Schritte zum Verbinden von Aqua Data Studio mit Query Service von Adobe Experience Platform erläutert.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 8%

---

# Verbinden von [!DNL Aqua Data Studio] mit dem Abfrage-Service

In diesem Dokument werden die Schritte zum Verbinden von [!DNL Aqua Data Studio] mit Adobe Experience Platform [!DNL Query Service] beschrieben.

## Erste Schritte

Für dieses Handbuch müssen Sie bereits Zugriff auf [!DNL Aqua Data Studio] haben und mit dem Navigieren in der zugehörigen Benutzeroberfläche vertraut sein. Weitere Informationen zu [!DNL Aqua Data Studio] finden Sie in der [offiziellen [!DNL Aqua Data Studio] Dokumentation](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Es gibt [!DNL Windows] und [!DNL macOS] Versionen von [!DNL Aqua Data Studio]. Screenshots in diesem Handbuch wurden mit dem [!DNL macOS] Desktop-Programm erstellt. Es kann zu geringfügigen Diskrepanzen zwischen den Versionen in der Benutzeroberfläche kommen.

Um die erforderlichen Anmeldeinformationen zum Verbinden von [!DNL Aqua Data Studio] mit Experience Platform zu erhalten, benötigen Sie Zugriff auf den Arbeitsbereich [!UICONTROL Abfragen] in der Platform-Benutzeroberfläche. Wenden Sie sich an den Admin Ihrer Organisation, wenn Sie derzeit keinen Zugriff auf den Arbeitsbereich [!UICONTROL Abfragen] haben.

## Registrieren des Servers {#register-server}

Nach der Installation von [!DNL Aqua Data Studio] müssen Sie zunächst den Server registrieren. In der offiziellen Aqua Data Studio-Dokumentation finden Sie Anweisungen zum [ (Starten des  [!DNL Register Server] -](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) und [Registrieren des Servers](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

Sobald das Dialogfeld **[!DNL Register Server]** für einen PostgresSQL-Server angezeigt wird, geben Sie die folgenden Details für die Server-Einstellungen an.

- **[!DNL Name]**: Der Name Ihrer Verbindung. Es wird empfohlen, einen Anzeigenamen anzugeben, um die Verbindung zu erkennen.
- **[!DNL Login Name]**: Der Anmeldename ist Ihre Platform-Organisations-ID. Es hat die Form von `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: Dies ist eine alphanumerische Zeichenfolge, die im Dashboard für [!DNL Query Service]-Anmeldeinformationen gefunden wurde.
- **[!DNL Host and Port]**: Der Host-Endpunkt und sein Port für [!DNL Query Service]. Sie müssen Port 80 verwenden, um eine Verbindung mit [!DNL Query Service] herzustellen.
- **[!DNL Database]:** Die zu verwendende Datenbank. Verwenden Sie den Wert für die `dbname` der Platform-Benutzeroberfläche: `prod:all`.

### [!DNL Query Service]

Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei der [!DNL Platform]-Benutzeroberfläche an und wählen Sie **[!UICONTROL Abfragen]** im linken Navigationsbereich aus, gefolgt von **[!UICONTROL Anmeldeinformationen]**. Eine vollständige Anleitung, um Ihre Anmeldedaten, Hosts, Ports und Datenbanknamen zu finden, finden Sie im [Handbuch zu Anmeldedaten](../ui/credentials.md).

[!DNL Query Service] bietet auch nicht ablaufende Anmeldeinformationen, um eine einmalige Einrichtung mit Drittanbieter-Clients zu ermöglichen. Siehe die Dokumentation für [vollständige Anweisungen zum Generieren und Verwenden nicht ablaufender Anmeldeinformationen](../ui/credentials.md#non-expiring-credentials).

### Festlegen des SSL-Modus

Als Nächstes müssen Sie den SSL-Modus-Wert auf `?sslmode=require` setzen. Dies erfolgt über die Registerkarte [!DNL Driver] des Dialogfelds [!DNL Edit Server Properties] . In der offiziellen Aqua Data Studio-Dokumentation finden Sie Anweisungen zum [ (Bearbeiten von Treibereigenschaften](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) und [Konfigurieren von SSL für [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). Verwenden Sie die Suchleiste, um die `sslmode` Eigenschaft zu finden.

>[!IMPORTANT]
>
>In der [[!DNL Query Service] SSL-](./ssl-modes.md) erfahren Sie mehr über die SSL-Unterstützung für Drittanbieterverbindungen zum Abfrage-Service von Adobe Experience Platform und darüber, wie Sie eine Verbindung mit `verify-full` SSL-Modus herstellen.

Nachdem Sie Ihre Verbindungsdetails eingegeben haben, wählen Sie auf derselben Registerkarte **[!DNL Test Connection]** aus, um sicherzustellen, dass Ihre Anmeldeinformationen ordnungsgemäß funktionieren. Wenn Ihr Verbindungstest erfolgreich war, wählen Sie **[!DNL Save]** aus, um Ihren Server zu registrieren. Es wird ein Bestätigungsdialogfeld angezeigt, das die Verbindung bestätigt, und das Verbindungssymbol wird im Dashboard angezeigt. Sie können jetzt eine Verbindung zum Server herstellen und dessen Schemaobjekte anzeigen.

## Nächste Schritte

Nachdem Sie nun eine Verbindung zu [!DNL Query Service] hergestellt haben, können Sie die **[!DNL Query Analyzer]** in [!DNL Aqua Data Studio] verwenden, um SQL-Anweisungen auszuführen und zu bearbeiten. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
