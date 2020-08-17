---
keywords: Experience Platform;home;popular topics;decision events;decision event;Decision events
solution: Experience Platform
title: Domain-Modell von Experience Decisioning
topic: overview
description: In diesem Abschnitt werden die Komponenten von Decisioning Service erläutert und die Art und Weise, wie diese Komponenten miteinander interagieren, genau beschrieben. Die Konzepte und ihre Beziehungen bilden die *Domäne* des Entscheidungsproblems. Diese grundlegenden Komponenten spielen eine Rolle, unabhängig davon, wie Sie Decisioning Service nutzen].
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 91%

---


# Experience [!DNL Decisioning] domain model

In this section, the components of [!DNL Decisioning Service] are explained and the ways in which those components interact are detailed. Die Konzepte und ihre Beziehungen bilden die *Domain* des Entscheidungsproblems. These fundamental components come into play regardless of how you use [!DNL Decisioning Service].

## Entscheidungsoptionen

Eine *Entscheidungsoption* für ein Erlebnis ist ein potenzielles Erlebnis, das einem bestimmten Kunden angezeigt werden kann. Eine Option wird auch als Wahl oder Alternative bezeichnet. When deciding on the next best option for a customer, [!DNL Decisioning Service] considers options ***d<sub>1</sub>*** to ***d<sub>N</sub>*** from amongst a finite set of options **`D`**.

Entscheidungen werden getroffen, indem aus einer Reihe verfügbarer Optionen die beste Option ermittelt wird. Eine Möglichkeit besteht darin, *Entscheidungsoptionen* ***d<sub>i</sub>*** nacheinander aus Satz ***D*** zu entfernen, bis entweder nur noch eine Option übrig ist oder aus dem verbleibenden Satz ein zufälliger „Gewinner“ ausgewählt wird. Eine weitere Form der Entscheidungsfindung besteht darin, die verbleibenden (qualifizierten) Entscheidungsoptionen hinsichtlich der zu erwartenden Ergebnisse zu bewerten.

### Endlicher Satz von Entscheidungsoptionen

In der Experience Decisioning-Domain sind die Optionen, aus denen eine oder mehrere ausgewählt werden, a priori vorhanden; durch Berechnung einer Entscheidung werden spontan keine neuen Optionen erstellt. Wir sagen, dass die Domain der Optionen zum Entscheidungszeitpunkt begrenzt ist. Dies mag nach einer Beschränkung aussehen, doch bietet ein endlicher Satz an Optionen die Möglichkeit, maschinelle Lernalgorithmen und ähnliche Verfahren zu nutzen, um zu entscheiden, welche der Optionen „die beste“ ist. Viele Lernalgorithmen wären nicht dazu in der Lage, eine beste Option aus einem Satz unendlicher Alternativen zu ermitteln, die sich nicht miteinander vergleichen lassen und für die es keine Musterdaten gibt.

## Entscheidungsergebnisse

Es ist wichtig, zwischen der Ausgabe der Entscheidung `d` und dem Ergebnis `o`, d. h. den beabsichtigten Ergebnissen, die von der Entscheidung vorgeschrieben wurden, zu unterscheiden. Eine Entscheidung kann oft nicht direkt für ein Ergebnis sorgen. Bei der Entscheidung wird lediglich die Option mit dem am besten zu erwartenden Ergebnis ausgewählt (oder vorgeschlagen). Zwischen Vorschlägen und Ergebnissen treten viele Ereignisse und Interaktionen auf, oft um Tage oder Wochen verzögert. Formell betrachtet ist das Ergebnis eine Funktion der Entscheidung `o = f(d)`.

Zum Ermitteln der optimalen Entscheidung wird jedem Ergebnis ein ***Nutzwert*** `U(o) = U(f(d))` zugewiesen.
Für das Anwendungsbeispiel Angebotsentscheidung würde diese Funktion die Kosten für die Ausführung des Angebots und den vom Unternehmen erzielten Nutzen berechnen, sollte der Kunde das Angebot annehmen. Das Ergebnis dient dazu, die optimale Entscheidung (das optimale Angebot) zu finden, indem der Nutzwert für alle Optionen (Angebote) maximiert wird.

