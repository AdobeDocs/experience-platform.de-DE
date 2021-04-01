---
keywords: Experience Platform;Startseite;beliebte Themen;Segmentierung;Segmentierung;Segmentdienst;Segment;Segmente;Segmente
solution: Experience Platform
title: Übersicht über den Segmentdienst
topic: Übersicht
description: Erfahren Sie mehr über den Adobe Experience Platform Segmentation Service und seine Rolle im Plattform-Ökosystem.
translation-type: tm+mt
source-git-commit: eff833f20eba4e51579a43fbb98c1e2333e326ef
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 7%

---


# [!DNL Segmentation Service]Übersicht

Adobe Experience Platform [!DNL Segmentation Service] bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und Audiencen aus Ihren [!DNL Real-time Customer Profile]-Daten generieren können. Diese Segmente werden zentral konfiguriert und auf [!DNL Platform] gepflegt und sind für jede Adobe leicht zugänglich.

Dieses Dokument gibt einen Überblick über [!DNL Segmentation Service] und die Rolle, die es in Adobe Experience Platform spielt.

## Erste Schritte mit [!DNL Segmentation Service]

Es ist wichtig, die folgenden Schlüsselbegriffe zu verstehen, die in diesem Dokument verwendet werden:

- **Segmentierung**: Die Unterteilung einer großen Gruppe von Einzelpersonen (z. B. Kunden, Potenzieller Kunde, Benutzer oder Organisationen) in kleinere Gruppen, die ähnliche Eigenschaften aufweisen und ähnlich wie Marketingstrategien reagieren.
- **Segmentdefinition**: Der Regelsatz, der zur Beschreibung der Hauptmerkmale oder des Verhaltens einer Zielgruppe-Audience verwendet wird. Nach der Konzeption werden die in einer Segmentdefinition beschriebenen Regeln verwendet, um qualifizierte Zielgruppenmitglieder für ein Segment zu bestimmen.
- **Audience**: Der resultierende Satz von Profilen, die den Kriterien einer Segmentdefinition entsprechen.

## Funktionsweise der Segmentierung

Bei Segmentierung handelt es sich um den Prozess der Definition spezifischer Attribute oder Verhaltensweisen, die von einer Untergruppe von Profilen in Ihrem Profilspeicher geteilt werden, sodass Sie eine vermarktbare Gruppe von Personen aus Ihrem Kundenstamm ermitteln können. In einer E-Mail-Kampagne mit dem Namen „Haben Sie vergessen, Schuhe zu kaufen?“ wollen Sie möglicherweise eine Zielgruppe aller Anwender auswählen, die in den letzten 30 Tagen nach Laufschuhen gesucht haben, den Kauf jedoch nicht abgeschlossen haben.

Sobald ein Segment konzeptionell definiert wurde, wird es in [!DNL Experience Platform] erstellt. In der Regel werden Segmente vom Marketingspezialisten oder Audiencen-Spezialisten erstellt, obwohl einige Unternehmen es vorziehen, dass sie in Zusammenarbeit mit ihren Datenanalysten von ihrer Marketingabteilung erstellt werden. Bei der Überprüfung der an [!DNL Platform] gesendeten Daten stellt der Datenanalyst die Segmentdefinition zusammen, indem er bestimmt, welche Felder und Werte zum Aufbau der Regeln oder Bedingungen des Segments verwendet werden. Dies erfolgt entweder über die Benutzeroberfläche oder die API.

## Segmente erstellen

Unabhängig davon, ob sie mit der API oder mit [!DNL Segment Builder] erstellt wurden, werden Segmente letztendlich mit [!DNL Profile Query Language] (PQL) definiert. Hier wird die Definition des konzeptionellen Segments in der Sprache beschrieben, die zum Abrufen von Profilen erstellt wurde, die den Kriterien entsprechen. Weitere Informationen finden Sie unter [PQL overview](./pql/overview.md).

Informationen zum Erstellen und Verwenden von Segmenten im [!DNL Segment Builder] (UI-Implementierung von [!DNL Segmentation Service]) finden Sie im Handbuch [Segmentaufbau](./ui/overview.md).

