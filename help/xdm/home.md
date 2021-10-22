---
keywords: Experience Platform;home;beliebte Themen;XDM;XDM;XDM-Profil;XDM ExperienceEvent;XDM Experience-Ereignis;Experience-Event;Experience-Ereignis;Field-groups;Feldgruppe;Feldgruppe;Experience-Ereignis;XDM Experience-Ereignis;XDM-Experience-Event;Experience-Event;XDM-Erlebnis;Erlebnisdatenmodell;Erlebnisdatenmodell;Erlebnisdatenmodell;Datenmodell;Schema-Registrierung;Schema-Registrierung;Schema-Bibliothek;Schema-Bibliothek;Schema;Datensatz;Zeitreihen;Zeitreihen
solution: Experience Platform
title: XDM-Systemübersicht
topic-legacy: overview
description: Normung und Interoperabilität sind Schlüsselkonzepte für Adobe Experience Platform. Das von Adobe unterstützte Experience-Datenmodell (XDM) ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Customer Experience Management zu definieren.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 196147e7691010707953561c110a3934fec8ba1b
workflow-type: tm+mt
source-wordcount: '1947'
ht-degree: 10%

---

# XDM-System – Übersicht

Normung und Interoperabilität sind Schlüsselkonzepte für Adobe Experience Platform. Das von Adobe unterstützte [!DNL Experience Data Model] (XDM)-System ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es enthält gemeinsame Strukturen und Definitionen, die es jeder Anwendung ermöglichen, mit Platform Services zu kommunizieren. Durch die Einhaltung der XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und integrierter liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Audiencen durch Segmente definieren und Kundenattribute für Personalisierungszwecke ausdrücken.

XDM ist der Grundgerüst, der es Adobe Experience Cloud, angetrieben von der Experience Platform, ermöglicht, die richtige Botschaft an die richtige Person, am richtigen Kanal, genau zum richtigen Zeitpunkt zu senden. Die Methodik, auf der die Experience Platform basiert, XDM-System, operiert [!DNL Experience Data Model] Schema für die Nutzung durch Plattformdienste.

Dieses Dokument gibt einen Überblick über die Rolle des XDM-Systems in der Experience Platform.

## XDM-Schemata

Schemas dienen in Experience Platform zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, die Bedeutung beizubehalten und somit Wert aus Daten zu ziehen.

Bevor Daten in die Plattform integriert werden können, muss ein Schema zusammengestellt werden, das die Datenstruktur beschreibt und Beschränkungen für den Datentyp enthält, der in jedem Feld enthalten sein kann. Schema bestehen aus einer Basisklasse und null oder mehr Schema-Feldgruppen.

Weitere Informationen zum Modell der Zusammensetzung des Schemas, einschließlich Designgrundsätze und bewährter Verfahren, finden Sie im [Grundlagen der Zusammensetzung des Schemas](schema/composition.md).

### Standard-XDM-Komponenten

XDM bietet eine robuste Sammlung von Standard-Feldgruppen und Datentypen, die dazu dienen, gemeinsame Konzepte zu erfassen und Fälle in verschiedenen Branchen zu verwenden. Experience Platform ermöglicht es Ihnen, diese Komponenten nach Branchen zu filtern und so schnell und sicher Schema zu erstellen, die Ihre spezifischen geschäftlichen Anforderungen am besten erfüllen.

Beim Erstellen von Schemas in der Benutzeroberfläche der Experience Platform werden die aufgelisteten Feldgruppen mit einer Beliebungsmetrik angezeigt. Diese Metrik wird durch die Häufigkeit bestimmt, mit der andere Plattformbenutzer die Feldgruppe in ihren Schemas verwenden. Je höher die Zahl, desto beliebter ist die Feldgruppe. Die Ergebnisse werden standardmäßig von den beliebtesten bis zu den am wenigsten populären angezeigt und halten Sie über die Datenmodellierungstrends in Ihrer Branche auf dem Laufenden.

![Feldgruppennutzung](./images/overview/popularity.png)

### [!DNL Schema Library]

Experience Platform bietet eine Benutzeroberfläche und RESTful API, über die Sie alle Schema-bezogenen Ressourcen in der Experience Platform Ansicht und verwalten können. **[!DNL Schema Library]**. Die [!DNL Schema Library] enthält standardmäßige XDM-Komponenten, die Ihnen nach Adobe zur Verfügung gestellt werden, sowie Ressourcen von Experience Platform-Partnern und Anbietern, deren Anwendungen Sie verwenden.

