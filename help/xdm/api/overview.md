---
keywords: Experience Platform; home; beliebte Themen; api; API; XDM; XDM; XDM-System; Experience-Datenmodell; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Datenmodell; Schemaregistrierung; Schema Registry;
solution: Experience Platform
title: Handbuch zur Schema Registry-API
description: Mit der Schema Registry-API können Entwickler alle Schemas und zugehörigen Experience-Datenmodell (XDM)-Ressourcen in Adobe Experience Platform programmgesteuert verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: 6e58f070c0a25d7434f1f165543f92ec5a081e66
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 8%

---

# [!DNL Schema Registry]-API-Handbuch

Der [!DNL Schema Registry] wird verwendet, um auf die Schema Library in Adobe Experience Platform zuzugreifen und eine Benutzeroberfläche und RESTful-API bereitzustellen, über die alle verfügbaren Bibliotheksressourcen zugänglich sind.

Die Schema Registry-API bietet mehrere Endpunkte, mit denen Sie alle Schemas und zugehörigen Experience-Datenmodell (XDM)-Ressourcen, die Ihnen in Platform zur Verfügung stehen, programmgesteuert verwalten können. Dazu gehören Adobe, [!DNL Experience Platform] Partner und Anbieter, deren Anwendungen Sie verwenden.

Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

