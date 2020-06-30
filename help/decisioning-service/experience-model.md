---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Domänenmodell für Erlebnisentscheidung
topic: overview
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 0%

---


# Erlebnis- [!DNL Decisioning] Domänenmodell

In diesem Abschnitt [!DNL Decisioning Service] werden die Komponenten erläutert und die Art und Weise, wie diese Komponenten interagieren, detailliert beschrieben. Die Konzepte und ihre Beziehungen bilden die *Domäne* des Entscheidungsproblems. Diese fundamentalen Komponenten spielen eine Rolle, unabhängig davon, wie Sie sie verwenden [!DNL Decisioning Service].

## Entscheidungsoptionen

Eine Erlebnis- *Entscheidungsoption* ist ein potenzielles Erlebnis, das einem bestimmten Kunden präsentiert werden kann. Eine Option wird auch als Alternative bezeichnet. Bei der Entscheidung über die nächste beste Option für einen Kunden [!DNL Decisioning Service] werden die Optionen ***d<sub>1</sub>***bis***<sub>dN</sub>*** aus einem begrenzten Optionssatz berücksichtigt **`D`**.

Entscheidungen werden getroffen, indem die beste Option in einer Reihe verfügbarer Optionen ermittelt wird. Eine Möglichkeit besteht darin, die *Entscheidungsoptionen* von ***<sub>Di</sub>***nacheinander aus dem Set*** D ***zu entfernen, bis entweder nur einer übrig bleibt, und dann einen &quot;Gewinner&quot;zufällig aus dem verbleibenden Satz zu wählen. Eine andere Form der Entscheidungsfindung besteht darin, die verbleibenden (förderfähigen) Entscheidungsoptionen nach ihrem erwarteten Ergebnis zu bewerten.

### Endlicher Satz von Entscheidungsoptionen

In der Erlebnisbestimmungsdomäne gibt es die Optionen, von denen eine oder mehrere ausgewählt sind, a priori, und durch die Berechnung einer Entscheidung werden keine neuen Optionen spontan erstellt. Wir sagen, dass der Bereich der Optionen zum Zeitpunkt der Entscheidungen begrenzt ist. Dies mag wie eine Einschränkung erscheinen, aber eine begrenzte Auswahl an Optionen gibt die Möglichkeit, maschinelle Lernalgorithmen und ähnliche Techniken zu verwenden, um zu entscheiden, welche der Optionen &quot;die beste&quot;ist. Viele Lernalgorithmen wären nicht in der Lage, eine der besten Optionen einer Reihe unendlicher Alternativen zu bieten, die nicht miteinander verglichen werden können und für die keine Musterdaten vorhanden sind.

## Entscheidungsergebnisse

Es ist wichtig, zwischen dem Ergebnis der Entscheidung `d` und dem Ergebnis, d.h. den beabsichtigten Ergebnissen, die in der Entscheidung festgelegt wurden, zu unterscheiden `o`. Eine Entscheidung kann oft nicht direkt zu einem Ergebnis führen. In der Entscheidung wird nur die Option mit dem am besten erwarteten Ergebnis ausgewählt (oder vorgeschlagen). Zwischen Vorschlägen und Ergebnissen treten viele Ereignis und Interaktionen auf, die oft durch Tage oder Wochen verzögert werden. Formell gesehen ist das Ergebnis eine Funktion des Beschlusses `o = f(d)`.

Zur optimalen Entscheidung wird jedem Ergebnis ein ***Dienstprogrammwert*** zugewiesen `U(o) = U(f(d))`.
Für den Anwendungsfall der Angebot-Entscheidungsfindung würde diese Funktion die Kosten für die Erfüllung des Angebots und den vom Unternehmen erzielten Wert berechnen, wenn das Angebot vom Kunden akzeptiert wird. Das Ergebnis wird verwendet, um die optimale Entscheidung (Angebot) zu finden, indem der Dienstprogrammwert über alle Optionen (Angebot) maximiert wird.

Es ist im Allgemeinen nicht möglich, mit Sicherheit vorherzusagen, wie das Ergebnis einer bestimmten Entscheidung aussehen wird, und daher ist ein probabilistischer Ansatz erforderlich. Der ***Dienstprogrammwert*** wird zum `U(o)` ***erwarteten Nutzwert einer Entscheidungsoption*** `EU(d)`

