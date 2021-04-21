---
keywords: Experience Platform;Home;beliebte Themen;API;XDM;XDM;Erlebnisdatenmodell;Erlebnisdatenmodell;Erlebnisdatenmodell;Datenmodell;Datenmodell;Datenmodell;Schema-Registrierung;Schema-Registrierung;
solution: Experience Platform
title: API-Handbuch zur Registrierung von Schemas
description: Die Schema Registry API ermöglicht es Entwicklern, alle Schema und zugehörigen Experience Data Model-(XDM-)Ressourcen innerhalb von Adobe Experience Platform programmatisch zu verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
topic-legacy: developer guide
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 2%

---

# [!DNL Schema Registry] API-Handbuch

Das [!DNL Schema Registry] wird verwendet, um auf die Schema-Bibliothek in Adobe Experience Platform zuzugreifen. Es stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle verfügbaren Bibliotheksressourcen zugänglich sind.

Die Schema Registry API bietet mehrere Endpunkte, mit denen Sie alle Schema und zugehörigen XDM-Ressourcen (Experience Data Model) programmgesteuert verwalten können, die Ihnen in der Plattform zur Verfügung stehen. Dazu gehören die von Adobe, [!DNL Experience Platform] Partnern und Anbietern, deren Anwendungen Sie verwenden, definierten Parameter.

Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern.[](./getting-started.md)

