---
keywords: Experience Platform; home; beliebte Themen; Query Service; Query Service; Aqua Data Studio; Aqua Data Studio; Verbindung mit Query Service;
solution: Experience Platform
title: Aqua Data Studio mit Query Service verbinden
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

Für dieses Handbuch müssen Sie bereits Zugriff auf [!DNL Aqua Data Studio] haben und sich mit der Navigation in der Benutzeroberfläche vertraut machen. Weitere Informationen zu [!DNL Aqua Data Studio] finden Sie in der [offiziellen [!DNL Aqua Data Studio] Dokumentation](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Es gibt [!DNL Windows] und [!DNL macOS] Versionen von [!DNL Aqua Data Studio]. Screenshots in diesem Handbuch wurden mit dem [!DNL macOS] -Desktop-Programm erstellt. In der Benutzeroberfläche können zwischen den Versionen geringfügige Unterschiede bestehen.

Um die erforderlichen Anmeldeinformationen zum Verbinden von [!DNL Aqua Data Studio] mit Experience Platform zu erhalten, müssen Sie auf den Arbeitsbereich [!UICONTROL Abfragen] in der Platform-Benutzeroberfläche zugreifen können. Wenden Sie sich an Ihren Organisationsadministrator, wenn Sie derzeit keinen Zugriff auf den Arbeitsbereich [!UICONTROL Abfragen] haben.

## Server registrieren {#register-server}

Nach der Installation von [!DNL Aqua Data Studio] müssen Sie zunächst den Server registrieren. Anweisungen zum Starten des  [!DNL Register Server] Dialogfelds](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) und zum Registrieren des Servers ](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio) finden Sie in der offiziellen Dokumentation zu Aqua Data Studio .[[

Sobald das Dialogfeld &quot;**[!DNL Register Server]**&quot;für einen PostgresSQL-Server angezeigt wird, geben Sie die folgenden Details für die Servereinstellungen an.

- **[!DNL Name]**: Der Name Ihrer Verbindung. Es wird empfohlen, einen benutzerfreundlichen Namen anzugeben, um die Verbindung zu erkennen.
- **[!DNL Login Name]**: Der Anmeldename ist Ihre Platform-Organisations-ID. Sie hat die Form &quot;`ORG_ID@AdobeOrg`&quot;.
- **[!DNL Password]**: Dies ist eine alphanumerische Zeichenfolge, die im Dashboard mit den Anmeldedaten für [!DNL Query Service] gefunden wird.
- **[!DNL Host and Port]**: Der Host-Endpunkt und sein Port für [!DNL Query Service]. Sie müssen Port 80 verwenden, um eine Verbindung mit [!DNL Query Service] herzustellen.
- **[!DNL Database]:** Die Datenbank, die verwendet wird. Verwenden Sie den Wert für die Berechtigung für die Platform-Benutzeroberfläche `dbname`: `prod:all`.

### [!DNL Query Service] Anmeldedaten

Um Ihre Anmeldedaten zu finden, melden Sie sich bei der Benutzeroberfläche von [!DNL Platform] an und wählen Sie **[!UICONTROL Abfragen]** aus der linken Navigation, gefolgt von **[!UICONTROL Anmeldeinformationen]**. Eine vollständige Anleitung zum Auffinden Ihrer Anmeldedaten, Ihres Hosts, Ports und des Datenbanknamens finden Sie im [Handbuch zu Anmeldeinformationen](../ui/credentials.md).

[!DNL Query Service] bietet auch nicht ablaufende Anmeldeinformationen, um eine einmalige Einrichtung mit Clients von Drittanbietern zu ermöglichen. Eine vollständige Anleitung zum Generieren und Verwenden von nicht ablaufenden Anmeldedaten finden Sie in der Dokumentation für [.](../ui/credentials.md#non-expiring-credentials)

### SSL-Modus festlegen

Als Nächstes müssen Sie den SSL-Moduswert auf `?sslmode=require` setzen. Dies erfolgt über die Registerkarte [!DNL Driver] des Dialogfelds [!DNL Edit Server Properties]. Anweisungen zum Bearbeiten der Treibereigenschaften](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) und zum Konfigurieren von SSL für  [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration) finden Sie in der offiziellen Dokumentation zu Aqua Data Studio . [[ Verwenden Sie die Suchleiste, um die Eigenschaft `sslmode` zu finden.

>[!IMPORTANT]
>
>In der [[!DNL Query Service] SSL-Dokumentation](./ssl-modes.md) erfahren Sie mehr über die SSL-Unterstützung für Verbindungen von Drittanbietern mit dem Adobe Experience Platform Query Service und über die Verbindung mit dem `verify-full` SSL-Modus.

Nachdem Sie Ihre Verbindungsdetails eingegeben haben, wählen Sie auf derselben Registerkarte **[!DNL Test Connection]** aus, um sicherzustellen, dass Ihre Anmeldedaten ordnungsgemäß funktionieren. Wenn Ihr Verbindungstest erfolgreich ist, wählen Sie **[!DNL Save]** aus, um den Server zu registrieren. Es wird ein Bestätigungsdialogfeld angezeigt, in dem die Verbindung bestätigt wird und das Verbindungssymbol im Dashboard angezeigt wird. Sie können jetzt eine Verbindung zum Server herstellen und seine Schemaobjekte anzeigen.

## Nächste Schritte

Nachdem Sie eine Verbindung zu [!DNL Query Service] hergestellt haben, können Sie die **[!DNL Query Analyzer]** in [!DNL Aqua Data Studio] verwenden, um SQL-Anweisungen auszuführen und zu bearbeiten. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
