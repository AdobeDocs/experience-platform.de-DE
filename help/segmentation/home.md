---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Segmentation Service
topic: overview
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '1971'
ht-degree: 6%

---


# Adobe Experience Platform [!DNL Segmentation Service] overview

Adobe Experience Platform [!DNL Segmentation Service] provides a user interface and RESTful API that allows you to build segments and generate audiences from your [!DNL Real-time Customer Profile] data. These segments are centrally configured and maintained on [!DNL Platform], and are readily accessible by any Adobe solution.

Dieses Dokument gibt einen Überblick über [!DNL Segmentation Service] die Rolle, die es in der Adobe Experience Platform spielt.

## Getting started with [!DNL Segmentation Service]

Es ist wichtig, die folgenden Schlüsselbegriffe zu verstehen, die in diesem Dokument verwendet werden:

- **Segmentierung**: Die Unterteilung einer großen Gruppe von Einzelpersonen (z. B. Kunden, Potenzieller Kunde, Benutzer oder Organisationen) in kleinere Gruppen, die ähnliche Eigenschaften aufweisen und ähnlich wie Marketingstrategien reagieren.
- **Segmentdefinition**: Der Regelsatz, der zur Beschreibung der Hauptmerkmale oder des Verhaltens einer Zielgruppe-Audience verwendet wird. Nach der Konzeption werden die in einer Segmentdefinition beschriebenen Regeln verwendet, um qualifizierte Zielgruppenmitglieder für ein Segment zu bestimmen.
- **Audience**: Der resultierende Satz von Profilen, die den Kriterien einer Segmentdefinition entsprechen.

## Funktionsweise der Segmentierung

Bei Segmentierung handelt es sich um den Prozess der Definition spezifischer Attribute oder Verhaltensweisen, die von einer Untergruppe von Profilen in Ihrem Profilspeicher geteilt werden, sodass Sie eine vermarktbare Gruppe von Personen aus Ihrem Kundenstamm ermitteln können. In einer E-Mail-Kampagne mit dem Namen „Haben Sie vergessen, Schuhe zu kaufen?“ wollen Sie möglicherweise eine Zielgruppe aller Anwender auswählen, die in den letzten 30 Tagen nach Laufschuhen gesucht haben, den Kauf jedoch nicht abgeschlossen haben.

Sobald ein Segment konzeptionell definiert wurde, wird es integriert [!DNL Experience Platform]. In der Regel werden Segmente vom Marketingspezialisten oder Audiencen-Spezialisten erstellt, obwohl einige Unternehmen es vorziehen, dass sie in Zusammenarbeit mit ihren Datenanalysten von ihrer Marketingabteilung erstellt werden. Bei der Überprüfung der Daten, an die gesendet wird, stellt der Datenanalyst die Segmentdefinition zusammen, indem er bestimmt, welche Felder und Werte zum Aufbau der Regeln oder Bedingungen des Segments verwendet werden. [!DNL Platform] Dies erfolgt entweder über die Benutzeroberfläche oder die API.

## Segmente erstellen

Unabhängig davon, ob sie mit der API erstellt wurden oder mit der [!DNL Segment Builder], werden Segmente letztendlich mit [!DNL Profile Query Language] (PQL) definiert. Hier wird die Definition des konzeptionellen Segments in der Sprache beschrieben, die zum Abrufen von Profilen erstellt wurde, die den Kriterien entsprechen. For more information, see the [PQL overview](./pql/overview.md).

Informationen zum Erstellen und Verwenden von Segmenten im [!DNL Segment Builder] (der UI-Implementierung von [!DNL Segmentation Service]) finden Sie im Handbuch [Segmentaufbau](./ui/overview.md).

