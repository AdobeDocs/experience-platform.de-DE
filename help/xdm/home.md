---
keywords: Experience Platform;Startseite;beliebte Themen;XDM;XDM-System;XDM Individual Profile;XDM ExperienceEvent;XDM Experience Event;Experience Event;Erlebnisereignis;Feldergruppen;Feldergruppen;Feldergruppe;Feldergruppe;Erlebnisereignis;XDM ExperienceEvent;experienceEvent;experienceEvent;XDM Experienceevent;Experience-Datenmodell;Experience Data Model;Datenmodell;Data Model;Schema Registry;Schema Library;Schemabibliothek;Schema;Datensatzdaten;Zeitreihen;Time Series
solution: Experience Platform
title: XDM-System – Übersicht
description: Standardisierung und Interoperabilität sind Schlüsselkonzepte von Adobe Experience Platform. Das von Adobe unterstützte Experience-Datenmodell (XDM) ermöglicht die Standardisierung von Kundenerlebnisdaten und die Definition von Schemas für das Customer Experience Management.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 8113b5298120f710f43c5a02504f19ca3af67c5a
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 74%

---

# XDM-System – Übersicht

Standardisierung und Interoperabilität sind Schlüsselkonzepte von Adobe Experience Platform. Das von Adobe unterstützte Experience-Datenmodell (XDM) ermöglicht die Standardisierung von Kundenerlebnisdaten und die Definition von Schemas für das Customer Experience Management.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Dieses Modell bietet allgemeine Strukturen und Definitionen, anhand derer jede beliebige Anwendung mit Platform-Diensten kommunizieren kann. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in ein gemeinsames System integriert werden, wodurch Erkenntnisse schneller und besser integriert verfügbar werden. Sie können wertvolle Einblicke durch Kundenaktionen gewinnen, Zielgruppen mithilfe von Segmenten definieren und Kundenattribute zur Personalisierung verwenden.

XDM ist das zugrunde liegende System, auf Basis dessen Adobe Experience Cloud als Teil von Experience Platform die richtige Botschaft der richtigen Person zur richtigen Zeit auf dem passenden Kanal präsentieren kann. Das XDM-System ist die Methode, auf der Experience Platform basiert. Es stellt Experience-Datenmodell-Schemata zur Verwendung durch Platform-Dienste bereit.

Erfahren Sie mehr über die Rolle des XDM-Systems innerhalb von Experience Platform.

## XDM-Schemas {#xdm-schemas}

Schemas dienen in Experience Platform zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, deren Bedeutung beizubehalten und somit Wert aus Daten zu ziehen.

Bevor Daten in Platform aufgenommen werden können, muss ein Schema erstellt werden, das die Datenstruktur beschreibt und den Datentyp entsprechend des jeweiligen Feldes einschränkt. Schemas bestehen aus einer Basisklasse und keiner oder mehreren Schema-Feldergruppen.

Weitere Informationen zum Schema-Kompositionsmodell, einschließlich Designgrundsätzen, und Best Practices finden Sie in der [Grundlagen der Schemakomposition](schema/composition.md).

### Standardmäßige XDM-Komponenten {#Standard-xdm-components}

XDM bietet eine Sammlung von standardmäßigen Feldergruppen und Datentypen, mit denen gängige Konzepte und Anwendungsfälle in verschiedenen Branchen abgedeckt werden. Sie können diese Komponenten in Experience Platform nach Branchen filtern, sodass Sie schnell und sicher Schemas erstellen können, die optimal zu Ihren speziellen Geschäftsanforderungen passen.

Beim Erstellen von Schemas in der Experience Platform-Benutzeroberfläche werden die aufgelistete Feldergruppen mit einer Beliebtheitsmetrik angezeigt. Diese Metrik wird durch die Häufigkeit bestimmt, mit der andere Platform-Benutzer die jeweilige Feldergruppe in ihren Schemas verwenden. Je höher die Zahl ist, desto beliebter ist die Feldergruppe. Standardmäßig werden die Ergebnisse von den beliebtesten zu den am wenigsten beliebten Ergebnissen gereiht, sodass Sie über die Datenmodellierungstrends in Ihrer Branche auf dem Laufenden bleiben.

![Die Popularitätsspalte der [!UICONTROL Feldergruppe hinzufügen] angezeigt.](./images/overview/popularity.png)

### [!DNL Schema Library] {#schema-library}

Experience Platform stellt eine Benutzeroberfläche und RESTful-API bereit, über die Sie alle mit einem Schema in Zusammenhang stehenden Ressourcen in der **[!DNL Schema Library]** von Experience Platform anzeigen und verwalten können. Die [!DNL Schema Library] enthält standardmäßige XDM-Komponenten, die Ihnen von Adobe zur Verfügung gestellt werden, sowie Ressourcen von Experience Platform-Partnern und Anbietern, deren Anwendungen Sie verwenden.

