---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Domain-Modell für Angebotsentscheidungen
topic: overview
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '2614'
ht-degree: 97%

---


# Übersicht über das Domain-Modell für Angebotsentscheidungen

Offer decisioning is a use case of [!DNL Decisioning Service] within which you formalize and centrally manage the rules and predictions used for engaging customers with offers. Angebotsentscheidungen werden als eine Art von _**Inhaltsentscheidung**_ betrachtet. In diesem Fall werden die _**Entscheidungsoptionen**_ als _**Angebote**_ bezeichnet und sind als solche durch den ihnen beigefügten Inhalt gekennzeichnet. For an introduction of the object model used by the [!DNL Decisioning Service], please refer to [Decisioning Service Domain Model](experience-model.md).

Ziel ist es, dem Endbenutzer auf Grundlage von Targeting-Kriterien, Kosten- und Frequenzbegrenzungen sowie vorherigen Interaktionen auf verschiedenen Kanälen (einschließlich zuvor vorgeschlagener Angebote) in jedem Kanal ein „bestes Angebot“ zu unterbreiten.

Wie bei allen Entscheidungsfällen werden die Entscheidungsoptionen (Angebote) in einem Repository verwaltet, das von einer beliebigen Anzahl von Anwendungen gemeinsam genutzt wird. Angebote können von verschiedenen Abteilungen Ihrer Organisation oder von Partnern erstellt werden; diese Angebote lassen sich täglich hinzufügen und entfernen.

Angebote werden von der Anwendung, die das Erlebnis bereitstellt, visuell in größere Erlebnisse eingefügt. _**Platzierungen**_, manchmal auch als Positionen oder Slots bezeichnet, sind wichtige Komponenten bei der Erstellung einer Strategie. Die Entwicklung einer Angebotsstrategie beginnt oft mit der Definition dieser Platzierungen. Ein Angebot verfügt in der Regel über mehrere _**Inhaltsdarstellungen**_, sodass es in verschiedene Erlebnisse richtig integriert werden kann. Jedes von ihnen weist unterschiedliche Dimensions- oder andere Begrenzungen auf und erfordert andere Medienformate.

Angebote sind häufig mit Waren oder Dienstleistungen verknüpft und es gibt eine Kostenberechnung. Eine Organisation muss in der Lage sein, die Ressourcen, die von Angeboten verbraucht werden, zu beschränken, und muss daher die Möglichkeit haben, die Gesamtanzahl der Vorschläge für ein Angebot zu _**begrenzen**_.

Der prognostizierte Wert eines akzeptierten Angebots für die Organisation ist das Optimierungskriterium und steht den Kosten für die Abgabe eines Angebots gegenüber. Kosten, Annahmewahrscheinlichkeit und voraussichtlicher Wert werden zur Anordnung der Angebote verwendet. Das beste Angebot ist das mit den höchsten prognostizierten positiven Auswirkungen auf die Ziele Ihrer Angebotsaktivitäten.

Bei Angebotsentscheidungen werden die Interaktionen, die ein Endbenutzer _**über verschiedene Kanäle**_ und Anwendungen hinweg hatte, sowie die Profil- und Erlebnisereignisdaten des Endbenutzers berücksichtigt. Beispielsweise kann eine Callcenter-Anwendung mithilfe der Angebotsentscheidung ein Angebot aktivieren oder unterdrücken, je nachdem, was der Endbenutzer gekauft und welche Reviews er veröffentlicht hat. Alternativ kann sich eine E-Mail-Verwaltungsanwendung darauf verlassen, dass die Angebotsentscheidung je nach dem Browser-Verlauf auf einer Website das „nächste beste Angebot“ in einem wöchentlichen Newsletter auswählt.

Angebote verfügen über andere interessante Eigenschaften. Häufig gibt es einen definierten _**Zeitplan**_ oder Datums- und Zeitbereich, in dem das Angebot gültig ist und bis zu dem das Angebot annulliert werden muss.

Schließlich reduziert sich die Attraktivität eines Angebots mit der Häufigkeit seiner Darstellung. Ein Angebot, das nicht angenommen wird, nachdem es wiederholt vorgeschlagen wurde, ist eine verlorene Chance, weil stattdessen ein anderes Angebot hätte angezeigt werden können. Aus diesem Grund muss die _**Ermüdung**_ von Endbenutzern verwaltet werden.

## Strategie für Angebotsentscheidungen auf einen Blick