Verwenden der [!DNL Schema Registry API] oder [!UICONTROL Schemas] Im Arbeitsbereich der Platform UI können Sie außerdem neue Schema und Ressourcen erstellen und verwalten, die für Ihr Unternehmen eindeutig sind.

Weitere Informationen zur Verwaltung und Interaktion mit Schemas in Plattformen finden Sie in der folgenden Dokumentation:

* [XDM-UI-Handbuch](./ui/overview.md)
* [Handbuch zur Schema Registry-API](./api/overview.md)

## Datenverhalten im XDM-System {#data-behaviors}

Daten, die in Experience Platform verwendet werden sollen, sind in zwei Verhaltenstypen unterteilt:

* **Aufzeichnen von Daten**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt könnte eine Organisation oder eine Einzelperson sein.
* **Zeitreihendaten**: Bietet eine Momentaufnahme des Systems zum Zeitpunkt der direkten oder indirekten Aktion eines Datensatzbetreibers.

Alle XDM-Schemas beschreiben Daten, die als Datensatz- oder Zeitreihen kategorisiert werden können. Das Datenverhalten eines Schemas wird durch die Klasse des Schemas definiert, die einem Schema beim ersten Erstellen zugewiesen wird. XDM-Klassen beschreiben die kleinste Anzahl von Eigenschaften, die ein Schema enthalten muss, um ein bestimmtes Datenverhalten darzustellen.

Sie können jedoch eigene Klassen innerhalb der [!DNL Schema Registry]wird empfohlen, dass Sie die bevorzugten Klassen verwenden **[!UICONTROL Individuelles XDM-Profil]** und **[!UICONTROL XDM ExperienceEvent]** für Datensatz- und Zeitreihendaten. Diese Klassen sind im Folgenden näher erläutert.

### [!UICONTROL Individuelles XDM-Profil] {#xdm-individual-profile}

[!UICONTROL Individuelles XDM-Profil] ist eine auf Aufzeichnungen basierende Klasse, die eine einmalige Darstellung der Attribute sowohl identifizierter als auch nur teilweise identifizierter Fächer darstellt. Profil, die als solche gekennzeichnet sind, können für persönliche Kommunikation oder zielgerichtete Interaktionen verwendet werden und detaillierte personenbezogene Daten wie Name, Geschlecht, Geburtsdatum, Ort und Kontaktdaten, einschließlich Telefonnummern und E-Mail-Adressen, enthalten.

Weniger identifizierte Profil können nur aus anonymen Verhaltenssignalen wie Browsercookies bestehen. In diesem Fall werden die spärlichen Profil-Daten verwendet, um eine Informationsbasis zu schaffen, in der die Interessen und Vorlieben des anonymen Profils erfasst und gespeichert werden. Diese Kennungen können im Laufe der Zeit detaillierter werden, da sich der Betreffende bei Benachrichtigungen, Abonnements, Einkäufen usw. anmeldet. Dieser Anstieg der Attribute des Profils kann schließlich zu einem bestimmten Thema führen und ein höheres Maß an gezieltem Engagement ermöglichen.

Mit zunehmendem Profil wird es zu einem robusten Archiv der persönlichen Daten, Identifizierungsinformationen, Kontaktdaten und Kommunikationseinstellungen einer Person.

Siehe [[!UICONTROL Individuelles XDM-Profil] Referenzhandbuch](./classes/individual-profile.md) für weitere Informationen über die Struktur und den Verwendungsfall der von der Klasse bereitgestellten Felder.

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent ist eine auf Zeitreihen basierende Klasse, die dazu verwendet wird, den Systemstatus zu erfassen, wenn ein Ereignis (oder eine Reihe von Ereignissen) auftritt, einschließlich des Zeitpunkts und der Identität des Betreffenden. Die Ereignis der Erfahrung sind unveränderlich, die Fakten über das, was zu diesem Zeitpunkt geschehen ist, stellen dar, was ohne Aggregation oder Interpretation passiert ist. Sie sind von entscheidender Bedeutung für die Analyse von Zeitbereichen, da sie zur Analyse von Änderungen in einem bestimmten Zeitfenster und zum Vergleich zwischen mehreren Zeitfenstern verwendet werden können, um Trends zu verfolgen.

