---
title: KI-Assistent in Adobe Experience Platform
description: Erfahren Sie, wie Sie mit dem KI-Assistenten zu Experience Platform- und Real-Time Customer Data Platform-Konzepten navigieren und diese verstehen können, sowie Informationen zur Verwendung Ihrer Objekte.
exl-id: 3fed2b1d-75fc-47ce-98d1-a811eb8a1d8e
source-git-commit: 8b0632efe10e280149d68facea44ea1f62267e3e
workflow-type: tm+mt
source-wordcount: '1946'
ht-degree: 0%

---

# Handbuch zur Benutzeroberfläche des KI-Assistenten (veraltet)

>[!IMPORTANT]
>
>Dieses Dokument gilt für den KI-Assistenten (veraltet). Informationen zum KI-Assistenten (der nächsten Generation) finden Sie im Handbuch [Benutzeroberfläche des KI-Assistenten](https://experienceleague.adobe.com/de/docs/experience-cloud-ai/experience-cloud-ai/ai-assistant/ai-assistant-ui) in der Dokumentation [KI in Experience Cloud](https://experienceleague.adobe.com/de/docs/experience-cloud-ai/experience-cloud-ai/home).

In der folgenden Tabelle finden Sie einen Vergleich von KI-Assistent (veraltet) und KI-Assistent (nächste Generation):

| Merkmalsbereich | KI-Assistent (veraltet) | KI-Assistent (nächste Generation) |
| --- | --- | --- |
| Benutzererlebnis | Der KI-Assistent (veraltet) ist nur in einem Bereich der rechten Leiste verfügbar. | Der KI-Assistent (der nächsten Generation) ist sowohl im Bereich der rechten Leiste als auch im immersiven Vollbilderlebnis verfügbar. |
| Funktionsumfang | Sie können den KI-Assistenten (frühere Version) sowohl für Produktkenntnisse als auch für betriebliche Einblicke verwenden. | Sie können den KI-Assistenten (der nächsten Generation) für Produktkenntnisse, operative Einblicke sowie erweiterte agentische Fähigkeiten und die Ausführung mehrstufiger Aufgaben verwenden. |
| Architektur von Platform | Der KI-Assistent (veraltet) wurde nicht auf dem Agent Orchestrator-Stack erstellt. | Der KI-Assistent (der nächsten Generation) wird von [Adobe Experience Platform Agent Orchestrator &#x200B;](https://experienceleague.adobe.com/de/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator) unterstützt und ermöglicht Erweiterbarkeit und erweiterte Koordinierung über Funktionen hinweg. |
| Anwendungsbereich | Der KI-Assistent (veraltet) ist eine anwendungsspezifische Implementierung. | Sie können den KI-Assistenten (der nächsten Generation) für ein einheitliches KI-Assistentenerlebnis in allen Adobe Experience Cloud-Programmen verwenden. |
| Zugriffs- und Berechtigungsmodell | Auf einzelne Produktgrenzen abgestimmtes Zugriffsmodell für die Anwendung. | Alle Benutzer erhalten Zugriff auf den KI-Assistenten (der nächsten Generation) und die zugehörigen Experience Platform-Agenten. **Hinweis**: <ul><li>**Adobe Experience Manager**: Ihr Administrator muss Ihnen über die [Adobe Admin Console](https://helpx.adobe.com/de/enterprise/using/admin-console.html) die Berechtigung für den Zugriff auf den KI-Assistenten (der nächsten Generation) erteilen.</li><li>**Customer Journey Analytics**: Ihr Administrator muss Ihnen die Berechtigung für den Zugriff auf den KI-Assistenten über die [Customer Journey Analytics-Zugriffssteuerung](https://experienceleague.adobe.com/de/docs/analytics-platform/using/technotes/access-control?lang=en) erteilen. Auf diese Weise können Sie Fragen zu Produktwissen und Dateneinblicken stellen. |

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie den KI-Assistenten in der Adobe Experience Platform-Benutzeroberfläche verwenden können.

## Zugriff auf den KI-Assistenten in der Experience Platform-Benutzeroberfläche

Um den KI-Assistenten zu starten, wählen Sie die **[!UICONTROL AI Assistant icon]** in der oberen Kopfzeile der Experience Platform-Benutzeroberfläche aus.

![Die Experience Platform-Startseite mit dem ausgewählten Symbol für den KI-Assistenten und der geöffneten Benutzeroberfläche des KI-Assistenten.](./images/ai-assistant-full-icon.png)

Die Benutzeroberfläche des KI-Assistenten wird angezeigt und stellt Ihnen sofort Informationen zum Einstieg bereit. Sie können die unter [!UICONTROL Ideas to get started] bereitgestellten Optionen verwenden, um Fragen und Befehle zu beantworten, z. B.:

* [!UICONTROL Which of my audiences are activated?]
* [!UICONTROL What is a schema?]
* [!UICONTROL Tell me some common use cases for Real-Time CDP]

## Handbuch zur Benutzeroberfläche des KI-Assistenten

>[!NOTE]
>
>Der folgende Workflow ist ein Beispiel, das den Erlebnisereignisschema-Erstellungsprozess verwendet, um zu veranschaulichen, wie Sie den KI-Assistenten bei der Verwendung der Experience Platform-Benutzeroberfläche verwenden können.

Stellen Sie sich einen Anwendungsfall vor, in dem Sie ein **Device Trade in Event Schema** erstellen. Während des Erstellungsprozesses des Erlebnisereignis-Schemas stoßen Sie auf das Feld `eventType` . „An dieser Stelle haben Sie die Möglichkeit, Ihren Workflow zu beenden und sich auf die Dokumentation [Grundlagen einer Schemakomposition](../xdm/schema/composition.md) zu beziehen. Alternativ können Sie den KI-Assistenten verwenden, um Antworten auf Ihre Fragen abzurufen und zusätzliche Ressourcen über die vom KI-Assistenten empfohlenen Dokumentations-Links zu finden.“

Um zu beginnen, geben Sie Ihre Frage in das bereitgestellte Textfeld ein. Im folgenden Beispiel wird der KI-Assistent mit der Frage bereitgestellt: &quot;**Was ist das eventType-Feld in einem ExperienceEvent-Schema?**&quot;

![KI-Assistent für Experience Platform mit der folgenden Frage zur Abfrage vorbereitet: „Was ist das eventType-Feld in einem ExperienceEvent-Schema?](./images/question.png)

Der KI-Assistent fragt dann seine Wissensdatenbank ab und berechnet eine Antwort. Nach einigen Augenblicken gibt der KI-Assistent eine Antwort und zugehörige Vorschläge zurück, die Sie als Folgeaufforderungen verwenden können.

![KI-Assistent für Experience Platform mit einer Antwort auf die vorherige Abfrage.](./images/answer.png)

Nachdem Sie eine Antwort vom KI-Assistenten erhalten haben, können Sie aus einer Reihe von Optionen auswählen, um zu entscheiden, wie Sie fortfahren möchten.

### Funktionen des KI-Assistenten {#features}

In diesem Abschnitt werden die verschiedenen Funktionen des KI-Assistenten beschrieben, die Sie während Ihrer Workflows auf Experience Platform verwenden können.

### Anzeigen von betrieblichen Datenobjekten {#view-operational-data-objects}

Abhängig von Ihrer Abfrage stellt der KI-Assistent zusätzliche Informationen zu den Daten in Ihrer Sandbox bereit. Um anzuzeigen, wie die Antwort auf Ihre Abfrage auf Ihre bestimmte Sandbox angewendet wird, wählen Sie **[!UICONTROL In your sandbox]aus.**

Beim Anzeigen von Daten zu Ihrer Sandbox kann der KI-Assistent direkte Links zu bestimmten Seiten der Benutzeroberfläche bereitstellen, auf denen Ihre abgefragten Daten angezeigt werden.

+++Beispiel anzeigen

In diesem Beispiel gibt der KI-Assistent zusätzliche Informationen zu den vorhandenen XDM-Schemata in Ihrer Sandbox zurück, einschließlich ihrer Gesamtanzahl und der fünf am häufigsten verwendeten Felder.

![&#x200B; Dropdown-Fenster „In Ihrer Sandbox“ wird geöffnet, in dem zusätzliche Informationen zu Ihren Schemata angezeigt werden.](./images/in-your-sandbox.png)

+++

### Zitate anzeigen {#view-citations}

Sie können die von KI-Assistent an Sie zurückgegebenen Antworten überprüfen, indem Sie die Zitate lesen, die mit jeder Antwort zum Produktwissen verfügbar sind.

+++Wählen Sie aus, um ein Beispiel für die Anzeige von Quellen anzuzeigen

Um Zitate anzuzeigen und die Antwort des KI-Assistenten zu validieren, wählen Sie **[!UICONTROL Show sources]** aus.

![Die Antwort des KI-Assistenten mit ausgewählter Option „Quellen anzeigen“](./images/show-sources.png)

Der KI-Assistent aktualisiert die Benutzeroberfläche und stellt Links zur Dokumentation bereit, die die ursprüngliche Antwort bestätigen. Wenn Zitate aktiviert sind, aktualisiert der KI-Assistent außerdem die Antwort, sodass sie Fußnoten enthält, um die spezifischen Teile der Antwort anzugeben, die auf die bereitgestellte Dokumentation verweisen.

![Ein Dropdown-Menü mit den Zitaten, die der KI-Assistent für Konzeptfragen bereitstellt.](./images/citations.png)

+++

### Betriebliche Erkenntnisse {#operational-insights}

Sie müssen sich in einer aktiven Sandbox befinden, damit der KI-Assistent eine Frage zu Ihren operativen Einblicken ausreichend beantworten kann.

+++Wählen Sie aus, um ein Beispiel für eine operative Insights-Frage anzuzeigen.

Im folgenden Beispiel wird der KI-Assistent nach der folgenden Abfrage gefragt: **„Anzeigen von Datenflüssen, die mit der Amazon S3-Quelle erstellt wurden“**.

![Eine Frage zu operativen Einblicken.](./images/op-insights-question.png)

Der KI-Assistent antwortet dann mit einer Tabelle, in der Ihre Datenflüsse und die entsprechenden IDs aufgelistet sind. Wählen Sie das Download-Symbol ![Download-Symbol](/help/images/icons/download.png), um die Tabelle als CSV-Datei herunterzuladen. Um die gesamte Tabelle anzuzeigen, klicken Sie auf das Symbol „Erweitern![&#x200B; (Symbol „Erweitern](/help/images/icons/expand.png)).

![Eine Antwort auf operative Erkenntnisse](./images/op-insights-answer.png)

Eine erweiterte Ansicht der Tabelle wird angezeigt, die Ihnen eine umfassendere Liste der Datenflüsse auf der Grundlage der Parameter Ihrer Abfrage bereitstellt.

![Eine Ansicht der erweiterten Tabelle.](./images/table.png)

Bei der Aufforderung mit einer Frage zu operativen Einblicken gibt der KI-Assistent eine Erklärung dazu ab, wie die Antwort berechnet wurde. Im folgenden Beispiel beschreibt der KI-Assistent die Schritte, die unternommen wurden, um die mithilfe der [!DNL Amazon S3] erstellten Datenflüsse zu identifizieren.

![KI-Assistent mit einer Erläuterung, wie die Antwort berechnet wurde.](./images/answer-explained.png)

Sie können auch Filter und Änderungen für Ihre Fragen angeben und den KI-Assistenten anweisen, seine Ergebnisse basierend auf den eingeschlossenen Filtern zu rendern. Sie können beispielsweise den KI-Assistenten bitten, Ihnen einen Trend der Anzahl der Segmentdefinitionen in der Reihenfolge ihres Erstellungsdatums anzuzeigen, Segmentdefinitionen mit null Gesamtprofilen zu entfernen und bei der Anzeige der Daten Monatsnamen anstelle von Ganzzahlen zu verwenden.

+++

### Überprüfen von Antworten auf betriebliche Einblicke {#verify-responses}

Sie können jede Antwort im Zusammenhang mit Fragen zu operativen Einblicken mithilfe einer SQL-Abfrage überprüfen, die der KI-Assistent bereitstellt.

+++Wählen Sie aus, um ein Beispiel für die Verifizierung von Antworten auf operative Insights anzuzeigen.

Nachdem Sie eine Antwort auf eine operative Insights-Frage erhalten haben, wählen Sie **[!UICONTROL Show sources]** und dann **[!UICONTROL View source query]** aus.

![Quellabfrage anzeigen](./images/view-source-query.png)

Bei der Abfrage mit einer operativen Insights-Frage stellt der KI-Assistent eine SQL-Abfrage bereit, mit der Sie den Prozess überprüfen können, der zur Berechnung der Antwort erforderlich war. Diese Quellabfrage dient nur zu Verifizierungszwecken und wird vom Abfrage-Service nicht unterstützt.

![Beispiel einer Quellabfrage](./images/source-query.png)

+++

### Entität für automatische Vervollständigung verwenden {#use-entity-auto-complete}

Sie können die Funktion zur automatischen Vervollständigung verwenden, um eine Liste von Datenobjekten zu erhalten, die in Ihrer Sandbox vorhanden sind. Empfehlungen zur automatischen Vervollständigung sind für die folgenden Domains verfügbar: Zielgruppen, Schemata, Datensätze, Journey, Quellen und Ziele.

+++Auswählen, um ein Beispiel für die automatische Vervollständigung anzuzeigen

Sie können die automatische Vervollständigung verwenden, indem Sie das Pluszeichen (**`+`**) in Ihre Abfrage aufnehmen. Alternativ können Sie auch das Pluszeichen (**`+`**) unten im Texteingabefeld auswählen. Es wird ein Fenster mit einer Liste empfohlener Datenobjekte aus Ihrer Sandbox angezeigt.

![Beispiel für automatische Vervollständigung](./images/autocomplete.png)

+++

### Verwenden von Multi-Turn {#use-multi-turn}

Sie können die Multi-Turn-Funktionen des KI-Assistenten nutzen, um während Ihres Erlebnisses eine natürlichere Konversation zu führen. Der KI-Assistent kann bei Bedarf Folgefragen beantworten. Dieser Kontext kann aus einer früheren Interaktion abgeleitet werden.

+++Wählen Sie aus, um ein Beispiel für die Mehrfachdrehung anzuzeigen.

Im folgenden Beispiel wird der KI-Assistent zunächst nach der Gesamtzahl der Datenflüsse gefragt und dann aufgefordert, die zehn neuesten Datenflüsse aufzulisten.

![Beispiel für Multi-Turn](./images/multiturn.png)

+++

### Neue Unterhaltung beginnen

Mit dem KI-Assistenten können Sie Themen ändern, indem Sie eine neue Konversation zurücksetzen und starten.

+++Wählen Sie aus, um ein Beispiel für das Zurücksetzen Ihrer Konversation zu sehen

Klicken Sie zum Zurücksetzen auf die Auslassungszeichen (**`...`**) auf der Benutzeroberfläche des KI-Assistenten und dann auf **[!UICONTROL Start new conversation]**. Dies informiert den KI-Assistenten darüber, dass Sie beabsichtigen, Themen zu ändern, und kann besonders bei der Fehlerbehebung bei Abfragen hilfreich sein, die entweder fehlschlagen oder auf falsche Informationen verweisen.

![Die Auslassungszeichen sind ausgewählt, und die Option Neue Konversation starten ist ausgewählt.](./images/reset.png)

+++

### Entdeckbarkeit verwenden {#use-discoverability}

Sie können die Auffindbarkeitsfunktion des KI-Assistenten verwenden, um eine Liste der allgemeinen Themen anzuzeigen, die in Entitäten gruppiert sind und die der KI-Assistent unterstützt.

+++Auswählen, um ein Beispiel für eine Entdeckung anzuzeigen

Um die Auffindbarkeit anzuzeigen, wählen Sie das Glühbirnensymbol in der oberen Kopfzeile der Benutzeroberfläche des KI-Assistenten aus.

![Die Entdeckungsfunktion des KI-Assistenten.](./images/lightbulb.png)

Wählen Sie als Nächstes eine Kategorie und dann eine Eingabeaufforderung aus der bereitgestellten Liste aus. Mithilfe dieser Funktion können Sie sich einen besseren Überblick über die Arten von Fragen verschaffen, die der KI-Assistent beantworten kann. Sie können auch die bereits vorhandenen Eingabeaufforderungen mit bestimmten Details aktualisieren, die sich auf Ihre Sandbox beziehen, indem Sie freien Text oder &quot;[&quot; &#x200B;](#use-auto-complete).

![Der KI-Assistent fordert zur Entdeckung auf.](./images/prompt.png)

+++

### Frage automatisch vervollständigen {#use-question-autocomplete}

Mit der Funktion zur automatischen Vervollständigung von Fragen des KI-Assistenten können Sie eine Frage aus einer Liste von Empfehlungen des KI-Assistenten auswählen.

+++Auswählen, um ein Beispiel für die automatische Vervollständigung einer Frage anzuzeigen

Um das Bedienfeld mit den vorgeschlagenen Fragen anzuzeigen, geben Sie mindestens sieben (7) Zeichen in das Eingabefeld ein. Wählen Sie anschließend aus dem angezeigten Menü die Frage aus, die für Sie relevant ist.

![Das Popup-Fenster mit vorgeschlagenen Fragen aus dem KI-Assistenten.](./images/suggested_questions.png)

Möglicherweise müssen Sie die Platzhalter in einigen Fällen aktualisieren, in denen eine vorgeschlagene Frage betriebliche Einblicke erfordert. Sie müssen beispielsweise den spezifischen Namen eines Datensatzes oder einer Zielgruppe hinzufügen, wenn der Vorschlag aus dem KI-Assistenten Platzhalter enthält.

![Ein Vorschlag des KI-Assistenten, der Platzhalter enthält.](./images/placeholder.png)

Platzhalter werden blau hervorgehoben. Wählen Sie den Platzhalter aus, um mit der Aktualisierung seines Werts zu beginnen. Um optimale Ergebnisse bei numerischen Platzhaltern zu erzielen, stellen Sie sicher, dass Sie Ziffern anstelle von Text verwenden. Sie können auch die Funktion zur automatischen Vervollständigung von Entitäten verwenden, um die Platzhalterwerte zu aktualisieren. Sie können keine Frage senden, die nicht ausgefüllte Platzhalter enthält.

**HINWEIS**: Vorschläge sind standardmäßig aktiviert. Wählen Sie den Umschalter **[!UICONTROL Suggest ideas]** aus, um die Funktion zu deaktivieren.

![Ein Vorschlag des KI-Assistenten mit aktualisierten Platzhaltern.](./images/updated_placeholder.png)

+++

### Verwandte Vorschläge verwenden {#use-related-suggestions}

Sie können den Abschnitt mit den zugehörigen Vorschlägen in jeder Antwort des KI-Assistenten verwenden, um Ihr Gespräch fortzusetzen.

+++Auswählen, um Beispiel für zugehörige Vorschläge anzuzeigen

Zugehörige Vorschläge werden mit jeder Antwort des KI-Assistenten zurückgegeben. Um Ihr Gespräch fortzusetzen, wählen Sie einen der Vorschläge im Abschnitt mit den entsprechenden Vorschlägen aus.

![Eine Liste zugehöriger Vorschläge des KI-Assistenten.](./images/related_suggestions.png)

Ähnlich wie bei Platzhaltern, die für die automatische Vervollständigung infrage kommen, müssen Sie Platzhalter, die in verknüpften Vorschlägen enthalten sind, aktualisieren, bevor Sie die Abfrage senden können.

![Eine Abfrage aus zugehörigen Vorschlägen mit aktualisierten Platzhaltern.](./images/related_suggestions_placeholder.png)

+++

## Feedback geben {#feedback}

Mithilfe der mit der Antwort bereitgestellten Optionen können Sie Feedback zu Ihren Erfahrungen mit dem KI-Assistenten geben.

Um Feedback zu geben, wählen Sie entweder Daumen hoch, Daumen runter oder eine Markierung aus, nachdem Sie eine Antwort vom KI-Assistenten erhalten haben, und geben Sie dann Ihr Feedback in das bereitgestellte Textfeld ein.

![Die Feedback-Option im KI-Assistenten.](./images/provide-feedback.png)

+++Auswählen, um weitere Beispiele anzuzeigen

>[!BEGINTABS]

>[!TAB Daumen hoch]

Wählen Sie das Symbol mit den Daumen nach oben aus, um Feedback zu der Frage zu geben, was mit Ihrem Erlebnis mit dem KI-Assistenten gut gelaufen ist.

![Das Fenster mit positivem Feedback.](./images/thumbs-up.png)

>[!TAB Daumen runter]

Wählen Sie das Symbol mit den Daumen nach unten aus, um Feedback zu dem zu geben, was basierend auf Ihren Erfahrungen mit dem KI-Assistenten verbessert werden könnte. In diesem Schritt können Sie auch spezifische Kommentare zu Ihrem Erlebnis eingeben. Das Feedback in den Kommentaren wird täglich überprüft.

![Das Negativ-Feedback-Fenster.](./images/thumbs-down.png)

>[!TAB Markierung]

Wählen Sie das Flag-Symbol aus, um weitere Berichte zu Ihrem Erlebnis mit dem KI-Assistenten bereitzustellen.

![Das Fenster „Berichtsergebnisse“.](./images/flag.png)

>[!ENDTABS]

+++