Sie können auch neue Schemata und Ressourcen erstellen und verwalten, die für Ihre Organisation eindeutig sind, indem Sie die [!DNL Schema Registry API]oder die [!UICONTROL Schemas] Arbeitsbereich in der Platform-Benutzeroberfläche.

Weitere Informationen zur Verwaltung und Interaktion mit Schemas in Platform finden Sie in der folgenden Dokumentation:

* [Handbuch zur XDM-Benutzeroberfläche](./ui/overview.md)
* [Handbuch zur Schema Registry-API](./api/overview.md)

## Datenverhalten im XDM-System {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="Datenverhalten"
>abstract="Die zur Verwendung in Experience Platform bestimmten Daten sind in drei Verhaltenstypen unterteilt: Datensatz, Zeitreihen und Ad-hoc-Analysen. Datensatzschemas liefern Informationen über die Attribute eines Subjekts, während Zeitreihenschemas eine Momentaufnahme des Systems zum Zeitpunkt der Durchführung einer Aktion erfassen. Ad-hoc-Schemata erfassen Felder, die Namespaces sind und von nur einem Datensatz verwendet werden können. Weitere Informationen zu Datenverhalten in Platform finden Sie in der Dokumentation."

Daten, die in Experience Platform verwendet werden können, sind in drei Verhaltenstypen unterteilt:

* **Datensatz**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt kann ein Unternehmen oder eine Person sein.
* **Zeitreihen**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt bereit, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.
* **Ad-hoc**: Erfasst Felder, die sich in einem Namespace befinden und nur von einem einzigen Datensatz verwendet werden. Ad-hoc-Schemas werden in verschiedenen Datenaufnahme-Workflows für Experience Platform verwendet, einschließlich der Aufnahme von CSV-Dateien und der Erstellung bestimmter Arten von Quellverbindungen.

Alle XDM-Schemas beschreiben Daten, die als Datensatz oder Zeitreihe kategorisiert werden können. Das Datenverhalten eines Schemas wird durch die Klasse des Schemas definiert, die einem Schema bei dessen Erstellung zugewiesen wird. XDM-Klassen beschreiben die Mindestanzahl von Eigenschaften, die ein Schema enthalten muss, um ein bestimmtes Datenverhalten zu haben.

Obwohl Sie in der Lage sind, Ihre eigenen Klassen innerhalb der [!DNL Schema Registry]wird empfohlen, die Standardklassen zu verwenden. **[!UICONTROL Individuelles XDM-Profil]** und **[!UICONTROL XDM ExperienceEvent]** für Datensatz- bzw. Zeitreihendaten. Diese Klassen werden weiter unten detaillierter beschrieben.

>[!NOTE]
>
>Es gibt keine Standardklassen, die auf dem Ad-hoc-Verhalten basieren. Ad-hoc-Schemata werden automatisch von den Platform-Prozessen generiert, die sie verwenden. Sie können aber auch [manuell mithilfe der Schema Registry-API erstellt wurde](./tutorials/ad-hoc.md).

### [!UICONTROL Individuelles XDM-Profil] {#xdm-individual-profile}

[!UICONTROL Individuelles XDM-Profil] ist eine auf Aufzeichnungen basierende Klasse, die eine einzige Darstellung der Attribute sowohl identifizierter als auch teilweise identifizierter Personen darstellt. Hoch identifizierte Profile können für persönliche Kommunikation oder zielgerichtete Interaktionen verwendet werden. Sehr identifizierte Profile können detaillierte persönliche Informationen wie Name, Geschlecht, Geburtsdatum, Standort und Kontaktinformationen enthalten, einschließlich Telefonnummern und E-Mail-Adressen.

Weniger identifizierte Profile bestehen möglicherweise nur aus anonymen Verhaltenssignalen wie Browser-Cookies. In diesem Fall wird mithilfe der wenigen Profildaten eine Informationsbasis geschaffen, in der die Interessen und Präferenzen des anonymen Profils erfasst und gespeichert werden. Die Anzahl dieser Daten kann im Laufe der Zeit anwachsen, wenn sich das Subjekt für Benachrichtigungen, Abonnements, Käufe usw. entscheidet. Dieses Anwachsen von Profilattributen kann als Ergebnis schließlich ein identifiziertes Subjekt haben und ein höheres Maß an zielgerichteter Interaktion ermöglichen.

Je mehr Daten zu einem Profil gesammelt werden, desto zuverlässiger wird der Bestand an personenbezogenen Daten, Identifizierungsinformationen, Kontaktdaten und Kommunikationsvorlieben einer Person.

