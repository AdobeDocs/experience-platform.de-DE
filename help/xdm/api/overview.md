---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: Entwicklerhandbuch zur Schema Registry-API
description: 'Mit der Schema Registry API können Sie alle Schema und zugehörigen XDM-Ressourcen, die Ihnen in der Experience Platform zur Verfügung stehen, programmatisch verwalten. '
topic: developer guide
translation-type: tm+mt
source-git-commit: 33f9ee45e8dd649d23f9b3b4f03ecf00d8e18fd2
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 5%

---


# [!DNL Schema Registry]-API-Entwicklerhandbuch

The [!DNL Schema Registry] is used to access the Schema Library within Adobe Experience Platform, providing a user interface and RESTful API from which all available library resources are accessible.

Die Schema Registry API bietet mehrere Endpunkte, mit denen Sie alle Schema und zugehörigen XDM-Ressourcen (Experience Data Model) programmgesteuert verwalten können, die Ihnen in der Plattform zur Verfügung stehen. This includes those defined by Adobe, [!DNL Experience Platform] partners, and vendors whose applications you use.

Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern. Weitere Informationen finden Sie im Handbuch [Erste Schritte](./getting-started.md) .

>[!IMPORTANT]
>
>XDM verwendet JSON-Schema-Formatierung, um die Struktur der erfassten Kundenerlebnisdaten zu beschreiben und zu validieren. Bevor Sie mit der Schema Registry API arbeiten, sollten Sie die [offizielle JSON-Schema-Dokumentation](https://json-schema.org/) lesen, um ein besseres Verständnis dieser zugrunde liegenden Technologie zu erhalten.

Um alle verfügbaren Endpunkte und CRUD-Vorgänge Ansicht, besuchen Sie die [Schema Registry API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Schemas

XDM-Schema stellen die Struktur und das Format der Daten dar, die in Plattform erfasst werden, und überprüfen sie. Ein Schema besteht aus einer Klasse und null oder mehr Mixins. You can create, view, edit, and delete schemas using the `/schemas` endpoint. Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Schemas-Endpunkthandbuch](./schemas.md).

Eine schrittweise Anleitung zum Erstellen eines vollständigen Schemas in der Schema Registry-API, einschließlich Erstellen und Hinzufügen von Mixins und Datentypen, finden Sie im Lernprogramm [zur Erstellung von](../tutorials/create-schema-api.md)API-Schemas.

## Verhalten

Verhalten definieren die Art der Daten, die ein Schema beschreibt. Jede XDM-Klasse muss auf ein bestimmtes Verhalten verweisen, das von allen Schemas, die diese Klasse verwenden, übernommen wird. Informationen zur Ansicht der verfügbaren Verhaltensweisen in der API finden Sie im [Endpunkthandbuch](./behaviors.md) &quot;Verhalten&quot;.

## Klassen

Eine Klasse definiert die Basisstruktur von allgemeinen Eigenschaften, die alle Schema, die auf dieser Klasse basieren, enthalten müssen, und bestimmt, welche Mixins für die Verwendung in diesen Schemas geeignet sind. Jede Klasse muss mit einem vorhandenen Verhalten verknüpft sein. Weitere Informationen zum Arbeiten mit Klassen in der API finden Sie im [Klassen-Endpunkthandbuch](./classes.md) .

## Mixins

Mixins sind wiederverwendbare Komponenten, die einen oder mehrere Felder definieren, die ein bestimmtes Konzept repräsentieren, z. B. eine einzelne Person, eine Postanschrift oder eine Webbrowser-Umgebung. Mixins sind als Teil eines Schemas gedacht, das eine kompatible Klasse implementiert, je nach dem Verhalten der von ihnen dargestellten Daten (Datensatz oder Zeitreihen). Informationen zum Arbeiten mit Mixins in der API finden Sie im [mixins-Endpunkthandbuch](./mixins.md) .

## Datentypen

Datentypen werden in Klassen oder Mixins genauso wie einfache Literalfelder als Referenztypen verwendet, wobei der Hauptunterschied darin besteht, dass Datentypen mehrere Unterfelder definieren können. Ähnlich wie Mixins, da sie die einheitliche Verwendung einer Mehrfeldstruktur ermöglichen, sind die Datentypen flexibler, da sie an jeder beliebigen Stelle in der Schema-Struktur enthalten sein können, während Mixins nur auf der Stammebene hinzugefügt werden können. Weitere Informationen zum Arbeiten mit Datentypen in der API finden Sie im Handbuch [zum](./data-types.md) Datentypendpunkt.

## Deskriptoren

Deskriptoren sind Metadaten-Sätze, die bestimmten Feldern in einem Schema zugewiesen werden, und bieten verschiedene kontextbezogene Details, wie diese Felder (und das Schema selbst) mit anderen Schemas verwandt sind. Jedes Schema kann eine oder mehrere Deskriptorentitäten anwenden, und es gibt mehrere verschiedene Deskriptortypen, die unterschiedlichen Zwecken dienen. Weitere Informationen zum Arbeiten mit Deskriptoren in der API sowie eine Übersicht über die verschiedenen Deskriptortypen und ihre Anwendungsfälle finden Sie im [Deskriptoren-Endpunkthandbuch](./descriptors.md) .

## Vereinigungen

Obwohl Plattform es Ihnen ermöglicht, Schema für bestimmte Anwendungsfälle zu erstellen, ermöglicht es Ihnen, eine &quot;Vereinigung&quot;von Schemas zu einer bestimmten Klasse zusammenzustellen. Ein Vereinigung-Schema Aggregat die Felder aller Schema, die dieselbe Klasse teilen, in einer einzigen Darstellung. Durch Aktivierung eines Schemas zur Verwendung mit [Echtzeit-Kundendaten](../../profile/home.md)wird dieses Schema für seine jeweilige Klasse in die Vereinigung aufgenommen. Vereinigung-Schema können daher nicht direkt bearbeitet werden und können nur dadurch beeinträchtigt werden, dass Schema für die Verwendung in Profil einbezogen oder ausgeschlossen werden.

Weitere Informationen zur Ansicht von Vereinigungen in der Schema Registry-API finden Sie im Handbuch [Vereinigungen-Endpunkt](./unions.md).

## Export/Import

Mit der Schema Registry API können Sie XDM-Ressourcen zwischen Sandboxen und IMS-Organisationen übertragen und freigeben. Für jedes Schema, jede Mischung oder jeden Datentyp können Sie eine Export-Nutzlast generieren, die die Ressourcenstruktur und alle abhängigen Ressourcen enthält. Diese Payload kann dann verwendet werden, um die Ressource in eine Ziel-Sandbox und IMS-Org zu importieren.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie in der API-Referenz [zur](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) Schema-Registrierung.

## Sample data

Sie können Musterdaten für jedes angegebene Schema in der Schema-Bibliothek generieren. Das zurückgegebene Antwortobjekt kann dann als Datenquelle für die Datenerfassung verwendet werden.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie in der API-Referenz [zur](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) Schema-Registrierung.

## Auditprotokoll

Die Schema-Registrierung führt ein Protokoll aller Änderungen, die zwischen verschiedenen Aktualisierungen an einer Ressource (Klasse, Mixin, Datentyp oder Schema) vorgenommen wurden. Sie können das Protokoll für eine bestimmte Ressource abrufen, indem Sie deren `$id` oder `meta:altId` im Pfad einer GET-Anforderung zu diesem Endpunkt angeben.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie in der API-Referenz [zur](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) Schema-Registrierung.

## Nächste Schritte

Um mit dem Aufrufen der Schema Registry API zu beginnen, lesen Sie die [Erste Schritte-Anleitung](./getting-started.md) und wählen Sie dann eine der Endpunktanleitungen, um zu erfahren, wie Sie bestimmte Endpunkte verwenden.