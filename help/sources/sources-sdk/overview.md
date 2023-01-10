---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
solution: Experience Platform
title: Überblick über Self-Serve-Quellen (Batch SDK)
description: Adobe Experience Platform Self-Serve Sources (Batch SDK) ist ein Satz von Konfigurations-APIs, mit denen Sie eine REST API-basierte Quelle mithilfe der Flow Service-API integrieren können, um Ihre Daten in die Experience Platform zu bringen.
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 8%

---

# Überblick über Self-Serve-Quellen (Batch SDK)

Adobe Experience Platform Self-Serve Sources (Batch SDK) ist ein Framework, mit dem Sie eine REST API-basierte Quelle mit dem Experience Platform Sources-Katalog integrieren können. [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Self-Serve-Quellen (Batch SDK) bieten eine Reihe von Konfigurations-APIs, mit denen Sie Ihre eigene Quelle erstellen und Ihre Batch-Daten in die Experience Platform übertragen können.

Mit Self-Serve-Quellen (Batch SDK) können Sie:

* Konfigurieren und integrieren Sie eine neue Quelle in den Experience Platform-Katalog mithilfe des [!DNL Flow Service] API.
* Definieren Sie Spezifikationen für Ihre Quelle, einschließlich Informationen zu unterstützten Authentifizierungstypen und dazu, wie Ressourcendaten abgerufen werden.
* Erstellen Sie eine benutzerfreundliche Dokumentation für Ihre neue Quelle.

Die Dokumentation zu Self-Serve-Quellen enthält Anweisungen zum Konfigurieren, Testen und Veröffentlichen einer REST API-basierten Quellintegration mit Experience Platform und dazu, dass Ihre Quelle Teil des ständig wachsenden Quellkatalogs wird.

![Katalog](./assets/catalog.png)

## Grundlagen zu Quellen

Experience Platform kann Daten aus externen Quellen erfassen und gleichzeitig diese Daten mithilfe von Experience Platform-Diensten strukturieren, beschriften und erweitern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Weitere Informationen zu den Quellen sowie eine Liste der verschiedenen derzeit von Experience Platform unterstützten Quellen finden Sie unter [Quellen - Übersicht](../home.md).

## Erstellen einer Quelle

Über Self-Serve-Quellen können Sie Ihre eigene REST-API-basierte Quelle integrieren und Ihre Daten in die Experience Platform mit [!DNL Flow Service]. Sie können eine Quelle in den Experience Platform-Quellkatalog integrieren, indem Sie neue Verbindungsspezifikationen erstellen, konfigurieren und senden, über die [!DNL Flow Service] API.

Siehe Handbuch unter [Erstellen einer neuen Verbindungsspezifikation](./api/api-overview.md) Informationen zur Integration einer neuen Quelle in Experience Platform.

## Quelle dokumentieren

Nachdem die Quelle erstellt wurde, lesen Sie den Abschnitt [Handbuch](./documentation/doc-overview.md) Anweisungen zum Dokumentieren der Quelle über das [!DNL GitHub] Web-Oberfläche oder über Ihren eigenen Texteditor.

## Allgemeine Vorgehensweise

Der Schritt-für-Schritt-Vorgang zum Konfigurieren der Quelle in Experience Platform ist unten beschrieben:

* Lesen Sie die [Handbuch zur API für Self-Serve-Quellen (Batch SDK)](./api/api-overview.md).
   * Lesen Sie die [Erste Schritte](./api/getting-started.md).
   * Folgen Sie dem Tutorial zu [Erstellen einer neuen Verbindungsspezifikation](./api/create.md).
   * Folgen Sie dem Tutorial zu [Aktualisieren der Verbindungsspezifikation](./api/update-connection-specs.md).
   * Folgen Sie dem Tutorial zu [Hinzufügen der neuen Verbindungsspezifikations-ID zu einer Flussspezifikation](./api/update-flow-specs.md)
   * [Neue Quelle senden](./api/submit.md).
* Um ein besseres Verständnis der Struktur und Eigenschaften einer Verbindungsspezifikation zu erhalten, lesen Sie das Handbuch unter [Konfigurationsoptionen für Self-Serve-Quellen (Batch-SDK)](./config/config.md).
   * Lesen Sie das Handbuch unter [Authentifizierungsspezifikationen konfigurieren](./config/authspec.md) , um ein besseres Verständnis der verschiedenen Authentifizierungstypen zu erhalten, die Sie für Ihre Quelle verwenden können.
   * Lesen Sie das Handbuch unter [Quellspezifikationen konfigurieren](./config/sourcespec.md) Informationen zu den verschiedenen Paginierungstypen, Planungsformaten und benutzerdefinierten Schemata, die für Ihre Quelle konfiguriert werden können.
   * Lesen Sie das Handbuch unter [Konfigurieren von Discover-Spezifikationen](./config/explorespec.md) für Informationen zur Definition der Parameter, die zum Erkunden und Überprüfen von Objekten in Ihrer Quelle erforderlich sind.
* Um mit der Dokumentation Ihrer Quelle zu beginnen, lesen Sie die [Übersicht über das Erstellen der Dokumentation für Self-Serve-Quellen](./documentation/doc-overview.md)
   * Sie können dies [Quellen-API-Dokumentationsvorlage](./documentation/template.md) , um Ihre API-Dokumentation zu strukturieren.
   * Sie können dies [Dokumentationsvorlage zur Quellenbenutzeroberfläche](./documentation/ui-template.md) , um die Dokumentation zur Benutzeroberfläche zu strukturieren.
   * Siehe Handbuch unter [Verwenden der GitHub-Webschnittstelle](./documentation/github.md) für Schritte zum Erstellen der Dokumentation mit GitHub.
   * Siehe Handbuch unter [mit einem Texteditor](./documentation/text-editor.md) Anweisungen zum Erstellen von Dokumentationen mit Ihrem lokalen Computer.
