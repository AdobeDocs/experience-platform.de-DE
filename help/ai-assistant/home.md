---
title: KI-Assistent in Adobe Experience Platform - Überblick
description: Erfahren Sie mehr über den KI-Assistenten, seine Funktionen und Anwendungsbeispiele sowie darüber, wie Sie damit Ihren Workflow mit Adobe Experience Platform und Real-time Customer Data Platform beschleunigen können.
exl-id: cfd4ac22-fff3-4b50-bbc2-85b6328f603c
source-git-commit: a1092e21940c5e4ba9b598bc51ba1243b57a0051
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 2%

---

# KI-Assistent in Adobe Experience Platform

Lesen Sie dieses Dokument, um mehr über AI Assistant in Adobe Experience Platform zu erfahren.

AI Assistant in Adobe Experience Platform ist eine Dialogerfahrung, mit der Sie Ihre Workflows in Adobe-Applikationen beschleunigen können. Sie können den AI-Assistenten verwenden, um Produktwissen besser zu verstehen, Probleme zu beheben oder Informationen zu durchsuchen und operative Einblicke zu erhalten. Der AI-Assistent unterstützt Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer und Customer Journey Analytics.

![Die Benutzeroberfläche des AI-Assistenten mit dem ersten ausgelösten Benutzererlebnis.](./images/blank.png)

>[!IMPORTANT]
>
>Sie müssen einer Benutzervereinbarung zustimmen, bevor Sie den KI-Assistenten verwenden können. Die Nutzervereinbarung enthält auch die öffentliche Betavereinbarung. Dies ist erforderlich, damit Sie zusätzliche Funktionen des KI-Assistenten verwenden können, wenn sie als Beta-Version eingeführt werden.

+++Auswählen zum Anzeigen der Benutzeroberfläche für Benutzervereinbarungen

![Die erste Seite der Benutzervereinbarung.](./images/user-agreement-1.png)

![Die letzte Seite der Benutzervereinbarung.](./images/user-agreement-2.png)

+++

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

### Funktionsumfang {#feature-scope}

Derzeit ist der Umfang des AI-Assistenten wie folgt:

* [Produktwissen](./home.md#product-knowledge): AI Assistant kann Fragen zu Produktwissen für Experience Platform, Real-time Customer Data Platform und Adobe Journey Optimizer beantworten. Sie können sich auch über die Customer Journey Analytics-Benutzeroberfläche mit Produktwissensthemen für Customer Journey Analytics befassen.
* [Operative Einblicke](./home.md#operational-insights): Sie können den KI-Assistenten mit Fragen zu betrieblichen Einblicken in die folgenden Datenobjekte befassen: Attribute, Zielgruppen, Datenflüsse, Datensätze, Ziele, Journey, Schemata und Quellen.

## Nächste Schritte

Da Sie nun über allgemeine Kenntnisse im Bereich KI-Assistenzkraft verfügen, können Sie jetzt fortfahren und KI-Assistenzkräfte während Ihrer Workflows verwenden. Weiterführende Informationen finden Sie in der folgenden Dokumentation:

* [Handbuch zur Benutzeroberfläche des AI-Assistenten](./ui-guide.md)
* [Funktionszugriff](./access.md)
* [Fragenleitfaden](./questions.md)
* [Datenschutz, Sicherheit und Governance im KI-Assistenten](./privacy.md)
* [Häufig gestellte Fragen](./faq.md)