Weitere Informationen zur Struktur und zum Anwendungsfall der Felder einer Klasse erhalten Sie im Referenzhandbuch [[!UICONTROL XDM Individual Profile]](./classes/individual-profile.md).

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent ist eine zeitreihenbasierte Klasse, mit der der Status des Systems beim Eintreten eines Ereignisses (oder einer Reihe von Ereignissen) erfasst wird, einschließlich des Zeitpunkts und der Identität des betroffenen Subjekts. Erlebnisereignisse sind unveränderliche, sachliche Aufzeichnungen darüber, was zu diesem Zeitpunkt geschehen ist, und stellen das dar, was ohne Aggregation oder Interpretation passiert ist. Sie sind für die Zeit-Domain-Analyse von entscheidender Bedeutung, da sie zur Analyse von Änderungen, die in einem bestimmten Zeitfenster auftreten, und zum Vergleich zwischen mehreren Zeitfenstern verwendet werden können, um Trends zu verfolgen.

Erlebnisereignisse können entweder explizit oder implizit sein. Explizite Ereignisse sind unmittelbar erkennbare menschliche Aktionen, die zu einem bestimmten Zeitpunkt in einer Journey stattfinden. Implizite Ereignisse sind Ereignisse, die ohne direkte menschliche Aktion ausgelöst werden, sich aber auf eine Person beziehen. Beispiele für implizite Ereignisse sind der planmäßige Versand von E-Mail-Newslettern oder die Akkuspannung, die einen bestimmten Schwellenwert erreicht.

Es ist zwar nicht einfach, alle Ereignisse in allen Datenquellen zu kategorisieren, doch ist es äußerst nützlich, ähnliche Ereignisse zu ähnlichen Typen zusammenzufassen, um sie verarbeiten zu können.

![Eine Infografik der Journey mit Erlebnisereignissen im Zeitverlauf.](images/overview/experience-event-journey.png)

Weitere Informationen zur Struktur und zum Anwendungsfall der Felder einer Klasse erhalten Sie im Referenzhandbuch [[!UICONTROL XDM ExperienceEvent]](./classes/experienceevent.md).

## XDM-Schemas und Experience Platform-Services {#schemas-and-platform-services}

Experience Platform ist schemaunabhängig, d. h. jedes Schema, das dem XDM-Standard entspricht, wird Platform-Services zur Verfügung gestellt. Die Verwendung von Schemas durch verschiedene Platform-Services wird weiter unten ausführlicher beschrieben.

### Catalog Service, Data Ingestion und Data Lake {#ingestion-catalog-and-storage}

Catalog Service ist das „System of Record“ für Experience Platform-Medienelemente und deren zugehörige Schemas. Catalog Service enthält nicht die eigentlichen Datendateien oder Ordner, sondern die Metadaten und Beschreibungen dieser Dateien und Ordner.

Katalogdaten werden im Data Lake gespeichert, einem hochgradig granularen Datenspeicher, der alle von Platform verwalteten Daten enthält, unabhängig von Herkunft oder Dateiformat.

Um mit der Aufnahme von Daten in Experience Platform zu beginnen, können Sie mithilfe von Catalog Service einen Datensatz erstellen. Der Datensatz verweist auf ein XDM-Schema, das die Struktur der aufzunehmenden Daten beschreibt. Wenn ein Datensatz ohne Schema erstellt wird, leitet Experience Platform ein „festgestelltes Schema“ ab, indem Typ und Inhalt der erfassten Datenfelder überprüft werden. Datensätze werden dann im Katalogdienst nachverfolgt und im Data Lake neben den Schemas und beobachteten Schemas, auf denen sie basieren, gespeichert.

Siehe [Catalog Service - Übersicht](../catalog/home.md) für weitere Informationen. Siehe [Datenerfassung - Übersicht](../ingestion/home.md) Weitere Informationen zur Datenerfassung in Adobe Experience Platform.

### Abfrage-Service {#query-service}

Sie können SQL-Standarddaten verwenden, um Experience Platform-Daten abzufragen und so viele verschiedene Anwendungsfälle mit Adobe Experience Platform Query Service zu unterstützen.

Nachdem ein Schema erstellt und ein Datensatz erstellt wurde, der auf dieses Schema verweist, werden die Daten erfasst und im Data Lake gespeichert. Anschließend können Sie Query Service verwenden, um beliebige Datensätze im Data Lake zu verbinden und die Abfrageergebnisse als neuen Datensatz zu erfassen, der für Berichte, maschinelles Lernen oder die Erfassung in das Echtzeit-Kundenprofil verwendet werden kann.

Weitere Informationen zu diesem Service finden Sie unter [Query Service – Übersicht](../query-service/home.md).

### Echtzeit-Kundenprofil {#real-time-customer-profile}

