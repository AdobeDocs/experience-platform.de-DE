---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
solution: Experience Platform
title: Übersicht über Selbstbedienungsquellen (Batch-SDK)
description: Adobe Experience Platform-Selbstbedienungsquellen (Batch-SDK) sind eine Reihe von Konfigurations-APIs, mit denen Sie eine REST-API-basierte Quelle mithilfe der Flow Service-API integrieren können, um Ihre Daten auf den Experience Platform zu bringen.
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 7%

---

# Übersicht über Selbstbedienungsquellen (Batch-SDK)

Adobe Experience Platform-Selbstbedienungsquellen (Batch-SDK) sind ein Framework, mit dem Sie eine REST-API-basierte Quelle mithilfe der -API in den Experience Platform-[[!DNL Flow Service]  integrieren ](https://www.adobe.io/experience-platform-apis/references/flow-service/). Self-Service Sources (Batch-SDK) bietet eine Reihe von Konfigurations-APIs, um Ihre eigene Quelle zu erstellen und Ihre Batch-Daten auf Experience Platform zu bringen.

Mit Selbstbedienungsquellen (Batch-SDK) können Sie:

* Konfigurieren und Integrieren einer neuen Quelle in den Experience Platform-Katalog mithilfe der [!DNL Flow Service]-API.
* Definieren Sie Spezifikationen für Ihre Quelle, einschließlich Informationen zu unterstützten Authentifizierungstypen und dazu, wie Ressourcendaten abgerufen werden.
* Erstellen Sie eine benutzerfreundliche Dokumentation für Ihre neue Quelle.

Die Dokumentation zu Selbstbedienungsquellen enthält Anweisungen zum Konfigurieren, Testen und Freigeben einer REST-API-basierten Quellintegration mit Experience Platform, sodass Ihre Quelle Teil des ständig wachsenden Quellkatalogs wird.

![Katalog](./assets/catalog.png)

## Verstehen von Quellen

Experience Platform kann Daten aus externen Quellen aufnehmen und ermöglicht es Ihnen, diese Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und zu verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Weitere Informationen zu Quellen und eine Liste der verschiedenen derzeit auf Experience Platform unterstützten Quellen finden Sie unter [Quellen - Übersicht](../home.md).

## Erstellen einer Quelle

Über Self-Service-Quellen können Sie Ihre eigene REST-API-basierte Quelle integrieren und Ihre Daten mit [!DNL Flow Service] auf Experience Platform bringen. Sie können eine Quelle in den Experience Platform-Quellkatalog integrieren, indem Sie neue Verbindungsspezifikationen über die [!DNL Flow Service]-API erstellen, konfigurieren und senden.

Informationen zum Integrieren einer neuen [ auf Experience Platform finden Sie ](./api/api-overview.md) Handbuch unter „Erstellen einer neuen Verbindungsspezifikation .

## Dokumentieren der Quelle

Nachdem Sie Ihre Quelle erstellt haben, finden Sie im [Dokumentationshandbuch](./documentation/doc-overview.md) Anweisungen, wie Sie Ihre Quelle über die [!DNL GitHub] Web-Oberfläche oder Ihren eigenen Texteditor dokumentieren.

## Allgemeine Vorgehensweise

Der schrittweise Prozess zum Konfigurieren Ihrer Quelle auf Experience Platform wird unten beschrieben:

* Lesen Sie [ API-Handbuch für Selbstbedienungsquellen (Batch-SDK](./api/api-overview.md).
   * Lesen Sie [Erste Schritte](./api/getting-started.md).
   * Befolgen Sie das Tutorial [Erstellen einer neuen Verbindungsspezifikation](./api/create.md).
   * Befolgen Sie das Tutorial [Aktualisieren Ihrer Verbindungsspezifikation](./api/update-connection-specs.md).
   * Befolgen Sie das Tutorial [Hinzufügen Ihrer neuen Verbindungsspezifikations-ID zu einer Flussspezifikation](./api/update-flow-specs.md)
   * [Neue Quelle übermitteln](./api/submit.md).
* Um ein besseres Verständnis der Struktur und der Eigenschaften einer Verbindungsspezifikation zu erhalten, lesen Sie das Handbuch [Konfigurationsoptionen für Selbstbedienungsquellen (Batch-SDK)](./config/config.md).
   * Lesen Sie das Handbuch unter [Konfigurieren Ihrer Authentifizierungsspezifikationen](./config/authspec.md) um ein besseres Verständnis der verschiedenen Authentifizierungstypen zu erhalten, die Sie für Ihre Quelle verwenden können.
   * Lesen Sie das Handbuch unter [Konfigurieren Ihrer Quellspezifikationen](./config/sourcespec.md) für Informationen zu den verschiedenen Paginierungstypen, Zeitplanformaten und benutzerdefinierten Schemata, die für Ihre Quelle konfiguriert werden können.
   * Lesen Sie das Handbuch unter [Konfigurieren Ihrer Erkundungsspezifikationen](./config/explorespec.md) für Informationen zum Definieren der Parameter, die zum Untersuchen und Überprüfen von in Ihrer Quelle enthaltenen Objekten erforderlich sind.
* Um mit der Dokumentation Ihrer Quelle zu beginnen, lesen Sie [Übersicht über das Erstellen der Dokumentation für Selbstbedienungsquellen](./documentation/doc-overview.md)
   * Sie können diese [Quellen-API-Dokumentationsvorlage](./documentation/template.md) zur Strukturierung Ihrer API-Dokumentation verwenden.
   * Sie können diese [Dokumentationsvorlage für die Quell-Benutzeroberfläche](./documentation/ui-template.md) verwenden, um Ihre Benutzeroberflächendokumentation zu strukturieren.
   * Anweisungen zum Erstellen [ Dokumentation mit GitHub finden Sie im Handbuch ](./documentation/github.md)Verwenden der GitHub-Web-Benutzeroberfläche“.
   * Anweisungen zum Erstellen [ Dokumentation auf Ihrem lokalen Computer finden Sie ](./documentation/text-editor.md) Handbuch unter „Verwenden eines Texteditors“.
