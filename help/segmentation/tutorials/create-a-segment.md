---
solution: Experience Platform
title: Erstellen einer Segmentdefinition mithilfe der Segmentation Service-API
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie eine Segmentdefinition mithilfe der Adobe Experience Platform Segmentation Service-API entwickeln, testen, in der Vorschau anzeigen und speichern.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 24%

---

# Erstellen einer Segmentdefinition mithilfe der Segmentation Service-API

Dieses Dokument bietet eine Anleitung zum Entwickeln, Testen, Anzeigen einer Vorschau und Speichern einer Segmentdefinition mit dem [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Informationen zum Erstellen von Segmentdefinitionen mithilfe der Benutzeroberfläche finden Sie im [Segment Builder-Handbuch](../ui/segment-builder.md).

## Erste Schritte

Dieses Tutorial setzt ein Verständnis der verschiedenen [!DNL Adobe Experience Platform]-Dienste voraus, die am Erstellen von Segmentdefinitionen beteiligt sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Ermöglicht Ihnen das Erstellen von Zielgruppen mithilfe von Segmentdefinitionen oder anderen externen Quellen aus Echtzeit-Kundenprofildaten.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten durch [!DNL Platform] organisiert werden. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profile und Ereignisse gemäß den [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md) aufgenommen werden.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die [!DNL Platform] -APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

## Entwickeln einer Segmentdefinition

Der erste Schritt bei der Segmentierung besteht darin, eine Segmentdefinition zu definieren. Eine Segmentdefinition ist ein Objekt, das eine in [!DNL Profile Query Language] (PQL) geschriebene Abfrage enthält. Dieses Objekt wird auch als PQL-Eigenschaft bezeichnet. PQL prädikiert die Definition der Regeln für die Segmentdefinition basierend auf Bedingungen, die sich auf Datensatz- oder Zeitreihendaten beziehen, die Sie für [!DNL Real-Time Customer Profile] angeben. Weitere Informationen zum Schreiben von PQL-Abfragen finden Sie im [PQL-Handbuch](../pql/overview.md) .

Sie können eine neue Segmentdefinition erstellen, indem Sie eine POST-Anfrage an den `/segment/definitions` -Endpunkt in der [!DNL Segmentation] -API richten. Im folgenden Beispiel wird beschrieben, wie Sie eine Definitionsanfrage formatieren, einschließlich der Informationen, die erforderlich sind, damit eine Segmentdefinition erfolgreich definiert werden kann.

Eine ausführliche Erläuterung zum Definieren einer Segmentdefinition finden Sie im [Entwicklerhandbuch für die Segmentdefinition](../api/segment-definitions.md#create).

## Schätzen und Anzeigen der Vorschau einer Zielgruppe {#estimate-and-preview-an-audience}

Bei der Entwicklung Ihrer Segmentdefinition können Sie die Schätzungs- und Vorschau-Tools in [!DNL Real-Time Customer Profile] verwenden, um Informationen auf Zusammenfassungsebene anzuzeigen und so sicherzustellen, dass Sie die erwartete Zielgruppe isolieren. Schätzungen liefern statistische Informationen über eine Segmentdefinition, z. B. die prognostizierte Zielgruppengröße und das Konfidenzintervall. Vorschau bietet paginierte Listen mit qualifizierten Profilen für eine Segmentdefinition, sodass Sie die Ergebnisse mit dem, was Sie erwarten, vergleichen können.

Durch Schätzung und Vorschau Ihrer Zielgruppe können Sie Ihre PQL-Prädikate testen und optimieren, bis sie ein gewünschtes Ergebnis erzielen und dort in einer aktualisierten Segmentdefinition verwendet werden können.

Es gibt zwei erforderliche Schritte, um eine Vorschau Ihrer Segmentdefinition anzuzeigen oder eine Schätzung davon zu erhalten:

1. [Vorschauauftrag erstellen](#create-a-preview-job)
2. [Anzeigen der Schätzung oder Vorschau](#view-an-estimate-or-preview) mithilfe der ID des Vorschauauftrags

### Erstellung von Schätzungen

Da für das Echtzeit-Kundenprofil aktivierte Daten in Platform erfasst werden, werden sie im Profildatenspeicher gespeichert. Wenn die Aufnahme von Datensätzen in den Profilspeicher die Gesamtzahl der Profile um mehr als 5 % erhöht oder verringert, wird ein Sampling-Auftrag ausgelöst, um die Anzahl zu aktualisieren. Wenn sich die Profilanzahl nicht um mehr als 5 % ändert, wird der Sampling-Auftrag wöchentlich automatisch ausgeführt.

Die Art und Weise, wie das Beispiel ausgelöst wird, hängt vom verwendeten Erfassungstyp ab:

- Für Streaming-Daten-Workflows wird stündlich geprüft, ob der Schwellenwert für eine Zu- oder Abnahme um 5 % erreicht wurde. Wenn dieser Schwellenwert erreicht wurde, wird automatisch ein Beispielauftrag ausgelöst, um die Anzahl zu aktualisieren.
- Bei der Batch-Erfassung wird innerhalb von 15 Minuten nach erfolgreicher Aufnahme eines Batches in den Profilspeicher ein Auftrag ausgeführt, um die Anzahl zu aktualisieren, wenn der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht ist. Mithilfe der Profil-API können Sie eine Vorschau des neuesten erfolgreichen Beispielauftrags anzeigen sowie die Profilverteilung nach Datensatz und Identitäts-Namespace auflisten.

Die Stichprobengröße hängt von der Gesamtanzahl der Entitäten in Ihrem Profilspeicher ab. Diese Stichprobengrößen sind in der folgenden Tabelle dargestellt:

| Entitäten im Profilspeicher | Stichprobengröße |
| ------------------------- | ----------- |
| Weniger als 1 Million | Vollständiger Datensatz |
| 1 bis 20 Millionen | 1 Million |
| Über 20 Millionen | 5 % der Gesamtgröße |

Schätzungen laufen in der Regel über 10-15 Sekunden, beginnend mit einer groben Schätzung und verfeinern, sobald mehr Datensätze gelesen werden.

### Vorschauauftrag erstellen

Sie können einen neuen Vorschauauftrag erstellen, indem Sie eine POST-Anfrage an den `/preview` -Endpunkt senden.

Detaillierte Anweisungen zum Erstellen eines Vorschauauftrags finden Sie im Handbuch [Endpunkte für Vorschau und Schätzungen](../api/previews-and-estimates.md#create-preview).

### Anzeigen einer Schätzung oder Vorschau

Schätzungs- und Vorschauprozesse werden asynchron ausgeführt, da unterschiedliche Abfragen unterschiedliche Zeiträume in Anspruch nehmen können. Nachdem eine Abfrage initiiert wurde, können Sie API-Aufrufe verwenden, um den aktuellen Status der Schätzung oder Vorschau während des Vorgangs abzurufen (GET).

Mit der API [!DNL Segmentation Service] können Sie den aktuellen Status eines Vorschauauftrags anhand seiner Kennung nachschlagen. Wenn der Status &quot;RESULT_READY&quot;lautet, können Sie die Ergebnisse anzeigen. Um den aktuellen Status eines Vorschauauftrags nachzuschlagen, lesen Sie den Abschnitt über den Abschnitt [Abrufen eines Vorschauauftrags](../api/previews-and-estimates.md#get-preview) im Handbuch zu Vorschauen und Schätzungen-Endpunkten. Um den aktuellen Status eines Schätzauftrags zu ermitteln, lesen Sie bitte den Abschnitt über das Abrufen eines Schätzauftrags ](../api/previews-and-estimates.md#get-estimate) im Handbuch für Vorschau- und Schätzendpunkte.[


## Nächste Schritte

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie einen Segmentauftrag erstellen, um mithilfe der [!DNL Segmentation Service] -API eine Zielgruppe zu erstellen. Detaillierte Anweisungen dazu finden Sie im Tutorial zum [Auswerten und Aufrufen von Segmentergebnissen](./evaluate-a-segment.md) .
