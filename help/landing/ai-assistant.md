---
title: KI-Assistent für Adobe Experience Platform
description: Erfahren Sie, wie Sie mit dem AI-Assistenten zu Experience Platform und Real-time Customer Data Platform-Konzepten navigieren und diese verstehen können, sowie Informationen zur Verwendung Ihrer Objekte.
badge: Alpha
hide: true
hidefromtoc: true
source-git-commit: e84f5aff6885535b58874a4fe02db2944e1d9b7f
workflow-type: tm+mt
source-wordcount: '2629'
ht-degree: 1%

---

# KI-Assistent für Adobe Experience Platform

>[!NOTE]
>
>Der AI-Assistent für Adobe Experience Platform befindet sich derzeit in Alpha. Die Funktion und die Dokumentation können sich ändern.

Der KI-Assistent für Adobe Experience Platform ist eine UI-Funktion, mit der Sie in Experience Platform und Real-time Customer Data Platform navigieren und deren Konzepte sowie Nutzungsinformationen zu Ihren Objekten verstehen können.

Sie können den KI-Assistenten nach Informationen wie den folgenden abfragen:

* Anleitung zur Durchführung von Aufgaben in Bezug auf Daten und Zielgruppen.
* Status und Metriken der vorhandenen Datenobjekte in Ihrer Organisation.
* Verwenden Sie Fallbeispiele und Nuancen, um Ihre Datenobjekte, einschließlich Attributen, Datensätzen, Zielen, Schemas, Segmenten und Quellen, besser zu verstehen.

In diesem Dokument erfahren Sie, wie Sie mit dem KI-Assistenten Fragen stellen und Antworten zu Experience Platform- und Real-Time CDP-Konzepten erhalten können.

>[!BEGINSHADEBOX]

**Wie wirkt die KI-Assistenzkraft?**

Der KI-Assistent beantwortet Ihre eingereichten Fragen, indem er eine Datenbank abfragt und dann Daten aus der Datenbank in eine für Menschen lesbare Antwort übersetzt.

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
   * Welche Segmente wurden aktiviert?

>[!ENDSHADEBOX]

## Zugriff auf den KI-Assistenten für Experience Platform in der Benutzeroberfläche

Sie können über die Kopfzeilennavigation in der Experience Platform-Benutzeroberfläche auf den AI-Assistenten zugreifen.

Wählen Sie die **[!UICONTROL Symbol &quot;KI-Assistent&quot;]** aus der Kopfzeile, um das Bedienfeld &quot;KI-Assistent&quot;zu starten.

![Die Startseite der Experience Platform-Benutzeroberfläche mit dem ausgewählten Symbol für den AI-Assistenten.](./images/ai-assistant/ai-assistant.png)

Hier können Sie Ihre Frage in das Textfeld eingeben und den KI-Assistenten nach Konzepten zu Daten oder Zielgruppen abfragen. Sie können auch Fragen zu Ihren Datenobjekten stellen, um besser zu verstehen, wie Sie sie für Ihren jeweiligen Anwendungsfall verwenden können.

### Anwendungsbeispiel: Verwenden des AI-Assistenten, um den Erstellungsprozess für Schemas zu beschleunigen

>[!NOTE]
>
>Der folgende Beispielworkflow verwendet den Erstellungsprozess des ExperienceEvent-Schemas, um zu veranschaulichen, wie Sie den AI-Assistenten bei Verwendung der Experience Platform-Benutzeroberfläche verwenden können.

Betrachten Sie einen Anwendungsfall, in dem Sie eine **Gerätehandel im Ereignisschema**. Während der Erstellung des ExperienceEvent-Schemas treffen Sie auf die `eventType` -Feld. An dieser Stelle können Sie Ihren Workflow verlassen und in der Dokumentation unter [Grundlagen der Schemakomposition](../xdm/schema/composition.md)oder Sie können den KI-Assistenten verwenden, um sofort Antworten auf Ihre Fragen abzurufen.

