---
title: Überwachen signifikanter Änderungen und Zielgruppenvorhersagen mit dem KI-Assistenten
description: Erfahren Sie, wie Sie mit dem KI-Assistenten signifikante Änderungen überwachen und Zielgruppen in Adobe Experience Platform prognostizieren können.
badge: Alpha
exl-id: 8f34d378-a8a0-420d-8e45-39a5aafdd7b7
source-git-commit: 4dc07313127e62e15a5090ab71ad62b8957df977
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 0%

---

# Überwachen Sie signifikante Änderungen und prognostizieren Sie das Zielgruppenwachstum mit AI Assistant

>[!AVAILABILITY]
>
>Diese Funktion befindet sich im Alpha und steht Ihrer Organisation möglicherweise nicht zur Verfügung. Um am Alpha-Programm teilzunehmen und auf diese Funktion zuzugreifen, wenden Sie sich an Ihr Adobe-Account-Team.

In der heutigen datengesteuerten Marketing-Landschaft sind rechtzeitige und genaue Einblicke unerlässlich. Egal, ob Sie ein Business-Anwender oder im Marketing-Bereich sind, Sie benötigen die Fähigkeit, konsistent mit Ihren Audiences zu interagieren und schnelle und wirkungsvolle Anpassungen auf der Grundlage klarer Einblicke vorzunehmen. Um die Ausrichtung beizubehalten oder Ihre Geschäftsziele zu erreichen, müssen Sie über die verwertbaren Informationen verfügen, die für effektive Kampagnen und die Optimierung von Ressourcen erforderlich sind.

Sie können den KI-Assistenten für Adobe Experience Platform verwenden, um signifikante Änderungen zu überwachen und Wachstumsprognosen für Ihre Audience und Datensatzgrößen bereitzustellen. Anschließend können Sie diese Informationen verwenden, um die Integrität Ihrer Zielgruppendaten sicherzustellen und zukunftsgerichtete Prognosen anzubieten, um dateninformierte Entscheidungsfindungen zu unterstützen.

Lesen Sie dieses Dokument, um zu erfahren, wie Sie mit dem KI-Assistenten signifikante Änderungen überwachen und das Zielgruppenwachstum und Schwankungen vorhersagen können.

## Wichtige Terminologie und Definitionen {#key-terminology-and-definitions}

In der folgenden Tabelle finden Sie eine Liste wichtiger Begriffe und der zugehörigen Definitionen.

| Terminologie | Definition |
| --- | --- |
| wesentliche Änderung | Eine signifikante Änderung ist eine große prozentuale Änderung der Zielgruppen- oder Datensatzgröße, die durch bestimmte Schwellenwerte definiert wird (z. B. 10 % für große Zielgruppen). Signifikante Änderungen können zur Identifizierung von Anomalien beitragen, die die Datenstabilität beeinträchtigen. |
| Anomalien | Anomalien sind unerwartete Variationen in den Daten, z. B. ein plötzliches Wachstum von 20 % bei einer Zielgruppe **High-Value-**). Eine Anomalie kann durch ein potenzielles Problem bei der Datenaufnahme oder eine Änderung der Zielgruppendefinition verursacht werden. |
| Historische Daten | Historische Daten beziehen sich auf langfristige Daten, die in der Regel ein bis drei Jahre umfassen. Sie können historische Daten verwenden, um Muster zu verfolgen. **Hinweis**: Während des Alphas liefert der KI-Assistent historische Daten von bis zu 13 Monaten. |
| Neue/aktuelle Daten | Neue oder aktuelle Daten beziehen sich auf Datenpunkte, die über einen kurzen Zeitraum, in der Regel eine Woche oder bis zu 30 Tage, beobachtet wurden. Sie können neue oder aktuelle Daten verwenden, um unmittelbare Trends hervorzuheben und schnelle Anpassungen vorzunehmen. |
| Prognose | A-Prognosen sind Vorhersagen der zukünftigen Zielgruppen- oder Datensatzgröße, die auf früheren Trends basieren. Prognosedaten können zur Unterstützung der langfristigen Planung verwendet werden. |
| Zielgruppengröße | Audience-Größe bezieht sich auf die Gesamtzahl der Profile innerhalb einer Audience. Die Zielgruppengröße wird mit jeder Iteration der Datenaufnahme aktualisiert. |
| Zeitrahmen für den Vergleich | Der KI-Assistent verwendet vordefinierte Vergleichszeitrahmen. Letzte Anomalien werden standardmäßig nach sieben Tagen zurückgeschaut, während vergangene Anomalien 30 Tage umfassen. Historische Trends erstrecken sich über bis zu 13 Monate. |

