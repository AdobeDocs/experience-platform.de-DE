---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Angebot-Entscheidungsdomänenmodell
topic: overview
translation-type: tm+mt
source-git-commit: fdaef24a23c1c1da064ca33e8bed522e506fead5
workflow-type: tm+mt
source-wordcount: '2621'
ht-degree: 0%

---


# Übersicht über das Angebot-Entscheidungsdomänenmodell

Die Entscheidungsfindung im Angebot ist ein Anwendungsfall des Entscheidungsdienstes, bei dem Sie die Regeln und Prognosen, die für die Kundenbindung mit Angeboten verwendet werden, formalisieren und zentral verwalten. Angebot-Entscheidungsfindung wird als eine Art von _**Inhaltsentscheidung**_ betrachtet. In diesem Fall werden die _**Entscheidungsoptionen**_ als _**Angebot**_ bezeichnet und als solche durch den ihnen beigefügten Inhalt gekennzeichnet. Eine Einführung in das vom Entscheidungsdienst verwendete Objektmodell finden Sie unter [Entscheidungsdienst-Domänenmodell](experience-model.md).

Ziel ist es, dem Endbenutzer in jedem Kanal ein &quot;bestes Angebot&quot;auf der Grundlage von Targeting-Kriterien, Kosten- und Frequenzbeschränkungen sowie vorherigen Interaktionen zwischen Kanälen, einschließlich der zuvor vorgeschlagenen Angebot, bereitzustellen.

Wie bei allen Entscheidungs-Anwendungsfällen werden die Entscheidungsoptionen (Angebot) in einem Repository verwaltet, das von einer beliebigen Anzahl von Anwendungen gemeinsam genutzt wird. Angebot können von verschiedenen Abteilungen Ihrer Organisation oder von Partnern erstellt werden, und diese Angebot können täglich hinzugefügt und entfernt werden.

Angebot werden visuell durch die Anwendung, die das Erlebnis bereitstellt, in größere Erlebnisse eingefügt. _**Platzierungen**_, manchmal auch als Plätze oder Slots bezeichnet, sind wichtige Komponenten für die Erstellung einer Strategie. Die Entwicklung einer Angebot-Strategie führt oft zu Beginn mit der Definition dieser Platzierungen. Ein Angebot verfügt in der Regel über mehrere _**Inhaltsdarstellungen**_ , sodass es korrekt in eine Vielzahl von Erlebnissen integriert werden kann, bei denen jedes unterschiedliche dimensionale oder andere Einschränkungen hat und unterschiedliche Medienformate erfordert.

Angebote haben oft einen Zusammenhang mit Waren oder Dienstleistungen und es geht um eine Kostenberechnung. Eine Organisation muss in der Lage sein, die Ressourcen, die von Angeboten verbraucht werden, zu begrenzen, und muss daher in der Lage sein, die Gesamtanzahl der Vorschläge für ein Angebot zu _**begrenzen**_ .

Der prognostizierte Wert eines akzeptierten Angebots für das Unternehmen ist das Optimierungskriterium und steht im Widerspruch zu den Kosten für die Erstellung eines Angebots. Kosten, Annahmewahrscheinlichkeit und voraussichtlicher Wert werden zur Rangordnung der Angebot verwendet. Das beste Angebot ist das mit den höchsten prognostizierten positiven Auswirkungen auf die Ziele Ihrer Angebot-Aktivitäten.

Bei der Angebot-Entscheidungsfindung werden die Interaktionen berücksichtigt, die ein Endbenutzer _**über viele Kanal**_ und Anwendungen hinweg hatte, und es werden die Daten des Profil- und Erlebnis-Ereignisses eines Endbenutzers genutzt. Beispielsweise kann eine Call-Center-Anwendung mithilfe der Angebot-Entscheidungsfunktion ein Angebot aktivieren oder unterdrücken, das auf Käufen und Reviews basiert, die vom Endbenutzer veröffentlicht wurden. oder eine E-Mail-Management-Anwendung kann sich darauf verlassen, dass Angebot-Entscheidungsfindung das Nächste Beste Angebot in einem wöchentlichen Newsletter auswählt, basierend auf dem Browserverlauf auf einer Website.

