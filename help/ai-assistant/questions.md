---
title: Fragenleitfaden für KI-Assistenten
description: In diesem Dokument erfahren Sie mehr über Beispielfragen, die Sie bei der Abfrage des KI-Assistenten verwenden können.
exl-id: d16d1262-cc2d-45c9-94c4-b86132183442
source-git-commit: 7268895d0b1924f9d3e7cee24e549c79245ef099
workflow-type: tm+mt
source-wordcount: '2105'
ht-degree: 0%

---

# Fragenleitfaden für KI-Assistenten

Lesen Sie dieses Dokument, um eine Reihe von Beispielfragen zu erhalten, die Sie bei der Abfrage des KI-Assistenten verwenden können.

In diesem Dokument erfahren Sie auch, wie Sie [&#x200B; Ihre Fragen formulieren können](#phrasing-your-questions) um vom KI-Assistenten optimale Antworten zu erhalten.

## Zielbezogene Fragen {#objectives-questions}

Die folgenden Beispielfragen sind nach Zielen gruppiert, die Sie mit dem KI-Assistenten erreichen können:

| Ziel | Beschreibung | Beispiel |
| --- | --- | --- |
| Lernkonzepte und fortlaufende Workflows | <ul><li>Als Anfänger können Sie den KI-Assistenten verwenden, um Real-Time CDP- und Adobe Journey Optimizer-Konzepte zu erlernen und sich mit Produkten und Funktionen vertraut zu machen, mit denen Sie nicht vertraut sind.</li><li>Als erfahrener Benutzer können Sie den KI-Assistenten verwenden, um einen Randfall zu lösen, der Ihren Workflow blockieren könnte. | <ul><li>Wie richte ich ein Dashboard in Journey Analytics ein?</li><li>Erzählen Sie mir einige Anwendungsfälle für Real-Time CDP.</li></ul> |
| Fehlerbehebung | Verwenden Sie den KI-Assistenten, um zu erfahren, wie Sie grundlegende Fehler debuggen, auf die Sie in Ihrem Workflow stoßen können. | <ul><li>Was bedeutet dieser Fehler {ERROR_MESSAGE}?</li><li>Warum kann ich die Zielgruppe mit dem Namen „Luma: E-Mail-Zielgruppe“ nicht löschen?</li></ul> |
| Sandbox-Hygiene | Verwenden Sie den KI-Assistenten, um Duplikate oder nicht verwendete Objekte zu identifizieren, damit Sie Ihre Sandbox effizient verwalten können. | <ul><li>Können Sie mir ähnliche Zielgruppen zeigen?</li><li>Gibt es Schemata, denen kein Datensatz zugeordnet ist?</li></ul> |
| Wertanalyse | Verwenden Sie den KI-Assistenten, um Ihre am häufigsten verwendeten Datenobjekte zu identifizieren und Leistungsindikatoren zu bewerten oder die wertvollsten Datenobjekte zu finden. | <ul><li>Wie viele Profile sind in unserer Segmentdefinition „Luma: E-Mail-Zielgruppe“?</li><li>Wann wurden Zielgruppen für das Experience Cloud-Zielgruppen-Ziel aktiviert?</li></ul> |
| Suche | Verwenden Sie den KI-Assistenten, um unterstützte Experience Platform-Objekte wie Zielgruppen, Datensätze, Ziele, Schemata und Quellen zu finden. | <ul><li>Listen Sie die Zielgruppen auf, die „Luma“ im Namen enthalten, die im letzten Quartal erstellt wurden.</li><li>Welche Attribute enthalten das XDM-Schema „Luma: Custom Actions“?</li></ul> |
| Wirkungsanalyse | Verwenden Sie den KI-Assistenten, um Datenobjekte zu identifizieren, die in bestimmten Workflows verwendet wurden, damit Sie die Auswirkungen von Änderungen bewerten können. | <ul><li>Welche Zielgruppen verwenden `homeAddress.city` im Schema „Luma: PersonProfiles“?</li><li>In welchen Datensätzen wird das `consents.marketing.push.val` Profilattribut gespeichert?</li></ul> |

{style="table-layout:auto"}

## Operative Einblicke nach Entität und Fragen zum Produktwissen{#objects-questions}

Die folgenden Fragen sind nach Datenobjekten gruppiert und werden entweder als [operative Erkenntnisse](./home.md#operational-insights) oder [Produktwissen](./home.md#product-knowledge) klassifiziert.

![](./images/prompt.png)

* **Zielgruppen - Operative Einblicke**
   * Welche Zielgruppen verwenden andere Zielgruppen?
   * Wie verteilt sich die Anzahl der Profile auf die Zielgruppen?
   * Zielgruppen anzeigen, die zuletzt vor dem {RELATIVE_DATE} geändert wurden.
   * Welche Zielgruppen haben 0 Profile?
   * Wird {USE_AUTO_COMPLETE_TO_FILL_AUDIENCE_NAME} in anderen Zielgruppen verwendet?
* **Attribute - operative Einblicke**
   * Welche Zielgruppen verfügen über XDM-{ATTRIBUTE_PATH} in ihrer Segmentdefinition?
   * Wie viele XDM-Schemaattribute werden in keiner Zielgruppe verwendet?
   * In welchen Schemata sind XDM-Attribute {ATTRIBUTE_PATH}?
   * Welche XDM-Attribute werden aktiviert?
   * Welche XDM-Attribute werden in Zielgruppen mit mehr als 10 Profilen verwendet?
* **Datenflüsse - operative Einblicke**
   * Welche Datenflüsse tragen zu {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} Datensatz bei?
   * Welche Quelldatenflüsse werden nicht verwendet oder haben keine Daten mehr?
   * Auflisten der Quelldatenflüsse, die ich habe.
   * Welche Datenflüsse werden für jeden Quell-Connector konfiguriert?
* **Datensätze - Operative Einblicke**
   * Wie viele Datensätze wurden mit demselben Schema aufgenommen?
   * Welcher Quell-Connector ist mit {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} Datensatz verknüpft?
   * Welche Datensätze werden in den einzelnen Zielgruppen verwendet?
   * Welche Schemata werden in keinem Datensatz verwendet?
   * Wie viele Datensätze habe ich?
* **Ziele - Operative Einblicke**
   * Welche Ziele befinden sich in einem aktiven Status?
   * Für welche Zielkonten sind 0 Zielgruppen aktiviert?
   * Wie viele Zielgruppen werden für jedes Ziel aktiviert?
   * Welche Ziele haben die höchste Anzahl aktivierter Zielgruppen?
* **Journey - Betriebseinblicke**
   * Wie viele Journey habe ich?
   * Welche Journey wurden in {RELATIVE_DATE} (z. B. in der letzten Woche) oder {RELATIVE_DATE} (z. B. vor/nach/an einem bestimmten Datum) erstellt?
   * Liste der Journey anzeigen, die in {RELATIVE_DATE} (z. B. in der letzten Woche) oder {RELATIVE_DATE} (z. B. vor/nach/an einem bestimmten Datum) geändert wurden?
   * Führt die Live-Journey auf, die ich habe.
   * Listen Sie die Zielgruppen auf, die in Live-Journey verwendet werden.
* **Quellen - Operative Einblicke**
   * Welche Quellen befinden sich im aktiven Status?
   * Welcher Quell-Connector mit Datensatz {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} verknüpft ist.
   * Welcher Quell-Connector hat die höchste Anzahl verknüpfter Konten?
   * Anzeigen der Datenflüsse und der zugehörigen Quell-Connectoren
* **Punktuelles Lernen - Produktwissen (Real-Time CDP und Journey Optimizer)**
   * Was sind Lookalike-Zielgruppen?
   * Wie sind Benutzergruppen mit Rollen verbunden?
   * Wann sollte ich einen Datentyp im Vergleich zu einer Feldergruppe verwenden?
   * Was ist der Unterschied zwischen einer Identität und einem Primär- oder Fremdschlüssel?
* **Fehlerbehebung - Produktkenntnisse (Real-Time CDP und Journey Optimizer)**
   * Wobei kann der KI-Assistent helfen?
   * Kann ich ein Profil-aktiviertes Schema nach der Datenaufnahme löschen?
   * Warum kann ich eine Zielgruppe nicht löschen?
   * Wie lange dauert es, bis Zielgruppen evaluiert und die Ergebnisse für die Zielgruppenbestimmung verfügbar sind?

## Formulieren von Fragen {#phrasing-your-questions}

Sie müssen Ihre Fragen an den KI-Assistenten mit Klarheit und Kontext formulieren, um eine möglichst präzise Antwort zu erhalten. Eine Anleitung dazu, wie Sie im Kontext eine klare Frage stellen, finden Sie in der folgenden Liste von Tipps:

* Geben Sie Ihre Aufgabe und/oder Frage kurz an.
* Vermeiden Sie mehrdeutige Sprache oder eine übermäßig komplexe Syntax, um das Verständnis zu erleichtern.
* Geben Sie einen relevanten Kontext zu Ihrer Aufgabe und/oder Frage an, da der Kontext dazu beitragen kann, dass der KI-Assistent relevantere Antworten generiert.

Lesen Sie die folgenden Tabellen, um weitere Anleitungen zu Best Practices zu erhalten, die bei der Beantwortung von Fragen an den KI-Assistenten befolgt werden sollten.

In den folgenden Tabellen sind Best Practices aufgeführt, die Sie bei der Verwendung des KI-Assistenten befolgen können:

| tun | Beispiel |
| --- | --- |
| <ul><li>Geben Sie das Objekt oder die Informationen an, die Sie abrufen oder analysieren möchten.</li><li>Versuchen Sie, Ihre Datenobjektnamen in Anführungszeichen zu setzen. Wenn Sie nur einen Teil des Objektnamens kennen, können Sie diesen auch in der Frage angeben.</li><li>Verwenden Sie [Objekt automatisch vervollständigen](./ui-guide.md#use-auto-complete), damit der KI-Assistent den Kontext Ihrer Abfrage besser verstehen kann.</li></ul> | <ul><li>Welche Datensätze verwenden das Schema „Luma - Treue“?</li><li>Die aktivierten Segmente anzeigen, deren Namen „Luma“ enthalten. Ordnen Sie sie nach der Anzahl der Profile zu.</li></ul> |
| <ul><li>Vermeiden Sie Mehrdeutigkeiten und verwenden Sie eine klare Sprache</li><li>Verwenden Sie eine präzise Terminologie, um eine klarere Abfrage zu ermöglichen.</li><li>Wenn Sie Fragen zu Adobe Experience Platform stellen, versuchen Sie, eine Experience Platform-spezifische Terminologie zu verwenden, um die Relevanz der Antworten zu verbessern.</li></ul> | <ul><li>Wie viele Profile habe ich in „ACME Audience“?</li><li>Zeigen Sie mir die fünf häufigsten XDM-Attribute, die in aktivierten Zielgruppen verwendet werden.</li></ul> |
| <ul><li>Geben Sie den Kontext an oder geben Sie ein Kriterium zum Filtern Ihrer Ergebnisse an.</li><li>Verwenden Sie in den Fragen ein Filterkriterium, um die Datenmenge in der Antwort zu begrenzen.</li></ul> | <ul><li>Zielgruppen anzeigen, die nicht aktiviert wurden, vor mehr als 6 Monaten erstellt wurden und noch nie geändert wurden.</li><li>Für „ACME-Ziel“ aktivierte Zielgruppen anzeigen, die mehr als 10000 Profile aufweisen.</li></ul> |

{style="table-layout:auto"}

| Tu das nicht | Beispiel |
| --- | --- |
| Verwende eine vage oder mehrdeutige Sprache. | <ul><li>Geben Sie mir Informationen zu Datensätzen.</li><li>Wie viele Benutzer habe ich in „ACME Audience“?</li><li>Segmente anzeigen.</li><li>Attribute auflisten.</li></ul> |
| Unvollständige Anfragen stellen. | „Luma - Treueprogramm-Datensatz“ |
| Annahme von Wissen ohne Kontext. | <ul><li>Zielgruppen in den letzten 6 Monaten.</li><li>Erstellen Sie eine Abfrage für mich.</li></ul> |
| Formulieren Sie übermäßig komplexe Abfragen. | Bieten Sie eine umfassende Analyse der Datenherkunft für alle Objekte und deren Abhängigkeiten. |
| Kriterien oder Parameter auslassen. | Anzeigen von Datensätzen |

{style="table-layout:auto"}

## Datensatz-Beobachtbarkeit {#dataset-observability}

Der KI-Assistent kann jetzt Fragen zu bestimmten Datensatzmetriken wie Speichergröße und Zeilenanzahl beantworten.

* Welche sind meine größten Datensätze nach Größe?
* Welches sind meine größten Datensätze nach Zeilen?
* Wie viele Datensätze sind leer?
* Welche Datensätze sind leer?

Darüber hinaus können Sie ähnliche Absichten durch eine Reihe von verschiedenen Varianten zu den vier oben genannten Fragen vermitteln.

+++Auswählen, um akzeptierte Varianten von Fragen zur Datensatzbeobachtung anzuzeigen

* Welche sind die fünf häufigsten Datensätze nach Größe?
* Welcher Datensatz hat die größte Anzahl von Zeilen?
* Wie viele Datensätze enthalten keine Daten?
* Datensätze mit einer Größe >10 MB auflisten?
* Datensätze mit Zeilen unter 10 auflisten.
* Können Sie mir die Datensätze zeigen, die vollständig leer sind?
* Welcher Datensatz ist gemessen an der Speichergröße der größte?
* Was ist der kleinste Datensatz in Bezug auf die Zeilenanzahl?
* Wie viele meiner Datensätze verfügen über Daten und wie viele sind leer?
* Wie hoch ist die Zeilenanzahl für den Datensatz mit dem Namen {DATASET_NAME}?
* Wie ist die Größe von {DATASET_NAME} im Vergleich zu meinen anderen Datensätzen?
* Wie groß ist {DATASET_NAME}?
* Wie viele Zeilen hat {DATASET_NAME}?
* Wie groß und wie viele Zeilen sind {DATASET_NAME}?
* Können die größten und kleinsten Datensätze nach Speichergröße aufgelistet werden?

+++

Sie können Ihre Fragen zur Datenbeobachtbarkeit auch mit einem Qualifizierer verfeinern, um Ihre Abfrage nach einem bestimmten Zeitraum zu filtern:

* Datensätze, die in den letzten (x) Tagen Batches erhalten
* Datensätze erhalten in den letzten (x) Tagen keine Batches
* Datensätze mit den meisten Daten, die in den letzten (x) Tagen aufgenommen wurden
* Datensatzanzahl für einen bestimmten Datensatz in den letzten (x) Tagen

+++Auswählen, um akzeptierte Varianten von Fragen zur Datensatzbeobachtung anzuzeigen

* Wie viele Datensätze haben in den letzten (x) Tagen Batches erhalten?
* Welche Datensätze haben in den letzten (x) Tagen Batches erhalten?
* Können Sie die Datensätze auflisten, die in den letzten (x) Tagen Daten aufgenommen haben?
* Wie viele Datensätze haben in den vorherigen (x) Tagen neue Batches erhalten?
* Welche Datensätze wurden in den letzten (x) Tagen mit neuen Daten aktualisiert?
* Listet Datensätze auf, die innerhalb der letzten (x) Tage Batch-Aktivitäten hatten.
* Wie viele Datensätze haben in den letzten (x) Tagen keine Batches erhalten?
* Welche Datensätze haben in den letzten (x) Tagen keine Batches erhalten?
* Können Sie Datensätze identifizieren, die in den letzten (x) Tagen keine Daten aufgenommen haben?
* Wie viele Datensätze haben in den letzten (x) Tagen keine Aktualisierungen erhalten?
* Welche Datensätze waren in den letzten (x) Tagen inaktiv?
* Listet Datensätze auf, die in den letzten (x) Tagen keine neuen Batches erhalten haben.
* Wann wurden die Daten zuletzt in den Datensatz (x) aufgenommen?
* Was sind die 10 wichtigsten Datensätze, in die die meisten Daten in den letzten (x) Tagen aufgenommen wurden?
* Welches sind die 10 beliebtesten Datensätze nach Datenvolumen, die in den letzten (x) Tagen aufgenommen wurden?
* Welche 10 Datensätze hatten die größte Datenaufnahme in den letzten (x) Tagen?
* Die 10 Datensätze mit der höchsten Datenaufnahme in den vorherigen (x) Tagen anzeigen.
* Welche Datensätze werden von den Daten am häufigsten in den letzten (x) Tagen empfangen?
* Listet die 10 beliebtesten Datensätze auf, die in den letzten (x) Tagen die meisten Daten aufgenommen haben.
* Wie viele Datensätze wurden in den letzten (y) Tagen im Datensatz (x) empfangen?
* Wie viele Datensätze hat Datensatz (X) in den letzten (Y) Tagen erhalten?
* Wie viele Datensätze wurden in den letzten (y) Tagen für Datensatz (x) aufgenommen?
* Kann die Anzahl der Datensätze angegeben werden, die in den letzten (y) Tagen zum Datensatz (x) hinzugefügt wurden?
* Wie viele Daten hat Datensatz (X) in den letzten (Y) Tagen erhalten?
* Wie viele Datensätze wurden in den vorherigen (y) Tagen für den Datensatz (x) aufgenommen?

+++


## Beispiele für nicht unterstützte Fragen {#unsupported-questions}

Im Folgenden finden Sie eine Liste mit Beispielen für Fragen, die derzeit nicht vom KI-Assistenten unterstützt werden.

+++Auswählen, um Beispiele für nicht unterstützte Fragen anzuzeigen

### Betriebliche Erkenntnisse

* Wie viele Profile in dieser Sandbox leben in Kalifornien? (**Hinweis**: Bei ähnlichen Fragen müssen Sie ein spezifisches Kriterium angeben, um ausreichend Kontext für Ihre Anfrage bereitzustellen. In diesem Fall lautet das spezifische Kriterium „Live in California“.)
* In welchen Segmenten befindet sich dieses Profil {PROFILE_INFO/ATTRIBUTE_VALUE}?
* Wie viele Profile im Datensatz verfügen über eine E-Mail?
* Welcher Datensatz stellt die maximale Anzahl von Profilen in dieser Sandbox dar?
* Welcher Datensatz hat die höchste Anzahl von Datensätzen?
* Wie viele Segmente wurden in {RELATIVE_DATE} gelöscht?
* Welcher meiner Datensätze hat die größte Größe?
* Geben Sie mir ein Profil im {AUDIENCE_NAME}.
* Wie viele Profile gibt es in meiner Sandbox?
* Wie viele Identity-Namespaces sind mit dem Zielgruppen-{AUDIENCE_NAME} verknüpft?
* Bericht mit allen Zielgruppensegmenten anzeigen, die heute ausgewertet wurden
* Wie viele Segmente haben überlappende Profile?
* Anzahl der Batches, die in {DATASET_NAME} geladen werden
* Wie viele aktive Angebote habe ich?
* Wie viele aktive Kampagnen habe ich?
* Woher stammen meine Datenquellen?
* Was ist der größte Datensatz oder die größte Datenquelle?
* Kann ich die Liste der Benutzer abrufen, die diese Schemata erstellt haben?

### Fehlerbehebung

* Warum wird dieser Batch {BATCH_NAME/BATCH_ID} noch verarbeitet?
* Warum qualifiziert sich niemand für diese Zielgruppe {AUDIENCE_NAME}?
* Ich kann die Kunden-KI nicht sehen. Warum und wie kann ich sie beheben?
* Ich kann die Datensatzvorschau nicht sehen. Warum und wie kann ich sie beheben?
* Warum kann ich {SEGMENT/DATASET/SCHEMA_NAME} nicht löschen?
* Habe ich Zugriff auf den Abfrage-Service?

### Aufgaben und Automatisierung

* Schreiben Sie eine Abfrage, die mir einen Datensatz aus dem {DATASET_NAME} gibt.
* Schreiben Sie einen Beispiel-API-Aufruf an /schemas/{schemaId}/fields/{fieldPath}/values.
* Richten Sie eine Quelle/ein Ziel für mich ein.
* Erstellen Sie eine Zielgruppe für mich mit den Kriterien {USER_SPECIFIC_CRITERIA}.

+++

## Nächste Schritte

Durch das Lesen dieses Dokuments wissen Sie jetzt, wie Sie Ihre Fragen für den KI-Assistenten optimieren können. Informationen zur Verwendung der Funktion während Ihrer Workflows finden Sie im Handbuch [Benutzeroberfläche des KI-Assistenten](ui-guide.md).
