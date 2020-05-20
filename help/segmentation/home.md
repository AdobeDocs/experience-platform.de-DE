---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform-Segmentdienst
topic: overview
translation-type: tm+mt
source-git-commit: a6a1ecd9ce49c0a55e14b0d5479ca7315e332904
workflow-type: tm+mt
source-wordcount: '2398'
ht-degree: 3%

---


# Übersicht über den Segmentierungsdienst

Der Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und Audiencen aus Ihren Echtzeit-Daten zum Profil von Kunden generieren können. Diese Segmente werden zentral auf der Plattform konfiguriert und gepflegt und stehen für jede Adobe-Lösung zur Verfügung.

Dieses Dokument bietet einen Überblick über den Segmentierungsdienst und die Rolle, die dieser in der Adobe Experience Platform spielt.

## Erste Schritte mit dem Segmentierungsdienst

Es ist wichtig, die folgenden Schlüsselbegriffe zu verstehen, die in diesem Dokument verwendet werden:

- **Segmentierung**: Die Unterteilung einer großen Gruppe von Einzelpersonen (z. B. Kunden, Potenzieller Kunde, Benutzer oder Organisationen) in kleinere Gruppen, die ähnliche Eigenschaften aufweisen und ähnlich wie Marketingstrategien reagieren.
- **Segmentdefinition**: Der Regelsatz, der zur Beschreibung der Hauptmerkmale oder des Verhaltens einer Zielgruppe-Audience verwendet wird. Nach der Konzeption werden die in einer Segmentdefinition beschriebenen Regeln verwendet, um qualifizierte Segmentmitglieder für eine Audience zu bestimmen.
- **Audience**: Der resultierende Satz von Profilen, die die Kriterien einer Segmentdefinition erfüllen.

## Funktionsweise der Segmentierung

Bei Segmentierung handelt es sich um den Prozess der Definition spezifischer Attribute oder Verhaltensweisen, die von einer Untergruppe von Profilen in Ihrem Profilspeicher geteilt werden, sodass Sie eine vermarktbare Gruppe von Personen aus Ihrem Kundenstamm ermitteln können. In einer E-Mail-Kampagne mit dem Namen „Haben Sie vergessen, Schuhe zu kaufen?“ wollen Sie möglicherweise eine Zielgruppe aller Anwender auswählen, die in den letzten 30 Tagen nach Laufschuhen gesucht haben, den Kauf jedoch nicht abgeschlossen haben.

Sobald ein Segment konzeptionell definiert wurde, wird es in Experience Platform integriert. In der Regel werden Segmente vom Marketingspezialisten oder Audiencen-Spezialisten erstellt, obwohl einige Unternehmen es vorziehen, dass sie in Zusammenarbeit mit ihren Datenanalysten von ihrer Marketingabteilung erstellt werden. Bei der Prüfung der an die Plattform gesendeten Daten erstellt der Datenanalyst die Segmentdefinition, indem er bestimmt, welche Felder und Werte zum Aufbau der Regeln oder Bedingungen des Segments verwendet werden. Dies erfolgt entweder über die Benutzeroberfläche oder die API.

## Segmente erstellen

Unabhängig davon, ob sie mit der API oder mit dem Segmentaufbau erstellt wurden, werden die Segmente letztendlich mithilfe der Profil Abfrage Language (PQL) definiert. Hier wird die Definition des konzeptionellen Segments in der Sprache beschrieben, die zum Abrufen von Profilen erstellt wurde, die den Kriterien entsprechen. Weitere Informationen finden Sie in der [PQL-Übersicht](./pql/overview.md).

Informationen zum Erstellen und Verwenden von Segmenten im Segmentaufbau (die Implementierung des Segmentierungsdiensts in der Benutzeroberfläche) finden Sie im Handbuch [Segmentaufbau](./ui/overview.md).

Informationen zum Erstellen von Segmentdefinitionen mit der API finden Sie im Lernprogramm zum [Erstellen von Segmenten mit der API](./tutorials/create-a-segment.md).

>[!NOTE] In dem Ereignis, in dem ein Schema erweitert wird, müssen alle zukünftigen Uploads neu hinzugefügte Felder entsprechend aktualisieren. Weitere Informationen zum Anpassen des Erlebnisdatenmodells (XDM) finden Sie im [Schema-Editor-Lernprogramm](../xdm/tutorials/create-schema-ui.md).

## Segmente bewerten

### Streaming-Segmentierung

>[!NOTE] Die Streaming-Segmentierung ist eine Beta-Funktion und steht auf Anfrage zur Verfügung.

