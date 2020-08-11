---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Getting started with the Policy Service API
topic: developer guide
translation-type: tm+mt
source-git-commit: cb3a17aa08c67c66101cbf3842bf306ebcca0305
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 23%

---


# Getting started with the [!DNL Policy Service] API

Mit der [!DNL Policy Service] API können Sie verschiedene Ressourcen im Zusammenhang mit Adobe Experience Platform erstellen und verwalten [!DNL Data Governance]. This document provides an introduction to the core concepts you need to know before attempting to make calls to the [!DNL Policy Service] API.

## Voraussetzungen 

Die Verwendung des Entwicklerhandbuchs erfordert ein grundlegendes Verständnis der verschiedenen [!DNL Experience Platform] Dienste, die beim Arbeiten mit Data Governance-Funktionen erforderlich sind. Before beginning to work with the [!DNL Policy Service API], please review the documentation for the following services:

* [[!DNL-Datenverwaltung]](../home.md): Das Framework, mit dem die Einhaltung der Datenverwendung [!DNL Experience Platform] erzwungen wird.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
* [[!DNL Echtzeit-Profil]](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] provides virtual sandboxes which partition a single [!DNL Platform] instance into separate virtual environments to help develop and evolve digital experience applications.

## Lesen von Beispiel-API-Aufrufen

The [!DNL Policy Service] API documentation provides example API calls to demonstrate how to format your requests. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

## Erforderliche Kopfzeilen

The API documentation also requires you to have completed the [authentication tutorial](../../tutorials/authentication.md) in order to successfully make calls to [!DNL Platform] endpoints. Completing the authentication tutorial provides the values for each of the required headers in [!DNL Experience Platform] API calls, as shown below:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Data Governance], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* `Content-Type: application/json`

## Kernressourcen und benutzerdefinierte Ressourcen

Within the [!DNL Policy Service] API, all policies and marketing actions are referred to as either `core` or `custom` resources.

`core` Ressourcen sind die von der Adobe definierten und verwalteten Ressourcen, während `custom` Ressourcen von Ihrer Organisation erstellt und verwaltet werden und daher einmalig und nur für Ihre IMS-Organisation sichtbar sind. Darum sind Auflistungs- und Nachschlagevorgänge (`GET`) die einzigen Vorgänge, die bei `core`-Ressourcen zulässig sind, während bei `custom`-Ressourcen Auflistungs-, Nachschlage- und Aktualisierungsvorgänge (`POST`, `PUT`, `PATCH` und `DELETE`) verfügbar sind.

## Nächste Schritte

Um mit dem Aufrufen der Policy Service API zu beginnen, wählen Sie eine der verfügbaren Endpunktleitfäden aus.