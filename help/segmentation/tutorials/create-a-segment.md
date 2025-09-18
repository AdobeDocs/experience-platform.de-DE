---
solution: Experience Platform
title: Erstellen einer Segmentdefinition mit der Segmentierungs-Service-API
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie mit der Segmentierungs-Service-API von Adobe Experience Platform eine Segmentdefinition entwickeln, testen, in der Vorschau anzeigen und speichern.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: a374d261e3b34b30869f1a9e8486d52f5bd658cb
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 24%

---

# Erstellen einer Segmentdefinition mit der Segmentierungs-Service-API

Dieses Dokument enthält ein Tutorial zum Entwickeln, Testen, Anzeigen einer Vorschau und Speichern einer Segmentdefinition mithilfe der [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Informationen zum Erstellen von Segmentdefinitionen mithilfe der Benutzeroberfläche finden Sie im [Segment Builder-Handbuch](../ui/segment-builder.md).

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der verschiedenen [!DNL Adobe Experience Platform]-Services voraus, die bei der Erstellung von Segmentdefinitionen zum Einsatz kommen. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Ermöglicht das Erstellen von Zielgruppen mithilfe von Segmentdefinitionen oder anderen externen Quellen aus Echtzeit-Kundenprofildaten.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten durch [!DNL Experience Platform] organisiert werden. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profile und Ereignisse gemäß den [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md) aufgenommen werden.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die [!DNL Experience Platform]-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Experience Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Experience Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

## Entwickeln einer Segmentdefinition

Der erste Schritt bei der Segmentierung besteht darin, eine Segmentdefinition zu definieren. Eine Segmentdefinition ist ein Objekt, das eine in [!DNL Profile Query Language] (PQL) geschriebene Abfrage kapselt. Dieses Objekt wird auch als PQL-Prädikat bezeichnet. PQL-Prädikate definieren die Regeln für die Segmentdefinition basierend auf Bedingungen, die sich auf Datensatz- oder Zeitreihendaten beziehen, die Sie [!DNL Real-Time Customer Profile] bereitstellen. Weitere Informationen zum Schreiben von PQL-Abfragen [ Sie im Handbuch zu PQL ](../pql/overview.md).

Sie können eine neue Segmentdefinition erstellen, indem Sie eine POST-Anfrage an den `/segment/definitions`-Endpunkt in der [!DNL Segmentation]-API stellen. Im folgenden Beispiel wird beschrieben, wie Sie eine Definitionsanfrage formatieren, einschließlich der Informationen, die für die erfolgreiche Definition einer Segmentdefinition erforderlich sind.

Eine ausführliche Erläuterung zur Definition einer Segmentdefinition finden Sie im [Entwicklerhandbuch zur Segmentdefinition](../api/segment-definitions.md#create).

## Schätzen und Anzeigen der Vorschau einer Zielgruppe {#estimate-and-preview-an-audience}

Bei der Entwicklung Ihrer Segmentdefinition können Sie die Tools Schätzung und Vorschau in [!DNL Real-Time Customer Profile] verwenden, um Informationen auf Zusammenfassungsebene anzuzeigen und so sicherzustellen, dass Sie die erwartete Zielgruppe isolieren. Schätzungen liefern statistische Informationen über eine Segmentdefinition, z. B. die projizierte Zielgruppengröße und das Konfidenzintervall. Die Vorschau bietet paginierte Listen von qualifizierten Profilen für eine Segmentdefinition, sodass Sie die Ergebnisse mit dem vergleichen können, was Sie erwarten.

Durch Schätzen und Vorschau Ihrer Zielgruppe können Sie Ihre PQL-Eigenschaften testen und optimieren, bis sie ein erwünschtes Ergebnis liefern, wo sie dann in einer aktualisierten Segmentdefinition verwendet werden können.

Es gibt zwei erforderliche Schritte, um eine Vorschau anzuzeigen oder eine Schätzung Ihrer Segmentdefinition abzurufen:

1. [Erstellen eines Vorschauauftrags](#create-a-preview-job)
2. [Schätzung oder Vorschau anzeigen](#view-an-estimate-or-preview) unter Verwendung der ID des Vorschauauftrags

### So werden Schätzungen generiert

Wenn für das Echtzeit-Kundenprofil aktivierte Daten in Experience Platform aufgenommen werden, werden sie im Profildatenspeicher gespeichert. Wenn die Aufnahme von Datensätzen in den Profilspeicher die Gesamtprofilanzahl um mehr als 3 % erhöht oder verringert, wird ein Sampling-Auftrag ausgelöst, um die Anzahl zu aktualisieren. Wenn sich die Profilanzahl nicht um mehr als 3 % ändert, wird der Sampling-Auftrag automatisch wöchentlich ausgeführt.

Die Art und Weise, wie die Stichprobe ausgelöst wird, hängt von der Art der Aufnahme ab, die verwendet wird:

- Bei Streaming-Daten-Workflows wird stündlich überprüft, ob der Anstieg- oder Abnahmeschwellenwert von 3 % erreicht wurde. Wenn dieser Schwellenwert erreicht wurde, wird automatisch ein Beispielvorgang ausgelöst, um die Anzahl zu aktualisieren.
- Bei der Batch-Aufnahme wird innerhalb von 15 Minuten nach der erfolgreichen Aufnahme eines Batches in den Profilspeicher ein Auftrag ausgeführt, um die Anzahl zu aktualisieren, wenn der Schwellenwert von 3 % für die Erhöhung oder Verringerung erreicht ist. Mit der Profil-API können Sie den neuesten erfolgreichen Beispielvorgang in der Vorschau anzeigen sowie die Profilverteilung nach Datensatz und Identity-Namespace auflisten.

Die Stichprobengröße hängt von der Gesamtzahl der Entitäten in Ihrem Profilspeicher ab. Diese Stichprobengrößen sind in der folgenden Tabelle dargestellt:

| Entitäten im Profilspeicher | Stichprobengröße |
| ------------------------- | ----------- |
| Weniger als 1 Million | Vollständiger Datensatz |
| 1 bis 20 Millionen | 1 Million |
| Über 20 Millionen | 5 % der Gesamtgröße |

Schätzungen dauern im Allgemeinen über 10-15 Sekunden, beginnend mit einer groben Schätzung und Verfeinerung, wenn mehr Datensätze gelesen werden.

### Erstellen eines Vorschauauftrags

Sie können einen neuen Vorschauauftrag erstellen, indem Sie eine POST-Anfrage an den `/preview`-Endpunkt senden.

Detaillierte Anweisungen zum Erstellen eines Vorschauauftrags finden Sie im [Handbuch zu Vorschauen und Schätzungen von Endpunkten](../api/previews-and-estimates.md#create-preview).

### Anzeigen eines Kostenvoranschlags oder einer Vorschau

Schätzungs- und Vorschauprozesse werden asynchron ausgeführt, da die Ausführung verschiedener Abfragen unterschiedlich lange dauern kann. Sobald eine Abfrage initiiert wurde, können Sie API-Aufrufe verwenden, um den aktuellen Status der Schätzung oder Vorschau abzurufen (GET), während sie fortgesetzt wird.

Mithilfe der [!DNL Segmentation Service]-API können Sie den aktuellen Status eines Vorschauauftrags anhand seiner ID nachschlagen. Wenn der Status „RESULT_READY“ lautet, können Sie die Ergebnisse anzeigen. Um den aktuellen Status eines Vorschauauftrags nachzuschlagen, lesen Sie bitte den Abschnitt zum [ eines Vorschauauftrags ](../api/previews-and-estimates.md#get-preview) Handbuch für Vorschauen und Schätzungen von Endpunkten. Um den aktuellen Status eines Schätzauftrags nachzuschlagen, lesen Sie bitte den Abschnitt zum Abrufen [ Schätzauftrags ](../api/previews-and-estimates.md#get-estimate) Handbuch für Vorschauen und Schätzungen von Endpunkten.


## Nächste Schritte

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie mithilfe der [!DNL Segmentation Service]-API einen Segmentauftrag erstellen, um eine Zielgruppe zu erstellen. Ausführliche Anweisungen dazu finden Sie im Tutorial [Bewerten von und Zugreifen auf ](./evaluate-a-segment.md)Segmentergebnisse).
