---
keywords: Experience Platform;Startseite;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;API
solution: Experience Platform
title: Erste Schritte mit der Segmentierungsdienst-API
topic-legacy: developer guide
description: Die folgende Dokumentation enthält zusätzliche Informationen, die Sie benötigen, um erfolgreich mit der Segmentierungs-API arbeiten zu können.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 20%

---

# Erste Schritte mit der Segmentierungsdienst-API {#getting-started}

Mit Adobe Experience Platform [!DNL Segmentation Service] können Sie Segmente erstellen und Audiencen in Adobe Experience Platform aus Ihren [!DNL Real-time Customer Profile]-Daten generieren.

Das Entwicklerhandbuch erfordert ein Verständnis der verschiedenen [!DNL Experience Platform]-Dienste, die mit der Verwendung von [!DNL Segmentation Service] verbunden sind.

- [[!DNL Segmentation]](../home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus  [!DNL Real-time Customer Profile] Daten.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
- [Sandboxen](../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne  [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich mit der [!DNL Segmentation]-API arbeiten zu können.

## Lesen von Beispiel-API-Aufrufen

Die [!DNL Segmentation Service]-API-Dokumentation enthält Beispiel-API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Fehlerbehebungshandbuch für [!DNL Experience Platform]

## Erforderliche Kopfzeilen

Die API-Dokumentation erfordert auch, dass Sie das [Authentifizierungstraining](https://www.adobe.com/go/platform-api-authentication-en) abgeschlossen haben, um erfolgreich Aufrufe an [!DNL Platform]-Endpunkte durchzuführen. Wenn Sie das Authentifizierungstreutorial abschließen, werden die Werte für die einzelnen erforderlichen Kopfzeilen in [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang stattfinden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zum Arbeiten mit Sandboxes in [!DNL Experience Platform] finden Sie in der [Übersicht über Sandboxen](../../sandboxes/home.md).

## Nächste Schritte

Um Aufrufe mit der [!DNL Segmentation Service]-API durchzuführen, wählen Sie eine der verfügbaren Endpunktleitfäden entweder mit der linken Navigation oder im [Übersicht über das Entwicklerhandbuch](./overview.md) aus
