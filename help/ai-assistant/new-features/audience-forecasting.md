---
title: Überwachen bedeutender Änderungen und Prognosen für Zielgruppen mit dem AI-Assistenten
description: Erfahren Sie, wie Sie mit AI Assistant signifikante Änderungen überwachen und Zielgruppen in Adobe Experience Platform vorhersagen können.
badge: Alpha
source-git-commit: 37d2886cc5d7b3a019d23f76973d79547865298b
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 0%

---

# Überwachen bedeutender Änderungen und Vorhersagen des Zielgruppenwachstums mit dem AI-Assistenten

>[!AVAILABILITY]
>
>Diese Funktion ist in Alpha verfügbar und steht Ihrem Unternehmen möglicherweise nicht zur Verfügung. Wenden Sie sich an Ihr Adobe-Account-Team, um am Alpha-Programm teilzunehmen und auf diese Funktion zuzugreifen.

In der heutigen datengesteuerten Marketing-Landschaft sind zeitnahe und genaue Einblicke unerlässlich. Egal ob Sie ein Business-Anwender oder Marketing-Benutzer sind, Sie benötigen die Möglichkeit, konsistent mit Ihren Zielgruppen zu interagieren und auf der Grundlage klarer Einblicke schnelle und wirkungsvolle Anpassungen vorzunehmen. Um die Ausrichtung Ihrer Geschäftsziele zu gewährleisten oder Ihre Geschäftsziele zu erreichen, benötigen Sie die umsetzbaren Informationen, die Sie benötigen, um effektive Kampagnen zu fördern und Ressourcen zu optimieren.

Sie können den AI-Assistenten für Adobe Experience Platform verwenden, um wichtige Änderungen zu überwachen und Wachstumsprognosen für Ihre Zielgruppe und Datensatzgrößen bereitzustellen. Anschließend können Sie diese Informationen verwenden, um die Integrität Ihrer Zielgruppendaten sicherzustellen und zukunftsorientierte Projektionen zur Unterstützung datenbasierter Entscheidungen anzubieten.

In diesem Dokument erfahren Sie, wie Sie mit dem AI-Assistenten signifikante Änderungen überwachen und das Zielgruppenwachstum und die Fluktuationen vorhersagen können.

## Wichtige Begriffe und Definitionen {#key-terminology-and-definitions}

In der folgenden Tabelle finden Sie eine Liste wichtiger Begriffe und der zugehörigen Definitionen.

| Terminologie | Definition |
| --- | --- |
| Wesentliche Änderung | Eine wesentliche Änderung ist eine große prozentuale Änderung der Zielgruppe oder Datensatzgröße, die durch bestimmte Schwellenwerte definiert wird (z. B. 10 % für große Zielgruppen). Erhebliche Änderungen helfen bei der Identifizierung von Anomalien, die sich auf die Datenstabilität auswirken. |
| Anomalien | Anomalien sind unerwartete Datenabweichungen, wie ein plötzliches Wachstum von 20 % in einer **hochwertigen Käufer** -Zielgruppe. Eine Anomalie kann durch ein Problem mit der potenziellen Datenerfassung oder eine Änderung der Zielgruppendefinition verursacht werden. |
| Historische Daten | Historische Daten beziehen sich auf langfristige Daten, in der Regel ein bis drei Jahre. Sie können historische Daten verwenden, um Muster zu verfolgen. **Hinweis**: Während des Alphas stellt der KI-Assistent historische Daten von bis zu 13 Monaten bereit. |
| Neu/Letzte Daten | Neu oder neu auftretende Daten beziehen sich auf Datenpunkte, die über einen kurzen Zeitraum (in der Regel eine Woche oder bis zu 30 Tage) beobachtet wurden. Sie können neue oder aktuelle Daten verwenden, um unmittelbare Trends hervorzuheben und schnelle Anpassungen vorzunehmen. |
| Prognose | Eine Prognose ist eine Vorhersage künftiger Zielgruppen- oder Datensatzgrößen, die auf vergangenen Trends basieren. Sie können Prognosedaten verwenden, um eine langfristige Planung zu unterstützen. |
| Zielgruppengröße | Die Zielgruppengröße bezieht sich auf die Gesamtzahl der Profile in einer Zielgruppe. Die Zielgruppengröße wird bei jeder Iteration der Datenerfassung aktualisiert. |
| Zeitrahmen für Vergleich | Der AI-Assistent verwendet vordefinierte Zeitrahmen für den Vergleich. Jüngste Anomalien haben standardmäßig einen 7-tägigen Rückblick, während vergangene Anomalien 30 Tage umfassen. Historische Trends reichen bis zu 13 Monate. |

