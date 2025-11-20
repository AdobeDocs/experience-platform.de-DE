---
keywords: Experience Platform;Startseite;beliebte Themen;XDM;XDM-System;XDM Individual Profile;XDM ExperienceEvent;XDM Experience Event;Experience Event;Erlebnisereignis;Feldergruppen;Feldergruppen;Feldergruppe;Feldergruppe;Erlebnisereignis;XDM ExperienceEvent;experienceEvent;experienceEvent;XDM Experienceevent;Experience-Datenmodell;Experience Data Model;Datenmodell;Data Model;Schema Registry;Schema Library;Schemabibliothek;Schema;Eintragsdaten;Zeitreihen;Zeitreihen
solution: Experience Platform
title: XDM-System – Übersicht
description: Standardisierung und Interoperabilität sind Schlüsselkonzepte von Adobe Experience Platform. Das von Adobe unterstützte Experience-Datenmodell (XDM) ermöglicht die Standardisierung von Kundenerlebnisdaten und die Definition von Schemata für das Customer Experience Management.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 57981d2e4306b2245ce0c1cdd9f696065c508a1d
workflow-type: tm+mt
source-wordcount: '2440'
ht-degree: 56%

---

# XDM-System – Übersicht

Standardisierung und Interoperabilität sind Schlüsselkonzepte von Adobe Experience Platform. Das von Adobe unterstützte Experience-Datenmodell (XDM) ermöglicht die Standardisierung von Kundenerlebnisdaten und die Definition von Schemata für das Customer Experience Management.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Sie bietet allgemeine Strukturen und Definitionen, anhand derer jede beliebige Anwendung mit Experience Platform-Services kommunizieren kann. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in ein gemeinsames System integriert werden, wodurch Erkenntnisse schneller und besser integriert verfügbar werden. Sie können wertvolle Einblicke durch Kundenaktionen gewinnen, Zielgruppen mithilfe von Segmenten definieren und Kundenattribute zur Personalisierung verwenden.

XDM ist das zugrunde liegende System, auf Basis dessen Adobe Experience Cloud als Teil von Experience Platform die richtige Botschaft der richtigen Person zur richtigen Zeit auf dem passenden Kanal präsentieren kann. Das XDM-System nutzt Experience-Datenmodell-Schemas, die Experience Platform Experience Platform-Services zur Verwendung bereitstellen.

Erfahren Sie mehr über die Rolle des XDM-Systems in Experience Platform.

## XDM-Schemata {#xdm-schemas}

Schemata dienen in Experience Platform zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, deren Bedeutung beizubehalten und somit Wert aus Daten zu ziehen.

Bevor Daten in Experience Platform aufgenommen werden können, muss ein Schema erstellt werden, das die Datenstruktur beschreibt und den Datentyp einschränkt, der in den einzelnen Feldern enthalten sein kann. Schemata bestehen aus einer Basisklasse und keiner oder mehreren Schema-Feldergruppen.

Weitere Informationen zum Schemakompositionsmodell, einschließlich Planungsgrundsätzen und Best Practices, finden Sie in den [Grundlagen der Schemakomposition](schema/composition.md).

### Standardmäßige XDM-Komponenten {#Standard-xdm-components}

XDM bietet eine Sammlung von standardmäßigen Feldergruppen und Datentypen, mit denen gängige Konzepte und Anwendungsfälle in verschiedenen Branchen abgedeckt werden. Sie können diese Komponenten in Experience Platform nach Branchen filtern, sodass Sie schnell und sicher Schemata erstellen können, die optimal zu Ihren speziellen Geschäftsanforderungen passen.

Beim Erstellen von Schemata in der Experience Platform-Benutzeroberfläche werden die aufgelistete Feldergruppen mit einer Beliebtheitsmetrik angezeigt. Diese Metrik wird durch die Häufigkeit bestimmt, mit der andere Experience Platform-Benutzende die Feldergruppe in ihren Schemata verwenden. Je höher die Zahl ist, desto beliebter ist die Feldergruppe. Standardmäßig werden die Ergebnisse von den beliebtesten zu den am wenigsten beliebten Ergebnissen gereiht, sodass Sie über die Datenmodellierungstrends in Ihrer Branche auf dem Laufenden bleiben.

![Die Spalte Popularität des [!UICONTROL Add field group]-Dialogfelds.](./images/overview/popularity.png)

### [!DNL Schema Library] {#schema-library}

