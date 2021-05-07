---
keywords: Experience Platform;Home;beliebte Themen;XDM;XDM-System;XDM-Profil;XDM-Erlebnis-Ereignis;Erlebnis-Ereignis;Erlebnis-Gruppen;Feldgruppen;Feldgruppe;Erlebnis-Ereignis;XDM-Ereignis;XDM-Erlebnis-Ereignis;Erlebnis-Ereignis;XDM-Erlebnis-Ereignis;Erlebnis-Datenmodell;Erlebnis-Datenmodell;Datenmodell;Schema-Registrierung;Schema-Registrierung;Schema-Bibliothek;Schema-Bibliothek;Schema;Datensatzdaten;Zeitreihen;Zeitreihen
solution: Experience Platform
title: XDM-Systemübersicht
topic-legacy: overview
description: Normung und Interoperabilität sind Schlüsselkonzepte für Adobe Experience Platform. Das von Adobe unterstützte Experience-Datenmodell (XDM) ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Customer Experience Management zu definieren.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
translation-type: tm+mt
source-git-commit: b70e693b4ffeda561de4d4c8dd8fd1adeec489f7
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 9%

---

# XDM-System – Übersicht

>[!NOTE]
>
>Der Begriff &quot;mixin&quot;wurde zum Schema &quot;Feldgruppe&quot;aktualisiert, um Verständnis zu fördern. Feldgruppen sind wiederverwendbare Feldsätze zur Unterstützung von Geschäftszwecken. Diese Änderung wird nun in der Schema Registry API, der Adobe Experience Platform-Benutzeroberfläche und in allen Plattformdokumenten widergespiegelt.

Normung und Interoperabilität sind Schlüsselkonzepte für Adobe Experience Platform. [!DNL Experience Data Model] (XDM), angetrieben von der Adobe, ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schema für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für alle Anwendungen bereit, die zur Kommunikation mit [!DNL Platform]-Diensten verwendet werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Audiencen durch Segmente definieren und Kundenattribute zu Personalisierungszwecken ausdrücken.

XDM ist das Fundament, das es Adobe Experience Cloud, powered by [!DNL Experience Platform], ermöglicht, die richtige Botschaft an die richtige Person, am richtigen Kanal, genau zum richtigen Zeitpunkt zu senden. Die Methodik, auf der [!DNL Experience Platform] erstellt wird, XDM-System, operalisiert [!DNL Experience Data Model]-Schema zur Verwendung durch [!DNL Platform]-Dienste.

Dieses Dokument bietet einen Überblick über die Rolle von XDM-System innerhalb von [!DNL Experience Platform].

## XDM-Schemata

[!DNL Experience Platform]Schemas dienen in zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, die Bedeutung beizubehalten und somit Wert aus Daten zu ziehen.

Bevor Daten in [!DNL Platform] aufgenommen werden können, muss ein Schema zusammengestellt werden, um die Datenstruktur zu beschreiben und Beschränkungen für den Datentyp bereitzustellen, der in den einzelnen Feldern enthalten sein kann. Schema bestehen aus einer Basisklasse und einer Schema- oder Feldgruppe.

Weitere Informationen zum Kompositionsmodell für Schemas, einschließlich Designprinzipien und Best Practices, finden Sie in den [Grundlagen der Schema-Komposition](schema/composition.md).

### [!DNL Schema Registry] und [!DNL Schema Library]

Das **[!DNL Schema Registry]** stellt eine Benutzeroberfläche und RESTful-API bereit, über die Sie alle Schema-bezogenen Ressourcen im Adobe Experience Platform **[!DNL Schema Library]** Ansicht und Verwaltung durchführen können. Das [!DNL Schema Library] enthält branchenübliche Ressourcen, die Ihnen nach Adobe zur Verfügung gestellt werden, sowie Ressourcen von [!DNL Experience Platform]-Partnern und -Anbietern, deren Anwendungen Sie verwenden. Die Benutzeroberfläche und die API der Schema-Registrierung können auch verwendet werden, um neue Schema und Ressourcen zu erstellen und zu verwalten, die für Ihr Unternehmen eindeutig sind.

