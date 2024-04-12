---
title: KI-Assistent für Adobe Experience Platform
description: Erfahren Sie, wie Sie mit dem AI-Assistenten zu Experience Platform- und Real-time Customer Data Platform-Konzepten navigieren und deren Konzepte sowie Nutzungsinformationen zu Ihren Objekten verstehen können.
badge: Alpha
hide: true
hidefromtoc: true
exl-id: 8be1c222-3ccd-4a41-978e-33ac9b730f8c
source-git-commit: f38f528c421c7cbf7116cc0ee323e8e7dcde6292
workflow-type: tm+mt
source-wordcount: '2730'
ht-degree: 1%

---

# KI-Assistent für Adobe Experience Platform

>[!NOTE]
>
> Der KI-Assistent für Adobe Experience Platform befindet sich derzeit in Alpha. Die Funktion und die Dokumentation können sich ändern.

Der AI-Assistent ist eine UI-Funktion, mit der Sie in Adobe Experience Platform und Real-time Customer Data Platform navigieren und deren Konzepte und Nutzungsinformationen zu Ihren Objekten verstehen können.

Sie können den AI-Assistenten nach Informationen wie den folgenden abfragen:

* Anleitung zur Durchführung von Aufgaben in Bezug auf Daten und Zielgruppen.
* Status und Metriken der vorhandenen Datenobjekte in Ihrer Organisation.
* Verwenden Sie Fallbeispiele und Nuancen, um Ihre Datenobjekte, einschließlich Attributen, Zielgruppen, Datenflüssen, Datensätzen, Zielen, Schemas und Quellen, besser zu verstehen.

In der folgenden Anleitung erfahren Sie, wie Sie mit dem KI-Assistenten in Experience Platform- und Real-Time CDP-Workflows navigieren und diese verstehen können.

>[!BEGINSHADEBOX]

**Wie wirkt die KI-Assistenzkraft?**

Der KI-Assistent antwortet auf Ihre gestellten Fragen, indem er eine Datenbank abfragt und dann Daten aus der Datenbank in eine für Menschen lesbare Antwort übersetzt.

Diese interne Darstellung der zugrunde liegenden Daten wird auch als Wissensdiagramm bezeichnet - ein umfassendes Netz von Konzepten, Daten und Metadaten für eine gegebene Antwort.

Das Wissensdiagramm besteht aus Unterdiagrammen, die bei jeder Übermittlung von Abfragen referenziert werden:

* Kundenverwendungsdaten.
* Kundenverwendungsdaten aus verschiedenen Meta Stores.
* Experience League.

Vor der Abfrage des AI-Assistenten müssen zwei Frageklassen beachtet werden:

* **Konzeptfragen**: Bei Konzeptfragen geht es um Adobe-Konzepte, die sich auf Daten oder Zielgruppen beziehen. Zu den Beispielen für Konzeptfragen gehören:
   * Was ist der Unterschied zwischen Batch- und Streaming-Segmentierung?
   * Gibt es Datenmodelle der Branche und wie verwende ich sie?
   * Wofür wird Real-Time CDP am besten verwendet?
* **Nutzungsfragen**: Nutzungsfragen beziehen sich auf die Datenobjekte in Ihrem Unternehmen. Beispiele für Nutzungsfragen sind:
   * Wie viele Datensätze habe ich?
   * Wie viele Schemaattribute wurden noch nie verwendet?
   * Welche Zielgruppen wurden aktiviert?

>[!ENDSHADEBOX]

## Ziele, die Sie mit dem KI-Assistenten erreichen können

Sie können den KI-Assistenten für folgende Ziele verwenden:

