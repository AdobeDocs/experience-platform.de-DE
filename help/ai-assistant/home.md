---
title: KI-Assistent (veraltet) in Adobe Experience Platform - Übersicht
description: Erfahren Sie mehr über den KI-Assistenten (alt), seine Nuancen und Anwendungsfälle und wie Sie damit Ihren Workflow mit Adobe Experience Platform und Real-Time Customer Data Platform beschleunigen können.
exl-id: cfd4ac22-fff3-4b50-bbc2-85b6328f603c
source-git-commit: 68c55e370cab58ce5c93359520bf4ce671282a1b
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 5%

---

# KI-Assistent (veraltet) in Adobe Experience Platform

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

Das folgende Video soll Ihnen dabei helfen, KI-Assistent zu verstehen.

>[!VIDEO](https://video.tv.adobe.com/v/3429845?learn=on)

Lesen Sie dieses Dokument, um mehr über den KI-Assistenten (veraltet) in Adobe Experience Platform zu erfahren.

Der KI-Assistent (veraltet) in Adobe Experience Platform ist ein Gesprächserlebnis, mit dem Sie Ihre Workflows in Adobe-Anwendungen beschleunigen können. Sie können den KI-Assistenten (frühere Version) verwenden, um Produktkenntnisse besser zu verstehen, Probleme zu beheben oder Informationen zu durchsuchen und operative Erkenntnisse zu erhalten. Der KI-Assistent (veraltet) unterstützt Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer und Customer Journey Analytics.

![Die Benutzeroberfläche des KI-Assistenten mit dem ausgelösten erstmaligen Benutzererlebnis.](./images/ai-assistant-full.png)

>[!IMPORTANT]
>
>Sie müssen einer [Benutzervereinbarung“ zustimmen](https://www.adobe.com/de/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html) bevor Sie den KI-Assistenten (veraltet) verwenden können. Die Benutzervereinbarung enthält auch die öffentliche Beta-Vereinbarung. Dies dient dazu, dass Sie zusätzliche KI-Assistenten-Funktionen (veraltete Funktionen) verwenden können, während sie in einer Beta-Funktion eingeführt werden.

+++Auswählen, um die Benutzervereinbarungsschnittstelle anzuzeigen

![Die erste Seite der Benutzervereinbarung.](./images/user-agreement-1.png)

![Die letzte Seite der Benutzervereinbarung.](./images/user-agreement-2.png)

+++

## Grundlagen zum KI-Assistenten {#understanding-ai-assistant}

Der KI-Assistent (veraltet) antwortet auf Ihre gesendeten Fragen, indem er eine Datenbank abfragt und dann Daten aus der Datenbank in eine für Menschen lesbare Antwort übersetzt.

Diese interne Darstellung der zugrunde liegenden Daten wird auch als **[!DNL Knowledge Graph]** bezeichnet - ein umfassendes Web von Konzepten, Daten und Metadaten für eine bestimmte Antwort.

Die [!DNL Knowledge Graph] besteht aus Unterdiagrammen, die bei jeder Übermittlung von Abfragen referenziert werden:

* Betriebsbezogene Einblicke des Kunden.
* Einblicke in den Betrieb von Kunden in verschiedenen Meta-Stores.
* Dokumentation zu Experience League.

Es gibt zwei Klassen von Fragen, die vor der Abfrage des KI-Assistenten (veraltet) zu berücksichtigen sind:

### Produktkenntnisse {#product-knowledge}

Produktkenntnisse beziehen sich auf Konzepte und Themen, die auf der Dokumentation zu Experience League basieren. Fragen zum Produktwissen können in den folgenden Untergruppen genauer spezifiziert werden:

| Produktkenntnisse | Beispiele |
| --- | --- |
| Punktuelles Lernen | <ul><li>Was ist der Unterschied zwischen einer Identität und einem Primär- oder Fremdschlüssel?</li><li>Was sind Lookalike-Zielgruppen?</li></ul> |
| Erkennung öffnen | <ul><li>Wie kann ich diesen Datensatz exportieren?</li><li>Gibt es Schemata für Kundinnen und Kunden im Gesundheitswesen?</li></ul> |
| Fehlerbehebung | <ul><li>Warum kann ich ein Schema, das Adobe gehört, nicht für das Profil aktivieren?</li><li>Warum kann ich ein Segment nicht löschen?</li></ul> |

{style="table-layout:auto"}

Sehen Sie sich das folgende Video an, um weitere Informationen zu KI-Assistent (veraltete Produktkenntnisse) zu erhalten:

>[!VIDEO](https://video.tv.adobe.com/v/3475939/?captions=ger&learn=on)

### Betriebliche Erkenntnisse {#operational-insights}

Operative Insights beziehen sich auf Antworten, die der KI-Assistent (veraltete Version) über Ihre Metadatenobjekte (Attribute, Zielgruppen, Datenflüsse, Datensätze, Ziele, Journey, Schemata und Quellen) generiert, einschließlich Zählungen, Suchen und Auswirkungen auf die Herkunft. Es werden keine Daten innerhalb der Sandbox betrachtet.

* Wie viele Datensätze habe ich?
* Wie viele Schemaattribute wurden noch nie verwendet?
* Welche Zielgruppen wurden aktiviert?

Sie können Fragen zum KI-Assistenten (frühere Version) zu Ihren betrieblichen Insights in den folgenden Bereichen stellen:

| Domain | Unterstützte Metadaten | Nicht unterstützte Metadaten |
| --- | --- | --- |
| Attribute | <ul><li>Suche nach Attributnamen</li><li>Attribut - Schemabeziehung</li><li>Attribut - Datensatzbeziehung</li><li>Attribut - Zielgruppenbeziehung</li><li>Attribut - Zielbeziehung</li></ul> | <ul><li>Attributklasse</li><li>Verfolgung</li><li>Veraltungsstatus</li><li>Beschriftungen</li><li>In Attributen gespeicherter Wert</li></ul> |
| Zielgruppen | <ul><li>Zielgruppengröße</li><li>Zielgruppentyp (Streaming oder Batch)</li><li>Erstellungs-/Änderungsdatum</li><li>Aktivierungsstatus</li><li>Anzahl der Profile</li><li>Duplizieren von Zielgruppen</li><li>Zielgruppen-Definitionssuche</li><li>Zielgruppe - Zielgruppenbeziehung</li><li>Zielgruppe - Attributbeziehung</li><li>Zielgruppe - Datensatzbeziehung</li><li>Zielgruppen-Ziel-Beziehung</li><li>Namenssuche</li><li>Name- und ID-Suche | <ul><li>Zielgruppenüberschneidungen</li><li>Zielgruppenaktivierung</li><li>Zielgruppe - Kampagnenbeziehungen</li><li>Verfolgung</li><li>Erstellen/Ändern</li><li>Beschriftungen</li><li>Trends bei der Profilqualifizierung</li></ul> |
| Datenflüsse | <ul><li>Anzahl der Datenflüsse</li><li>Datenflussstatus</li><li>Datenfluss - Datensatzbeziehung</li><li>Datenfluss-Quelle-Beziehung</li></ul> | <ul><li>Erstellung/Änderung</li><li>Datenfluss-Batch-Beziehungen</li><li>Anzahl der aufgenommenen Profile</li></ul> |
| Datensätze | <ul><li>Anzahl der Datensätze</li><li>Profilaktivierungsstatus</li><li>Erstellungs-/Änderungsdatum</li><li>Datensatz - Schemabeziehung</li><li>Datensatz-Zielgruppen-Beziehung</li><li>Datensatz - Attributbeziehung</li><li>Datensatz - Datenflussbeziehung</li><li>Datensatzgröße</li><li>Anzahl Zeilen</li><li>Namenssuche </li><li>Name- und ID-Suche</li></ul> | <ul><li>Verfolgung</li><li>Erstellt von</li><li>Datensatz - Batch-Beziehung</li><li>Erstellen/Ändern von Datensätzen</li><li>Anzahl der Profile</li><li>Wertesuche</li></ul> |
| Ziele | <ul><li>Konfigurierte Zielzählungen</li><li>Ziel - Zielgruppenbeziehung</li><li>Zielattributbeziehung</li></ul> | <ul><li>Konto eingerichtet</li><li>Informationen zu Kontoanmeldeinformationen</li><li>Eindeutige Profile aktiviert</li></ul> |
| Journeys | <ul><li>Zählungen</li><li>Namenssuche</li><li>Name- und ID-Suche</li><li>Journey-Status</li><li>Ausgelöster Status (Zielgruppe vs. Ereignisse)</li><li>Erstellungs-/Änderungsdatum</li><li>Wiederkehrende Häufigkeit</li></ul> | <ul><li>Attribute - Journey-Beziehungen</li><li>Verfolgung</li><li>Erstellung/Änderung</li><li>Erstellt von</li><li>Ereignisse</li><li>Journey - Datensatz</li><li>Journey - Schema</li><li>Angebote</li><li>Trends bei der Profilqualifizierung</li><li>Schrittereignisse</li></ul> |
| Schemata | <ul><li>Anzahl der Schemata</li><li>Erstellungs-/Änderungsdatum</li><li>Schema - Attributbeziehung</li><li>Schema - Datensatzbeziehung</li><li>Schema - Zielgruppenbeziehung</li><li>Profilaktivierungsstatus</li><li>Namenssuche</li><li>Name- und ID-Suche</li></ul> | <ul><li>Verfolgung</li><li>Erstellung/Änderung</li><li>Erstellt von</li><li>Feldergruppen</li><li>Identitäten</li><li>Identity-Namespaces</li><li>Beschriftungen</li><li>Anzahl der Profile</li></ul> |
| Quellen | <ul><li>Anzahl der Konten</li><li>Kontostatus</li><li>Aktive/inaktive Datenflüsse für jedes Konto</li><li>Source-Connector - Datenflussbeziehung</li><li>Source-Konto - Datenflussbeziehung</li></ul> | <ul><li>Informationen zu Kontoanmeldeinformationen</li><li>Konto eingerichtet</li><li>Metriken zur Datenaufnahme</li><li>Anzahl der Profile</li><li>Source - Batch-Beziehungen</li></ul> |

{style="table-layout:auto"}

Bei Fragen zu operativen Einblicken spiegeln die Antworten möglicherweise nicht den aktuellen Status der Benutzeroberfläche wider. Die Daten, die diese Fragen stützen, werden alle 24 Stunden einmal aktualisiert. Änderungen, die Benutzende tagsüber in Real-Time CDP vornehmen, werden beispielsweise nachts mit den Datenspeichern synchronisiert und stehen dann morgens für Benutzerfragen zur Verfügung. Sie müssen sich bei einer Sandbox anmelden, um bestimmte Daten im Zusammenhang mit -Objekten abzufragen.

Sehen Sie sich das folgende Video an, um weitere Informationen zu den operativen Einblicken des KI-Assistenten (veraltete Version) zu erhalten:

>[!VIDEO](https://video.tv.adobe.com/v/3444041?captions=ger&learn=on&enablevpops)

### Funktionsumfang {#feature-scope}

Derzeit umfasst der Umfang des KI-Assistenten (veraltet) Folgendes:

* [Produktwissen](./home.md#product-knowledge): KI-Assistent (veraltet) kann Fragen zu Produktkenntnissen für Experience Platform, Real-Time Customer Data Platform und Adobe Journey Optimizer beantworten. Sie können auch Produktwissensthemen für Customer Journey Analytics behandeln, jedoch nur über die Customer Journey Analytics-Benutzeroberfläche.
* [Operative Einblicke](./home.md#operational-insights): Sie können dem KI-Assistenten (veraltet) Fragen zu operativen Einblicken in die folgenden Datenobjekte stellen: Attribute, Zielgruppen, Datenflüsse, Datensätze, Ziele, Journey, Schemata und Quellen.

## Nächste Schritte

Nachdem Sie nun über ein allgemeines Verständnis von KI-Assistent (veraltet) verfügen, können Sie jetzt fortfahren und den KI-Assistenten (veraltet) während Ihrer Workflows verwenden. Weiterführende Informationen finden Sie in der folgenden Dokumentation:

* [Handbuch zur Benutzeroberfläche des KI-Assistenten (veraltet)](./ui-guide.md)
* [Zugriff auf Funktionen](./access.md)
* [Handbuch zu Fragen](./questions.md)
* [Datenschutz, Sicherheit und Governance im KI-Assistenten (veraltet)](./privacy.md)
* [Häufig gestellte Fragen](./faq.md)