Eine umfassende Anleitung zu den wichtigsten in [!DNL Schema Registry] verfügbaren Vorgängen finden Sie im [Schema Registry-Entwicklerhandbuch](api/getting-started.md).

## Datenverhalten im XDM-System {#data-behaviors}

Daten, die in [!DNL Experience Platform] verwendet werden sollen, sind in zwei Verhaltenstypen unterteilt:

* **Aufzeichnen von Daten**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt könnte eine Organisation oder eine Einzelperson sein.
* **Zeitreihendaten**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt bereit, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

Alle XDM-Schemas beschreiben Daten, die als Datensatz- oder Zeitreihen kategorisiert werden können. Das Datenverhalten eines Schemas wird durch die Klasse des Schemas definiert, die einem Schema beim ersten Erstellen zugewiesen wird. XDM-Klassen beschreiben die kleinste Anzahl von Eigenschaften, die ein Schema enthalten muss, um ein bestimmtes Datenverhalten darzustellen.

Obwohl Sie in der Lage sind, Ihre eigenen Klassen innerhalb von [!DNL Schema Registry] zu definieren, wird empfohlen, die bevorzugten Klassen **[!DNL XDM Individual Profile]** und **[!DNL XDM ExperienceEvent]** für Datensatz- und Zeitreihendaten zu verwenden. Diese Klassen werden nachfolgend detaillierter beschrieben.

### [!DNL XDM Individual Profile] {#xdm-individual-profile}

[!DNL XDM Individual Profile] ist eine auf Aufzeichnungen basierende Klasse, die eine einzigartige Darstellung der Attribute sowohl identifizierter als auch nur teilweise identifizierter Subjekte bildet. Profil, die eindeutig identifiziert werden, können für persönliche Kommunikation oder zielgerichtete Interaktionen verwendet werden und detaillierte persönliche Informationen wie Name, Geschlecht, Geburtsdatum, Ort und Kontaktdaten wie Telefonnummern und E-Mail-Adressen enthalten.

Weniger identifizierte Profil können nur aus anonymen Verhaltenssignalen wie Browser-Cookies bestehen. In diesem Fall werden die spärlichen Profil-Daten zum Aufbau einer Informationsbasis verwendet, in der die Interessen und Vorlieben des anonymen Profils erfasst und gespeichert werden. Diese Bezeichner können im Laufe der Zeit detaillierter werden, wenn sich der Betreff für Benachrichtigungen, Abonnements, Käufe usw. anmeldet. Diese Zunahme der Attribute von Profilen kann schließlich zu einem bestimmten Thema führen und ein höheres Maß an gezieltem Einsatz ermöglichen.

Mit zunehmendem Profil für Verbraucher wird es zu einem robusten Archiv mit persönlichen Daten, Identifizierungsinformationen, Kontaktdaten und Kommunikationsvorlieben einer Person.

### [!DNL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent ist eine zeitreihenbasierte Klasse, die zum Erfassen des Systemzustands verwendet wird, wenn ein Ereignis (oder eine Gruppe von Ereignissen) aufgetreten ist, einschließlich des Zeitpunkts und der Identität des betreffenden Objekts. Erfahrungs-Ereignisse sind Faktenaufzeichnungen dessen, was geschehen ist, und somit sind sie unveränderlich und stellen dar, was ohne Aggregation oder Interpretation passiert ist. Sie sind für die Analyse von Zeitdomänen von entscheidender Bedeutung, da sie zur Analyse von Änderungen in einem bestimmten Zeitfenster und zum Vergleich zwischen mehreren Zeitfenstern verwendet werden können, um Trends zu verfolgen.

Erlebnis-Ereignis können explizit oder implizit sein. Explizite Ereignis sind unmittelbar erkennbare menschliche Handlungen, die während einer Journey stattfinden. Implizite Ereignisse sind Ereignisse, die ohne unmittelbare menschliche Handlungen aufgeworfen werden, aber immer noch mit einer Person in Verbindung stehen. Beispiele für implizite Ereignis können das geplante Senden von E-Mail-Newslettern oder eine Akkulaufzeit bis zu einem bestimmten Schwellenwert sein.