Experience Ereignisses kann entweder explizit oder implizit sein. Explizite Ereignisse sind direkt beobachtbare menschliche Handlungen, die während eines bestimmten Punktes in einer Journey stattfinden. Implizite Ereignisse sind Ereignisse, die ohne direkte menschliche Handlungen aufgezogen werden, aber immer noch mit einer Person in Verbindung stehen. Beispiele impliziter Ereignis können das geplante Versenden von E-Mail-Newslettern oder die Akkulaufspannung bis zu einem bestimmten Schwellenwert sein.

Obwohl nicht alle Ereignis leicht in alle Datenquellen eingeteilt werden können, ist es äußerst nützlich, ähnliche Ereignis für die Verarbeitung nach Möglichkeit in ähnliche Typen zu harmonisieren.

![ExperienceEvent Customer Journey](images/overview/experience-event-journey.png)

Siehe [[!UICONTROL XDM ExperienceEvent] Referenzhandbuch](./classes/experienceevent.md) für weitere Informationen über die Struktur und den Verwendungsfall der von der Klasse bereitgestellten Felder.

## XDM-Schema und -Experience Platform

Experience Platform ist vom Schema unabhängig, d. h. jedes Schema, das dem XDM-Standard entspricht, wird für Plattformdienste zur Verfügung gestellt. Wie verschiedene Plattformdienste Schema verwenden, wird im Folgenden näher erläutert.

### Katalogdienst, Dateningestion und Datensee

Katalogdienst ist das Aufzeichnungssystem für Experience Platformen-Assets und die zugehörigen Schema. Katalog enthält nicht die eigentlichen Datendateien oder Verzeichnisse, sondern enthält die Metadaten und Beschreibungen dieser Dateien und Verzeichnisse.

Katalogdaten werden im Data Lake gespeichert, einem hochgradig detaillierten Datenspeicher mit allen Daten, die von Platform verwaltet werden, unabhängig von Herkunft oder Dateiformat.

Um mit dem Erfassen von Daten in die Experience Platform zu beginnen, können Sie den Katalogdienst verwenden, um ein Dataset zu erstellen. Das DataSet verweist auf ein XDM-Schema, das die Struktur der zu ingetierenden Daten beschreibt. Wenn ein Datensatz ohne Schema erstellt wird, leitet die Experience Platform ein &quot;beobachtetes Schema&quot;ab, indem sie Typ und Inhalt der erfassten Datenfelder prüft. Die Datensätze werden dann im Katalog nachverfolgt und im Data Lake neben den Schemas und beobachteten Schemas, auf denen sie basieren, gespeichert.

Weitere Informationen zum Katalog finden Sie im [Katalogdienst - Übersicht](../catalog/home.md). Weitere Informationen zur Datenüberlastung in Adobe Experience Platform finden Sie im [Dateneinspeisungsübersicht](../ingestion/home.md).

### Query Service

Adobe Experience Platform Abfrage Service ermöglicht Ihnen die Verwendung von SQL-Standarddaten zur Abfrage von Experience Platformen, um viele verschiedene Anwendungsfälle zu unterstützen.

Nachdem ein Schema erstellt und ein DataSet erstellt wurde, das auf dieses Schema verweist, werden Daten im Data Lake erfasst und gespeichert. Mit dem Abfrage Service können Sie beliebige Datensätze in den Data Lake integrieren und die Abfragen als neues DataSet erfassen, das im Berichte, maschinellem Lernen oder für die Aufnahme in Echtzeit-Kundendaten verwendet werden kann.

Siehe [Übersicht über den Abfrage Service](../query-service/home.md) für weitere Informationen über den Dienst.

### Echtzeit-Kundenprofil

Echtzeit-Customer-Profil bietet ein zentralisiertes Consumer-Profil für zielgerichtetes und personalisiertes Erlebnismanagement. Jedes Profil enthält Daten, die über alle Systeme hinweg aggregiert werden, sowie belastbare Zeitstempel-Konten von Ereignissen, an denen sich der Einzelne beteiligt, die in einem der Systeme, die Sie mit der Experience Platform verwenden, stattgefunden haben.

