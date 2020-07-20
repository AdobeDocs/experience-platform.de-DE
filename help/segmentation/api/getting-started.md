---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für Segmentation Service
topic: developer guide
translation-type: tm+mt
source-git-commit: aff81a4f3243ef77cbdfc776220a5de46e360084
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 42%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

Mit dem Segmentierungsdienst für Adobe Experience Platformen können Sie Segmente erstellen und Audiencen in Adobe Experience Platform aus Ihren [!DNL Real-time Customer Profile] Daten generieren.

The developer guide requires a working understanding of the various Experience Platform services involved with using [!DNL Segmentation Service].

- [!DNL Segmentation](../home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus Echtzeitdaten zum Profil von Kunden.
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
- [!DNL Real-time Customer Profile](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
- [Sandbox-Umgebungen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen für die Entwicklung und Erweiterung von Anwendungen für digitale Erlebnisse unterteilen.

The following sections provide additional information that you will need to know in order to successfully work with the [!DNL Segmentation] API.

## Lesehilfe für Beispiel-API-Aufrufe

The [!DNL Segmentation Service] API documentation provides example API calls to demonstrate how to format your requests. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung in Experience Platform.

## Erforderliche Kopfzeilen

Außerdem setzt die API-Dokumentation voraus, dass Sie das [Authentifizierungs-Tutorial](../../tutorials/authentication.md) abgeschlossen haben, um Platform-Endpunkte erfolgreich aufrufen zu können. Wenn Sie das Authentifizierungs-Tutorial absolvieren, erhalten Sie die Werte für jede der erforderlichen Kopfzeilen in Experience Platform-API-Aufrufen, wie unten dargestellt:

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