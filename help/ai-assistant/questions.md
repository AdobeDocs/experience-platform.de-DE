---
title: Fragenleitfaden für den AI-Assistenten
description: Lesen Sie dieses Dokument, um Beispielfragen zu erfahren, die Sie bei der Abfrage von AI Assistant verwenden können.
source-git-commit: a1092e21940c5e4ba9b598bc51ba1243b57a0051
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 0%

---

# Fragenleitfaden für den AI-Assistenten

Lesen Sie dieses Dokument für eine Reihe von Beispielfragen, die Sie bei der Abfrage des AI-Assistenten verwenden können.

Sie können dieses Dokument auch verwenden, um Tipps zu [So stellen Sie Ihre Fragen](#phrasing-your-questions) , um optimale Antworten von AI Assistant zu erhalten.

## Objektive Fragen {#objectives-questions}

Die folgenden Beispielfragen sind nach Zielen gruppiert, die Sie bei der Verwendung des AI-Assistenten ausführen können:

| Ziel | Beschreibung | Beispiel |
| --- | --- | --- |
| Lernkonzepte und kontinuierliche Workflows | <ul><li>Als neuer Benutzer können Sie mit dem AI-Assistenten Real-Time CDP- und Adobe Journey Optimizer-Konzepte erlernen und sich mit Produkten und Funktionen vertraut machen, mit denen Sie nicht vertraut sind.</li><li>Als erfahrener Benutzer können Sie den AI-Assistenten verwenden, um einen Randfall zu lösen, der Ihren Workflow blockieren könnte. | <ul><li>Wie richte ich ein Dashboard in Journey Analytics ein?</li><li>Erfahren Sie mehr über einige Anwendungsfälle für Real-Time CDP.</li></ul> |
| Fehlerbehebung | Verwenden Sie den KI-Assistenten, um zu erfahren, wie Sie grundlegende Fehler beheben können, die in Ihrem Workflow auftreten können. | <ul><li>Was bewirkt dieser Fehler? {ERROR_MESSAGE} gemein?</li><li>Warum kann ich die Zielgruppe mit dem Namen &quot;Luma: E-Mail-Zielgruppe&quot;nicht löschen?</li></ul> |
| Sandbox-Hygiene | Verwenden Sie den KI-Assistenten, um Duplikate oder nicht verwendete Objekte zu identifizieren, damit Sie Ihre Sandbox effizient verwalten können. | <ul><li>Können Sie mir ähnliche Zielgruppen zeigen?</li><li>Gibt es Schemas, denen kein Datensatz zugeordnet ist?</li></ul> |
| Werteanalyse | Verwenden Sie den KI-Assistenten, um die am häufigsten verwendeten Datenobjekte zu identifizieren und Leistungsindikatoren zu bewerten oder die wertvollsten Datenobjekte zu finden. | <ul><li>Wie viele Profile enthält unsere Segmentdefinition &quot;Luma: E-Mail-Zielgruppe&quot;?</li><li>Wann wurden Zielgruppen für das Experience Cloud Audiences-Ziel aktiviert?</li></ul> |
| Suche | Verwenden Sie den AI-Assistenten, um unterstützte Experience Platform-Objekte wie Zielgruppen, Datensätze, Ziele, Schemas und Quellen zu finden. | <ul><li>Geben Sie die Zielgruppen mit &quot;Luma&quot;im Namen an, die im letzten Quartal erstellt wurden.</li><li>Welche Attribute sind im XDM-Schema &quot;Luma: Benutzerdefinierte Aktionen&quot; enthalten?</li></ul> |
| Folgenabschätzung | Verwenden Sie den KI-Assistenten, um Datenobjekte zu identifizieren, die in bestimmten Workflows verwendet wurden, damit Sie die Auswirkungen von Änderungen bewerten können. | <ul><li>Welche Zielgruppen verwenden `homeAddress.city` im Schema &quot;Luma: PersonProfiles&quot;?</li><li>Welche Datensätze sind die `consents.marketing.push.val` Profilattribut gespeichert in?</li></ul> |

{style="table-layout:auto"}

## Operative Einblicke nach Entitäts- und Produktwissensfragen{#objects-questions}

Die folgenden Fragen werden nach Datenobjekten gruppiert und entweder als [operative Erkenntnisse](./home.md#operational-insights) oder [Produktkenntnis](./home.md#product-knowledge).

| Objekt | Beschreibung |
| --- | --- |
| Zielgruppen - operative Einblicke | <ul><li>Welche Zielgruppen verwenden andere Zielgruppen?</li><li>Wie verteilt sich die Anzahl der Profile auf die Zielgruppen?</li><li>Anzeigen der Zielgruppen, die zuletzt geändert wurden, bevor {RELATIVE_DATE}.</li><li>Welche Zielgruppen haben 0 Profile?</li><li>Is {USE_AUTOCOMPLETE_TO_FILL_AUDIENCE_NAME} in einer anderen Zielgruppe verwendet werden?</li></ul> |
| Attribute - operative Einblicke | <ul><li>Welche Zielgruppen haben ein XDM-Attribut {ATTRIBUTE_PATH} in ihrer Segmentdefinition?</li><li>Wie viele XDM-Schemaattribute werden in keiner Zielgruppe verwendet?</li><li>Welche Schemas haben ein XDM-Attribut {ATTRIBUTE_PATH} in ihnen?</li><li>Welche XDM-Attribute werden aktiviert?</li><li>Welche XDM-Attribute werden in Zielgruppen mit mehr als 10 Profilen verwendet?</li></ul> |
| Datenflüsse - operative Einblicke | <ul><li>Welche Datenflüsse tragen zu {DATASET_NAME} Datensatz?</li><li>Welche Quell-Datenflüsse werden nicht verwendet oder haben keine Daten mehr, die eingehen?</li><li> |
| Datensätze - operative Einblicke | <ul><li>Wie viele Datensätze wurden mit demselben Schema erfasst?</li><li>Welcher Quell-Connector ist mit {DATASET_NAME} Datensatz></li><li>Welche Datensätze werden in den einzelnen Zielgruppen verwendet?</li><li>Welche Schemas werden in keinem Datensatz verwendet?</li><li>Wie viele Datensätze habe ich?</li></ul> |
| Ziele - operative Einblicke | <ul><li>Welche Ziele sind aktiv?</li><li>Für welche Zielkonten sind 0 Zielgruppen aktiviert?</li><li> |
| Journey - operative Einblicke | <ul><li>Wie viele Journey habe ich?</li><li>Welche Journey wurden in erstellt {RELATIVE_DATE} (z. B. letzte Woche) oder {RELATIVE_DATE} (z. B. vor/nach/an einem bestimmten Datum)?</li><li>Zeigen Sie mir die Liste der Journey an, die in {RELATIVE_DATE} (z. B. letzte Woche) oder {RELATIVE_DATE} (z. B. vor/nach/an einem bestimmten Datum)?</li><li>Listet die Journey auf, die ich habe.</li><li>Auflisten der Zielgruppen, die in Live-Journey verwendet werden.</li></ul> |
| Schemas - operative Einblicke | <ul><li>Welche Schemafelder haben zu den meisten Zielgruppen beigetragen?</li><li>Wie viele Schemas sind Profil aktiviert?</li><li>Liste aller in der letzten Woche geänderten Schemata.</li><li>Welche Schemas werden in keinem Datensatz verwendet?</li><li>Liste aller in der letzten Woche erstellten Schemata.</li></ul> |
| Quellen - operative Einblicke | <ul><li>Welche Quellen sind aktiv?</li><li>Welcher Quell-Connector mit Datensatz verknüpft ist {DATASET_NAME}?</li><li>Welcher Quell-Connector weist die höchste Anzahl verknüpfter Konten auf?</li><li>Zeigen Sie mir die Datenflüsse und die zugehörigen Quell-Connectoren.</li></ul> |
| Zielgerichtetes Lernen - Produktwissen (Real-Time CDP und Journey Optimizer) | <ul><li>Worin kann die KI-Assistenzkraft bestehen?</li><li>Was sind Lookalike-Zielgruppen?</li><li>Wie sind Benutzergruppen mit Rollen verbunden?</li><li>Wann sollte ich einen Datentyp oder eine Feldergruppe verwenden?</li><li>Was ist der Unterschied zwischen einer Identität und einem Primärschlüssel oder Fremdschlüssel?</li><li>Wie wird der Reichtum des Profils berechnet?</li></ul> |
| Fehlerbehebung - Produktwissen (Real-Time CDP und Journey Optimizer) | <ul><li>Worin kann die KI-Assistenzkraft bestehen?</li><li>Kann ich ein profilaktiviertes Schema löschen, nachdem Daten erfasst wurden?</li><li>Warum kann ich eine Zielgruppe nicht löschen?</li><li>Wie lange dauert es, bis Zielgruppen ausgewertet und Ergebnisse für die Zielgruppenbestimmung verfügbar sind?</li></ul> |

{style="table-layout:auto"}

## Formulieren Ihrer Fragen {#phrasing-your-questions}

Sie müssen Ihre Fragen an den KI-Assistenten mit Klarheit und Kontext formulieren, um eine möglichst genaue Antwort zu erhalten. In der folgenden Liste finden Sie Hinweise dazu, wie Sie eine klare Frage mit Kontext stellen:

* Geben Sie Ihre Aufgabe und/oder Frage kurz an.
* Vermeiden Sie mehrdeutige oder zu komplexe Syntax, um das Verständnis zu erleichtern.
* Stellen Sie relevanten Kontext zu Ihrer Aufgabe und/oder Frage bereit, da der Kontext AI Assistant bei der Generierung relevanterer Antworten unterstützen kann.

In den folgenden Tabellen finden Sie weitere Anleitungen zu Best Practices, die Sie bei Fragen an den AI-Assistenten befolgen können.

In den folgenden Tabellen finden Sie Best Practices, die Sie bei der Verwendung des AI-Assistenten befolgen können:

| Do | Beispiel |
| --- | --- |
| <ul><li>Seien Sie spezifisch hinsichtlich des Objekts oder der Informationen, die Sie abrufen oder analysieren möchten.</li><li>Versuchen Sie, Ihre Datenobjektnamen in Anführungszeichen zu setzen. Wenn Sie nur einen Teil des Objektnamens kennen, können Sie dies auch in der Frage angeben.</li><li>Verwendung [Objekt automatisch vervollständigen](./ui-guide.md#use-auto-complete) um AI Assistant dabei zu unterstützen, den Kontext Ihrer Abfrage besser zu verstehen.</li></ul> | <ul><li>Welche Datensätze verwenden das Schema &quot;Luma - Loyalität&quot;?</li><li>Zeigen Sie mir die aktivierten Segmente, deren Namen &quot;Luma&quot;enthalten. Ordnen Sie sie nach Anzahl der Profile.</li></ul> |
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

## Nächste Schritte

Durch Lesen dieses Dokuments können Sie jetzt Ihre Fragen für AI Assistant optimieren. Informationen zur Verwendung der Funktion während Ihrer Workflows finden Sie im Abschnitt [Handbuch zur Benutzeroberfläche des AI-Assistenten](ui-guide.md).
