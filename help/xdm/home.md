---
keywords: Experience Platform;Startseite;beliebte Themen;XDM;XDM-System;XDM-individuelles Profil;XDM ExperienceEvent;XDM ExperienceEvent;Erlebnisereignis;Feldergruppen;Feldergruppen;Feldergruppe;Feldergruppe;Erlebnisereignis;XDM ExperienceEvent;experienceEvent;experienceEvent;XDM Experience Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell Registrierung;Schema Registry;Schema Library;Schema;Schema;Datensatzdaten;Zeitreihen;Zeitreihen
solution: Experience Platform
title: XDM-Systemübersicht
topic-legacy: overview
description: Standardisierung und Interoperabilität sind Schlüsselkonzepte von Adobe Experience Platform. Das von Adobe unterstützte Experience-Datenmodell (XDM) ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Customer Experience Management zu definieren.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 9fda5dad7b7e29c88598ff299c26277a015277a6
workflow-type: tm+mt
source-wordcount: '1993'
ht-degree: 9%

---

# XDM-System – Übersicht

>[!NOTE]
>
>Der Begriff &quot;Mixin&quot;wurde zum Schema &quot;Feldergruppe&quot;aktualisiert, um das Verständnis zu fördern. Feldergruppen sind wiederverwendbare Feldsätze zur Unterstützung von geschäftlichen Anwendungsfällen. Diese Änderung wird jetzt in der Schema Registry-API, der Adobe Experience Platform-Benutzeroberfläche und in der gesamten Platform-Dokumentation widergespiegelt.

Standardisierung und Interoperabilität sind Schlüsselkonzepte von Adobe Experience Platform. Das von Adobe unterstützte [!DNL Experience Data Model] (XDM)-System ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es bietet allgemeine Strukturen und Definitionen, die es jeder Anwendung ermöglichen, mit Platform-Diensten zu kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Einblicke schneller und besser integriert liefern kann. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Kundenzielgruppen über Segmente definieren und Kundenattribute zu Personalisierungszwecken ausdrücken.

XDM ist ein grundlegendes Framework, das es Adobe Experience Cloud ermöglicht, basierend auf Experience Platform, die richtige Botschaft zum richtigen Zeitpunkt an die richtige Person auf dem richtigen Kanal zu senden. Das XDM-System, die Methode, auf der die Experience Platform basiert, stellt [!DNL Experience Data Model]-Schemas für die Verwendung durch Platform-Dienste bereit.

Dieses Dokument bietet einen Überblick über die Rolle des XDM-Systems in Experience Platform.

## XDM-Schemata

Schemas dienen in Experience Platform zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, die Bedeutung beizubehalten und somit Wert aus Daten zu ziehen.

Bevor Daten in Platform erfasst werden können, muss ein Schema erstellt werden, das die Datenstruktur beschreibt und Einschränkungen für den Datentyp enthält, der in jedem Feld enthalten sein kann. Schemas bestehen aus einer Basisklasse und keiner oder mehr Schemafeldgruppen.

Weitere Informationen zum Schema-Kompositionsmodell, einschließlich Designprinzipien und Best Practices, finden Sie in den [Grundlagen der Schemakomposition](schema/composition.md).

### Standard-XDM-Komponenten

XDM bietet eine robuste Sammlung von Standardfeldgruppen und -datentypen, mit denen gängige Konzepte und Anwendungsfälle in verschiedenen Branchen erfasst werden sollen. Mit Experience Platform können Sie diese Komponenten nach Branchen filtern, sodass Sie schnell und sicher Schemata erstellen können, die Ihre speziellen Geschäftsanforderungen am besten unterstützen.

Beim Erstellen von Schemas in der Experience Platform-Benutzeroberfläche werden aufgelistete Feldgruppen mit einer Beliebtheitsmetrik angezeigt. Diese Metrik wird durch die Häufigkeit bestimmt, mit der andere Platform-Benutzer die Feldergruppe in ihren Schemas verwenden. Je höher die Zahl, desto beliebter ist die Feldergruppe. Die Ergebnisse werden standardmäßig von den beliebtesten zu den am wenigsten beliebten Ergebnissen angezeigt und halten Sie über die Datenmodellierungstrends in Ihrer Branche auf dem Laufenden.

![Feldgruppenbeliebtheit](./images/overview/popularity.png)

### [!DNL Schema Library]

