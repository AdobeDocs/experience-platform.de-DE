---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erlebnis-Datenmodell (XDM)-System
topic: overview
translation-type: tm+mt
source-git-commit: c07f926a71447e840c692ed15e85c9e02f1106ab
workflow-type: tm+mt
source-wordcount: '1744'
ht-degree: 0%

---


# XDM-System - Übersicht

Standardisierung und Interoperabilität sind Schlüsselkonzepte der Adobe Experience Platform. Das von Adobe unterstützte Experience Data Model (XDM) ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schema für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für jede Anwendung bereit, die zur Kommunikation mit Plattformdiensten verwendet werden kann. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Audiencen durch Segmente definieren und Kundenattribute zu Personalisierungszwecken ausdrücken.

XDM ist das grundlegende Framework, mit dem Adobe Experience Cloud, powered by Experience Platform, die richtige Botschaft an die richtige Person im richtigen Kanal und genau zum richtigen Zeitpunkt senden kann. Die Methodik, auf der Experience Platform aufgebaut ist, **XDM-System**, operalisiert Experience Data Model-Schema für die Verwendung durch Plattformdienste.

Dieses Dokument gibt einen Überblick über die Rolle des XDM-Systems in Experience Platform.

## XDM-Schemas

Experience Platform verwendet Schema, um die Datenstruktur konsistent und wiederverwendbar zu beschreiben. Durch die systemübergreifende Definition von Daten wird es einfacher, ihre Bedeutung beizubehalten und dadurch wertvolle Daten zu erhalten.

Bevor Daten in eine Plattform aufgenommen werden können, muss ein Schema zusammengestellt werden, das die Datenstruktur beschreibt und Einschränkungen für den Datentyp bereitstellt, der in den einzelnen Feldern enthalten sein kann. Schema bestehen aus einer Basisklasse und Null oder mehr Mixins.

Weitere Informationen zum Schema-Kompositionsmodell, einschließlich Entwurfsprinzipien und Best Practices, finden Sie in den [Grundlagen der Schema-Komposition](schema/composition.md).

### Schema-Registrierung und Schema-Bibliothek

Die **Schema-Registrierung** bietet eine Benutzeroberfläche und eine RESTful-API, über die Sie alle Schema-bezogenen Ressourcen in der Adobe Experience Platform- **Schema-Bibliothek** Ansicht und verwalten können. Die Schema Library enthält branchenübliche Ressourcen, die Ihnen von Adobe zur Verfügung gestellt werden, sowie Ressourcen von Experience Platform-Partnern und -Anbietern, deren Anwendungen Sie verwenden. Die Benutzeroberfläche und die API der Schema-Registrierung können auch verwendet werden, um neue Schema und Ressourcen zu erstellen und zu verwalten, die für Ihr Unternehmen eindeutig sind.

Eine ausführliche Anleitung zu den wichtigsten in der Schema-Registrierung verfügbaren Vorgängen finden Sie im [Schema Registry-Entwicklerhandbuch](api/getting-started.md).

## Datenverhalten im XDM-System {#data-behaviors}

Daten, die in Experience Platform verwendet werden sollen, sind in zwei Verhaltenstypen unterteilt:

* **Daten** aufzeichnen: Stellt Informationen zu den Attributen eines Betreffs bereit. Ein Thema könnte eine Organisation oder eine Einzelperson sein.
* **Zeitreihendaten**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt dar, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

Alle XDM-Schema beschreiben Daten, die als Datensatz- oder Zeitreihen kategorisiert werden können. Das Datenverhalten eines Schemas wird durch die **Klasse** des Schemas definiert, die einem Schema beim ersten Erstellen zugewiesen wird. XDM-Klassen beschreiben die kleinste Anzahl von Eigenschaften, die ein Schema enthalten muss, um ein bestimmtes Datenverhalten darzustellen.

Obwohl Sie in der Schema-Registrierung eigene Klassen definieren können, wird empfohlen, die bevorzugten Klassen **XDM Individual Profil** und **XDM ExperienceEvent** für Datensatz- bzw. Zeitreihendaten zu verwenden. Diese Klassen werden nachfolgend detaillierter beschrieben.

### XDM Individuelles Profil

XDM Individual Profil ist eine Datensatzklasse, die eine eindeutige Darstellung der Attribute sowohl identifizierter als auch teilweise identifizierter Subjekte bildet. Profil, die eindeutig identifiziert werden, können für persönliche Kommunikation oder zielgerichtete Interaktionen verwendet werden und detaillierte persönliche Informationen wie Name, Geschlecht, Geburtsdatum, Ort und Kontaktdaten wie Telefonnummern und E-Mail-Adressen enthalten.