{style="table-layout:auto"}

## Anwendungsbeispiele {#use-case-examples}

Die Funktion des KI-Assistenten zur Überwachung signifikanter Änderungen und zur Prognose von Zielgruppen kann besonders für die folgenden Anwendungsfälle hilfreich sein:

### Marketing-Vorgänge

Experten für Marketing-Vorgänge (Marketing-Vorgänge) sind dafür verantwortlich, die Integrität und Konsistenz der Zielgruppendaten sicherzustellen. Als Mitglied eines Marketing-Opportunities-Teams können Sie die Datenqualität überwachen, auf unerwartete Verschiebungen reagieren und eine stabile Grundlage für alle Marketing-Maßnahmen erhalten. Sie können die Anomalieerkennung des KI-Assistenten verwenden, um signifikante Änderungen an Zielgruppen oder Datensätzen zu erkennen und anzusprechen und so Unterbrechungen zu verhindern, die sich auf die Kampagnenleistung auswirken könnten.

### Business-Anwender und Marketing-Experten

Als Business-Anwenderin bzw. -Anwender und Marketing-Expertin können Sie sich auf präzise Zielgruppeneinblicke verlassen, um datengestützte Entscheidungen zu treffen und sicherzustellen, dass Ihre Kampagnen die gewünschten Zielgruppen effektiv erreichen. Mit den Prognosefunktionen des KI-Assistenten können Sie das Wachstum oder die Reduzierung der Zielgruppe antizipieren und strategische Anpassungen der Ressourcen und des Targeting im Laufe der Zeit ermöglichen.

## Wichtigste Funktionen

>[!IMPORTANT]
>
>Die folgenden Funktionen befinden sich im Alpha und konzentrieren sich auf grundlegende Funktionen für die Überwachung und Prognose. Da sich diese Funktion im Alpha befindet, müssen Sie sicherstellen, dass Sie die Antworten, die Sie vom KI-Assistenten erhalten, auf Korrektheit überprüfen.

### Überwachung signifikanter Änderungen bei Zielgruppe und Daten

Sie können den KI-Assistenten verwenden, um signifikante Änderungen der Zielgruppen- und Datensatzgrößen zu identifizieren, indem Sie Abweichungen von typischen Mustern verfolgen. Jede signifikante Änderung basiert auf vordefinierten Schwellenwerten, die auf die Größe der Zielgruppe zugeschnitten sind.

| Zielgruppengröße | Anzahl der Profile | Beschreibung |
| --- | --- | --- |
| Kleine Zielgruppen | 1 bis 100.000 Profile | Markiert eine Änderung von 30 % oder mehr, es sei denn, ein bestimmter Prozentsatz ist angegeben. |
| Medium-Zielgruppen | 100.000 bis 500.000 Profile | Markiert eine Änderung von 25 % oder mehr, es sei denn, ein bestimmter Prozentsatz ist angegeben. |
| Große Zielgruppen | 500.000 bis 1 Million Profile | Markiert eine Änderung von 20 % oder mehr, es sei denn, ein bestimmter Prozentsatz ist angegeben. |
| Sehr große Zielgruppen | Über 1 Million Profile | Markiert eine Änderung von 10 % oder mehr, es sei denn, ein bestimmter Prozentsatz ist angegeben. |

