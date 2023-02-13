---
keywords: Experience Platform;Startseite;beliebte Themen;XDM;XDM-System;XDM Individual Profile;XDM ExperienceEvent;XDM Experience Event;Experience Event;Erlebnisereignis;Feldergruppen;Feldergruppen;Feldergruppe;Feldergruppe;Erlebnisereignis;XDM ExperienceEvent;experienceEvent;experienceEvent;XDM Experienceevent;Experience-Datenmodell;Experience Data Model;Datenmodell;Data Model;Schema Registry;Schema Library;Schemabibliothek;Schema;Datensatzdaten;Zeitreihen;Time Series
solution: Experience Platform
title: XDM-System – Übersicht
description: Standardisierung und Interoperabilität sind Schlüsselkonzepte von Adobe Experience Platform. Das von Adobe unterstützte Experience-Datenmodell (XDM) ermöglicht die Standardisierung von Kundenerlebnisdaten und die Definition von Schemas für das Customer Experience Management.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: ht
source-wordcount: '2087'
ht-degree: 100%

---

# XDM-System – Übersicht

Standardisierung und Interoperabilität sind Schlüsselkonzepte von Adobe Experience Platform. Das von Adobe unterstützte [!DNL Experience Data Model] (XDM) ermöglicht die Standardisierung von Kundenerlebnisdaten und die Definition von Schemas für das Customer Experience Management.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Dieses Modell bietet allgemeine Strukturen und Definitionen, anhand derer jede beliebige Anwendung mit Platform-Diensten kommunizieren kann. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in ein gemeinsames System integriert werden, wodurch Erkenntnisse schneller und besser integriert verfügbar werden. Sie können wertvolle Einblicke durch Kundenaktionen gewinnen, Zielgruppen mithilfe von Segmenten definieren und Kundenattribute zur Personalisierung verwenden.

XDM ist das zugrunde liegende System, auf Basis dessen Adobe Experience Cloud als Teil von Experience Platform die richtige Botschaft der richtigen Person zur richtigen Zeit auf dem passenden Kanal präsentieren kann. Das XDM-System nutzt [!DNL Experience Data Model]-Schemas, die Experience Platform-Diensten zur Verwendung bereitstehen.

Dieses Dokument gibt einen Überblick über die Rolle des XDM-Systems in Experience Platform.

## XDM-Schemas

Schemas dienen in Experience Platform zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, deren Bedeutung beizubehalten und somit Wert aus Daten zu ziehen.

Bevor Daten in Platform aufgenommen werden können, muss ein Schema erstellt werden, das die Datenstruktur beschreibt und den Datentyp entsprechend des jeweiligen Feldes einschränkt. Schemas bestehen aus einer Basisklasse und keiner oder mehreren Schema-Feldergruppen.

Weitere Informationen zum Schemaaufbaumodell, einschließlich Planungsgrundsätzen und Best Practices, finden Sie in den [Grundlagen des Schemaaufbaus](schema/composition.md).

### Standardmäßige XDM-Komponenten

XDM bietet eine Sammlung von standardmäßigen Feldergruppen und Datentypen, mit denen gängige Konzepte und Anwendungsfälle in verschiedenen Branchen abgedeckt werden. Sie können diese Komponenten in Experience Platform nach Branchen filtern, sodass Sie schnell und sicher Schemas erstellen können, die optimal zu Ihren speziellen Geschäftsanforderungen passen.

Beim Erstellen von Schemas in der Experience Platform-Benutzeroberfläche werden die aufgelistete Feldergruppen mit einer Beliebtheitsmetrik angezeigt. Diese Metrik wird durch die Häufigkeit bestimmt, mit der andere Platform-Benutzer die jeweilige Feldergruppe in ihren Schemas verwenden. Je höher die Zahl ist, desto beliebter ist die Feldergruppe. Standardmäßig werden die Ergebnisse von den beliebtesten zu den am wenigsten beliebten Ergebnissen gereiht, sodass Sie über die Datenmodellierungstrends in Ihrer Branche auf dem Laufenden bleiben.

![Beliebtheit der Feldergruppen](./images/overview/popularity.png)

### [!DNL Schema Library]

Experience Platform stellt eine Benutzeroberfläche und RESTful-API bereit, über die Sie alle mit einem Schema in Zusammenhang stehenden Ressourcen in der **[!DNL Schema Library]** von Experience Platform anzeigen und verwalten können. Die [!DNL Schema Library] enthält standardmäßige XDM-Komponenten, die Ihnen von Adobe zur Verfügung gestellt werden, sowie Ressourcen von Experience Platform-Partnern und Anbietern, deren Anwendungen Sie verwenden.

