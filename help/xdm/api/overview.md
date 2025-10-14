---
keywords: Experience Platform;Startseite;beliebte Themen;API;API;XDM;XDM-System;Experience-Datenmodell;Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell;Schemaregistrierung;Schemaregistrierung;
solution: Experience Platform
title: Handbuch zur Schema Registry-API
description: Mit der Schema Registry-API können Entwicklerinnen und Entwickler alle Schemas und zugehörigen Experience-Datenmodell (XDM)-Ressourcen in Adobe Experience Platform programmgesteuert verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 8%

---

# [!DNL Schema Registry]-API-Handbuch

Die [!DNL Schema Registry] wird verwendet, um auf die Schemabibliothek in Adobe Experience Platform zuzugreifen und eine Benutzeroberfläche und RESTful-API bereitzustellen, von der aus auf alle verfügbaren Bibliotheksressourcen zugegriffen werden kann.

Die Schema Registry-API bietet mehrere Endpunkte, mit denen Sie alle Schemas und zugehörigen Experience-Datenmodell (XDM)-Ressourcen, die Ihnen in Experience Platform zur Verfügung stehen, programmgesteuert verwalten können. Dazu gehören auch die von Adobe, [!DNL Experience Platform] und Anbietern definierten Anwendungen, die Sie verwenden.

Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