{style="table-layout:auto"}

>[!BEGINSHADEBOX]

#### Beispielszenario

Signifikante Änderungen weisen auf Anomalien hin, die sich auf die Zielgruppenstabilität oder die Datenzuverlässigkeit auswirken können. Wenn beispielsweise eine Zielgruppe **hochwertige Käufer** einen plötzlichen Größenrückgang von 15 % erlebt, kennzeichnet der KI-Assistent dies als eine wesentliche Änderung. Anschließend können Sie diese Informationen verwenden, um potenzielle Probleme zu untersuchen und zu beheben, bevor sie sich auf Ihre Kampagnen auswirken.

>[!ENDSHADEBOX]

>[!TIP]
>
>Der KI-Assistent benachrichtigt Sie nicht automatisch über signifikante Änderungen der Zielgruppengrößen. Sie müssen ein Gespräch mit dem KI-Assistenten beginnen und fragen, welche Zielgruppen sich innerhalb eines bestimmten Zeitraums signifikant oder um einen bestimmten Rand verändert haben.

### Prognostiziertes Zielgruppen- und Datensatzwachstum

Sie können den KI-Assistenten verwenden, um historische Datentrends und zukünftige Projektzielgruppen- und Datensatzgrößen zu referenzieren. Sie können diese Einblicke dann verwenden, um Ihre Ressourcenplanung und Strategieanpassungen zu unterstützen. Derzeit können Sie den KI-Assistenten verwenden, um das Zielgruppen- und Datensatzwachstum für 30 Tage zu prognostizieren. Indem Sie das erwartete Zielgruppenwachstum oder den erwarteten Zielgruppenrückgang verstehen, können Sie Zielgruppenbestimmungsstrategien anpassen und Ihre Ressourcen entsprechend zuweisen.

### Einblicke in historische Zielgruppengrößen

Zusätzlich zur Erkennung signifikanter Änderungen können Sie den KI-Assistenten verwenden, um historische Einblicke abzurufen und aktuelle Zielgruppen- oder Datensatzgrößen mit früheren Daten zu vergleichen. Diese Funktion unterstützt die Verfolgung langfristiger Trends und die Bewertung der Auswirkungen früherer Marketing-Aktivitäten.

Sie können Fragen an den KI-Assistenten stellen, z. B.: „Wie groß war im letzten Monat meine Zielgruppe „Treuekunden“? um historische Daten zum Wachstum oder Rückgang dieser spezifischen Zielgruppe anzuzeigen.

## Beispielfragen zur Überwachung signifikanter Änderungen

Sie können Ihre Fragen zum KI-Assistenten auf verschiedene Weise umrahmen.

* Wenn Ihre Frage einen Prozentsatz umfasst, z. B. **„Welche Zielgruppen haben sich über 30 % oder mehr geändert?“,** verwendet der KI-Assistent den Prozentsatz als Referenzpunkt.
* Wenn in der Frage kein Prozentsatz angegeben ist, interpretiert der KI-Assistent signifikante Änderungen basierend auf den Standardeinstellungen.

Die folgenden Tabellen enthalten Beispielabfragen, die veranschaulichen, wie der KI-Assistent signifikante Änderungen basierend auf der Zielgruppengröße interpretiert:

| Zielgruppeninformationen oder Zielgruppenänderung | Beispiel |
| --- | --- |
| <ul><li>Wie groß ist {AUDIENCE_NAME} derzeit?</li><li>Zeigen Sie die Zielgruppen, bei denen sich die {PERCENT} im Laufe der {DATE_DURATION} geändert hat.</li></ul> | <ul><li>Wie groß ist die Zielgruppe der High-Value-Shopper derzeit?</li><li>Zeigt die Zielgruppen an, die in der letzten Woche eine Änderung von 20 % gezeigt haben.</li></ul> |

