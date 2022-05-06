---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
solution: Experience Platform
title: Erste Schritte mit dem Quellen-SDK (Beta)
topic-legacy: developer guide
description: Dieses Dokument bietet eine Einführung in die erforderlichen Informationen, die Sie kennen müssen, bevor Sie versuchen, eine neue Quelle mit dem Quellen-SDK zu erstellen.
hide: true
hidefromtoc: true
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 63%

---

# Erste Schritte mit dem Quellen-SDK (Beta)

>[!IMPORTANT]
>
>Das Quellen-SDK befindet sich derzeit in der Beta-Phase und Ihre Organisation hat möglicherweise noch keinen Zugriff darauf. Die in dieser Dokumentation beschriebene Funktionalität kann sich ändern.

Mit dem Sources-SDK können Sie Ihre eigene REST-basierte Quelle integrieren, um Daten an Adobe Experience Platform zu übertragen. In diesem Dokument erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen sollten, bevor Sie Aufrufe an die [[!DNL Flow Service] -API durchführen](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Voraussetzungen

Um das Sources-SDK zu verwenden, müssen Sie sicherstellen, dass Sie Zugriff auf eine mit Adobe Experience Platform-Quellen bereitgestellte Sandbox der IMS-Organisation haben.

Dieses Handbuch setzt außerdem ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Lesen von Beispiel-API-Aufrufen

Das Quellen-SDK und [!DNL Flow Service] Die API-Dokumentation enthält Beispiel-API-Aufrufe, die zeigen, wie Sie Ihre Anfragen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

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

Informationen zum Erstellen einer neuen Quelle mit dem Quellen-SDK finden Sie im Tutorial zu [Erstellen einer neuen Quelle](./create.md).