Durch Verwendung der [!DNL Schema Registry API] oder des Arbeitsbereichs [!UICONTROL Schemas] in der Platform-Benutzeroberfläche können Sie auch neue, unternehmensspezifische Schemas und Ressourcen erstellen und verwalten.

Weitere Informationen zur Verwaltung und Interaktion mit Schemas in Platform finden Sie in der folgenden Dokumentation:

* [Handbuch zur XDM-Benutzeroberfläche](./ui/overview.md)
* [Handbuch zur Schema Registry-API](./api/overview.md)

## Datenverhalten im XDM-System {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="Datenverhalten"
>abstract="Die zur Verwendung in Experience Platform bestimmten Daten sind in drei Verhaltenstypen unterteilt: Datensatz, Zeitreihen und Ad-hoc-Analysen. Datensatzschemas liefern Informationen über die Attribute eines Subjekts, während Zeitreihenschemas eine Momentaufnahme des Systems zum Zeitpunkt der Durchführung einer Aktion erfassen. Ad-hoc-Schemas erfassen Felder, die Namespaces sind und nur von einem Datensatz verwendet werden können. Weitere Informationen zu Datenverhalten in Platform finden Sie in der Dokumentation."

Daten, die in Experience Platform verwendet werden können, sind in drei Verhaltenstypen unterteilt:

* **Datensatz**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt kann ein Unternehmen oder eine Person sein.
* **Zeitreihe**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt bereit, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.
* **Ad-hoc**: Erfasst Felder, die sich in einem Namespace befinden und nur von einem einzigen Datensatz verwendet werden. Ad-hoc-Schemas werden in verschiedenen Datenaufnahme-Workflows für Experience Platform verwendet, einschließlich der Aufnahme von CSV-Dateien und der Erstellung bestimmter Arten von Quellverbindungen.

Alle XDM-Schemas beschreiben Daten, die als Datensatz oder Zeitreihe kategorisiert werden können. Das Datenverhalten eines Schemas wird durch die Klasse des Schemas definiert, die einem Schema bei dessen Erstellung zugewiesen wird. XDM-Klassen beschreiben die Mindestanzahl von Eigenschaften, die ein Schema enthalten muss, um ein bestimmtes Datenverhalten zu haben.

Obwohl Sie in der [!DNL Schema Registry] Ihre eigenen Klassen definieren können, wird empfohlen, die Standardklassen **[!UICONTROL XDM Individual Profile]** für Datensatzdaten und **[!UICONTROL XDM ExperienceEvent]** für Zeitreihedaten zu verwenden. Diese Klassen werden weiter unten detaillierter beschrieben.

>[!NOTE]
>
>Es gibt keine Standardklassen, die auf dem Ad-hoc-Verhalten basieren. Ad-hoc-Schemas werden automatisch von den Platform-Prozessen generiert, die sie nutzen. Sie können aber auch [manuell mithilfe der Schema Registry-API erstellt wurde](./tutorials/ad-hoc.md).

### [!UICONTROL XDM Individual Profile] {#xdm-individual-profile}

[!UICONTROL XDM Individual Profile] ist eine auf einem Datensatz basierende Klasse, die eine einzige Repräsentation der Attribute sowohl identifizierter als auch teilweise identifizierter Subjekte darstellt. Hochgradig identifizierte Profile können für die persönliche Kommunikation oder zielgerichtete Interaktionen verwendet werden und detaillierte persönliche Informationen wie Name, Geschlecht, Geburtsdatum, Ort und Kontaktinformationen, einschließlich Telefonnummern und E-Mail-Adressen, enthalten.

Weniger identifizierte Profile bestehen möglicherweise nur aus anonymen Verhaltenssignalen wie Browser-Cookies. In diesem Fall wird mithilfe der wenigen Profildaten eine Informationsbasis geschaffen, in der die Interessen und Präferenzen des anonymen Profils erfasst und gespeichert werden. Die Anzahl dieser Daten kann im Laufe der Zeit anwachsen, wenn sich das Subjekt für Benachrichtigungen, Abonnements, Käufe usw. entscheidet. Dieses Anwachsen von Profilattributen kann als Ergebnis schließlich ein identifiziertes Subjekt haben und ein höheres Maß an zielgerichteter Interaktion ermöglichen.

Je mehr Daten zu einem Profil gesammelt werden, desto zuverlässiger wird der Bestand an personenbezogenen Daten, Identifizierungsinformationen, Kontaktdaten und Kommunikationsvorlieben einer Person.

