---
keywords: Experience Platform;home;popular topics;DULE;dule
solution: Experience Platform
title: Erste Schritte mit der Policy Service API
topic: developer guide
description: Mit der Policy Service API können Sie verschiedene Ressourcen im Zusammenhang mit der Adobe Experience Platform-Datenverwaltung erstellen und verwalten. In diesem Dokument erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen sollten, bevor Sie Aufrufe an die Policy Service-API durchführen.
translation-type: tm+mt
source-git-commit: 3376d6cace9ab196f457e2bf7b84cde06693103c
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 29%

---


# Getting started with the [!DNL Policy Service] API

Mit der [!DNL Policy Service] API können Sie verschiedene Ressourcen im Zusammenhang mit Adobe Experience Platform erstellen und verwalten [!DNL Data Governance]. This document provides an introduction to the core concepts you need to know before attempting to make calls to the [!DNL Policy Service] API.

## Voraussetzungen 

Die Verwendung des Entwicklerhandbuchs erfordert ein grundlegendes Verständnis der verschiedenen [!DNL Experience Platform] Dienste, die beim Arbeiten mit Data Governance-Funktionen erforderlich sind. Before beginning to work with the [!DNL Policy Service API], please review the documentation for the following services:

* [[!DNL Data Governance]](../home.md): Das Framework, mit dem die Einhaltung der Datenverwendung [!DNL Experience Platform] erzwungen wird.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

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