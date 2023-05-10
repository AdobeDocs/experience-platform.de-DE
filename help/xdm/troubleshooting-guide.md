---
keywords: Experience Platform;beliebte Themen;XDM;XDM-System;individuelles XDM-Profil;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience eventExperience event;XDM Experience Event;XDM ExperienceEvent;Experience-Datenmodell;Experience Datenmodell;experience datenmodell;Datenmodell;Schema;Fehlerbehebung;Häufig gestellte Fragen;häufig gestellte Fragen;Vereinigungsschema;VEREINIGUNGSPROFIL;Vereinigungsprofil;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: Handbuch zur Fehlerbehebung beim XDM-System
description: Hier finden Sie Antworten auf häufig gestellte Fragen zum Experience-Datenmodell (XDM), einschließlich schrittweiser Anweisungen zur Behebung gängiger API-Fehler.
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2073'
ht-degree: 100%

---

# Handbuch zur Fehlerbehebung beim XDM-System

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zum [!DNL Experience Data Model] (XDM) und XDM-System in Adobe Experience Platform, einschließlich einer Anleitung zur Behebung gängiger Fehler. Fragen und Fehlerbehebungen für andere Platform-Dienste finden Sie im [Handbuch zur Fehlerbehebung in Experience Platform](../landing/troubleshooting.md).

Das **[!DNL Experience Data Model] (XDM)** ist eine Open-Source-Spezifikation, die standardisierte Schemas für das Customer Experience Management definiert. Die Methodologie, auf der [!DNL Experience Platform] basiert, das **XDM-System**, nutzt [!DNL Experience Data Model]-Schemas, die für [!DNL Platform]-Services zur Verwendung bereitstehen. Die **[!DNL Schema Registry]** bietet eine Benutzeroberfläche und eine RESTful-API für den Zugriff auf die **[!DNL Schema Library]** innerhalb von [!DNL Experience Platform]. Weitere Informationen finden Sie in der [XDM-Dokumentation](home.md).

## Häufig gestellte Fragen

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zum XDM-System und zur Verwendung der [!DNL Schema Registry]-API.

### Wie füge ich einem Schema Felder hinzu?

Mithilfe einer Schemafeldgruppe können Sie einem Schema Felder hinzufügen. Jede Feldgruppe ist mit einer oder mehreren Klassen kompatibel, sodass die Feldgruppe in einem beliebigen Schema verwendet werden kann, das eine dieser kompatiblen Klassen implementiert. Adobe Experience Platform stellt mehrere branchenbezogene Feldgruppen mit eigenen vordefinierten Feldern bereit. Sie können jedoch eigene Felder zu einem Schema hinzufügen, indem Sie benutzerdefinierte Feldgruppen mithilfe der API oder der Benutzeroberfläche erstellen.