Experience Platform bietet eine Benutzeroberfläche und RESTful-API, über die Sie alle schemabezogenen Ressourcen in der Experience Platform **[!DNL Schema Library]** anzeigen und verwalten können. Die [!DNL Schema Library] enthält standardmäßige XDM-Komponenten, die Ihnen nach Adobe zur Verfügung gestellt werden, sowie Ressourcen von Experience Platform-Partnern und Anbietern, deren Anwendungen Sie verwenden.

Mit dem Arbeitsbereich [!DNL Schema Registry API] oder [!UICONTROL Schemas] in der Platform-Benutzeroberfläche können Sie auch neue Schemata und Ressourcen erstellen und verwalten, die für Ihr Unternehmen spezifisch sind.

Weitere Informationen zur Verwaltung und Interaktion mit Schemata in Platform finden Sie in der folgenden Dokumentation:

* [Handbuch zur XDM-Benutzeroberfläche](./ui/overview.md)
* [Handbuch zur Schema Registry-API](./api/overview.md)

## Datenverhalten im XDM-System {#data-behaviors}

Daten, die in Experience Platform verwendet werden sollen, sind in zwei Verhaltenstypen unterteilt:

* **Aufzeichnen von Daten**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt könnte eine Organisation oder eine Einzelperson sein.
* **Zeitreihendaten**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt bereit, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

Alle XDM-Schemas beschreiben Daten, die als Datensatz- oder Zeitreihen kategorisiert werden können. Das Datenverhalten eines Schemas wird durch die Klasse des Schemas definiert, die einem Schema beim ersten Erstellen zugewiesen wird. XDM-Klassen beschreiben die kleinste Anzahl von Eigenschaften, die ein Schema enthalten muss, um ein bestimmtes Datenverhalten darzustellen.

Sie können zwar innerhalb von [!DNL Schema Registry] eigene Klassen definieren, es wird jedoch empfohlen, die bevorzugten Klassen **[!UICONTROL XDM Individual Profile]** und **[!UICONTROL XDM ExperienceEvent]** für Datensatz- und Zeitreihendaten zu verwenden. Diese Klassen werden nachfolgend detaillierter beschrieben.

### [!UICONTROL XDM Individual Profile] {#xdm-individual-profile}

[!UICONTROL XDM Individual ] Profile ist eine auf einem Datensatz basierende Klasse, die eine eindeutige Darstellung der Attribute sowohl identifizierter als auch teilweise identifizierter Subjekte bildet. Hoch identifizierte Profile können für persönliche Kommunikation oder zielgerichtete Interaktionen verwendet werden und detaillierte persönliche Informationen wie Name, Geschlecht, Geburtsdatum, Ort und Kontaktinformationen, einschließlich Telefonnummern und E-Mail-Adressen, enthalten.

Weniger identifizierte Profile können nur aus anonymen Verhaltenssignalen wie Browser-Cookies bestehen. In diesem Fall werden die spärlichen Profildaten zum Aufbau einer Informationsbasis verwendet, in der die Interessen und Voreinstellungen des anonymen Profils erfasst und gespeichert werden. Diese Kennungen können im Laufe der Zeit detaillierter werden, wenn sich der Betreff für Benachrichtigungen, Abonnements, Käufe usw. anmeldet. Diese Steigerung der Profilattribute kann schließlich zu einem identifizierten Subjekt führen und ein höheres Maß an zielgerichteter Interaktion ermöglichen.

Mit zunehmendem Profil wird es zu einem robusten Repository der personenbezogenen Daten, Identifizierungsinformationen, Kontaktdaten und Kommunikationseinstellungen einer Person.

Weitere Informationen zur Struktur und zum Anwendungsfall der von der Klasse bereitgestellten Felder finden Sie im Referenzhandbuch [[!UICONTROL XDM Individual Profile]](./classes/individual-profile.md) .

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent ist eine zeitreihenbasierte Klasse, mit der der Status des Systems beim Eintreten eines Ereignisses (oder einer Reihe von Ereignissen) erfasst wird, einschließlich des Zeitpunkts und der Identität des betroffenen Subjekts. Erlebnisereignisse sind unveränderlich, sachliche Aufzeichnungen darüber, was zu diesem Zeitpunkt geschehen ist, und repräsentieren das, was ohne Aggregation oder Interpretation passiert ist. Sie sind für die Zeitdomänenanalyse von entscheidender Bedeutung, da sie zur Analyse von Änderungen verwendet werden können, die in einem bestimmten Zeitfenster auftreten, und zum Vergleich zwischen mehreren Zeitfenstern, um Trends zu verfolgen.