Im Allgemeinen ist es nicht möglich, mit Sicherheit vorherzusagen, wie das Ergebnis einer bestimmten Entscheidung aussehen wird. Das macht einen probabilistischen Ansatz erforderlich. Der ***Nutzwert*** `U(o)` wird zum ***erwarteten Nutzwert einer Entscheidungsoption*** `EU(d)`.

## Entscheidungsvorschläge

Bei einem *Entscheidungsvorschlag* handelt es sich um eine Auswahl von Entscheidungsoptionen, die als Reaktion auf eine tatsächliche Entscheidungsanfrage getroffen wurde. Wie bereits erwähnt, können die Ergebnisse einer Entscheidung viel später eintreten; zudem werden die Ergebnisse möglicherweise nicht in einem Schritt erreicht. Daher ist es wichtig, die Vorschläge über verschiedene *Erlebnisereignisse* hinweg zu verfolgen, damit sie sich wieder den Entscheidungsoptionen zuordnen lassen. Diese Feedback-Schleife dient dazu, die Vorhersagegenauigkeit für `EU(d)` zu erhöhen.

Ein Vorschlag wird als Entität persistiert und verfügt somit über eine Kennung. Die Entität enthält Verweise auf die ausgewählten Optionen und kann Kontextdaten erfassen, die bei der Entscheidungsfindung verwendet wurden. Dank der Kennung können auch andere Entitäten darauf verweisen. Eine dieser Entitäten ist ein *Entscheidungsereignis*. Es enthält den Zeitstempel, der den Zeitpunkt markiert, zu dem die Entscheidung (Vorschlag) getroffen wurde. Ein Entscheidungsereignis ist ein erfasstes Auftreten der Aktion zur Ausführung der Entscheidung. Andere Ereignisse, die auf die Vorschlagsentität verweisen, sind Erlebnisereignisse. Jedes Erlebnisereignis kann erweitert werden, um auf einen Entscheidungsvorschlag zu verweisen. Die Auslegung besteht darin, dass sich das Erlebnisereignis ganz oder teilweise auf den Vorschlag der Entscheidung zurückführen lässt.

## Entscheidungsstrategie – Algorithmus

Mit einem endlichen Satz an Alternativen, aus denen gewählt werden kann, ist jede *Entscheidungsstrategie* im Wesentlichen ein Algorithmus – oder eine Funktion –, der **`N`** Entscheidungsoptionen *{d<sub>1</sub>, d<sub>2</sub>, …d<sub>N</sub>}* als Eingabe verwendet und eine Rangfolge von Entscheidungsoptionen erzeugt *(d<sub>r1</sub>, d<sub>r2</sub>,…d<sub>rk</sub>)*. Dabei wird die erste Entscheidungsoption in der Liste mit Blick auf einen erwarteten Nutzen als optimal, die zweite Option in der Ergebnisliste als die zweitbeste Option betrachtet usw. In der Regel hat der Satz eine höhere Kardinalität als die resultierende Rangliste, da der Entscheidungsalgorithmus unqualifizierte Optionen eliminiert und ein Algorithmus möglicherweise so konfiguriert ist, dass nur die besten **`K`** Optionen zurückgegeben werden und der Algorithmus angehalten wird, sobald genügend Optionen gefunden wurden.
Das grundlegende Entscheidungs-Framework ist in der folgenden Abbildung dargestellt.

![Abb. 1](./images/decisioning-optimization.png)

## Entscheidungsaktivitäten

*Entscheidungsaktivitäten* konfigurieren den Algorithmus und stellen Parameter für eine bestimmte Entscheidungsstrategie bereit. Die Strategieparameter umfassen die Begrenzungen, die auf die Optionen und die Ranglistenfunktion angewendet werden. Alle Entscheidungen werden im Kontext einer Aktivität getroffen. [!DNL Decisioning Service] bietet zahlreiche Aktivitäten; Aktivitäten können kanalübergreifend wiederverwendet werden. Für jeden beliebigen Zeitpunkt wird die beste Option auf Grundlage des aktuellsten Satzes an Begrenzungen, Regeln und Modellen ausgewertet.