Experience Platform stellt eine Benutzeroberfläche und RESTful-API bereit, über die Sie alle mit einem Schema in Zusammenhang stehenden Ressourcen in der **[!DNL Schema Library]** von Experience Platform anzeigen und verwalten können. Die [!DNL Schema Library] enthält standardmäßige XDM-Komponenten, die Ihnen von Adobe zur Verfügung gestellt werden, sowie Ressourcen von Experience Platform-Partnern und Anbietern, deren Anwendungen Sie verwenden.

Sie können auch neue, unternehmensspezifische Schemata und Ressourcen mithilfe der [!DNL Schema Registry API] oder des Arbeitsbereichs [!UICONTROL Schemas] in der Benutzeroberfläche von Experience Platform erstellen und verwalten.

Weitere Informationen zur Verwaltung von und Interaktion mit Schemas in Experience Platform finden Sie in der folgenden Dokumentation:

* [Handbuch zur XDM-Benutzeroberfläche](./ui/overview.md)
* [Handbuch zur Schema Registry-API](./api/overview.md)

## Datenverhalten im XDM-System {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="Datenverhalten"
>abstract="Die zur Verwendung in Experience Platform bestimmten Daten sind in drei Verhaltenstypen unterteilt: Eintrag, Zeitreihen und Ad-hoc-Analysen. Eintragsschemata liefern Informationen über die Attribute eines Subjekts, während Zeitreihenschemata eine Momentaufnahme des Systems zum Zeitpunkt der Durchführung einer Aktion erfassen. Ad-hoc-Schemata erfassen Felder, die Namespaces sind und von nur einem Datensatz verwendet werden können. Weitere Informationen zu Datenverhalten in Experience Platform finden Sie in der Dokumentation."

Daten, die in Experience Platform verwendet werden können, sind in drei Verhaltenstypen unterteilt:

* **Eintrag**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt kann ein Unternehmen oder eine Person sein.
* **Zeitreihe**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt bereit, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.
* **Ad-hoc**: Erfasst Felder, die sich in einem Namespace befinden und nur von einem einzigen Datensatz verwendet werden. Ad-hoc-Schemata werden in verschiedenen Datenaufnahme-Workflows für Experience Platform verwendet, einschließlich der Aufnahme von CSV-Dateien und der Erstellung bestimmter Arten von Quellverbindungen.

Alle XDM-Schemata beschreiben Daten, die als Eintrag oder Zeitreihe kategorisiert werden können. Das Datenverhalten eines Schemas wird durch die Klasse des Schemas definiert, die einem Schema bei dessen Erstellung zugewiesen wird. XDM-Klassen beschreiben die Mindestanzahl von Eigenschaften, die ein Schema enthalten muss, um ein bestimmtes Datenverhalten zu haben.

Obwohl Sie in der [!DNL Schema Registry] Ihre eigenen Klassen definieren können, wird empfohlen, die Standardklassen **[!UICONTROL XDM Individual Profile]** und **[!UICONTROL XDM ExperienceEvent]** für Datensatz- bzw. Zeitreihendaten zu verwenden. Diese Klassen werden weiter unten detaillierter beschrieben.

>[!NOTE]
>
>Es gibt keine Standardklassen, die auf dem Ad-hoc-Verhalten basieren. Ad-hoc-Schemata werden automatisch von den Experience Platform-Prozessen generiert, die sie verwenden. Sie können aber auch [manuell mithilfe der Schema Registry-API erstellt werden](./tutorials/ad-hoc.md).

### [!UICONTROL XDM Individual Profile] {#xdm-individual-profile}

[!UICONTROL XDM Individual Profile] ist eine auf einem Datensatz basierende Klasse, die eine einzige Repräsentation der Attribute sowohl identifizierter als auch teilweise identifizierter Subjekte darstellt. Hochgradig identifizierte Profile können für persönliche Kommunikation oder zielgerichtete Interaktionen verwendet werden. Hochgradig identifizierte Profile können detaillierte persönliche Informationen wie Name, Geschlecht, Geburtsdatum, Standort und Kontaktinformationen, einschließlich Telefonnummern und E-Mail-Adressen, enthalten.

Weniger identifizierte Profile bestehen möglicherweise nur aus anonymen Verhaltenssignalen wie Browser-Cookies. In diesem Fall wird mithilfe der wenigen Profildaten eine Informationsbasis geschaffen, in der die Interessen und Präferenzen des anonymen Profils erfasst und gespeichert werden. Die Anzahl dieser Daten kann im Laufe der Zeit anwachsen, wenn sich das Subjekt für Benachrichtigungen, Abonnements, Käufe usw. entscheidet. Dieses Anwachsen von Profilattributen kann als Ergebnis schließlich ein identifiziertes Subjekt haben und ein höheres Maß an zielgerichteter Interaktion ermöglichen.