Informationen zum Erstellen von Segmentdefinitionen mit der API finden Sie im Lernprogramm zum [Erstellen von Segmenten mit der API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>In dem Ereignis, in dem ein Schema erweitert wird, müssen alle zukünftigen Uploads neu hinzugefügte Felder entsprechend aktualisieren. Weitere Informationen zum Anpassen [!DNL Experience Data Model] (XDM) finden Sie im [Schema-Editor-Lernprogramm](../xdm/tutorials/create-schema-ui.md).

## Segmente bewerten

### Streaming-Segmentierung

Streaming-Segmentierung ist ein fortlaufender Datenauswahlprozess, der Ihre Segmente entsprechend der Aktivität des Benutzers aktualisiert. Nachdem ein Segment erstellt und gespeichert wurde, wird die Segmentdefinition auf eingehende Daten angewendet [!DNL Real-time Customer Profile]. Segmentzufügungen und -entfernungen werden regelmäßig verarbeitet, um sicherzustellen, dass Ihre Audience der Zielgruppe relevant bleibt.

Weitere Informationen zur Streaming-Segmentierung finden Sie in der Dokumentation zur [Streaming-Segmentierung](./api/streaming-segmentation.md).

### Stapelsegmentierung

Als Alternative zu einem laufenden Datenauswahlprozess verschiebt die Stapelsegmentierung alle Profil-Daten gleichzeitig durch Segmentdefinitionen, um entsprechende Audiencen zu erstellen. Nach der Erstellung wird dieses Segment gespeichert und gespeichert, damit Sie es zur Verwendung exportieren können.

Informationen zur Bewertung von Segmenten finden Sie im Tutorial zur [Segmentbewertung](./tutorials/evaluate-a-segment.md).

## Zugriff auf Segmentierungsergebnisse

Informationen zum Zugriff auf ein exportiertes Segment finden Sie im Lernprogramm zur [Segmentbewertung](./tutorials/evaluate-a-segment.md).

## Segmentmetadaten

Segmentmetadaten erleichtern die Indexierung im Ereignis, in dem alle Segmente wiederverwendet und/oder kombiniert werden sollen.

Zum Erstellen Ihrer Segmente (entweder über die API oder [!DNL Segment Builder]) müssen Sie einen Segmentnamen und eine Richtlinie zum Zusammenführen definieren.

### Segmentnamen

Beim Erstellen eines neuen Segments müssen Sie einen Segmentnamen angeben. Der Segmentname wird verwendet, um ein bestimmtes Segment in der von [!DNL Segmentation Service]erstellten Sammlung zu identifizieren. Segmentnamen sollten daher beschreibend, knapp und eindeutig sein.

>[!NOTE]
>
>Denken Sie beim Planen eines Segments daran, dass Segmente aus einem beliebigen anderen Segment referenziert und mit diesem kombiniert werden können. Berücksichtigen Sie bei der Auswahl eines Namens die Möglichkeit, dass Ihr Segment wiederverwendbare Teile enthalten kann.

### Zusammenführungsrichtlinien

Zusammenführungsrichtlinien sind Regeln, [!DNL Profile] mit denen bestimmt wird, wie Daten priorisiert und unter bestimmten Voraussetzungen zu einer einheitlichen Ansicht kombiniert werden.
Wenn keine Richtlinie zum Zusammenführen definiert ist, wird die standardmäßige [!DNL Platform] Richtlinie zum Zusammenführen verwendet. Wenn Sie lieber eine für Ihr Unternehmen spezifische Richtlinie zum Zusammenführen verwenden möchten, können Sie eine eigene Richtlinie erstellen und diese als Standard Ihres Unternehmens markieren.

Weitere Informationen zu Zusammenführungsrichtlinien finden Sie im Leitfaden zu [Zusammenführungsrichtlinien](../profile/api/merge-policies.md).

>[!NOTE]
>
>Die Schätzung der Audience basiert auf der standardmäßigen Profil-Zusammenführungs-Richtlinie des Unternehmens.

### Andere Segmentmetadaten

Neben der Segmentnamen- und der Zusammenführungsrichtlinie [!DNL Segment Builder] wird ein zusätzliches Metadatenfeld &quot;Segmentbeschreibung&quot;Angebot, in dem Sie den Zweck Ihrer Segmentdefinition zusammenfassen können.

## Erweiterte Segmentierungsfunktionen

Segmente können so konfiguriert werden, dass sie eine Audience fortlaufend generieren, indem [Streaming-Datenerfassung](../ingestion/streaming-ingestion/overview.md) mit einer der folgenden erweiterten Segmentierungsfunktionen kombiniert wird:
- [Sequenzielle Segmentierung](#sequential)
- [Dynamische Segmentierung](#dynamic)
- [Segmentierung mehrerer Entitäten](#multi-entity)

Diese erweiterten Funktionen werden in den folgenden Abschnitten ausführlicher erläutert.

## Sequenzielle Segmentierung {#sequential}

Eine normale Benutzerreise ist sequenziell. Mit der Adobe Experience Platform können Sie eine Reihe von Segmenten definieren, die diese Reise widerspiegeln, und dabei Ereignis während ihres Auftretens erfassen. Sie können die Ereignisse in der gewünschten Reihenfolge anordnen, indem Sie die Zeitleiste des visuellen Ereignisses in der [!DNL Segment Builder].

Ein Beispiel für eine Customer Journey, die eine sequenzielle Segmentierung erfordern würde, wäre die Ansicht des Produkts > Hinzufügen des Produkts > Kassengang > Kein Kauf.

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

## Segmentierung mehrerer Entitäten {#multi-entity}

Mit der erweiterten Segmentierungsfunktion für mehrere Entitäten können Sie Segmente mit mehreren XDM-Klassen erstellen und damit Erweiterungen zu persönlichen Schemas hinzufügen. Dadurch [!DNL Segmentation Service] können Sie während der Segmentdefinition auf zusätzliche Felder zugreifen, als wären sie nativ im Profil-Datenspeicher.

Die Segmentierung mehrerer Entitäten bietet die erforderliche Flexibilität, um Audiencen anhand von Daten zu identifizieren, die für Ihre Geschäftsanforderungen relevant sind. Dieser Vorgang kann schnell und einfach durchgeführt werden, ohne dass Fachwissen in der Abfrage von Datenbanken erforderlich ist. Auf diese Weise können Sie wichtige Daten zu Ihren Segmenten hinzufügen, ohne kostspielige Änderungen an den Datenströmen vornehmen zu müssen oder auf eine Back-End-Datenzusammenführung zu warten.

Das folgende Video soll Ihr Verständnis der Segmentierung mehrerer Entitäten unterstützen und erläutert sowohl die Segmentierung mehrerer Entitäten als auch den Segmentkontext (Segmentnutzlast).

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

### Verwendungsfall: Preisorientierte Werbung

Um den Wert dieser erweiterten Segmentierungsfunktion zu veranschaulichen, sollten Sie einen Datenarchitekten in Betracht ziehen, der mit einem Marketingspezialisten zusammenarbeitet.

In diesem Beispiel verbindet der Datenarchitekt Daten für eine Einzelperson (bestehend aus Schemas mit [!DNL XDM Individual Profile] und [!DNL XDM ExperienceEvent] als Basisklassen) mit einer anderen Klasse, die einen Schlüssel verwendet. Nach dem Verbinden können der Datenarchitekt oder der Marketingspezialist diese neuen Felder während der Segmentdefinition so verwenden, als wären sie nativ zum Schema der Basisklasse.

**Das Problem**

Sowohl der Datenarchitekt als auch der Vermarkter arbeiten für denselben Bekleidungshändler. Der Einzelhändler verfügt über mehr als 1.000 Geschäfte in Nordamerika und senkt regelmäßig die Produktpreise während ihres gesamten Lebenszyklus. Daher möchte der Vermarkter eine besondere Kampagne durchführen, um Käufern, die für diese Artikel gekauft haben, die Möglichkeit zu geben, diese Artikel zum ermäßigten Preis zu erwerben.

Zu den Ressourcen des Datenarchitekten gehören der Zugriff auf Webdaten aus dem Browsen von Kunden sowie Daten zum Hinzufügen des Einkaufswagens, die Produkt-SKU-IDs enthalten. Sie haben auch Zugang zu einer gesonderten Produktklasse, in der zusätzliche Produktinformationen (einschließlich des Produktpreises) gespeichert werden. Ihre Anleitung besteht darin, sich auf Kunden zu konzentrieren, die in den letzten 14 Tagen ein Produkt in ihren Einkaufswagen gelegt haben, aber den Artikel nicht gekauft haben, dessen Preis jetzt gefallen ist.

**Die Lösung**

>[!NOTE]
>
>In diesem Beispiel gehen wir davon aus, dass der Datenarchitekt bereits einen ID-Namensraum eingerichtet hat.

Bei Verwendung der API bezieht sich der Datenarchitekt den Schlüssel aus dem [!DNL ExperienceEvent] Schema mit der Produktklasse. Auf diese Weise kann der Datenarchitekt die zusätzlichen Felder aus der Produktklasse so nutzen, als wären sie nativ für das [!DNL ExperienceEvent] Schema. Als letzter Schritt der Konfiguration muss der Datenarchitekt die entsprechenden Daten einbringen [!DNL Real-time Customer Profile]. Dies geschieht durch Aktivierung des &quot;products&quot;-Datensatzes zur Verwendung mit [!DNL Profile]. Nachdem die Konfiguration abgeschlossen ist, kann entweder der Datenarchitekt oder der Marketingspezialist das Zielgruppen-Segment in erstellen [!DNL Segment Builder].

Informationen zum Definieren von Beziehungen zwischen XDM-Klassen finden Sie in der Übersicht über die [Schema-Komposition](../xdm/schema/composition.md#union) .

<!-- ## Personalization payload

Segments can now carry a payload of contextual details to enable deep personalization of Adobe Solutions as well as external non-Adobe applications. These payloads can be added while defining your target segment.

With contextual data built into the segment itself, this advanced Segmentation Service feature allows you to better connect with your customer.

Segment Payload helps you answer questions surrounding your customer’s frame of reference such as:
- What: What product was purchased? What product should be recommended next?
- When: At what time and date did the purchase occur?
- Where: In which store or city did the customer make their purchase?

While this solution does not change the binary nature of segment membership, it does add additional context to each profile through an associated segment membership object. Each segment membership object has the capacity to include three kinds of contextual data:

- **Identifier**: this is the ID for the segment 
- **Attributes**: this would include information about the segment ID such as last qualification time, XDM version, status and so on.
- **Event data**: Specific aspects of experience events which resulted in the profile qualifying for the segment

Adding this specific data to the segment itself allows execution engines to personalize the experience for the customers in their target audience. -->

### Anwendungsbeispiele

Um den Wert dieser erweiterten Segmentierungsfunktion zu illustrieren, sollten Sie drei Standardverwendungsfälle erwägen, die die Herausforderungen illustrieren, die vor der SegmentPayload-Verbesserung in Marketinganwendungen aufgetreten sind:
- E-Mail-Personalisierung
- Email-Retargeting
- AnzeigenreTargeting

**E-Mail-Personalisierung**

Ein Marketingspezialist, der eine E-Mail-Kampagne erstellt hat, hat möglicherweise versucht, ein Segment für eine Audience der Zielgruppe zu erstellen, indem er in den letzten drei Monaten Käufe im Kundenspeicher verwendet hat. Idealerweise würde dieses Segment sowohl den Artikelnamen als auch den Namen des Geschäfts erfordern, in dem der Kauf getätigt wurde. Vor der Verbesserung bestand die Herausforderung darin, die Store-ID aus dem Kauf-Ereignis zu erfassen und sie dem Profil des Kunden zuzuweisen.

**Email-Retargeting**

Es ist häufig schwierig, Segmente für E-Mail-Kampagnen zu erstellen und zu qualifizieren, die auf &quot;Warenkorbabbruch&quot;abzielen. Vor der Verbesserung war es aufgrund der Verfügbarkeit der erforderlichen Daten schwierig, zu wissen, welche Produkte in eine personalisierte Nachricht aufgenommen werden sollten. Die Daten, für die die Produkte aufgegeben wurden, sind an Ereignis gebunden, die früher für die Überwachung und Extraktion von Daten schwierig waren.

**AnzeigenreTargeting**

Eine weitere traditionelle Herausforderung für Marketingexperten ist die Erstellung von Anzeigen, um Kunden mit aufgegebenen Warenkorbartikeln wieder anzusprechen. Während Segmentdefinitionen diese Herausforderung angehen, gab es vor der Verbesserung keine formale Methode, um zwischen gekauften und abgebrochenen Produkten zu unterscheiden. Jetzt können Sie bestimmte Datensätze während der Segmentdefinition Zielgruppe haben.

## [!DNL Segmentation Service] Datentypen

[!DNL Segmentation Service] unterstützt eine Vielzahl von Datentypen, darunter:

- Zeichenfolge
- Einheitliche Ressourcenkennung
- Enum
- Zahl
- Lang
- Ganzzahl
- Kurz
- Byte
- Boolesch
- Datum
- Datum-Uhrzeit
- Array
- Objekt
- Zuordnung
- Ereignisse

Ausführlichere Informationen zu diesen unterstützten Datentypen finden Sie im Dokument [für](./data-types.md)Support-Datentypen.

## Nächste Schritte

[!DNL Segmentation Service] bietet einen konsolidierten Arbeitsablauf zum Erstellen von Segmenten aus [!DNL Real-time Customer Profile] Daten. Zusammenfassung:

- [!DNL Segmentation] ist der Prozess der Definition einer Untergruppe von Profilen aus Ihrem Profil Store, mit dem Sie Verhalten oder Attribute einer gewünschten marktfähigen Gruppe charakterisieren können. [!DNL Segmentation Service] macht diesen Prozess möglich.
- Denken Sie beim Planen eines Segments daran, dass ein Segment aus einem beliebigen anderen Segment referenziert und mit diesem kombiniert werden kann.
- Ein Profil kann anhand von Regeln erstellt werden, die auf den Daten der zugehörigen Zeitreihen oder beidem basieren.
- Segmente können entweder bei Bedarf oder kontinuierlich ausgewertet werden. Bei einer bedarfsgerechten Bewertung werden alle Profil-Daten gleichzeitig durch die Segmentdefinitionen weitergeleitet. Bei kontinuierlicher Auswertung fließen die Daten durch die eingegebene Segmentdefinition [!DNL Platform].

Informationen zum Definieren von Segmenten in der Benutzeroberfläche finden Sie im Handbuch [Segmentaufbau](./ui/overview.md). Informationen zum Erstellen von Segmentdefinitionen mit der API finden Sie im Lernprogramm zum [Erstellen von Segmenten mit der API](./tutorials/create-a-segment.md).