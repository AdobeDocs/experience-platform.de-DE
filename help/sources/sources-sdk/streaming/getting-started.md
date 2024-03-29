---
title: Erste Schritte mit Self-Serve-Quellen (Streaming-SDK)
description: Dieses Dokument bietet eine Einführung in die erforderlichen Informationen, die Sie kennen müssen, bevor Sie versuchen, eine neue Quelle mit Self-Serve-Quellen (Streaming-SDK) zu erstellen.
exl-id: 6cc13279-ce0b-45bc-ad25-e2e6aafc2af0
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 34%

---

# Erste Schritte mit Self-Serve-Quellen (Streaming-SDK)

>[!NOTE]
>
>Das Streaming-SDK für Self-Serve-Quellen befindet sich in der Beta-Phase. Bitte lesen Sie die [Quellen - Übersicht](../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

Self-Serve-Quellen (Streaming-SDK) ermöglichen Ihnen die Integration Ihrer eigenen Quelle, um Streaming-Daten an Adobe Experience Platform zu übertragen. Dieses Dokument bietet eine Einführung in die grundlegenden Konzepte, die Sie kennen müssen, bevor Sie Aufrufe an die [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Allgemeine Vorgehensweise

Der Schritt-für-Schritt-Vorgang zum Konfigurieren der Quelle unter Experience Platform ist unten beschrieben:

### Integration

* [Neue Verbindungsspezifikation für Streaming SDK erstellen](create.md).
* [Aktualisieren der Streaming-Flussspezifikation mit Ihrer neuen Verbindungsspezifikations-ID](update-flow-specs.md).
* [Streaming-Quelle testen und senden](submit.md).

### Dokumentation

* Um mit der Dokumentation Ihrer Quelle zu beginnen, lesen Sie die [Übersicht über das Erstellen der Dokumentation für Self-Serve-Quellen](../documentation/doc-overview.md).
* Lesen Sie das Handbuch unter [Verwenden der GitHub-Web-Oberfläche](../documentation/github.md) für Schritte zum Erstellen der Dokumentation mit GitHub.
* Lesen Sie das Handbuch unter [mit einem Texteditor](../documentation/text-editor.md) Anweisungen zum Erstellen von Dokumentationen mit Ihrem lokalen Computer.
* [Verwenden Sie die Dokumentationsvorlage zur Streaming-SDK-API, um Ihre Quelle in der API zu dokumentieren.](streaming-template-api.md).
* [Verwenden Sie die Dokumentationsvorlage zur Streaming-SDK-Benutzeroberfläche, um Ihre Quelle in der Benutzeroberfläche zu dokumentieren.](streaming-template-ui.md).

Sie können auch die folgenden Dokumentationsvorlagen herunterladen:

* [API-Dokumentationsvorlage](../assets/streaming/streaming-template-api.zip)
* [Benutzeroberflächendokumentationsvorlage](../assets/streaming/streaming-template-ui.zip)

## Voraussetzungen

>[!IMPORTANT]
>
>Die Quelle, die Sie mit Experience Platform integrieren, muss in der Lage sein, einen Webhook zu unterstützen, für den ein Endpunkt angemeldet werden kann, um Updates zu senden.

Um Self-Serve-Quellen (Streaming-SDK) zu verwenden, müssen Sie sicherstellen, dass Sie Zugriff auf eine Sandbox-Organisation haben, die über Adobe Experience Platform-Quellen verfügt.

Dieses Handbuch setzt außerdem ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Lesen von Beispiel-API-Aufrufen

Die Self-Serve-Quellen (Streaming-SDK) und [!DNL Flow Service] Die API-Dokumentation enthält Beispiel-API-Aufrufe, die zeigen, wie Sie Ihre Anfragen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

## Sammeln von Werten für erforderliche Kopfzeilen

Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in Platform, einschließlich derjenigen, die zu [!DNL Flow Service], werden auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in Platform finden Sie unter [Sandbox-Dokumentation](../../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* `Content-Type: application/json`

## Nächste Schritte

Informationen zum Erstellen einer neuen Quelle mit Self-Serve-Quellen (Streaming-SDK) finden Sie im Tutorial zu [Erstellen einer neuen Quelle](./create.md).