| Ziel | Beschreibung | Beispiel |
| --- | --- | --- |
| Lernkonzepte und kontinuierliche Workflows | <ul><li>Als neuer Benutzer können Sie mit dem AI-Assistenten Real-Time CDP- und Adobe Journey Optimizer-Konzepte erlernen und sich mit Produkten und Funktionen vertraut machen, mit denen Sie nicht vertraut sind.</li><li>Als erfahrener Benutzer können Sie den AI-Assistenten verwenden, um einen Randfall zu lösen, der Ihren Workflow blockieren könnte. | <ul><li>Wie richte ich ein Dashboard in Journey Analytics ein?</li><li>Erfahren Sie mehr über einige Anwendungsfälle für Real-Time CDP.</li></ul> |
| Fehlerbehebung | Verwenden Sie den KI-Assistenten, um zu erfahren, wie Sie grundlegende Fehler beheben können, die in Ihrem Workflow auftreten können. | <ul><li>Was bewirkt dieser Fehler? {ERROR_MESSAGE} gemein?</li><li>Warum kann ich die Zielgruppe mit dem Namen &quot;Luma: E-Mail-Zielgruppe&quot;nicht löschen?</li></ul> |
| Sandbox-Hygiene | Verwenden Sie den KI-Assistenten, um Duplikate oder nicht verwendete Objekte zu identifizieren, damit Sie Ihre Sandbox effizient verwalten können. | <ul><li>Können Sie mir ähnliche Zielgruppen zeigen?</li><li>Gibt es Schemas, denen kein Datensatz zugeordnet ist?</li></ul> |
| Werteanalyse | Verwenden Sie den KI-Assistenten, um die am häufigsten verwendeten Datenobjekte zu identifizieren und Leistungsindikatoren zu bewerten oder die wertvollsten Datenobjekte zu finden. | <ul><li>Wie viele Profile enthält unsere Segmentdefinition &quot;Luma: E-Mail-Zielgruppe&quot;?</li><li>Wann wurden Zielgruppen für das Experience Cloud Audiences-Ziel aktiviert?</li></ul> |
| Suche | Verwenden Sie den AI-Assistenten, um unterstützte Experience Platform-Objekte wie Zielgruppen, Datensätze, Ziele, Schemas und Quellen zu finden. | <ul><li>Geben Sie die Zielgruppen mit &quot;Luma&quot;im Namen an, die im letzten Quartal erstellt wurden.</li><li>Welche Attribute sind im XDM-Schema &quot;Luma: Benutzerdefinierte Aktionen&quot; enthalten?</li></ul> |
| Folgenabschätzung | Verwenden Sie den KI-Assistenten, um Datenobjekte zu identifizieren, die in bestimmten Workflows verwendet wurden, damit Sie die Auswirkungen von Änderungen bewerten können. | <ul><li>Welche Zielgruppen verwenden `homeAddress.city` im Schema &quot;Luma: PersonProfiles&quot;?</li><li>Welche Datensätze sind die `consents.marketing.push.val` Profilattribut gespeichert in?</li></ul> |

## Zugriff auf den KI-Assistenten in der Experience Platform-Benutzeroberfläche

Um den KI-Assistenten zu starten, wählen Sie die **[!UICONTROL Symbol &quot;KI-Assistent&quot;]** aus der oberen Kopfzeile der Experience Platform-Benutzeroberfläche.

![Die Experience Platform-Startseite mit dem ausgewählten Symbol für den AI-Assistenten und der geöffneten Benutzeroberfläche des AI-Assistenten.](./images/ai-assistant/ai-assistant.png)

Die Benutzeroberfläche des KI-Assistenten wird angezeigt und stellt Ihnen sofort Informationen zu den ersten Schritten bereit. Sie können die unter [!UICONTROL Erste Schritte] um Fragen und Befehle zu beantworten, z. B.:

* [!UICONTROL Welche meiner Zielgruppen sind aktiviert?]
* [!UICONTROL Was ist ein Schema?]
* [!UICONTROL Erzählen Sie mir einige häufige Anwendungsfälle für Real-Time CDP]

![Abschnitt &quot;Erste Schritte&quot;der KI-Assistenzkraft.](./images/ai-assistant/ideas-to-get-started.png)

Verwenden Sie das Eingabefeld, um Ihre Abfragen oder Befehle einzugeben, um mit dem AI-Assistenten zu interagieren. Sie können auch die **`+`**), um die Funktion zur automatischen Vervollständigung und das Lesezeichensymbol zu verwenden, um auf Ihre mit Lesezeichen versehenen Abfragen und Befehle zuzugreifen.

