---
solution: Experience Platform
title: Segmentierungs-Service – Übersicht
description: Erfahren Sie mehr über den Segmentierungs-Service von Adobe Experience Platform und die Rolle, die dieser im Platform-Ökosystem spielt.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 44c92e2163e2b6c0c140c64bba41dfbcc15d5d7f
workflow-type: tm+mt
source-wordcount: '1633'
ht-degree: 50%

---

# [!DNL Segmentation Service] – Übersicht

Adobe Experience Platform [!DNL Segmentation Service] bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihrer [!DNL Real-Time Customer Profile] Daten. Diese Zielgruppen werden zentral konfiguriert und verwaltet in [!DNL Platform]und für jede Adobe leicht zugänglich sind.

Dieses Dokument bietet einen Überblick über [!DNL Segmentation Service] und die Rolle, die er in Adobe Experience Platform spielt.

## Erste Schritte mit [!DNL Segmentation Service]

Sie sollten die folgenden Schlüsselbegriffe verstehen, die in diesem Dokument verwendet werden:

- **Segmentierung**: Die Unterteilung einer großen Personengruppe (z. B. Kunden, Interessenten, Benutzer oder Unternehmen) in kleinere Gruppen, die ähnliche Eigenschaften aufweisen und ähnlich auf Marketing-Strategien reagieren.
- **Zielgruppe**: Eine Sammlung von Personen, die ähnliche Verhaltensweisen und/oder Merkmale aufweisen. Diese Personensammlung kann entweder von Adobe Experience Platform mithilfe von Segmentdefinitionen (plattformgenerierte Zielgruppe) oder aus externen Quellen (extern generierte Zielgruppe) erstellt werden.
- **Segmentdefinition**: Der Regelsatz, den Adobe Experience Platform verwendet, um die Hauptmerkmale oder das Verhalten einer Zielgruppe zu beschreiben.

## Funktionsweise der Segmentierung

Bei der Segmentierung handelt es sich um den Prozess der Definition spezifischer Attribute oder Verhaltensweisen, die eine Profil-Untergruppe in Ihrem Profilspeicher hat, anhand der eine vermarktbare Personengruppe in Ihrem Kundenstamm ermittelt werden kann. Beispielsweise könnten Sie für eine E-Mail-Kampagne mit dem Namen „Haben Sie vergessen, Ihre Schuhe zu kaufen?“ eine Zielgruppe bestehend aus allen Anwendern zusammenstellen, die in den letzten 30 Tagen nach Laufschuhen gesucht, den Kauf jedoch nicht abgeschlossen haben.

Nachdem eine Audience konzeptionell definiert wurde, ist sie integriert [!DNL Experience Platform]. In der Regel werden Zielgruppen vom Marketing- oder Zielgruppenspezialisten erstellt, obwohl einige Unternehmen es vorziehen, dass sie in Zusammenarbeit mit ihren Datenanalysten von ihrer Marketing-Abteilung erstellt werden. Nach Überprüfung der gesendeten Daten an [!DNL Platform]kann der Datenanalyst die Zielgruppe auf zwei Arten erstellen - entweder durch Erstellen einer Segmentdefinition durch Auswahl der Felder und Werte, die zum Erstellen der Regeln oder Bedingungen der Zielgruppe verwendet werden, oder durch Zusammenstellen einer Zielgruppe mithilfe der Zielgruppenkomposition.

## Erstellen von Zielgruppen

Zielgruppen können auf zwei verschiedene Arten in Adobe Experience Platform erstellt werden - entweder direkt als Zielgruppen oder über Platform-abgeleitete Segmentdefinitionen.

### Zielgruppenkomposition

Beim direkten Erstellen einer Zielgruppe in Platform können Sie die Zielgruppenkomposition verwenden. Informationen zur Verwendung der Zielgruppenkomposition zum Erstellen einer Zielgruppe finden Sie in der [Handbuch zur Zielgruppenkomposition](./ui/audience-composition.md) für weitere Informationen.

### Segmentdefinitionen

Ob mit der API oder mit der [!DNL Segment Builder], werden Segmentdefinitionen letztendlich mithilfe von [!DNL Profile Query Language] (PQL). Dabei wird die konzeptionelle Segmentdefinition in der Sprache beschrieben, mit der die Profile, die den Kriterien entsprechen, abgerufen werden. Weiterführende Informationen finden Sie in der [Übersicht zur PQL](./pql/overview.md).