Auch wenn nicht alle Ereignis leicht in alle Datenquellen eingeordnet werden können, ist es äußerst nützlich, ähnliche Ereignis möglichst für die Verarbeitung in ähnliche Typen zu vereinheitlichen.

![ExperienceEvent Customer Journey](images/overview/experience-event-journey.png)

## XDM-Schema und [!DNL Experience Platform]-Dienste

[!DNL Experience Platform] ist Schema-agnostisch, d. h. jedes Schema, das dem XDM-Standard entspricht, ist für  [!DNL Platform] Dienste verfügbar. Wie verschiedene [!DNL Platform]-Dienste Schema verwenden, wird nachfolgend detaillierter beschrieben.

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] ist das Aufzeichnungssystem für  [!DNL Experience Platform] Vermögenswerte und damit verbundene Schemas. [!DNL Catalog] ist nicht die eigentlichen Dateien oder Verzeichnisse, die Daten enthalten, sondern enthält die Metadaten und Beschreibungen dieser Dateien und Ordner.

[!DNL Catalog] Daten werden im  [!DNL Data Lake]hochgradig granularen Datenspeicher gespeichert, der alle von  [!DNL Platform]Ihnen verwalteten Daten unabhängig von der Herkunft oder dem Dateiformat enthält.

Um Daten in [!DNL Experience Platform] einzufügen, wird ein Datensatz mit [!DNL Catalog Service] erstellt. Der Datensatz verweist auf ein XDM-Schema, das die Struktur der zu ingetierenden Daten beschreibt. Wenn ein Datensatz ohne Schema erstellt wird, leitet [!DNL Experience Platform] ein &quot;beobachtetes Schema&quot;ab, indem Typ und Inhalt der erfassten Datenfelder geprüft werden. Die Datensätze werden dann in [!DNL Catalog] verfolgt und in [!DNL Data Lake] neben den Schemas und beobachteten Schemas, auf denen sie basieren, gespeichert.

Weitere Informationen zu [!DNL Catalog] finden Sie unter [Übersicht über den Katalogdienst](../catalog/home.md). Weitere Informationen zur Adobe Experience Platform Data Ingestion finden Sie unter [Übersicht über die Dateneinbettung](../ingestion/home.md).

### [!DNL Query Service]

Mit Adobe Experience Platform [!DNL Query Service] können Sie standardmäßige SQL-Daten zur Abfrage [!DNL Experience Platform] verwenden, um viele verschiedene Anwendungsfälle zu unterstützen.

Nachdem ein Schema erstellt und ein Datensatz erstellt wurde, der auf dieses Schema verweist, werden die Daten in das [!DNL Data Lake]-Element aufgenommen und gespeichert. Mit [!DNL Query Service] können Sie alle Datensätze in [!DNL Data Lake] einbinden und die Abfragen als neuen Datensatz erfassen, der im Berichte, maschinellem Lernen oder zur Aufnahme in [!DNL Real-time Customer Profile] verwendet werden kann.

Weitere Informationen zu [!DNL Query Service] finden Sie in der [Abfrage Service-Einführung](../query-service/home.md).

### [!DNL Real-time Customer Profile]

Echtzeit-Customer-Profil bietet ein zentrales Profil für zielgerichtetes und personalisiertes Erlebnis-Management. Jedes Profil enthält Daten, die über alle Systeme aggregiert werden, sowie umsetzbare Zeitstempelkonten von Ereignissen, die die Einzelperson betreffen, die in einem der mit [!DNL Experience Platform] verwendeten Systeme aufgetreten sind.

[!DNL Real-time Customer Profile] verarbeitet Schema-formatierte Daten basierend auf der  [!DNL XDM Individual Profile] oder- [!DNL XDM ExperienceEvent] Klasse und reagiert auf Abfragen, die auf diesen Daten basieren. [!DNL Profile] unterstützt nicht die Verwendung von Schemas, die auf anderen Klassen basieren.