![Das Eingabefeld des KI-Assistenten wurde hervorgehoben.](./images/ai-assistant/interact.png)

## Anwendungsbeispiel: Verwenden des AI-Assistenten, um den Erstellungsprozess für Schemas zu beschleunigen

>[!NOTE]
>
>Der folgende Workflow ist ein Beispiel für die Erstellung eines Erlebnisereignisschemas, um zu veranschaulichen, wie Sie den AI-Assistenten bei Verwendung der Experience Platform-Benutzeroberfläche verwenden können.

Betrachten Sie einen Anwendungsfall, in dem Sie eine **Gerätehandel im Ereignisschema**. Während des Erstellungsprozesses des Erlebnisereignisschemas treffen Sie auf die `eventType` -Feld. &quot;An dieser Stelle haben Sie die Möglichkeit, Ihren Workflow zu beenden, indem Sie auf den Abschnitt [Grundlagen der Schemakomposition](../xdm/schema/composition.md) oder Sie können den AI-Assistenten verwenden, um Antworten auf Ihre Fragen abzurufen und zusätzliche Ressourcen über die Dokumentationslinks zu finden, die von AI Assistant empfohlen werden.&quot;

Geben Sie zunächst Ihre Frage in das bereitgestellte Textfeld ein. Im folgenden Beispiel wird der KI-Assistent mit der Frage konfrontiert: &quot;**Was ist das Feld eventType in einem ExperienceEvent-Schema?**&quot;

![AI-Assistent für das Experience Platform mit der folgenden Frage, die zur Abfrage vorbereitet wurde: &quot;Was ist das Feld eventType in einem ExperienceEvent-Schema?](./images/ai-assistant/question.png)

AI Assistant fragt dann seine Wissensdatenbank ab und berechnet eine Antwort. Nach einigen Augenblicken gibt der KI-Assistent eine Antwort und entsprechende Vorschläge zurück, die Sie als Aufforderung zur Nachverfolgung verwenden können.

![KI-Assistent für Experience Platform mit einer Antwort auf die vorherige Abfrage.](./images/ai-assistant/answer.png)

Nach Erhalt einer Antwort des KI-Assistenten können Sie aus einer Reihe von Optionen auswählen, um zu entscheiden, wie Sie vorgehen möchten.

### Speichern Sie Ihre Abfrage {#save-your-query}

+++Auswählen , um ein Beispiel für das Speichern einer Abfrage anzuzeigen

Um Ihre Abfrage zu speichern, wählen Sie das Lesezeichen-Symbol neben Ihrer Frage aus.

![Screenshot eines ausgewählten Lesezeichens.](./images/ai-assistant/save-your-query.png)

Um auf Ihre gespeicherten Abfragen zuzugreifen, wählen Sie das Lesezeichensymbol unter dem Eingabefeld aus und wählen Sie dann die Abfrage aus, die Sie ausführen möchten.

![Screenshot des Lesezeichensymbols und eine Liste der gespeicherten Abfragen.](./images/ai-assistant/bookmarks.png)

+++

### Daten in der Sandbox anzeigen {#view-data-in-your-sandbox}

+++Auswählen zum Anzeigen des Beispiels

Je nach Abfrage stellt der KI-Assistent zusätzliche Informationen zu den Daten in Ihrer Sandbox bereit. Um anzuzeigen, wie die Antwort auf Ihre Abfrage auf Ihre Sandbox zutrifft, wählen Sie **[!UICONTROL In der Sandbox].**

Während dieses Schritts kann der AI-Assistent direkte Links zu den Benutzeroberflächen-Seiten bestimmter Objekte bereitstellen. Im folgenden Beispiel stellt der KI-Assistent direkte Links zur [!UICONTROL Schemas] und [!UICONTROL Segmente] Benutzeroberflächen-Seiten.

![Screenshot der Option &quot;In Ihrer Sandbox&quot;.](./images/ai-assistant/in-your-sandbox.png)

+++

### Überprüfen der Antwort {#verify-the-response}