## Beschlussvorschläge

Bei einem *Entscheidungsvorschlag* handelt es sich um eine Auswahl der Entscheidungsoption, die auf ein tatsächliches Entscheidungsersuchen hin getroffen wurde. Wie bereits erwähnt, können die Ergebnisse einer Entscheidung viel später eintreten, und die Ergebnisse werden möglicherweise auch nicht in einem Schritt erreicht. Daher ist es wichtig, die Vorschläge über verschiedene *Erfahrungswerte* nachzuverfolgen, damit sie den Entscheidungsoptionen zugeordnet werden können. Diese Feedback-Schleife wird verwendet, um die Präzisionsgenauigkeit für `EU(d)`die Vorschau zu verbessern.

Ein Vorschlag wird als Entität beibehalten und hat daher einen Bezeichner. Die Entität enthält Verweise auf die ausgewählten Optionen und kann Kontextdaten aufzeichnen, die bei der Entscheidungsfindung verwendet wurden. Mit einer Kennung können auch andere Entitäten darauf verweisen. Eine dieser Einrichtungen ist *Decision Ereignis*. Es enthält den Zeitstempel und kennzeichnet den Zeitpunkt, zu dem seine Entscheidung (Vorschlag) getroffen wurde. Ein Ereignis einer Entscheidung ist ein festgestelltes Vorkommen der Maßnahme zur Vollstreckung der Entscheidung. Andere Ereignis, die auf die Entität des Proposition verweisen, sind Erlebnis-Ereignis. Jedes Erlebnis-Ereignis kann erweitert werden, um auf ein Entscheidungsvorschlag zu verweisen. Die Auslegung, dies zu tun, ist, dass das Ereignis der Erfahrung ganz oder teilweise auf den Vorschlag der Entscheidung zurückgeführt werden kann.

## Entscheidungsstrategie - Algorithmus

Mit einem endlichen Satz an Alternativen, aus denen Sie wählen können, ist jede *Entscheidungsstrategie* im Wesentlichen ein Algorithmus - oder eine Funktion -, der **`N`** Entscheidungsoptionen *{d<sub>1</sub>, d<sub>2</sub>, ...<sub>dN</sub>}als Eingabe trifft und eine Rangfolge von Entscheidungsoptionen erzeugt (siehe z.B.* *<sub></sub><sub></sub><sub></sub>* dR1, drk...Listedrdk.)Wenn die erste Entscheidungsoption in der Liste gemäß einem erwarteten Dienstprogramm als optimal angesehen wird, gilt die zweite Option in der Ergebnisoption als die zweitbeste Liste usw. In der Regel hat der Satz eine höhere Kardinalität als die resultierende Rangansicht-Liste, da der Entscheidungsalgorithmus Optionen eliminiert, die nicht zugelassen sind, und ein Algorithmus möglicherweise so konfiguriert wird, dass nur die obersten **`K`** Optionen zurückgegeben werden, wobei der Algorithmus angehalten wird, nachdem genügend Optionen gefunden wurden.
Der allgemeine Entscheidungsrahmen ist in der folgenden Abbildung dargestellt.

![Abb. 1](./images/decisioning-optimization.png)

## Entscheidungs-Aktivitäten

*Entscheidungs-Aktivitäten* konfigurieren den Algorithmus und die Lieferparameter für eine bestimmte Entscheidungsstrategie. Die Strategieparameter umfassen die Beschränkungen, die auf die Optionen und die Rangfunktion angewendet werden. Alle Entscheidungen werden im Rahmen einer Aktivität getroffen. [!DNL Decisioning Service] Hosts viele Aktivitäten und Aktivitäten können über Kanal hinweg wiederverwendet werden. Die beste Option wird zu jeder Zeit auf der Grundlage der aktuellsten Beschränkungen, Regeln und Modelle bewertet.

Eine Entscheidungs-Aktivität definiert die Erhebung der zu berücksichtigenden Entscheidungsoptionen. Es wird eine Untergruppe aller Optionen Filter, die für diese Aktivität von Interesse sind. Dadurch kann die [!DNL Decisioning service] Verwaltung von topischen Kategorien im Katalog aller Optionen erfolgen.