Informationen zum Erstellen von Segmentdefinitionen mit der API finden Sie im Lernprogramm zum Erstellen von Segmenten mit der Audience mit der API](./tutorials/create-a-segment.md).[

>[!NOTE]
>
>In dem Ereignis, in dem ein Schema erweitert wird, müssen alle zukünftigen Uploads neu hinzugefügte Felder entsprechend aktualisieren. Weitere Informationen zum Anpassen von [!DNL Experience Data Model] (XDM) finden Sie im Tutorial [Schema-Editor](../xdm/tutorials/create-schema-ui.md).

## Segmente bewerten

Die Plattform unterstützt derzeit drei Methoden zur Bewertung von Segmenten: Streaming-Segmentierung, Stapelsegmentierung und Kantensegmentierung.

### Streaming-Segmentierung

Streaming-Segmentierung ist ein fortlaufender Datenauswahlprozess, der Ihre Segmente entsprechend der Aktivität des Benutzers aktualisiert. Nachdem ein Segment erstellt und gespeichert wurde, wird die Segmentdefinition auf eingehende Daten auf [!DNL Real-time Customer Profile] angewendet. Segmentzufügungen und -entfernungen werden regelmäßig verarbeitet, um sicherzustellen, dass Ihre Audience der Zielgruppe relevant bleibt.

Weitere Informationen zur Streaming-Segmentierung finden Sie in der [Streaming-Segmentierungsdokumentation](./api/streaming-segmentation.md).

### Stapelsegmentierung

Als Alternative zu einem laufenden Datenauswahlprozess verschiebt die Stapelsegmentierung alle Profil-Daten gleichzeitig durch Segmentdefinitionen, um entsprechende Audiencen zu erstellen. Nach der Erstellung wird dieses Segment gespeichert und gespeichert, damit Sie es zur Verwendung exportieren können.

**Inkrementelle Segmentierung (Beta)**

Stapelsegmente werden alle 24 Stunden ausgewertet. Bei vorhandenen Segmenten hält die inkrementelle Segmentierung Segmente jedoch bis zu einer Stunde frisch.

Die inkrementelle Segmentierung wird mit neuen Daten ausgeführt, die in den Profil Store gelangen. Für die inkrementelle Segmentierung gelten jedoch die folgenden Einschränkungen:

- Bei neuen oder kürzlich geänderten Segmenten werden Profil mit neuen Daten im nächsten inkrementellen Beginn qualifiziert. Profil ohne Änderungen werden jedoch im nächsten vollständigen Stapelsegmentierungsauftrag nachgeholt.
- Segmente mit mehreren Entitäten werden in der inkrementellen Segmentierung aktualisiert. Wenn Entitätsaktualisierungen vorhanden sind, werden Profil mit neuen Daten im nächsten inkrementellen Beginn verwendet. Profil ohne Änderungen werden jedoch im nächsten vollständigen Stapelsegmentierungsauftrag nachgeholt.
- Ereignis, die das Zeitfenster eines Segments verlassen, werden im nächsten vollständigen Stapelsegmentierungsauftrag abgeglichen.

Informationen zur Bewertung von Segmenten finden Sie im Lehrgang [Segmentbewertung](./tutorials/evaluate-a-segment.md).

### Kantensegmentierung

Bei der Edge-Segmentierung können Segmente direkt am Rand in der Plattform ausgewertet werden, sodass dieselben Anwendungsfälle für die Personalisierung der Seite und der nächsten Seite möglich sind.

Weitere Informationen zur Kantensegmentierung finden Sie in der [API-Dokumentation](./api/edge-segmentation.md) oder in der [UI-Dokumentation](./ui/edge-segmentation.md).

## Zugriff auf Segmentierungsergebnisse

Informationen zum Zugriff auf ein exportiertes Segment finden Sie im Lehrgang [Segmentbewertung](./tutorials/evaluate-a-segment.md).

## Segmentmetadaten

Segmentmetadaten erleichtern die Indexierung im Ereignis, in dem alle Segmente wiederverwendet und/oder kombiniert werden sollen.

Zum Erstellen Ihrer Segmente (entweder über die API oder [!DNL Segment Builder]) müssen Sie einen Segmentnamen und eine Richtlinie zum Zusammenführen definieren.

### Segmentnamen

Beim Erstellen eines neuen Segments müssen Sie einen Segmentnamen angeben. Der Segmentname wird verwendet, um ein bestimmtes Segment in der von [!DNL Segmentation Service] erstellten Sammlung zu identifizieren. Segmentnamen sollten daher beschreibend, knapp und eindeutig sein.

>[!NOTE]
>
>Denken Sie beim Planen eines Segments daran, dass Segmente aus einem beliebigen anderen Segment referenziert und mit diesem kombiniert werden können. Berücksichtigen Sie bei der Auswahl eines Namens die Möglichkeit, dass Ihr Segment wiederverwendbare Teile enthalten kann.

### Zusammenführungsrichtlinien

Merge-Richtlinien sind Regeln, die von [!DNL Profile] verwendet werden, um zu bestimmen, wie Daten priorisiert und unter bestimmten Bedingungen zu einer einheitlichen Ansicht kombiniert werden.
Wenn keine Richtlinie zum Zusammenführen definiert ist, wird die standardmäßige [!DNL Platform]-Richtlinie zum Zusammenführen verwendet. Wenn Sie lieber eine für Ihr Unternehmen spezifische Richtlinie zum Zusammenführen verwenden möchten, können Sie eine eigene Richtlinie erstellen und diese als Standard Ihres Unternehmens markieren.

Weitere Informationen zu Zusammenführungsrichtlinien finden Sie im Handbuch [Richtlinien zusammenführen](../profile/api/merge-policies.md).

>[!NOTE]
>
>Die Schätzung der Audience basiert auf der standardmäßigen Profil-Zusammenführungs-Richtlinie des Unternehmens.

### Andere Segmentmetadaten

Neben der Segmentnamen- und der Zusammenführungsrichtlinie gibt [!DNL Segment Builder] Ihnen ein weiteres Metadatenfeld &quot;Segmentbeschreibung&quot;ein, in dem Sie den Zweck Ihrer Segmentdefinition zusammenfassen können.

## Erweiterte Segmentierungsfunktionen

Segmente können so konfiguriert werden, dass sie eine Audience fortlaufend generieren, indem [Streaming-Datenerfassung](../ingestion/streaming-ingestion/overview.md) mit einer der folgenden erweiterten Segmentierungsfunktionen kombiniert wird:
- [Sequenzielle Segmentierung](#sequential)
- [Dynamische Segmentierung](#dynamic)
- [Segmentierung mehrerer Entitäten](#multi-entity)

Diese erweiterten Funktionen werden in den folgenden Abschnitten ausführlicher erläutert.

## Sequenzielle Segmentierung {#sequential}

Eine Standard-Journey ist sequenziell. Mit Adobe Experience Platform können Sie eine geordnete Segmentreihe definieren, die diese Journey widerspiegelt. Dadurch werden Sequenzen von Ereignissen beim Auftreten erfasst. Sie können die Ereignis in der gewünschten Reihenfolge anordnen, indem Sie die Zeitleiste des visuellen Ereignisses in [!DNL Segment Builder] verwenden.

Ein Beispiel für eine Journey eines Kunden, für die eine sequenzielle Segmentierung erforderlich wäre, wäre die Ansicht des Produkts > Hinzufügen des Produkts > Kassengang > Kein Kauf.

## Dynamische Segmentierung {#dynamic}

Die dynamische Segmentierung löst die Skalierbarkeitsprobleme, mit denen Marketingexperten beim Aufbau von Segmenten für Marketing-Kampagnen konfrontiert sind.

Im Gegensatz zur statischen Segmentierung, bei der Sie jeden möglichen Anwendungsfall explizit und wiederholt erfassen müssen, verwendet die dynamische Segmentierung Variablen, um die Regellogik zu erstellen und Beziehungen dynamisch auszudrücken.

### Verwendungsfall: Kunden suchen, die außerhalb ihres Heimatstaates Einkäufe tätigen

Um den Wert dieser erweiterten Segmentierungsfunktion zu veranschaulichen, sollten Sie einen Datenarchitekten erwägen, der mit einem Marketingspezialisten zusammenarbeitet, um Kunden zu identifizieren, die Käufe außerhalb ihres Heimatstaates getätigt haben.

**Das Problem**

Bei der statischen Segmentierung müssen Sie einzelne Segmente mit einem eindeutigen Attribut des Startstatus definieren, bevor Sie nach Ereignissen filtern, die nicht dem Startstatus entsprechen. Ein explizites Segment dieses Typs würde lauten: &quot;Ich suche Leute aus Utah, deren Kaufstatus nicht Utah ist.&quot; Wenn Sie eine Audience mit dieser Methode erstellen, müssen Sie für jeden US-Bundesstaat ein Segment für insgesamt 50 Segmente definieren.

Infolge der unterschiedlichen Segmentkombinationen, die beim Skalieren unvermeidlich auftreten, wird der manuelle Prozess für die statische Segmentierung zeitaufwendiger, was Ihre Effizienz insgesamt reduziert.

**Die Lösung**

Indem Sie dem Attribut &quot;Kaufstatus&quot;eine Variable zuweisen, wird Ihr dynamisches Segment vereinfacht, um &quot;einen Kauf zu finden, bei dem der Status dieses Kaufs nicht dem Herkunftsstatus des Kunden entspricht&quot;. Auf diese Weise können Sie dann 50 statische Segmente zu einem einzigen dynamischen Segment zusammenfassen.

## Segmentierung mit mehreren Entitäten {#multi-entity}

Mit der erweiterten Segmentierungsfunktion für mehrere Entitäten können Sie [!DNL Real-time Customer Profile]-Daten um zusätzliche Daten erweitern, die auf Produkten, Stores oder anderen Nicht-Personen basieren, die auch als &quot;Dimensionsentitäten&quot;bezeichnet werden. Daher kann [!DNL Segmentation Service] während der Segmentdefinition auf zusätzliche Felder zugreifen, als wären sie nativ im [!DNL Profile]-Datenspeicher. Die Segmentierung mehrerer Entitäten bietet Flexibilität bei der Identifizierung von Audiencen anhand von Daten, die für Ihre individuellen Geschäftsanforderungen relevant sind. Weitere Informationen, einschließlich Anwendungsfällen und Workflows, finden Sie im [Handbuch zur Segmentierung mehrerer Entitäten](multi-entity-segmentation.md).

## [!DNL Segmentation Service] Datentypen

[!DNL Segmentation Service] unterstützt eine Vielzahl von primitiven und komplexen Datentypen. Detaillierte Informationen, einschließlich einer Liste der unterstützten Datentypen, finden Sie im Handbuch [Unterstützte Datentypen](./data-types.md).

## Nächste Schritte

[!DNL Segmentation Service] bietet einen konsolidierten Arbeitsablauf zum Erstellen von Segmenten aus  [!DNL Real-time Customer Profile] Daten. Zusammenfassung:

- [!DNL Segmentation] ist der Prozess der Definition einer Untergruppe von Profilen aus Ihrem Profil Store, mit dem Sie Verhalten oder Attribute einer gewünschten marktfähigen Gruppe charakterisieren können. [!DNL Segmentation Service] macht diesen Prozess möglich.
- Denken Sie beim Planen eines Segments daran, dass ein Segment aus einem beliebigen anderen Segment referenziert und mit diesem kombiniert werden kann.
- Ein Profil kann anhand von Regeln erstellt werden, die auf den Daten der zugehörigen Zeitreihen oder beidem basieren.
- Segmente können entweder bei Bedarf oder kontinuierlich ausgewertet werden. Bei einer bedarfsgerechten Bewertung werden alle Profil-Daten gleichzeitig durch die Segmentdefinitionen weitergeleitet. Wenn Daten kontinuierlich ausgewertet werden, werden sie durch Segmentdefinitionen gestreamt, die [!DNL Platform] eingeben.

Informationen zum Definieren von Segmenten in der Benutzeroberfläche finden Sie im Handbuch [Segmentaufbau](./ui/overview.md). Informationen zum Erstellen von Segmentdefinitionen mit der API finden Sie im Tutorial zum Erstellen von Segmenten mit der API](./tutorials/create-a-segment.md).[