Weniger identifizierte Profil können nur aus anonymen Verhaltenssignalen wie Browser-Cookies bestehen. In diesem Fall werden die spärlichen Profil-Daten zum Aufbau einer Informationsbasis verwendet, in der die Interessen und Vorlieben des anonymen Profils erfasst und gespeichert werden. Diese Bezeichner können im Laufe der Zeit detaillierter werden, wenn sich der Betreff für Benachrichtigungen, Abonnements, Käufe usw. anmeldet. Diese Zunahme der Attribute von Profilen kann schließlich zu einem bestimmten Thema führen und ein höheres Maß an gezieltem Einsatz ermöglichen.

Mit zunehmendem Profil für Verbraucher wird es zu einem robusten Archiv mit persönlichen Daten, Identifizierungsinformationen, Kontaktdaten und Kommunikationsvorlieben einer Person.

### XDM ExperienceEvent

XDM ExperienceEvent ist eine zeitreihenbasierte Klasse, die zum Erfassen des Systemzustands verwendet wird, wenn ein Ereignis (oder eine Gruppe von Ereignissen) aufgetreten ist, einschließlich des Zeitpunkts und der Identität des betreffenden Objekts. Erfahrungs-Ereignisse sind Faktenaufzeichnungen dessen, was geschehen ist, und somit sind sie unveränderlich und stellen dar, was ohne Aggregation oder Interpretation passiert ist. Sie sind für die Analyse von Zeitdomänen von entscheidender Bedeutung, da sie zur Analyse von Änderungen in einem bestimmten Zeitfenster und zum Vergleich zwischen mehreren Zeitfenstern verwendet werden können, um Trends zu verfolgen.

Erlebnis-Ereignis können explizit oder implizit sein. Explizite Ereignis sind unmittelbar erkennbare menschliche Handlungen, die während einer Reise stattfinden. Implizite Ereignisse sind Ereignisse, die ohne unmittelbare menschliche Handlungen aufgeworfen werden, aber immer noch mit einer Person in Verbindung stehen. Beispiele für implizite Ereignis können das geplante Senden von E-Mail-Newslettern oder eine Akkulaufzeit bis zu einem bestimmten Schwellenwert sein.

Auch wenn nicht alle Ereignis leicht in alle Datenquellen eingeordnet werden können, ist es äußerst nützlich, ähnliche Ereignis möglichst für die Verarbeitung in ähnliche Typen zu vereinheitlichen.

![ExperienceEvent Customer Journey](images/overview/experience-event-journey.png)

## XDM-Schema und Experience Platform-Dienste

Experience Platform ist ein Schema-Agnostiker, d. h. jedes Schema, das dem XDM-Standard entspricht, steht für Plattformdienste zur Verfügung. Wie verschiedene Plattformdienste Schema verwenden, wird nachfolgend genauer erläutert.

### Katalogdienst, Dateneinbettung und Datensee

Der Katalogdienst ist das Datensatzsystem für Experience Platform-Assets und zugehörige Schema. Katalog sind nicht die eigentlichen Dateien oder Verzeichnisse, die Daten enthalten, sondern enthält die Metadaten und Beschreibungen dieser Dateien und Ordner.

Katalogdaten werden im Data Lake gespeichert, einem hochgradig granulären Datenspeicher mit allen von Platform verwalteten Daten, unabhängig von der Herkunft oder dem Dateiformat.

Um Daten in die Experience Platform zu integrieren, wird ein Datensatz mithilfe des Katalogdienstes erstellt. Der Datensatz verweist auf ein XDM-Schema, das die Struktur der zu ingetierenden Daten beschreibt. Wenn ein Datensatz ohne Schema erstellt wird, leitet Experience Platform ein &quot;beobachtetes Schema&quot;ab, indem Art und Inhalt der erfassten Datenfelder geprüft werden. Die Datensätze werden dann im Katalog nachverfolgt und im Data Lake neben den Schemas und beobachteten Schemas, auf denen sie basieren, gespeichert.

Weitere Informationen zum Katalog finden Sie in der Übersicht über den [Katalogdienst](../catalog/home.md). Weitere Informationen zur Dateneinbettung in Adobe Experience Platform finden Sie in der Übersicht über die [Dateneinbettung](../ingestion/home.md).

### Abfrage

Mit dem Adobe Experience Platform Abfrage Service können Sie SQL-Standarddaten für Abfrage Experience Platform verwenden, um viele verschiedene Anwendungsfälle zu unterstützen.

Nachdem ein Schema erstellt und ein Datensatz erstellt wurde, der auf dieses Schema verweist, werden die Daten in den Data Lake aufgenommen und gespeichert. Mit dem Abfrage Service können Sie alle Datensätze in den Data Lake einbinden und die Abfragen als neuen Datensatz erfassen, der im Berichte, maschinellem Lernen oder zur Erfassung in Echtzeit-Kundendaten verwendet werden kann.

Weitere Informationen zu Abfrage Service finden Sie in der Einführung zum [Abfrage Service](../query-service/home.md).

### Echtzeit-Kundenprofil

