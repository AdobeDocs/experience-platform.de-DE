---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Experience-Datenmodell (XDM)-System
topic: overview
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '1606'
ht-degree: 8%

---


# XDM-System – Übersicht

Normung und Interoperabilität sind Schlüsselkonzepte der Adobe Experience Platform. [!DNL Experience Data Model]Das von Adobe unterstützte  (XDM) ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für jede Anwendung bereit, die zur Kommunikation mit [!DNL Platform] Diensten verwendet werden kann. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Audiencen durch Segmente definieren und Kundenattribute zu Personalisierungszwecken ausdrücken.

XDM is the foundational framework that allows Adobe Experience Cloud, powered by [!DNL Experience Platform], to deliver the right message to the right person, on the right channel, at exactly the right moment. Die Methode, auf der [!DNL Experience Platform] aufgebaut wird, **XDM System**, operalisiert [!DNL Experience Data Model] Schema für die Verwendung durch [!DNL Platform] Dienste.

This document provides an overview of the role of XDM System within [!DNL Experience Platform].

## XDM-Schemata

[!DNL Experience Platform] verwendet Schema, um die Datenstruktur konsistent und wiederverwendbar zu beschreiben. Durch die systemübergreifende Definition von Daten wird es einfacher, ihre Bedeutung beizubehalten und dadurch wertvolle Daten zu erhalten.

Bevor Daten erfasst werden können, muss ein Schema zusammengestellt werden, [!DNL Platform]um die Datenstruktur zu beschreiben und Beschränkungen für den Datentyp bereitzustellen, der in den einzelnen Feldern enthalten sein kann. Schema bestehen aus einer Basisklasse und Null oder mehr Mixins.

Weitere Informationen zum Schema-Kompositionsmodell, einschließlich Entwurfsprinzipien und Best Practices, finden Sie in den [Grundlagen der Schema-Komposition](schema/composition.md).

### [!DNL Schema Registry] und [!DNL Schema Library]

The **[!DNL Schema Registry]** provides a user interface and RESTful API from which you can view and manage all schema-related resources in the Adobe Experience Platform **[!DNL Schema Library]**. Der [!DNL Schema Library] enthält branchenübliche Ressourcen, die Ihnen von Adobe zur Verfügung gestellt werden, sowie Ressourcen von [!DNL Experience Platform] Partnern und Anbietern, deren Anwendungen Sie verwenden. Die Benutzeroberfläche und die API der Schema-Registrierung können auch verwendet werden, um neue Schema und Ressourcen zu erstellen und zu verwalten, die für Ihr Unternehmen eindeutig sind.

For a comprehensive guide to the major operations available in the [!DNL Schema Registry], see the [Schema Registry developer guide](api/getting-started.md).

## Datenverhalten im XDM-System {#data-behaviors}

Data intended for use in [!DNL Experience Platform] is grouped into two behavior types:

* **Aufzeichnen von Daten**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt könnte eine Organisation oder eine Einzelperson sein.
* **Zeitreihendaten**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt bereit, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

Alle XDM-Schemas beschreiben Daten, die als Datensatz- oder Zeitreihen kategorisiert werden können. Das Datenverhalten eines Schemas wird durch die **Klasse** des Schemas definiert, die einem Schema beim ersten Erstellen zugewiesen wird. XDM-Klassen beschreiben die kleinste Anzahl von Eigenschaften, die ein Schema enthalten muss, um ein bestimmtes Datenverhalten darzustellen.

Obwohl Sie in der Lage sind, Ihre eigenen Klassen innerhalb der [!DNL Schema Registry]zu definieren, wird empfohlen, die bevorzugten Klassen **[!DNL XDM Individual Profile]** bzw. **[!DNL XDM ExperienceEvent]** für die Daten der Datensatz- und Zeitreihen zu verwenden. Diese Klassen werden nachfolgend detaillierter beschrieben.

### [!DNL XDM Individual Profile]

[!DNL XDM Individual Profile] ist eine auf Aufzeichnungen basierende Klasse, die eine einzigartige Darstellung der Attribute sowohl identifizierter als auch nur teilweise identifizierter Subjekte bildet. Profil, die eindeutig identifiziert werden, können für persönliche Kommunikation oder zielgerichtete Interaktionen verwendet werden und detaillierte persönliche Informationen wie Name, Geschlecht, Geburtsdatum, Ort und Kontaktdaten wie Telefonnummern und E-Mail-Adressen enthalten.

Weniger identifizierte Profil können nur aus anonymen Verhaltenssignalen wie Browser-Cookies bestehen. In diesem Fall werden die spärlichen Profil-Daten zum Aufbau einer Informationsbasis verwendet, in der die Interessen und Vorlieben des anonymen Profils erfasst und gespeichert werden. Diese Bezeichner können im Laufe der Zeit detaillierter werden, wenn sich der Betreff für Benachrichtigungen, Abonnements, Käufe usw. anmeldet. Diese Zunahme der Attribute von Profilen kann schließlich zu einem bestimmten Thema führen und ein höheres Maß an gezieltem Einsatz ermöglichen.