{style="table-layout:auto"}

## Anwendungsbeispiele {#use-case-examples}

Die Fähigkeit des KI-Assistenten, wesentliche Änderungen zu überwachen und Zielgruppen vorherzusagen, kann in den folgenden Anwendungsfällen besonders hilfreich sein:

### Marketing-Vorgänge

Für die Integrität und Konsistenz von Zielgruppendaten sind die Fachkräfte für Marketing-Vorgänge (Marketing-ops) verantwortlich. Als Mitglied eines Marketing-Teams können Sie unter anderem die Überwachung der Datenqualität, die Reaktion auf unerwartete Veränderungen und die Aufrechterhaltung einer stabilen Grundlage für alle Marketing-Maßnahmen übernehmen. Sie können die Anomalieerkennung des AI-Assistenten verwenden, um signifikante Zielgruppen- oder Datensatzänderungen zu erkennen und zu beheben und so Unterbrechungen zu verhindern, die sich auf die Kampagnenleistung auswirken könnten.

### Geschäftsbenutzer und Marketing-Experten

Als Business-Anwender und Marketing-Experte können Sie sich auf genaue Zielgruppeneinblicke verlassen, um datengesteuerte Entscheidungen zu treffen und sicherzustellen, dass Ihre Kampagnen ihre gewünschten Zielgruppen effektiv erreichen. Mit den Prognosefunktionen des AI-Assistenten können Sie das Wachstum oder die Reduzierung von Zielgruppen vorhersagen und strategische Anpassungen der Ressourcen und Zielgruppen im Laufe der Zeit ermöglichen.

## Wichtigste Funktionen

>[!IMPORTANT]
>
>Die folgenden Funktionen sind in Alpha verfügbar und konzentrieren sich auf grundlegende Funktionen zur Überwachung und Vorhersage. Da sich diese Funktion im Alpha befindet, müssen Sie sicherstellen, dass Sie die Antworten, die Sie von AI Assistant erhalten, auf ihre Richtigkeit doppelprüfen.

### Überwachen bedeutender Änderungen an Zielgruppe und Daten

Sie können den AI-Assistenten verwenden, um signifikante Änderungen an Zielgruppen und Datensatzgrößen zu identifizieren, indem Sie Abweichungen von typischen Mustern verfolgen. Jede signifikante Änderung basiert auf vordefinierten Schwellenwerten, die auf die Größe der Zielgruppe zugeschnitten sind.

| Zielgruppengröße | Anzahl Profile | Beschreibung |
| --- | --- | --- |
| Kleine Zielgruppen | 1 bis 100.000 Profile | Kennzeichnet eine Änderung von 30 % oder mehr, es sei denn, es wird ein bestimmter Prozentsatz angegeben. |
| Medium-Zielgruppen | 100.000 bis 500.000 Profile | Kennzeichnet eine Veränderung von 25 % oder mehr, es sei denn, es wird ein bestimmter Prozentsatz angegeben. |
| Große Zielgruppen | 500.000 bis 1 Million Profile | Kennzeichnet eine Veränderung von 20 % oder mehr, es sei denn, ein bestimmter Prozentsatz ist angegeben. |
| Sehr große Zielgruppen | Über 1 Million Profile | Kennzeichnet eine Änderung von 10 % oder mehr, es sei denn, es wird ein bestimmter Prozentsatz angegeben. |

