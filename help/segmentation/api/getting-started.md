---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für Segmentation Service
topic: developer guide
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 21%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

Mit der Adobe Experience Platform [!DNL Segmentation Service] können Sie Segmente erstellen und Audiencen in Adobe Experience Platform aus Ihren [!DNL Real-time Customer Profile] Daten generieren.

Das Entwicklerhandbuch erfordert ein funktionierendes Verständnis der verschiedenen [!DNL Experience Platform] Dienste, die mit der Verwendung verbunden sind [!DNL Segmentation Service].

- [!DNL Segmentation](../home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus [!DNL Real-time Customer Profile] Daten.
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
- [!DNL Real-time Customer Profile](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
- [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully work with the [!DNL Segmentation] API.

## Lesehilfe für Beispiel-API-Aufrufe

The [!DNL Segmentation Service] API documentation provides example API calls to demonstrate how to format your requests. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Die in der Dokumentation zu Beispielen für API-Aufrufe verwendeten Konventionen werden im Handbuch zur Fehlerbehebung für unter [Lesehilfe für Beispiel-API-Aufrufe](../../landing/troubleshooting.md#how-do-i-format-an-api-request) erläutert.[!DNL Experience Platform]

## Erforderliche Kopfzeilen

The API documentation also requires you to have completed the [authentication tutorial](../../tutorials/authentication.md) in order to successfully make calls to [!DNL Platform] endpoints. Completing the authentication tutorial provides the values for each of the required headers in [!DNL Experience Platform] API calls, as shown below:

- Autorisierung: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox in which the operation will take place:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on working with sandboxes in [!DNL Experience Platform], see the [sandboxes overview documentation](../../sandboxes/home.md).

## Nächste Schritte

Um Aufrufe mithilfe der [!DNL Segmentation Service] API durchzuführen, wählen Sie eine der verfügbaren Endpunkthandbücher entweder über die linke Navigation oder im [Entwicklerhandbuch aus](./overview.md)