Das Echtzeit-Kundenprofil bietet ein zentralisiertes Kundenprofil für zielgerichtetes und personalisiertes Erlebnis-Management. Jedes Profil enthält Daten, die über alle Systeme hinweg aggregiert werden und verwertbare Zeitstempelkonten für Ereignisse enthalten, die den Profilsubjekt betreffen. Diese Ereignisse können in allen Systemen, die Sie mit Experience Platform verwenden, stattgefunden haben.

Das Echtzeit-Kundenprofil nutzt schemaformatierte Daten basierend auf dem [!UICONTROL Individuelles XDM-Profil] und [!UICONTROL XDM ExperienceEvent] und antwortet auf Abfragen, die auf diesen Daten basieren.

>[!NOTE]
>
>Das Echtzeit-Kundenprofil funktioniert **not** unterstützen Schemas, die auf anderen Klassen als der [!UICONTROL XDM ExperienceEvent] -Klasse.

Das System bildet für jedes Kundenprofil eine Instanz und vereint Daten einer Person zu einer „Single Source of Truth“. Diese zusammengeführten Daten werden mithilfe eines so genannten „Vereinigungsschemas“ dargestellt (auch als „Vereinigungsansicht“ bezeichnet). Ein Vereinigungsschema aggregiert die Felder aller Schemas, die dieselbe Klasse implementieren, in einem Schema. Wenn Sie ein Schema mithilfe der Benutzeroberfläche oder API erstellen, können Sie es aktivieren, damit es mit dem Echtzeit-Kundenprofil verwendet werden kann, und es zur Aufnahme in die Vereinigung mit einem Tag versehen. Das mit einem Tag versehene Schema wird dann Teil der Schemadefinition, die an das Profil übergeben wird.

As [!UICONTROL Individuelles XDM-Profil] und [!UICONTROL XDM ExperienceEvent] -Daten in den Daten-Pool aufgenommen werden, erfasst das Echtzeit-Kundenprofil alle Daten, die für seine Verwendung aktiviert wurden. Je mehr Interaktionen und Details aufgenommen werden, desto zuverlässiger werden die einzelnen Profile.

Die Daten von [!UICONTROL XDM Individual Profile] helfen bei der Kommunikation und der Aktivierung von Aktionen auf allen Kanälen und allen Adobe-Produkten. In Kombination mit umfangreichen Verhaltens- und Interaktionsdaten können diese Daten für maschinelles Lernen verwendet werden. Darüber hinaus kann die Echtzeit-Kundenprofil-API genutzt werden, um die Funktionalität von Drittanbieterlösungen, CRM-Systemen und proprietären Lösungen zu erweitern.

Weitere Informationen dazu finden Sie in der [Übersicht zum Echtzeit-Kundenprofil](../profile/home.md).

### Data Science Workspace {#data-science-workspace}

Data Science Workspace in Adobe Experience Platform nutzt maschinelles Lernen und künstliche Intelligenz, um Einblicke aus den in Experience Platform gespeicherten Daten zu gewinnen. Data Science Workspace ermöglicht es Datenwissenschaftlern, Rezepte zu erstellen, die auf [!UICONTROL Individuelles XDM-Profil] und [!UICONTROL XDM ExperienceEvent] Daten zu Kunden und deren Aktivitäten. Diese Rezepte erleichtern Vorhersagen wie Kaufneigung und empfohlene Angebote, die der Kontakt schätzen und nutzen kann.

Mit Data Science Workspace können Datenwissenschaftler einfach intelligente, auf maschinellem Lernen basierende Service-APIs erstellen. Diese Services sind mit anderen Adobe-Lösungen kompatibel, einschließlich Adobe Target und Adobe Analytics Cloud, und helfen Ihnen bei der Automatisierung personalisierter, zielgerichteter digitaler Erlebnisse.

Weitere Informationen zur Verwendung von Experience Platform-Daten zur Bereitstellung von Einblicken finden Sie in [Data Science Workspace – Übersicht](../data-science-workspace/home.md).

## Nächste Schritte und zusätzliche Ressourcen

Jetzt, da Sie die Rolle von Schemas in Experience Platform besser verstehen, können Sie beginnen, eigene Schemas zu erstellen.

Um mehr über die Prinzipien und Best Practices beim Erstellen von Schemas zu erfahren, die mit Experience Platform verwendet werden können, lesen Sie den Abschnitt [Grundlagen der Schemaaufbaus](schema/composition.md). Eine schrittweise Anleitung zum Erstellen eines Schemas finden Sie in den Tutorials zum Erstellen eines Schemas mithilfe [der API](tutorials/create-schema-api.md) oder [der Benutzeroberfläche](tutorials/create-schema-ui.md).

Sehen Sie sich das folgende Video an, um [!DNL XDM System] in Experience Platform besser zu verstehen:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