+++Auswählen , um ein Beispiel für die Anzeige von Quellen anzuzeigen

Um Zitate anzuzeigen und die Antwort der KI-Assistenzkraft zu validieren, wählen Sie **[!UICONTROL Quellen anzeigen]**. Der AI-Assistent bietet Links zur Dokumentation, die seine Antwort bestätigt. Sie können auch die Abfragen verwenden, die der AI-Assistent unter [!UICONTROL Verwandte Vorschläge] , um die Themen zu Ihrer ursprünglichen Abfrage weiter zu untersuchen.

![Screenshot von &quot;Quellen anzeigen&quot;.](./images/ai-assistant/show-sources.png)

+++

### Datennutzung und -visualisierung {#data-usage-and-visualization}

+++Auswählen , um ein Beispiel für Fragen zur Datennutzung und Datenvisualisierung anzuzeigen

Damit der KI-Assistent auf eine Abfrage zur Datennutzung in Ihrem Unternehmen antworten kann, müssen Sie sich in einer aktiven Sandbox befinden.

Im folgenden Beispiel wird der AI-Assistent mit der folgenden Abfrage bereitgestellt: **&quot;Zeigen Sie mir Segmentdefinitionen mit mehr als 1000 Profilen an und fügen Sie den Aktivierungsstatus hinzu.&quot;** Der KI-Assistent antwortet dann mit einem Diagramm, das Ihre Segment- und Profildaten visualisiert.

![Folgen Sie der Frage zur Datennutzung.](./images/ai-assistant/data-usage-question.png)

Sie können den Mauszeiger über eine einzelne Leiste bewegen, um bestimmte Daten anzuzeigen. Sie können auch das Symbol zum Erweitern für eine größere Ansicht des Diagramms auswählen.

![Folgenfragen zur Illustration der Datenvisualisierung.](./images/ai-assistant/data-visualization.png)

Eine erweiterte Ansicht der Visualisierung wird angezeigt. Sie können das erweiterte Modal verwenden, um Ihre Daten weiter zu überprüfen. Dies ist besonders nützlich, wenn die Visualisierung mit einer großen Anzahl von Spalten zurückgegeben wird.

![Erweiterte Grafik.](./images/ai-assistant/chart-expanded.png)

Wenn Sie mit einer Frage zur Datennutzung aufgefordert werden, erläutert der AI-Assistent, wie die Antwort berechnet wurde. Im folgenden Beispiel beschreibt der KI-Assistent die Schritte zur Anzeige von Segmentdefinitionen mit mehr als 1000 Profilen und deren Aktivierungsstatus.

![Folgen Sie der Frage zu Segmentdefinitionen, die veranschaulichen, wie der KI-Assistent die Antwort berechnet hat.](./images/ai-assistant/results-explained.png)

Sie können auch Filter und Änderungen an Ihren Abfragen bereitstellen und AI Assistant anweisen, seine Ergebnisse anhand der von Ihnen eingeschlossenen Filter zu rendern. Sie können beispielsweise den AI-Assistenten bitten, Ihnen einen Trend der Definitionen des Zählersegments in der Reihenfolge ihres Erstellungsdatums anzuzeigen, Segmentdefinitionen mit Nullsummenprofilen zu entfernen und bei der Anzeige der Daten Monatsnamen anstelle von Ganzzahlen zu verwenden.

+++

### Automatische Vervollständigung verwenden {#use-auto-complete}

+++Auswählen , um ein Beispiel für die automatische Vervollständigung anzuzeigen

Sie können die Funktion zum automatischen Ausfüllen verwenden, um eine Liste von Datenobjekten zu erhalten, die in Ihrer Sandbox vorhanden sind. Empfehlungen zur automatischen Vervollständigung stehen für die folgenden Domänen zur Verfügung: Zielgruppen, Schemata, Datensätze, Quellen und Ziele.

Sie können AutoComplete verwenden, indem Sie das Pluszeichen (**`+`**) in Ihrer Abfrage. Alternativ können Sie auch das Pluszeichen (**`+`**) am unteren Rand des Texteingabefelds. Es wird ein Fenster mit einer Liste der empfohlenen Datenobjekte aus Ihrer Sandbox angezeigt.