Der übergeordnete Ansatz besteht darin, die Auswahl der Angebote einzugrenzen, bis alle Begrenzungen erfüllt sind, dann das Ranking-Modell auf die verbleibenden Optionen anzuwenden und schließlich mithilfe von Begrenzungen (Deduplizierung und Vermeidung von Fallback-Optionen) über verschiedene Aktivitäten hinweg zu optimieren.

| Strategiekomponente | Realisiert als |
| --- | --- |
| Entscheidungsaktivitäten | Angebotsaktivitäten |
| Entscheidungsoptionen | Angebot mit Inhaltsdarstellungen |
| Fallback-Optionen | Fallback-Angebot mit Inhaltsdarstellungen |
| Endlicher Satz von Entscheidungsoptionen | Angebotsinventar (auch Angebotsbibliothek genannt) |
| Topische Kategorien | Angebotsfilter basierend auf Tags und Angebotskennungen |
| Entscheidungsausgaben | Vorschlagen eines Angebots pro Aktivität für mehrere Aktivitäten auf einmal |
| Entscheidungsergebnisse | Erwartetes Erlebnisereignis mit Verweis auf das Angebot, z. B. `eventType='opened'` |
| Entscheidungsalgorithmus | Interne Dienstlogik, parametrisiert |
| Begrenzungen | Platzierungsbegrenzungen, kalendarische Begrenzungen, globale Begrenzungen und pro Benutzer, Deduplizierungsbegrenzungen |
| Entscheidungsregeln | Eignungsregeln |
| Modell für *erwartetes Dienstprogramm* | Angebotsrang oder -priorität |

Die Gesamtzahl der Angebote im Optionsinventar ist in der Regel recht groß (in der Größenordnung von 10.000en); jede Angebotsaktivität kann sich ggf. auf Angebote konzentrieren, die in eine andere Kategorie fallen (Thema). Die Strategie für Angebotsentscheidungen ermöglicht das Beifügen eines Angebotsfilters zu einer Angebotsaktivität. Weitere Begrenzungen werden zum Zeitpunkt der Anforderung der Entscheidung bewertet.
In den folgenden Abschnitten werden die Komponenten für die Angebotsentscheidungs-Domain detailliert erläutert.

## Allgemeine Angebote