>[!IMPORTANT]
>
>XDM verwendet die JSON-Schema-Formatierung, um die Struktur der erfassten Kundenerlebnisdaten zu beschreiben und zu validieren. Bevor Sie mit der Schema Registry-API arbeiten, wird dringend empfohlen, die [offizielle JSON-Schema-Dokumentation](https://json-schema.org/) zu lesen, um ein besseres Verständnis dieser zugrunde liegenden Technologie zu erhalten.

Um alle verfügbaren Endpunkte und CRUD-Vorgänge anzuzeigen, besuchen Sie die [Schema Registry-API-Referenz](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Schemata

XDM-Schemata stellen die Struktur und das Format der in Platform erfassten Daten dar und validieren sie. Ein Schema besteht aus einer Klasse und keiner oder mehr Schemafeldgruppen. Sie können Schemas mit dem `/schemas` -Endpunkt erstellen, anzeigen, bearbeiten und löschen. Informationen zur Verwendung dieses Endpunkts finden Sie im [Schemas-Endpunkthandbuch](./schemas.md).

Eine schrittweise Anleitung zum manuellen Erstellen eines kompletten Schemas in der Schema Registry-API, einschließlich Erstellen und Hinzufügen von Feldergruppen und Datentypen, finden Sie im Tutorial zur Erstellung von API-Schemas](../tutorials/create-schema-api.md).[

Wenn Sie CSV-Daten erfassen, finden Sie weitere Informationen im Abschnitt [CSV zur Schemakonvertierung](#csv-to-schema).

## Verhalten

Verhaltensweisen definieren die Art der Daten, die ein Schema beschreibt. Jede XDM-Klasse muss auf ein bestimmtes Verhalten verweisen, das von allen Schemas übernommen wird, die diese Klasse verwenden. Informationen zum Anzeigen der verfügbaren Verhaltensweisen in der API finden Sie im [Endpoint-Handbuch zum Verhalten](./behaviors.md) .

## Klassen

Eine Klasse definiert die Basisstruktur von allgemeinen Eigenschaften, die alle Schemas, die auf dieser Klasse basieren, enthalten müssen, und bestimmt, welche Feldgruppen für die Verwendung in diesen Schemas geeignet sind. Jede Klasse muss mit einem vorhandenen Verhalten verknüpft sein. Weitere Informationen zum Arbeiten mit Klassen in der API finden Sie im [Klassen-Endpunkthandbuch](./classes.md) .

## Feldergruppen

Feldergruppen sind wiederverwendbare Komponenten, die ein oder mehrere Felder definieren, die ein bestimmtes Konzept repräsentieren, z. B. eine Einzelperson, eine Postanschrift oder eine Webbrowser-Umgebung. Feldergruppen sind als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert, je nach dem Verhalten der Daten, die sie darstellen (Datensatz oder Zeitreihen). Informationen zum Arbeiten mit Feldergruppen in der API finden Sie im Handbuch [Feldergruppen-Endpunkt](./field-groups.md) .

## Datentypen

Datentypen werden in Klassen oder Feldergruppen auf die gleiche Weise wie einfache literale Felder als Referenztypen verwendet, wobei der wesentliche Unterschied darin besteht, dass Datentypen mehrere Unterfelder definieren können. Auch wenn sie Feldgruppen insofern ähnlich sind, als sie die konsistente Verwendung einer Mehrfeld-Struktur ermöglichen, sind Datentypen flexibler, da sie an einer beliebigen Stelle in die Schemastruktur aufgenommen werden können, während Feldgruppen nur auf der Stammebene hinzugefügt werden können. Weitere Informationen zum Arbeiten mit Datentypen in der API finden Sie im [Endpunkthandbuch zu Datentypen](./data-types.md) .

>[!NOTE]
>
>Wenn ein Feld als spezifischer Datentyp definiert ist, können Sie dasselbe Feld mit einem anderen Datentyp nicht in einem anderen Schema erstellen. Diese Einschränkung gilt für den gesamten Mandanten Ihres Unternehmens.

## Deskriptoren

Deskriptoren sind Metadatensätze, die bestimmten Feldern innerhalb eines Schemas zugewiesen werden und verschiedene kontextbezogene Details enthalten, darunter auch die Art und Weise, wie diese Felder (und das Schema selbst) mit anderen Schemas verbunden sind. Auf jedes Schema können eine oder mehrere Deskriptorentitäten angewendet werden, und es gibt mehrere verschiedene Deskriptortypen, die unterschiedlichen Zwecken dienen. Weitere Informationen zum Arbeiten mit Deskriptoren in der API sowie einen Überblick über die verschiedenen Deskriptortypen und ihre Anwendungsfälle finden Sie im [Endpunkthandbuch zu Deskriptoren](./descriptors.md) .

## Vereinigungen

Platform ermöglicht es Ihnen zwar, Schemas für bestimmte Anwendungsfälle zu erstellen, ermöglicht es Ihnen aber auch, eine &quot;Vereinigung&quot;von Schemas zu erstellen, die zu einer bestimmten Klasse gehören. Ein Vereinigungsschema aggregiert die Felder aller Schemas, die dieselbe Klasse teilen, in einer einzigen Darstellung. Durch Aktivierung eines Schemas zur Verwendung mit [Echtzeit-Kundenprofil](../../profile/home.md) wird dieses Schema in die Vereinigung für die jeweilige Klasse aufgenommen. Vereinigungsschemata können daher nicht direkt bearbeitet werden und können nur durch das Einschließen oder Ausschließen von Schemas zur Verwendung in Profil beeinflusst werden.

Informationen zum Anzeigen von Vereinigungen in der Schema Registry-API finden Sie im [Vereinigungs-Endpunkthandbuch](./unions.md).

## Konvertierung von CSV in Schemas {#csv-to-schema}

Sie können automatisch ein XDM-Schema mit einer CSV-Datei als Vorlage generieren, um Vorlagen zum Massenimport von Schemafeldern zu erstellen und die manuelle API- oder UI-Arbeit zu reduzieren.

Weitere Informationen finden Sie im Leitfaden [CSV zum Schema-Konversions-Endpunkt](./export.md) .

>[!NOTE]
>
>Sie können die Benutzeroberfläche auch verwenden, um mit KI-generierten Empfehlungen](../../ingestion/tutorials/map-csv/recommendations.md) (aktuell in Beta) eine CSV-Datei einem Schema zuzuordnen.[

## Exportieren {#export}

Mit der Schema Registry-API können Sie XDM-Ressourcen zwischen Sandboxes und Organisationen übertragen und freigeben. Für jedes Schema, jede Feldergruppe oder jeden Datentyp können Sie eine Export-Payload generieren, die die Struktur der Ressource und alle abhängigen Ressourcen enthält. Diese Payload kann dann verwendet werden, um die Ressource in eine Ziel-Sandbox und eine Organisation zu importieren.

Weitere Informationen zum Erstellen einer Export-Payload für eine vorhandene XDM-Ressource finden Sie im [Export-Endpunkthandbuch](./export.md) .

## Importieren

Wenn Sie die Endpunkte [export](#export) oder [CSV to schema conversion](./import.md) verwenden, um eine Export-Payload zu erstellen, können Sie diese Payload an eine Zielorganisation und Sandbox senden, um die angegebenen Ressourcen zu importieren.

Weitere Informationen zum Generieren von XDM-Ressourcen aus Export-Payloads finden Sie im [Import-Endpunkthandbuch](./export.md) .

## Beispieldaten

Sie können Beispieldaten für jedes angegebene Schema in der Schema Library generieren. Das zurückgegebene Antwortobjekt kann dann als Quelle der Datenerfassung verwendet werden.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Beispiel-Daten-Endpunkthandbuch](./sample-data.md) .

## Auditprotokoll

Die Schema Registry verwaltet ein Protokoll aller Änderungen, die zwischen verschiedenen Aktualisierungen an einer Ressource (Klasse, Feldergruppe, Datentyp oder Schema) vorgenommen wurden. Sie können das Protokoll für eine bestimmte Ressource abrufen, indem Sie deren `$id` oder `meta:altId` im Pfad einer GET-Anfrage an diesen Endpunkt angeben.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunkt-Handbuch zum Auditprotokoll](./audit-log.md) .

## Nächste Schritte

Um mit der Durchführung von Aufrufen mit der Schema Registry API zu beginnen, lesen Sie das [Erste-Schritte-Handbuch](./getting-started.md) und wählen Sie dann eines der Endpunkt-Handbücher aus, um zu erfahren, wie Sie bestimmte Endpunkte verwenden.