![Beispiel der automatischen Vervollständigung](./images/ai-assistant/auto-complete-one.png)

Wählen Sie als Nächstes das Datenobjekt aus, das Sie abfragen möchten, um Ihre Frage abzuschließen, und senden Sie dann Ihre Frage.

![Beispiel der automatischen Vervollständigung mit Frage und Antwort](./images/ai-assistant/auto-complete-two.png)

+++

### Mehrdrehzahl verwenden {#use-multi-turn}

+++Auswählen, um ein Beispiel für eine Mehrfachumstellung anzuzeigen

Sie können die mehrgleisigen Funktionen des KI-Assistenten verwenden, um während Ihres Erlebnisses ein natürlicheres Gespräch zu führen. Die KI-Assistenzkraft ist in der Lage, die gegebenen Folgefragen zu beantworten. Dieser Kontext kann aus einer früheren Interaktion abgeleitet werden.

Im folgenden Beispiel wird der KI-Assistent nach der Gesamtzahl der Datenflüsse in der aktuellen Organisation gefragt.

![Beispiel einer Mehrfachumstellung](./images/ai-assistant/multi-turn-one.png)

Als Nächstes erhält der KI-Assistent eine weitere Folgeanfrage. Diesmal antwortet der KI-Assistent, indem er die Datenflüsse auflistet, die derzeit in Ihrem Unternehmen vorhanden sind.

![Beispiel einer Umkehrung mit Frage und Antwort](./images/ai-assistant/multi-turn-two.png)

+++

## Dokumentation {#documentation}

Derzeit umfasst der Dokumentationsindex Adobe Experience Platform (Real-Time CDP und Audiences). Der Index wird regelmäßig aktualisiert.

Das Modell zum Abrufen der Dokumentation wird auf Experience Platform (Real-Time CDP und Zielgruppen) trainiert. Fragen, die nicht in Adobe Experience Platform enthalten sind, wie z. B. Fragen zu anderen Adobe-Produkten wie Adobe Target und der Creative Cloud Suite, können nicht beantwortet werden.

## Datennutzung {#data-usage}

Sie können auch Fragen zu Ihrer Datennutzung in den folgenden Domänen stellen:

* Attribute
* Zielgruppen
* Datenflüsse
* Datensätze
* Ziele _(Fragen zu Konten und einige Fragen zum Datenfluss können derzeit nicht beantwortet werden.)_
* Schemas _(Fragen zu Feldergruppen können derzeit nicht beantwortet werden.)_
* Quellen _(Fragen zu den Rechnungsabschlüssen können derzeit nicht beantwortet werden.)_

Bei Nutzungsdatenabfragen spiegeln Antworten möglicherweise nicht den aktuellen Status der Benutzeroberfläche wider. Die Daten, die diese Fragen unterstützen, werden alle 24 Stunden aktualisiert. Beispielsweise werden Änderungen, die Benutzer tagsüber in Real-Time CDP vornehmen, mit den Datenspeichern nachts synchronisiert und stehen dann morgens für Benutzerfragen zur Verfügung. Möglicherweise müssen Sie Ihre Fragen wie folgt formatieren: &quot;Wann war die Zielgruppe mit dem Titel {TITLE} created?&quot; statt &quot;Wann war die {TITLE} Zielgruppe erstellt?&quot;

Sie müssen sich bei einer Sandbox anmelden, um sich über bestimmte Daten zu Objekten wie Zielgruppen, Schemata, Datensätzen, Attributen und Zielen zu informieren.

### Beispielhafte Fragen zur Datennutzung {#example-data-usage-questions}

+++Auswählen, um eine Liste mit Beispieldatenverwendungsfragen anzuzeigen