Angebote haben andere interessante Eigenschaften. Häufig gibt es einen definierten _**Zeitplan**_ oder einen Datums- und Zeitbereich, wann das Angebot gültig ist und wann das Angebot ungültig gemacht werden muss.

Schließlich verschlechtert sich die Attraktivität eines Angebots mit der Häufigkeit seiner Darstellung. Ein Angebot, das nicht akzeptiert wird, nachdem es wiederholt vorgeschlagen wurde, ist eine verlorene Chance, weil ein anderes Angebot hätte vorgelegt werden können. Aus diesem Grund muss die _**Ermüdung**_ der Endbenutzer beherrscht werden.

## Entscheidungsstrategie für Angebote auf einen Blick

Der Gesamtansatz besteht darin, die Auswahl der Angebot einzugrenzen, bis alle Einschränkungen erfüllt sind, dann das Rangmodell auf die verbleibenden Optionen anzuwenden und dann mithilfe von Einschränkungen (Deduplizierung und Vermeidung von Ausweichmöglichkeiten) über mehrere Aktivitäten hinweg zu optimieren.

| Strategiekomponente | Realisiert als |
| --- | --- |
| Entscheidungs-Aktivitäten | Angebot-Aktivitäten |
| Entscheidungsoptionen | Angebot mit Inhaltsdarstellungen |
| Ausweichoptionen | Fallback-Angebot mit Inhaltsdarstellungen |
| Endgültige Reihe von Entscheidungsoptionen | Angebot-Inventar (auch bekannt als Angebot-Bibliothek) |
| Topische Kategorien | Angebot-Filter basierend auf Tags und Angebot-IDs |
| Entscheidungsergebnisse | Vorschlag eines Angebots pro Aktivität für mehrere Aktivitäten gleichzeitig |
| Entscheidungsergebnisse | Erwartetes Erlebnis-Ereignis mit Verweis auf das Angebot, z. `eventType='opened'` |
| Entscheidungsalgorithmus | Interne Dienstlogik, parametrisiert |
| Einschränkungen | Platzierungsbeschränkungen, Kalendereinschränkungen, Einschränkungen für globale und pro Benutzer-Capping, Deduplizierungseinschränkungen |
| Entscheidungsregeln | Eignungsregeln |
| Modell für *erwartetes Dienstprogramm* | Angebot-Rang oder -Priorität |

Die Gesamtzahl der Angebot im Bestand an Optionen ist in der Regel recht groß (in der Größenordnung von 10.000), und jede Angebot-Aktivität kann sich auf Angebot konzentrieren, die in eine andere Kategorie fallen (Thema). Die Angebot-Entscheidungsstrategie ermöglicht das Anhängen eines Angebot-Filters an eine Angebot-Aktivität. Weitere Einschränkungen werden zum Zeitpunkt der Anforderung der Entscheidung bewertet.
In den folgenden Abschnitten werden die Komponenten für die Angebot-Entscheidungsdomäne detailliert erläutert.

## Allgemeine Angebote