Geben Sie zunächst Ihre Frage in das bereitgestellte Textfeld ein. Im folgenden Beispiel wird der KI-Assistent mit der Frage konfrontiert: &quot;**Was ist das Feld eventType in einem Erlebnisereignis-Schema?**&quot;

![Der KI-Assistent für das Experience Platform mit der folgenden Frage, der zur Abfrage vorbereitet wurde: &quot;Was ist das Feld eventType in einem ExperienceEvent-Schema?](./images/ai-assistant/question.png)

Der KI-Assistent fragt dann seine Wissensdatenbank ab und berechnet eine Antwort. Nach einigen Augenblicken gibt der KI-Assistent eine Antwort und entsprechende Vorschläge zurück, die Sie als Aufforderung zur Weiterverfolgung verwenden können.

![Der KI-Assistent für Experience Platform mit einer Antwort auf die vorherige Abfrage.](./images/ai-assistant/answer.png)

Sie können mehr über ein bestimmtes Thema erfahren, indem Sie eine Frage stellen. Im nächsten Beispiel wird der KI-Assistent gefragt, wie der eventType in der Segmentierung verwendet werden kann.

![Eine Folgenachricht und eine Antwort wurden im KI-Assistenten für Experience Platform angezeigt.](./images/ai-assistant/follow-up-answer.png)

Sie können auch Fragen zu Ihrer Datennutzung an den KI-Assistenten stellen. Wenn Sie sich nach der Datennutzung erkundigen, müssen Sie sich in einer aktiven Sandbox befinden, damit der KI-Assistent Ihre Abfrage beantworten kann.

![Eine Frage zur Datennutzung, die fragt, wie viele Segmente ein Benutzer hat.](./images/ai-assistant/data-usage-question.png)

Mit jeder Antwort bietet Ihnen der KI-Assistent eine Möglichkeit, Ihre Antwort zu validieren, indem er dessen Quelle anzeigt. Links zur Dokumentation werden für Konzeptfragen bereitgestellt, während Datennutzungsfragen mit einer SQL-Abfrage überprüft werden können, die zeigt, wie die Antwort berechnet wurde.

>[!BEGINSHADEBOX]

**Ihr Feedback wird angefordert**

In dieser Alpha-Phase werden Sie eingeladen, Feedback zu den Antworten zu geben, die Sie vom KI-Assistenten erhalten. Alle Antworten und eingereichten Feedback werden geprüft, um das KI-Assistenzerlebnis weiter zu verbessern.

Um Feedback zu geben, wählen Sie entweder Daumen nach oben oder Daumen nach dem Erhalt einer Antwort vom AI-Assistenten aus und geben Sie dann Ihr Feedback in das bereitgestellte Textfeld ein. Wählen Sie als Nächstes **[!UICONTROL Feedback senden]** zu senden.

>[!ENDSHADEBOX]

>[!BEGINTABS]

>[!TAB Quelle ansehen]

Auswählen **[!UICONTROL Quelle anzeigen]** für eine Liste von Links zur Dokumentation, auf die der AI-Assistent verweist, um seine Antwort zu berechnen.

![Die Links zur im KI-Assistenten angezeigten Quelle.](./images/ai-assistant/show-sources.png)

>[!TAB Wirbel nach oben]

Wählen Sie das Daumen-nach-oben-Symbol aus, um Feedback dazu zu geben, was mit Ihrem Erlebnis mit dem KI-Assistenten gut gelaufen ist.

![Das positive Feedback-Fenster.](./images/ai-assistant/positive-feedback.png)

>[!TAB Daumen nach unten]

Wählen Sie das Daumendown-Symbol aus, um Feedback dazu zu geben, was basierend auf Ihrem Erlebnis mit dem KI-Assistenten verbessert werden könnte. Während dieses Schritts können Sie auch spezifische Kommentare zu Ihrem Erlebnis angeben. Das in den Kommentaren enthaltene Feedback wird täglich überprüft.

![Das negative Feedback-Fenster.](./images/ai-assistant/negative-feedback.png)

>[!TAB Markierung]