Eine Entscheidungsaktivität definiert die Sammlung der zu berücksichtigenden Entscheidungsoptionen. Es wird die Teilmenge aller Optionen herausgefiltert, die für diese Aktivität von Interesse sind. This allows the [!DNL Decisioning service] to manage topical categories within the catalog of all options.

Eine Entscheidungsaktivität gibt eine *Fallback-Option* an, falls die kombinierten Begrenzungen alle anderen Optionen disqualifizieren. Das heißt, dass es stets eine Antwort auf die Frage gibt: Was ist die derzeit „beste“ Option?

Entscheidungsaktivitäten können den Ort angeben, an dem das Erlebnis bereitgestellt wird. Dadurch wird die Zahl der Entscheidungsoptionen, die in Betracht gezogen werden können, weiter verringert; es handelt sich um eine weitere Begrenzung, die von der Entscheidungsaktivität auferlegt wird. Dieses Mittel wird als *Platzierungsbegrenzung* bezeichnet. Es werden nur solche Entscheidungsoptionen berücksichtigt, deren Inhalt die Platzierungsbegrenzung erfüllt. Dies wird in den frühen Phasen der Entscheidungsstrategie ausgewertet. Bei einer Änderung von Definitionen werden die Platzierungsbegrenzungen jeder Entscheidungsaktivität neu ausgewertet und die Entscheidungsoption kann für eine oder mehrere Entscheidungsaktivitäten in Betracht kommen bzw. außer Acht gelassen werden.

## Entscheidungskontext

Bisher wurde nur die geschäftliche *Logik* beschrieben, die sich auf die Entscheidung auswirkt. Noch wichtiger für die Ausgabe sind jedoch die *Eingabedaten* der Entscheidung. Diese Daten werden als *Entscheidungskontext* bezeichnet und unterscheiden sich je nach Benutzer und Zeitpunkt, zu dem eine Entscheidung getroffen wird – anders als Begrenzungen, Regeln und Modelle, die für verschiedene Benutzer bei der gleichen Aktivität gleich sind. Die Regeln, Begrenzungen und Modelle ändern sich auch seltener. Für Echtzeitentscheidungen muss auch der Entscheidungskontext in Echtzeit ermittelt werden.

Entscheidungskontextdaten können in mit Benutzerprofilen verbundene Daten, Geschäftsdaten und intern erfasste Daten unterteilt werden.

- *Profilentitäten* dienen zur Darstellung von Endbenutzerdaten, doch stellt nicht jede Profilentität eine einzelne Person dar. Es kann sich dabei auch um einen Haushalt, eine soziale Gruppe oder ein anderes Subjekt handeln. Erlebnisereignisse sind an ein Profil angehängte Zeitreihendatensätze. Wenn ein Erlebnis vorhanden ist, dann sind diese Daten das *Subjekt* dieses Erlebnisses.
- Auf der anderen Seite gibt es die *Geschäftsentitäten*. Sie können als die *Objekte* der Interaktionen betrachtet werden. Auf diese Entitäten wird häufig in den Erlebnisereignissen von Profilentitäten verwiesen. Beispiele für Geschäftsentitäten sind Websites und Seiten, Geschäfte, Produktdetails, digitale Inhalte, Produktinventardaten usw.
- The last category of data in the decision context is data that was created during operation of the [!DNL Decisioning Service]. Alle Entscheidungsereignisse fallen in diese Kategorie; zusammen mit den Antworten von Kunden bilden die Vorschlagsdaten einen internen Datensatz namens *Vorschlags-Antwort-Verlauf*.

Es gibt drei Wege, die die Daten nehmen können, um Teil des Entscheidungskontexts zu werden. Daten aus Datensätzen und Zeitreihen können über Datensatzdateien hochgeladen werden. Dieser Weg dient hauptsächlich der Massensynchronisierung mit externen Systemen. Record and time series data can also be streamed into [!DNL Platform] where the data is indexed and joined to form entities. Mit dem dritten Weg können Kontextdaten als Parameter an die Entscheidungsanfrage übergeben werden. Diese Form von Daten ist kurzlebig und nur für die angefragte Entscheidung relevant. Sie werden nicht als Entität persistiert und stehen nicht für andere Anfragen zur Verfügung.
