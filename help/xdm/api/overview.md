---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Datenmodell; Schemaregistrierung; Schema Registry;
solution: Experience Platform
title: Handbuch zur Schema Registry-API
description: Mit der Schema Registry-API können Entwickler alle Schemas und zugehörigen Experience-Datenmodell (XDM)-Ressourcen in Adobe Experience Platform programmgesteuert verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
topic-legacy: developer guide
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 9%

---

# [!DNL Schema Registry]-API-Handbuch

Die [!DNL Schema Registry] wird verwendet, um auf die Schema Library in Adobe Experience Platform zuzugreifen und eine Benutzeroberfläche und RESTful-API bereitzustellen, über die alle verfügbaren Bibliotheksressourcen zugänglich sind.

Die Schema Registry-API bietet mehrere Endpunkte, mit denen Sie alle Schemas und zugehörigen Experience-Datenmodell (XDM)-Ressourcen, die Ihnen in Platform zur Verfügung stehen, programmgesteuert verwalten können. Dies schließt die durch die Adobe definierten [!DNL Experience Platform] Partner und Anbieter, deren Anwendungen Sie verwenden.

Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

>[!IMPORTANT]
>
>XDM verwendet die JSON-Schema-Formatierung, um die Struktur der erfassten Kundenerlebnisdaten zu beschreiben und zu validieren. Bevor Sie mit der Schema Registry-API arbeiten, wird dringend empfohlen, die [offizielle JSON-Schema-Dokumentation](https://json-schema.org/) für ein besseres Verständnis dieser zugrunde liegenden Technologie.

Um alle verfügbaren Endpunkte und CRUD-Vorgänge anzuzeigen, besuchen Sie die [Referenz zur Schema Registry-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Schemata

XDM-Schemata stellen die Struktur und das Format der in Platform erfassten Daten dar und validieren sie. Ein Schema besteht aus einer Klasse und keiner oder mehr Schemafeldgruppen. Sie können Schemata mit dem `/schemas` -Endpunkt. Informationen zur Verwendung dieses Endpunkts finden Sie unter [Endpunktleitfaden für Schemata](./schemas.md).

Eine schrittweise Anleitung zum Erstellen eines vollständigen Schemas in der Schema Registry-API, einschließlich Erstellen und Hinzufügen von Feldergruppen und Datentypen, finden Sie im Abschnitt [Tutorial zur Erstellung von API-Schemas](../tutorials/create-schema-api.md).

## Verhalten

Verhaltensweisen definieren die Art der Daten, die ein Schema beschreibt. Jede XDM-Klasse muss auf ein bestimmtes Verhalten verweisen, das von allen Schemas übernommen wird, die diese Klasse verwenden. Siehe [Handbuch zum Verhaltensendpunkt](./behaviors.md) , um zu erfahren, wie Sie verfügbare Verhaltensweisen in der API anzeigen können.

## Klassen

Eine Klasse definiert die Basisstruktur von allgemeinen Eigenschaften, die alle Schemas, die auf dieser Klasse basieren, enthalten müssen, und bestimmt, welche Feldgruppen für die Verwendung in diesen Schemas geeignet sind. Jede Klasse muss mit einem vorhandenen Verhalten verknüpft sein. Siehe [Endpunktleitfaden für Klassen](./classes.md) für Details zum Arbeiten mit Klassen in der API.

## Feldergruppen

Feldergruppen sind wiederverwendbare Komponenten, die ein oder mehrere Felder definieren, die ein bestimmtes Konzept repräsentieren, z. B. eine Einzelperson, eine Postanschrift oder eine Webbrowser-Umgebung. Feldergruppen sind als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert, je nach dem Verhalten der Daten, die sie darstellen (Datensatz oder Zeitreihen). Siehe [Endpunktleitfaden für Feldergruppen](./field-groups.md) , um zu erfahren, wie Sie mit Feldergruppen in der API arbeiten.

## Datentypen

Datentypen werden in Klassen oder Feldergruppen auf die gleiche Weise wie einfache literale Felder als Referenztypen verwendet, wobei der wesentliche Unterschied darin besteht, dass Datentypen mehrere Unterfelder definieren können. Auch wenn sie Feldgruppen insofern ähnlich sind, als sie die konsistente Verwendung einer Mehrfeld-Struktur ermöglichen, sind Datentypen flexibler, da sie an einer beliebigen Stelle in die Schemastruktur aufgenommen werden können, während Feldgruppen nur auf der Stammebene hinzugefügt werden können. Siehe [Endleitfaden für Datentypen](./data-types.md) Weitere Informationen zum Arbeiten mit Datentypen in der API.

## Deskriptoren

Deskriptoren sind Metadatensätze, die bestimmten Feldern innerhalb eines Schemas zugewiesen werden und verschiedene kontextbezogene Details enthalten, darunter auch die Art und Weise, wie diese Felder (und das Schema selbst) mit anderen Schemas verbunden sind. Auf jedes Schema können eine oder mehrere Deskriptorentitäten angewendet werden, und es gibt mehrere verschiedene Deskriptortypen, die unterschiedlichen Zwecken dienen. Siehe [Endpunktleitfaden für Deskriptoren](./descriptors.md) für weitere Informationen zum Arbeiten mit Deskriptoren in der API sowie einen Überblick über die verschiedenen Deskriptortypen und ihre Anwendungsfälle.

## Vereinigungen

Platform ermöglicht es Ihnen zwar, Schemas für bestimmte Anwendungsfälle zu erstellen, ermöglicht es Ihnen aber auch, eine &quot;Vereinigung&quot;von Schemas zu erstellen, die zu einer bestimmten Klasse gehören. Ein Vereinigungsschema aggregiert die Felder aller Schemas, die dieselbe Klasse teilen, in einer einzigen Darstellung. Durch Aktivierung eines Schemas zur Verwendung mit [Echtzeit-Kundenprofil](../../profile/home.md), wird dieses Schema in die Vereinigung für die jeweilige Klasse aufgenommen. Vereinigungsschemata können daher nicht direkt bearbeitet werden und können nur durch das Einschließen oder Ausschließen von Schemas zur Verwendung in Profil beeinflusst werden.

Informationen zum Anzeigen von Vereinigungen in der Schema Registry-API finden Sie unter [Endpunktleitfaden für Vereinigungen](./unions.md).

## Konvertierung von CSV in Schemas {#csv-to-schema}

Sie können automatisch ein XDM-Schema mit einer CSV-Datei als Vorlage generieren, um Vorlagen zum Massenimport von Schemafeldern zu erstellen und die manuelle API- oder UI-Arbeit zu reduzieren.

Siehe [Handbuch zur Konversion von CSV zu Schemas](./export.md) für weitere Informationen.

## Exportieren {#export}

Mit der Schema Registry-API können Sie XDM-Ressourcen zwischen Sandboxes und IMS-Organisationen übertragen und freigeben. Für jedes Schema, jede Feldergruppe oder jeden Datentyp können Sie eine Export-Payload generieren, die die Struktur der Ressource und alle abhängigen Ressourcen enthält. Diese Payload kann dann verwendet werden, um die Ressource in eine Ziel-Sandbox und IMS-Organisation zu importieren.

Siehe [Export-Endpunkthandbuch](./export.md) für weitere Informationen zum Erstellen einer Export-Payload für eine vorhandene XDM-Ressource.

## Importieren

Wenn Sie [export](#export) oder [Konvertierung von CSV in Schemas](./import.md) -Endpunkte zum Erstellen einer Export-Payload können Sie diese Payload an eine Zielorganisation und Sandbox senden, um die angegebenen Ressourcen zu importieren.

Siehe [Import-Endpunkthandbuch](./export.md) für weitere Informationen zum Generieren von XDM-Ressourcen aus Export-Payloads.

## Beispieldaten

Sie können Beispieldaten für jedes angegebene Schema in der Schema Library generieren. Das zurückgegebene Antwortobjekt kann dann als Quelle der Datenerfassung verwendet werden.

Siehe [Beispiel-Daten-Endpunkthandbuch](./sample-data.md) für weitere Informationen zur Verwendung dieses Endpunkts.

## Auditprotokoll

Die Schema Registry verwaltet ein Protokoll aller Änderungen, die zwischen verschiedenen Aktualisierungen an einer Ressource (Klasse, Feldergruppe, Datentyp oder Schema) vorgenommen wurden. Sie können das Protokoll für eine bestimmte Ressource abrufen, indem Sie ihr `$id` oder `meta:altId` im Pfad einer GET-Anfrage an diesen Endpunkt.

Siehe [Endpunktleitfaden für das Audit-Protokoll](./audit-log.md) für weitere Informationen zur Verwendung dieses Endpunkts.

## Nächste Schritte

Um mit der Durchführung von Aufrufen mit der Schema Registry API zu beginnen, lesen Sie das [Erste-Schritte-Handbuch](./getting-started.md) und wählen Sie dann eines der Endpunkt-Handbücher aus, um zu erfahren, wie Sie bestimmte Endpunkte verwenden.
