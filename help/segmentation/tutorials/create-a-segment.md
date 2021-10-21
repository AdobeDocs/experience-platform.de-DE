---
keywords: Experience Platform;Startseite;beliebte Themen;Segment;Segment;Segment;Segmentierung;Segmentierung;Segment erstellen;Segmentierungsdienst
solution: Experience Platform
title: Ein Segment mithilfe der Segmentierungsdienst-API erstellen
topic-legacy: tutorial
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie eine Segmentdefinition mithilfe der Adobe Experience Platform Segmentation Service API entwickeln, testen, Vorschau und speichern.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: 8325ae6fd7d0013979e80d56eccd05b6ed6f5108
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 21%

---

# Segment mithilfe der Segmentierungsdienst-API erstellen

Dieses Dokument bietet eine Anleitung zum Entwickeln, Testen, Anzeigen und Speichern einer Segmentdefinition unter Verwendung der [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Informationen zum Erstellen von Segmenten mithilfe der Benutzeroberfläche finden Sie in der [Handbuch zum Segmentaufbau](../ui/overview.md).

## Erste Schritte

Dieses Tutorial erfordert ein Verständnis der verschiedenen [!DNL Adobe Experience Platform] Dienste, die mit der Erstellung von Audiencen-Segmenten verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus Echtzeitdaten zum Kundenverhalten.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profil und Ereignis gemäß der [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md).

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen müssen, um erfolgreich Aufrufe an die [!DNL Platform] APIs.

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

## Segmentdefinition entwickeln

Der erste Schritt in der Segmentierung besteht darin, ein Segment zu definieren, das in einem Konstrukt namens Segmentdefinition dargestellt wird. Eine Segmentdefinition ist ein Objekt, das eine in [!DNL Profile Query Language] (PQL). Dieses Objekt wird auch als PQL-Prädikat bezeichnet. PQL-Prädikate definieren die Regeln für das Segment basierend auf Bedingungen, die sich auf beliebige Daten aus Datensatz oder Zeitreihen beziehen, an die Sie Folgendes übermitteln [!DNL Real-time Customer Profile]. Siehe [PQL-Leitfaden](../pql/overview.md) für weitere Informationen zum Schreiben von PQL-Abfragen.

Sie können eine neue Segmentdefinition erstellen, indem Sie eine POST anfordern bei `/segment/definitions` Endpunkt im [!DNL Segmentation] API. Im folgenden Beispiel wird erläutert, wie eine Definitionsanforderung formatiert wird, einschließlich der Informationen, die erforderlich sind, damit ein Segment erfolgreich definiert werden kann.

Eine ausführliche Erläuterung zur Definition eines Segments finden Sie im [Entwicklerleitfaden für Segmentdefinition](../api/segment-definitions.md#create).

## Schätzung und Vorschau einer Audience {#estimate-and-preview-an-audience}

Wenn Sie Ihre Segmentdefinition entwickeln, können Sie die Tools zur Schätzung und Vorschau innerhalb von [!DNL Real-time Customer Profile] Informationen auf Zusammenfassungsebene der Ansicht, um sicherzustellen, dass Sie die erwartete Audience isolieren. Schätzungen liefern statistische Informationen über eine Segmentdefinition, wie z. B. die erwartete Audience und das Konfidenzintervall. Vorschauen bieten paginierte Listen von qualifizierenden Profilen für eine Segmentdefinition, mit denen Sie die Ergebnisse mit den Erwartungen vergleichen können.

Durch die Schätzung und Vorschau Ihrer Audience können Sie Ihre PQL-Vorhersagen testen und optimieren, bis sie ein erwünschtes Ergebnis liefern und dann in einer aktualisierten Segmentdefinition verwendet werden können.

Es sind zwei Schritte erforderlich, um ein Segment zu Vorschauen oder eine Schätzung Ihres Segments zu erhalten:

1. [Vorschau erstellen](#create-a-preview-job)
2. [Schätzung der Ansicht oder Vorschau](#view-an-estimate-or-preview) mit der ID des Auftrags der Vorschau

### Erstellung von Schätzungen

Datenstichproben werden verwendet, um Segmente zu bewerten und die Anzahl der qualifizierten Profil zu schätzen. Jeden Morgen werden neue Daten in den Speicher geladen (zwischen 12:00 und 2:00 Uhr, d.h. 7:9 Uhr UTC), und alle Segmentierungs-Abfragen werden anhand der Beispieldaten dieses Tages geschätzt. Folglich werden alle neu hinzugefügten oder zusätzlichen Daten am folgenden Tag in Schätzungen berücksichtigt.

Die Stichprobengröße hängt von der Gesamtanzahl der Entitäten in Ihrem Profil-Store ab. Diese Stichprobengrößen sind in der folgenden Tabelle dargestellt:

| Einrichtungen im Profil-Store | Stichprobengröße |
| ------------------------- | ----------- |
| Weniger als 1 Million | Vollständiger Datensatz |
| 1 bis 20 Millionen | 1 Million |
| über 20 Millionen | 5 % der Gesamtmittel |

Schätzungen laufen im Allgemeinen 10-15 Sekunden, beginnend mit einer groben Schätzung und der Verfeinerung, wenn mehr Datensätze gelesen werden.

### Vorschau erstellen

Sie können einen neuen Auftrag für die Vorschau erstellen, indem Sie eine POST anfordern an die `/preview` Endpunkt.

Detaillierte Anweisungen zum Erstellen eines Vorschau-Auftrags finden Sie im [Leitfaden zu Vorschauen und Schätzendpunkten](../api/previews-and-estimates.md#create-preview).

### Ansicht, Schätzung oder Vorschau

Schätzungs- und Vorschau-Prozesse werden asynchron ausgeführt, da verschiedene Abfragen unterschiedliche Zeitspannen benötigen. Sobald eine Abfrage initiiert wurde, können Sie mithilfe von API-Aufrufen den aktuellen Zustand der Schätzung oder Vorschau während des Fortschreitens abrufen (GET).

Verwenden der [!DNL Segmentation Service] API, können Sie den aktuellen Status eines Vorschau-Auftrags anhand seiner ID nachschlagen. Wenn der Status &quot;RESULT_READY&quot; lautet, können Sie die Ergebnisse Ansicht. Um den aktuellen Status eines Vorschau-Auftrags nachzuschlagen, lesen Sie den Abschnitt unter [Abrufen eines Vorschau-Auftrags](../api/previews-and-estimates.md#get-preview) im Handbuch zu Vorschauen und Schätzungen-Endpunkten. Lesen Sie den Abschnitt über, um den aktuellen Status eines schätzungsauftrags nachzuschlagen. [Abruf eines Schätzauftrags](../api/previews-and-estimates.md#get-estimate) im Handbuch zu Vorschauen und Schätzungen-Endpunkten.


## Nächste Schritte

Sobald Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie einen Segmentauftrag erstellen, um eine Audience zu erstellen, indem Sie [!DNL Segmentation Service] API. Siehe Tutorial zu [Segmentergebnisse bewerten und darauf zugreifen](./evaluate-a-segment.md) für detaillierte Schritte, wie Sie dies erreichen können.