Erlebnisereignisse können entweder explizit oder implizit sein. Explizite Ereignisse sind unmittelbar erkennbare menschliche Aktionen, die während eines bestimmten Zeitpunkts in einer Journey stattfinden. Implizite Ereignisse sind Ereignisse, die ohne direkte menschliche Aktion ausgelöst werden, sich aber immer noch auf eine Person beziehen. Beispiele für implizite Ereignisse sind der geplante Versand von E-Mail-Newslettern oder die Batteriespannung, die einen bestimmten Schwellenwert erreicht.

Zwar sind nicht alle Ereignisse leicht in alle Datenquellen kategorisiert, doch ist es äußerst nützlich, ähnliche Ereignisse nach Möglichkeit zur Verarbeitung in ähnliche Typen zu harmonisieren.

![ExperienceEvent-Kunden-Journey](images/overview/experience-event-journey.png)

Weitere Informationen zur Struktur und zum Anwendungsfall der von der Klasse bereitgestellten Felder finden Sie im Referenzhandbuch [[!UICONTROL XDM ExperienceEvent]](./classes/experienceevent.md) .

## XDM-Schemata und Experience Platform-Services

Experience Platform ist schemaunabhängig, d. h. jedes Schema, das dem XDM-Standard entspricht, wird Platform-Diensten zur Verfügung gestellt. Die Verwendung von Schemas durch verschiedene Platform-Dienste wird nachfolgend ausführlicher beschrieben.

### Catalog Service, Datenerfassung und Data Lake

Catalog Service ist das Aufzeichnungssystem für Experience Platform-Assets und die zugehörigen Schemata. Der Katalog enthält nicht die eigentlichen Datendateien oder Ordner, sondern die Metadaten und Beschreibungen dieser Dateien und Ordner.

Katalogdaten werden im Data Lake gespeichert, einem hochgradig granularen Datenspeicher, der alle von Platform verwalteten Daten enthält, unabhängig von Herkunft oder Dateiformat.

Um mit der Aufnahme von Daten in Experience Platform zu beginnen, können Sie zum Erstellen eines Datensatzes den Catalog Service verwenden. Der Datensatz verweist auf ein XDM-Schema, das die Struktur der aufzunehmenden Daten beschreibt. Wenn ein Datensatz ohne Schema erstellt wird, leitet Experience Platform ein &quot;beobachtetes Schema&quot;ab, indem Typ und Inhalt der erfassten Datenfelder überprüft werden. Datensätze werden dann im Katalog nachverfolgt und im Data Lake neben den Schemas und beobachteten Schemas gespeichert, auf denen sie basieren.

Weitere Informationen zu Catalog finden Sie unter [Catalog Service - Übersicht](../catalog/home.md). Weitere Informationen zur Datenerfassung in Adobe Experience Platform finden Sie unter [Datenerfassung - Übersicht](../ingestion/home.md).

### Query Service

Mit Adobe Experience Platform Query Service können Sie SQL-Standarddaten zur Abfrage von Experience Platform-Daten verwenden, um viele verschiedene Anwendungsfälle zu unterstützen.

Nachdem ein Schema erstellt und ein Datensatz erstellt wurde, der auf dieses Schema verweist, werden die Daten erfasst und im Data Lake gespeichert. Mithilfe von Query Service können Sie beliebige Datensätze in den Data Lake einbinden und die Abfrageergebnisse als neuen Datensatz erfassen, der für Berichte, maschinelles Lernen oder die Aufnahme in das Echtzeit-Kundenprofil verwendet werden kann.

Weitere Informationen zum Dienst finden Sie in der [Query Service - Übersicht](../query-service/home.md) .

### Echtzeit-Kundenprofil

Das Echtzeit-Kundenprofil bietet ein zentralisiertes Kundenprofil für zielgerichtetes und personalisiertes Erlebnismanagement. Jedes Profil enthält Daten, die systemübergreifend aggregiert werden, sowie umsetzbare Zeitstempelkonten für Ereignisse, an denen die Person beteiligt ist, die in einem der mit Experience Platform verwendeten Systeme stattgefunden haben.