Die Streaming-Segmentierung ist ein fortlaufender Datenauswahlprozess, der Ihre Segmente entsprechend der Aktivität des Benutzers aktualisiert. Nachdem ein Segment erstellt und gespeichert wurde, wird die Segmentdefinition auf eingehende Daten im Echtzeit-Kundensegment angewendet. Segmentzufügungen und -entfernungen werden regelmäßig verarbeitet, um sicherzustellen, dass Ihre Audience der Zielgruppe relevant bleibt.

Weitere Informationen zur Streaming-Segmentierung finden Sie in der Dokumentation zur [Streaming-Segmentierung](./api/streaming-segmentation.md).

### Stapelsegmentierung

Als Alternative zu einem laufenden Datenauswahlprozess verschiebt die Stapelsegmentierung alle Profil-Daten gleichzeitig durch Segmentdefinitionen, um entsprechende Audiencen zu erstellen. Nach der Erstellung wird dieses Segment gespeichert und gespeichert, damit Sie es zur Verwendung exportieren können.

Informationen zur Bewertung von Segmenten finden Sie im Tutorial zur [Segmentbewertung](./tutorials/evaluate-a-segment.md).

## Zugriff auf Segmentierungsergebnisse

Informationen zum Zugriff auf ein exportiertes Segment finden Sie im Lernprogramm zur [Segmentbewertung](./tutorials/evaluate-a-segment.md).

## Segmentmetadaten

Segmentmetadaten erleichtern die Indexierung im Ereignis, in dem alle Segmente wiederverwendet und/oder kombiniert werden sollen.

Zum Erstellen Ihrer Segmente (entweder über die API oder den Segmentaufbau) müssen Sie einen Segmentnamen und eine Richtlinie zum Zusammenführen definieren.

### Segmentnamen

Beim Erstellen eines neuen Segments müssen Sie einen Segmentnamen angeben. Der Segmentname wird verwendet, um ein bestimmtes Segment in der vom Segmentierungsdienst erstellten Sammlung zu identifizieren. Segmentnamen sollten daher beschreibend, knapp und eindeutig sein.

>[!NOTE] Denken Sie beim Planen eines Segments daran, dass Segmente aus einem beliebigen anderen Segment referenziert und mit diesem kombiniert werden können. Berücksichtigen Sie bei der Auswahl eines Namens die Möglichkeit, dass Ihr Segment wiederverwendbare Teile enthalten kann.

### Zusammenführungsrichtlinien

Zusammenführungsrichtlinien sind Regeln, die von Profil verwendet werden, um zu bestimmen, wie Daten priorisiert und unter bestimmten Voraussetzungen zu einer einheitlichen Ansicht kombiniert werden.
Wenn keine Richtlinie zum Zusammenführen definiert ist, wird die standardmäßige Richtlinie zum Zusammenführen von Plattformen verwendet. Wenn Sie lieber eine für Ihr Unternehmen spezifische Richtlinie zum Zusammenführen verwenden möchten, können Sie eine eigene Richtlinie erstellen und diese als Standard Ihres Unternehmens markieren.

>[!NOTE] Die Schätzung der Audience basiert auf der standardmäßigen Profil-Zusammenführungs-Richtlinie des Unternehmens.

### Andere Segmentmetadaten

Zusätzlich zu den Segmentnamen- und -zusammenführungsrichtlinien bietet Ihnen der Segmentaufbau ein zusätzliches Metadatenfeld &quot;Segmentbeschreibung&quot;, in dem Sie den Zweck Ihrer Segmentdefinition zusammenfassen können.

## Erweiterte Segmentierungsfunktionen

