---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Grundlagen der Schema-Komposition
topic: overview
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '2628'
ht-degree: 60%

---


# Grundlagen der Schema-Komposition

This document provides an introduction to [!DNL Experience Data Model] (XDM) schemas and the building blocks, principles, and best practices for composing schemas to be used in Adobe Experience Platform. For general information on XDM and how it is used within [!DNL Platform], see the [XDM System overview](../home.md).

## Verstehen von Schemas

Ein Schema ist ein Regelsatz, der die Datenstruktur und das Datenformat darstellt und überprüft. Auf hoher Ebene bieten Schemas eine abstrakte Definition eines realen Objekts (z. B. einer Person) und legen dar, welche Daten in jeder Instanz dieses Objekts enthalten sein sollen (z. B. Vorname, Nachname, Geburtsdatum usw.).

Zusätzlich zur Beschreibung der Datenstruktur wenden Schemas Einschränkungen und Erwartungen an Daten an, damit diese bei ihren Bewegungen zwischen den Systemen validiert werden können. Diese Standarddefinitionen ermöglichen eine konsistente Interpretation der Daten, unabhängig von ihrer Herkunft, und machen eine anwendungsübergreifende Übersetzung überflüssig.

[!DNL Experience Platform]Die erhält diese semantische Normalisierung durch die Verwendung von Schemas aufrecht. Schemas are the standard way of describing data in [!DNL Experience Platform], allowing all data that conforms to schemas to be reusable without conflicts across an organization and even to be sharable between multiple organizations.

### Relationale Tabellen versus eingebettete Objekte

Bei der Arbeit mit relationalen Datenbanken bestehen die Best Practices darin, Daten zu normalisieren oder eine Entität in diskrete Teile zu zerlegen, die dann in mehreren Tabellen angezeigt werden. Um die Daten als Ganzes zu lesen oder die Entität zu aktualisieren, müssen Lese- und Schreibvorgänge über viele einzelne Tabellen mit JOIN durchgeführt werden.

Durch den Einsatz von eingebetteten Objekten können XDM-Schemas komplexe Daten direkt darstellen und in eigenständigen Dokumenten mit hierarchischer Struktur speichern. Einer der Hauptvorteile dieser Struktur besteht darin, dass Sie damit die Daten abfragen können, ohne die Entität durch teure Verbindungen zu mehreren denormalisierten Tabellen rekonstruieren zu müssen.

### Schemas und Big Data

Moderne digitale Systeme generieren enorme Mengen von Verhaltenssignalen (Transaktionsdaten, Weblogs, Internet der Dinge, Anzeige usw.). Diese Big-Data-Daten bieten außergewöhnliche Möglichkeiten zur Optimierung von Erlebnissen, sind aber aufgrund der Größe und Vielfalt der Daten schwierig zu nutzen. Um aus den Daten Nutzen zu ziehen, müssen Struktur, Format und Definitionen standardisiert werden, damit sie konsistent und effizient verarbeitet werden können.

Schemas lösen dieses Problem, indem sie die Integration von Daten aus mehreren Quellen, die Standardisierung durch gemeinsame Strukturen und Definitionen und die lösungsübergreifende gemeinsame Nutzung ermöglichen. Dadurch können nachfolgende Prozesse und Dienste jede Art von Frage beantworten, die von den Daten gestellt wird, und sich von dem herkömmlichen Ansatz zur Datenmodellierung abwenden, bei dem alle Fragen, die an die Daten gestellt werden, im Voraus bekannt sind und die Daten modelliert werden, um diesen Erwartungen zu entsprechen.

### Schema-based workflows in [!DNL Experience Platform]

Standardization is a key concept behind [!DNL Experience Platform]. XDM, von Adobe gesteuert, ist eine Bestrebung, Kundenerlebnisdaten zu standardisieren und Standard-Schemas für das Customer Experience Management zu definieren.

Die so genannte [!DNL Experience Platform] Infrastruktur, auf der Schema-basierte Workflows erstellt werden, ermöglicht die Erstellung von [!DNL XDM System][!DNL Schema Registry][!DNL Schema Editor]Schema-Metadaten und die Verwendung von Dienstmustern. Weitere Informationen finden Sie in der [XDM-Systemübersicht](../home.md).

## Planen Ihres Schemas