Wählen Sie das Flag-Symbol aus, um weitere Berichte zu Ihrem Erlebnis mit dem KI-Assistenten bereitzustellen.

![Das Fenster mit den Berichtsergebnissen.](./images/ai-assistant/report-results.png)

>[!ENDTABS]

### Erste Schritte

Sie können auch die vom AI-Assistenten bereitgestellten voreingestellten Eingabeaufforderungen für die ersten Schritte verwenden.

![Die angegebenen Eingabeaufforderungen finden Sie im Bedienfeld &quot;KI-Assistent&quot;.](./images/ai-assistant/ideas.png)

## Weitere Informationen

Weitere Informationen zum KI-Assistenten für Experience Platform finden Sie in diesem Abschnitt .

### Anwendungsbereich

Der KI-Assistent kann Abfragen basierend auf der Dokumentation und Ihrer Datennutzung beantworten.

#### Dokumentation

Sie können Dokumentationsfragen basierend auf Real-time Customer Data Platform und Zielgruppen stellen. Derzeit umfasst der Dokumentationsindex Adobe Experience Platform (Real-Time CDP und Audiences). Der Index wird regelmäßig aktualisiert.

Das Modell zum Abrufen der Dokumentation wird auf Experience Platform (Real-Time CDP und Zielgruppen) trainiert. Fragen, die nicht in Adobe Experience Platform enthalten sind, wie z. B. Fragen zu anderen Adobe-Produkten wie Adobe Target und der Creative Cloud Suite, können nicht beantwortet werden.

#### Datennutzung

Sie können den AI Assistant auch Fragen zur Datennutzung in den folgenden Domänen stellen:

* Attribute
* Datensätze
* Ziele
* Schemas
* Segmente
* Quellen

Bei Nutzungsdatenabfragen spiegeln Antworten möglicherweise nicht den aktuellen Status der Benutzeroberfläche wider. Die Daten, die diese Fragen unterstützen, werden alle 12 bis 24 Stunden aktualisiert. Möglicherweise müssen Sie Ihre Fragen wie folgt formatieren: &quot;Wann war das Segment mit dem Titel {TITLE} created?&quot; statt &quot;Wann war die {TITLE} Segment erstellt?&quot;

Sie müssen sich bei einer Sandbox anmelden, um sich über bestimmte Daten zu Objekten wie Schemas, Datensätzen, Attributen, Zielen und Segmenten zu informieren.

+++Auswählen für eine Liste unterstützter Datennutzungsfragen

Im Folgenden finden Sie eine Liste der derzeit unterstützten Datennutzungsfragen, gruppiert nach Domain.

>[!BEGINTABS]

>[!TAB Segmente]