Eine Entscheidungs-Aktivität gibt eine *Ausweichoption* an, falls die kombinierten Beschränkungen alle anderen Optionen deaktivieren. Das bedeutet, dass es immer eine Antwort auf die Frage gibt: Was ist derzeit die beste Option?

Die Aktivitäten der Entscheidung können den Ort angeben, an dem das Erlebnis bereitgestellt wird. Dadurch wird die Anzahl der Entscheidungsoptionen, die in Betracht gezogen werden können, weiter verringert, und es handelt sich um eine weitere Einschränkung, die durch die Aktivität der Entscheidung auferlegt wird. Dies wird als *Platzierungsbeschränkung* bezeichnet. Es werden nur die Entscheidungsoptionen berücksichtigt, bei denen Inhalt diese Platzierungseinschränkung erfüllt. Dies wird in den frühen Phasen der Entscheidungsstrategie bewertet. Bei einer Änderung der Begriffsbestimmungen werden die Platzierungseinschränkungen jeder Entscheidungs-Aktivität neu bewertet und die Entscheidungsoption kann für eine oder mehrere Aktivitäten in Betracht kommen oder außer Acht gelassen werden.

## Entscheidungskontext

Bisher wurde nur die *Geschäftslogik* beschrieben, die die Entscheidung beeinflusst. Noch wirkungsvoller für die Produktion sind jedoch die *Eingabedaten* der Entscheidung. Diese Daten werden als *Entscheidungskontext* bezeichnet und unterscheiden sich für jeden Nutzer und jedes Mal, wenn eine Entscheidung getroffen wird - im Gegensatz zu Einschränkungen, Regeln und Modellen, die für verschiedene Nutzer für die gleiche Aktivität gleich sind. Die Regeln, Einschränkungen und Modelle ändern sich ebenfalls seltener. Für Entscheidungen in Echtzeit muss der Entscheidungskontext auch in Echtzeit festgelegt werden.

Die Kontextdaten von Entscheidungen können in benutzerspezifische Daten, Geschäftsdaten und intern erfasste Profil unterteilt werden.

- *Profil-Entitäten* werden zur Darstellung von Endbenutzerdaten verwendet, aber nicht jede Profil-Entität stellt eine Einzelperson dar. Es könnte ein Haushalt, eine soziale Gruppe oder ein anderes Thema sein. Erlebnis-Ereignis sind an ein Profil angehängte Datensätze aus der Zeitreihe. Wenn ein Erlebnis vorhanden ist, dann sind diese Daten der *Gegenstand* dieses Erlebnisses.
- Auf der anderen Seite gibt es die *Geschäftseinheiten*. Sie können als *Objekte* der Interaktionen betrachtet werden. Auf diese Entitäten wird häufig in den Erlebnis-Ereignissen von Profil-Entitäten verwiesen. Beispiele für Geschäftseinheiten sind Websites und Seiten, Stores, Produktdetails, digitale Inhalte, Produktinventardaten usw.
- Die letzte Kategorie von Daten im Entscheidungskontext sind Daten, die während des Betriebs der [!DNL Decisioning Service]Variablen erstellt wurden. Jedes Ereignis der Entscheidungsfindung fällt in diese Kategorie, zusammen mit den Antworten der Kunden bilden die Propositiondaten einen internen Datensatz namens *Proposition-Response-Verlauf*.

Es gibt drei Wege, die die Daten einschlagen können, um Teil des Entscheidungskontexts zu werden. Daten aus Datensatz- und Zeitreihen können über Datensatzdateien hochgeladen werden. Dieser Pfad dient hauptsächlich zur Massensynchronisierung mit externen Systemen. Daten aus Datensatz- und Zeitreihen können auch an [!DNL Platform] die Stelle gestreamt werden, an der die Daten indexiert und mit Formularelementen verbunden sind. Über den dritten Pfad können Kontextdaten als Parameter an die Entscheidungsanforderung übergeben werden. Diese Datenform ist vorübergehend und nur für die erbetene Entscheidung relevant. Es wird nicht als Entität beibehalten und steht nicht für andere Anforderungen zur Verfügung.