Der erste Schritt beim Erstellen eines Schemas besteht darin, das Konzept oder das Objekt der realen Welt zu bestimmen, das Sie im Schema erfassen möchten. Sobald Sie das Konzept, das Sie beschreiben möchten, identifizieren, können Sie mit der Planung Ihres Schemas beginnen, indem Sie über Dinge wie die Art der Daten, potenzielle Identitätsfelder und wie sich das Schema in Zukunft entwickeln könnte, nachdenken.

### Data behaviors in [!DNL Experience Platform]

Data intended for use in [!DNL Experience Platform] is grouped into two behavior types:

* **Aufzeichnen von Daten**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt könnte eine Organisation oder eine Einzelperson sein.
* **Zeitreihendaten**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt bereit, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

Alle XDM-Schemas beschreiben Daten, die als Datensatz- oder Zeitreihen kategorisiert werden können. Das Datenverhalten eines Schemas wird durch die **Klasse** des Schemas definiert, die einem Schema beim ersten Erstellen zugewiesen wird. XDM-Klassen werden nachstehend in diesem Dokument detailliert beschrieben.

Sowohl Schemas der Datensätze als auch der Zeitreihen enthalten eine Zuordnung der Identitäten (`xdm:identityMap`). Dieses Feld enthält die Identitätsdarstellung eines Subjekts, die aus den als „Identität“ markierten Feldern gezogen wird, wie im nächsten Abschnitt beschrieben.

### [!UICONTROL Identität]

Schemas are used for ingesting data into [!DNL Experience Platform]. Diese Daten können über mehrere Dienste hinweg verwendet werden, um eine einzelne, einheitliche Ansicht einer einzelnen Entität zu erstellen. Therefore, it is important when thinking about schemas to think about &quot;[!UICONTROL Identity]&quot; and which fields can be used to identify a subject regardless of where the data may be coming from.

To help with this process, key fields can be marked as &quot;[!UICONTROL Identity]&quot;. Upon data ingestion, the data in those fields will be inserted into the &quot;[!UICONTROL Identity Graph]&quot; for that individual. The graph data can then be accessed by [!DNL Real-time Customer Profile](../../profile/home.md) and other [!DNL Experience Platform] services to provide a stitched-together view of each individual customer.