Details zum Erstellen von Feldgruppen in der [!DNL Schema Registry]-API finden Sie im [Handbuch zu Endpunkten für Feldgruppen](api/field-groups.md#create). Wenn Sie die Benutzeroberfläche verwenden, finden Sie im [Tutorial zum Schema-Editor](./tutorials/create-schema-ui.md) weitere Informationen.

### Wie lassen sich Feldgruppen und Datentypen am besten verwenden?

[Feldgruppen](./schema/composition.md#field-group) sind Komponenten, die ein oder mehrere Felder in einem Schema definieren. Feldgruppen erzwingen, wie ihre Felder in der Hierarchie des Schemas angezeigt werden, und weisen daher in jedem Schema, in dem sie enthalten sind, dieselbe Struktur auf. Feldgruppen sind nur mit bestimmten Klassen kompatibel, angegeben durch ihr `meta:intendedToExtend`-Attribut.

[Datentypen](./schema/composition.md#data-type) können ebenfalls ein oder mehrere Felder für ein Schema bereitstellen. Im Gegensatz zu Feldgruppen sind Datentypen jedoch nicht auf eine bestimmte Klasse beschränkt. Dadurch stellen Datentypen eine flexiblere Möglichkeit dar, um allgemeine Datenstrukturen zu beschreiben, die über mehrere Schemas mit potenziell unterschiedlichen Klassen hinweg wiederverwendet werden können.

### Was ist die eindeutige ID für ein Schema?

Alle [!DNL Schema Registry]-Ressourcen (Schemas, Feldgruppen, Datentypen, Klassen) verfügen über einen URI, der zu Referenz- und Suchzwecken als eindeutige ID dient. Wenn Sie ein Schema in der API anzeigen, finden Sie es in den `$id`- und `meta:altId`-Attributen der obersten Ebene.

Weiterführende Informationen finden Sie im Abschnitt [Ressourcenkennung](api/getting-started.md#resource-identification) des [!DNL Schema Registry]-API-Handbuchs.

### Wann verhindert ein Schema umfassende Änderungen?

Umfassende Änderungen können an einem Schema vorgenommen werden, solange es noch nie bei der Erstellung eines Datensatzes verwendet oder für die Verwendung im [[!DNL Real-Time Customer Profile]](../profile/home.md) aktiviert wurde. Sobald ein Schema bei der Erstellung eines Datensatzes verwendet oder für die Verwendung mit dem [!DNL Real-Time Customer Profile] aktiviert wurde, werden die Regeln der [Schemaentwicklung](schema/composition.md#evolution) vom System streng durchgesetzt.

### Wie groß ist ein Feld vom Typ „long“ maximal?

Bei einem Feld vom Typ „long“ handelt es sich um eine Ganzzahl mit einer maximalen Größe von 53(+1) Bit, wodurch ein potenzieller Bereich zwischen -9007199254740992 und 9007199254740992 gegeben ist. Dies liegt an einer Beschränkung der Darstellung langer Ganzzahlen durch JavaScript-Implementierungen von JSON.

Weiterführende Informationen zu Feldtypen finden Sie im Dokument zu [Begrenzungen für XDM-Feldtypen](./schema/field-constraints.md).

### Wie kann ich Identitäten für mein Schema definieren?

In [!DNL Experience Platform] werden Identitäten verwendet, um ein Subjekt (normalerweise eine einzelne Person) unabhängig von den Datenquellen, die interpretiert werden, zu identifizieren. Sie werden in Schemas definiert, indem Schlüsselfelder als „Identität“ markiert werden. Häufig verwendete Identitätsfelder sind E-Mail-Adresse, Telefonnummer, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de), CRM-ID und andere eindeutige ID-Felder.

Felder können entweder über die API oder die Benutzeroberfläche als Identitäten markiert werden.

#### Definieren von Identitäten in der API

In der API werden Identitäten durch Erstellen von Identitätsdeskriptoren erstellt. Identitätsdeskriptoren signalisieren, dass eine bestimmte Eigenschaft für ein Schema eine eindeutige Kennung ist.

Identitätsdeskriptoren werden durch eine POST-Anfrage an den Endpunkt „/descriptors“ erstellt. Bei erfolgreicher Ausführung erhalten Sie einen HTTP-Status 201 (Erstellt) und ein Antwortobjekt mit den Details des neuen Deskriptors.

Weitere Details zum Erstellen von Identitätsdeskriptoren in der API finden Sie im Abschnitt [Deskriptoren](api/descriptors.md) des [!DNL Schema Registry]-Entwicklerhandbuchs.

#### Definieren von Identitäten in der Benutzeroberfläche

Wenn Ihr Schema im Schema-Editor geöffnet ist, wählen Sie das Feld im Abschnitt **[!UICONTROL Struktur]** des Editors aus, das Sie als Identität markieren möchten. Wählen Sie rechts unter **[!UICONTROL Feldeigenschaften]** die Option **[!UICONTROL Identität]** aus.

Weitere Details zum Verwalten von Identitäten in der Benutzeroberfläche finden Sie im Abschnitt zum [Definieren von Identitätsfeldern](./tutorials/create-schema-ui.md#identity-field) im Tutorial für den Schema-Editor.

### Benötigt mein Schema eine primäre Identität?

Primäre Identitäten sind optional, da Schemas entweder keine oder eine davon aufweisen können. Ein Schema muss jedoch über eine primäre Identität verfügen, damit das Schema zur Verwendung im [!DNL Real-Time Customer Profile] aktiviert werden kann. Weiterführende Informationen finden Sie im Abschnitt [Identität](./tutorials/create-schema-ui.md#identity-field) des Tutorials für den Schema-Editor.

### Wie aktiviere ich ein Schema zur Verwendung im [!DNL Real-Time Customer Profile]?

Schemas werden zur Verwendung im [[!DNL Real-Time Customer Profile]](../profile/home.md) aktiviert, indem das Tag „union“ (Vereinigung) innerhalb des `meta:immutableTags`-Attributs des Schemas hinzugefügt wird. Eine Aktivierung eines Schemas zur Verwendung mit dem [!DNL Profile] kann über die API oder die Benutzeroberfläche erfolgen.

#### Aktivieren eines vorhandenen Schemas für das [!DNL Profile] über die API

Stellen Sie eine PATCH-Anfrage, um das Schema zu aktualisieren und das `meta:immutableTags`-Attribut als Array mit dem Wert „union“ hinzuzufügen. Wenn die Aktualisierung erfolgreich ist, zeigt die Antwort das aktualisierte Schema an, das jetzt das Tag „union“ enthält.

Weiterführende Informationen zur Verwendung der API zum Aktivieren eines Schemas für das [!DNL Real-Time Customer Profile] finden Sie im Dokument zu [Vereinigungen](./api/unions.md) im [!DNL Schema Registry] Entwicklerhandbuch.

#### Aktivieren eines vorhandenen Schemas für das [!DNL Profile] über die Benutzeroberfläche

Wählen Sie in [!DNL Experience Platform] im linken Navigationsbereich die Option **[!UICONTROL Schemas]** und dann den Namen des Schemas aus der Liste der Schemas aus, das Sie aktivieren möchten. Aktivieren Sie anschließend rechts im Editor unter **[!UICONTROL Schemaeigenschaften]** die Option **[!UICONTROL Profil]**.


Weiterführende Informationen finden Sie im Abschnitt zur [Verwendung im Echtzeit-Kundenprofil](./tutorials/create-schema-ui.md#profile) im Tutorial [!UICONTROL Schema-Editor].

### Kann ich ein Vereinigungsschema direkt bearbeiten?

Vereinigungsschemas sind schreibgeschützt und werden automatisch vom System generiert. Sie können nicht direkt bearbeitet werden. Vereinigungsschemas werden für eine bestimmte Klasse erstellt, wenn einem Schema, das diese Klasse implementiert, das Tag „union“ (Vereinigung) hinzugefügt wird.

Weiterführende Informationen zu Vereinigungen in XDM finden Sie im Abschnitt [Vereinigungen](./api/unions.md) des [!DNL Schema Registry]-API-Handbuchs.

### Wie sollte ich meine Datendatei formatieren, um Daten in mein Schema aufzunehmen?

[!DNL Experience Platform] akzeptiert Datendateien im [!DNL Parquet]- oder JSON-Format. Die Inhalte dieser Dateien müssen mit dem Schema übereinstimmen, auf das der Datensatz verweist. Details zu Best Practices für die Datendateiaufnahme finden Sie in der [Übersicht zur Batch-Aufnahme](../ingestion/home.md).

## Fehler und Fehlerbehebung

Im Folgenden finden Sie eine Liste von Fehlermeldungen, auf die Sie bei der Arbeit mit der [!DNL Schema Registry]-API stoßen können.

### Ressource nicht gefunden

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1010-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found.",
        "sub-errors": []
    },
    "detail": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found."
}
```

Dieser Fehler wird angezeigt, wenn das System eine bestimmte Ressource nicht finden konnte. Die Ressource wurde möglicherweise gelöscht oder der Pfad im API-Aufruf ist ungültig. Vergewissern Sie sich, dass Sie einen gültigen Pfad für Ihren API-Aufruf eingegeben haben, bevor Sie es erneut versuchen. Sie sollten überprüfen, ob Sie die richtige ID für die Ressource eingegeben haben und ob der Pfad den richtigen Namespace gemäß dem entsprechenden Container (global oder Mandant) erhalten hat.

>[!NOTE]
>
>Je nach Ressourcentyp, der abgerufen wird, kann dieser Fehler einen der folgenden `type`-URIs verwenden:
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


Weiterführende Informationen zum Erstellen von Suchpfaden in der API finden Sie in den Abschnitten [Container](./api/getting-started.md#container) und [Ressourcenkennung](api/getting-started.md#resource-identification) des [!DNL Schema Registry]-Entwicklerhandbuchs.

### Titel nicht eindeutig

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1521-400",
    "title": "Title not unique",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title",
        "sub-errors": []
    },
    "detail": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title"
}
```

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, eine Ressource mit einem Titel zu erstellen, der bereits von einer anderen Ressource verwendet wird. Titel müssen unten allen Ressourcentypen eindeutig sein. Wenn Sie beispielsweise versuchen, eine Feldgruppe mit einem Titel zu erstellen, der bereits von einem Schema verwendet wird, erhalten Sie diesen Fehler.

### Namespace-Validierungsfehler

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1021-400",
    "title": "Namespace validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}.",
        "sub-errors": []
    },
    "detail": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}."
}
```

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, eine Ressource mit Feldern zu erstellen, die über keinen ordnungsgemäßen Namespace verfügen, oder einer vorhandenen Ressource Felder mit falschem Namespace hinzuzufügen.

Für Ressourcen, die von Ihrer Organisation definiert werden, müssen ihre Felder unter Ihrer Mandanten-ID mit einem Namespace versehen werden, um Konflikte mit anderen Branchen- und Anbieterressourcen zu vermeiden. Beim Erstellen eines Schemas mit Standardfeldgruppen müssen alle benutzerdefinierten Felder, die Sie innerhalb der Struktur dieser Feldgruppen hinzufügen, auch unter Ihrer Mandanten-ID mit einem Namespace versehen werden.

>[!NOTE]
>
>Abhängig von der spezifischen Art des Namespace-Fehlers kann dieser Fehler einen der folgenden `type`-URIs mit verschiedenen Meldungsdetails verwenden:
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`


Ausführliche Beispiele für ordnungsgemäße Datenstrukturen für XDM-Ressourcen finden Sie im Handbuch zur API für die Schemaregistrierung:

* [Erstellen einer benutzerdefinierter Klasse](./api/classes.md#create)
* [Erstellen einer benutzerdefinierten Feldgruppe](./api/field-groups.md#create)
* [Erstellen eines benutzerdefinierten Datentyps](./api/data-types.md#create)

### Accept-Kopfzeile ungültig

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1006-400",
    "title": "Accept header invalid",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json",
        "sub-errors": []
    },
    "detail": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json"
}
```

GET-Anfragen in der [!DNL Schema Registry]-API erfordern eine `Accept`-Kopfzeile, damit das System die Formatierung der Antwort festlegen kann. Dieser Fehler tritt auf, wenn die erforderliche `Accept`-Kopfzeile ungültig ist oder fehlt.

Je nach verwendetem Endpunkt gibt die `detailed-message`-Eigenschaft an, wie eine gültige `Accept`-Kopfzeile für eine erfolgreiche Antwort aussehen sollte. Vergewissern Sie sich, dass Sie die `Accept`-Kopfzeile, die mit der zu erstellenden API-Anfrage kompatibel ist, korrekt eingegeben haben, bevor Sie es erneut versuchen.

>[!NOTE]
>
>Je nach verwendetem Endpunkt kann dieser Fehler einen der folgenden `type`-URIs verwenden:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


Eine Liste kompatibler Accept-Kopfzeilen für verschiedene API-Anfragen finden Sie in den entsprechenden Abschnitten im [Entwicklerhandbuch zur Schemaregistrierung](./api/overview.md).

### [!DNL Real-Time Customer Profile]-Fehler

Die folgenden Fehlermeldungen sind mit Vorgängen verknüpft, die mit der Aktivierung von Schemas für das [!DNL Real-Time Customer Profile] im Zusammenhang stehen. Weiterführende Informationen finden Sie im Abschnitt [Vereinigungen](./api/unions.md) des [!DNL Schema Registry]-API-Handbuchs.

#### Referenz-Identitätsdeskriptor erforderlich

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1526-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union.",
        "sub-errors": []
    },
    "detail": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union."
}
```

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, ein Schema für das [!DNL Profile] zu aktivieren und eine seiner Eigenschaften einen Beziehungsdeskriptor ohne Referenz-Identitätsdeskriptor enthält. Fügen Sie dem betreffenden Schemafeld einen Referenz-Identitätsdeskriptor hinzu, um diesen Fehler zu beheben.

#### Namespaces des Referenz-Identitätsdeskriptorfelds und Zielschemas müssen übereinstimmen

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1527-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field.",
        "sub-errors": []
    },
    "detail": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field."
}
```

>[!NOTE]
>
>Bei diesem Fehler bezieht sich das „Zielschema“ auf das Referenzschema in der Beziehung.

Um Schemas, die Beziehungsdeskriptoren enthalten, für die Verwendung im [!DNL Profile] zu aktivieren, müssen der Namespace des Quellfelds und der primäre Namespace des Referenzfelds identisch sein. Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, ein Schema zu aktivieren, das einen nicht übereinstimmenden Namespace für den zugehörigen Referenz-Identitätsdeskriptor enthält.

Stellen Sie sicher, dass der `xdm:namespace`-Wert des Identitätsfelds des Referenzschemas mit dem der `xdm:identityNamespace`-Eigenschaft im Referenz-Identitätsdeskriptor des Quellfelds übereinstimmt, um dieses Problem zu beheben.

Eine Liste der standardmäßigen Identity-Namespace-Codes finden Sie im Abschnitt zu [Standard-Namespaces](../identity-service/namespaces.md) in der Übersicht zu Identity-Namespaces.

#### Das Schema muss eine identityMap oder eine primäre Identität enthalten

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1528-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor.",
        "sub-errors": []
    },
    "detail": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor."
}
```

Bevor Sie ein Schema für das Profil aktivieren, müssen Sie zunächst für das Schema [einen primären Identitätsdeskriptor erstellen](./api/descriptors.md#create) oder ein Identitätszuordnungsfeld einschließen, das stattdessen als primäre Identität agiert.

#### Zusammenführen inkompatibler Datentypen nicht möglich

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1413-400",
    "title": "Merge Schema Error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object",
        "sub-errors": []
    },
    "detail": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object"
}
```

Alle profilaktivierten Schemas, die zur gleichen Klasse gehören, müssen zusammengeführt werden können, um das Vereinigungsschema für diese Klasse zu erstellen. Dieser Fehler wird angezeigt, wenn Sie versuchen, ein Feld zu einem Schema hinzuzufügen, dessen Pfad ebenfalls von einem anderen profilaktivierten Schema genutzt wird und dessen Datentyp sich vom ursprünglichen unterscheidet. Da die Schemas profilaktiviert sind und denselben Feldpfad enthalten, versucht das Profil, diese beiden Felder beim Erstellen des Vereinigungsschemas zusammenzuführen. Da verschiedene Datentypen nicht zusammengeführt werden können, wird dies als Zusammenführungskonflikt betrachtet und der Vorgang ist unzulässig.

Um das Problem zu beheben, wählen Sie einen anderen Namen für das Feld aus oder verschachteln Sie es unter einem Objekt mit eindeutigem Namespace, um Zusammenführungskonflikte mit anderen profilaktivierten Schemas unter derselben Klasse mit ähnlichen Feldern zu vermeiden.
