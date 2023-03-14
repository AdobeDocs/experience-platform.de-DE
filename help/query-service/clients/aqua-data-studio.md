---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Aqua Data Studio; Aqua Data Studio; Verbindung mit Query Service;
solution: Experience Platform
title: Aqua Data Studio mit Query Service verbinden
description: In diesem Dokument werden die Schritte zum Verbinden von Aqua Data Studio mit Query Service von Adobe Experience Platform erläutert.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: 3ffb535e9a6648f037678acebba0de5f2088e79e
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 11%

---

# Verbinden von [!DNL Aqua Data Studio] mit dem Abfrage-Service

In diesem Dokument werden die Schritte zum Verbinden von [!DNL Aqua Data Studio] mit Adobe Experience Platform [!DNL Query Service].

## Erste Schritte

Für dieses Handbuch benötigen Sie bereits Zugriff auf [!DNL Aqua Data Studio] und kennen die Navigation in der Benutzeroberfläche. Weitere Informationen [!DNL Aqua Data Studio] finden Sie im Abschnitt [offiziell [!DNL Aqua Data Studio] Dokumentation](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Es gibt [!DNL Windows] und [!DNL macOS] Versionen von [!DNL Aqua Data Studio]. Screenshots in diesem Handbuch wurden mit dem [!DNL macOS] Desktop-Programm. In der Benutzeroberfläche können zwischen den Versionen geringfügige Unterschiede bestehen.

Um die erforderlichen Anmeldeinformationen zum Verbinden von [!DNL Aqua Data Studio] mit Experience Platform zu erhalten, benötigen Sie Zugriff auf den Arbeitsbereich „Abfragen“ in der Platform-Benutzeroberfläche.  Wenden Sie sich an Ihren IMS-Organisationsadministrator, wenn Sie derzeit keinen Zugriff auf die [!UICONTROL Abfragen] Arbeitsbereich.

## Server registrieren {#register-server}

Nach der Installation [!DNL Aqua Data Studio]müssen Sie zunächst den Server registrieren. Anweisungen dazu finden Sie in der offiziellen Aqua Data Studio-Dokumentation . [starten Sie die [!DNL Register Server] dialog](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) und [Server registrieren](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

Einmal **[!DNL Register Server]** für einen PostgresSQL-Server angezeigt wird, geben Sie die folgenden Details für die Servereinstellungen an.

- **[!DNL Name]**: Der Name Ihrer Verbindung. Es wird empfohlen, einen benutzerfreundlichen Namen anzugeben, um die Verbindung zu erkennen.
- **[!DNL Login Name]**: Der Anmeldename ist Ihre Platform-Organisations-ID. Sie hat folgende Form: `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: Dies ist eine alphanumerische Zeichenfolge, die auf der [!DNL Query Service] Anmeldedaten-Dashboard.
- **[!DNL Host and Port]**: Der Host-Endpunkt und sein Port für [!DNL Query Service]. Sie müssen Port 80 verwenden, um eine Verbindung mit [!DNL Query Service].
- **[!DNL Database]:** Die zu verwendende Datenbank. Verwenden Sie den Wert für die Anmeldedaten der Platform-Benutzeroberfläche `dbname`: `prod:all`.

### [!DNL Query Service] Anmeldeinformationen

Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei der [!DNL Platform] Benutzeroberfläche und Auswahl **[!UICONTROL Abfragen]** aus der linken Navigation, gefolgt von **[!UICONTROL Anmeldeinformationen]**. Eine vollständige Anleitung zum Finden Ihrer Anmeldedaten, des Hosts, Ports und des Datenbanknamens finden Sie in der [Handbuch zu Anmeldeinformationen](../ui/credentials.md).

[!DNL Query Service] bietet auch nicht ablaufende Anmeldeinformationen, um eine einmalige Einrichtung mit Drittanbieterclients zu ermöglichen. Weitere Informationen finden Sie in der Dokumentation für [Vollständige Anweisungen zum Generieren und Verwenden von nicht ablaufenden Anmeldedaten](../ui/credentials.md#non-expiring-credentials).

### SSL-Modus festlegen

Als Nächstes müssen Sie den SSL-Moduswert auf `?sslmode=require`. Dies geschieht über die [!DNL Driver] des [!DNL Edit Server Properties] angezeigt. Anweisungen dazu finden Sie in der offiziellen Aqua Data Studio-Dokumentation . [Treibereigenschaften bearbeiten](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) und [SSL konfigurieren für [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). Verwenden Sie die Suchleiste, um die `sslmode` -Eigenschaft.

>[!IMPORTANT]
>
>Siehe [[!DNL Query Service] SSL-Dokumentation](./ssl-modes.md) Erfahren Sie mehr über die SSL-Unterstützung für Drittanbieterverbindungen zu Adobe Experience Platform Query Service und über die Verbindung mit `verify-full` SSL-Modus.

Nachdem Sie Ihre Verbindungsdetails eingegeben haben, wählen Sie auf derselben Registerkarte die Option **[!DNL Test Connection]** , um sicherzustellen, dass Ihre Anmeldeinformationen ordnungsgemäß funktionieren. Wenn Ihr Verbindungstest erfolgreich ist, wählen Sie **[!DNL Save]** um Ihren Server zu registrieren. Es wird ein Bestätigungsdialogfeld angezeigt, in dem die Verbindung bestätigt wird und das Verbindungssymbol im Dashboard angezeigt wird. Sie können jetzt eine Verbindung zum Server herstellen und seine Schemaobjekte anzeigen.

## Nächste Schritte

Nachdem Sie sich mit [!DNL Query Service], können Sie die **[!DNL Query Analyzer]** Innerhalb [!DNL Aqua Data Studio] um SQL-Anweisungen auszuführen und zu bearbeiten. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