* Gibt es doppelte Segmente?
* Zeigen Sie mir alle Streaming-Segmente.
* Ist Segment benannt {SEGMENT_ID} im Batch OR Stream ausgewertet?
* Welche Segmente sind Duplikate?
* Wie viele Segmente gibt es insgesamt?
* Gibt es Segmente mit denselben Namen, aber unterschiedlichen IDs?
* Wie werden Auswertungsmethoden (Batch, Edge, Streaming) segmentübergreifend verteilt?
* Zeigen Sie mir eine Liste der Segmente an, die zuletzt im letzten Monat geändert wurden.
* Welche Segmente wurden in der letzten Woche geändert?
* Gibt es Segmente, die in den letzten sechs Monaten nicht geändert wurden?
* Auflisten von Segmenten, die im letzten Jahr erstellt wurden.
* Zeigen Sie mir Segmente an, die zuletzt vor heute geändert wurden.
* Gibt es Muster oder Trends bei den Daten zur Segmenterstellung im vergangenen Jahr?
* Können Sie Segmente identifizieren, die seit ihrer Erstellung nicht geändert wurden?
* Gibt es Segmente, die seit ihrer Erstellung nicht geändert wurden?
* Wie sieht der Trend bei der Segmenterstellung im Zeitverlauf aus?
* Wie ist die Verteilung der Erstellungsdaten von Segmenten?
* Wie werden die Daten für die Segmentänderung verteilt?
* Welche Segmente haben die meisten Benutzerprofile?
* Welche Segmente haben die geringsten Benutzerprofile?
* Auflisten aller Batch-Segmente.
* Listet alle Kantensegmente auf.
* Welche Segmente werden aktiviert?
* Welche Segmente werden an Facebook weitergeleitet?
* Ist das Segment &quot;APAC-Kunden&quot;Batch oder Streaming?
* Wie viele Profile hat das Segment Aktive Arbeit?
* Haben einige meiner Segmente 0 Profile?
* Welche Datensätze wirken sich auf das Treuesegment der Bronze aus?
* Welche Segmentdefinitionen verwenden XDM-Felder, die &quot;Geschlecht&quot;enthalten?
* Welche ausgefüllten XDM-Felder treten in Streaming-Segmenten auf?
* Wie viele XDM-Felder gibt es für alle Segmentdefinitionen?
* Welche Segmente hat der Datensatz &quot;Professional Users&quot;Auswirkungen?
* Welche Segmente werden an die HTTP-API weitergeleitet?
* Welche der aktivierten Segmente sind für die meisten Zieltypen aktiviert?
* Wie hoch ist die Gesamtanzahl der aktivierten Segmente?
* Wie viele Segmente sind aktiviert?
* Wie viele doppelte Segmente werden aktiviert?
* Wie viele Segmente werden für jedes Ziel aktiviert?
* Welche Segmente werden für 0, 1 oder mehrere Ziele aktiviert? Anzeigen der Distribution.
* Welche Segmente sind für die meisten Ziele aktiviert?
* Welche doppelten Segmente werden aktiviert?
* Welche Segmente sind für Adobe Target aktiviert?
* Wie oft wird jede Zusammenführungsrichtlinie für alle Segmente verwendet?

>[!TAB Schemata]

* Wie viele XDM-Schemas sind definiert?
* Was sind die zuletzt erstellten Schemata?
* Wie viele Schemas für jede XDM-Klasse?
* Welches Schema verwendet der Datensatz &quot;Segmentaufnahme&quot;?
* Welche Schemas werden von keinem Datensatz verwendet?

>[!TAB Ziele]

* Wie viele Ziele gibt es?
* Was sind die zuletzt erstellten Ziele?
* Welche Ziele sind mit den einzelnen Segmenten verbunden?

>[!TAB Quellen]

* Wie viele Quellen wurden erstellt?
* Was sind die zuletzt erstellten Quellen?
* Wie viele Quellen sind verfügbar, aufgeschlüsselt nach Kategorie?
* Kann ich eine Quellverbindung von S3 erstellen?
* Welche Quellen haben zum Datensatz &quot;Mutual365&quot;beigetragen?

>[!TAB Datensätze]

* Wie viele Datensätze gibt es?
* Was sind die zuletzt erstellten Datensätze?
* Welche Datensätze sind für ein einheitliches Profil aktiviert?
* Gibt es einen TTL-Satz für den Datensatz &quot;Segmentaufnahme&quot;?
* Was ist die TTL für den Datensatz &quot;Professional Users&quot;?
* Welche Datensätze verwenden das Schema Professional Users?

>[!TAB Attribute]

* Welche XDM-Felder werden am häufigsten in allen DataSets ausgefüllt?
* Welche XDM-Felder und Attribute werden am häufigsten über Schemas hinweg verwendet?
* Welche XDM-Felder und Attribute werden im Professional Users-Schema verwendet?
* Die für dieses Segment verwendeten Attribute mit ID auflisten {SEGMENT_ID}.
* Wie viele XDM-Felder werden in mehr als 2 Segmenten verwendet?
* Welche Felder werden am häufigsten segmentübergreifend verwendet?
* Gibt es Felder, die nur in einem Segment verwendet werden?
* Welche Attribute werden für das Treuesegment &quot;Bronze&quot;verwendet?
* Welche Attribute werden in keinem Segment verwendet?
* Welche Attribute werden am häufigsten in Segmenten verwendet?

>[!ENDTABS]

+++