Weitere Informationen zur Struktur und zum Anwendungsfall der Felder einer Klasse erhalten Sie im Referenzhandbuch [[!UICONTROL XDM Individual Profile]](./classes/individual-profile.md).

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent ist eine zeitreihenbasierte Klasse, mit der der Status des Systems beim Eintreten eines Ereignisses (oder einer Reihe von Ereignissen) erfasst wird, einschließlich des Zeitpunkts und der Identität des betroffenen Subjekts. Erlebnisereignisse sind unveränderliche, sachliche Aufzeichnungen darüber, was zu diesem Zeitpunkt geschehen ist, und stellen das dar, was ohne Aggregation oder Interpretation passiert ist. Sie sind für die Zeit-Domain-Analyse von entscheidender Bedeutung, da sie zur Analyse von Änderungen, die in einem bestimmten Zeitfenster auftreten, und zum Vergleich zwischen mehreren Zeitfenstern verwendet werden können, um Trends zu verfolgen.

Erlebnisereignisse können entweder explizit oder implizit sein. Explizite Ereignisse sind unmittelbar erkennbare menschliche Aktionen, die zu einem bestimmten Zeitpunkt in einer Journey stattfinden. Implizite Ereignisse sind Ereignisse, die ohne direkte menschliche Aktion ausgelöst werden, sich aber auf eine Person beziehen. Beispiele für implizite Ereignisse sind der planmäßige Versand von E-Mail-Newslettern oder die Akkuspannung, die einen bestimmten Schwellenwert erreicht.

Es ist zwar nicht einfach, alle Ereignisse in allen Datenquellen zu kategorisieren, doch ist es äußerst nützlich, ähnliche Ereignisse zu ähnlichen Typen zusammenzufassen, um sie verarbeiten zu können.

![ExperienceEvent Customer Journey](images/overview/experience-event-journey.png)

Weitere Informationen zur Struktur und zum Anwendungsfall der Felder einer Klasse erhalten Sie im Referenzhandbuch [[!UICONTROL XDM ExperienceEvent]](./classes/experienceevent.md).

## XDM-Schemas und Experience Platform-Services

Experience Platform ist schemaunabhängig, d. h. jedes Schema, das dem XDM-Standard entspricht, wird Platform-Services zur Verfügung gestellt. Die Verwendung von Schemas durch verschiedene Platform-Services wird weiter unten ausführlicher beschrieben.

### Catalog Service, Datenaufnahme und Data Lake

Catalog Service ist das „System of Record“ für Experience Platform-Medienelemente und deren zugehörige Schemas. Catalog Service enthält nicht die eigentlichen Datendateien oder Ordner, sondern die Metadaten und Beschreibungen dieser Dateien und Ordner.

Die Katalogdaten werden im Data Lake gespeichert, einem hochgradig granularen Datenspeicher, der unabhängig von Herkunft oder Dateiformat alle von Platform verwalteten Daten enthält.

Um mit der Aufnahme von Daten in Experience Platform zu beginnen, können Sie mithilfe von Catalog Service einen Datensatz erstellen. Der Datensatz verweist auf ein XDM-Schema, das die Struktur der aufzunehmenden Daten beschreibt. Wenn ein Datensatz ohne Schema erstellt wird, leitet Experience Platform ein „festgestelltes Schema“ ab, indem Typ und Inhalt der erfassten Datenfelder überprüft werden. Datensätze werden dann im Katalog getrackt und im Data Lake gemeinsam mit den Schemas und festgestellten Schemas, auf denen sie basieren, gespeichert.

Weitere Informationen zum Katalog finden Sie im Abschnitt [Catalog Service – Übersicht](../catalog/home.md). Weitere Informationen zur Datenaufnahme in Adobe Experience Platform finden Sie unter [Datenaufnahme – Übersicht](../ingestion/home.md).

### Query Service

Mit Query Service von Adobe Experience Platform können Sie SQL-Standarddaten zur Abfrage von Experience Platform-Daten verwenden, um viele verschiedene Anwendungsfälle zu unterstützen.

Nachdem ein Schema konzipiert und ein Datensatz erstellt wurde, der auf dieses Schema verweist, werden Daten aufgenommen und im Data Lake gespeichert. Mit Query Service können Sie beliebige Datensätze in den Data Lake einbinden und die Abfrageergebnisse als neuen Datensatz erfassen, der beim Reporting, für das maschinelle Lernen oder zur Aufnahme in das Echtzeit-Kundenprofil verwendet werden kann.

Weitere Informationen zu diesem Service finden Sie unter [Query Service – Übersicht](../query-service/home.md).

### Echtzeit-Kundenprofil