Mit zunehmendem Profil für Verbraucher wird es zu einem robusten Archiv mit persönlichen Daten, Identifizierungsinformationen, Kontaktdaten und Kommunikationsvorlieben einer Person.

### [!DNL XDM ExperienceEvent]

XDM ExperienceEvent ist eine zeitreihenbasierte Klasse, die zum Erfassen des Systemzustands verwendet wird, wenn ein Ereignis (oder eine Gruppe von Ereignissen) aufgetreten ist, einschließlich des Zeitpunkts und der Identität des betreffenden Objekts. Erfahrungs-Ereignisse sind Faktenaufzeichnungen dessen, was geschehen ist, und somit sind sie unveränderlich und stellen dar, was ohne Aggregation oder Interpretation passiert ist. Sie sind für die Analyse von Zeitdomänen von entscheidender Bedeutung, da sie zur Analyse von Änderungen in einem bestimmten Zeitfenster und zum Vergleich zwischen mehreren Zeitfenstern verwendet werden können, um Trends zu verfolgen.

Erlebnis-Ereignis können explizit oder implizit sein. Explizite Ereignis sind unmittelbar erkennbare menschliche Handlungen, die während einer Reise stattfinden. Implizite Ereignisse sind Ereignisse, die ohne unmittelbare menschliche Handlungen aufgeworfen werden, aber immer noch mit einer Person in Verbindung stehen. Beispiele für implizite Ereignis können das geplante Senden von E-Mail-Newslettern oder eine Akkulaufzeit bis zu einem bestimmten Schwellenwert sein.

Auch wenn nicht alle Ereignis leicht in alle Datenquellen eingeordnet werden können, ist es äußerst nützlich, ähnliche Ereignis möglichst für die Verarbeitung in ähnliche Typen zu vereinheitlichen.

![ExperienceEvent Customer Journey](images/overview/experience-event-journey.png)

## XDM-Schema und - [!DNL Experience Platform] Dienste

[!DNL Experience Platform] ist Schema agnostisch, d. h. jedes Schema, das dem XDM-Standard entspricht, ist für die Verwendung durch [!DNL Platform] Dienste verfügbar. Die Nutzung von Schemas durch verschiedene [!DNL Platform] Dienste wird nachfolgend genauer erläutert.

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] ist das Aufzeichnungssystem für [!DNL Experience Platform] Vermögenswerte und damit verbundene Schemas. [!DNL Catalog] ist nicht die eigentlichen Dateien oder Verzeichnisse, die Daten enthalten, sondern enthält die Metadaten und Beschreibungen dieser Dateien und Ordner.

[!DNL Catalog] Daten werden im [!DNL Data Lake]hochgradig granularen Datenspeicher gespeichert, der alle von [!DNL Platform]Ihnen verwalteten Daten unabhängig von der Herkunft oder dem Dateiformat enthält.

Um mit der Erfassung von Daten zu beginnen, [!DNL Experience Platform]wird ein Datensatz mit [!DNL Catalog Service]erstellt. Der Datensatz verweist auf ein XDM-Schema, das die Struktur der zu ingetierenden Daten beschreibt. Wenn ein Datensatz ohne Schema erstellt wird, [!DNL Experience Platform] wird ein &quot;beobachtetes Schema&quot;abgeleitet, indem Art und Inhalt der erfassten Datenfelder geprüft werden. Die Datensätze werden dann neben den Schemas [!DNL Catalog] und beobachteten Schemas, auf denen sie basieren, in der [!DNL Data Lake] Datenbank nachverfolgt und gespeichert.

For more information on [!DNL Catalog], see the [Catalog Service overview](../catalog/home.md). Weitere Informationen zur Dateneinbettung in der Adobe Experience Platform finden Sie in der Übersicht über die [Dateneinbettung](../ingestion/home.md).

### [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] ermöglicht Ihnen die Verwendung von SQL zur Abfrage von [!DNL Experience Platform] Daten, um viele verschiedene Anwendungsfälle zu unterstützen.

Nachdem ein Schema zusammengestellt und ein Datensatz erstellt wurde, der auf dieses Schema verweist, werden die Daten in der Datei erfasst und gespeichert [!DNL Data Lake]. Using [!DNL Query Service], you can join any datasets in the [!DNL Data Lake] and capture the query results as a new dataset for use in reporting, machine learning, or for ingestion into [!DNL Real-time Customer Profile].

Weitere Informationen [!DNL Query Service]finden Sie in der Einführung zum [Abfrage-Service](../query-service/home.md).

### [!DNL Real-time Customer Profile]

Echtzeit-Customer-Profil bietet ein zentrales Profil für zielgerichtetes und personalisiertes Erlebnis-Management. Jedes Profil enthält Daten, die über alle Systeme aggregiert werden, sowie umsetzbare Zeitstempelkonten von Ereignissen, an denen die Einzelperson beteiligt ist, die in einem der von Ihnen verwendeten Systeme aufgetreten sind [!DNL Experience Platform].

