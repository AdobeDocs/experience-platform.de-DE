---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
solution: Experience Platform
title: Überblick über Self-Serve-Quellen (Batch SDK)
description: Adobe Experience Platform Self-Serve Sources (Batch SDK) ist eine Reihe von Konfigurations-APIs, mit denen Sie eine REST API-basierte Quelle mithilfe der Flow Service-API integrieren können, um Ihre Daten an Experience Platform zu übertragen.
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 7%

---

# Überblick über Self-Serve-Quellen (Batch SDK)

Adobe Experience Platform Self-Serve Sources (Batch SDK) ist ein Framework, mit dem Sie eine REST API-basierte Quelle mit der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) in den Experience Platform-Quellkatalog integrieren können. Self-Serve Sources (Batch SDK) bietet eine Reihe von Konfigurations-APIs, mit denen Sie Ihre eigene Quelle erstellen und Ihre Batch-Daten an Experience Platform übertragen können.

Mit Self-Serve-Quellen (Batch SDK) können Sie:

* Konfigurieren und integrieren Sie mithilfe der [!DNL Flow Service] -API eine neue Quelle in den Experience Platform-Katalog.
* Definieren Sie Spezifikationen für Ihre Quelle, einschließlich Informationen zu unterstützten Authentifizierungstypen und dazu, wie Ressourcendaten abgerufen werden.
* Erstellen Sie eine benutzerfreundliche Dokumentation für Ihre neue Quelle.

Die Dokumentation zu Self-Serve-Quellen enthält Anweisungen zum Konfigurieren, Testen und Veröffentlichen einer REST API-basierten Quellintegration mit Experience Platform und dazu, dass Ihre Quelle Teil des ständig wachsenden Quellkatalogs wird.

![Katalog](./assets/catalog.png)

## Grundlagen zu Quellen

Experience Platform kann Daten aus externen Quellen erfassen und gleichzeitig diese Daten mithilfe von Experience Platform-Diensten strukturieren, beschriften und erweitern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Weitere Informationen zu Quellen und eine Liste der verschiedenen derzeit auf Experience Platform unterstützten Quellen finden Sie in der [Quellenübersicht](../home.md).

## Erstellen einer Quelle

Über Self-Serve-Quellen können Sie Ihre eigene REST-API-basierte Quelle integrieren und Ihre Daten mit [!DNL Flow Service] an Experience Platform übergeben. Sie können eine Quelle in den Experience Platform-Quellkatalog integrieren, indem Sie neue Verbindungsspezifikationen über die [!DNL Flow Service] -API erstellen, konfigurieren und senden.

Informationen zur Integration einer neuen Quelle in Experience Platform finden Sie im Handbuch zum [Erstellen einer neuen Verbindungsspezifikation](./api/api-overview.md) .

## Quelle dokumentieren

Nachdem die Quelle erstellt wurde, finden Sie im [Dokumentationshandbuch](./documentation/doc-overview.md) Anweisungen dazu, wie Sie Ihre Quelle über die [!DNL GitHub] -Web-Oberfläche oder Ihren eigenen Texteditor dokumentieren.

## Allgemeine Vorgehensweise

Der Schritt-für-Schritt-Vorgang zum Konfigurieren der Quelle unter Experience Platform ist unten beschrieben:

* Lesen Sie den API-Leitfaden für die [Self-Serve-Quellen (Batch SDK)](./api/api-overview.md).
   * Lesen Sie den Leitfaden [Erste Schritte](./api/getting-started.md).
   * Befolgen Sie das Tutorial zum Erstellen einer neuen Verbindungsspezifikation ](./api/create.md).[
   * Befolgen Sie das Tutorial zum Aktualisieren Ihrer Verbindungsspezifikation ](./api/update-connection-specs.md).[
   * Befolgen Sie das Tutorial zum Hinzufügen der neuen Verbindungsspezifikations-ID zu einer Flussspezifikation ](./api/update-flow-specs.md)[
   * [Senden Sie Ihre neue Quelle](./api/submit.md).
* Um ein besseres Verständnis der Struktur und Eigenschaften einer Verbindungsspezifikation zu erhalten, lesen Sie das Handbuch zu [Konfigurationsoptionen für Self-Serve-Quellen (Batch SDK)](./config/config.md).
   * Lesen Sie das Handbuch zu [Konfigurieren Ihrer Authentifizierungsspezifikationen](./config/authspec.md) , um ein besseres Verständnis der verschiedenen Authentifizierungstypen zu erhalten, die Sie für Ihre Quelle verwenden können.
   * Informationen zu den verschiedenen Paginierungstypen, Planungsformaten und benutzerdefinierten Schemata, die für Ihre Quelle konfiguriert werden können, finden Sie im Handbuch unter [Konfigurieren Ihrer Quellspezifikationen](./config/sourcespec.md) .
   * Informationen zum Definieren der Parameter, die zum Erkunden und Untersuchen von in der Quelle enthaltenen Objekten erforderlich sind, finden Sie im Handbuch unter [Konfigurieren Ihrer Erkundungsspezifikationen](./config/explorespec.md) .
* Um mit der Dokumentation Ihrer Quelle zu beginnen, lesen Sie die [Übersicht über das Erstellen der Dokumentation für Self-Serve-Quellen](./documentation/doc-overview.md) .
   * Sie können diese [Quellen-API-Dokumentationsvorlage](./documentation/template.md) verwenden, um Ihre API-Dokumentation zu strukturieren.
   * Sie können diese Dokumentationsvorlage für die [Quellenbenutzeroberfläche](./documentation/ui-template.md) verwenden, um Ihre Benutzeroberflächendokumentation zu strukturieren.
   * Anweisungen zum Erstellen einer Dokumentation mit GitHub finden Sie im Handbuch zu [Verwendung der GitHub-Web-Oberfläche](./documentation/github.md) .
   * Anweisungen zum Erstellen von Dokumentationen mit Ihrem lokalen Computer finden Sie im Handbuch zu [Verwendung eines Texteditors](./documentation/text-editor.md) .