Das Echtzeit-Kundenprofil nutzt schemaformatierte Daten basierend auf den Klassen [!UICONTROL XDM Individual Profile] und [!UICONTROL XDM ExperienceEvent] und reagiert auf Abfragen, die auf diesen Daten basieren. Profil unterstützt nicht die Verwendung von Schemas, die auf anderen Klassen basieren.

Das System verwaltet eine Instanz jedes Kundenprofils und führt Daten zu einer &quot;einzigen Quelle der Wahrheit&quot;für die Person zusammen. Diese einheitlichen Daten werden mithilfe eines so genannten &quot;Vereinigungsschemas&quot;(manchmal auch als &quot;Vereinigungsansicht&quot;bezeichnet) dargestellt. Ein Vereinigungsschema aggregiert die Felder aller Schemas, die dieselbe Klasse implementieren, in einem Schema.  Beim Erstellen eines Schemas mithilfe der Benutzeroberfläche oder API können Sie das Schema zur Verwendung mit dem Echtzeit-Kundenprofil aktivieren und es zur Aufnahme in die Vereinigung taggen. Das getaggte Schema nimmt dann an der Schemadefinition teil, die an Profil übergeben wird.

Da [!UICONTROL XDM Individual Profile] und [!UICONTROL XDM ExperienceEvent] Daten in den Data Lake aufgenommen werden, erfasst das Echtzeit-Kundenprofil alle Daten, die für seine Verwendung aktiviert wurden. Je mehr Interaktionen und Details erfasst werden, desto robuster werden einzelne Profile.

[!UICONTROL XDM Individual ] ProfileData unterstützt Sie bei der Information und Aktivierung von Aktionen über alle Kanäle oder Adobe-Produktintegrationen hinweg. In Verbindung mit einer umfangreichen Geschichte von Verhaltens- und Interaktionsdaten können diese Daten für maschinelles Lernen verwendet werden. Die Echtzeit-Kundenprofil-API kann auch verwendet werden, um die Funktionalität von Drittanbieterlösungen, CRMs und proprietären Lösungen zu erweitern.

Weitere Informationen finden Sie unter [Übersicht über das Echtzeit-Kundenprofil](../profile/home.md) .

### Data Science Workspace

Data Science Workspace in Adobe Experience Platform nutzt maschinelles Lernen und künstliche Intelligenz, um Einblicke aus den in Experience Platform gespeicherten Daten zu gewinnen. Data Science Workspace ermöglicht es Datenwissenschaftlern, Rezepte zu erstellen, die auf [!UICONTROL XDM Individual Profile] und [!UICONTROL XDM ExperienceEvent] Daten über Kunden und ihre Aktivitäten basieren. Dies erleichtert Prognosen wie Kaufneigung und empfohlene Angebote, die der Kontakt wahrscheinlich schätzen und verwenden wird.

Mit Data Science Workspace können Datenwissenschaftler einfach intelligente Service-APIs erstellen, die auf maschinellem Lernen basieren. Diese Dienste arbeiten mit anderen Adobe-Lösungen, einschließlich Adobe Target und Adobe Analytics Cloud, zusammen, um Ihnen bei der Automatisierung personalisierter, zielgerichteter digitaler Erlebnisse zu helfen.

Weitere Informationen zur Verwendung von Experience Platform-Daten zur Unterstützung von Einblicken finden Sie in der [Übersicht über Data Science Workspace](../data-science-workspace/home.md).

## Nächste Schritte und zusätzliche Ressourcen

Jetzt, da Sie die Rolle von Schemas in der ganzen Experience Platform besser verstehen, können Sie beginnen, sich selbst zu komponieren.

Um mehr über Design-Prinzipien und Best Practices beim Erstellen von Schemas zu erfahren, die mit Experience Platform verwendet werden sollen, lesen Sie zunächst die [Grundlagen der Schemakomposition](schema/composition.md). Eine schrittweise Anleitung zum Erstellen eines Schemas finden Sie in den Tutorials zum Erstellen eines Schemas [mithilfe der API](tutorials/create-schema-api.md) oder [mithilfe der Benutzeroberfläche](tutorials/create-schema-ui.md).

Sehen Sie sich das folgende Video an, um Ihr Verständnis von [!DNL XDM System] in Experience Platform zu vertiefen:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