Je mehr Daten zu einem Profil gesammelt werden, desto zuverlässiger wird der Bestand an personenbezogenen Daten, Identifizierungsinformationen, Kontaktdaten und Kommunikationsvorlieben einer Person.

Weitere Informationen zur Struktur und [[!UICONTROL XDM Individual Profile] Anwendungsfall der Felder einer Klasse finden Sie im ](./classes/individual-profile.md)-Referenzhandbuch .

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent ist eine zeitreihenbasierte Klasse, mit der der Status des Systems beim Eintreten eines Ereignisses (oder einer Reihe von Ereignissen) erfasst wird, einschließlich des Zeitpunkts und der Identität des betroffenen Subjekts. Erlebnisereignisse sind unveränderliche, sachliche Aufzeichnungen darüber, was zu diesem Zeitpunkt geschehen ist, und stellen das dar, was ohne Aggregation oder Interpretation passiert ist. Sie sind für die Zeit-Domain-Analyse von entscheidender Bedeutung, da sie zur Analyse von Änderungen, die in einem bestimmten Zeitfenster auftreten, und zum Vergleich zwischen mehreren Zeitfenstern verwendet werden können, um Trends zu verfolgen.

Erlebnisereignisse können entweder explizit oder implizit sein. Explizite Ereignisse sind unmittelbar erkennbare menschliche Aktionen, die zu einem bestimmten Zeitpunkt in einer Journey stattfinden. Implizite Ereignisse sind Ereignisse, die ohne direkte menschliche Aktion ausgelöst werden, sich aber auf eine Person beziehen. Beispiele für implizite Ereignisse sind der planmäßige Versand von E-Mail-Newslettern oder die Akkuspannung, die einen bestimmten Schwellenwert erreicht.

Es ist zwar nicht einfach, alle Ereignisse in allen Datenquellen zu kategorisieren, doch ist es äußerst nützlich, ähnliche Ereignisse zu ähnlichen Typen zusammenzufassen, um sie verarbeiten zu können.

![Eine Infografik der Kunden-Journey, die mit Erlebnisereignissen im Laufe der Zeit visualisiert wurde.](images/overview/experience-event-journey.png)

Weitere Informationen zur Struktur und [[!UICONTROL XDM ExperienceEvent] Anwendungsfall der Felder einer Klasse finden Sie im ](./classes/experienceevent.md)-Referenzhandbuch .

## XDM-Schemata und Experience Platform-Services {#schemas-and-platform-services}

Experience Platform ist schemaunabhängig, d. h. jedes Schema, das dem XDM-Standard entspricht, wird Experience Platform-Services zur Verfügung gestellt. Die Verwendung von Schemas durch verschiedene Experience Platform-Services wird im Folgenden genauer beschrieben.

### Katalog-Service, Datenaufnahme und Data Lake {#ingestion-catalog-and-storage}

Catalog Service ist das „System of Record“ für Experience Platform-Medienelemente und deren zugehörige Schemata. Catalog Service enthält nicht die eigentlichen Datendateien oder Ordner, sondern die Metadaten und Beschreibungen dieser Dateien und Ordner.

Katalogdaten werden im Data Lake gespeichert, einem hochgradig granularen Datenspeicher, der unabhängig von Herkunft oder Dateiformat alle von Experience Platform verwalteten Daten enthält.

Um mit der Aufnahme von Daten in Experience Platform zu beginnen, können Sie mithilfe von Catalog Service einen Datensatz erstellen. Der Datensatz verweist auf ein XDM-Schema, das die Struktur der aufzunehmenden Daten beschreibt. Wenn ein Datensatz ohne Schema erstellt wird, leitet Experience Platform ein „festgestelltes Schema“ ab, indem Typ und Inhalt der erfassten Datenfelder überprüft werden. Datensätze werden dann im Katalog-Service verfolgt und im Data Lake zusammen mit den Schemas und festgestellten Schemas, auf denen sie basieren, gespeichert.

Weitere Informationen finden Sie [ „Übersicht ](../catalog/home.md) Katalog-Service“. Weitere Informationen zur Datenaufnahme in [ finden ](../ingestion/home.md) in der Übersicht zur Datenaufnahme in Adobe Experience Platform .

### Data Mirror und relationale Schemata {#relational-schemas}

>[!AVAILABILITY]
>
>Data Mirror und relationale Schemata stehen Adobe Journey Optimizer-Lizenzinhabern **Orchestrierte Kampagnen** zur Verfügung. Sie sind auch als **eingeschränkte Version** für Customer Journey Analytics-Benutzer verfügbar, je nach Ihrer Lizenz und der Aktivierung von Funktionen. Wenden Sie sich an den Adobe-Support, um Zugang zu erhalten.