### Konversationserfahrung

Bei der Abfrage des KI-Assistenten müssen Sie verschiedene Aspekte bezüglich der Unterhaltserfahrung berücksichtigen.

>[!NOTE]
>
>Diese Einschränkungen sind temporär und werden während der Alpha-Phase verbessert.

>[!BEGINTABS]

>[!TAB Kontext kann nicht aus vorheriger Diskussion abgeleitet werden]

Der KI-Assistent kann frühere Diskussionen derzeit nicht als Kontext für eine bestimmte Frage betrachten. Beispiele finden Sie in der folgenden Tabelle:

| Zweideutige Frage | Frage löschen | Hinweis |
| --- | --- | --- |
| <ul><li>Erste Frage: Was ist ein Segment?</li><li>Folgenachfrage: &quot;Gibt es unterschiedliche Typen von ihnen?&quot;</li></ul> | <ul><li>Erste Frage: Was ist ein Segment?</li><li>Folgenachfrage: &quot;Gibt es unterschiedliche Typen von **Segmente**?&quot;</li></ul> | Der KI-Assistent kann nicht erkennen, was &quot;sie&quot;bedeutet. |
| <ul><li>Erste Frage: Was ist ein Segment?</li><li>Folgenachfrage: &quot;Können Sie mehr erarbeiten?&quot;</li></ul> | <ul><li>Erste Frage: Was ist ein Segment?</li><li>Folgenachfrage: &quot;Erläutern Sie, was ein Segment im Detail ist&quot;</li></ul> | Der KI-Assistent kann keine Dokumentation intelligent referenzieren, die auf &quot;Mehr&quot;basiert. |
| <ul><li>Erste Frage: Was ist ein Segment?</li><li>Folgt der Frage: &quot;Können Sie mir ein Beispiel für ein Beispiel geben?&quot;</li></ul> | <ul><li>Erste Frage: Was ist ein Segment?</li><li>Folgenachfrage: &quot;Können Sie mir ein Beispiel für ein Segment geben?&quot;</li></ul> | Der KI-Assistent kann nicht erkennen, wofür Sie ein Beispiel wünschen. |
| <ul><li>Erste Frage: Was ist ein Batch-Segment?</li><li>Folgenachfrage: &quot;Wie lässt sich ein Streaming-Segment vergleichen?&quot;</li></ul> | <ul><li>Erste Frage: Was ist ein Batch-Segment?</li><li>Folgenachfrage: &quot;Können Sie ein Streaming-Segment mit einem Batch-Segment vergleichen?&quot;</li></ul> | Der AI-Assistent kann nicht erkennen, worauf &quot;er&quot;sich bezieht, und kann daher das Streaming-Segment nicht vergleichen. |
| <ul><li>Erste Frage: &quot;Wie viele Segmente habe ich?&quot;</li><li>Folgenachfrage: &quot;Wie viele von ihnen verwenden Facebook als Ziel?&quot;</li></ul> | <ul><li>Erste Frage: &quot;Wie viele Segmente habe ich?&quot;</li><li>Folgenachfrage: &quot;Wie viele Segmente verwende ich Facebook als Ziel?&quot;</li></ul> | Der KI-Assistent kann nicht erkennen, worauf &quot;sie&quot;Bezug nimmt. |

{style="table-layout:auto"}

>[!TAB Kontext kann nicht von einer Seite abgeleitet werden]

Wenn Sie den KI-Assistenten nach einem bestimmten Element der Experience Platform-UI-Seite fragen, auf der Sie sich befinden, müssen Sie das spezifische Element in Ihrer Frage klar definieren.

| Zweideutige Frage | Frage löschen | Hinweis |
| --- | --- | --- |
| &quot;Was macht das?&quot; | &quot;Was bewirkt {PAGE_NAME} do? | Der KI-Assistent kann nicht erkennen, worauf sich &quot;dies&quot;bezieht. Sie müssen das spezifische Seitenelement angeben, über das Sie abfragen. |
| &quot;Warum wird es nicht retten?&quot; | &quot;Warum kann ich keine neue Sandbox mit dem Namen {NAME}?&quot; | Der KI-Assistent kann nicht erkennen, worauf &quot;er&quot;sich bezieht, und kann nicht erkennen, dass Sie Probleme mit einer Entität haben. |

