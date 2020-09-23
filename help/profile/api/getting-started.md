---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: Erste Schritte mit der Echtzeit-Profil-API
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 22%

---


# Getting started with the [!DNL Real-time Customer Profile] API {#getting-started}

Using the [!DNL Real-time Customer Profile] API, you can perform basic CRUD operations against Profile resources, such as configuring computed attributes, accessing entities, exporting Profile data, and deleting unneeded datasets or batches.

Using the developer guide requires a working understanding of the various Adobe Experience Platform services involved in working with [!DNL Profile] data. Before beginning to work with the [!DNL Real-time Customer Profile] API, please review the documentation for the following services:

* [[!DNL Echtzeit-Profil]](../home.md): Bietet ein einheitliches, kundenspezifisches Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Erhalten Sie eine bessere Ansicht Ihres Kundenverhaltens, indem Sie Identitäten zwischen verschiedenen Geräten und Systemen überbrücken.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus Echtzeitdaten zum Profil von Kunden.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully make calls to [!DNL Profile] API endpoints.

## Lesen von Beispiel-API-Aufrufen

The [!DNL Real-time Customer Profile] API documentation provides example API calls to demonstrate how to properly format requests. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

## Erforderliche Kopfzeilen

The API documentation also requires you to have completed the [authentication tutorial](../../tutorials/authentication.md) in order to successfully make calls to [!DNL Platform] endpoints. Completing the authentication tutorial provides the values for each of the required headers in [!DNL Experience Platform] API calls, as shown below:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. Requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* `x-sandbox-name: {SANDBOX_NAME}`

For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Alle Anfragen mit einer Payload im Anfragetext (wie POST-, PUT- und PATCH-Aufrufe) müssen eine `Content-Type`-Kopfzeile enthalten. Akzeptierte Werte, die für jeden Aufruf spezifisch sind, werden in den Aufrufparametern angegeben.

## Nächste Schritte

Um mit dem Aufrufen der [!DNL Real-time Customer Profile] API zu beginnen, wählen Sie eine der verfügbaren Endpunktleitfäden aus.