Segmente können so konfiguriert werden, dass sie eine Audience fortlaufend generieren, indem [Streaming-Datenerfassung](../ingestion/streaming-ingestion/overview.md) mit einer der folgenden erweiterten Segmentierungsfunktionen kombiniert wird:
- [Sequenzielle Segmentierung](#sequential)
- [Dynamische Segmentierung](#dynamic)
- [Segmentierung mehrerer Entitäten](#multi-entity)

Diese erweiterten Funktionen werden in den folgenden Abschnitten ausführlicher erläutert.

## Sequenzielle Segmentierung {#sequential}

Eine normale Benutzerreise ist sequenziell.  Mit der Adobe Experience Platform können Sie eine Reihe geordneter Segmente definieren, die diese Reise widerspiegeln, und dabei Sequenzen von Ereignissen während ihres Auftretens erfassen. Sie können Ereignis mithilfe der Zeitleiste des visuellen Ereignisses im Segmentaufbau in der gewünschten Reihenfolge anordnen.

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

Mit der erweiterten Segmentierungsfunktion für mehrere Entitäten können Sie Segmente mit mehreren XDM-Klassen erstellen und damit Erweiterungen zu persönlichen Schemas hinzufügen. Daher kann der Segmentdienst während der Segmentdefinition auf zusätzliche Felder zugreifen, als wären sie nativ im Profil-Datenspeicher.

Die Segmentierung mehrerer Entitäten bietet die erforderliche Flexibilität, um Audiencen anhand von Daten zu identifizieren, die für Ihre Geschäftsanforderungen relevant sind. Dieser Vorgang kann schnell und einfach durchgeführt werden, ohne dass Fachwissen in der Abfrage von Datenbanken erforderlich ist. Auf diese Weise können Sie wichtige Daten zu Ihren Segmenten hinzufügen, ohne kostspielige Änderungen an den Datenströmen vornehmen zu müssen oder auf eine Back-End-Datenzusammenführung zu warten.

### Verwendungsfall: Preisorientierte Werbung

Um den Wert dieser erweiterten Segmentierungsfunktion zu veranschaulichen, sollten Sie einen Datenarchitekten in Betracht ziehen, der mit einem Marketingspezialisten zusammenarbeitet.

In diesem Beispiel verbindet der Datenarchitekt Daten für eine Einzelperson (bestehend aus Schemas mit XDM Individual Profil und XDM ExperienceEvent als Basisklassen) mit einer anderen Klasse, die einen Schlüssel verwendet. Nach dem Verbinden können der Datenarchitekt oder der Marketingspezialist diese neuen Felder während der Segmentdefinition so verwenden, als wären sie nativ zum Schema der Basisklasse.

**Das Problem**

Sowohl der Datenarchitekt als auch der Vermarkter arbeiten für denselben Bekleidungshändler. Der Einzelhändler verfügt über mehr als 1.000 Geschäfte in Nordamerika und senkt regelmäßig die Produktpreise während ihres gesamten Lebenszyklus. Daher möchte der Vermarkter eine besondere Kampagne durchführen, um Käufern, die für diese Artikel gekauft haben, die Möglichkeit zu geben, diese Artikel zum ermäßigten Preis zu erwerben.

Zu den Ressourcen des Datenarchitekten gehören der Zugriff auf Webdaten aus dem Browsen von Kunden sowie Daten zum Hinzufügen des Einkaufswagens, die Produkt-SKU-IDs enthalten. Sie haben auch Zugang zu einer gesonderten Produktklasse, in der zusätzliche Produktinformationen (einschließlich des Produktpreises) gespeichert werden. Ihre Anleitung besteht darin, sich auf Kunden zu konzentrieren, die in den letzten 14 Tagen ein Produkt in ihren Einkaufswagen gelegt haben, aber den Artikel nicht gekauft haben, dessen Preis jetzt gefallen ist.

**Die Lösung**

>[!NOTE] In diesem Beispiel gehen wir davon aus, dass der Datenarchitekt bereits einen ID-Namensraum eingerichtet hat.

Mithilfe der API verknüpft der Datenarchitekt den Schlüssel aus dem ExperienceEvent-Schema mit der Produktklasse. Auf diese Weise kann der Datenarchitekt die zusätzlichen Felder der &quot;products&quot;-Klasse so nutzen, als wären sie nativ für das ExperienceEvent-Schema. Als letzter Schritt der Konfiguration muss der Datenarchitekt die entsprechenden Daten in das Echtzeit-Customer-Profil einbringen. Dies geschieht, indem der &quot;products&quot;-Datensatz für die Verwendung mit Profil aktiviert wird. Nachdem die Konfiguration abgeschlossen ist, kann entweder der Datenarchitekt oder der Marketingspezialist das Segmentsegment Zielgruppe im Segmentaufbau erstellen.

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

## Segmentierungsdienstdatentypen

Alle XDM-Datentypen werden im Segmentierungsdienst unterstützt. Die Regeln, die eine Segmentdefinition bilden, werden durch die folgenden Datentypen kontextualisiert.

### Zeichenfolgendaten

Segmentdefinitionen verwenden Zeichenfolgendaten, um nicht-numerische Beschränkungen für Segmentdefinitionen zu definieren, wie z. B. &quot;Ländername&quot;oder &quot;Treuhandstufe&quot;für Programme.

Stringdaten werden in Segmentdefinitionen mit logischen, einschließlich-/ausschließlichen und Vergleichsanweisungen eingeschlossen. Nachdem Sie Ihrer Segmentdefinition ein Zeichenfolgenattribut hinzugefügt haben, können Sie mit Zeichenfolgen-relevanten Anweisungen das Attribut mit anderen Zeichenfolgenfeldern vergleichen.

| Anweisungstyp | Beispiele |
| -------------- | -------- |
| Logisch | und, oder nicht |
| Inklusiv/exklusiv | einschließlich, muss vorhanden, exklusiv, darf nicht vorhanden sein |
| Vergleich | gleich, ungleich, enthält, Beginn mit |


### Datumsdaten

Mit den Datumsdaten können Sie Ihren Segmentdefinitionen zeitbasierten Kontext zuweisen, entweder durch Verwendung spezifischer Beginn-/Enddaten oder durch Verwendung datumsrelevanter Anweisungen, wie in der unten stehenden Tabelle dargestellt. Eine Implementierung könnte eine Audience von Kunden schaffen, die *dieses Jahr* jederzeit mit Ihrer Marke interagiert haben und auch in den letzten Tagen aktiv *gewesen* sind.

| Beispielfeld | Datumsbezogene Aussagen | Timeline |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | heute, gestern, diesen Monat, dieses Jahr | Relevant für den Tag, an dem das Segment erstellt wurde. |
| person.lastPurchase | zuletzt, während, vor, nach, innerhalb | Relevant innerhalb einer beliebigen Woche/eines Monats. |

### Experience Ereignisses

Als Adobe Experience Platform-Schema zeichnet XDM ExperienceEvents explizite und implizite Kundeninteraktionen mit plattformintegrierten Anwendungen auf, einschließlich einer Momentaufnahme des Systems zum Zeitpunkt der Interaktion. ExperienceEvents sind Faktendatensätze. Sie sind daher eine Datenquelle, die Ihnen während der Segmentdefinition zur Verfügung steht.

Wie in der unten stehenden Tabelle dargestellt, werden die Ereignis-Daten mit Suchbegriffen wiedergegeben, die das Verhalten von Ereignissen verfeinern und Ereignis-Attribute angeben.

| Schlüsselwort | Verwenden von  |
| ------- | --- |
| Einbeziehen/Ausschließen | Beschreibt das Verhalten des Ereignisses durch die Einbeziehung oder Auslassung von Daten. |
| Beliebig/Alle | Hilft bei der Bestimmung der Anzahl der qualifizierten Segmente. |
| Umschalter &quot;Zeitregel anwenden&quot; | Enthält Datumsdaten. |
| Gleich, ungleich, Beginn mit, nicht Beginn mit, endet mit, endet nicht mit, enthält, enthält nicht enthält, ist vorhanden, nicht vorhanden | Enthält Zeichenfolgendaten. |

### Segmente

Bestehende Segmentdefinitionen können auch als Komponenten einer neuen Segmentdefinition verwendet werden, wobei ihre Attribut- und Ereignis-basierten Regeln dem neuen Segment hinzugefügt werden.

### Zielgruppen

Externe Audiencen können auch als Komponenten einer neuen Segmentdefinition verwendet werden, wobei ihre Attributregeln dem neuen Segment hinzugefügt werden.

Derzeit wird nur Adobe Audience Manager als Audience unterstützt. Weitere Quellen werden in Zukunft aktiviert.

### Sonstige Datentypen

Zusätzlich zu den oben genannten umfasst die Liste unterstützter Datentypen auch:
- Zeichenfolge
- Einheitliche Ressourcenkennung
- Enum
- Zahl
- lang
- Ganzzahl
- Short
- Byte
- Boolesch
- Datum
- Datum/Uhrzeit
- Array
- Objekt
- Landkarte
- Ereignisse

## Nächste Schritte

Der Segmentierungsdienst bietet einen konsolidierten Arbeitsablauf zum Erstellen von Segmenten aus Daten des Echtzeit-Profils. Zusammenfassung:

- Bei der Segmentierung wird eine Untergruppe von Profilen aus Ihrem Profil-Store definiert, sodass Sie Verhalten oder Attribute einer gewünschten marktfähigen Gruppe charakterisieren können. Der Segmentierungsdienst ermöglicht diesen Vorgang.
- Denken Sie beim Planen eines Segments daran, dass ein Segment aus einem beliebigen anderen Segment referenziert und mit diesem kombiniert werden kann.
- Ein Profil kann anhand von Regeln erstellt werden, die auf den Daten der zugehörigen Zeitreihen oder beidem basieren.
- Segmente können entweder bei Bedarf oder kontinuierlich ausgewertet werden. Bei einer bedarfsgerechten Bewertung werden alle Profil-Daten gleichzeitig durch die Segmentdefinitionen weitergeleitet. Bei kontinuierlicher Auswertung werden Daten durch Segmentdefinitionen gestreamt, sobald sie in die Plattform gelangen.

Informationen zum Definieren von Segmenten in der Benutzeroberfläche finden Sie im Handbuch [Segmentaufbau](./ui/overview.md). Informationen zum Erstellen von Segmentdefinitionen mit der API finden Sie im Lernprogramm zum [Erstellen von Segmenten mit der API](./tutorials/create-a-segment.md).