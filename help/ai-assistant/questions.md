---
title: Fragenleitfaden für den AI-Assistenten
description: Lesen Sie dieses Dokument, um Beispielfragen zu erfahren, die Sie bei der Abfrage von AI Assistant verwenden können.
exl-id: d16d1262-cc2d-45c9-94c4-b86132183442
source-git-commit: 196a39edd493dcc8296f4b6d2904393dd6f6cdd4
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 1%

---

# Fragenleitfaden für den AI-Assistenten

Lesen Sie dieses Dokument für eine Reihe von Beispielfragen, die Sie bei der Abfrage des AI-Assistenten verwenden können.

Sie können dieses Dokument auch verwenden, um Tipps zu [finden, wie Sie Ihre Fragen stellen](#phrasing-your-questions), um optimale Antworten von AI Assistant zu erhalten.

## Objektive Fragen {#objectives-questions}

Die folgenden Beispielfragen sind nach Zielen gruppiert, die Sie bei der Verwendung des AI-Assistenten ausführen können:

| Ziel | Beschreibung | Beispiel |
| --- | --- | --- |
| Lernkonzepte und kontinuierliche Workflows | <ul><li>Als neuer Benutzer können Sie mit dem AI-Assistenten Real-Time CDP- und Adobe Journey Optimizer-Konzepte erlernen und sich mit Produkten und Funktionen vertraut machen, mit denen Sie nicht vertraut sind.</li><li>Als erfahrener Benutzer können Sie den AI-Assistenten verwenden, um einen Randfall zu lösen, der Ihren Workflow blockieren könnte. | <ul><li>Wie richte ich ein Dashboard in Journey Analytics ein?</li><li>Erfahren Sie mehr über einige Anwendungsfälle für Real-Time CDP.</li></ul> |
| Fehlerbehebung | Verwenden Sie den KI-Assistenten, um zu erfahren, wie Sie grundlegende Fehler beheben können, die in Ihrem Workflow auftreten können. | <ul><li>Was bedeutet dieser Fehler {ERROR_MESSAGE}?</li><li>Warum kann ich die Zielgruppe mit dem Namen &quot;Luma: E-Mail-Zielgruppe&quot;nicht löschen?</li></ul> |
| Sandbox-Hygiene | Verwenden Sie den KI-Assistenten, um Duplikate oder nicht verwendete Objekte zu identifizieren, damit Sie Ihre Sandbox effizient verwalten können. | <ul><li>Können Sie mir ähnliche Zielgruppen zeigen?</li><li>Gibt es Schemas, denen kein Datensatz zugeordnet ist?</li></ul> |
| Werteanalyse | Verwenden Sie den KI-Assistenten, um die am häufigsten verwendeten Datenobjekte zu identifizieren und Leistungsindikatoren zu bewerten oder die wertvollsten Datenobjekte zu finden. | <ul><li>Wie viele Profile enthält unsere Segmentdefinition &quot;Luma: E-Mail-Zielgruppe&quot;?</li><li>Wann wurden Zielgruppen für das Experience Cloud Audiences-Ziel aktiviert?</li></ul> |
| Suche | Verwenden Sie den AI-Assistenten, um unterstützte Experience Platform-Objekte wie Zielgruppen, Datensätze, Ziele, Schemas und Quellen zu finden. | <ul><li>Geben Sie die Zielgruppen mit &quot;Luma&quot;im Namen an, die im letzten Quartal erstellt wurden.</li><li>Welche Attribute sind im XDM-Schema &quot;Luma: Benutzerdefinierte Aktionen&quot; enthalten?</li></ul> |
| Folgenabschätzung | Verwenden Sie den KI-Assistenten, um Datenobjekte zu identifizieren, die in bestimmten Workflows verwendet wurden, damit Sie die Auswirkungen von Änderungen bewerten können. | <ul><li>Welche Zielgruppen verwenden `homeAddress.city` im Schema &quot;Luma: PersonProfiles&quot;?</li><li>In welchen Datensätzen ist das Profilattribut &quot;`consents.marketing.push.val`&quot; gespeichert?</li></ul> |

{style="table-layout:auto"}

## Operative Einblicke nach Entitäts- und Produktwissensfragen{#objects-questions}

Die folgenden Fragen werden nach Datenobjekten gruppiert und entweder als [operative Einblicke](./home.md#operational-insights) oder als [Produktkenntnis](./home.md#product-knowledge) klassifiziert.

* **Zielgruppen - operative Einblicke**
   * Welche Zielgruppen verwenden andere Zielgruppen?
   * Wie verteilt sich die Anzahl der Profile auf die Zielgruppen?
   * Zeigt Zielgruppen an, die zuletzt vor {RELATIVE_DATE} geändert wurden.
   * Welche Zielgruppen haben 0 Profile?
   * Wird {USE_AUTO_COMPLETE_TO_FILL_AUDIENCE_NAME} in anderen Zielgruppen verwendet?
* **Attribute - operative Einblicke**
   * Welche Zielgruppen haben in ihrer Segmentdefinition das XDM-Attribut {ATTRIBUTE_PATH}?
   * Wie viele XDM-Schemaattribute werden in keiner Zielgruppe verwendet?
   * Welche Schemas enthalten das xdm-Attribut {ATTRIBUTE_PATH}?
   * Welche XDM-Attribute werden aktiviert?
   * Welche XDM-Attribute werden in Zielgruppen mit mehr als 10 Profilen verwendet?
* **Datenflüsse - operative Einblicke**
   * Welche Datenflüsse tragen zum {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} -Datensatz bei?
   * Welche Quell-Datenflüsse werden nicht verwendet oder haben keine Daten mehr, die eingehen?
   * Geben Sie die Quell-Datenflüsse an, die ich habe.
   * Welche Datenflüsse sind für jeden Quell-Connector konfiguriert?
* **Datensätze - operative Einblicke**
   * Wie viele Datensätze wurden mit demselben Schema erfasst?
   * Welcher Quell-Connector ist mit dem {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} -Datensatz verknüpft?
   * Welche Datensätze werden in den einzelnen Zielgruppen verwendet?
   * Welche Schemas werden in keinem Datensatz verwendet?
   * Wie viele Datensätze habe ich?
* **Ziele - operative Einblicke**
   * Welche Ziele sind aktiv?
   * Für welche Zielkonten sind 0 Zielgruppen aktiviert?
   * Wie viele Zielgruppen werden für jedes Ziel aktiviert?
   * Welche Ziele haben die höchste Anzahl an aktivierten Zielgruppen?
* **Journey - Operative Einblicke**
   * Wie viele Journey habe ich?
   * Welche Journey wurden in {RELATIVE_DATE} (z. B. der letzten Woche) oder {RELATIVE_DATE} (z. B. vor/nach/an einem bestimmten Datum) erstellt?
   * Zeigen Sie mir die Liste der Journey, die in {RELATIVE_DATE} (z. B. der letzten Woche) oder {RELATIVE_DATE} (z. B. vor/nach/an einem bestimmten Datum) geändert wurden?
   * Listet die Live-Journey auf, die ich habe.
   * Auflisten der Zielgruppen, die in Live-Journey verwendet werden.
* **Quellen - operative Einblicke**
   * Welche Quellen sind aktiv?
   * Welcher Quell-Connector mit Datensatz {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} verknüpft ist.
   * Welcher Quell-Connector weist die höchste Anzahl verknüpfter Konten auf?
   * Zeigen Sie mir die Datenflüsse und die zugehörigen Quell-Connectoren.
* **Gezieltes Lernen - Produktwissen (Real-Time CDP und Journey Optimizer)**
   * Was sind Lookalike-Zielgruppen?
   * Wie sind Benutzergruppen mit Rollen verbunden?
   * Wann sollte ich einen Datentyp oder eine Feldergruppe verwenden?
   * Was ist der Unterschied zwischen einer Identität und einem Primärschlüssel oder Fremdschlüssel?
   * Wie wird der Reichtum des Profils berechnet?
* **Fehlerbehebung - Produktwissen (Real-Time CDP und Journey Optimizer)**
   * Wobei kann der KI-Assistent helfen?
   * Kann ich ein Profil-aktiviertes Schema löschen, nachdem Daten erfasst wurden?
   * Warum kann ich eine Zielgruppe nicht löschen?
   * Wie lange dauert es, bis Zielgruppen ausgewertet und Ergebnisse für die Zielgruppenbestimmung verfügbar sind?

## Formulieren Ihrer Fragen {#phrasing-your-questions}

Sie müssen Ihre Fragen an den KI-Assistenten mit Klarheit und Kontext formulieren, um eine möglichst genaue Antwort zu erhalten. In der folgenden Liste finden Sie Hinweise dazu, wie Sie eine klare Frage mit Kontext stellen:

* Geben Sie Ihre Aufgabe und/oder Frage kurz an.
* Vermeiden Sie mehrdeutige oder zu komplexe Syntax, um das Verständnis zu erleichtern.
* Stellen Sie relevanten Kontext zu Ihrer Aufgabe und/oder Frage bereit, da der Kontext AI Assistant bei der Generierung relevanterer Antworten unterstützen kann.

In den folgenden Tabellen finden Sie weitere Anleitungen zu Best Practices, die Sie bei Fragen an den AI-Assistenten befolgen können.

In den folgenden Tabellen finden Sie Best Practices, die Sie bei der Verwendung des AI-Assistenten befolgen können:

| Do | Beispiel |
| --- | --- |
| <ul><li>Seien Sie spezifisch hinsichtlich des Objekts oder der Informationen, die Sie abrufen oder analysieren möchten.</li><li>Versuchen Sie, Ihre Datenobjektnamen in Anführungszeichen zu setzen. Wenn Sie nur einen Teil des Objektnamens kennen, können Sie dies auch in der Frage angeben.</li><li>Verwenden Sie die Funktion [Automatische Objektvervollständigung](./ui-guide.md#use-auto-complete), um AI Assistant dabei zu unterstützen, den Kontext Ihrer Abfrage besser zu verstehen.</li></ul> | <ul><li>Welche Datensätze verwenden das Schema &quot;Luma - Loyalität&quot;?</li><li>Zeigen Sie mir die aktivierten Segmente, deren Namen &quot;Luma&quot;enthalten. Ordnen Sie sie nach Anzahl der Profile.</li></ul> |
| <ul><li>Vermeiden Sie Mehrdeutigkeit und verwenden Sie klare Sprache</li><li>Verwenden Sie präzise Terminologie, um eine bessere Übersichtlichkeit in Ihrer Abfrage sicherzustellen.</li><li>Versuchen Sie bei Fragen zu Adobe Experience Platform, die Experience Platform-spezifische Terminologie zu verwenden, um die Relevanz der Antworten zu verbessern.</li></ul> | <ul><li>Wie viele Profile habe ich in &quot;ACME Audience&quot;.</li><li>Zeigen Sie mir die fünf wichtigsten XDM-Attribute, die in aktivierten Zielgruppen verwendet werden.</li></ul> |
| <ul><li>Geben Sie einen Kontext oder ein Kriterium zum Filtern Ihrer Ergebnisse an.</li><li>Verwenden Sie ein Filterkriterium in den Fragen, um das Datenvolumen in der Antwort zu begrenzen.</li></ul> | <ul><li>Zeigen Sie Zielgruppen an, die nicht aktiviert wurden und vor mehr als 6 Monaten erstellt wurden und noch nie geändert wurden.</li><li>Zeigen Sie mir Zielgruppen an, die für &quot;ACME Destination&quot;aktiviert sind und mehr als 10000 Profile aufweisen.</li></ul> |

{style="table-layout:auto"}

| Don&#39;t | Beispiel |
| --- | --- |
| Verwenden Sie eine vage oder mehrdeutige Sprache. | <ul><li>Geben Sie mir Informationen zu Datensätzen.</li><li>Wie viele Benutzer habe ich in &quot;ACME Audience&quot;?</li><li>Segmente anzeigen.</li><li>Listenattribute.</li></ul> |
| Unvollständige Anforderungen stellen. | &quot;Luma - Loyalitätsdatensatz&quot; |
| Vermutlich Wissen ohne Kontext. | <ul><li>Zielgruppen in den letzten 6 Monaten.</li><li>Erstellen Sie eine Abfrage für mich.</li></ul> |
| Formulieren Sie zu komplexe Abfragen. | Stellen Sie eine umfassende Analyse der Datenherkunft über alle Objekte und deren Abhängigkeiten hinweg bereit. |
| Kriterien oder Parameter auslassen. | Zeigen Sie mir Datensätze an. |

{style="table-layout:auto"}

## Beispiele für nicht unterstützte Fragen {#unsupported-questions}

Im Folgenden finden Sie eine Liste von Beispielen für Fragen, die derzeit nicht von AI Assistant unterstützt werden.

+++Auswählen, um Beispiele für nicht unterstützte Fragen anzuzeigen

### Betriebliche Erkenntnisse

* Wie viele Profile in dieser Sandbox leben in Kalifornien? (**Hinweis**: Für ähnliche Fragen müssen Sie ein bestimmtes Kriterium angeben, um genügend Kontext für Ihre Anfrage bereitzustellen. In diesem Fall lautet das spezifische Kriterium &quot;Live in Kalifornien&quot;).
* In welchen Segmenten befindet sich dieses Profil {PROFILE_INFO/ATTRIBUTE_VALUE}?
* Wie viele Profile im Datensatz haben eine E-Mail?
* Welcher Datensatz stellt eine maximale Anzahl von Profilen in dieser Sandbox dar?
* Welcher Datensatz weist die höchste Anzahl von Datensätzen auf?
* Wie viele Segmente wurden in {RELATIVE_DATE} gelöscht?
* Welcher meiner Datensätze hat die größte Größe?
* Geben Sie mir ein Profil in der {AUDIENCE_NAME}.
* Wie viele Profile hat meine Sandbox insgesamt?
* Wie viele Identitäts-Namespaces sind mit der Zielgruppe {AUDIENCE_NAME} verknüpft?
* Anzeigen eines Berichts aller Zielgruppensegmente, die heute ausgewertet wurden
* Wie viele Segmente haben sich überschneidende Profile?
* Wie viele Batches in {DATASET_NAME} geladen werden
* Wie viele aktive Angebote habe ich?
* Wie viele aktive Kampagnen habe ich?
* Woher stammen meine Datenquellen?
* Was ist der größte Datensatz oder die größte Datenquelle?
* Kann ich die Liste der Benutzer erhalten, die diese Schemas erstellt haben?

### Fehlerbehebung

* Warum wird dieser Batch {BATCH_NAME/BATCH_ID} noch verarbeitet?
* Warum qualifiziert sich niemand für diese Zielgruppe {AUDIENCE_NAME}?
* Ich kann Customer AI nicht sehen, warum und wie kann ich es beheben?
* Ich kann die Datensatzvorschau nicht sehen, warum und wie kann ich sie reparieren?
* Warum kann ich {SEGMENT/DATASET/SCHEMA_NAME} nicht löschen?
* Habe ich Zugriff auf Query Service?

### Aufgaben und Automatisierung

* Schreiben Sie eine Abfrage, die mir einen Datensatz aus dem {DATASET_NAME} gibt.
* Schreiben Sie einen Beispiel-API-Aufruf an /schemas/{schemaId}/fields/{fieldPath}/values.
* Richten Sie eine Quelle/ein Ziel für mich ein.
* Erstellen Sie eine Zielgruppe für mich mit den Kriterien {USER_SPECIFIC_CRITERIA}.

+++

## Nächste Schritte

Durch Lesen dieses Dokuments können Sie jetzt Ihre Fragen für AI Assistant optimieren. Informationen zur Verwendung der Funktion während Ihrer Workflows finden Sie im Handbuch [AI Assistant UI Guide](ui-guide.md).
