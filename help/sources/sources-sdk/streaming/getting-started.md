---
title: Erste Schritte mit Selbstbedienungsquellen (Streaming-SDK)
description: In diesem Dokument erhalten Sie eine Einführung in die erforderlichen Informationen, die Sie kennen sollten, bevor Sie versuchen, eine neue Quelle mithilfe von Selbstbedienungsquellen (Streaming-SDK) zu erstellen.
exl-id: 6cc13279-ce0b-45bc-ad25-e2e6aafc2af0
badge: Beta
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 34%

---

# Erste Schritte mit Selbstbedienungsquellen (Streaming-SDK)

>[!NOTE]
>
>Selbstbedienungsquellen-Streaming SDK befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../home.md#terms-and-conditions) „Quellen - Übersicht“.

Mit Selbstbedienungsquellen (Streaming-SDK) können Sie Ihre eigene Quelle integrieren, um Streaming-Daten an Adobe Experience Platform zu übertragen. In diesem Dokument erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen sollten, bevor Sie Aufrufe an die [[!DNL Flow Service] API) ](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Allgemeine Vorgehensweise

Der schrittweise Prozess zum Konfigurieren Ihrer Quelle auf Experience Platform wird unten beschrieben:

### Integration

* [Erstellen Sie eine neue Verbindungsspezifikation für Streaming-SDK](create.md).
* [Aktualisieren der Streaming-Flussspezifikation mit Ihrer neuen Verbindungsspezifikations-ID](update-flow-specs.md).
* [Testen und Senden Ihrer Streaming-Quelle](submit.md).

### Dokumentation

* Um mit der Dokumentation Ihrer Quelle zu beginnen, lesen Sie [Übersicht über das Erstellen der Dokumentation für Selbstbedienungsquellen](../documentation/doc-overview.md).
* Anweisungen zum Erstellen [ Dokumentation mit GitHub finden Sie im Handbuch unter ](../documentation/github.md)Verwenden der GitHub-Web-Benutzeroberfläche“.
* Anweisungen zum Erstellen [ Dokumentation auf Ihrem lokalen Computer finden Sie ](../documentation/text-editor.md) Handbuch unter „Verwenden eines Texteditors“.
* [Verwenden Sie die Dokumentationsvorlage für die Streaming-SDK-API , um Ihre Quelle in der API zu dokumentieren](streaming-template-api.md).
* [Verwenden Sie die Dokumentationsvorlage für die Streaming-SDK-Benutzeroberfläche, um Ihre Quelle in der Benutzeroberfläche zu dokumentieren](streaming-template-ui.md).

Sie können auch die folgenden Dokumentationsvorlagen herunterladen:

* [API-Dokumentationsvorlage](../assets/streaming/streaming-template-api.zip)
* [Dokumentationsvorlage für die Benutzeroberfläche](../assets/streaming/streaming-template-ui.zip)

## Voraussetzungen

>[!IMPORTANT]
>
>Die Quelle, die Sie mit Experience Platform integrieren, muss einen Webhook unterstützen können, für den ein Endpunkt abonniert werden kann, um Aktualisierungen zu senden.

Um Selbstbedienungsquellen (Streaming-SDK) verwenden zu können, müssen Sie sicherstellen, dass Sie Zugriff auf eine Sandbox-Organisation haben, die mit Adobe Experience Platform-Quellen bereitgestellt ist.

Dieses Handbuch setzt außerdem ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Lesen von Beispiel-API-Aufrufen

In der Dokumentation zu den Selbstbedienungsquellen (Streaming-SDK) und der [!DNL Flow Service]-API wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

## Sammeln von Werten für erforderliche Kopfzeilen

Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in Platform, einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, sind in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Dokumentation](../../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* `Content-Type: application/json`

## Nächste Schritte

Informationen zum Erstellen einer neuen Quelle mit Selbstbedienungsquellen (Streaming-SDK) finden Sie im Tutorial [Erstellen einer neuen Quelle](./create.md).
