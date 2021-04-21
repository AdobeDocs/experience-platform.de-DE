---
keywords: Experience Platform;Startseite;beliebte Themen;Segment;Segment;Segment;Segment erstellen;Segmentierung;Segment erstellen;Segmentierungsdienst;
solution: Experience Platform
title: Erstellen eines Segments mithilfe der Segmentierungsdienst-API
topic-legacy: tutorial
type: Tutorial
description: In diesem Lernprogramm erfahren Sie, wie Sie eine Segmentdefinition mithilfe der Adobe Experience Platform Segmentation Service API entwickeln, testen, testen und speichern.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 15%

---

# Erstellen eines Segments mit der Segmentierungsdienst-API

Dieses Dokument bietet eine Anleitung zum Entwickeln, Testen, Anzeigen einer Vorschau und Speichern einer Segmentdefinition mit dem [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Informationen zum Erstellen von Segmenten mithilfe der Benutzeroberfläche finden Sie im Handbuch [Segmentaufbau](../ui/overview.md).

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der verschiedenen [!DNL Adobe Experience Platform]-Dienste, die beim Erstellen von Audiencen-Segmenten erforderlich sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus Echtzeitdaten zum Profil von Kunden.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen müssen, um die [!DNL Platform]-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Fehlerbehebungshandbuch für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

## Entwickeln einer Segmentdefinition

Der erste Schritt bei der Segmentierung besteht darin, ein Segment zu definieren, das in einem Konstrukt namens Segmentdefinition dargestellt wird. Eine Segmentdefinition ist ein Objekt, das eine in [!DNL Profile Query Language] (PQL) geschriebene Abfrage kapselt. Dieses Objekt wird auch als PQL-Vorhersage bezeichnet. PQL-Prädikate definieren die Regeln für das Segment basierend auf Bedingungen, die sich auf die Daten aus Datensatz oder Zeitreihen beziehen, die Sie an [!DNL Real-time Customer Profile] übermitteln. Weitere Informationen zum Schreiben von PQL-Abfragen finden Sie im Handbuch [PQL.](../pql/overview.md)

Sie können eine neue Segmentdefinition erstellen, indem Sie eine POST an den `/segment/definitions`-Endpunkt in der [!DNL Segmentation]-API anfordern. Im folgenden Beispiel wird beschrieben, wie eine Definitionsanforderung formatiert wird, einschließlich der Informationen, die erforderlich sind, damit ein Segment erfolgreich definiert werden kann.

Eine ausführliche Erläuterung zum Definieren eines Segments finden Sie im [Segment Definition Developer Guide](../api/segment-definitions.md#create).

## Schätzen und Vorschau einer Audience {#estimate-and-preview-an-audience}

Während Sie Ihre Segmentdefinition entwickeln, können Sie die Tools für Schätzung und Vorschau innerhalb von [!DNL Real-time Customer Profile] verwenden, um Informationen auf Ansicht-Zusammenfassungsebene zu erhalten, um sicherzustellen, dass Sie die erwartete Audience isolieren. Schätzungen liefern statistische Informationen zu einer Segmentdefinition, wie zum Beispiel die projizierte Audience und das Konfidenzintervall. Vorschauen bieten paginierte Listen von qualifizierten Profilen für eine Segmentdefinition, mit denen Sie die Ergebnisse mit Ihren Erwartungen vergleichen können.

Durch die Schätzung und Vorschau Ihrer Audience können Sie Ihre PQL-Vorhersagen testen und optimieren, bis sie ein erwünschtes Ergebnis erzielen und dann in einer aktualisierten Segmentdefinition verwendet werden können.

Zur Vorschau oder Schätzung Ihres Segments sind zwei Schritte erforderlich:

1. [Erstellen eines Vorschau-Auftrags](#create-a-preview-job)
2. [Schätzung der Ansicht oder ](#view-an-estimate-or-preview) Vorschau mit der ID des Vorschau-Auftrags

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

Sie können einen neuen Vorschau-Auftrag erstellen, indem Sie eine POST an den `/preview`-Endpunkt anfordern.

Detaillierte Anweisungen zum Erstellen eines Vorschau-Auftrags finden Sie im Handbuch [Vorschauen und geschätzte Endpunkte](../api/previews-and-estimates.md#create-preview).

### Ansicht einer Schätzung oder Vorschau

Schätzungs- und Vorschauen-Vorgänge werden asynchron ausgeführt, da unterschiedliche Abfragen unterschiedliche Zeiträume benötigen können. Nachdem eine Abfrage initiiert wurde, können Sie mit API-Aufrufen den aktuellen Status der Schätzung oder Vorschau abrufen (GET), während sie fortschreitet.

Mit der API [!DNL Segmentation Service] können Sie den aktuellen Status eines Vorschau-Auftrags anhand seiner ID nachschlagen. Wenn der Status &quot;RESULT_READY&quot;lautet, können Sie die Ansicht der Ergebnisse durchführen. Um den aktuellen Status eines Vorschau-Auftrags nachzuschlagen, lesen Sie bitte den Abschnitt [Abrufen eines Vorschau-Auftrags](../api/previews-and-estimates.md#get-preview) im Handbuch Vorschauen- und Schätzung-Endpunkte. Um den aktuellen Status eines Schätzauftrags nachzuschlagen, lesen Sie bitte den Abschnitt [Abrufen eines Schätzauftrags](../api/previews-and-estimates.md#get-estimate) im Handbuch Vorschauen und geschätzte Endpunkte.


## Nächste Schritte

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie einen Segmentauftrag erstellen, um eine Audience mit der API [!DNL Segmentation Service] zu erstellen. Ausführliche Anweisungen dazu finden Sie im Tutorial [Evaluieren und Zugreifen auf Segmentergebnisse](./evaluate-a-segment.md).