{style="table-layout:auto"}

Darüber hinaus kann der KI-Assistent nur Fragen zu Fehlermeldungen beantworten, da der Fehler im Experience League dokumentiert ist.

>[!TAB Ambiguität]

Sie müssen Ihre Fragen klar formulieren und innerhalb eines Produkts, einer Anwendung oder einer Domäne eingrenzen, da der KI-Assistent derzeit keine Zweifel daran aufkommen lässt.

| Zweideutige Frage | Frage löschen | Hinweis |
| --- | --- | --- |
| &quot;Wie erstelle ich einen Filter? | Wie erstelle ich einen Filter in der Profilabfragesprache? | Sie müssen die Funktion angeben, nach der Sie filtern, da eine Vielzahl von Experience Platform-Funktionen die Filterung unterstützen. |
| &quot;Wie sehen die ersten Schritte aus? | Wie gehe ich mit der Verwendung von Zielen vor? | Sie müssen Klarheit über Ihre Ziele und Anwendungsfälle schaffen, da zu weit gefasste Konzepte zu generischen oder unnötig spezifischen Antworten führen können. |

{style="table-layout:auto"}

>[!ENDTABS]

### Geringfügiger kleiner Vortrag

Sie können mit dem KI-Assistenten kleine Gespräche führen, aber diese Kapazität ist derzeit begrenzt.

### Funktionsfragen

Der KI-Assistent vermittelt möglicherweise einen ungenauen Eindruck davon, was er tun kann. Es kann die folgenden Arten von Fragen falsch beantworten:

| Beispielfrage | Hinweis |
| --- | --- |
| &quot;Können Sie Fragen beantworten zu {ENTITY}?&quot; | Solange der KI-Assistent in der Lage ist, eine einzelne Seite zu finden, die auf eine bestimmte Entität verweist, antwortet er mit &quot;Ja&quot;. |
| &quot;Weißt du das? **x** Sprache?&quot; | Der KI-Assistent unterstützt derzeit nur Englisch, kann aber &quot;Ja&quot;beantworten, da das zugrunde liegende Modell es unterstützen kann. |
| &quot;Können Sie...?&quot; | Der KI-Assistent kann ja antworten, auch wenn dies nicht möglich ist. |

### Tipps

#### Fragen können mit der falschen Informationsquelle beantwortet werden

Es gibt Fälle, in denen Ihre Frage zu Ihren Nutzungsdaten zu einer Antwort führen kann, die auf der Dokumentation basiert. Der Grund dafür ist, dass der KI-Assistent Ihre Frage fälschlicherweise an die falsche Informationsquelle weiterleiten kann. Sie können dies verhindern, indem Sie:

* Umkehren Ihrer Frage zur Verwendung SQL-ähnlicher Sprachen
* Explizites Aufrufen der zu verwendenden Informationsquelle.

Beispiele finden Sie in der folgenden Tabelle:

| Ungültige Frage | Gute Frage | Anmerkungen |
| --- | --- | --- |
| Was ist mein größtes Segment? | Was ist mein größtes Segment? Verwendung von Daten. | Teilen Sie dem KI-Assistenten explizit mit, dass die Antwort auf Daten basieren soll. |
| Was ist mein größtes Segment? | Geben Sie mein größtes Segment an. | Es gibt Fälle, in denen eine &quot;Was...&quot;-Frage mit einer dokumentationsbasierten Frage verwechselt werden kann. Die Verwendung eines Befehls wie &quot;list&quot;ist ein stärkerer Indikator dafür, dass Sie eine Frage mit Daten im Kontext stellen. |
| Wie viele Datensätze habe ich? | Zählen Sie meine Datensätze. | Die ursprüngliche Frage funktioniert für Segmente, funktioniert jedoch möglicherweise nicht mit Datensätzen. |