Echtzeit-Customer-Profil bietet ein zentrales Profil für zielgerichtetes und personalisiertes Erlebnis-Management. Jedes Profil enthält Daten, die über alle Systeme aggregiert werden, sowie umsetzbare Zeitstempelkonten von Ereignissen, an denen die Einzelperson beteiligt ist, die in einem der mit Experience Platform verwendeten Systeme aufgetreten sind.

Echtzeit-Kundendaten werden vom Schema-Profil basierend auf den XDM Individual Profil- oder XDM ExperienceEvent-Klassen verarbeitet und reagieren auf Abfragen, die auf diesen Daten basieren. Profil unterstützt nicht die Verwendung von Schemas, die auf anderen Klassen basieren.

Profil behält eine Instanz jedes Profils bei und führt Daten zusammen, um eine &quot;einzige Quelle der Wahrheit&quot;für den Einzelnen zu bilden. Diese vereinheitlichten Daten werden mithilfe einer so genannten &quot;Vereinigung-Ansicht&quot;dargestellt. Eine Vereinigung-Ansicht Aggregat die Felder aller Schema, die dieselbe Klasse implementieren, in einem Schema.  Wenn Sie ein Schema mithilfe der Benutzeroberfläche oder API erstellen, können Sie das Schema für die Verwendung mit dem Echtzeit-Kunden-Profil aktivieren und es zur Einbindung in die Vereinigung-Ansicht taggen. Das getaggte Schema nimmt dann an der Schema-Definition teil, die an Profil übergeben wird.

Da XDM Individual Profil- und XDM ExperienceEvent-Daten von Catalog erfasst und verwaltet werden, löst dies ein Echtzeit-Kundendaten-Profil aus, um Daten zu erfassen, die für die Verwendung aktiviert wurden. Je mehr Interaktionen und Details einbezogen werden, desto robuster werden die einzelnen Profil.

XDM Individuelle Profil-Daten unterstützen Sie bei der Information und Ermöglichung von Aktionen in allen Kanal- oder Adobe-Lösungsintegrationen. Wenn diese Daten mit einer umfangreichen Geschichte von Verhaltensdaten und Interaktionsdaten gepaart werden, werden diese Daten zur Förderung des maschinellen Lernens verwendet. Die Echtzeit-Customer-Profil-API kann auch verwendet werden, um die Funktionalität von Drittanbieterlösungen, CRMs und proprietären Lösungen zu erweitern.

Weitere Informationen finden Sie in der Übersicht [zum](../profile/home.md) Echtzeit-Customer-Profil.

### Data Science-Arbeitsbereich

Der Data Science Workspace der Adobe Experience Platform nutzt maschinelles Lernen und künstliche Intelligenz, um Einblicke aus den in Experience Platform gespeicherten Daten zu gewinnen. Data Science Workspace ermöglicht es Datenwissenschaftlern, Rezepte zu erstellen, die auf XDM Individual Profil- und XDM ExperienceEvent-Daten über Kunden und deren Aktivitäten basieren. Dies erleichtert Prognosen wie Kaufneigung und empfohlene Angebot, die die Einzelperson schätzen und nutzen kann.

Mit Data Science Workspace können Datenwissenschaftler auf einfache Weise intelligente Services-APIs erstellen, die auf maschinellem Lernen basieren. Diese Dienste arbeiten mit anderen Adobe-Lösungen zusammen, einschließlich Adobe Zielgruppe und Adobe Analytics Cloud, um Ihnen bei der Automatisierung personalisierter, zielgerichteter digitaler Erlebnisse zu helfen.

Weitere Informationen zur Verwendung von Experience Platform-Daten zur Erzielung von Einblicken finden Sie in der Übersicht über den [Data Science Workspace](../data-science-workspace/home.md).

### Entscheidungsdienst

Der Entscheidungsdienst bietet die Möglichkeit, personalisierte Angebot-Entscheidungsfindungen in plattformintegrierten Anwendungen zu konfigurieren. Angebot können Produktempfehlungen, Inhaltskomponenten für ein Web-Erlebnis, Konversationsskripte und zu ergreifende Aktionen sein.

Der Entscheidungsdienst nutzt Echtzeit-Kundendaten und ist daher nur mit Datensätzen kompatibel, die auf Schemas basieren, die das XDM Individual-Profil oder die XDM ExperienceEvent-Klasse implementieren.

See the [Decisioning Service overview](../decisioning-service/home.md) for more information.

## Nächste Schritte

Jetzt, da Sie die Rolle von Schemas in der gesamten Experience Platform besser verstehen, sind Sie bereit, Beginn zu erstellen, die Ihre eigenen.

Um Designgrundsätze und Best Practices für das Erstellen von Schemas zu lernen, die mit Experience Platform verwendet werden, sollten Sie zunächst die [Grundlagen der Schema-Komposition](schema/composition.md)lesen. Eine schrittweise Anleitung zum Erstellen eines Schemas finden Sie in den Lernprogrammen zum Erstellen eines Schemas [mit der API](tutorials/create-schema-api.md) oder [mithilfe der Benutzeroberfläche](tutorials/create-schema-ui.md).