{style="table-layout:auto"}

>[!BEGINSHADEBOX]

#### Beispielszenario

Erhebliche Änderungen weisen auf Anomalien hin, die sich auf die Stabilität oder Zuverlässigkeit der Zielgruppe auswirken können. Wenn beispielsweise eine Audience mit dem Namen **High-Value Shoppers** eine plötzliche Reduzierung der Größe um 15 % erfährt, markiert der AI-Assistent diese als wesentliche Änderung. Mithilfe dieser Informationen können Sie dann mögliche Probleme untersuchen und beheben, bevor sie sich auf Ihre Kampagnen auswirken.

>[!ENDSHADEBOX]

>[!TIP]
>
>Der KI-Assistent benachrichtigt Sie nicht automatisch über bedeutende Änderungen der Zielgruppengröße. Sie müssen innerhalb eines bestimmten Zeitraums eine Konversation mit AI Assistant starten und fragen, welche Zielgruppen sich signifikant oder innerhalb eines bestimmten Zeitraums geändert haben.

### Prognostizieren der Zielgruppe und des Datensatzwachstums

Mit dem AI-Assistenten können Sie auf historische Datentrends und zukünftige Zielgruppen- und Datensatzgrößen des Projekts verweisen. Anschließend können Sie diese Einblicke verwenden, um Ihre Ressourcenplanung und Strategieanpassungen zu unterstützen. Derzeit können Sie den AI-Assistenten verwenden, um das Zielgruppen- und Datensatzwachstum für 30 Tage vorherzusagen. Durch Verständnis des erwarteten Wachstums oder Rückgangs der Zielgruppe können Sie Zielgruppenstrategien anpassen und Ihre Ressourcen entsprechend zuweisen.

### Einblicke in historische Zielgruppengrößen

Zusätzlich zur Erkennung bedeutender Änderungen können Sie den AI-Assistenten verwenden, um historische Einblicke abzurufen und aktuelle Zielgruppen- oder Datensatzgrößen mit früheren Daten zu vergleichen. Diese Funktion unterstützt das Tracking langfristiger Trends und die Bewertung der Auswirkungen vorheriger Marketingaktivitäten.

Sie können Fragen an den KI-Assistenten stellen, z. B. &quot;Wie groß war meine Zielgruppe &quot;Loyalitätskunden&quot;im letzten Monat? um historische Daten zum Wachstum oder Rückgang dieser spezifischen Zielgruppe anzuzeigen.

## Beispielfragen zur Überwachung wesentlicher Änderungen

Sie können Fragen zu Ihrer KI-Assistenzkraft auf verschiedene Arten stellen.

* Wenn Ihre Frage einen Prozentsatz enthält, z. B. **&quot;Welche Zielgruppen haben sich über 30 % oder mehr verändert?&quot;**, verwendet der AI-Assistent den Prozentsatz als Referenzpunkt.
* Wenn in Ihrer Frage kein Prozentsatz angegeben ist, interpretiert der AI-Assistent wichtige Änderungen basierend auf den Standardeinstellungen.

In den folgenden Tabellen finden Sie beispielsweise Abfragen, die veranschaulichen, wie der AI-Assistent wichtige Änderungen basierend auf der Zielgruppengröße interpretiert:

| Zielgruppeninformationen oder Zielgruppenänderung | Beispiel |
| --- | --- |
| <ul><li>Wie groß ist derzeit {AUDIENCE_NAME}?</li><li>Zeigen Sie die Zielgruppen an, für die eine Änderung von {PERCENT} gegenüber {DATE_DURATION} angezeigt wurde.</li></ul> | <ul><li>Wie groß ist die aktuelle Zielgruppe der hochwertigen Käufer?</li><li>Zeigen Sie die Zielgruppen an, für die in der letzten Woche eine Veränderung von 20 % festgestellt wurde.</li></ul> |

