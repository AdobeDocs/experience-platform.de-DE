---
keywords: Experience Platform; beliebte Themen; XDM; XDM-System; XDM-individuelles Profil; XDM ExperienceEvent; XDM Experience Event; experienceEvent; experience eventExperience-Ereignis; XDM Experience Event; XDM ExperienceEvent; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Datenmodell; Schema; Fehlerbehebung; FAQ; FAQ; Vereinigungsschema; UNION PROFILE; Vereinigungsprofil; http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei XDM-Systemen
description: Hier finden Sie Antworten auf häufig gestellte Fragen zum Experience-Datenmodell (XDM), einschließlich Anweisungen zur Behebung häufiger API-Fehler.
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '2060'
ht-degree: 1%

---

# Handbuch zur Fehlerbehebung bei XDM-Systemen

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu [!DNL Experience Data Model] (XDM) und XDM-System in Adobe Experience Platform, einschließlich einer Anleitung zur Fehlerbehebung bei häufigen Fehlern. Fragen und Fehlerbehebungen für andere Platform-Dienste finden Sie im [Handbuch zur Fehlerbehebung in Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** ist eine Open-Source-Spezifikation, die standardisierte Schemas für das Customer Experience Management definiert. Die Methode, nach der [!DNL Experience Platform] erstellt wird, **XDM-System**, operationalisiert [!DNL Experience Data Model] Schemata zur Verwendung durch [!DNL Platform] Dienste. Die **[!DNL Schema Registry]** bietet eine Benutzeroberfläche und eine RESTful-API für den Zugriff auf **[!DNL Schema Library]** Innerhalb [!DNL Experience Platform]. Weitere Informationen finden Sie in der [XDM-Dokumentation](home.md).

## FAQs

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zum XDM-System und zur Verwendung der [!DNL Schema Registry] API.

### Wie füge ich einem Schema Felder hinzu?

Mithilfe einer Schemafeldgruppe können Sie einem Schema Felder hinzufügen. Jede Feldergruppe ist mit einer oder mehreren Klassen kompatibel, sodass die Feldergruppe in jedem Schema verwendet werden kann, das eine dieser kompatiblen Klassen implementiert. Adobe Experience Platform stellt mehrere Industriefeldergruppen mit eigenen vordefinierten Feldern bereit. Sie können jedoch eigene Felder zu einem Schema hinzufügen, indem Sie benutzerdefinierte Feldergruppen mithilfe der API oder der Benutzeroberfläche erstellen.

Weitere Informationen zum Erstellen von Feldergruppen finden Sie unter [!DNL Schema Registry] API, siehe [Endpunktleitfaden für Feldergruppen](api/field-groups.md#create). Wenn Sie die Benutzeroberfläche verwenden, lesen Sie den Abschnitt [Tutorial zum Schema Editor](./tutorials/create-schema-ui.md).

### Was sind die besten Verwendungszwecke für Feldergruppen und Datentypen?

[Feldergruppen](./schema/composition.md#field-group) sind Komponenten, die ein oder mehrere Felder in einem Schema definieren. Feldergruppen erzwingen, wie ihre Felder in der Hierarchie des Schemas angezeigt werden, und weisen daher in jedem Schema, in dem sie enthalten sind, dieselbe Struktur auf. Feldergruppen sind nur mit bestimmten Klassen kompatibel, die durch ihre `meta:intendedToExtend` -Attribut.

[Datentypen](./schema/composition.md#data-type) kann auch ein oder mehrere Felder für ein Schema bereitstellen. Im Gegensatz zu Feldergruppen sind Datentypen jedoch nicht auf eine bestimmte Klasse beschränkt. Dadurch sind Datentypen flexibler, um allgemeine Datenstrukturen zu beschreiben, die über mehrere Schemas mit potenziell unterschiedlichen Klassen hinweg wiederverwendet werden können.

### Was ist die eindeutige ID für ein Schema?

Alle [!DNL Schema Registry] -Ressourcen (Schemas, Feldergruppen, Datentypen, Klassen) verfügen über einen URI, der zu Referenz- und Suchzwecken als eindeutige ID dient. Wenn Sie ein Schema in der API anzeigen, finden Sie es auf der obersten Ebene `$id` und `meta:altId` -Attribute.

Weitere Informationen finden Sie unter [Ressourcenkennung](api/getting-started.md#resource-identification) im Abschnitt [!DNL Schema Registry] API-Handbuch.

### Wann verhindert ein Schema das Umbrechen von Änderungen?

Umfassende Änderungen können an einem Schema vorgenommen werden, solange es noch nie bei der Erstellung eines Datensatzes verwendet oder für die Verwendung in [[!DNL Real-Time Customer Profile]](../profile/home.md). Sobald ein Schema bei der Erstellung eines Datensatzes verwendet oder für die Verwendung mit [!DNL Real-Time Customer Profile], die Regeln der [Schemaentwicklung](schema/composition.md#evolution) streng durchgesetzt werden.

### Wie groß ist ein langer Feldtyp maximal?

Ein langer Feldtyp ist eine Ganzzahl mit einer maximalen Größe von 53(+1) Bit, wodurch ein potenzieller Bereich zwischen -9007199254740992 und 9007199254740992 liegt. Dies liegt an einer Beschränkung der Darstellung langer Ganzzahlen durch JavaScript-Implementierungen von JSON.

Weitere Informationen zu Feldtypen finden Sie im Dokument unter [XDM-Feldtypbegrenzungen](./schema/field-constraints.md).

### Wie kann ich Identitäten für mein Schema definieren?

In [!DNL Experience Platform], werden Identitäten verwendet, um ein Subjekt (normalerweise eine einzelne Person) unabhängig von den Datenquellen, die interpretiert werden, zu identifizieren. Sie werden in Schemata definiert, indem Schlüsselfelder als &quot;Identität&quot;markiert werden. Häufig verwendete Identitätsfelder sind E-Mail-Adresse, Telefonnummer, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de), CRM-ID und andere eindeutige ID-Felder.

Felder können entweder über die API oder die Benutzeroberfläche als Identitäten markiert werden.

#### Identitäten in der API definieren

In der API werden Identitäten durch Erstellen von Identitätsdeskriptoren erstellt. Identitätsdeskriptoren signalisieren, dass eine bestimmte Eigenschaft für ein Schema eine eindeutige Kennung ist.

Identitätsdeskriptoren werden durch eine POST-Anfrage an den /descriptors-Endpunkt erstellt. Bei erfolgreicher Ausführung erhalten Sie einen HTTP-Status 201 (Erstellt) und ein Antwortobjekt mit den Details des neuen Deskriptors.

Weitere Informationen zum Erstellen von Identitätsdeskriptoren in der API finden Sie im Dokument unter [deskriptoren](api/descriptors.md) im Abschnitt [!DNL Schema Registry] Entwicklerhandbuch.

#### Identitäten in der Benutzeroberfläche definieren

Wenn Ihr Schema im Schema-Editor geöffnet ist, wählen Sie das Feld im **[!UICONTROL Struktur]** -Abschnitt des Editors, den Sie als Identität markieren möchten. under **[!UICONTROL Feldeigenschaften]** Wählen Sie rechts die **[!UICONTROL Identität]** aktivieren.

Weitere Informationen zum Verwalten von Identitäten in der Benutzeroberfläche finden Sie im Abschnitt unter [Identitätsfelder definieren](./tutorials/create-schema-ui.md#identity-field) im Tutorial zum Schema-Editor.

### Benötigt mein Schema eine primäre Identität?

Primäre Identitäten sind optional, da Schemas entweder null oder eine davon haben können. Ein Schema muss jedoch über eine primäre Identität verfügen, damit das Schema zur Verwendung in [!DNL Real-Time Customer Profile]. Siehe [identity](./tutorials/create-schema-ui.md#identity-field) Abschnitt des Tutorials zum Schema-Editor für weitere Informationen.

### Wie aktiviere ich ein Schema zur Verwendung in [!DNL Real-Time Customer Profile]?

Schemas sind zur Verwendung in [[!DNL Real-Time Customer Profile]](../profile/home.md) durch Hinzufügen eines &quot;union&quot;-Tags innerhalb der `meta:immutableTags` -Attribut des Schemas. Aktivieren eines Schemas zur Verwendung mit [!DNL Profile] kann über die API oder die Benutzeroberfläche erfolgen.

#### Aktivieren eines vorhandenen Schemas für [!DNL Profile] Verwendung der API

Stellen Sie eine PATCH-Anfrage, um das Schema zu aktualisieren und die `meta:immutableTags` -Attribut als Array mit dem Wert &quot;union&quot;. Wenn die Aktualisierung erfolgreich ist, zeigt die Antwort das aktualisierte Schema an, das jetzt das Vereinigungs-Tag enthält.

Weitere Informationen zur Verwendung der API zum Aktivieren eines Schemas zur Verwendung in [!DNL Real-Time Customer Profile], siehe [Vereinigungen](./api/unions.md) des [!DNL Schema Registry] Entwicklerhandbuch.

#### Aktivieren eines vorhandenen Schemas für [!DNL Profile] über die Benutzeroberfläche

In [!DNL Experience Platform]auswählen **[!UICONTROL Schemas]** im linken Navigationsbereich und wählen Sie den Namen des Schemas aus, das Sie aktivieren möchten. Dann auf der rechten Seite des Editors unter **[!UICONTROL Schemaeigenschaften]** auswählen **[!UICONTROL Profil]** , um es zu aktivieren.


Weitere Informationen finden Sie im Abschnitt zu [Verwendung im Echtzeit-Kundenprofil](./tutorials/create-schema-ui.md#profile) im [!UICONTROL Schema Editor] Tutorial.

### Kann ich ein Vereinigungsschema direkt bearbeiten?

Vereinigungsschemas sind schreibgeschützt und werden automatisch vom System generiert. Sie können nicht direkt bearbeitet werden. Vereinigungsschemas werden für eine bestimmte Klasse erstellt, wenn einem Schema, das diese Klasse implementiert, ein &quot;union&quot;-Tag hinzugefügt wird.

Weitere Informationen zu Vereinigungen in XDM finden Sie unter [Vereinigungen](./api/unions.md) im Abschnitt [!DNL Schema Registry] API-Handbuch.

### Wie sollte ich meine Datendatei so formatieren, dass Daten in mein Schema aufgenommen werden?

[!DNL Experience Platform] akzeptiert Datendateien in [!DNL Parquet] oder im JSON-Format. Der Inhalt dieser Dateien muss mit dem Schema übereinstimmen, auf das der Datensatz verweist. Weitere Informationen zu Best Practices für die Datendateiaufnahme finden Sie unter [Batch-Erfassung - Übersicht](../ingestion/home.md).

## Fehler und Fehlerbehebung

Im Folgenden finden Sie eine Liste von Fehlermeldungen, auf die Sie bei der Arbeit mit der [!DNL Schema Registry] API.

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

Dieser Fehler wird angezeigt, wenn das System eine bestimmte Ressource nicht finden konnte. Die Ressource wurde möglicherweise gelöscht oder der Pfad im API-Aufruf ist ungültig. Vergewissern Sie sich, dass Sie einen gültigen Pfad für Ihren API-Aufruf eingegeben haben, bevor Sie es erneut versuchen. Sie können überprüfen, ob Sie die richtige ID für die Ressource eingegeben haben und ob der Pfad mit dem entsprechenden Container (global oder Mandant) richtig benannt wurde.

>[!NOTE]
>
>Je nach Ressourcentyp, der abgerufen wird, kann dieser Fehler Folgendes verwenden: `type` URIs:
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


Weitere Informationen zum Erstellen von Suchpfaden in der API finden Sie unter [container](./api/getting-started.md#container) und [Ressourcenkennung](api/getting-started.md#resource-identification) in [!DNL Schema Registry] Entwicklerhandbuch.

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

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, eine Ressource mit einem Titel zu erstellen, der bereits von einer anderen Ressource verwendet wird. Titel müssen für alle Ressourcentypen eindeutig sein. Wenn Sie beispielsweise versuchen, eine Feldergruppe mit einem Titel zu erstellen, der bereits von einem Schema verwendet wird, erhalten Sie diesen Fehler.

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

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, eine Ressource mit nicht ordnungsgemäßen Namespaced-Feldern zu erstellen oder einer vorhandenen Ressource falsch benannte Felder hinzuzufügen.

Ressourcen, die von Ihrer IMS-Organisation definiert werden, müssen ihre Felder unter Ihrer Mandanten-ID mit Namespace versehen, um Konflikte mit anderen Ressourcen der Branche und des Anbieters zu vermeiden. Beim Erstellen eines Schemas mit Standardfeldgruppen müssen alle benutzerdefinierten Felder, die Sie innerhalb der Struktur dieser Feldgruppen hinzufügen, auch unter Ihrer Mandanten-ID als Namespace angegeben werden.

>[!NOTE]
>
>Abhängig von der spezifischen Art des Namespace-Fehlers kann dieser Fehler Folgendes verwenden: `type` URIs zusammen mit verschiedenen Nachrichtendetails:
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`


Ausführliche Beispiele für ordnungsgemäße Datenstrukturen für XDM-Ressourcen finden Sie im Handbuch zur Schema Registry-API:

* [Benutzerdefinierte Klasse erstellen](./api/classes.md#create)
* [Benutzerdefinierte Feldergruppe erstellen](./api/field-groups.md#create)
* [Benutzerdefinierten Datentyp erstellen](./api/data-types.md#create)

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

GET-Anforderungen in [!DNL Schema Registry] API erfordert `Accept` -Kopfzeile, damit das System bestimmen kann, wie die Antwort formatiert werden soll. Dieser Fehler tritt auf, wenn erforderlich `Accept` -Kopfzeile ist ungültig oder fehlt.

Je nach verwendetem Endpunkt wird die `detailed-message` -Eigenschaft gibt an, was gültig ist `Accept` -Kopfzeile sollte wie für eine erfolgreiche Antwort aussehen. Vergewissern Sie sich, dass Sie die `Accept` -Kopfzeile, die mit der API-Anfrage kompatibel ist, die Sie erstellen möchten, bevor Sie es erneut versuchen.

>[!NOTE]
>
>Je nach verwendetem Endpunkt kann dieser Fehler Folgendes verwenden: `type` URIs:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


Eine Liste kompatibler Accept-Kopfzeilen für verschiedene API-Anfragen finden Sie in den entsprechenden Abschnitten im [Entwicklerhandbuch zur Schema Registry](./api/overview.md).

### [!DNL Real-Time Customer Profile] errors

Die folgenden Fehlermeldungen sind mit Vorgängen verknüpft, die an der Aktivierung von Schemas für [!DNL Real-Time Customer Profile]. Siehe [Vereinigungen](./api/unions.md) im Abschnitt [!DNL Schema Registry] API-Handbuch für weitere Informationen.

#### Es muss einen Referenz-Identitätsdeskriptor geben

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

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, ein Schema für [!DNL Profile] und eine seiner Eigenschaften einen Beziehungsdeskriptor ohne Referenzidentitätsdeskriptor enthält. Fügen Sie dem betreffenden Schemafeld einen Referenzidentitätsdeskriptor hinzu, um diesen Fehler zu beheben.

#### Die Namespaces des Referenzidentitätsdeskriptorfelds und des Zielschemas müssen übereinstimmen

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

So aktivieren Sie Schemas, die Beziehungsdeskriptoren enthalten, für die Verwendung in [!DNL Profile], müssen der Namespace des Quellfelds und der primäre Namespace des Zielfelds identisch sein. Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, ein Schema zu aktivieren, das einen nicht übereinstimmenden Namespace für den Referenzidentitätsdeskriptor enthält. Stellen Sie sicher, dass `xdm:namespace` -Wert des Identitätsfelds des Zielschemas mit dem des `xdm:identityNamespace` -Eigenschaft im Referenz-Identitätsdeskriptor des Quellfelds verwenden, um dieses Problem zu beheben.

Eine Liste der standardmäßigen Identitäts-Namespace-Codes finden Sie im Abschnitt unter [Standard-Namespaces](../identity-service/namespaces.md) in der Übersicht zum Identitäts-Namespace.

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

Bevor Sie ein Schema für Profile aktivieren, müssen Sie zunächst [Erstellen eines primären Identitätsdeskriptors](./api/descriptors.md#create) für das Schema oder ein Identitätszuordnungsfeld einschließen, um stattdessen auf die primäre Identität zu reagieren.

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

Alle für Profile aktivierten Schemas, die zur gleichen Klasse gehören, müssen zusammengeführt werden können, um das Vereinigungsschema für diese Klasse zu erstellen. Dieser Fehler wird angezeigt, wenn Sie versuchen, ein Feld zu einem Schema hinzuzufügen, dessen Pfad von einem anderen Profil-aktivierten Schema gemeinsam genutzt wird und dessen Datentyp sich vom ursprünglichen unterscheidet. Da die Schemas sowohl Profil-fähig sind als auch denselben Feldpfad enthalten, versucht Profile, diese beiden Felder beim Erstellen des Vereinigungsschemas zu einem zusammenzuführen. Da verschiedene Datentypen nicht zusammengeführt werden können, wird dies als Zusammenführungskonflikt betrachtet und ist nicht zulässig.

Um das Problem zu beheben, wählen Sie einen anderen Namen für das Feld aus oder verschachteln Sie es unter einem eindeutigen Namespace-Objekt, um Zusammenführungskonflikte mit anderen Profil-aktivierten Schemas unter derselben Klasse mit ähnlichen Feldern zu vermeiden.