Echtzeit-Kundendaten verbrauchen Schema-formatierte Daten basierend auf [!UICONTROL Individuelles XDM-Profil] und [!UICONTROL XDM ExperienceEvent] und reagiert auf Abfragen, die auf diesen Daten basieren. Profil unterstützt nicht die Verwendung von Schemas, die auf anderen Klassen basieren.

Das System verwaltet ein Exemplar jedes Profils und führt Daten zu einer &quot;einzigen Quelle der Wahrheit&quot; für den Einzelnen zusammen. Diese vereinheitlichten Daten werden mithilfe eines so genannten &quot;Vereinigung Schemas&quot; (manchmal auch als &quot;Vereinigung Ansicht&quot; bezeichnet) dargestellt. Ein Vereinigung-Schema Aggregat die Felder aller Schema, die dieselbe Klasse implementieren, in einem einzigen Schema.  Wenn Sie ein Schema mithilfe der Benutzeroberfläche oder API erstellen, können Sie das Schema für die Verwendung mit Echtzeit-Kundendaten-Profil aktivieren und für die Aufnahme in die Vereinigung mit Tags versehen. Das getaggte Schema nimmt dann an der Schema-Definition teil, die an Profil übergeben wird.

As [!UICONTROL Individuelles XDM-Profil] und [!UICONTROL XDM ExperienceEvent] Daten werden in den Data Lake eingebunden, Echtzeit-Kundendaten werden von Profil erfasst, die für die Nutzung aktiviert wurden. Je mehr Interaktionen und Details inbegriffen sind, desto robuster werden die individuellen Profil.

[!UICONTROL Individuelles XDM-Profil] Daten helfen, Aktionen über alle Kanal oder Adoben hinweg zu informieren und zu stärken. In Verbindung mit einer reichen Geschichte von Verhaltensdaten und Interaktionsdaten können diese Daten dazu verwendet werden, maschinelles Lernen zu fördern. Die Echtzeit-Customer-Profil-API kann auch dazu verwendet werden, die Funktionalität von Drittanbieterlösungen, CRMs und proprietären Lösungen zu erweitern.

Siehe [Überblick über Echtzeit-Kundenerlebnisse im Profil](../profile/home.md) für weitere Informationen.

### Data Science Workspace

Data Science Workspace in Adobe Experience Platform nutzt maschinelles Lernen und künstliche Intelligenz, um Einblicke aus den in Experience Platform gespeicherten Daten zu gewinnen. Data Science Workspace ermöglicht es Datenwissenschaftlern, Rezepte basierend auf [!UICONTROL Individuelles XDM-Profil] und [!UICONTROL XDM ExperienceEvent] Daten über Kunden und deren Aktivitäten, die Prognosen erleichtern, wie z. B. Kaufneigung und empfohlene Angebot, die der Einzelne schätzen und nutzen kann.

Mit Data Science Workspace können Datenwissenschaftler ganz einfach intelligente Service-APIs mit maschinellem Lernen erstellen. Diese Dienste arbeiten mit anderen Adobe-Lösungen, darunter Adobe Target und Adobe Analytics Cloud, zusammen, um Ihnen die Automatisierung personalisierter, gezielter digitaler Erlebnisse zu ermöglichen.

Weitere Informationen zur Verwendung von Daten aus der Experience Platform, um Einblicke zu gewinnen, finden Sie im [Übersicht über Data Science Workspace](../data-science-workspace/home.md).

## Nächste Schritte und zusätzliche Ressourcen

Jetzt, da man die Rolle von Schemas in der ganzen Experience Platform besser versteht, ist man bereit, einen eigenen Beginn zu erstellen.

Lesen Sie zunächst die folgenden Informationen, wie Sie Design-Prinzipien und Best Practices für die Erstellung von Schemas lernen können, die mit der Experience Platform verwendet werden sollen: [Grundlagen der Zusammensetzung des Schemas](schema/composition.md). Schrittweise Anleitungen zum Erstellen eines Schemas finden Sie in den Tutorials zum Erstellen eines Schemas [über die API](tutorials/create-schema-api.md) oder [über die Benutzeroberfläche](tutorials/create-schema-ui.md).

Um Ihr Verständnis von [!DNL XDM System] in der Experience Platform:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
