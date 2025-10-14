---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
solution: Experience Platform
title: Erste Schritte mit Selbstbedienungsquellen (Batch-SDK)
description: In diesem Dokument erhalten Sie eine Einführung in die erforderlichen Informationen, die Sie kennen sollten, bevor Sie versuchen, eine neue Quelle mithilfe von Selbstbedienungsquellen (Batch-SDK) zu erstellen.
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 27%

---

# Erste Schritte mit Selbstbedienungsquellen (Batch-SDK)

Mit Selbstbedienungsquellen (Batch-SDK) können Sie Ihre eigene REST-basierte Quelle integrieren, um Batch-Daten in Adobe Experience Platform zu bringen. In diesem Dokument erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen sollten, bevor Sie Aufrufe an die [[!DNL Flow Service] API) &#x200B;](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Voraussetzungen

Um Selbstbedienungsquellen (Batch-SDK) verwenden zu können, müssen Sie sicherstellen, dass Sie Zugriff auf eine Organisations-Sandbox mit Adobe Experience Platform-Quellen haben.

Dieses Handbuch setzt außerdem ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

## Lesen von Beispiel-API-Aufrufen

In der Dokumentation zu den Selbstbedienungsquellen (Batch-SDK) und der [!DNL Flow Service]-API wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

## Sammeln von Werten für erforderliche Kopfzeilen

Um Experience Platform-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in Experience Platform, einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, sind in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an Experience Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in Experience Platform finden Sie in der [Sandbox-Dokumentation](../../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* `Content-Type: application/json`

## Nächste Schritte

Informationen zum Erstellen einer neuen Quelle mit Selbstbedienungsquellen (Batch-SDK) finden Sie im Tutorial [Erstellen einer neuen Quelle](./create.md).
