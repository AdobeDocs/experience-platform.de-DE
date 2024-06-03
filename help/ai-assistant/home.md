---
title: KI-Assistent in Adobe Experience Platform - Überblick
description: Erfahren Sie mehr über den KI-Assistenten, seine Funktionen und Anwendungsbeispiele sowie darüber, wie Sie damit Ihren Workflow mit Adobe Experience Platform und Real-time Customer Data Platform beschleunigen können.
hide: true
hidefromtoc: true
source-git-commit: fe87a487079f5154f238b2d425cdd249a4724762
workflow-type: tm+mt
source-wordcount: '2294'
ht-degree: 1%

---

# KI-Assistent in Adobe Experience Platform

Lesen Sie dieses Dokument, um mehr über AI Assistant in Adobe Experience Platform zu erfahren.

AI Assistant in Adobe Experience Platform ist eine Dialogerfahrung, mit der Sie Ihre Workflows in Adobe-Applikationen beschleunigen können. Sie können den AI-Assistenten verwenden, um Produktwissen besser zu verstehen, Probleme zu beheben oder Informationen zu durchsuchen und operative Einblicke zu erhalten. Der AI-Assistent unterstützt Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer und Customer Journey Analytics.

>[!IMPORTANT]
>
>* Sie müssen zustimmen, [eine Benutzervereinbarung](https://adobe.sharepoint.com/:w:/s/ExCUserExperience/EVzJv1jFBiZGnaFEufsfIqwBC_9ehv3KaXTkEMTGpQFRpg?e=qzwOo8) bevor Sie den KI-Assistenten verwenden können. Die Nutzervereinbarung enthält auch die öffentliche Betavereinbarung. Dies ist erforderlich, damit Sie zusätzliche Funktionen des KI-Assistenten verwenden können, wenn sie als Beta-Version eingeführt werden.

![Die Benutzeroberfläche des AI-Assistenten mit dem ersten ausgelösten Benutzererlebnis.](./images/blank.png)

## Grundlegendes zum KI-Assistenten {#understanding-ai-assistant}

Der KI-Assistent antwortet auf Ihre gestellten Fragen, indem er eine Datenbank abfragt und dann Daten aus der Datenbank in eine für Menschen lesbare Antwort übersetzt.

Diese interne Darstellung der zugrunde liegenden Daten wird auch als **[!DNL Knowledge Graph]** - ein umfassendes Netz von Konzepten, Daten und Metadaten für eine gegebene Antwort.

Die [!DNL Knowledge Graph] besteht aus Unterdiagrammen, die bei jeder Übermittlung von Abfragen referenziert werden:

* Betriebliche Einblicke des Kunden.
* Betriebliche Einblicke des Kunden in verschiedene Meta-Stores.
* Experience League.

Vor der Abfrage des AI-Assistenten müssen zwei Frageklassen beachtet werden:

### Produktwissen {#product-knowledge}

Produktkenntnis bezieht sich auf Konzepte und Themen, die auf der Experience League-Dokumentation basieren. Produktwissensfragen können in die folgenden Untergruppen weiter spezifiziert werden:

| Produktwissen | Beispiele |
| --- | --- |
| Zielgerichtetes Lernen | <ul><li>Was ist der Unterschied zwischen einer Identität und einem Primärschlüssel oder Fremdschlüssel?</li><li>Wie wird der Reichtum des Profils berechnet?</li></ul> |
| Offene Entdeckung | <ul><li>Wie kann ich diesen Datensatz exportieren?</li><li>Gibt es Schemata für Kunden im Gesundheitswesen?</li></ul> |
| Fehlerbehebung | <ul><li>Warum kann ich ein Schema, das im Besitz von Adobe ist, nicht für ein Profil aktivieren?</li><li>Warum kann ich ein Segment nicht löschen?</li></ul> |

{style="table-layout:auto"}

### Operative Einblicke {#operational-insights}

>[!IMPORTANT]
>
>Die Antworten auf operative Einblicke befinden sich in der Beta-Phase. Jeder, der Zugriff auf die **Anzeigen operativer Einblicke** -Berechtigung Zugriff auf betriebliche Einblicke erhalten.

Operative Einblicke beziehen sich auf Antworten, die der KI-Assistent über Ihre Metadatendatenobjekte (Attribute, Zielgruppen, Datenflüsse, Datensätze, Ziele, Journey, Schemas und Quellen) generiert, einschließlich Zählungen, Suchen und Auswirkungen auf die Herkunft. Es werden keine Daten innerhalb der Sandbox angezeigt.

* Wie viele Datensätze habe ich?
* Wie viele Schemaattribute wurden noch nie verwendet?
* Welche Zielgruppen wurden aktiviert?

Sie können in den folgenden Bereichen Fragen zu Ihren operativen Einblicken an den KI-Assistenten stellen:

* Attribute
* Zielgruppen
* Datenflüsse
* Datensätze
* Ziele _(Fragen zu Konten und einige Fragen zum Datenfluss können derzeit nicht beantwortet werden.)_
* Journeys
* Schemas _(Fragen zu Feldergruppen können derzeit nicht beantwortet werden.)_
* Quellen _(Fragen zu den Rechnungsabschlüssen können derzeit nicht beantwortet werden.)_

Bei Fragen zu operativen Einblicken spiegeln die Antworten möglicherweise nicht den aktuellen Status der Benutzeroberfläche wider. Die Daten, die diese Fragen unterstützen, werden alle 24 Stunden aktualisiert. Beispielsweise werden Änderungen, die Benutzer tagsüber in Real-Time CDP vornehmen, mit den Datenspeichern nachts synchronisiert und stehen dann morgens für Benutzerfragen zur Verfügung. Sie müssen sich bei einer Sandbox anmelden, um sich über bestimmte Daten zu Objekten zu informieren.

## Funktionszugriff {#feature-access}

Der Zugriff auf den AI-Assistenten wird durch die folgenden Parameter gesteuert:

* **Zugriff auf die Anwendung:** Sie können auf den KI-Assistenten in Adobe Experience Platform, Adobe Real-Time CDP, Adobe Journey Optimizer und [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).
* **Vertraglicher Zugang:** Ihr Unternehmen muss bestimmten [!DNL GenAI]-zugehörige rechtliche Begriffe, bevor Ihr Unternehmen den KI-Assistenten verwenden kann. Wenden Sie sich an den Administrator Ihres Unternehmens oder an Ihr Adobe Account-Team, wenn Sie nicht auf den AI-Assistenten zugreifen können.
* **Berechtigungen:** Verwenden Sie die [Berechtigungs-Benutzeroberfläche](../access-control/abac/ui/permissions.md) , um den Zugriff auf AI Assistant in Ihrer Organisation zu gewähren oder zu widerrufen. Um den AI-Assistenten verwenden zu können, muss ein bestimmter Benutzer einer Rolle angehören, die mit dem **Aktivieren des KI-Assistenten** und **Anzeigen operativer Einblicke** Berechtigungen.
   * Als Administrator können Sie die **Aktivieren des KI-Assistenten** einer bestimmten Rolle zuweisen und dieser Rolle einen Benutzer hinzufügen, damit er in Ihrem Unternehmen auf den KI-Assistenten zugreifen kann.
   * Als Administrator können Sie die **Anzeigen operativer Einblicke** zu einer bestimmten Rolle hinzufügen und dieser Rolle einen Benutzer hinzufügen, damit er die operativen Einblicke des AI-Assistenten verwenden kann. Betriebliche Einblicke befinden sich derzeit in der Beta-Phase.

![Die Berechtigungs-UI-Seite mit den Berechtigungen &quot;Enable AI Assistant&quot;und &quot;View Operations Insights&quot;, die in einer bestimmten Rolle enthalten sind.](./images/permissions.png)

## Beispielfragen {#example-questions}

In diesem Abschnitt werden Beispielfragen beschrieben, auf die Sie während Ihrer Workflows verweisen können. Die Fragen sind in drei Abschnitte unterteilt: operative Einblicke, Ziele und Objekte.

### Beispielfragen, gruppiert nach operativen Einblicken {#operational-insights-questions}

+++Auswählen , um Beispiele für betriebliche Insight-Fragen und die entsprechenden Anwendungsfälle anzuzeigen:

| Fragetyp | Anwendungsfall | Beispiele |
| --- | --- | --- | 
| Datenherkunft | Verwendung eines oder mehrerer Objekte über andere Experience Platform-Objekte hinweg verfolgen | <ul><li>Welche Datensätze verwenden das Schema &quot;ACME schema&quot;?</li><li>Wie viele Datensätze wurden mit demselben Schema erfasst?</li><li>Welche Datensätze wurden in aktivierten Zielgruppen verwendet?</li><li>Listen Sie die Schemas auf, deren Attribute in aktivierten Zielgruppen verwendet werden.</li><li>Zeigen Sie die Zielgruppen an, die für &quot;ACME Destinations&quot;aktiviert sind und mehr als 1000 Profile haben.</li><li>Zeigen Sie mir die Attribute an, die in den aktivierten Zielgruppen verwendet werden, die nach Januar 2023 geändert wurden.</li><li>Welche Datensätze werden über die Quelle &quot;ACME Amazon S3&quot;erfasst?</li><li>Welche Datenflüsse sind mit &quot;ACME Loyalty Dataflow&quot;verknüpft?</li><li>Listen Sie die Schemata auf, die für aktivierte Zielgruppen erstellt wurden und im letzten 1 Jahr erstellt wurden.</li></ul> |
| Verteilung und Aggregationen | Zusammenfassende Fragen zur Verwendung von Experience Platform-Objekten | <ul><li>Wie hoch ist der Prozentsatz der aktivierten Zielgruppen?</li><li>Wie viele Felder werden in der Segmentierung verwendet?</li><li>Welche Zielgruppen werden für die meisten Ziele aktiviert?</li><li>Listen Sie doppelte Zielgruppen auf.</li><li>Zeigen Sie mir die für &quot;ACME Destinations&quot;aktivierten Zielgruppen an und ordnen Sie sie nach Profilgröße an.</li><li>Wie hoch ist der Prozentsatz der Zielgruppen, die nicht aktiviert wurden, aber über mehr als 100 Profile verfügen. Zeigen Sie mir ihre Namen.</li><li>Geben Sie die 3 Quell-Connectoren an, die Daten in meine Datensätze aufnehmen.</li><li>Geben Sie die fünf wichtigsten Attribute an, die in aktivierten Zielgruppen basierend auf ihrem Vorkommen verwendet werden.</li></ul> |
| Objektsuche | Rufen Sie ein Experience Platform-Objekt oder dessen Eigenschaften ab oder greifen Sie darauf zu. | <ul><li>Welche Datensätze sind mit keinem Schema verknüpft?</li><li>Geben Sie die Attribute an, die für &quot;ACME Audience&quot;verwendet werden?</li><li>Geben Sie mir die Liste der Schemas an, für die Profil aktiviert, aber seit ihrer Erstellung nicht geändert wurde.</li><li>Welche Zielgruppen wurden in der letzten Woche geändert?</li><li>Geben Sie die Zielgruppen an, die über dieselben Segmentdefinitionen und deren Erstellungsdatum verfügen.</li><li>Welche Datensätze sind profilaktiviert und enthalten auch die Anzahl der Zielgruppen, die aus jedem Datensatz erstellt wurden.</li><li>Welche Quellkonten sind mit dem Datensatz XYZ verknüpft?</li><li>Zeigen Sie mir die Segmentdefinition und das Änderungsdatum von &quot;ACME Audience&quot;an.</li></ul> |
| Objektvergleich | Identifizierung doppelter Zielgruppen. | <ul><li>Führen Sie basierend auf der Segmentdefinition die Zielgruppen auf, die Dubletten sind.</li><li>Welche doppelten Zielgruppen werden für &quot;ACME Destinations&quot;aktiviert.</li></ul> |

{style="table-layout:auto"}

+++

### Beispielfragen, nach Zielen gruppiert {#objectives-questions}

+++Auswählen, um eine Liste der Ziele anzuzeigen, die Sie mit dem KI-Assistenten erreichen können

| Ziel | Beschreibung | Beispiel |
| --- | --- | --- |
| Lernkonzepte und kontinuierliche Workflows | <ul><li>Als neuer Benutzer können Sie mit dem AI-Assistenten Real-Time CDP- und Adobe Journey Optimizer-Konzepte erlernen und sich mit Produkten und Funktionen vertraut machen, mit denen Sie nicht vertraut sind.</li><li>Als erfahrener Benutzer können Sie den AI-Assistenten verwenden, um einen Randfall zu lösen, der Ihren Workflow blockieren könnte. | <ul><li>Wie richte ich ein Dashboard in Journey Analytics ein?</li><li>Erfahren Sie mehr über einige Anwendungsfälle für Real-Time CDP.</li></ul> |
| Fehlerbehebung | Verwenden Sie den KI-Assistenten, um zu erfahren, wie Sie grundlegende Fehler beheben können, die in Ihrem Workflow auftreten können. | <ul><li>Was bewirkt dieser Fehler? {ERROR_MESSAGE} gemein?</li><li>Warum kann ich die Zielgruppe mit dem Namen &quot;Luma: E-Mail-Zielgruppe&quot;nicht löschen?</li></ul> |
| Sandbox-Hygiene | Verwenden Sie den KI-Assistenten, um Duplikate oder nicht verwendete Objekte zu identifizieren, damit Sie Ihre Sandbox effizient verwalten können. | <ul><li>Können Sie mir ähnliche Zielgruppen zeigen?</li><li>Gibt es Schemas, denen kein Datensatz zugeordnet ist?</li></ul> |
| Werteanalyse | Verwenden Sie den KI-Assistenten, um die am häufigsten verwendeten Datenobjekte zu identifizieren und Leistungsindikatoren zu bewerten oder die wertvollsten Datenobjekte zu finden. | <ul><li>Wie viele Profile enthält unsere Segmentdefinition &quot;Luma: E-Mail-Zielgruppe&quot;?</li><li>Wann wurden Zielgruppen für das Experience Cloud Audiences-Ziel aktiviert?</li></ul> |
| Suche | Verwenden Sie den AI-Assistenten, um unterstützte Experience Platform-Objekte wie Zielgruppen, Datensätze, Ziele, Schemas und Quellen zu finden. | <ul><li>Geben Sie die Zielgruppen mit &quot;Luma&quot;im Namen an, die im letzten Quartal erstellt wurden.</li><li>Welche Attribute sind im XDM-Schema &quot;Luma: Benutzerdefinierte Aktionen&quot; enthalten?</li></ul> |
| Folgenabschätzung | Verwenden Sie den KI-Assistenten, um Datenobjekte zu identifizieren, die in bestimmten Workflows verwendet wurden, damit Sie die Auswirkungen von Änderungen bewerten können. | <ul><li>Welche Zielgruppen verwenden `homeAddress.city` im Schema &quot;Luma: PersonProfiles&quot;?</li><li>Welche Datensätze sind die `consents.marketing.push.val` Profilattribut gespeichert in?</li></ul> |

{style="table-layout:auto"}

+++

### Beispielfragen, gruppiert nach Objekten {#objects-questions}

+++Auswählen, um eine Liste mit Beispielfragen anzuzeigen, die der KI-Assistent Ihnen bei Folgendem helfen kann:

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

+++

## Formulieren Ihrer Fragen {#phrasing-your-questions}

Sie müssen Ihre Fragen an den KI-Assistenten mit Klarheit und Kontext formulieren, um eine möglichst genaue Antwort zu erhalten. In der folgenden Liste finden Sie Hinweise dazu, wie Sie eine klare Frage mit Kontext stellen:

* Geben Sie Ihre Aufgabe und/oder Frage kurz an.
* Vermeiden Sie mehrdeutige oder zu komplexe Syntax, um das Verständnis zu erleichtern.
* Stellen Sie relevanten Kontext zu Ihrer Aufgabe und/oder Frage bereit, da der Kontext AI Assistant bei der Generierung relevanterer Antworten unterstützen kann.

In den folgenden Tabellen finden Sie weitere Anleitungen zu Best Practices, die Sie bei Fragen an den AI-Assistenten befolgen können.

+++Auswählen , um Beispiele für Best Practices anzuzeigen, die bei der Formulierung Ihrer Fragen befolgt werden sollen

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

+++

## Nächste Schritte

Da Sie nun über allgemeine Kenntnisse im Bereich KI-Assistenzkraft verfügen, können Sie jetzt fortfahren und KI-Assistenzkräfte während Ihrer Workflows verwenden. Weiterführende Informationen finden Sie in der folgenden Dokumentation:

* [Handbuch zur Benutzeroberfläche des AI-Assistenten](./ui-guide.md)
* [Datenschutz, Sicherheit und Governance im KI-Assistenten](./privacy.md)
* [Häufig gestellte Fragen](./faq.md)