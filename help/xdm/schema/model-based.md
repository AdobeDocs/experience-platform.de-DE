---
keywords: Experience Platform;Startseite;beliebte Themen;modellbasiertes Schema;relationales Schema;relationale Schemata;Schema;Schema;Schema;XDM;Experience-Datenmodell;
solution: Experience Platform
title: Modellbasierte Schemata
description: Erfahren Sie mehr über modellbasierte Schemata (auch als relationale Schemata bezeichnet) in Adobe Experience Platform, einschließlich Funktionen, erforderliche Felder, Beziehungen und Einschränkungen.
badge: Eingeschränkte Verfügbarkeit
exl-id: 397e5937-b892-4fd3-b90e-29ed9229dc69
source-git-commit: 4586a820556919aeb6cebd94d961c3f726637f16
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 0%

---

# Modellbasierte Schemata

>[!AVAILABILITY]
>
>Data Mirror und modellbasierte Schemata stehen Adobe Journey Optimizer-Lizenzinhabern (**Kampagnen** zur Verfügung. Sie sind auch als **eingeschränkte Version** für Customer Journey Analytics-Benutzer verfügbar, je nach Ihrer Lizenz und der Aktivierung von Funktionen. Wenden Sie sich an den Adobe-Support, um Zugang zu erhalten.

Modellbasierte Schemata bieten ein flexibles, gesteuertes Modellierungsmuster zur Darstellung strukturierter Daten im Data Lake von Adobe Experience Platform. Sie unterstützen erzwungene Primärschlüssel, Beziehungen auf Schemaebene und eine differenzierte Kontrolle über Datensätze - alles ohne auf Vereinigungsschemata oder vollständige relationale Datenbanksysteme angewiesen zu sein.

>[!IMPORTANT]
>
>Überlegungen zum Löschen von Daten gelten für alle modellbasierten Schemaimplementierungen. Anwendungen, die diese Schemata verwenden, müssen verstehen, wie sich Löschungen auf zugehörige Datensätze, Compliance-Anforderungen und nachgelagerte Prozesse auswirken. Planen Sie Löschszenarien und überprüfen Sie [Datenhygiene-](../../hygiene/ui/record-delete.md#model-based-record-delete)) vor der Implementierung.

>[!NOTE]
>
>Anwendungen können modellbasierte Schemata als „relationale Schemata“ bezeichnen, wenn sie die Schemaerstellung für Anwendungsfälle der relationalen Datenmodellierung anfordern.

Verwenden Sie modellbasierte Schemata, um:

* Datenintegrität mit erzwungenen Primärschlüsseln mit einem Feld oder mit zusammengesetzten Schlüsseln sicherstellen.
* Aktivieren Sie präzises Änderungs-Tracking mithilfe der Versionierung für Einfügungen, Aktualisierungen und Löschungen.
* Definieren Sie wiederverwendbare Beziehungen auf Schemaebene, um Entitätsverbindungen in der realen Welt zu modellieren.
* Vermeiden Sie das programmübergreifende Duplizieren von Schemastrukturen, indem Sie mehrere Datenmodelle unterstützen.
* Überspringen Sie die Vereinigungsschemaeinschränkungen, um das Onboarding zu optimieren, das Aufblähen des Schemas zu reduzieren und unerwünschte Schemaänderungen zu vermeiden.

## Unterschiede zwischen modellbasierten Schemas und standardmäßigen XDM-Schemas

Standard-XDM-Schemata in Experience Platform folgen einem von drei Datenverhalten: Datensatz, Zeitreihen oder Ad-hoc. Definitionen und Details finden Sie unter [XDM-Datenverhalten](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home#data-behaviors).

Im traditionellen Modell sind Datensatz- und Zeitreihenschemas Teil von [Vereinigungsschemata](../api/unions.md) (siehe auch das [Handbuch zur Vereinigungsschema-Benutzeroberfläche](../../profile/ui/union-schema.md)). Diese Schemata entwickeln sich automatisch weiter[ wenn freigegebene (](./composition.md#field-group)) aktualisiert werden und benutzerdefinierte Felder unter einem Mandanten-Namespace verschachtelt werden müssen. Dieses Modell ist zwar leistungsstark, kann aber das Onboarding verlangsamen, übermäßig komplexe Schemata mit nicht verwendeten Feldern produzieren und zusätzliche Datenzuordnungen oder Umwandlungen erfordern. Diese Faktoren erhöhen die Lernkurve und den laufenden Wartungsaufwand.

Modellbasierte Schemata entfernen Vereinigungsschemaabhängigkeiten, wodurch automatische Aktualisierungen aus freigegebenen Feldergruppen vermieden werden und direkte Felddefinitionen ohne Einschränkungen für Mandanten-Namespaces möglich sind. Sie erhalten explizite Kontrolle über Primärschlüssel, Beziehungen und den anfänglichen Schemaentwurf, was die Modellierung der Daten zur Erstellungszeit vereinfacht.

## Funktionen modellbasierter Schemata

Verwenden Sie die folgenden Funktionen, um strukturierte Daten im Data Lake zu modellieren und dabei Governance, Integrität und Interoperabilität beizubehalten.

* **Unterstützung des Schemaverhaltens**: Konfigurieren von mit:
   * **Datensatzverhalten**: Erfasst den aktuellen Status einer Entität, z. B. eines Kunden, Kontos oder einer Kampagne.
   * **Zeitreihenverhalten**: Erfasst Ereignisse und den Zeitpunkt ihres Auftretens, was für das Tracking von Sequenzen oder Änderungen im Zeitverlauf nützlich ist.
* **Primäre Durchsetzung von Schlüsseln**: Definieren Sie einen Primärschlüssel, um jeden Datensatz eindeutig zu identifizieren und Duplikate während der Aufnahme zu vermeiden.
* **Versionskontrolle**: Verwenden Sie eine **Versionskennung** (einen Deskriptor), um sicherzustellen, dass Aktualisierungen in der richtigen Reihenfolge angewendet werden, auch wenn Datensätze nicht in der richtigen Reihenfolge eingehen.
* **Beziehungszuordnung**: Erstellen Sie Eins-zu-eins- oder Viele-zu-eins-Beziehungen zwischen modellbasierten Schemas oder zwischen modellbasierten und Standardschemas. Beziehungsdefinitionen werden als Deskriptoren gespeichert, um effiziente Joins zu ermöglichen.
* **Vereinfachte Entwicklung**: Modellbasierte Schemata sind nicht Teil von Vereinigungsansichten und werden nicht aktualisiert, wenn sich freigegebene Feldergruppen ändern, was unerwartete nachgelagerte Änderungen verhindert.
* **Flexible Felddefinition**: Fügen Sie Felder direkt ohne den Namespace der Mandanten-ID hinzu. Modellbasierte Schemata unterstützen keine XDM-Feldergruppen.
* **Keine Abhängigkeit von Vereinigungsschemata**: Verbessert die Abfrageleistung und reduziert den betrieblichen Mehraufwand für die Verwaltung globaler Schemaansichten.
* **Ereigniszeitreihenfolge**: Verwenden Sie bei Zeitreihenschemata einen **Zeitstempelbezeichner**, um Ereignisse nach Ereigniszeit anstatt nach Aufnahmezeit zu sortieren.

## Erforderliche Felder

Modellbasierte Schemata erfordern bestimmte Deskriptoren - Metadaten in der Schemadefinition, die wichtige Verhaltensweisen und Einschränkungen steuern. Fügen Sie die folgenden Deskriptoren als Teil Ihrer Schemadefinition hinzu.

### Primärer Schlüsseldeskriptor

Verwenden Sie einen Primärschlüsseldeskriptor, um sicherzustellen, dass jeder Datensatz eindeutig identifizierbar ist. Folgende Konfigurationen werden unterstützt:

* **Primärschlüssel mit einem Feld**: Verwenden Sie für jeden Datensatz ein Feld mit einem eindeutigen Wert.
* **Zusammengesetzter Primärschlüssel**: Mehrere Felder zur Erstellung einer eindeutigen Kennung verwenden. Bei Zeitreihenschemata muss der zusammengesetzte Schlüssel das Zeitstempelfeld enthalten, das durch den Zeitstempeldeskriptor identifiziert wird.

>[!NOTE]
>
>Im Benutzeroberflächenschema-Editor werden der Versionsdeskriptor und der Zeitstempeldeskriptor als &quot;[!UICONTROL Versionskennung“ &#x200B;] &quot;[!UICONTROL Zeitstempelkennung]&quot; angezeigt.

**Beispiel (ein Feld):**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": "customerId"
}
```

**Beispiel (Composite für Zeitreihen)**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": ["customerId", "eventTimestamp"]
}
```

### Versionsdeskriptor (Kennung)

Definieren Sie einen Versionsdeskriptor (Bezeichner), um den korrekten Datensatzstatus beizubehalten und sicherzustellen, dass die neueste Aktualisierung angewendet wird. Wenn mehrere Datensätze denselben Primärschlüssel gemeinsam haben, wird der Datensatz mit dem höchsten Versionswert als der neueste Datensatz betrachtet.

**Beispiel:**

```json
{
  "xdm:descriptor": "xdm:descriptorVersion",
  "xdm:sourceProperty": "lastModified"
}
```

### Zeitstempel-Deskriptor (Kennung)

Definieren Sie für Zeitreihenschemata einen Zeitstempeldeskriptor (Bezeichner), um die Ereigniszeit für die Sortierung festzulegen.

**Beispiel:**

```json
{
  "xdm:descriptor": "xdm:descriptorTimestamp",
  "xdm:sourceProperty": "eventTimestamp"
}
```

>[!NOTE]
>
>Deskriptoren sind Teil der Metadaten der Schemadefinition und werden nicht in Datenzeilen gespeichert.

Anweisungen zum Erstellen von Deskriptoren im Schema-Editor finden Sie unter [Erstellen von Deskriptoren im Schema-Editor](../tutorials/relationship-ui.md). Informationen zur API-basierten Erstellung finden Sie unter [Erstellen von Deskriptoren mithilfe der API](../tutorials/relationship-api.md).

## Beziehungsunterstützung {#relationship-support}

Die relationale Datenmodellierung ist eine primäre Verwendung modellbasierter Schemata. Anwendungsfälle können sich sogar auf diese Schemata beziehen „relationale Schemata“. Beziehungsdeskriptoren ermöglichen diese Verbindungen, indem sie Datensätze schemaübergreifend verknüpfen, ohne Fremdschlüssel in Datenzeilen einzubetten. Sie verbessern die referenzielle Integrität, ermöglichen wiederverwendbare Modellierungsmuster und unterstützen programmübergreifend verbundene Abfragen.

Erstellen Sie Beziehungsdeskriptoren auf Schemaebene für eine dynamische Auflösung zum Zeitpunkt der Abfrage. Kardinalitätswerte (1:1, Viele-zu-eins) bieten eine Orientierungshilfe, erzwingen jedoch keine Einschränkungen während der Aufnahme und unterstützen eine flexible Datenmodellierung über verbundene Datensätze hinweg.

Bevor Sie Beziehungsdeskriptoren hinzufügen, bestimmen Sie den entsprechenden Typ und die Zielgruppe:

* **Eins-zu-eins** - Jeder Datensatz im Quellschema entspricht höchstens einem Datensatz im Zielschema.
* **Viele zu eins** - Mehrere Datensätze im Quellschema können auf denselben Datensatz im Zielschema verweisen.

>[!NOTE]
>
>Sie können Beziehungen zwischen zwei modellbasierten Schemata oder zwischen einem modellbasierten Schema und einem Standardschema definieren. Beziehungen zu Ad-hoc-Schemata werden nicht unterstützt.

<!-- Q) 
Madeline commented: "model-based schema to standard might only be offered for b2b customers; that's how it will be on the UI" - is that still accurate? -->

**Beispiel: Eins-zu-eins-Beziehung**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "accountId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/account",
  "xdm:destinationProperty": "accountId"
}
```

<!-- Q) 
Should these be `@type: "xdm:descriptorRelationship",` This could be a copy-pasting error? -->

**Beispiel: Viele-zu-eins-Beziehung**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "customerId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/customer",
  "xdm:destinationProperty": "customerId"
}
```

Eine Liste der Beziehungsdeskriptortypen und der Syntax finden Sie unter [Deskriptoren-API-Referenz](../api/descriptors.md). Um zu erfahren, wie Sie diese Konzepte in der Praxis anwenden, folgen Sie den Tutorials zum [Definieren einer Beziehung in der API](../tutorials/relationship-api.md) oder [Erstellen einer Beziehung in der Benutzeroberfläche](../tutorials/relationship-ui.md).

>[!NOTE]
>
>Da Beziehungen auf Schemaebene definiert werden, müssen Sie sicherstellen, dass Sie verwandte Datensätze explizit in Ihren Abfragen verbinden. Verwenden Sie ein Tool wie Data Distiller, um diese Beziehungen während der Abfragezeit aufzulösen.

>[!IMPORTANT]
>
>Die Beziehungskardinalität ist informativ und wird bei der Aufnahme nicht erzwungen. Sie wird nur angewendet, wenn Beziehungen während einer Abfrage oder Analyse aufgelöst werden. Verlassen Sie sich nicht auf Kardinalitätseinstellungen, um Ihre Daten während der Aufnahme zu validieren. Überprüfen und bereinigen Sie Ihre Daten selbst und stellen Sie sicher, dass die von Ihnen definierten Beziehungsregeln mit der Art und Weise übereinstimmen, wie Sie die Daten abfragen oder analysieren möchten.

>[!NOTE]
>
> Modellbasierte Schemata können eine Verknüpfung zu Standardschemata, jedoch nicht zu Ad-hoc-Schemata herstellen.

## Überlegungen zum Löschen und zur Datenhygiene {#data-hygiene-support}

Modellbasierte Schemata ermöglichen präzise Löschungen auf Datensatzebene, die universelle Auswirkungen auf alle Anwendungen und Anwendungsfälle haben. Primäre Schlüssel-, Version- und Zeitstempeldeskriptoren bilden die Grundlage für die genaue Identifizierung von Datensätzen während Löschvorgängen.

### Auswirkungen des universellen Löschens

Alle Anwendungen, die modellbasierte Schemata verwenden, müssen Folgendes berücksichtigen:

* **Referenzintegrität**: Löschungen können sich auf verwandte Datensätze in allen verbundenen Datensätzen auswirken
* **Compliance-Anforderungen**: Einige Branchen erfordern ein spezifisches Löschverhalten und Audit-Trails
* **Anwendungsverhalten**: Nachgelagerte Systeme müssen möglicherweise Löschereignisse angemessen handhaben
* **Datenkonsistenz**: Verknüpfte Datensätze müssen beim Löschen konsistent bleiben
* **Löschplanung**: Berücksichtigung nachgelagerter Auswirkungen auf alle verbundenen Datensätze und Anwendungen während der Designphase

Eine Implementierungsanleitung finden Sie unter [Löschen von Datensätzen aus modellbasierten Datensätzen](../../hygiene/ui/record-delete.md#model-based-record-delete).

## Einschränkungen und Überlegungen {#limitations}

Überprüfen Sie die folgenden Einschränkungen, bevor Sie modellbasierte Schemata verwenden:

* Modellbasierte Schemata werden nicht in Vereinigungsschemata einbezogen.
* Die Schemaentwicklung erfolgt manuell. Sie werden nicht automatisch aktualisiert, wenn sich die Feldergruppen ändern.

>[!IMPORTANT]
>
>Die Schemaentwicklung wird eingeschränkt, nachdem ein Datensatz mithilfe des Schemas initialisiert wurde. Planen Sie Feldnamen und -typen sorgfältig im Voraus, da Felder nach der Aufnahme von Daten nicht mehr gelöscht oder geändert werden können.

* Beziehungen sind auf Eins-zu-eins und Viele-zu-eins beschränkt.
* Die Verfügbarkeit hängt von Ihrer Lizenz oder der Aktivierung von Funktionen ab.
* Zusammengesetzte Primärschlüssel sind für Zeitreihenschemata erforderlich.