Allgemeine Angebote, auch als personalisierte Angebote bezeichnet, stehen im Mittelpunkt der Aktivitäten der Angebote. Sie haben Attribute wie Name und Status. Das Statusattribut gibt an, ob die Entität bereit ist, in die Liste aktiver genehmigter Angebot aufgenommen zu werden. Allgemeine Angebote werden mehrere Einschränkungen haben. Mehr dazu in Abschnitt ‎ Einschränkungen [unten](#offer-constraints).

## Inhalt in Angeboten

### Praktika für Angebote

Platzierungen definieren Inhaltsbeschränkungen und geben mit einer Aktivität den Ort an, an dem das nächste beste Erlebnis bereitgestellt wird. Dies verringert die Anzahl der Optionen, die in Betracht gezogen werden können, und stellt eine weitere Einschränkung dar, die von der Aktivität auferlegt wird. Dies wird als Platzierungsbeschränkung bezeichnet. Es werden nur Optionen in Betracht gezogen, bei denen Inhalt eine Platzierungseinschränkung erfüllt, z. B. Angebote. Dies wird in den frühen Phasen der Entscheidungsstrategie bewertet. Wenn Optionsobjekte die Platzierungseinschränkungen jeder Aktivität ändern, werden diese neu bewertet und die Option kann für eine oder mehrere Aktivitäten in Betracht gezogen oder ausgeschlossen werden.

Der Entscheidungsdienst ist nicht dafür verantwortlich, die komplexen Details der Inhaltsabhängigkeiten zu formalisieren. Stattdessen identifiziert jeder Kunde die Liste der Platzierungen in allen Kanälen und gibt diesen Platzierungen eindeutige Bezeichner und Namen. Durch Verweis auf eine bestimmte Platzierung bestätigt der Designer, dass der angegebene Inhalt in die Platzierung passt.

Wenn Inhalte entwickelt werden, wird der Angebot-Marketingspezialist und der Inhaltsentwickler einfach einen &quot;impliziten Vertrag&quot;vereinbaren, der hinter dem Namen &quot;Startseite Hero Image&quot;oder &quot;Service Call Open Script&quot;steht. Das erste Bild kann als Bild von 600 px Breite und 350 px Höhe vereinbart werden, und das zweite kann den Inhalt auf Text in zwei Sprachvarianten beschränken, die nicht mehr als 50 Wörter in drei oder vier Sätzen mit semantischer Struktur sind. Platzierung, um nicht die gesamte Bedeutung des ausgeblendeten Vertrags zu speichern.

### Angebotsdarstellungen

Um sicherzustellen, dass ein Angebot in den verschiedenen Parametern der Platzierungen in Ihren Kanälen korrekt dargestellt werden kann, müssen verschiedene Darstellungen dieses Angebots erstellt werden. Der an Angebot angehängte Inhalt wird nach Platzierungen gruppiert. Jedes Angebot kann eine oder mehrere Darstellungen aufweisen, bei denen jede dieser Darstellungen auf eine der definierten Platzierungen verweist. Jede Darstellung in einem Angebot muss eine andere Platzierung verwenden. Je mehr Darstellungen ein Angebot hat, desto mehr Möglichkeiten besteht es, das Angebot in verschiedenen Platzierungs-Kontexten zu verwenden.

Eine Platzierung schränkt den Typ der Inhaltselemente ein, die der Präsentation hinzugefügt werden können.

## Fallback-Angebote

Fallback-Angebot sind Entscheidungsoptionen, für die außer den Platzierungsregeln keine zusätzlichen Einschränkungen gelten. Fallback-Angebot haben Inhaltsdarstellungen, die wie jedes andere Angebot an Platzierungen gebunden sind.

Fallback-Angebot werden in Aktivitäten angegeben, um ein brauchbares Inhaltserlebnis anzuzeigen, das verwendet werden kann, wenn kombinierte Einschränkungen alle eingeschränkten Optionen deaktivieren. Da die Platzierungsbeschränkung nicht vom Laufzeitkontext oder vom Profil abhängig ist, kann sie bereits im Vorfeld des Zusammenbaus der Aktivität überprüft werden. Mithilfe von Fallback-Angeboten gibt es immer eine Antwort auf die Frage: Welches ist derzeit das beste Angebot?

## Einschränkungen des Angebots

### Kalendereinschränkungen

In der Entscheidungsdomäne &quot;Angebot&quot;haben die Angebot eine Gültigkeitsdauer. Das bedeutet, dass das Angebot nicht vor Ablauf des Beginns und der Uhrzeit vorgeschlagen werden kann und nach Ablauf des Enddatums und der Frist nicht mehr vorgeschlagen werden kann. Die Angebot-Entität verfügt über eine einfache Struktur, die diese Kalendereinschränkungen definiert.

In regelmäßigen Abständen werden abgelaufene Angebot aus der Liste der betreffenden Optionen entfernt. Der Kalenderfilter wird jedoch zum Zeitpunkt der Anforderung der Entscheidung angewendet, damit die Beschränkungen präzise angewendet werden.

### Beschränkungen für die Deckelung

Angebot können eine optionale Beschränkung zum Kappen haben. Es besteht aus zwei Werten:

- Der globale Grenzwert beschränkt, wie oft ein Angebot im gesamten Profil (gezielte Audience) vorgeschlagen werden kann.

- Die Obergrenze pro Profil und legt fest, wie oft das Angebot für dasselbe Profil vorgeschlagen werden kann.

### Duplizierungsbeschränkungen

Wenn eine Entscheidung beantragt wird, kann der Kunde gleichzeitig nach Vorschlägen für mehrere Aktivitäten fragen. Dies ist ein typisches Szenario bei der Inhaltsentscheidung. Jede Aktivität trägt eine oder mehrere Inhaltsoptionen zum Gesamterlebnis bei. Aufgrund der Zusammensetzung müssen Entscheidungen über mehrere Aktivitäten hinweg getroffen werden, um Doppelarbeit zu vermeiden - es sei denn, die Aktivitäten wählen jeweils einen Teil des GesamtOptionsinventars aus. Eine hochrangige Option wird in allen Aktivitäten wahrscheinlich einen hohen Rang einnehmen, und es wäre eine schlechte Erfahrung, wenn alle Aktivitäten dieselbe Option vorschlagen würden. Wenn ein Versand andererseits wissen möchte, was die &quot;Nächste beste Konversion&quot;über alle Kanal hinweg ist und es keine Beschränkung der Deckelung gibt, könnte es in Ordnung sein, dieselbe Option für verschiedene Aktivitäten vorzuschlagen.

Duplizierungsbeschränkungen werden derzeit nicht in das Repository für Geschäftsobjekte geschrieben. Stattdessen ist die Deduplizierung zur Laufzeit die Standardstrategie. Ein Anforderungsparameter kann das Standardverhalten überschreiben, um Deduplizierungsschritte zu unterdrücken.

### Einschränkungen des Profils - Eignungsregeln

Bislang waren die diskutierten Einschränkungen unabhängig davon anwendbar, für wen das Angebot ausgewählt wurde. Die Erfahrungsentscheidung unterstützt auch einen Anwendungsfall, bei dem die Personalisierung von Angeboten auf den Ereignissen der Datensatz- und Zeitreihen des Kunden basiert. Regeln werden pro Profil ausgewertet, um zu entscheiden, ob ein Angebot für diesen Benutzer qualifiziert ist oder unterdrückt werden muss. Dazu kann jedem Angebot eine Eignungsregel zugeordnet werden. Neben den Profil- und Erlebnis-Ereignissen eines Endbenutzers berücksichtigt die Eignungsregel Echtzeitkontextdaten. Diese Daten werden vom Versand-Dienst bereitgestellt und können in Form von Daten vorliegen, die nicht mit einem Profil in Zusammenhang stehen, z. B. Lagerbestände, Wetterbedingungen und Flugpläne.

Es ist wichtig, zwischen Targeting- und Segmentierungsregeln und zwischen Berechtigungs- und Prioritätsregeln für die Entscheidungsfindung zu unterscheiden. Für das Targeting einer Reihe von Profilen ist die Ausgabe (Auswahl der Audience) für die Berechtigung ein Optionssatz (zulässige Angebot) ist die Ausgabe der Auswertung.

## Angebot-Sammlungen

Die Bestandsaufnahme ist der Gesamtpool der Optionen, die bei der Entscheidungsfindung berücksichtigt werden. Das Inventar kann weiter in Kategorien oder Sammlungen unterteilt werden. Eine Reihe von Optionen wird durch ein gemeinsames Tag dargestellt, über das diese Optionen verfügen. Filter werden zum Testen verwendet, wenn Angebot in eine bestimmte Kategorie fallen oder, genauer gesagt, dieselben Tags oder Tags gemeinsam verwenden.

### Tags

Tags bieten eine Möglichkeit, auszudrücken, dass eine Gruppe von Optionen zu einer Kategorie gehört.

Eine Option kann über mehr als ein Tag verfügen und kann daher gleichzeitig in mehreren Kategorien vorliegen. Kategorien können sich auch überlappen oder andere enthalten. Wenn eine Kategorie &quot;S&quot;von Angeboten mit dem Tag &quot;A&quot;und die Kategorie &quot;R&quot;durch Optionen mit den Tags &quot;A&quot;und &quot;B&quot;definiert wird, wird &quot;S&quot;eine Obermenge von &quot;R&quot;sein.

### Filter

Filter werden verwendet, um die Kriterien für einen Optionssatz zu definieren, der zu einer Kategorie gehört. Filter können als Abfragen gegen das Inventar von Angeboten betrachtet werden. Es gibt zwei grundsätzliche Möglichkeiten, einen Filter zu bilden: durch Angabe, dass ein Angebot über ein oder mehrere Tags verfügt, und durch explizite Auswahl der Angebot. Die bisherige Methode kann so konfiguriert werden, dass festgestellt wird, dass ein Angebot in dieser Sammlung alle angegebenen Tags aufweisen muss oder dass eine Option qualifiziert ist, wenn es mindestens eines der angegebenen Tags hat.

Wenn Optionen explizit in eine Sammlung platziert werden, wird ihr Tag-Satz für diese Sammlung ignoriert.

## Angebot-Aktivitäten

Aktivitäten konfigurieren und steuern den Entscheidungsprozess. Derzeit ist die Entscheidungsstrategie im Wesentlichen vorab festgelegt, aber künftige Iterationen des Angebot Decision Domain-Modells werden die Auswahl von Modellen, zusätzlichen Regeln und Einschränkungen ermöglichen.

Ein Erlebnis kann mit vielen Aktivitäten gleichzeitig zusammengestellt werden. Derzeit können bis zu 30 Aktivitäten in einer einzigen Entscheidungsanforderung behandelt werden. Wenn mehr als 30 Aktivitäten oder Slots in einem Erlebnis mit Inhalten gefüllt werden müssen, können für dasselbe Profil mehrere Anforderungen gestellt werden. Werden jedoch Aktivitäten in ein und demselben Entscheidungsersuchen einbezogen, so werden die Angebotsvorschläge zwischen diesen Aktivitäten dedupliziert.

Wenn Aktivitäten so definiert werden, dass sie aus unterschiedlichen Angeboten ausgewählt werden, macht es kaum einen Unterschied, ob Aktivitäten in derselben Anforderung kombiniert oder in separate Anforderungen aufgeteilt werden. Allerdings erfordern Netzwerk- und Reaktionszeitbeschränkungen möglicherweise, dass Aktivitäten in derselben Anforderung kombiniert werden. Da verschiedene Anforderungen an verschiedene Dienstknoten weitergeleitet werden, müssen möglicherweise dieselben Profil-Daten in verschiedene Nodes abgerufen werden. Dadurch wird die effektive IO-Bandbreite für andere Anforderungen reduziert.

Aktivitäten werden verwendet, um Inhalte in ein Erlebnis einzufügen. Um sicherzustellen, dass die Inhaltselemente korrekt &quot;passen&quot;, verweist eine Aktivität auf eine einzelne Platzierung. Beachten Sie, dass eine Platzierung nicht immer ein konkreter Ort/Steckplatz ist, sondern eher eine Abstraktion dieser Orte/Slots. Beispielsweise könnte jede Kachel auf einer Webseite mit einem Raster aus Kacheln durch die gleiche Platzierung gesteuert werden, vorausgesetzt, sie haben alle eine ähnliche Form und Größe und können ähnliche Inhalte enthalten. Eine einzelne Kachel würde jedoch in der Regel von ihrer eigenen Aktivität bereitgestellt.

Die folgende Abbildung zeigt, wie die Geschäftseinheiten miteinander verbunden sind:

![](./images/figure-10.png)

Wenn Kunden das Objektdiagramm für Entscheidungen erstellen und verknüpfen, gibt es in der Regel drei verschiedene Arbeitsströme. Folgende sind vorhanden:

- Einrichten der unterstützenden Entitäten wie Tags und Platzierungen. Diese Entitäten werden verwendet, um andere Entitäten zu strukturieren, zu filtern und zu gruppieren. Sie werden auch verwendet, um eine gewisse Koordinierung zwischen dem zweiten und dritten Arbeitsablauf zu gewährleisten. Dieser Arbeitsablauf stellt eine gewisse Vorarbeit dar, kann jedoch jederzeit verfeinert werden. Tags sind relativ einfach, Platzierungen erfordern jedoch etwas mehr Planung. Ein Unternehmen muss mindestens eine Bestandsaufnahme aller Stellen vornehmen, an denen eine Entscheidung getroffen wird.

- Erstellen von Angeboten mit den verschiedenen Darstellungen und Geschäftsregeln (Einschränkungen). Dieser zentrale Arbeitsablauf bietet die Optionen, unter denen wir die besten auswählen müssen. Die Tags des ersten Workflows werden zur Kategorisierung von Angeboten verwendet, und die Platzierungen geben an, welche Optionen und wo angezeigt werden können.

   - Dieser Arbeitsablauf definiert auch absolute Einschränkungen für die Angebot. Sie sind absolut, weil sie immer durchgesetzt werden und sich nicht nur auf die Rangliste einer Reihe von Angeboten auswirken. Wenn beispielsweise eine Kalenderbeschränkung festgelegt wird, wird erzwungen, dass das Angebot nie vor dem festgelegten Beginn (Datum/Uhrzeit) und nie nach dem Enddatum/der Endzeit ausgewählt wird. Die Einschränkungen, die in diesem Workflow festgelegt werden, sind die [Kalendereinschränkungen](#calendar-constraints), [Beschränkungen](#capping-constraints) für die Begrenzung und [Einschränkungen](#profile-constraints---eligibility-rules)der Berechtigung. Ein Unterarbeitsablauf hier ist die Definition zusätzlicher Regeln, die bestimmen, wer für ein bestimmtes Angebot berechtigt ist.

      - Bei der Erstellung von Einschränkungen für ein Angebot werden dessen Darstellungen ausgewählt. Bei diesem Arbeitsablauf wird davon ausgegangen, dass der Inhalt bereits irgendwo erstellt wurde und einfach in das Inhalts-Repository hochgeladen und dort ausgewählt wird. Hier werden die Platzierungen des ersten Workflows abgespielt. Ein Angebot kann Platzierungen auswählen und den Inhalt unter dieser [Platzierung](#offer-placements)verknüpfen.

      - Das Erstellen geeigneter Fallback-Angebot ist der letzte Schritt in diesem Arbeitsablauf. Ein Fallback-Angebot ähnelt einem allgemeinen Angebot ohne Einschränkungen.

- Der letzte Arbeitsablauf betrifft die Erstellung von Aktivitäten. Dieser Schritt erfolgt jedoch nicht unbedingt sequenziell nach dem Arbeitsablauf zum Erstellen von Angeboten. Beide Prozesse laufen noch und sind gleichzeitig. Aktivitäten werden dazu verwendet, den Umfang der Optionen nach Thema und Ort der Entscheidungsvorstellung einzugrenzen. Eine Aktivität verweist auf eine [Sammlung](#offer-collections) und eine Platzierung. Es muss auch ein [Ausweich-Angebot](#fallback-offers) angeben, das verwendet wird, wenn ein qualifizierendes Angebot nicht ermittelt werden kann.