{style="table-layout:auto"}

| Zielgruppenspezifische Abfragen | Beispiel |
| --- | --- |
| <ul><li>Welche Zielgruppen haben sich in {DATE_OR_DURATION} mehr als {PERCENT} geändert?</li><li>Zeigen Sie mir Zielgruppen mit einer signifikanten Änderung im Laufe der {DATE_OR_DURATION}.</li><li>Verteilung der Zielgruppen mit den größten Änderungen im {DATE_OR_DURATION} anzeigen.</li><li>Zielgruppen anzeigen, deren Anzahl auf {DATE_OR_DURATION} um mehr als {PERCENT} verringert wurde.</li></ul> | <ul><li>Welche Zielgruppen haben sich in der letzten Woche um mehr als 20 % verändert?</li><li>Zeigen Sie mir Zielgruppen mit einer signifikanten Änderung in den letzten sechs Monaten.</li><li>Verteilung der Zielgruppen mit den größten Änderungen vom 1. Oktober bis zum 31. Oktober anzeigen.</li><li> Zielgruppen anzeigen, die seit dem 31. August um mehr als 20 % gesunken sind. |

{style="table-layout:auto"}

## Weitere Informationen

### Erläuterung des Schwellenwerts für „signifikante Änderung“

Sie können einen bestimmten Prozentsatz angeben, wenn Sie den KI-Assistenten nach Informationen zu wichtigen Änderungen fragen. Wenn Sie keinen bestimmten Prozentsatz angeben, verweist der KI-Assistent auf einen vordefinierten Satz von Schwellenwerten, um zu bestimmen, was als signifikante Änderung gilt. Die Standardschwellenwerte basieren auf der Größe einer bestimmten Zielgruppe. In der folgenden Tabelle finden Sie Informationen darüber, was eine signifikante Änderung basierend auf der Zielgruppengröße darstellt:

| Zielgruppengröße | Was ist signifikant? |
| --- | --- |
| 1 Million oder mehr | 10 % oder mehr |
| 500.000 bis 1 Million | 20 % oder mehr |
| 100 K bis 500 K | 25 % oder mehr |
| Weniger als 100 KB | 30 % oder mehr |

### Allgemeine Zeitleisten und bestimmte Daten

Der KI-Assistent unterstützt sowohl spezifische als auch generische zeitbasierte Vergleiche für Zielgruppengrößen und interpretiert sie basierend auf dem in der Abfrage bereitgestellten Kontext.

>[!BEGINTABS]

>[!TAB Allgemeine Timelines]

Generische Zeitleisten beziehen sich auf Abfragen, die eine Sprache wie „diese Woche“ oder „letzte Woche“ verwenden. Wenn Sie dem KI-Assistenten eine Frage stellen, z. B.: „Welche Zielgruppen haben sich in der letzten Woche um mehr als 20 % geändert?“, berechnet der KI-Assistent die Größe **durchschnittliche Zielgruppe** über den angegebenen Zeitraum und vergleicht sie.

Verwenden Sie diesen Ansatz für eine breitere Ansicht der Zielgruppenänderungen im Laufe der Zeit, sodass Sie Trends innerhalb von wöchentlichen oder monatlichen Intervallen besser verstehen können.

>[!TAB Bestimmte Daten]

