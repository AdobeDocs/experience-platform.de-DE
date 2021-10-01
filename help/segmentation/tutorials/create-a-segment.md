---
keywords: Experience Platform; Startseite; beliebte Themen; Segment; Segment erstellen; Segment erstellen; Segmentierung; Segment erstellen; Segmentierungsdienst
solution: Experience Platform
title: Erstellen eines Segments mithilfe der Segmentation Service-API
topic-legacy: tutorial
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie eine Segmentdefinition mithilfe der Adobe Experience Platform Segmentation Service-API entwickeln, testen, in der Vorschau anzeigen und speichern.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 22%

---

# Erstellen eines Segments mithilfe der Segmentation Service-API

Dieses Dokument bietet ein Tutorial zum Entwickeln, Testen, Anzeigen einer Vorschau und Speichern einer Segmentdefinition mit [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Informationen zum Erstellen von Segmenten mithilfe der Benutzeroberfläche finden Sie im [Segment Builder-Handbuch](../ui/overview.md).

## Erste Schritte

Dieses Tutorial setzt ein grundlegendes Verständnis der verschiedenen [!DNL Adobe Experience Platform]-Dienste voraus, die am Erstellen von Zielgruppensegmenten beteiligt sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Ermöglicht das Erstellen von Zielgruppensegmenten aus Echtzeit-Kundenprofildaten.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die [!DNL Platform]-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

## Entwickeln einer Segmentdefinition

Der erste Schritt bei der Segmentierung besteht darin, ein Segment zu definieren, das in einem Konstrukt dargestellt wird, das als Segmentdefinition bezeichnet wird. Eine Segmentdefinition ist ein Objekt, das eine in [!DNL Profile Query Language] (PQL) geschriebene Abfrage enthält. Dieses Objekt wird auch als PQL-Prädikat bezeichnet. PQL-Prädikate definieren die Regeln für das Segment basierend auf Bedingungen, die sich auf Datensatz- oder Zeitreihendaten beziehen, die Sie [!DNL Real-time Customer Profile] angeben. Weitere Informationen zum Schreiben von PQL-Abfragen finden Sie im [PQL-Handbuch](../pql/overview.md) .

Sie können eine neue Segmentdefinition erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/segment/definitions` in der API [!DNL Segmentation] stellen. Im folgenden Beispiel wird beschrieben, wie Sie eine Definitionsanfrage formatieren, einschließlich der Informationen, die erforderlich sind, damit ein Segment erfolgreich definiert werden kann.

Eine ausführliche Erklärung zum Definieren eines Segments finden Sie im [Entwicklerhandbuch für die Segmentdefinition](../api/segment-definitions.md#create).

## Schätzen und Anzeigen einer Vorschau einer Zielgruppe {#estimate-and-preview-an-audience}

Bei der Entwicklung Ihrer Segmentdefinition können Sie die Schätzungs- und Vorschau-Tools in [!DNL Real-time Customer Profile] verwenden, um Informationen auf Zusammenfassungsebene anzuzeigen und so sicherzustellen, dass Sie die erwartete Zielgruppe isolieren. Schätzungen liefern statistische Informationen über eine Segmentdefinition, z. B. die prognostizierte Zielgruppengröße und das Konfidenzintervall. Vorschau bietet paginierte Listen mit qualifizierten Profilen für eine Segmentdefinition, sodass Sie die Ergebnisse mit dem, was Sie erwarten, vergleichen können.

Durch Schätzung und Vorschau Ihrer Zielgruppe können Sie Ihre PQL-Eigenschaften testen und optimieren, bis sie ein gewünschtes Ergebnis liefern, in dem sie dann in einer aktualisierten Segmentdefinition verwendet werden können.

Es gibt zwei erforderliche Schritte, um eine Vorschau Ihres Segments anzuzeigen oder eine Schätzung davon zu erhalten:

1. [Erstellen eines Vorschauauftrags](#create-a-preview-job)
2. [Anzeigen der Schätzung oder ](#view-an-estimate-or-preview) Vorschau mit der ID des Vorschauauftrags

### Erstellung von Schätzungen

Datenbeispiele werden verwendet, um Segmente zu bewerten und die Anzahl der qualifizierten Profile zu schätzen. Jeden Morgen werden neue Daten in den Speicher geladen (zwischen 12:00 und 2:00 Uhr PT, was 7:00 Uhr UTC entspricht) und alle Segmentierungsabfragen werden anhand der Beispieldaten dieses Tages geschätzt. Folglich werden alle neuen hinzugefügten Felder oder erfassten zusätzlichen Daten am folgenden Tag in Schätzungen übernommen.

Die Stichprobengröße hängt von der Gesamtanzahl der Entitäten in Ihrem Profilspeicher ab. Diese Stichprobengrößen werden in der folgenden Tabelle dargestellt:

| Entitäten im Profilspeicher | Stichprobengröße |
| ------------------------- | ----------- |
| Weniger als 1 Million | Vollständiger Datensatz |
| 1 bis 20 Mio. | 1 Mio. |
| Über 20 Millionen | 5 % des Gesamtbetrags |

Schätzungen laufen in der Regel über 10-15 Sekunden, beginnend mit einer groben Schätzung und verfeinern, sobald mehr Datensätze gelesen werden.

### Erstellen eines Vorschauauftrags

Sie können einen neuen Vorschauauftrag erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/preview` senden.

Detaillierte Anweisungen zum Erstellen eines Vorschauauftrags finden Sie im [Handbuch zu Vorschauen und Schätzungen-Endpunkten](../api/previews-and-estimates.md#create-preview).

### Anzeigen einer Schätzung oder Vorschau

Schätzungs- und Vorschauprozesse werden asynchron ausgeführt, da unterschiedliche Abfragen unterschiedliche Zeiträume in Anspruch nehmen können. Nachdem eine Abfrage initiiert wurde, können Sie API-Aufrufe verwenden, um den aktuellen Status der Schätzung oder Vorschau während des Vorgangs abzurufen (GET).

Mit der API [!DNL Segmentation Service] können Sie den aktuellen Status eines Vorschauauftrags anhand seiner Kennung nachschlagen. Wenn der Status &quot;RESULT_READY&quot;lautet, können Sie die Ergebnisse anzeigen. Um den aktuellen Status eines Vorschauauftrags nachzuschlagen, lesen Sie den Abschnitt [Abrufen eines Vorschauauftragsabschnitts](../api/previews-and-estimates.md#get-preview) im Handbuch für Vorschau- und Schätzungen-Endpunkte. Um den aktuellen Status eines Schätzauftrags zu ermitteln, lesen Sie den Abschnitt [Abrufen eines Schätzauftrags](../api/previews-and-estimates.md#get-estimate) im Handbuch zu Vorschau- und Schätzendpunkten.


## Nächste Schritte

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie einen Segmentauftrag erstellen, um mithilfe der [!DNL Segmentation Service]-API eine Zielgruppe zu erstellen. Detaillierte Anweisungen dazu finden Sie im Tutorial zu [Auswerten und Aufrufen von Segmentergebnissen](./evaluate-a-segment.md).