{style="table-layout:auto"}

| Zielgruppenspezifische Abfragen | Beispiel |
| --- | --- |
| <ul><li>Welche Zielgruppen haben sich in {DATE_OR_DURATION} mehr als {PERCENT} geändert?</li><li>Zeigen Sie mir Zielgruppen mit einer signifikanten Änderung im Vergleich zu {DATE_OR_DURATION}.</li><li>Zeigen Sie mir die Verteilung der Zielgruppen mit den größten Änderungen über {DATE_OR_DURATION}.</li><li>Zeigen Sie mir Zielgruppen, die bei {DATE_OR_DURATION} mehr als {PERCENT} reduziert wurden.</li></ul> | <ul><li>Welche Zielgruppen haben sich in der letzten Woche um mehr als 20 % verändert?</li><li>Zeigen Sie mir Zielgruppen mit einer signifikanten Veränderung in den letzten sechs Monaten.</li><li>Zeigen Sie mir die Verteilung der Zielgruppen mit den größten Änderungen vom 1. Oktober bis 31. Oktober.</li><li> Zeigen Sie mir Zielgruppen, die seit dem 31. August um mehr als 20 % gesunken sind. |

{style="table-layout:auto"}

## Weitere Informationen

### Grundlegendes zur Schwellenwertänderung

Sie können einen bestimmten Prozentsatz angeben, wenn Sie AI Assistant nach Informationen zu wesentlichen Änderungen fragen. Wenn Sie keinen bestimmten Prozentsatz angeben, verweist der KI-Assistent auf einen vordefinierten Satz von Schwellenwerten, um zu bestimmen, welche Kriterien als wesentliche Änderung gelten. Die Standardschwellen basieren auf der Größe einer bestimmten Zielgruppe. In der folgenden Tabelle finden Sie Informationen dazu, was eine wesentliche Änderung basierend auf der Zielgruppengröße darstellt:

| Zielgruppengröße | Was ist von Bedeutung? |
| --- | --- |
| 1 Million oder mehr | 10 % oder mehr |
| 500 bis 1 Million | 20 % oder mehr |
| 100 bis 500 k | 25 % oder mehr |
| Weniger als 100 k | 30 % oder mehr |

### Allgemeine Zeitleisten und spezifische Daten

Der AI-Assistent unterstützt sowohl spezifische als auch generische zeitbasierte Vergleiche für Zielgruppengrößen und interpretiert sie basierend auf dem in der Abfrage angegebenen Kontext.

>[!BEGINTABS]

>[!TAB Allgemeine Zeitleisten]

Generische Zeitleisten beziehen sich auf Abfragen, die eine Sprache wie &quot;diese Woche&quot;oder &quot;letzte Woche&quot;verwenden. Wenn Sie den KI-Assistenten z. B. fragen: &quot;Welche Zielgruppen haben sich in der letzten Woche um mehr als 20 % verändert?&quot;, berechnet und vergleicht der KI-Assistent die Größe der **durchschnittlichen Zielgruppe** über den angegebenen Zeitraum.

Verwenden Sie diesen Ansatz für eine umfassendere Ansicht der Zielgruppenänderungen im Zeitverlauf, sodass Sie Trends in Wochen- oder Monatsintervallen besser verstehen können.

>[!TAB Bestimmte Datumswerte]

Wenn Ihre Frage auf ein bestimmtes Datum verweist, vergleicht der KI-Assistent die **genauen Zielgruppengrößen** an jedem von Ihnen angegebenen Datum.

Verwenden Sie diesen präzisen Vergleich, um Änderungen zwischen bestimmten Zeitpunkten zu analysieren und Klarheit darüber zu erhalten, wie sich die Zielgruppengröße an bestimmten Tagen entwickeln kann.

>[!ENDTABS]