>[!NOTE]
>
>Relationale Schemata wurden in früheren Versionen der Adobe Experience Platform-Dokumentation zuvor als modellbasierte Schemata bezeichnet. Die Funktionalität bleibt gleich, nur die Terminologie wurde aus Gründen der Übersichtlichkeit geändert.

Data Mirror ist eine Adobe Experience Platform-Funktion, die eine erweiterte Datenbanksynchronisierung mithilfe von relationalen Schemata ermöglicht. Einen vollständigen Überblick über die Funktionen und Anwendungsfälle von Data Mirror finden Sie in der Übersicht zu [Data Mirror](./data-mirror/overview.md).

Data Mirror arbeitet mit relationalen Schemata, die für strukturierte Datenmuster im relationalen Stil entwickelt wurden. Sie erzwingen Primärschlüssel, unterstützen Versionskennungen und definieren Schema-zu-Schema-Beziehungen mit Primär- und Fremdschlüsseln. Im Gegensatz zu Standard-XDM-Schemata erfordern sie keine Klassen oder Feldergruppen und sind für Workflows zur Erfassung von Änderungsdaten optimiert.

Weitere Informationen zum Definieren von Schema-zu-Schema-Beziehungen finden Sie in der [Deskriptoren-Endpunktdokumentation](./api/descriptors.md).

Verwenden Sie Data Mirror bei folgenden Aufgaben:

* Synchronisieren von Datenänderungen aus externen Systemen wie Snowflake, Databricks oder BigQuery
* Beibehalten von Datenbankbeziehungen und Erzwingen der Datenintegrität während der Aufnahme
* Unterstützung erweiterter Analysen und Journey-Orchestrierung
* Präzises Änderungs-Tracking mit Upserts und Löschvorgängen aktivieren

Um ein relationales Schema zu erstellen, wählen Sie beim Erstellen eines Schemas **[!UICONTROL Relational]** aus. Relationale Schemata verwenden keine Klassen oder Feldergruppen. Stattdessen definieren Sie die Struktur manuell oder laden eine DDL-Datei hoch. Relationale Schemata erfordern einen Primärschlüssel, eine Versionskennung und gegebenenfalls Zeitstempelkennungsfelder. Anschließend können Sie zusätzliche Felder konfigurieren und Beziehungen zu anderen Schemata definieren.

>[!NOTE]
>
>Während der Aufnahme verwendete Kontrollspalten (z. B. `_change_request_type` für Workflows zur Erfassung von Änderungsdaten) werden zur Aufnahmezeit gelesen und nicht im Schema gespeichert oder XDM-Feldern zugeordnet. Relationale Schemata sind mit entsprechenden Experience Platform-Berechtigungen und aktivierten Funktionen verfügbar.

Ausführliche Anweisungen und Anleitungen für Anwendungsfälle finden Sie unter:

* [Übersicht über Data Mirror](./data-mirror/overview.md) - Funktionen, Anwendungsfälle und Implementierungsplanung
* [Technische Referenz zum relationalen Schema](./schema/relational.md) - Technische Spezifikationen und Einschränkungen
* [Tutorial zur Benutzeroberfläche](./ui/resources/schemas.md#create-relational-schema)
* [API-Tutorial](./api/schemas.md#create-relational-schema)
* [Dokumentation zu Deskriptoren (Bezeichnern)](./api/descriptors.md#relationship-descriptor)
* [Änderungsdatenerfassung aktivieren](../sources/tutorials/api/change-data-capture.md)

### Abfrage-Service {#query-service}

Sie können Standard-SQL zur Abfrage von Experience Platform-Daten verwenden, um viele verschiedene Anwendungsfälle mit dem Abfrage-Service von Adobe Experience Platform zu unterstützen.

Nachdem ein Schema erstellt und ein Datensatz erstellt wurde, der auf dieses Schema verweist, werden die Daten aufgenommen und im Data Lake gespeichert. Anschließend können Sie den Abfrage-Service verwenden, um beliebige Datensätze im Data Lake zu verbinden und die Abfrageergebnisse als neuen Datensatz zu erfassen, der bei Reporting, maschinellem Lernen oder der Aufnahme in das Echtzeit-Kundenprofil verwendet werden kann.

Weitere Informationen zu diesem Service finden Sie unter [Query Service – Übersicht](../query-service/home.md).

### Echtzeit-Kundenprofil {#real-time-customer-profile}

Das Echtzeit-Kundenprofil bietet ein zentralisiertes Kundenprofil für zielgerichtetes und personalisiertes Erlebnis-Management. Jedes Profil enthält Daten, die systemübergreifend aggregiert werden, und enthält aussagekräftige Konten mit Zeitstempel von Ereignissen, die das Profilsubjekt betreffen. Diese Ereignisse haben möglicherweise in allen Systemen stattgefunden, die Sie mit Experience Platform verwenden.

Das Echtzeit-Kundenprofil nutzt schemaformatierte Daten basierend auf den Klassen [!UICONTROL XDM Individual Profile] und [!UICONTROL XDM ExperienceEvent] und reagiert auf Abfragen, die auf diesen Daten basieren.

Das System bildet für jedes Kundenprofil eine Instanz und führt Daten einer Person zu einer „Single Source of Truth“ zusammen. Diese zusammengeführten Daten werden mithilfe eines so genannten „Vereinigungsschemas“ dargestellt (auch als „Vereinigungsansicht“ bezeichnet). Ein Vereinigungsschema aggregiert die Felder aller Schemas, die dieselbe Klasse implementieren, in ein einziges Schema. Wenn Sie ein Schema mithilfe der Benutzeroberfläche oder API erstellen, können Sie es aktivieren, damit es mit dem Echtzeit-Kundenprofil verwendet werden kann, und es zur Aufnahme in die Vereinigung mit einem Tag versehen. Das mit einem Tag versehene Schema wird dann Teil der Schemadefinition, die an das Profil übergeben wird.

Wenn [!UICONTROL XDM Individual Profile] und [!UICONTROL XDM ExperienceEvent] Daten in den Data Lake aufgenommen werden, nimmt das Echtzeit-Kundenprofil alle Daten auf, die für dessen Verwendung aktiviert wurden. Je mehr Interaktionen und Details aufgenommen werden, desto zuverlässiger werden die einzelnen Profile.

[!UICONTROL XDM Individual Profile] Daten helfen bei der Kommunikation und der Aktivierung von Aktionen auf allen Kanälen und allen Adobe-Produkten. In Kombination mit umfangreichen Verhaltens- und Interaktionsdaten können diese Daten für maschinelles Lernen verwendet werden. Darüber hinaus kann die Echtzeit-Kundenprofil-API genutzt werden, um die Funktionalität von Drittanbieterlösungen, CRM-Systemen und proprietären Lösungen zu erweitern.

Weitere Informationen dazu finden Sie in der [Übersicht zum Echtzeit-Kundenprofil](../profile/home.md).

### Data Science Workspace {#data-science-workspace}

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich. Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Data Science Workspace in Adobe Experience Platform nutzt maschinelles Lernen und künstliche Intelligenz, um Einblicke aus den in Experience Platform gespeicherten Daten zu gewinnen. Mit Data Science Workspace können Datenwissenschaftler Rezepte erstellen, die auf [!UICONTROL XDM Individual Profile] und [!UICONTROL XDM ExperienceEvent] Daten über Kunden und ihre Aktivitäten basieren. Diese Rezepte erleichtern Prognosen wie Kaufneigung und empfohlene Angebote, die von Einzelpersonen geschätzt und verwendet werden.

Mit Data Science Workspace können Datenwissenschaftler einfach intelligente, auf maschinellem Lernen basierende Service-APIs erstellen. Diese Services sind mit anderen Adobe-Lösungen kompatibel, einschließlich Adobe Target und Adobe Analytics Cloud, und helfen Ihnen bei der Automatisierung personalisierter, zielgerichteter digitaler Erlebnisse.

Weitere Informationen zur Verwendung von Experience Platform-Daten zur Bereitstellung von Einblicken finden Sie in [Data Science Workspace – Übersicht](../data-science-workspace/home.md).

## Nächste Schritte und zusätzliche Ressourcen

Jetzt, da Sie die Rolle von Schemata in Experience Platform besser verstehen, können Sie beginnen, eigene Schemata zu erstellen.

Um mehr über die Prinzipien und Best Practices beim Erstellen von Schemata zu erfahren, die mit Experience Platform verwendet werden können, lesen Sie den Abschnitt [Grundlagen der Schemaaufbaus](schema/composition.md). Eine schrittweise Anleitung zum Erstellen eines Schemas finden Sie in den Tutorials zum Erstellen eines Schemas mithilfe [der API](tutorials/create-schema-api.md) oder [der Benutzeroberfläche](tutorials/create-schema-ui.md).

Sehen Sie sich das folgende Video an, um [!DNL XDM System] in Experience Platform besser zu verstehen:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