Allgemeine Angebote, auch als personalisierte Angebote bezeichnet, stehen im Mittelpunkt der Aktivitäten von Angebotsentscheidungen. Sie weisen Attribute wie Name und Status auf. Das Statusattribut gibt an, ob die Entität bereit ist, in die Liste aktiver genehmigter Angebote aufgenommen zu werden. Allgemeinen Angeboten werden unterschiedliche Begrenzungen hinzugefügt. Siehe mehr dazu im Abschnitt ‎[Begrenzungen](#offer-constraints) unten.

## Inhalt in Angeboten

### Angebotsplatzierungen

Platzierungen definieren Inhaltsbegrenzungen und werden mit einer Aktivität genutzt, um die Position anzugeben, an der das nächste beste Erlebnis bereitgestellt wird. Dies verringert die Anzahl der Optionen, die in Betracht gezogen werden können, weiter und stellt eine weitere Begrenzung dar, die von der Aktivität auferlegt wird. Dies wird als Platzierungsbegrenzung bezeichnet. Es werden nur Optionen in Betracht gezogen, die Inhalte aufweisen, die eine Platzierungsbegrenzung erfüllen (z. B. Angebote). Dies wird in den frühen Phasen der Entscheidungsstrategie ausgewertet. Wenn sich Optionsobjekte ändern, werden die Platzierungsbegrenzungen der einzelnen Aktivitäten neu bewertet und kann die Option für eine oder mehrere Aktivitäten in Betracht gezogen oder ausgeschlossen werden.

It is not the responsibility of the [!DNL Decisioning Service] to formalize the complex details of content dependencies. Stattdessen ermittelt jeder Client die Liste der Platzierungen in allen Kanälen und gibt diesen Platzierungen eindeutige Kennungen und Namen. Durch Verweis auf eine bestimmte Platzierung bestätigt der Designer, dass der angegebene Inhalt in die Platzierung passt.

Bei der Entwicklung von Inhalten müssen der Angebots-Marketer und der Inhalts-Designer einen „impliziten Vertrag“ vereinbaren, der hinter dem Namen „Homepage Hero Image“ oder „Service Call Opening Script“ steht. Das erste Element kann als Bild von 600 px Breite und 350 px Höhe vereinbart werden; das zweite Element kann den Inhalt auf Text in zwei Sprachvarianten begrenzen, die nicht mehr als 50 Wörter in drei oder vier Sätzen mit semantischer Struktur aufweisen. Platzierung, um nicht die gesamte Bedeutung des ausgeblendeten Vertrags zu speichern.

### Angebotsdarstellungen

Um sicherzustellen, dass ein Angebot in den verschiedenen Parametern der Platzierungen in Ihren Kanälen korrekt dargestellt werden kann, müssen verschiedene Darstellungen des Angebots erstellt werden. Der Angeboten beigefügte Inhalt wird nach Platzierungen angeordnet. Jedes Angebot kann eine oder mehrere Darstellungen aufweisen, wobei jede dieser Darstellungen auf eine der definierten Platzierungen verweist. Jede Darstellung in einem Angebot muss eine andere Platzierung verwenden. Je mehr Darstellungen ein Angebot hat, desto mehr Möglichkeiten gibt es, das Angebot in verschiedenen Platzierungskontexten zu nutzen.

Eine Platzierung beschränkt den Typ der Inhaltselemente, die der Darstellung hinzugefügt werden können.

## Fallback-Angebote

Fallback-Angebote sind Entscheidungsoptionen, die außer den Platzierungsregeln keine anderen Begrenzungen aufweisen. Fallback-Angebote verfügen über Inhaltsdarstellungen, die wie bei jedem anderen Angebot mit Platzierungen verbunden sind.

Fallback-Angebote werden in Aktivitäten angegeben, um ein sinnvolles Inhaltserlebnis festzulegen, das verwendet werden kann, wenn kombinierte Begrenzungen alle eingeschränkten Optionen disqualifizieren. Da die Platzierungsbegrenzung nicht vom Laufzeitkontext oder vom Profil abhängig ist, kann sie bereits im Vorfeld beim Zusammenstellen der Aktivität geprüft werden. Bei Einsatz von Fallback-Angeboten gibt es immer eine Antwort auf die Frage: Welches ist derzeit das beste Angebot?

## Angebotsbegrenzungen

### Kalendarische Begrenzungen

In der Domain für Angebotsentscheidungen haben die Angebote eine Gültigkeitsdauer. Das bedeutet, dass das Angebot erst nach dem Anfangsdatum inklusive Uhrzeit und nicht mehr nach dem Enddatum inklusive Uhrzeit vorgeschlagen werden kann. Die Angebotsentität verfügt über eine einfache Struktur, die diese kalendarischen Begrenzungen definiert.

In regelmäßigen Abständen werden abgelaufene Angebote aus der Liste der berücksichtigten Optionen entfernt. Der Kalenderfilter wird jedoch zum Zeitpunkt der Anforderung der Entscheidung angewendet, damit die Begrenzungen präzise angewendet werden.

### Begrenzungen

Angebote können eine optionale Begrenzung aufweisen. Diese besteht aus zwei Werten:

- Die globale Obergrenze beschränkt, wie oft ein Angebot im gesamten Profilsatz vorgeschlagen werden kann (beabsichtigte Zielgruppe).

- Die Obergrenze pro Profil legt fest, wie oft das Angebot demselben Profil vorgeschlagen werden kann.

### Duplizierungsbegrenzungen

Wenn eine Entscheidung angefordert wird, kann der Client nach Vorschlägen für mehrere Aktivitäten gleichzeitig fragen. Dies ist ein typisches Szenario bei der Inhaltsentscheidung. Jede Aktivität trägt eine oder mehrere Inhaltsoptionen zum Gesamterlebnis bei. Aufgrund des Kompositionsaspekts müssen Entscheidungen über mehrere Aktivitäten hinweg vermittelt werden, um Duplizierung zu vermeiden – es sei denn, die Aktivitäten wählen jeweils aus einem unzusammenhängenden Untersatz des Gesamtoptionsinventars aus. Eine hochplatzierte Option wird wahrscheinlich in allen Aktivitäten einen hohen Rang einnehmen, und das Erlebnis wäre schlecht, wenn alle Aktivitäten dieselbe Option vorschlagen würden. Wenn ein Versandsystem andererseits wissen möchte, was die „nächste beste Konversion“ für alle Kanäle ist und es keine Obergrenze gibt, kann es in Ordnung sein, dieselbe Option bei verschiedenen Aktivitäten vorzuschlagen.

Duplizierungsbegrenzungen sind derzeit nicht in das Repository für Geschäftsobjekte geschrieben. Stattdessen ist Deduplizierung zur Laufzeit die Standardstrategie. Ein Anfrageparameter kann das Standardverhalten überschreiben, um den Deduplizierungsschritt zu unterdrücken.

### [!DNL Profile] Einschränkungen - Eignungsregeln

Bislang waren die diskutierten Begrenzungen unabhängig davon anwendbar, für wen das Angebot ausgewählt wurde. Erlebnisentscheidungen unterstützen auch einen Anwendungsfall, bei dem Personalisierungsangebote auf Datensatz- und Zeitreihenereignissen des Kunden basieren. Regeln werden pro Profil ausgewertet, um zu entscheiden, ob ein Angebot für diesen Benutzer qualifiziert ist oder unterdrückt werden soll. Dazu kann jedem Angebot eine Eignungsregel zugeordnet werden. Neben den Profil- und Erlebnisereignissen eines Endbenutzers berücksichtigt die Eignungsregel Echtzeit-Kontextdaten. Diese Daten werden vom Versanddienst bereitgestellt und können in Form von Daten vorliegen, die nicht mit einem Profil in Zusammenhang stehen, z. B. Lagerbestände, Wetterbedingungen oder Flugpläne.

Es ist wichtig, bei der Entscheidungsfindung zwischen Targeting- und Segmentierungsregeln sowie zwischen Eignungs- und Prioritätsregeln zu unterscheiden. Beim Targeting ist eine Reihe von Profilen die Ausgabe (Auswahl der Zielgruppe), bei der Eignung ist eine Reihe von Optionen (zulässige Angebote) die Ausgabe der Auswertung.

## Angebotskollektionen

Das Inventar ist der Gesamt-Pool der Optionen, die bei Entscheidungen berücksichtigt werden. Das Inventar kann weiter in Kategorien oder Kollektionen unterteilt werden. Eine Kollektion von Optionen wird durch ein gemeinsames Tag dargestellt, das diese Optionen aufweisen. Filter werden zum Testen verwendet, ob Angebote in eine bestimmte Kategorie fallen oder, genauer gesagt, dieselben Tags verwenden.

### Tags

Tags bieten eine Möglichkeit, um auszudrücken, dass eine Gruppe von Optionen zu einer Kategorie gehört.

Eine Option kann über mehr als ein Tag verfügen und daher mehreren Kategorien gleichzeitig angehören. Kategorien können sich auch überlappen oder gegenseitig enthalten. Wenn eine Kategorie „S“ von Angeboten mit dem Tag „A“ und eine Kategorie „R“ von Optionen mit den Tags „A“ und auch „B“ definiert wird, ist „S“ eine Obermenge von „R“.

### Filter

Filter dienen dazu, die Kriterien für einen Satz von Optionen zu definieren, der zu einer Kategorie gehört. Filter können als Abfragen zum Inventar von allgemeinen Angeboten betrachtet werden. Es gibt zwei grundlegende Möglichkeiten, einen Filter zu erstellen: durch Angabe, dass ein Angebot über ein oder mehrere Tags verfügt, und durch explizite Auswahl des Angebotssatzes. Die erste Methode kann so konfiguriert werden, dass festgelegt wird, dass ein Angebot in dieser Kollektion alle angegebenen Tags aufweisen muss, oder dass eine Option qualifiziert ist, wenn sie mindestens eines der angegebenen Tags aufweist.

Wenn Optionen explizit in einer Kollektion platziert werden, wird ihr Tag-Satz bei dieser Kollektion ignoriert.

## Angebotsaktivitäten

Aktivitäten konfigurieren und steuern die Entscheidungsfindung. Aktuell ist die Entscheidungsstrategie im Wesentlichen vorab festgelegt, aber künftige Iterationen des Domain-Modells für Angebotsentscheidungen werden eine Auswahl von Modellen, zusätzlichen Regeln und Begrenzungen ermöglichen.

Ein Erlebnis kann unter Verwendung vieler Aktivitäten gleichzeitig zusammengestellt werden. Derzeit können in einer einzigen Entscheidungsanfrage bis zu 30 Aktivitäten bearbeitet werden. Wenn mehr als 30 Aktivitäten oder Slots in einem Erlebnis mit Inhalten gefüllt werden müssen, können für dasselbe Profil mehrere Anfragen gestellt werden. Werden jedoch Aktivitäten in derselben Entscheidungsanfrage einbezogen, so wird für diese Aktivitäten eine Deduplizierung der Angebotsvorschläge vorgenommen.

Wenn Aktivitäten so definiert sind, dass sie aus unzusammenhängenden Sätzen von Angeboten ausgewählt werden, macht es kaum einen Unterschied, ob Aktivitäten in derselben Anfrage zusammengefasst oder in separate Anfragen aufgeteilt werden. Allerdings erfordern Netzwerk- und Reaktionszeitbegrenzungen möglicherweise, dass Aktivitäten in einer Anfrage kombiniert werden. Da verschiedene Anfragen ggf. an verschiedene Dienstknoten weitergeleitet werden, müssen möglicherweise dieselben Profildaten in verschiedene Knoten abgerufen werden. Dadurch wird die effektive I/O-Bandbreite für andere Anfragen reduziert.

Aktivitäten dienen dazu, Inhalte in ein Erlebnis einzufügen. Um zu erleichtern (nicht um sicherzustellen), dass die Inhaltselemente richtig „passen“, verweist eine Aktivität auf eine einzelne Platzierung. Beachten Sie, dass eine Platzierung nicht immer ein konkreter Ort/Slot ist, sondern eher eine Abstraktion dieser Orte/Slots. Beispielsweise könnte jede Kachel auf einer Web-Seite mit einem Raster aus Kacheln durch die gleiche Platzierung gesteuert werden, vorausgesetzt, sie weisen alle eine ähnliche Form und Größe auf und können ähnliche Inhalte enthalten. Eine einzelne Kachel würde jedoch in der Regel von ihrer eigenen Aktivität bereitgestellt.

Die folgende Abbildung zeigt, wie die Geschäftseinheiten miteinander verbunden sind:

![](./images/figure-10.png)

Wenn Kunden das Objektdiagramm für Entscheidungen erstellen und verknüpfen, gibt es in der Regel drei verschiedene Workflows. Das sind Folgende:

- Einrichten der unterstützenden Entitäten wie Tags und Platzierungen. Diese Entitäten dienen dazu, andere Entitäten zu strukturieren, zu filtern und anzuordnen. Außerdem werden sie verwendet, um eine gewisse Koordinierung zwischen dem zweiten und dritten Workflow zu erreichen. Dieser Workflow ist mit einer gewissen Vorarbeit verbunden, kann jedoch jederzeit verfeinert werden. Während Tags relativ einfach sind, erfordern Platzierungen etwas mehr Planung. Unternehmen müssen mindestens eine Bestandsaufnahme aller Positionen vornehmen, an denen eine Entscheidung präsentiert wird.

- Erstellen von Angeboten mit den verschiedenen Darstellungen und Geschäftsregeln (Begrenzungen). Dieser zentrale Workflow stellt die Optionen bereit, unter denen wir die besten auswählen müssen. Die Tags des ersten Workflows werden zur Kategorisierung von Angeboten verwendet, während die Platzierungen angeben, welche Optionen wo angezeigt werden können.

   - Dieser Workflow definiert für die Angebote auch absolute Begrenzungen. Sie sind absolut, weil sie stets durchgesetzt werden und sich nicht nur auf die Reihenfolge einer Gruppe von Angeboten auswirken. Wenn beispielsweise eine kalendarische Begrenzung festgelegt wird, wird durchgesetzt, dass das Angebot nie vor dem festgelegten Anfangstermin und nie nach dem Endtermin ausgewählt wird. Die Begrenzungen, die in diesem Workflow festgelegt werden, sind die [kalendarischen Begrenzungen](#calendar-constraints), [Begrenzungen](#capping-constraints) und [Eignungsbegrenzungen](#profile-constraints---eligibility-rules). Ein Unter-Workflow besteht hier aus der Definition zusätzlicher Regeln, die bestimmen, wer für ein bestimmtes Angebot geeignet ist.

      - Bei der Erstellung von Begrenzungen für ein Angebot werden dessen Darstellungen ausgewählt. Bei diesem Workflow wird davon ausgegangen, dass der Inhalt bereits irgendwo erstellt wurde und einfach in das Inhalts-Repository hochgeladen und dort ausgewählt wird. Hier kommen die Platzierungen aus dem ersten Workflow in Spiel. Ein Angebot kann Platzierungen auswählen und den Inhalt unter dieser [Platzierung](#offer-placements) verknüpfen.

      - Das Erstellen geeigneter Fallback-Angebote ist der letzte Schritt in diesem Workflow. Ein Fallback-Angebot ähnelt einem allgemeinen Angebot ohne Begrenzungen.

- Der letzte Workflow betrifft die Erstellung von Aktivitäten. Dieser Schritt erfolgt jedoch nicht unbedingt auf den Workflow zum Erstellen von Angeboten. Beide Prozesse sind fortlaufend und gleichzeitig. Aktivitäten dienen dazu, den Umfang der Optionen nach Thema und Ort der Präsentation der Entscheidungen zu begrenzen. Eine Aktivität verweist auf eine [Kollektion](#offer-collections) und eine Platzierung. Es muss auch ein [Fallback-Angebot](#fallback-offers) angeben werden, das zum Einsatz kommt, wenn kein qualifizierendes Angebot ermittelt werden kann.