Sie können diese Flexibilität nutzen, um die Dynamik von Zielgruppen sowohl über einen breiten als auch über einen präzisen Zeitraum hinweg besser zu verstehen. Unabhängig davon, ob Sie allgemeine Trends verfolgen oder exakte Verschiebungen zwischen bestimmten Daten untersuchen, können Sie den adaptiven Mechanismus des AI-Assistenten verwenden, um den relativen Vergleich für Ihre Abfrage abzurufen.

## Häufig gestellte Fragen {#faq}

In diesem Abschnitt finden Sie Antworten auf häufig gestellte Fragen zur Überwachung wesentlicher Änderungen und zur Vorhersage von Zielgruppen mit dem AI-Assistenten.

### Wie viele historische Daten kann ich betrachten, um Vergrößerungen oder Verkleinerungen von Zielgruppen anzuzeigen?

Der AI-Assistent behält Daten zur historischen Zielgruppengröße von 12 Monaten bei. Sie können innerhalb dieses Zeitrahmens Fragen zu Zielgruppenänderungen stellen, um die Wachstums- oder Abwärtsmuster des vergangenen Jahres zu verstehen.

### Wie weit in der Geschichte kann ich noch gehen, um Zielgruppenänderungen zu sehen?

Der KI-Assistent verfolgt Zielgruppenänderungen ab dem Tag, an dem sie in Ihrer Organisation aktiviert werden, und geht bis zur letzten Änderung der Zielgruppendefinition zurück. Nach der Aktivierung überwacht und zeichnet AI Assistant Definitionsänderungen bis zu 12 Monate lang kontinuierlich auf, sodass Daten künftig verfolgt und verglichen werden können.

### Wie viele historische Daten sind für eine Prognose erforderlich?

Daten aus mindestens 30 Tagen sind erforderlich, um eine zuverlässige Prognose aus der letzten Änderung der Zielgruppendefinition zu erhalten. In bestimmten Fällen, z. B. beim Planen von [!DNL Black Friday], benötigt der KI-Assistent möglicherweise bis zu 12 Monate historischer Daten.

### Wie interpretiert der KI-Assistent &quot;vor Kurzem&quot;?

Die KI-Assistenzkraft interpretiert &quot;kürzlich&quot;als die letzten sieben Tage. Bei Fragen, die auf aktuelle Änderungen verweisen, berücksichtigt der AI-Assistent Daten aus diesem Zeitraum, um Trends oder Verschiebungen zu identifizieren.

### Wie vergleicht der KI-Assistent Zielgruppengrößen?

Wenn bestimmte Daten erwähnt werden, vergleicht der AI-Assistent die Zielgruppengrößen an diesen spezifischen Tagen. Bei allgemeineren Fragen, z. B. bezüglich der &quot;letzten drei Monate&quot;oder der &quot;letzten Woche&quot;, vergleicht die Assistenzkraft die durchschnittliche Größe dieses Zeitraums mit dem Durchschnitt des letzten Tages.

### Wie aktuell sind die Zielgruppendaten des KI-Assistenten?

Es kann 24 bis 48 Stunden dauern, bis der AI-Assistent Daten aus Real-time Customer Data Platform aktualisiert. Daher interpretiert AI Assistant bei Fragen, die auf &quot;gestern&quot;verweisen, dies als einen Tag, bevor die aktuellsten Daten verfügbar sind.

## Out-of-Scope-Funktionen

Die folgenden Funktionen werden derzeit nicht unterstützt:

### Erweiterte Wurzellenanalyse

Der KI-Assistent kann zwar wichtige Änderungen identifizieren, kann aber derzeit keine detaillierte Analyse der Ursachen für diese Veränderungen bereitstellen. Zukünftige Iterationen des AI Assistant zielen darauf ab, festzulegen, welche Datensätze oder Attribute zu signifikanten Änderungen in Ihren Zielgruppen beitragen.

### Umfassende historische Datensatzgrößen

Das vollständige historische Tracking von Datengrößen wird derzeit nicht unterstützt. Der AI-Assistent bietet Zielgruppe und Datensatzverlauf derzeit für bis zu 13 Monate an.