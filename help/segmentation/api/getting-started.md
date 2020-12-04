---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;api;
solution: Experience Platform
title: Entwicklerhandbuch für Segmentation Service
topic: developer guide
description: Die folgende Dokumentation enthält zusätzliche Informationen, die Sie benötigen, um erfolgreich mit der Segmentierungs-API arbeiten zu können.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 22%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

Mit Adobe Experience Platform [!DNL Segmentation Service] können Sie Segmente erstellen und aus Ihren [!DNL Real-time Customer Profile] Daten Audiencen in Adobe Experience Platform generieren.

Das Entwicklerhandbuch erfordert ein funktionierendes Verständnis der verschiedenen [!DNL Experience Platform] Dienste, die mit der Verwendung verbunden sind [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus [!DNL Real-time Customer Profile] Daten.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
- [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully work with the [!DNL Segmentation] API.

## Lesen von Beispiel-API-Aufrufen

The [!DNL Segmentation Service] API documentation provides example API calls to demonstrate how to format your requests. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

## Erforderliche Kopfzeilen

The API documentation also requires you to have completed the [authentication tutorial](../../tutorials/authentication.md) in order to successfully make calls to [!DNL Platform] endpoints. Completing the authentication tutorial provides the values for each of the required headers in [!DNL Experience Platform] API calls, as shown below:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox in which the operation will take place:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on working with sandboxes in [!DNL Experience Platform], see the [sandboxes overview documentation](../../sandboxes/home.md).

## Nächste Schritte

Um Aufrufe mithilfe der [!DNL Segmentation Service] API durchzuführen, wählen Sie eine der verfügbaren Endpunkthandbücher entweder über die linke Navigation oder im [Entwicklerhandbuch aus](./overview.md)