| Fragetyp | Beschreibung | Beispiele |
| --- | --- | --- | 
| Datenherkunft | Verwendung eines oder mehrerer Objekte über andere Experience Platform-Objekte hinweg verfolgen | <ul><li>Welche Datensätze werden verwendet? {SCHEMA_NAME} schema?</li><li>Wie viele Datensätze wurden mit demselben Schema erfasst?</li><li>Welche Datensätze wurden in aktivierten Zielgruppen verwendet?</li><li>Listen Sie die Schemas auf, deren Attribute in aktivierten Zielgruppen verwendet werden.</li><li>Anzeigen der Zielgruppen, für die aktiviert sind {DESTINATION_ACCOUNT_NAME} und haben mehr als 1000 Profile.</li><li>Zeigen Sie mir die Attribute an, die in den aktivierten Zielgruppen verwendet werden, die nach Januar 2023 geändert wurden.</li><li>Über welche Datensätze werden erfasst? {SOURCE_NAME}?</li><li>Welche Datenflüsse sind mit {DATAFLOW_NAME}</li><li>Listen Sie die Schemata auf, die für aktivierte Zielgruppen erstellt wurden und im letzten 1 Jahr erstellt wurden.</li></ul> |
| Verteilung und Aggregationen | Zusammenfassende Fragen zur Verwendung von Experience Platform-Objekten | <ul><li>Wie hoch ist der Prozentsatz der aktivierten Zielgruppen?</li><li>Wie viele Felder werden in der Segmentierung verwendet?</li><li>Welche Zielgruppen werden für die meisten Ziele aktiviert?</li><li>Listen Sie doppelte Zielgruppen auf.</li><li>Anzeigen der aktivierten Zielgruppen für {DESTINATION_ACCOUNT_NAME} und ordnen Sie sie nach Profilgröße an.</li><li>Wie hoch ist der Prozentsatz der Zielgruppen, die nicht aktiviert wurden, aber über mehr als 100 Profile verfügen. Zeigen Sie mir ihre Namen.</li><li>Geben Sie die 3 Quell-Connectoren an, die Daten in meine Datensätze aufnehmen.</li><li>Geben Sie die fünf wichtigsten Attribute an, die in aktivierten Zielgruppen basierend auf ihrem Vorkommen verwendet werden.</li></ul> |
| Objektsuche | Rufen Sie ein Experience Platform-Objekt oder dessen Eigenschaften ab oder greifen Sie darauf zu. | <ul><li>Welche Datensätze sind mit keinem Schema verknüpft?</li><li>Auflisten der Attribute, die für {AUDIENCE_NAME}?</li><li>Geben Sie mir die Liste der Schemas an, für die Profil aktiviert, aber seit ihrer Erstellung nicht geändert wurde.</li><li>Welche Zielgruppen wurden in der letzten Woche geändert?</li><li>Geben Sie die Zielgruppen an, die über dieselben Segmentdefinitionen und deren Erstellungsdatum verfügen.</li><li>Welche Datensätze sind profilaktiviert und enthalten auch die Anzahl der Zielgruppen, die aus jedem Datensatz erstellt wurden.</li><li>Welche Quellkonten sind mit dem Datensatz XYZ verknüpft?</li><li>Anzeigen der Segmentdefinition und des Änderungsdatums von {AUDIENCE_NAME}.</li></ul> |

+++

## Feedback geben {#feedback}

>[!BEGINSHADEBOX]

**Ihr Feedback wird angefordert**

Im Verlauf dieses Alphas werden Sie eingeladen, Feedback zu den Antworten zu geben, die Sie vom KI-Assistenten erhalten. Alle Antworten und eingereichten Feedback werden geprüft, um das KI-Assistenzerlebnis weiter zu verbessern.

Um Feedback zu geben, wählen Sie entweder Daumen nach oben oder Daumen nach dem Erhalt einer Antwort vom AI-Assistenten aus und geben Sie dann Ihr Feedback in das bereitgestellte Textfeld ein. Wählen Sie als Nächstes **[!UICONTROL Feedback senden]** zu senden.

>[!ENDSHADEBOX]

+++ Feedback geben

>[!BEGINTABS]

>[!TAB Wirbel nach oben]

Wählen Sie das Daumen-nach-oben-Symbol aus, um Feedback dazu zu geben, was mit Ihrem Erlebnis mit dem KI-Assistenten gut gelaufen ist.