[!DNL Profile] unterhält eine Instanz jedes Profils und führt Daten zusammen, um eine &quot;einzige Wahrheitsquelle&quot;für die Einzelperson zu schaffen. Diese vereinheitlichten Daten werden mithilfe einer so genannten &quot;Vereinigung-Ansicht&quot;dargestellt. Eine Vereinigung-Ansicht Aggregat die Felder aller Schema, die dieselbe Klasse implementieren, in einem Schema.  Wenn Sie ein Schema mithilfe der Benutzeroberfläche oder API erstellen, können Sie das Schema für die Verwendung mit [!DNL Real-time Customer Profile] aktivieren und es zur Aufnahme in die Ansicht &quot;Vereinigung&quot;taggen. Das getaggte Schema nimmt dann an der Schema-Definition teil, die an [!DNL Profile] übertragen wird.

Da [!DNL XDM Individual Profile]- und [!DNL XDM ExperienceEvent]-Daten von [!DNL Catalog] erfasst und verwaltet werden, beginnen die Trigger [!DNL Real-time Customer Profile] mit der Erfassung von Daten, die für die Verwendung aktiviert wurden. Je mehr Interaktionen und Details einbezogen werden, desto robuster werden die einzelnen Profil.

[!DNL XDM Individual Profile] Daten helfen bei der Information und Ermöglichung von Aktionen in allen Kanal- oder Adoben-Lösungsintegrationen. Wenn diese Daten mit einer umfangreichen Geschichte von Verhaltensdaten und Interaktionsdaten gepaart werden, werden diese Daten zur Förderung des maschinellen Lernens verwendet. Die [!DNL Real-time Customer Profile]-API kann auch verwendet werden, um die Funktionalität von Lösungen von Drittanbietern, CRMs und proprietären Lösungen zu erweitern.

Weitere Informationen finden Sie unter Übersicht über das Echtzeit-Profil des Kunden](../profile/home.md).[

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] verwendet maschinelles Lernen und künstliche Intelligenz, um Einblicke aus Daten zu gewinnen, die innerhalb von [!DNL Experience Platform] gespeichert werden. [!DNL Data Science Workspace] ermöglicht es Datenwissenschaftlern, Rezepte auf Basis von XDM Individual  [!DNL Profile] und  [!DNL XDM ExperienceEvent] Daten über Kunden und ihre Aktivitäten zu erstellen, wodurch Prognosen wie Kaufneigung und empfohlene Angebot erleichtert werden, die der Einzelne schätzen und nutzen kann.

Mit [!DNL Data Science Workspace] können Datenwissenschaftler auf einfache Weise intelligente Dienste-APIs erstellen, die auf maschinellem Lernen basieren. Diese Dienste arbeiten mit anderen Adoben zusammen, einschließlich Adobe Target und Adobe Analytics Cloud, um Ihnen bei der Automatisierung personalisierter, zielgerichteter digitaler Erlebnisse zu helfen.

Weitere Informationen zur Verwendung von [!DNL Experience Platform]-Daten zur Erzielung von Einblicken finden Sie unter [Übersicht über den Data Science Workspace](../data-science-workspace/home.md).

## Nächste Schritte und zusätzliche Ressourcen

Jetzt, da Sie die Rolle von Schemas in [!DNL Experience Platform] besser verstehen, sind Sie bereit, Beginn zu komponieren Ihre eigenen. Um Ihre Lernerfahrung weiter zu ergänzen, lesen Sie die Beginn der vorgeschlagenen Dokumentation und sehen Sie sich das Video unten an.

Um Entwurfsgrundsätze und Best Practices für das Erstellen von Schemas zu lernen, die mit [!DNL Experience Platform] verwendet werden, lesen Sie zunächst die [Grundlagen der Schema-Komposition](schema/composition.md). Eine schrittweise Anleitung zum Erstellen eines Schemas finden Sie in den Lernprogrammen zum Erstellen eines Schemas [mit der API](tutorials/create-schema-api.md) oder [mithilfe der Benutzeroberfläche](tutorials/create-schema-ui.md).

Sehen Sie sich das folgende Video an, um Ihr Verständnis von [!DNL XDM System] in [!DNL Experience Platform] zu vertiefen:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
