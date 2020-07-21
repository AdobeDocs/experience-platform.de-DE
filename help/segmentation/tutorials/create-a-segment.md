---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Segments
topic: tutorial
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 12%

---


# Erstellen eines Segments

Dieses Dokument bietet eine Anleitung zum Entwickeln, Testen, Anzeigen einer Segmentdefinition und zum Speichern einer Segmentdefinition mithilfe der [DNL-Adobe Experience Platform-Segmentierungsdienst-API](../api/getting-started.md).

Informationen zum Erstellen von Segmenten mithilfe der Benutzeroberfläche finden Sie im Handbuch [Segmentaufbau](../ui/overview.md).

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der verschiedenen [!DNL Adobe Experience Platform] Dienste, die beim Erstellen von Segmenten für die Audience erforderlich sind. Bevor Sie mit dem Tutorial beginnen, lesen Sie bitte die Dokumentation für folgende Dienste:

- [!DNL Real-time Customer Profile](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
- [!DNL Adobe Experience Platform Segmentation Service](../home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus Echtzeitdaten zum Profil von Kunden.
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Platform] organisiert werden.

The following sections provide additional information that you will need to know in order to successfully make calls to the [!DNL Platform] APIs.

### Lesehilfe für Beispiel-API-Aufrufe

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Die in der Dokumentation zu Beispielen für API-Aufrufe verwendeten Konventionen werden im Handbuch zur Fehlerbehebung für unter [Lesehilfe für Beispiel-API-Aufrufe](../../landing/troubleshooting.md#how-do-i-format-an-api-request) erläutert.[!DNL Experience Platform]

### Werte der zu verwendenden Kopfzeilen

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Alle Anfragen, die eine Payload enthalten (also POST-, PUT- und PATCH-Anfragen), erfordern eine zusätzliche Kopfzeile:

- Content-Type: application/json

## Entwickeln einer Segmentdefinition

Der erste Schritt bei der Segmentierung besteht darin, ein Segment zu definieren, das in einem Konstrukt namens **Segmentdefinition** dargestellt wird. Eine Segmentdefinition ist ein Objekt, das eine in [!DNL Profile Query Language] (PQL) geschriebene Abfrage kapselt. Dieses Objekt wird auch als **PQL-Vorhersage** bezeichnet. PQL-Prädikate definieren die Regeln für das Segment basierend auf Bedingungen, die sich auf die Daten aus Datensatz oder Zeitreihen beziehen, die Sie bereitstellen [!DNL Real-time Customer Profile]. Weitere Informationen zum Schreiben von PQL-Abfragen finden Sie im [PQL-Handbuch](../pql/overview.md) .

You can create a new segment definition by making a POST request to the `/segment/definitions` endpoint in the [!DNL Segmentation] API. Im folgenden Beispiel wird beschrieben, wie eine Definitionsanforderung formatiert wird, einschließlich der Informationen, die erforderlich sind, damit ein Segment erfolgreich definiert werden kann.

Eine ausführliche Erläuterung zum Definieren eines Segments finden Sie im Entwicklerhandbuch für die [Segmentdefinition](../api/segment-definitions.md#create).

## Schätzung und Vorschau einer Audience {#estimate-and-preview-an-audience}

Bei der Entwicklung Ihrer Segmentdefinition können Sie die Tools für Schätzung und Vorschau innerhalb der Informationen auf der Ebene der Ansicht verwenden, um sicherzustellen, dass Sie die erwartete Audience isolieren. [!DNL Real-time Customer Profile] Schätzungen liefern statistische Informationen zu einer Segmentdefinition, wie zum Beispiel die projizierte Audience und das Konfidenzintervall. Vorschauen bieten paginierte Listen von qualifizierten Profilen für eine Segmentdefinition, mit denen Sie die Ergebnisse mit Ihren Erwartungen vergleichen können.

Durch die Schätzung und Vorschau Ihrer Audience können Sie Ihre PQL-Vorhersagen testen und optimieren, bis sie ein erwünschtes Ergebnis erzielen und dann in einer aktualisierten Segmentdefinition verwendet werden können.

Zur Vorschau oder Schätzung Ihres Segments sind zwei Schritte erforderlich:

1. [Erstellen eines Vorschau-Auftrags](#create-a-preview-job)
2. [Schätzung der Ansicht oder Vorschau](#view-an-estimate-or-preview) mithilfe der ID des Vorschau-Auftrags

### Erstellung von Schätzungen

Mithilfe von Datenmustern können Sie Segmente bewerten und die Anzahl der qualifizierten Profil schätzen. Jeden Morgen werden neue Daten in den Speicher geladen (zwischen 12AM-2AM PT, was 7-9AM UTC entspricht), und alle Abfragen der Segmentierung werden anhand der Musterdaten dieses Tages geschätzt. Daher werden alle neuen Felder, die hinzugefügt oder zusätzliche Daten gesammelt werden, am folgenden Tag in Schätzungen übernommen.

Die Stichprobengröße hängt von der Gesamtanzahl der Entitäten in Ihrem Profil-Store ab. Diese Stichprobengrößen sind in der folgenden Tabelle dargestellt:

| Entitäten im Profil Store | Stichprobengröße |
| ------------------------- | ----------- |
| Weniger als 1 Million | Vollständiger Datensatz |
| 1 bis 20 Mio. | 1 Mio. |
| Über 20 Mio. | 5 % des Gesamtbetrags |

Schätzungen laufen in der Regel über 10-15 Sekunden, beginnend mit einer groben Schätzung und einer Feinabstimmung, wenn mehr Datensätze gelesen werden.

### Erstellen eines Vorschau-Auftrags

You can create a new preview job by making a POST request to the `/preview` endpoint.

Detaillierte Anweisungen zum Erstellen eines Vorschau-Auftrags finden Sie im Handbuch [Vorschauen und Schätzungen-Endpunkte](../api/previews-and-estimates.md#create-preview).

### Ansicht einer Schätzung oder Vorschau

Schätzungs- und Vorschauen-Vorgänge werden asynchron ausgeführt, da unterschiedliche Abfragen unterschiedliche Zeiträume benötigen können. Nachdem eine Abfrage initiiert wurde, können Sie mit API-Aufrufen den aktuellen Status der Schätzung oder Vorschau abrufen (GET), während sie fortschreitet.

Mithilfe der [!DNL Segmentation Service] API können Sie den aktuellen Status eines Vorschau-Auftrags anhand seiner ID nachschlagen. Wenn der Status &quot;RESULT_READY&quot;lautet, können Sie die Ansichten durchführen. Um den aktuellen Status eines Vorschau-Auftrags nachzuschlagen, lesen Sie bitte den Abschnitt zum [Abrufen eines Vorschau-Auftrags](../api/previews-and-estimates.md#get-preview) im Handbuch Vorschauen und geschätzte Endpunkte. Um den aktuellen Status eines Schätzauftrags zu ermitteln, lesen Sie bitte den Abschnitt zum [Abrufen eines Schätzauftrags](../api/previews-and-estimates.md#get-estimate) im Handbuch Vorschauen und geschätzte Endpunkte.


## Nächste Schritte

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie einen Segmentauftrag erstellen, um eine Audience mithilfe der [!DNL Segmentation Service] API zu erstellen. Ausführliche Anweisungen dazu finden Sie im Tutorial zur [Evaluierung und zum Zugriff auf Segmentergebnisse](./evaluate-a-segment.md) .