![Das positive Feedback-Fenster.](./images/ai-assistant/thumbs-up.png)

>[!TAB Daumen nach unten]

Wählen Sie das Daumendown-Symbol aus, um Feedback dazu zu geben, was basierend auf Ihrem Erlebnis mit dem KI-Assistenten verbessert werden könnte. Während dieses Schritts können Sie auch spezifische Kommentare zu Ihrem Erlebnis angeben. Das in den Kommentaren enthaltene Feedback wird täglich überprüft.

![Das negative Feedback-Fenster.](./images/ai-assistant/thumbs-down.png)

>[!TAB Markierung]

Wählen Sie das Flag-Symbol aus, um weitere Berichte zu Ihrem Erlebnis mit dem KI-Assistenten bereitzustellen.

![Das Fenster mit den Berichtsergebnissen.](./images/ai-assistant/flag.png)

>[!ENDTABS]

+++

## Weitere Informationen {#additional-information}

Weitere Informationen zum KI-Assistenten für Experience Platform finden Sie in diesem Abschnitt .

### Einschränkungen {#caveats-and-limitations}

Im folgenden Abschnitt werden die aktuellen Einschränkungen und Einschränkungen bei der Verwendung des AI-Assistenten beschrieben.

#### Geringfügiger kleiner Vortrag

Sie können mit dem KI-Assistenten kleine Gespräche führen, aber diese Kapazität ist derzeit begrenzt.

#### Funktionsfragen

Der KI-Assistent vermittelt möglicherweise einen ungenauen Eindruck davon, was er tun kann. Es kann die folgenden Arten von Fragen falsch beantworten:

| Beispielfrage | Hinweis |
| --- | --- |
| &quot;Können Sie Fragen beantworten zu {ENTITY}?&quot; | Solange der KI-Assistent in der Lage ist, eine einzelne Seite zu finden, die auf eine bestimmte Entität verweist, antwortet er mit &quot;Ja&quot;. |
| &quot;Weißt du das? **x** Sprache?&quot; | Der KI-Assistent unterstützt derzeit nur Englisch, kann aber &quot;Ja&quot;beantworten, da das zugrunde liegende Modell es unterstützen kann. |
| &quot;Können Sie...?&quot; | Der KI-Assistent kann ja antworten, auch wenn dies nicht möglich ist. |

### Tipps {#tips}

Im folgenden Abschnitt finden Sie einige Tipps und Problemumgehungen, die bei der Verwendung des AI-Assistenten beachtet werden müssen.

#### Fragen können mit der falschen Informationsquelle beantwortet werden

Es gibt Fälle, in denen Ihre Frage zu Ihren Nutzungsdaten zu einer Antwort führen kann, die auf der Dokumentation basiert. Der Grund dafür ist, dass der KI-Assistent Ihre Frage fälschlicherweise an die falsche Informationsquelle weiterleiten kann. Sie können dies verhindern, indem Sie:

* Umkehren Ihrer Frage zur Verwendung SQL-ähnlicher Sprachen
* Explizites Aufrufen der zu verwendenden Informationsquelle.

Beispiele finden Sie in der folgenden Tabelle:

| Ungültige Frage | Gute Frage | Anmerkungen |
| --- | --- | --- |
| Was ist mein größtes Publikum? | Was ist mein größtes Publikum? Verwendung von Daten. | Teilen Sie dem KI-Assistenten explizit mit, dass die Antwort auf Daten basieren soll. |
| Was ist mein größtes Publikum? | Geben Sie meine größte Zielgruppe an. | Es gibt Fälle, in denen eine &quot;Was...&quot;-Frage mit einer dokumentationsbasierten Frage verwechselt werden kann. Die Verwendung eines Befehls wie &quot;list&quot;ist ein stärkerer Indikator dafür, dass Sie eine Frage mit Daten im Kontext stellen. |
| Wie viele Datensätze habe ich? | Zählen Sie meine Datensätze. | Die ursprüngliche Frage funktioniert für Zielgruppen, funktioniert jedoch möglicherweise nicht mit Datensätzen. |