>[!IMPORTANT]
>
>XDM verwendet JSON-Schemaformatierung, um die Struktur der aufgenommenen Kundenerlebnisdaten zu beschreiben und zu validieren. Bevor Sie mit der Schema Registry-API arbeiten, wird dringend empfohlen, die [offizielle JSON-Schema-Dokumentation](https://json-schema.org/) zu lesen, um diese zugrunde liegende Technologie besser zu verstehen.

Um alle verfügbaren Endpunkte und CRUD-Vorgänge anzuzeigen, besuchen Sie die [API-Referenz zur Schemaregistrierung](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Schemata

XDM-Schemata stellen die Struktur und das Format von Daten dar, die in Experience Platform aufgenommen werden, und validieren diese. Ein Schema besteht aus einer Klasse und keiner oder mehreren Schemafeldgruppen. Sie können Schemas mithilfe des `/schemas`-Endpunkts erstellen, anzeigen, bearbeiten und löschen. Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch zu Schemas-Endpunkten](./schemas.md).

Eine schrittweise Anleitung zum manuellen Erstellen eines vollständigen Schemas in der Schema Registry-API, einschließlich des Erstellens und Hinzufügens von Feldergruppen und Datentypen, finden Sie im [API-Tutorial zur Schemaerstellung](../tutorials/create-schema-api.md).

Wenn Sie CSV-Daten aufnehmen, lesen Sie den Abschnitt zur [&#x200B; von CSV in Schemas](#csv-to-schema).

## Verhalten

Verhaltensweisen definieren die Art der Daten, die ein Schema beschreibt. Jede XDM-Klasse muss auf ein bestimmtes Verhalten verweisen, das alle Schemas, die diese Klasse verwenden, erben. Informationen [&#x200B; Anzeigen verfügbarer Verhaltensweisen in der API finden &#x200B;](./behaviors.md) im Handbuch zum Behaviors-Endpunkt .

## Klassen

Eine Klasse definiert die Basisstruktur von allgemeinen Eigenschaften, die alle Schemata enthalten müssen, die auf dieser Klasse basieren, und bestimmt, welche Feldergruppen für die Verwendung in diesen Schemata geeignet sind. Jede Klasse muss mit einem vorhandenen Verhalten verknüpft sein. Weitere Informationen zur Verwendung von Klassen in [&#x200B; API finden &#x200B;](./classes.md) im Klassenendpunkthandbuch .

## Feldergruppen

Feldergruppen sind wiederverwendbare Komponenten, die ein oder mehrere Felder definieren, die ein bestimmtes Konzept repräsentieren, z. B. eine einzelne Person, eine E-Mail-Adresse oder eine Webbrowser-Umgebung. Feldergruppen sind je nach dem Verhalten der Daten, die sie darstellen (Datensatz oder Zeitreihe), als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert. Informationen [&#x200B; Arbeiten mit Feldergruppen in der API &#x200B;](./field-groups.md) Sie im Handbuch zu Feldergruppen-Endpunkten .

## Datentypen

Datentypen werden in Klassen oder Feldergruppen auf dieselbe Weise als Felder vom Typ „Verweis“ verwendet wie grundlegende Literalfelder, wobei der wesentliche Unterschied darin besteht, dass Datentypen mehrere Unterfelder definieren können. Datentypen ähneln zwar den Feldergruppen insofern, als sie die konsistente Verwendung einer Struktur mit mehreren Feldern ermöglichen, sind jedoch flexibler, da sie an einer beliebigen Stelle in die Schemastruktur aufgenommen werden können, während Feldergruppen nur auf der Stammebene hinzugefügt werden können. Weitere Informationen [&#x200B; Arbeiten mit Datentypen in der API &#x200B;](./data-types.md) Sie im Handbuch zum Datentypendpunkt .

>[!NOTE]
>
>Wenn ein Feld als spezifischer Datentyp definiert ist, können Sie dasselbe Feld mit einem anderen Datentyp in einem anderen Schema nicht erstellen. Diese Einschränkung gilt für den Mandanten Ihrer Organisation.

## Deskriptoren

Deskriptoren sind Metadatensätze, die bestimmten Feldern innerhalb eines Schemas zugewiesen werden und verschiedene kontextuelle Details bereitstellen, darunter die Beziehung dieser Felder (und des Schemas selbst) zu anderen Schemas. Auf jedes Schema können eine oder mehrere Deskriptorentitäten angewendet werden. Es gibt mehrere verschiedene Deskriptortypen, die unterschiedlichen Zwecken dienen. Weitere Informationen zum Arbeiten mit Deskriptoren in [&#x200B; API sowie &#x200B;](./descriptors.md) Überblick über die verschiedenen Deskriptortypen und ihre Anwendungsfälle finden Sie im Handbuch zum descriptors-.

## Vereinigungen

Experience Platform ermöglicht es Ihnen zwar, Schemata für bestimmte Anwendungsfälle zu erstellen, aber auch, eine „Vereinigung“ von Schemata zu erstellen, die zu einer bestimmten Klasse gehören. Ein Vereinigungsschema aggregiert die Felder aller Schemata, die dieselbe Klasse haben, in einer einzigen Darstellung. Wenn Sie ein Schema für die Verwendung mit [Echtzeit-Kundenprofil](../../profile/home.md) aktivieren, wird dieses Schema in die Vereinigung für seine bestimmte Klasse aufgenommen. Vereinigungsschemata können daher nicht direkt bearbeitet werden und können nur durch das Ein- oder Ausschließen von Schemata zur Verwendung im Profil beeinflusst werden.

Informationen zum Anzeigen von Vereinigungen in der Schema Registry-API finden Sie im [Handbuch zum Vereinigungsendpunkt](./unions.md).

## Konvertierung von CSV in Schemas {#csv-to-schema}

Sie können automatisch ein XDM-Schema mithilfe einer CSV-Datei als Vorlage generieren, sodass Sie Vorlagen erstellen können, um Schemafelder per Massenimport zu importieren und den manuellen API- oder UI-Arbeitsaufwand zu reduzieren.

Weitere Informationen finden Sie [&#x200B; Handbuch zum Konvertierungsendpunkt von CSV &#x200B;](./export.md) Schema .

>[!NOTE]
>
>Sie können die Benutzeroberfläche auch verwenden, um ([&#x200B; einer CSV mithilfe von KI-generierten Empfehlungen einem Schema zuzuordnen](../../ingestion/tutorials/map-csv/recommendations.md) (derzeit in der Beta-Phase).

## Exportieren {#export}

Mit der Schema Registry-API können Sie XDM-Ressourcen zwischen Sandboxes und Organisationen übertragen und freigeben. Für jedes Schema, jede Feldergruppe oder jeden Datentyp können Sie eine Export-Payload generieren, die die Struktur der Ressource und alle abhängigen Ressourcen enthält. Diese Payload kann dann zum Importieren der Ressource in eine Ziel-Sandbox und in eine Organisation verwendet werden.

Weitere Informationen [&#x200B; Erstellen einer Export-Payload für &#x200B;](./export.md) vorhandene XDM-Ressource finden Sie im Handbuch zum Exportieren von Endpunkten .

## Importieren

Wenn Sie die Endpunkte [Export](#export) oder [CSV in Schema-Konversion](./import.md) zum Erstellen einer Export-Payload verwenden, können Sie diese Payload an eine Zielorganisation und Sandbox senden, um die angegebenen Ressourcen zu importieren.

Weitere Informationen zum Generieren von XDM[Ressourcen aus Export-Payloads finden Sie &#x200B;](./export.md) Handbuch zum Import-Endpunkt .

## Beispieldaten

Sie können Beispieldaten für jedes angegebene Schema in der Schemabibliothek generieren. Das zurückgegebene Antwortobjekt kann dann als Datenquelle für die Datenaufnahme verwendet werden.

Weitere Informationen [&#x200B; Verwendung dieses Endpunkts finden &#x200B;](./sample-data.md) im Handbuch zum Beispieldaten-.

## Auditprotokoll

Die Schemaregistrierung verwaltet ein Protokoll aller Änderungen, die an einer Ressource (Klasse, Feldergruppe, Datentyp oder Schema) zwischen verschiedenen Aktualisierungen vorgenommen wurden. Sie können das Protokoll für eine bestimmte Ressource abrufen, indem Sie deren `$id` oder `meta:altId` im Pfad einer GET-Anfrage an diesen Endpunkt angeben.

Weitere [&#x200B; zur Verwendung dieses Endpunkts finden &#x200B;](./audit-log.md) im Handbuch zum audit log endpoint .

## Nächste Schritte

Um mit der Durchführung von Aufrufen mit der Schema Registry API zu beginnen, lesen Sie das [Erste-Schritte-Handbuch](./getting-started.md) und wählen Sie dann eines der Endpunkt-Handbücher aus, um zu erfahren, wie Sie bestimmte Endpunkte verwenden.
