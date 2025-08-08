---
title: Lizenznutzung und -kapazität
description: Erfahren Sie mehr über Ihre Lizenznutzung und Kapazitätsbeschränkungen in Adobe Experience Platform.
exl-id: 38dad2f1-bd0f-4cc3-a3a6-5105ea866ea4
source-git-commit: 326710e48ea9d6eb16f62b9f288311a1d255b287
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 12%

---

# Lizenznutzung und -kapazitäten

In Adobe Experience Platform informieren Sie die -Kapazitäten, wenn Ihr Unternehmen eine Ihrer Leitplanken überschritten hat, und erhalten Informationen zur Behebung dieser Probleme.

Weitere Informationen zu Leitplanken in Experience Platform finden Sie in der Übersicht über [Real-Time CDP-Leitplanken](../../rtcdp/guardrails/overview.md).

## Kapazitätsverhalten {#behavior}

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingthroughput"
>title="Streaming-Durchsatz"
>abstract="Der Wert für den Streaming-Durchsatz misst die kombinierten Spitzenwerte der eingehenden Ereignisse pro Sekunde für die Streaming-Aufnahme in den Profil-Service über Ihre Produktions- und Entwicklungs-Sandboxes hinweg."

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingaudiences"
>title="Anzahl der Streaming-Zielgruppen"
>abstract="Die maximale Anzahl von Streaming-Zielgruppen pro Sandbox. Diese Anzahl enthält auch die Anzahl der Edge-Zielgruppen in Ihrer Sandbox."

>[!CONTEXTUALHELP]
>id="platform_capacity_edgeaudiences"
>title="Edge-Zielgruppen"
>abstract="Die maximale Anzahl von Edge-Zielgruppen pro Sandbox."

Derzeit unterstützt Capacity die folgenden Services:

- Streaming-Segmentierung 
- Streaming-Aufnahme

Innerhalb dieser Services werden die folgenden Leitplanken verfolgt:

- Die maximale Anzahl von Streaming-Zielgruppen ist 500
   - Von diesen 500 Streaming-Zielgruppen sind maximal 150 Edge-Zielgruppen zulässig
- Der maximale kombinierte Durchsatz für die Streaming-Segmentierung beträgt 1500 Datensätze pro Sekunde (rps)

Die Zielgruppenkapazität befindet sich auf **Sandbox**-Ebene. Das bedeutet, dass Sie für jede Sandbox in Ihrem Unternehmen 500 Streaming-Zielgruppen haben können, davon 150 Edge-Zielgruppen.

Die Durchsatzkapazität befindet sich auf **Organisations**-Ebene und kann an Ihre individuellen Sandboxes verteilt werden. Beispielsweise können Sie mit den 1.500 U/s für den Durchsatz der Streaming-Segmentierung Ihre Produktions-Sandbox auf 1.500 U/s und Ihre Entwicklungs-Sandbox auf 150 U/s festlegen.

Experience Platform berechnet den Durchsatz der Sandbox in rollierenden Intervallen von 15 Minuten. Dieser Durchsatz wird in Echtzeit gemessen, wobei die Daten alle 60 Sekunden aktualisiert werden.

Wenn Ihre Nutzung 80 % und 90 % Ihrer lizenzierten Kapazität erreicht, gibt Experience Platform einen Warnhinweis aus, der Sie darüber informiert, dass Sie die Höchstkapazität Ihrer angegebenen Kapazität erreichen. Sie können die Einstellungen ändern, um den Prozentsatz der Kapazität anzupassen, um den Warnhinweis zu erhalten, oder den Warnhinweis vollständig entfernen.

Wenn Ihre Nutzung mehr als 100 % Ihrer lizenzierten Kapazität beträgt, wird dies als Verstoß gegen Ihre Kapazität angesehen. An dieser Stelle tritt Leistungslatenz auf, und Ihre Service-Level-Ziele (SLTs) **nicht** garantiert.

## Häufig gestellte Fragen

Im folgenden Abschnitt werden häufig gestellte Fragen zu den Funktionen von beschrieben.

### Kann ich eine maximale kombinierte Durchsatzbegrenzung haben, die sich auf weniger als mein Zielmaximum summiert?

+++ Antwort

Nein. Die maximale kombinierte Durchsatzbegrenzung **muss** muss bis zur Leitplanke Ihres Unternehmens summiert werden.

+++

### Was passiert, wenn ich meine maximale Kapazität übertreffe?

+++ Antwort

Dies hängt davon ab, welche Kapazität überschritten wird.

Wenn Sie die maximal zulässige Anzahl von Zielgruppen überschreiten, sind Ihre übermäßigen Zielgruppen derzeit nicht betroffen. Die Möglichkeit, neue Zielgruppen zu erstellen, könnte jedoch in Zukunft eingeschränkt sein.

Wenn Sie Ihren Streaming-Durchsatz überschreiten, tritt bei Ihrer Aufnahme und Segmentierung eine Leistungslatenz auf.

+++

### Warum sollte ich meine maximalen Kapazitäten einhalten?

+++ Antwort

Das Arbeiten mit Ihren maximalen Kapazitäten stellt sicher, dass Ihre Daten konsistent bleiben und Ihre Datenintegrität intakt bleibt.

Sie stellen eine konsistente Leistung während Spitzenzeiten sicher und vermeiden technische Probleme, die sich negativ auf die Systemleistung auswirken und Ihre nachgelagerten Kundenerlebnisse beeinträchtigen könnten. Dies führt letztendlich zu einer Verbesserung Ihrer Datenhygiene und der Gesamtsystemleistung.

+++

### Was sind die Best Practices für die Verwaltung des Durchsatzes der Streaming-Segmentierung?

+++ Antwort

Um den Durchsatz Ihrer Streaming-Segmentierung optimal zu verwalten, sollten Sie Ihre Datensätze bewerten, um sicherzustellen, dass sie Daten priorisieren, die für die Personalisierung erforderlich sind.


Wenn keine Echtzeitverarbeitung erforderlich ist, sollten Sie die Batch-Aufnahme anstelle der Streaming-Aufnahme verwenden.

+++