Informationen zum Erstellen und Verwenden von Segmenten in [!DNL Segment Builder] (die Benutzeroberflächen-Implementierung von [!DNL Segmentation Service]) finden Sie im [Segment Builder-Handbuch](./ui/overview.md).

Informationen zum Erstellen von Segmentdefinitionen mithilfe der API finden Sie im Tutorial zu [Erstellen von Segmentdefinitionen mithilfe der API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Bei einer Erweiterung eines Schemas müssen bei allen künftigen Uploads auch die neu hinzugefügten Felder entsprechend aktualisiert werden. Weitere Informationen zum Anpassen von [!DNL Experience Data Model] (XDM) finden Sie im [Tutorial zum Schema-Editor](../xdm/tutorials/create-schema-ui.md).
>
>Wenn außerdem ein Erlebnisereignis-Ablaufwert für den Datensatz aktiviert ist, könnte sich dies auf die Mitgliedschaft in der erstellten Segmentdefinition auswirken. Weiterführende Informationen dazu, wie sich diese Funktion auf die Segmentierung auswirken kann, finden Sie im Handbuch zur [Gültigkeitsdauer von Erlebnisereignissen](../profile/event-expirations.md).

## Audiences bewerten {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Auswertungsmethoden"
>abstract="Platform unterstützt derzeit drei Methoden zum Auswerten von Zielgruppen: Streaming-Segmentierung, Batch-Segmentierung und Edge-Segmentierung."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Streaming-Auswertung"
>abstract="Die Streaming-Segmentierung ist ein fortlaufender Datenauswahlprozess, der Ihre Zielgruppen infolge von Benutzeraktivität aktualisiert."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=de" text="Auswerten von Ereignissen mit Streaming-Segmentierung nahezu in Echtzeit"

Platform unterstützt derzeit drei Methoden zum Auswerten von Zielgruppen: Streaming-Segmentierung, Batch-Segmentierung und Edge-Segmentierung.

### Streaming-Segmentierung  {#streaming}

Die Streaming-Segmentierung ist ein fortlaufender Datenauswahlprozess, der Ihre Zielgruppen infolge von Benutzeraktivität aktualisiert. Nachdem eine Zielgruppe erstellt und gespeichert wurde, wird die Segmentdefinition auf eingehende Daten angewendet auf [!DNL Real-Time Customer Profile]. Ergänzungen und Entfernungen der Audience werden regelmäßig verarbeitet, sodass Ihre Zielgruppe auch weiterhin relevant ist.

Weitere Informationen zur Streaming-Segmentierung finden Sie in der [Dokumentation zur Streaming-Segmentierung](./api/streaming-segmentation.md).

### Batch-Segmentierung {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Batch-Auswertung"
>abstract="Als Alternative zum kontinuierlichen Datenauswahlprozess werden bei der Batch-Segmentierung alle Profildaten gleichzeitig mit Segmentdefinitionen verglichen, um entsprechende Zielgruppen zu erstellen. Nach der Erstellung einer Zielgruppe wird sie gespeichert, sodass Sie sie exportieren und weiterverwenden können."

Als Alternative zum kontinuierlichen Datenauswahlprozess werden bei der Batch-Segmentierung alle Profildaten gleichzeitig mit Segmentdefinitionen verglichen, um entsprechende Zielgruppen zu erstellen. Nach der Erstellung wird die resultierende Audience gespeichert und zur Verwendung exportiert.

Batch-Zielgruppen werden automatisch alle 24 Stunden ausgewertet. Wenn Sie eine Batch-Zielgruppe nach Bedarf bewerten möchten, können Sie einen Segmentauftrag verwenden. Weitere Informationen zu Segmentierungsvorgängen finden Sie in der [Dokumentation zu Segmentierungsvorgängen](./api/segment-jobs.md).

### Edge-Segmentierung {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Edge-Auswertung"
>abstract="Bei der Edge-Segmentierung werden Segmente in Platform sofort in Experience Edge ausgewertet, was Anwendungsfälle mit Personalisierung auf derselben Seite und auf der nächsten Seite ermöglicht."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=de" text="Handbuch zur Benutzeroberfläche für Edge-Segmentierung"

Bei der Edge-Segmentierung werden Segmente in Platform sofort [in Experience Edge](../edge/home.md) ausgewertet, was Anwendungsfälle mit Personalisierung auf derselben Seite und auf der nächsten Seite ermöglicht.

Weitere Informationen zur Edge-Segmentierung finden Sie in der [API-Dokumentation](./api/edge-segmentation.md) oder [Benutzeroberflächendokumentation](./ui/edge-segmentation.md).

## Zugriff auf Segmentierungsergebnisse

Informationen zum Zugriff auf eine exportierte Zielgruppe finden Sie unter [Tutorial zur Segmentdefinitionsbewertung](./tutorials/evaluate-a-segment.md).

## Segmentdefinitionsmetadaten

Segmentdefinitionsmetadaten erleichtern die Indizierung für das Ereignis, bei dem eine beliebige Zielgruppe wiederverwendet und/oder kombiniert werden soll.

Erstellen einer Segmentdefinition (entweder über die API oder [!DNL Segment Builder]) erfordert, dass Sie einen Namen und eine Zusammenführungsrichtlinie definieren.

### Segmentdefinitionsnamen

Beim Erstellen einer neuen Segmentdefinition müssen Sie einen Namen angeben. Der Segmentdefinitionsname wird verwendet, um eine bestimmte Segmentdefinition innerhalb der von [!DNL Segmentation Service]. Segmentdefinitionsnamen sollten daher beschreibend, kurz und eindeutig sein.

>[!NOTE]
>
>Beachten Sie bei der Planung einer Segmentdefinition, dass Segmentdefinitionen aus jeder anderen Segmentdefinition referenziert und mit ihr kombiniert werden können. Erwägen Sie bei der Auswahl eines Namens die Möglichkeit, dass Ihre Segmentdefinition wiederverwendbare Teile enthalten kann.

### Zusammenführungsrichtlinien

Zusammenführungsrichtlinien sind Regeln, die von [!DNL Profile] verwendet werden. um zu bestimmen, wie Daten priorisiert und unter bestimmten Bedingungen zu einer vereinigten Ansicht kombiniert werden.

Wenn keine Zusammenführungsrichtlinie definiert ist, wird die Standard-Zusammenführungsrichtlinie von [!DNL Platform] verwendet. Wenn Sie lieber eine für Ihr Unternehmen spezifische Zusammenführungsrichtlinie verwenden möchten, können Sie eine eigene erstellen und diese als Standard für Ihr Unternehmen festlegen.

Weitere Informationen zu Zusammenführungsrichtlinien finden Sie im [Handbuch zu Zusammenführungsrichtlinien](../profile/api/merge-policies.md).

>[!NOTE]
>
>Die Schätzung der Zielgruppengrößen basiert auf der standardmäßigen Profilzusammenführungsrichtlinie des Unternehmens.

### Andere Segmentdefinitionsmetadaten

Zusätzlich zur Namen- und Zusammenführungsrichtlinie [!DNL Segment Builder] bietet Ihnen ein zusätzliches Metadatenfeld für Beschreibungen, in dem Sie den Zweck Ihrer Segmentdefinition zusammenfassen können.

## Erweiterte Segmentierungsfunktionen

Segmentdefinitionen können so konfiguriert werden, dass eine Zielgruppe laufend generiert wird, indem eine Kombination [Streaming-Datenerfassung](../ingestion/streaming-ingestion/overview.md) mit einer der folgenden erweiterten Segmentierungsfunktionen:
- [Sequenzielle Segmentierung](#sequential)
- [Dynamische Segmentierung](#dynamic)
- [Segmentierung mit mehreren Entitäten](#multi-entity)

Diese erweiterten Funktionen werden in den folgenden Abschnitten ausführlicher erläutert.

### Sequenzielle Segmentierung {#sequential}

Eine standardmäßige Customer Journey ist sequenziell. Mit Adobe Experience Platform können Sie eine geordnete Zielgruppenserie definieren, die diese Journey widerspiegelt und somit Ereignissequenzen erfasst, sobald sie auftreten. Über die Timeline für visuelle Ereignisse in [!DNL Segment Builder] können Sie Ereignisse in der gewünschten Reihenfolge anordnen.

Ein Beispiel für eine Customer Journey, für die eine sequenzielle Segmentierung erforderlich ist, wäre Produkt ansehen > Produkt hinzufügen > Kasse > Kein Kauf.

### Dynamische Segmentierung {#dynamic}

Die dynamische Segmentierung löst die Skalierbarkeitsprobleme, mit denen Marketingexperten traditionell beim Erstellen von Zielgruppen für Marketing-Kampagnen konfrontiert sind.

Im Gegensatz zur statischen Segmentierung, bei der Sie jeden möglichen Anwendungsfall explizit und wiederholt erfassen müssen, verwendet die dynamische Segmentierung Variablen, um die Regellogik zu erstellen und Beziehungen dynamisch auszudrücken.

Bei dieser erweiterten Segmentierungsfunktion sollte ein Datenarchitekt mit einem Marketing-Experten zusammenarbeiten, um Kunden zu identifizieren, die außerhalb ihres Bundesstaats Einkäufe getätigt haben.

Für die statische Segmentierung müssen Sie einzelne Segmente mit einem eindeutigen Attribut für den heimatlichen Bundesstaat definieren, bevor Sie nach Kaufereignissen filtern, die nicht dem Bundesland-Status entsprechen. Eine explizite Segmentdefinition dieses Typs würde lauten: &quot;Ich suche nach Personen aus Utah, deren Kaufstatus nicht Utah ist&quot;. Wenn Sie eine Zielgruppe mit dieser Methode erstellen, müssen Sie für jeden US-Bundesstaat eine Segmentdefinition für insgesamt 50 Segmente definieren.

Aufgrund der unterschiedlichen Segmentdefinitionskombinationen, die sich unweigerlich bei der Skalierung ergeben, wird der manuelle Prozess, der für die statische Segmentierung erforderlich ist, zeitaufwendiger, wodurch sich Ihre Gesamteffizienz verringert.

Durch die Zuweisung einer Variablen zum Kaufstatusattribut vereinfacht Ihre dynamische Segmentdefinition die Suche nach einem Kauf, bei dem der Status dieses Kaufs nicht mit dem Herkunftsstatus des Kunden übereinstimmt. Auf diese Weise können Sie dann 50 statische Segmente in einer einzelnen dynamischen Segmentdefinition zusammenfassen.

### Segmentierung mit mehreren Entitäten {#multi-entity}

Mit der erweiterten Segmentierungsfunktion für mehrere Entitäten können Sie die Daten von [!DNL Real-Time Customer Profile] mit zusätzlichen Daten erweitern, die auf Produkten, Geschäften oder anderen Nicht-Personen-Entitäten basieren und auch als „Dimensionsentitäten“ bezeichnet werden. Folglich kann [!DNL Segmentation Service] während der Segmentdefinition auf zusätzliche Felder zugreifen, als ob sie nativ im [!DNL Profile]-Datenspeicher enthalten wären. Die Segmentierung mehrerer Entitäten bietet Flexibilität bei der Identifizierung von Zielgruppen anhand von Daten, die für Ihre individuellen Geschäftsanforderungen relevant sind. Weitere Informationen, einschließlich Anwendungsfällen und Workflows, finden Sie im [Handbuch zur Segmentierung mehrerer Entitäten](multi-entity-segmentation.md).

## [!DNL Segmentation Service]-Datentypen

[!DNL Segmentation Service] unterstützt eine Vielzahl von einfachen und komplexen Datentypen. Detaillierte Informationen, einschließlich einer Liste der unterstützten Datentypen, finden Sie im [Handbuch zu unterstützten Datentypen](./data-types.md).

## Nächste Schritte

[!DNL Segmentation Service] bietet einen konsolidierten Workflow zum Erstellen von Zielgruppen aus [!DNL Real-Time Customer Profile] Daten.

Weitere Informationen zur Verwendung der Segmentation Service-Benutzeroberfläche finden Sie in der [Übersicht über die Benutzeroberfläche des Segmentierungsdienstes](./ui/overview.md).

Informationen zum Erstellen von Zielgruppen in der Benutzeroberfläche finden Sie in der [Handbuch zur Zielgruppenkomposition](./ui/audience-composition.md). Informationen zum Definieren von Segmentdefinitionen in der Benutzeroberfläche finden Sie in der [Segment Builder-Handbuch](./ui/overview.md). Informationen zum Erstellen von Segmentdefinitionen mithilfe der API finden Sie im Tutorial zu [Erstellen von Segmentdefinitionen mithilfe der API](./tutorials/create-a-segment.md).
