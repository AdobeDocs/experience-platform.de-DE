---
keywords: Experience Platform; Startseite; beliebte Themen; Quellen; Connectoren; Quell-Connectoren; Quellen-SDK; SDK
solution: Experience Platform
title: Quellen-SDK - Überblick (Beta)
topic-legacy: overview
description: Das Adobe Experience Platform Sources-SDK ist eine Reihe von Konfigurations-APIs, mit denen Sie eine REST-API-basierte Quelle mithilfe der Flow Service-API integrieren können, um Ihre Daten in die Experience Platform zu übertragen.
hide: true
hidefromtoc: true
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: ce902e461c748e30e0307558da894a4dbdd212a4
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 8%

---

# Quellen-SDK - Übersicht (Beta)

>[!IMPORTANT]
>
>Das Quellen-SDK befindet sich derzeit in der Beta-Phase und Ihr Unternehmen hat möglicherweise noch keinen Zugriff darauf. Die in dieser Dokumentation beschriebene Funktionalität kann sich ändern.

Das Adobe Experience Platform Sources-SDK ist ein Satz von Konfigurations-APIs, mit denen Sie eine REST-API-basierte Quelle mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) , um Ihre Daten in die Experience Platform zu übertragen.

Mit dem Sources-SDK können Sie:

* Konfigurieren Sie eine neue Quelle für den Platform-Katalog, einschließlich der Funktionen zum Erstellen, Lesen, Aktualisieren und Löschen mithilfe des [!DNL Flow Service] API.
* Definieren Sie Spezifikationen für Ihre Quelle, einschließlich Informationen zu unterstützten Authentifizierungstypen und dazu, wie Ressourcendaten abgerufen werden.
* Erstellen Sie eine benutzerfreundliche Dokumentation für Ihre neue Quelle.

Die Dokumentation zum Sources-SDK enthält Anweisungen zur Verwendung des Adobe Experience Platform Sources-SDK zum Konfigurieren, Testen und Veröffentlichen einer REST API-basierten Quellintegration mit Platform und dazu, dass Ihre Quelle Teil des ständig wachsenden Quellkatalogs wird.

![Katalog](./assets/catalog.png)

## Grundlagen zu Quellen

Mit Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Weitere Informationen zu Quellen und eine Liste der verschiedenen Quellen, die derzeit auf Platform unterstützt werden, finden Sie unter [Quellen - Übersicht](../home.md).

## Erstellen einer Quelle

Über das Sources-SDK können Sie Ihre eigene REST-API-basierte Quelle integrieren und Ihre Daten an Platform übertragen mit [!DNL Flow Service]. Mit dem Quellen-SDK können Sie eine neue Quelle in Platform integrieren, indem Sie neue Verbindungsspezifikationen über das [!DNL Flow Service] API.

Siehe Handbuch unter [Erstellen einer neuen Verbindungsspezifikation](./api/api-overview.md) Informationen zur Integration einer neuen Quelle in Platform.

## Quelle dokumentieren

Nachdem die Quelle erstellt wurde, lesen Sie den Abschnitt [Handbuch](./documentation/doc-overview.md) Anweisungen zum Dokumentieren der Quelle über das [!DNL GitHub] Web-Oberfläche oder über Ihren eigenen Texteditor.

## Verfahren auf hoher Ebene

Der Schritt-für-Schritt-Vorgang zum Konfigurieren der Quelle in Experience Platform ist unten beschrieben:

* Lesen Sie die [API-Handbuch für Quellen-SDK](./api/api-overview.md);
   * Lesen Sie die [Erste Schritte](./api/getting-started.md);
   * Folgen Sie dem Tutorial zu [Erstellen einer neuen Verbindungsspezifikation](./api/create.md);
   * Folgen Sie dem Tutorial zu [Aktualisieren der Verbindungsspezifikation](./api/update-connection-specs.md);
   * Folgen Sie dem Tutorial zu [Hinzufügen der neuen Verbindungsspezifikations-ID zu einer Flussspezifikation](./api/update-flow-specs.md)
   * [Neue Quelle senden](./api/submit.md).
* Um ein besseres Verständnis der Struktur und Eigenschaften einer Verbindungsspezifikation zu erhalten, lesen Sie das Handbuch unter [Konfigurationsoptionen für das Quellen-SDK](./config/config.md);
   * Siehe Handbuch unter [Authentifizierungsspezifikationen konfigurieren](./config/authspec.md);
   * Siehe Handbuch unter [Quellspezifikationen konfigurieren](./config/sourcespec.md);
   * Siehe Handbuch unter [Konfigurieren von Discover-Spezifikationen](./config/explorespec.md);
* Informationen zum Dokumentieren der Quelle finden Sie unter [Übersicht über das Erstellen der Dokumentation für das Quellen-SDK](./documentation/doc-overview.md)
   * Sie können dies [Quellen-API-Dokumentationsvorlage](./documentation/template.md) die Struktur der API-Dokumentation;
   * Sie können dies [Dokumentationsvorlage zur Quellenbenutzeroberfläche](./documentation/ui-template.md) zur Strukturierung der Benutzeroberflächendokumentation;
   * Siehe Handbuch unter [Verwenden der GitHub-Webschnittstelle](./documentation/github.md) Anweisungen zum Erstellen der Dokumentation mit GitHub;
   * Siehe Handbuch unter [mit einem Texteditor](./documentation/text-editor.md) Anweisungen zum Erstellen von Dokumentationen mit Ihrem lokalen Computer.