Fields that are commonly marked as &quot;[!UICONTROL Identity]&quot; include: email address, phone number, [!DNL Experience Cloud ID (ECID)](https://docs.adobe.com/content/help/de-DE/id-service/using/home.html), CRM ID, or other unique ID fields. You should also consider any unique identifiers specific to your organization, as they may be good &quot;[!UICONTROL Identity]&quot; fields as well.

Es ist wichtig, während der Schema-Planungsphase über Kundenidentitäten nachzudenken, um sicherzustellen, dass die Daten zusammengeführt werden, um ein möglichst robustes Profil zu erstellen. Siehe [Identitätsdienst – Übersicht](../../identity-service/home.md), um mehr darüber zu erfahren, wie Identitätsinformationen Ihnen dabei helfen können, Ihren Kunden digitale Erlebnisse bereitzustellen.

### Schema-Evolutionsprinzipien {#evolution}

In dem Maße, wie sich die Art der digitalen Erfahrungen weiterentwickelt, müssen sich auch die Schemas, die zu ihrer Darstellung verwendet werden, weiterentwickeln. Ein gut entworfenes Schema ist daher in der Lage, sich bei Bedarf anzupassen und weiterzuentwickeln, ohne destruktive Änderungen an früheren Versionen des Schemas zu verursachen.

Since maintaining backwards compatibility is crucial for schema evolution, [!DNL Experience Platform] enforces a purely additive versioning principle to ensure that any revisions to the schema only result in non-destructive updates and changes. Mit anderen Worten: **brechende Änderungen werden nicht unterstützt.**

| Unterstützte Änderungen | Brechende Änderungen (nicht unterstützt) |
|------------------------------------|---------------------------------|
| <ul><li>Hinzufügen neuer Felder zu einem vorhandenen Schema</li><li>Definieren eines obligatorischen Felds als optional</li></ul> | <ul><li>Entfernen zuvor definierter Felder</li><li>Einführen neuer obligatorischer Felder</li><li>Umbenennen oder Neudefinieren vorhandener Felder</li><li>Entfernen oder Eingrenzen zuvor unterstützter Feldwerte</li><li>Verschieben von Attributen an eine andere Position in der Baumstruktur</li></ul> |

>[!NOTE]
>
>If a schema has not yet been used to ingest data into [!DNL Experience Platform], you may introduce a breaking change to that schema. However, once the schema has been used in [!DNL Platform], it must adhere to the additive versioning policy.

### Schemas und Datenaufnahme

In order to ingest data into [!DNL Experience Platform], a dataset must first be created. Datasets are the building blocks for data transformation and tracking for [!DNL Catalog Service](../../catalog/home.md), and generally represent tables or files that contain ingested data. Alle Datensätze basieren auf vorhandenen XDM-Schemas, die Einschränkungen dafür enthalten, was die aufgenommenen Daten enthalten und wie sie strukturiert sein sollten. Weitere Informationen hierzu finden Sie in der Übersicht über die [Adobe Experience Platform Datenaufnahme](../../ingestion/home.md).

## Bausteine eines Schemas

[!DNL Experience Platform]Die verwendet einen Kompositionsansatz, bei dem Standardbausteine kombiniert werden, um Schemas zu erstellen. This approach promotes the reusability of existing components and drives standardization across the industry to support vendor schemas and components in [!DNL Platform].

Schemas werden nach folgender Formel zusammengestellt:

**Klasse + Mixin&amp;ast; = XDM-Schema**

&amp;ast;Ein Schema besteht aus einer Klasse und _Null oder mehr_ Mixins. Dies bedeutet, dass Sie in Datensatzschema ohne jegliche Verwendung von Mixins erstellen könnten.

### Klasse

Das Erstellen eines Schemas beginnt mit dem Zuweisen einer Klasse. Klassen definieren die Verhaltensaspekte der Daten, die das Schema enthalten soll (Datensatz oder Zeitreihen). Darüber hinaus beschreiben Klassen die kleinste Anzahl gemeinsamer Eigenschaften, die alle Schemas, die auf dieser Klasse basieren, beinhalten müssen, und bieten eine Möglichkeit zum Zusammenführen mehrerer kompatibler Datensätze.

Eine Klasse bestimmt auch, welche Mixins für die Verwendung im Schema zugelassen werden. Dies wird im folgenden Abschnitt [Mixin](#mixin) ausführlicher erläutert.

There are standard classes provided with every integration of [!DNL Experience Platform], known as &quot;Industry&quot; classes. Branchenklassen sind allgemein anerkannte Industriestandards, die für eine breite Palette von Anwendungsfällen gelten. Examples of Industry classes include the [!DNL XDM Individual Profile] and [!DNL XDM ExperienceEvent] classes provided by Adobe.

[!DNL Experience Platform] ermöglicht auch &quot;Vendor&quot;-Klassen, bei denen es sich um von [!DNL Experience Platform] Partnern definierte Klassen handelt, die allen Kunden zur Verfügung gestellt werden, die den Service oder die Anwendung des Anbieters innerhalb [!DNL Platform]des Unternehmens nutzen.

There are also classes used to describe more specific use cases for individual organizations within [!DNL Platform], called &quot;Customer&quot; classes. Kundenklassen werden von einer Organisation definiert, wenn keine Branchen- oder Anbieterklassen zur Verfügung stehen, um einen einzigartigen Verwendungsfall zu beschreiben.

For example, a schema representing members of a Loyalty program describes record data about an individual and therefore can be based on the [!DNL XDM Individual Profile] class, a standard Industry class defined by Adobe.

### Mixin {#mixin}

Ein Mixin ist eine wiederverwendbare Komponente, die ein oder mehrere Felder definiert, die bestimmte Funktionen wie persönliche Details, Hotelpräferenzen oder Adressen implementieren. Mixins sind als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert.

Mixins definieren, mit welcher/n Klasse(n) sie kompatibel sind, basierend auf dem Verhalten der Daten, die sie darstellen (Datensatz- oder Zeitreihen). Das bedeutet, dass nicht alle Mixins für alle Klassen verfügbar sind.

Mixins have the same scope and definition as classes: there are Industry mixins, Vendor mixins, and Customer mixins that are defined by individual organizations using [!DNL Platform]. [!DNL Experience Platform]Die umfasst viele Standardbranchen-Mixins, erlaubt aber auch Anbietern, Mixins für ihre Benutzer und einzelnen Benutzern, Mixins für ihre eigenen spezifischen Konzepte zu definieren.

For example, to capture details such as &quot;[!UICONTROL First Name]&quot; and &quot;[!UICONTROL Home Address]&quot; for your &quot;[!UICONTROL Loyalty Members]&quot; schema, you would be able to use standard mixins that define those common concepts. However, concepts that are specific to less-common use cases (such as &quot;[!UICONTROL Loyalty Program Level]&quot;) often do not have a pre-defined mixin. In diesem Fall müssen Sie einen eigenen Mixin definieren, um diese Informationen zu erfassen.

Denken Sie daran, dass Schemas aus „Null oder mehr“ Mixins bestehen, was bedeutet, dass Sie ein gültiges Schema zusammenstellen können, ohne überhaupt Mixins zu verwenden.

### Datentyp {#data-type}

Datentypen werden als Referenzfeldtypen in Klassen oder Schemata auf die gleiche Weise verwendet wie grundlegende literale Felder. Der wesentliche Unterschied besteht darin, dass Datentypen mehrere Teilfelder definieren können. Ähnlich wie ein Mixin ermöglicht ein Datentyp die konsistente Verwendung einer Mehrfeldstruktur, ist jedoch flexibler als ein Mixin, da ein Datentyp an beliebiger Stelle in ein Schema aufgenommen werden kann, indem er als „Datentyp“ eines Feldes hinzugefügt wird.

[!DNL Experience Platform] bietet eine Reihe von gebräuchlichen Datentypen als Teil der [!DNL Schema Registry] zur Unterstützung der Verwendung von Standardmustern zur Beschreibung allgemeiner Datenstrukturen. This is explained in more detail in the [!DNL Schema Registry] tutorials, where it will become more clear as you walk through the steps to define data types.

### Feld

Ein Feld ist der grundlegendste Baustein eines Schemas. Felder bieten Einschränkungen hinsichtlich der Art der Daten, die sie enthalten können, indem sie einen bestimmten Datentyp definieren. Diese grundlegenden Datentypen definieren ein einzelnes Feld, wohingegen die zuvor erwähnten [Datentypen](#data-type) es Ihnen ermöglichen, mehrere Teilfelder zu definieren und dieselbe Mehrfeldstruktur in verschiedenen Schemas wiederzuverwenden. So, in addition to defining a field&#39;s &quot;data type&quot; as one of the data types defined in the registry, [!DNL Experience Platform] supports basic scalar types such as:

* Zeichenfolge
* Ganzzahl
* Zahl
* Boolesch
* Array
* Objekt

Die gültigen Bereiche dieser Skalartypen können weiter auf bestimmte Muster, Formate, Minima/Maxima oder vordefinierte Werte eingeschränkt werden. Mithilfe dieser Einschränkungen kann eine breite Palette speziellerer Feldtypen dargestellt werden, darunter:

* Enum
* Lang
* Kurz
* Byte
* Datum
* Datum-Uhrzeit
* Karte

>[!NOTE]
>
>Der Feldtyp „Karte“ ermöglicht Daten für Schlüssel-Wertepaare, einschließlich mehrerer Werte für einen einzelnen Schlüssel. Karten können nur auf Systemebene definiert werden, d. h. Sie können in einem branchen- oder herstellerdefinierten Schema auf eine Karte stoßen, diese steht jedoch nicht für die Verwendung in von Ihnen definierten Feldern zur Verfügung. Das [Entwicklerhandbuch für Schema-Registry-API](../api/getting-started.md) enthält weitere Informationen zum Definieren von Feldtypen.

Einige Datenoperationen, die von nachgeschalteten Diensten und Anwendungen verwendet werden, erzwingen Einschränkungen für bestimmte Feldtypen. Betroffene Dienste sind u. a., aber nicht ausschließlich:

* [!DNL Real-time Customer Profile](../../profile/home.md)
* [!DNL Identity Service](../../identity-service/home.md)
* [!DNL Segmentation](../../segmentation/home.md)
* [!DNL Query Service](../../query-service/home.md)
* [!DNL Data Science Workspace](../../data-science-workspace/home.md)

Bevor Sie ein Schema für die Verwendung in nachgelagerten Diensten erstellen, lesen Sie bitte die entsprechende Dokumentation für diese Dienste, um die Feldanforderungen und Einschränkungen für die Datenoperationen, für die das Schema bestimmt ist, besser zu verstehen.

### XDM-Felder

In addition to basic fields and the ability to define your own data types, XDM provides a standard set of fields and data types that are implicitly understood by [!DNL Experience Platform] services and provide greater consistency when used across [!DNL Platform] components.

These fields, such as &quot;First Name&quot; and &quot;Email Address&quot; contain added connotations beyond basic scalar field types, telling [!DNL Platform] that any fields sharing the same XDM data type will behave in the same way. This behavior can be trusted to be consistent regardless of where the data is coming from, or in which [!DNL Platform] service the data is being used.

Eine vollständige Liste der verfügbaren XDM-Felder finden Sie im [XDM-Feldwörterbuch](field-dictionary.md). It is recommended to use XDM fields and data types wherever possible to support consistency and standardization across [!DNL Experience Platform].

## Kompositionsbeispiel

Schemas represent the format and structure of data that will be ingested into [!DNL Platform], and are built using a composition model. Wie bereits erwähnt, bestehen diese Schemas aus einer Klasse und Null oder mehr Mixins, die mit dieser Klasse kompatibel sind.

For example, a schema describing purchases made at a retail store might be called &quot;[!UICONTROL Store Transactions]&quot;. The schema implements the [!DNL XDM ExperienceEvent] class combined with the standard [!UICONTROL Commerce] mixin and a user-defined [!UICONTROL Product Info] mixin.

Another schema which tracks website traffic might be called &quot;[!UICONTROL Web Visits]&quot;. It also implements the [!DNL XDM ExperienceEvent] class, but this time combines the standard [!UICONTROL Web] mixin.

Das folgende Diagramm zeigt diese Schemas und die von den einzelnen Mixins hinzugefügten Felder. It also contains two schemas based on the [!DNL XDM Individual Profile] class, including the &quot;[!UICONTROL Loyalty Members]&quot; schema mentioned previously in this guide.

![](../images/schema-composition/composition.png)

### Vereinigung {#union}

While [!DNL Experience Platform] allows you to compose schemas for particular use cases, it also allows you to see a &quot;union&quot; of schemas for a specific class type. The previous diagram shows two schemas based on the XDM ExperienceEvent class and two schemas based on [!DNL XDM Individual Profile] class. The union, shown below, aggregates the fields of all schemas that share the same class ([!DNL XDM ExperienceEvent] and [!DNL XDM Individual Profile], respectively).

![](../images/schema-composition/union.png)

By enabling a schema for use with [!DNL Real-time Customer Profile], it will be included in the union for that class type. [!DNL Profile] bietet stabile, zentralisierte Profil von Kundenattributen sowie ein zeitgestempeltes Kundenkonto für jedes Ereignis, das über ein in [!DNL Platform]das System integriertes System verfügt. [!DNL Profile] verwendet die vereinigte Ansicht, um diese Daten zu repräsentieren und eine ganzheitliche Ansicht jedes einzelnen Kunden bereitzustellen.

For more information on working with [!DNL Profile], see the [Real-time Customer Profile overview](../../profile/home.md).

## Zuordnen von Datendateien zu XDM-Schemas

All datafiles that are ingested into [!DNL Experience Platform] must conform to the structure of an XDM schema. Weitere Informationen zum Formatieren von Datendateien mit XDM-Hierarchien (einschließlich Beispieldateien) finden Sie im Dokument zu [Beispiel-ETL-Transformationen](../../etl/transformations.md). For general information about ingesting datafiles into [!DNL Experience Platform], see the [batch ingestion overview](../../ingestion/batch-ingestion/overview.md).

## Nächste Schritte

Now that you understand the basics of schema composition, you are ready to begin building schemas using the [!DNL Schema Registry].

The [!DNL Schema Registry] is used to access the [!DNL Schema Library] within Adobe Experience Platform, and provides a user interface and RESTful API from which all available library resources are accessible. The [!DNL Schema Library] contains Industry resources defined by Adobe, Vendor resources defined by [!DNL Experience Platform] partners, and classes, mixins, data types, and schemas that have been composed by members of your organization.

Um mit dem Erstellen von Schemas über die Benutzeroberfläche zu beginnen, folgen Sie dem [Schema-Editor-Tutorial](../tutorials/create-schema-ui.md), um das Schema „Loyalty Members“ zu erstellen, das in diesem Dokument erwähnt wird.

To begin using the [!DNL Schema Registry] API, start by reading the [Schema Registry API developer guide](../api/getting-started.md). Nachdem Sie das Entwicklerhandbuch gelesen haben, führen Sie die Schritte aus, die im Tutorial zum [Erstellen eines Schemas mit der Schema Registry-API](../tutorials/create-schema-api.md) beschrieben werden.