Das Echtzeit-Kundenprofil bietet ein zentralisiertes Kundenprofil für zielgerichtetes und personalisiertes Erlebnis-Management. Jedes Profil enthält Daten, die systemübergreifend aggregiert werden, sowie relevante, mit einem Zeitstempel versehene Ereignisse, an denen die entsprechende Person beteiligt ist und die in einem der Systeme stattfanden, die Sie in Verbindung mit Experience Platform verwenden.

Das Echtzeit-Kundenprofil nutzt schemaformatierte Daten basierend auf den Klassen [!UICONTROL XDM-Kontaktprofil] und [!UICONTROL XDM ExperienceEvent] und reagiert auf Abfragen, die auf diesen Daten basieren. Das Profil unterstützt nicht die Verwendung von Schemas, die auf anderen Klassen basieren.

Das System bildet für jedes Kundenprofil eine Instanz und vereint Daten einer Person zu einer „Single Source of Truth“. Diese zusammengeführten Daten werden mithilfe eines so genannten „Vereinigungsschemas“ dargestellt (auch als „Vereinigungsansicht“ bezeichnet). Ein Vereinigungsschema aggregiert die Felder aller Schemas, die dieselbe Klasse in ein einziges Schema implementieren.  Wenn Sie ein Schema mithilfe der Benutzeroberfläche oder API erstellen, können Sie es aktivieren, damit es mit dem Echtzeit-Kundenprofil verwendet werden kann, und es zur Aufnahme in die Vereinigung mit einem Tag versehen. Das mit einem Tag versehene Schema wird dann Teil der Schemadefinition, die an das Profil übergeben wird.

Wenn [!UICONTROL XDM-Kontaktprofil]- und [!UICONTROL XDM ExperienceEvent]-Daten in den Data Lake aufgenommen werden, nimmt das Echtzeit-Kundenprofil alle Daten auf, die für dessen Verwendung aktiviert wurden. Je mehr Interaktionen und Details aufgenommen werden, desto zuverlässiger werden die einzelnen Profile.

Die Daten von [!UICONTROL XDM Individual Profile] helfen bei der Kommunikation und der Aktivierung von Aktionen auf allen Kanälen und allen Adobe-Produkten. In Kombination mit umfangreichen Verhaltens- und Interaktionsdaten können diese Daten für maschinelles Lernen verwendet werden. Darüber hinaus kann die Echtzeit-Kundenprofil-API genutzt werden, um die Funktionalität von Drittanbieterlösungen, CRM-Systemen und proprietären Lösungen zu erweitern.

Weitere Informationen dazu finden Sie in der [Übersicht zum Echtzeit-Kundenprofil](../profile/home.md).

### Data Science Workspace

Data Science Workspace in Adobe Experience Platform nutzt maschinelles Lernen und künstliche Intelligenz, um Einblicke aus den in Experience Platform gespeicherten Daten zu gewinnen. Data Science Workspace ermöglicht es Datenwissenschaftlern, Rezepte zu erstellen, die auf Daten zu Kunden und ihren Aktivitäten basieren, die von [!UICONTROL XDM Individual Profile] und [!UICONTROL XDM ExperienceEvent] stammen. Dies erleichtert Prognosen z. B. zu Kaufneigung und empfohlenen Angeboten, die die jeweilige Person schätzt und nutzt.

Mit Data Science Workspace können Datenwissenschaftler einfach intelligente, auf maschinellem Lernen basierende Service-APIs erstellen. Diese Services sind mit anderen Adobe-Lösungen kompatibel, einschließlich Adobe Target und Adobe Analytics Cloud, und helfen Ihnen bei der Automatisierung personalisierter, zielgerichteter digitaler Erlebnisse.

Weitere Informationen zur Verwendung von Experience Platform-Daten zur Bereitstellung von Einblicken finden Sie in [Data Science Workspace – Übersicht](../data-science-workspace/home.md).

## Nächste Schritte und zusätzliche Ressourcen

Jetzt, da Sie die Rolle von Schemas in Experience Platform besser verstehen, können Sie beginnen, eigene Schemas zu erstellen.

Um mehr über die Prinzipien und Best Practices beim Erstellen von Schemas zu erfahren, die mit Experience Platform verwendet werden können, lesen Sie den Abschnitt [Grundlagen der Schemaaufbaus](schema/composition.md). Eine schrittweise Anleitung zum Erstellen eines Schemas finden Sie in den Tutorials zum Erstellen eines Schemas mithilfe [der API](tutorials/create-schema-api.md) oder [der Benutzeroberfläche](tutorials/create-schema-ui.md).

Sehen Sie sich das folgende Video an, um [!DNL XDM System] in Experience Platform besser zu verstehen:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