Wenn sich Ihre Frage auf ein bestimmtes Datum bezieht, vergleicht der KI **Assistent die (exakten Zielgruppengrößen** zu jedem Ihrer angegebenen Daten.

Verwenden Sie diesen präzisen Vergleich, um Änderungen zwischen bestimmten Zeitpunkten zu analysieren und Klarheit darüber zu erhalten, wie sich die Zielgruppengröße an bestimmten Tagen entwickeln kann.

>[!ENDTABS]

Sie können diese Flexibilität nutzen, um die Zielgruppendynamik über einen breiten und präzisen Zeitraum hinweg besser zu verstehen. Unabhängig davon, ob Sie allgemeine Trends verfolgen oder exakte Verschiebungen zwischen bestimmten Daten untersuchen, können Sie den adaptiven Mechanismus des KI-Assistenten verwenden, um den relativsten Vergleich für Ihre Abfrage abzurufen.

## Häufig gestellte Fragen {#faq}

In diesem Abschnitt finden Sie Antworten auf häufig gestellte Fragen zur Überwachung signifikanter Änderungen und zur Prognose von Zielgruppen mit dem KI-Assistenten.

### Wie viele historische Daten kann ich betrachten, um zu sehen, wie die Zielgruppengröße zunimmt oder abnimmt?

Der KI-Assistent speichert Daten zu historischen Zielgruppengrößen für 12 Monate. Sie können Fragen zu Zielgruppenänderungen innerhalb dieses Zeitraums stellen, um Wachstums- oder Rückgangsmuster im Laufe des letzten Jahres zu verstehen.

### Wie weit kann ich zurückgehen, um Zielgruppenänderungen zu sehen?

Der KI-Assistent verfolgt Zielgruppenänderungen ab dem Tag, an dem er in Ihrer Organisation aktiviert wird, und geht bis zur letzten Änderung der Zielgruppendefinition zurück. Nach der Aktivierung überwacht und zeichnet der KI-Assistent Definitionsänderungen bis zu 12 Monate lang kontinuierlich auf, sodass zukünftige Daten verfolgt und verglichen werden können.

### Wie viele historische Daten werden für eine Prognose benötigt?

Für zuverlässige Prognosen ab der letzten Änderung der Zielgruppendefinition sind Daten von mindestens 30 Tagen erforderlich. In bestimmten Fällen, z. B. bei der Prognose für [!DNL Black Friday], kann der KI-Assistent bis zu 12 Monate historischer Daten benötigen.

### Wie interpretiert der KI-Assistent „kürzlich“?

Der KI-Assistent interpretiert „kürzlich“ als die letzten sieben Tage. Bei Fragen zu den letzten Änderungen berücksichtigt der KI-Assistent Daten aus diesem Zeitraum, um Trends oder Verschiebungen zu identifizieren.

### Wie vergleicht der KI-Assistent die Zielgruppengrößen?

Wenn bestimmte Daten erwähnt werden, vergleicht der KI-Assistent die Zielgruppengrößen an diesen bestimmten Tagen. Bei allgemeineren Fragen, wie z. B. „Letzte drei Monate“ oder „Letzte Woche“, vergleicht der KI-Assistent die durchschnittliche Größe dieses Zeitraums mit dem Durchschnitt des letzten Tages.

### Wie aktuell sind die Zielgruppendaten des KI-Assistenten?

Es kann 24 bis 48 Stunden dauern, bis der KI-Assistent Daten aus Real-time Customer Data Platform aktualisiert. Daher interpretiert der KI-Assistent bei Fragen, die auf „gestern“ verweisen, dies als einen Tag vor den neuesten verfügbaren Daten.

## Nicht im Umfang enthaltene Funktionen

Die folgenden Funktionen werden derzeit nicht unterstützt:

### Erweiterte Ursachenanalyse

Der KI-Assistent kann zwar signifikante Änderungen identifizieren, aber derzeit keine detaillierte Ursachenanalyse für diese Verschiebungen bereitstellen. Künftige Iterationen des KI-Assistenten dienen dazu, anzugeben, welche Datensätze oder Attribute zu signifikanten Änderungen in Ihren Zielgruppen beitragen.

### Umfassende historische Datensatzgrößen

Das vollständige historische Tracking der Datengrößen wird derzeit nicht unterstützt. Derzeit stellt der KI-Assistent Zielgruppen- und Datensatzverlauf für bis zu 13 Monate bereit.