[!DNL Real-time Customer Profile] verarbeitet Schema-formatierte Daten basierend auf der [!DNL XDM Individual Profile] oder- [!DNL XDM ExperienceEvent] Klassen und reagiert auf Abfragen, die auf diesen Daten basieren. [!DNL Profile] unterstützt nicht die Verwendung von Schemas, die auf anderen Klassen basieren.

[!DNL Profile] unterhält eine Instanz jedes Profils und führt Daten zusammen, um eine &quot;einzige Wahrheitsquelle&quot;für die Einzelperson zu schaffen. Diese vereinheitlichten Daten werden mithilfe einer so genannten &quot;Vereinigung-Ansicht&quot;dargestellt. Eine Vereinigung-Ansicht Aggregat die Felder aller Schema, die dieselbe Klasse implementieren, in einem Schema.  Wenn Sie ein Schema mithilfe der Benutzeroberfläche oder API erstellen, können Sie das Schema für die Verwendung mit aktivieren [!DNL Real-time Customer Profile] und es für die Aufnahme in die Ansicht &quot;Vereinigung&quot;taggen. Das getaggte Schema nimmt dann an der Schema-Definition teil, an die [!DNL Profile]es gesendet wird.

Während [!DNL XDM Individual Profile] und [!DNL XDM ExperienceEvent] Daten erfasst und verwaltet werden [!DNL Catalog], werden Daten, die für ihre Verwendung aktiviert wurden, [!DNL Real-time Customer Profile] in die Erfassung aufgenommen. Je mehr Interaktionen und Details einbezogen werden, desto robuster werden die einzelnen Profil.

[!DNL XDM Individual Profile] Daten helfen bei der Information und Ermöglichung von Aktionen in allen Kanälen oder bei der Adobe-Lösungsintegration. Wenn Daten zu Verhalten und Interaktion mit einer umfangreichen Geschichte verknüpft werden, werden diese Daten zur Förderung des maschinellen Lernens verwendet. Die [!DNL Real-time Customer Profile] API kann auch verwendet werden, um die Funktionalität von Lösungen von Drittanbietern, CRMs und proprietären Lösungen zu erweitern.

Weitere Informationen finden Sie in der Übersicht [zum](../profile/home.md) Echtzeit-Customer-Profil.

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] uses machine learning and artificial intelligence to gain insights from data stored within [!DNL Experience Platform]. [!DNL Data Science Workspace] ermöglicht es Datenwissenschaftlern, Rezepte auf Basis von XDM Individual [!DNL Profile] und [!DNL XDM ExperienceEvent] Daten über Kunden und ihre Aktivitäten zu erstellen, wodurch Prognosen wie Kaufneigung und empfohlene Angebot erleichtert werden, die der Einzelne schätzen und nutzen kann.

Mithilfe [!DNL Data Science Workspace]von Daten können Wissenschaftler auf einfache Weise intelligente Dienste-APIs erstellen, die auf maschinellem Lernen basieren. Diese Dienste arbeiten mit anderen Adobe-Lösungen zusammen, einschließlich Adobe Target und Adobe Analytics Cloud, um Ihnen bei der Automatisierung personalisierter, gezielter digitaler Erlebnisse zu helfen.

Weitere Informationen zur Verwendung von [!DNL Experience Platform] Daten zur Erzielung von Einblicken finden Sie in der Übersicht über den [Data Science Workspace](../data-science-workspace/home.md).

### [!DNL Decisioning Service]

[!DNL Decisioning Service] bietet die Möglichkeit, personalisierte Angebot-Entscheidungsfindungen in [!DNL Platform]integrierten Anwendungen zu konfigurieren. Angebot können Produktempfehlungen, Inhaltskomponenten für ein Web-Erlebnis, Konversationsskripte und zu ergreifende Aktionen sein.

[!DNL Decisioning Service] nutzt [!DNL Real-time Customer Profile] Daten und ist daher nur mit Datensätzen kompatibel, die auf Schemas basieren, die die [!DNL XDM Individual Profile] oder [!DNL XDM ExperienceEvent] -Klasse implementieren.

See the [Decisioning Service overview](../decisioning-service/home.md) for more information.

## Nächste Schritte und zusätzliche Ressourcen

Jetzt, da Sie die Rolle der Schemas im Ganzen besser verstehen, [!DNL Experience Platform]sind Sie bereit, Beginn zu erstellen, die Ihre eigenen. Um Ihre Lernerfahrung weiter zu ergänzen, lesen Sie die Beginn der vorgeschlagenen Dokumentation und sehen Sie sich das Video unten an.

Um Designprinzipien und Best Practices für das Erstellen von Schemas zu lernen, mit denen verwendet werden [!DNL Experience Platform], beginnen Sie mit dem Lesen der [Grundlagen der Schema-Komposition](schema/composition.md). Eine schrittweise Anleitung zum Erstellen eines Schemas finden Sie in den Lernprogrammen zum Erstellen eines Schemas [mit der API](tutorials/create-schema-api.md) oder [mithilfe der Benutzeroberfläche](tutorials/create-schema-ui.md).

Sehen Sie sich das folgende Video an, um Ihr Verständnis [!DNL XDM System] [!DNL Experience Platform]in zu vertiefen:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)

