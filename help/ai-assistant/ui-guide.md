---
title: KI-Assistent in Adobe Experience Platform
description: Erfahren Sie, wie Sie mit dem AI-Assistenten zu Experience Platform- und Real-time Customer Data Platform-Konzepten navigieren und deren Konzepte sowie Nutzungsinformationen zu Ihren Objekten verstehen können.
exl-id: 3fed2b1d-75fc-47ce-98d1-a811eb8a1d8e
source-git-commit: 94245fe25828025b60ea57ddebede2b3ccf890eb
workflow-type: tm+mt
source-wordcount: '1517'
ht-degree: 0%

---

# Handbuch zur Benutzeroberfläche des AI-Assistenten

In diesem Handbuch erfahren Sie, wie Sie den KI-Assistenten in der Adobe Experience Platform-Benutzeroberfläche verwenden können.

Das folgende Video soll Ihr Verständnis von AI Assistant unterstützen.

>[!VIDEO](https://video.tv.adobe.com/v/3429845?learn=on)

## Zugriff auf den KI-Assistenten in der Experience Platform-Benutzeroberfläche

Um den KI-Assistenten zu starten, wählen Sie die **[!UICONTROL Symbol &quot;KI-Assistent&quot;]** aus der oberen Kopfzeile der Experience Platform-Benutzeroberfläche.

![Die Experience Platform-Startseite mit dem ausgewählten Symbol für den AI-Assistenten und der geöffneten Benutzeroberfläche des AI-Assistenten.](./images/ai-assistant-full-icon.png)

Die Benutzeroberfläche des KI-Assistenten wird angezeigt und stellt Ihnen sofort Informationen zu den ersten Schritten bereit. Sie können die unter [!UICONTROL Erste Schritte] um Fragen und Befehle zu beantworten, z. B.:

* [!UICONTROL Welche meiner Zielgruppen sind aktiviert?]
* [!UICONTROL Was ist ein Schema?]
* [!UICONTROL Erzählen Sie mir einige häufige Anwendungsfälle für Real-Time CDP]

## Handbuch zur Benutzeroberfläche des AI-Assistenten

>[!NOTE]
>
>Der folgende Workflow ist ein Beispiel für die Erstellung eines Erlebnisereignisschemas, um zu veranschaulichen, wie Sie den AI-Assistenten bei Verwendung der Experience Platform-Benutzeroberfläche verwenden können.

Betrachten Sie einen Anwendungsfall, in dem Sie eine **Gerätehandel im Ereignisschema**. Während des Erstellungsprozesses des Erlebnisereignisschemas treffen Sie auf die `eventType` -Feld. &quot;An dieser Stelle haben Sie die Möglichkeit, Ihren Workflow zu beenden, indem Sie auf den Abschnitt [Grundlagen der Schemakomposition](../xdm/schema/composition.md) oder Sie können den AI-Assistenten verwenden, um Antworten auf Ihre Fragen abzurufen und zusätzliche Ressourcen über die Dokumentationslinks zu finden, die von AI Assistant empfohlen werden.&quot;

Geben Sie zunächst Ihre Frage in das bereitgestellte Textfeld ein. Im folgenden Beispiel wird der KI-Assistent mit der Frage konfrontiert: &quot;**Was ist das Feld eventType in einem ExperienceEvent-Schema?**&quot;

![AI-Assistent für das Experience Platform mit der folgenden Frage, die zur Abfrage vorbereitet wurde: &quot;Was ist das Feld eventType in einem ExperienceEvent-Schema?](./images/question.png)

AI Assistant fragt dann seine Wissensdatenbank ab und berechnet eine Antwort. Nach einigen Augenblicken gibt der KI-Assistent eine Antwort und entsprechende Vorschläge zurück, die Sie als Aufforderung zur Nachverfolgung verwenden können.

![KI-Assistent für Experience Platform mit einer Antwort auf die vorherige Abfrage.](./images/answer.png)

Nach Erhalt einer Antwort des KI-Assistenten können Sie aus einer Reihe von Optionen auswählen, um zu entscheiden, wie Sie vorgehen möchten.

### Funktionen des KI-Assistenten {#features}

In diesem Abschnitt werden die verschiedenen Funktionen des KI-Assistenten beschrieben, die Sie während Ihrer Workflows auf dem Experience Platform verwenden können.

### Anzeigen betrieblicher Datenobjekte {#view-operational-data-objects}

Je nach Abfrage stellt der KI-Assistent zusätzliche Informationen zu den Daten in Ihrer Sandbox bereit. Um anzuzeigen, wie die Antwort auf Ihre Abfrage auf Ihre jeweilige Sandbox zutrifft, wählen Sie **[!UICONTROL In der Sandbox].**

Beim Anzeigen von Daten zu Ihrer Sandbox kann der KI-Assistent direkte Links zu bestimmten Benutzeroberflächen-Seiten bereitstellen, auf denen Ihre abgefragten Daten angezeigt werden.

+++Auswählen zum Anzeigen des Beispiels

In diesem Beispiel gibt der KI-Assistent zusätzliche Informationen zu den vorhandenen XDM-Schemas in Ihrer Sandbox zurück, einschließlich der Gesamtzahl der Schemas und der fünf am häufigsten verwendeten Felder.

![Das Dropdown-Fenster &quot;in Ihrer Sandbox&quot;mit zusätzlichen Informationen zu Ihren Schemas wird geöffnet.](./images/in-your-sandbox.png)

+++

### Zitate anzeigen {#view-citations}

Sie können die von AI Assistant an Sie zurückgegebenen Antworten überprüfen, indem Sie die verfügbaren Zitate mit jeder Antwort auf das Produktwissen überprüfen.

+++Auswählen , um ein Beispiel für die Anzeige von Quellen anzuzeigen

Um Zitate anzuzeigen und die Antwort der KI-Assistenzkraft zu validieren, wählen Sie **[!UICONTROL Quellen anzeigen]**.

![Die Antwort des AI-Assistenten mit ausgewählter Option &quot;Quellen anzeigen&quot;.](./images/show-sources.png)

Der AI-Assistent aktualisiert die Benutzeroberfläche und bietet Ihnen Links zur Dokumentation, die die ursprüngliche Antwort bestätigen. Wenn Zitate aktiviert sind, aktualisiert der KI-Assistent die Antwort dahingehend, dass er Fußnoten enthält, die die spezifischen Teile der Antwort angeben, die auf die bereitgestellte Dokumentation verweisen.

![Ein Dropdown-Menü mit den von AI Assistant für Konzeptfragen bereitgestellten Zitaten.](./images/citations.png)

Sie können auch die Vorschläge verwenden, die der KI-Assistent unter **[!UICONTROL Verwandte Vorschläge]** weiter zu erkunden Themen, die sich auf Ihre ursprüngliche Frage beziehen.

![Eine Liste von Vorschlägen, die von der KI-Assistenzkraft bereitgestellt werden.](./images/related-suggestions.png)

+++

### Betriebliche Erkenntnisse {#operational-insights}

Sie müssen sich in einer aktiven Sandbox befinden, damit der KI-Assistent ausreichend auf eine Frage zu Ihren operativen Einblicken antworten kann.

+++Auswählen , um ein Beispiel für eine operative Insights-Frage anzuzeigen

Im folgenden Beispiel wird der KI-Assistent mit der folgenden Abfrage gefragt: **&quot;Anzeigen von Datenflüssen, die mit der Amazon S3-Quelle erstellt wurden&quot;**.

![Eine Frage zu operativen Einblicken.](./images/op-insights-question.png)

Der AI-Assistent antwortet dann mit einer Tabelle, in der Ihre Datenflüsse und die zugehörigen IDs aufgelistet sind. Um die gesamte Datentabelle anzuzeigen, wählen Sie oben rechts das Symbol zum Erweitern aus.

![Eine Antwort auf operative Erkenntnisse](./images/op-insights-answer.png)

Eine erweiterte Ansicht der Tabelle mit einer umfassenderen Liste von Datenflüssen, die auf den Parametern Ihrer Abfrage basieren, wird angezeigt.

![Eine Ansicht der erweiterten Tabelle.](./images/table.png)

Wenn eine Frage zu operativen Einblicken gestellt wird, erläutert der KI-Assistent, wie die Antwort berechnet wurde. Im folgenden Beispiel beschreibt der AI-Assistent die Schritte, die zur Identifizierung der Datenflüsse unternommen wurden, die mithilfe des [!DNL Amazon S3] -Quelle.

![KI-Assistent, der eine Erläuterung der Art und Weise der Berechnung der Antwort liefert](./images/answer-explained.png)

Sie können auch Filter bereitstellen und Änderungen an Ihren Fragen vornehmen und AI Assistant anweisen, seine Ergebnisse anhand der von Ihnen eingeschlossenen Filter zu rendern. Beispielsweise können Sie den AI-Assistenten bitten, Ihnen einen Trend zur Anzahl der Segmentdefinitionen in der Reihenfolge ihres Erstellungsdatums anzuzeigen, Segmentdefinitionen mit null Gesamtprofilen zu entfernen und bei der Anzeige der Daten Monatsnamen anstelle von Ganzzahlen zu verwenden.

**Hinweis:** Antworten auf operative Einblicke befinden sich derzeit in der Beta-Phase. Wählen Sie das QuickInfo-Symbol in der Benutzeroberfläche des AI-Assistenten aus, um den Beta-Hinweis und einen Link zur Dokumentation anzuzeigen.

![Symbol für QuickInfo des AI-Assistenten ausgewählt.](./images/op-insights-beta-note.png)

+++

### Überprüfen der betrieblichen Insights-Antworten {#verify-responses}

Sie können jede Antwort im Zusammenhang mit betrieblichen Insights-Fragen mithilfe einer SQL-Abfrage überprüfen, die von AI Assistant bereitgestellt wird.

+++Auswählen zum Anzeigen eines Beispiels für die Überprüfung operativer Insights-Antworten

Nachdem Sie eine Antwort auf eine operative Insights-Frage erhalten haben, wählen Sie **[!UICONTROL Quellen anzeigen]** und wählen Sie **[!UICONTROL Quellabfrage anzeigen]**.

![Quellabfrage anzeigen](./images/view-source-query.png)

Bei Fragen zu operativen Einblicken stellt der AI-Assistent eine SQL-Abfrage bereit, mit der Sie den Prozess zur Berechnung der Antwort überprüfen können. Diese Quellabfrage dient nur zu Überprüfungszwecken und wird von Query Service nicht unterstützt.

![Beispiel einer Quellabfrage](./images/source-query.png)

+++

### Automatische Vervollständigung verwenden {#use-auto-complete}

Sie können die Funktion zum automatischen Ausfüllen verwenden, um eine Liste von Datenobjekten zu erhalten, die in Ihrer Sandbox vorhanden sind. Empfehlungen zur automatischen Vervollständigung stehen für die folgenden Domänen zur Verfügung: Zielgruppen, Schemata, Datensätze, Quellen und Ziele.

+++Auswählen , um ein Beispiel für die automatische Vervollständigung anzuzeigen

Sie können AutoComplete verwenden, indem Sie das Pluszeichen (**`+`**) in Ihrer Abfrage. Alternativ können Sie auch das Pluszeichen (**`+`**) am unteren Rand des Texteingabefelds. Es wird ein Fenster mit einer Liste der empfohlenen Datenobjekte aus Ihrer Sandbox angezeigt.

![Beispiel der automatischen Vervollständigung](./images/autocomplete.png)

+++

### Mehrdrehzahl verwenden {#use-multi-turn}

Sie können die mehrgleisigen Funktionen des KI-Assistenten verwenden, um während Ihres Erlebnisses ein natürlicheres Gespräch zu führen. Die KI-Assistenzkraft ist in der Lage, die gegebenen Folgefragen zu beantworten. Dieser Kontext kann aus einer früheren Interaktion abgeleitet werden.

+++Auswählen, um ein Beispiel für eine Mehrfachumstellung anzuzeigen

Im folgenden Beispiel wird der KI-Assistent zunächst nach der Gesamtzahl der Datenflüsse gefragt und dann aufgefordert, die 10 neuesten Datenflüsse aufzulisten.

![Beispiel einer Mehrfachumstellung](./images/multiturn.png)

+++

### Neue Unterhaltung beginnen

Sie können Themen mit dem KI-Assistenten ändern, indem Sie eine neue Unterhaltung zurücksetzen und starten.

+++Auswählen , um ein Beispiel für das Zurücksetzen der Konversation anzuzeigen

Um das Zurücksetzen vorzunehmen, wählen Sie die Auslassungszeichen (**`...`**) auf der Benutzeroberfläche des AI-Assistenten und wählen Sie **[!UICONTROL Neue Unterhaltung beginnen]**. Dies informiert den AI-Assistenten darüber, dass Sie beabsichtigen, Themen zu ändern. Dies kann besonders bei der Fehlerbehebung von Abfragen hilfreich sein, die entweder fehlschlagen oder auf falsche Informationen verweisen.

![Die ausgewählten Ellipsen und die ausgewählte Option Neue Konversation starten .](./images/reset.png)

+++

### Erkennung verwenden {#use-discoverability}

Sie können die Funktion zur Auffindbarkeit von AI-Assistenten verwenden, um eine Liste der allgemeinen Themen anzuzeigen, die von AI Assistant unterstützt werden und in Entitäten gruppiert sind.

+++Auswählen, um ein Beispiel für Entdeckbarkeit anzuzeigen

Um die Entdeckung anzuzeigen, wählen Sie das Glühbirnensymbol in der oberen Kopfzeile der Benutzeroberfläche des AI-Assistenten aus.

![Die Funktion &quot;AI Assistant Discover&quot;.](./images/lightbulb.png)

Wählen Sie als Nächstes eine Kategorie aus und wählen Sie dann eine Eingabeaufforderung aus der bereitgestellten Liste aus. Sie können diese Funktion verwenden, um eine bessere Vorstellung davon zu erhalten, welche Arten von Fragen der KI-Assistent beantworten kann. Sie können die bereits vorhandenen Eingabeaufforderungen auch mit spezifischen Details aktualisieren, die sich auf Ihre Sandbox beziehen, indem Sie freien Text verwenden oder [autocomplete](#use-auto-complete).

![Der KI-Assistent fordert Sie zur Erkennung von Personen auf.](./images/prompt.png)

+++

## Feedback geben {#feedback}

Sie können mithilfe der Antwortmöglichkeiten Feedback zu Ihrer Erfahrung mit dem KI-Assistenten geben.

Um Feedback zu geben, wählen Sie entweder Daumen nach oben, Daumen nach unten oder eine Markierung aus, nachdem Sie eine Antwort vom AI-Assistenten erhalten haben, und geben Sie dann Ihr Feedback in das bereitgestellte Textfeld ein.

![Die Feedback-Option im AI-Assistenten.](./images/provide-feedback.png)

+++Auswählen , um weitere Beispiele anzuzeigen

>[!BEGINTABS]

>[!TAB Wirbel nach oben]

Wählen Sie das Daumen-nach-oben-Symbol aus, um Feedback dazu zu geben, was mit Ihrem Erlebnis mit dem KI-Assistenten gut gelaufen ist.

![Das positive Feedback-Fenster.](./images/thumbs-up.png)

>[!TAB Daumen nach unten]

Wählen Sie das Daumendown-Symbol aus, um Feedback dazu zu geben, was basierend auf Ihrem Erlebnis mit dem KI-Assistenten verbessert werden könnte. Während dieses Schritts können Sie auch spezifische Kommentare zu Ihrem Erlebnis angeben. Das in den Kommentaren enthaltene Feedback wird täglich überprüft.

![Das negative Feedback-Fenster.](./images/thumbs-down.png)

>[!TAB Markierung]

Wählen Sie das Flag-Symbol aus, um weitere Berichte zu Ihrem Erlebnis mit dem KI-Assistenten bereitzustellen.

![Das Fenster mit den Berichtsergebnissen.](./images/flag.png)

>[!ENDTABS]

+++
