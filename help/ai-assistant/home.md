---
title: KI-Assistent in Adobe Experience Platform - Übersicht
description: Erfahren Sie mehr über den KI-Assistenten, seine Funktionen und Anwendungsbeispiele sowie darüber, wie Sie damit Ihren Workflow mit Adobe Experience Platform und Real-time Customer Data Platform beschleunigen können.
exl-id: cfd4ac22-fff3-4b50-bbc2-85b6328f603c
source-git-commit: e90333d09585c8aa0ef176dcfc4717e86364fd54
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 9%

---

# KI-Assistent in Adobe Experience Platform

Das folgende Video soll Ihnen dabei helfen, KI-Assistent zu verstehen.

>[!VIDEO](https://video.tv.adobe.com/v/3429845?learn=on)

Lesen Sie dieses Dokument, um mehr über den KI-Assistenten in Adobe Experience Platform zu erfahren.

Der KI-Assistent in Adobe Experience Platform ist ein Gesprächserlebnis, mit dem Sie Ihre Workflows in Adobe-Anwendungen beschleunigen können. Sie können den KI-Assistenten verwenden, um Produktkenntnisse besser zu verstehen, Probleme zu beheben oder Informationen zu durchsuchen und betriebliche Erkenntnisse zu gewinnen. Der KI-Assistent unterstützt Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer und Customer Journey Analytics.

![Die Benutzeroberfläche des KI-Assistenten mit dem ausgelösten erstmaligen Benutzererlebnis.](./images/ai-assistant-full.png)

>[!IMPORTANT]
>
>Sie müssen einer [Benutzervereinbarung“ zustimmen](https://www.adobe.com/de/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html) bevor Sie den KI-Assistenten verwenden können. Die Benutzervereinbarung enthält auch die öffentliche Beta-Vereinbarung. Dies dient dazu, dass Sie zusätzliche KI-Assistenten-Funktionen verwenden können, während sie in einer Beta-Funktion eingeführt werden.

+++Auswählen, um die Benutzeroberfläche für Benutzervereinbarungen anzuzeigen

![Die erste Seite der Benutzervereinbarung.](./images/user-agreement-1.png)

![Die letzte Seite der Benutzervereinbarung.](./images/user-agreement-2.png)

+++

## Grundlagen zum KI-Assistenten {#understanding-ai-assistant}

Der KI-Assistent antwortet auf Ihre gesendeten Fragen, indem er eine Datenbank abfragt und dann Daten aus der Datenbank in eine für Menschen lesbare Antwort übersetzt.

Diese interne Darstellung der zugrunde liegenden Daten wird auch als **[!DNL Knowledge Graph]** bezeichnet - ein umfassendes Web von Konzepten, Daten und Metadaten für eine bestimmte Antwort.

Die [!DNL Knowledge Graph] besteht aus Unterdiagrammen, die bei jeder Übermittlung von Abfragen referenziert werden:

* Betriebsbezogene Einblicke des Kunden.
* Einblicke in den Betrieb von Kunden in verschiedenen Meta-Stores.
* Dokumentation zu Experience League.

Es gibt zwei Klassen von Fragen, die vor der Abfrage des KI-Assistenten zu berücksichtigen sind:

### Produktkenntnisse {#product-knowledge}

Produktkenntnisse beziehen sich auf Konzepte und Themen, die auf der Dokumentation zu Experience League basieren. Fragen zum Produktwissen können in den folgenden Untergruppen genauer spezifiziert werden:

| Produktkenntnisse | Beispiele |
| --- | --- |
| Punktuelles Lernen | <ul><li>Was ist der Unterschied zwischen einer Identität und einem Primär- oder Fremdschlüssel?</li><li>Was sind Lookalike-Zielgruppen?</li></ul> |
| Erkennung öffnen | <ul><li>Wie kann ich diesen Datensatz exportieren?</li><li>Gibt es Schemata für Kundinnen und Kunden im Gesundheitswesen?</li></ul> |
| Fehlerbehebung | <ul><li>Warum kann ich ein Schema, das Adobe gehört, nicht für das Profil aktivieren?</li><li>Warum kann ich ein Segment nicht löschen?</li></ul> |

{style="table-layout:auto"}

Sehen Sie sich das folgende Video an, um weitere Informationen zu KI-Assistent-Produktkenntnissen zu erhalten:

>[!VIDEO](https://video.tv.adobe.com/v/3438032/?learn=on)

### Betriebliche Erkenntnisse {#operational-insights}

Operative Einblicke beziehen sich auf Antworten, die der KI-Assistent zu Ihren Metadatenobjekten (Attributen, Zielgruppen, Datenflüssen, Datensätzen, Zielen, Journey, Schemata und Quellen) generiert, einschließlich Zählungen, Suchen und Auswirkungen auf die Herkunft. Es werden keine Daten innerhalb der Sandbox betrachtet.

* Wie viele Datensätze habe ich?
* Wie viele Schemaattribute wurden noch nie verwendet?
* Welche Zielgruppen wurden aktiviert?

Sie können Fragen zum KI-Assistenten zu Ihren betrieblichen Erkenntnissen in den folgenden Bereichen stellen:

| Domain | Unterstützte Metadaten | Nicht unterstützte Metadaten |
| --- | --- | --- |
| Attribute | <ul><li>Suche nach Attributnamen</li><li>Attribut - Schemabeziehung</li><li>Attribut - Datensatzbeziehung</li><li>Attribut - Zielgruppenbeziehung</li><li>Attribut - Zielbeziehung</li></ul> | <ul><li>Attributklasse</li><li>Verfolgung</li><li>Veraltungsstatus</li><li>Beschriftungen</li><li>In Attributen gespeicherter Wert</li></ul> |
| Zielgruppen | <ul><li>Zielgruppengröße</li><li>Zielgruppentyp (Streaming oder Batch)</li><li>Erstellungs-/Änderungsdatum</li><li>Aktivierungsstatus</li><li>Anzahl der Profile</li><li>Duplizieren von Zielgruppen</li><li>Zielgruppen-Definitionssuche</li><li>Zielgruppe - Zielgruppenbeziehung</li><li>Zielgruppe - Attributbeziehung</li><li>Zielgruppe - Datensatzbeziehung</li><li>Zielgruppen-Ziel-Beziehung</li><li>Namenssuche</li><li>Name- und ID-Suche | <ul><li>Zielgruppenüberschneidungen</li><li>Zielgruppen-Aktivierung</li><li>Zielgruppe - Kampagnenbeziehungen</li><li>Verfolgung</li><li>Erstellen/Ändern</li><li>Beschriftungen</li><li>Trends bei der Profilqualifizierung</li></ul> |
| Datenflüsse | <ul><li>Anzahl der Datenflüsse</li><li>Datenflussstatus</li><li>Datenfluss - Datensatzbeziehung</li><li>Datenfluss-Quelle-Beziehung</li></ul> | <ul><li>Erstellung/Änderung</li><li>Datenfluss-Batch-Beziehungen</li><li>Anzahl der aufgenommenen Profile</li></ul> |
| Datensätze | <ul><li>Anzahl der Datensätze</li><li>Profilaktivierungsstatus</li><li>Erstellungs-/Änderungsdatum</li><li>Datensatz - Schemabeziehung</li><li>Datensatz-Zielgruppen-Beziehung</li><li>Datensatz - Attributbeziehung</li><li>Datensatz - Datenflussbeziehung</li><li>Namenssuche </li><li>Name- und ID-Suche</li></ul> | <ul><li>Verfolgung</li><li>Erstellt von</li><li>Datensatz - Batch-Beziehung</li><li>Erstellen/Ändern von Datensätzen</li><li>Datensatzgröße</li><li>Anzahl der Profile</li><li>Anzahl Zeilen</li><li>Wertesuche</li></ul> |
| Ziele | <ul><li>Konfigurierte Zielzählungen</li><li>Ziel - Zielgruppenbeziehung</li><li>Zielattributbeziehung</li></ul> | <ul><li>Konto eingerichtet</li><li>Informationen zu Kontoanmeldeinformationen</li><li>Eindeutige Profile aktiviert</li></ul> |
| Journeys | <ul><li>Zählungen</li><li>Namenssuche</li><li>Name- und ID-Suche</li><li>Journey-Status</li><li>Ausgelöster Status (Zielgruppe vs. Ereignisse)</li><li>Erstellungs-/Änderungsdatum</li><li>Wiederkehrende Häufigkeit</li></ul> | <ul><li>Attribute - Journey-Beziehungen</li><li>Verfolgung</li><li>Erstellung/Änderung</li><li>Erstellt von</li><li>Events</li><li>Journey - Datensatz</li><li>Journey - Schema</li><li>Angebote</li><li>Trends bei der Profilqualifizierung</li><li>Schrittereignisse</li></ul> |
| Schemata | <ul><li>Anzahl der Schemata</li><li>Erstellungs-/Änderungsdatum</li><li>Schema - Attributbeziehung</li><li>Schema - Datensatzbeziehung</li><li>Schema - Zielgruppenbeziehung</li><li>Profilaktivierungsstatus</li><li>Namenssuche</li><li>Name- und ID-Suche</li></ul> | <ul><li>Verfolgung</li><li>Erstellung/Änderung</li><li>Erstellt von</li><li>Feldergruppen</li><li>Identitäten</li><li>Identity-Namespaces</li><li>Beschriftungen</li><li>Anzahl der Profile</li></ul> |
| Quellen | <ul><li>Anzahl der Konten</li><li>Kontostatus</li><li>Aktive/inaktive Datenflüsse für jedes Konto</li><li>Source-Connector - Datenflussbeziehung</li><li>Source-Konto - Datenflussbeziehung</li></ul> | <ul><li>Informationen zu Kontoanmeldeinformationen</li><li>Konto eingerichtet</li><li>Metriken zur Datenaufnahme</li><li>Anzahl der Profile</li><li>Source - Batch-Beziehungen</li></ul> |

{style="table-layout:auto"}

Bei Fragen zu operativen Einblicken spiegeln die Antworten möglicherweise nicht den aktuellen Status der Benutzeroberfläche wider. Die Daten, die diese Fragen stützen, werden alle 24 Stunden einmal aktualisiert. Änderungen, die Benutzende tagsüber in Real-Time CDP vornehmen, werden beispielsweise nachts mit den Datenspeichern synchronisiert und stehen dann morgens für Benutzerfragen zur Verfügung. Sie müssen sich bei einer Sandbox anmelden, um bestimmte Daten im Zusammenhang mit -Objekten abzufragen.

Sehen Sie sich das folgende Video an, um weitere Informationen zu den operativen Einblicken des KI-Assistenten zu erhalten:

>[!VIDEO](https://video.tv.adobe.com/v/3444041?learn=on&enablevpops&captions=ger)

### Funktionsumfang {#feature-scope}

Derzeit umfasst der KI-Assistent Folgendes:

* [Produktkenntnisse](./home.md#product-knowledge): Der KI-Assistent beantwortet Fragen zu Produktkenntnissen für Experience Platform, Real-Time Customer Data Platform und Adobe Journey Optimizer. Sie können auch Produktwissensthemen für Customer Journey Analytics behandeln, jedoch nur über die Customer Journey Analytics-Benutzeroberfläche.
* [Operative Einblicke](./home.md#operational-insights): Sie können dem KI-Assistenten Fragen zu operativen Einblicken in die folgenden Datenobjekte stellen: Attribute, Zielgruppen, Datenflüsse, Datensätze, Ziele, Journey, Schemata und Quellen.

## Nächste Schritte

Nachdem Sie nun über ein allgemeines Verständnis des KI-Assistenten verfügen, können Sie jetzt fortfahren und den KI-Assistenten während Ihrer Workflows verwenden. Weiterführende Informationen finden Sie in der folgenden Dokumentation:

* [Handbuch zur Benutzeroberfläche des KI-Assistenten](./ui-guide.md)
* [Zugriff auf Funktionen](./access.md)
* [Handbuch zu Fragen](./questions.md)
* [Datenschutz, Sicherheit und Governance im KI-Assistenten](./privacy.md)
* [Häufig gestellte Fragen](./faq.md)