>[!IMPORTANT]
>
>XDM verwendet JSON-Schema-Formatierung, um die Struktur der erfassten Kundenerlebnisdaten zu beschreiben und zu validieren. Bevor Sie mit der Schema Registry API arbeiten, sollten Sie sich unbedingt die [offizielle JSON-Schema-Dokumentation](https://json-schema.org/) ansehen, um ein besseres Verständnis dieser zugrunde liegenden Technologie zu erhalten.

Um alle verfügbaren Endpunkte und CRUD-Vorgänge Ansicht, besuchen Sie die [Schema Registry API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Schemas

XDM-Schema stellen die Struktur und das Format der Daten dar, die in Plattform erfasst werden, und überprüfen sie. Ein Schema besteht aus einer Klasse und null oder mehr Mixins. Sie können Schema mit dem Endpunkt `/schemas` erstellen, Ansicht, bearbeiten und löschen. Informationen zur Verwendung dieses Endpunkts finden Sie im Endpunktleitfaden [Schema](./schemas.md).

Eine schrittweise Anleitung zum Erstellen eines vollständigen Schemas in der Schema-Registrierungs-API, einschließlich Erstellen und Hinzufügen von Mixins und Datentypen, finden Sie im Lernprogramm [API-Schema erstellen](../tutorials/create-schema-api.md).

## Verhalten

Verhalten definieren die Art der Daten, die ein Schema beschreibt. Jede XDM-Klasse muss auf ein bestimmtes Verhalten verweisen, das von allen Schemas, die diese Klasse verwenden, übernommen wird. Informationen zur Ansicht der verfügbaren Verhaltensweisen in der API finden Sie im Handbuch [verhaltensbasierte Endpunkte](./behaviors.md).

## Klassen

Eine Klasse definiert die Basisstruktur von allgemeinen Eigenschaften, die alle Schema, die auf dieser Klasse basieren, enthalten müssen, und bestimmt, welche Mixins für die Verwendung in diesen Schemas geeignet sind. Jede Klasse muss mit einem vorhandenen Verhalten verknüpft sein. Weitere Informationen zum Arbeiten mit Klassen in der API finden Sie im Handbuch [classes endpoint guide](./classes.md).

## Mixins

Mixins sind wiederverwendbare Komponenten, die einen oder mehrere Felder definieren, die ein bestimmtes Konzept repräsentieren, z. B. eine einzelne Person, eine Postanschrift oder eine Webbrowser-Umgebung. Mixins sind als Teil eines Schemas gedacht, das eine kompatible Klasse implementiert, je nach dem Verhalten der von ihnen dargestellten Daten (Datensatz oder Zeitreihen). Informationen zum Arbeiten mit Mixins in der API finden Sie im Handbuch [mixins endpoint.](./mixins.md)

## Datentypen

Datentypen werden in Klassen oder Mixins genauso wie einfache Literalfelder als Referenztypen verwendet, wobei der Hauptunterschied darin besteht, dass Datentypen mehrere Unterfelder definieren können. Ähnlich wie Mixins, da sie die einheitliche Verwendung einer Mehrfeldstruktur ermöglichen, sind die Datentypen flexibler, da sie an jeder beliebigen Stelle in der Schema-Struktur enthalten sein können, während Mixins nur auf der Stammebene hinzugefügt werden können. Weitere Informationen zum Arbeiten mit Datentypen in der API finden Sie im Endpunkthandbuch [Datentypen](./data-types.md).

## Deskriptoren

Deskriptoren sind Metadaten-Sätze, die bestimmten Feldern in einem Schema zugewiesen werden, und bieten verschiedene kontextbezogene Details, wie diese Felder (und das Schema selbst) mit anderen Schemas verwandt sind. Jedes Schema kann eine oder mehrere Deskriptorentitäten anwenden, und es gibt mehrere verschiedene Deskriptortypen, die unterschiedlichen Zwecken dienen. Weitere Informationen zum Arbeiten mit Deskriptoren in der API sowie eine Übersicht über die verschiedenen Deskriptortypen und ihre Anwendungsfälle finden Sie im Handbuch [descriptors endpoint guide](./descriptors.md).

## Vereinigungen

Obwohl Plattform es Ihnen ermöglicht, Schema für bestimmte Anwendungsfälle zu erstellen, ermöglicht es Ihnen, eine &quot;Vereinigung&quot;von Schemas zu einer bestimmten Klasse zusammenzustellen. Ein Vereinigung-Schema Aggregat die Felder aller Schema, die dieselbe Klasse teilen, in einer einzigen Darstellung. Durch Aktivierung eines Schemas für die Verwendung mit [Echtzeit-Kundenkonto](../../profile/home.md) wird dieses Schema in die Vereinigung für die jeweilige Klasse aufgenommen. Vereinigung-Schema können daher nicht direkt bearbeitet werden und können nur dadurch beeinträchtigt werden, dass Schema für die Verwendung in Profil einbezogen oder ausgeschlossen werden.

Informationen zum Ansicht von Vereinigungen in der Schema Registry-API finden Sie im Endpunktleitfaden [Vereinigungen](./unions.md).

## Export/Import

Mit der Schema Registry API können Sie XDM-Ressourcen zwischen Sandboxen und IMS-Organisationen übertragen und freigeben. Für jedes Schema, jede Mischung oder jeden Datentyp können Sie eine Export-Nutzlast generieren, die die Ressourcenstruktur und alle abhängigen Ressourcen enthält. Diese Payload kann dann verwendet werden, um die Ressource in eine Ziel-Sandbox und IMS-Org zu importieren.

Weitere Informationen zur Verwendung dieser Endpunkte finden Sie im Handbuch [export/import endpoints](./export-import.md).

## Sample data

Sie können Musterdaten für jedes angegebene Schema in der Schema-Bibliothek generieren. Das zurückgegebene Antwortobjekt kann dann als Datenquelle für die Datenerfassung verwendet werden.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im Handbuch [Beispiel-Datenendpunkt](./sample-data.md).

## Auditprotokoll

Die Schema-Registrierung führt ein Protokoll aller Änderungen, die zwischen verschiedenen Aktualisierungen an einer Ressource (Klasse, Mixin, Datentyp oder Schema) vorgenommen wurden. Sie können das Protokoll für eine bestimmte Ressource abrufen, indem Sie die `$id` oder `meta:altId` im Pfad einer GET-Anforderung zu diesem Endpunkt angeben.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im Handbuch [Auditprotokoll-Endpunkt](./audit-log.md).

## Nächste Schritte

Um mit dem Aufrufen mit der Schema Registry API zu beginnen, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) und wählen Sie dann eine der Endpunktleitfäden aus, um zu erfahren, wie bestimmte Endpunkte verwendet werden.
