---
keywords: Experience Platform;home;popular topics;;XDM;XDM system;XDM individual profile;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience eventExperience event;XDM Experience Event;XDM ExperienceEvent;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema;troubleshooting;FAQ;faq;
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei Experience Data Model (XDM)
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zum Experience Data Model (XDM) System sowie eine Anleitung zur Fehlerbehebung für häufige Fehler.
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '1862'
ht-degree: 0%

---


# [!DNL Experience Data Model] (XDM) Handbuch zur Systemfehlerbehebung

This document provides answers to frequently asked questions about [!DNL Experience Data Model] (XDM) System, as well as a troubleshooting guide for common errors. For questions and troubleshooting related to other services in Adobe Experience Platform, please refer to the [Experience Platform troubleshooting guide](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** ist eine Open-Source-Spezifikation, die standardisierte Schema für das Kundenerlebnis-Management definiert. Die Methode, auf der [!DNL Experience Platform] aufgebaut wird, **XDM System**, operalisiert [!DNL Experience Data Model] Schema für die Verwendung durch [!DNL Platform] Dienste. Die **[!DNL Schema Registry]** bietet eine Benutzeroberfläche und eine RESTful-API für den Zugriff auf die **[!DNL Schema Library]** Umgebung [!DNL Experience Platform]. See the [XDM documentation](home.md) for more information.

## FAQs

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zum XDM-System und zur Verwendung der [!DNL Schema Registry] API.

### Wie füge ich einem Schema Felder hinzu?

Sie können einem Schema Felder mit einem Mixin hinzufügen. Jedes Mixin ist mit einer oder mehreren Klassen kompatibel, sodass das Mixin in jedem Schema verwendet werden kann, das eine dieser kompatiblen Klassen implementiert. Adobe Experience Platform stellt verschiedene Branchenmixins mit eigenen vordefinierten Feldern zur Verfügung. Sie können jedoch eigene Felder zu einem Schema hinzufügen, indem Sie neue Mixins mit der API oder der Benutzeroberfläche erstellen.

Weitere Informationen zum Erstellen neuer Mixins in der API finden Sie im API-Entwicklerhandbuch im [Dokument zum Erstellen eines Mixins](api/create-mixin.md) [!DNL Schema Registry] . Wenn Sie die Benutzeroberfläche verwenden, finden Sie weitere Informationen im Tutorial zum [Schema-Editor](./tutorials/create-schema-ui.md).

### Welches sind die besten Verwendungen für Mixins und Datentypen?

[Mixins](./schema/composition.md#mixin) sind Komponenten, die ein oder mehrere Felder in einem Schema definieren. Mixins erzwingen, wie ihre Felder in der Hierarchie des Schemas angezeigt werden, und weisen daher in jedem Schema dieselbe Struktur auf, in dem sie enthalten sind. Mixins sind nur mit bestimmten Klassen kompatibel, die durch ihr `meta:intendedToExtend` Attribut gekennzeichnet sind.

[Datentypen](./schema/composition.md#data-type) können auch ein oder mehrere Felder für ein Schema bereitstellen. Im Gegensatz zu Mixins sind Datentypen jedoch nicht auf eine bestimmte Klasse beschränkt. Dadurch werden Datentypen flexibler, um häufig verwendete Datenstrukturen zu beschreiben, die über mehrere Schema mit potenziell unterschiedlichen Klassen hinweg wiederverwendet werden können.

### Was ist die eindeutige ID für ein Schema?

Alle [!DNL Schema Registry] Ressourcen (Schemas, Mixins, Datentypen, Klassen) verfügen über einen URI, der als eindeutige ID für Referenz- und Suchzwecke dient. Wenn Sie ein Schema in der API anzeigen, finden Sie es in den Attributen der obersten Ebene `$id` und `meta:altId` .

Weitere Informationen finden Sie im Abschnitt zur [Schema-Identifizierung](api/getting-started.md#schema-identification) im [!DNL Schema Registry] API-Entwicklerhandbuch.

### Wann verhindert ein Schema-Beginn Umbrüche?

Umbrüchige Änderungen können an einem Schema vorgenommen werden, solange es noch nie zur Erstellung eines Datensatzes verwendet oder für die Verwendung im [[!DNL Echtzeit-Kundendienstprogramm]](../profile/home.md)aktiviert wurde. Sobald ein Schema bei der Erstellung eines Datensatzes verwendet oder für die Verwendung mit aktiviert wurde, [!DNL Real-time Customer Profile]werden die Regeln der [Schema-Evolution](schema/composition.md#evolution) vom System strikt durchgesetzt.

### Wie hoch ist die maximale Größe eines langen Feldtyps?

Ein langer Feldtyp ist eine Ganzzahl mit einer maximalen Größe von 53 (+1) Bit, wodurch ein potenzieller Bereich zwischen -9007199254740992 und 9007199254740992 liegt. Dies liegt daran, dass JavaScript-Implementierungen von JSON keine langen Ganzzahlen darstellen.

Weitere Informationen zu Feldtypen finden Sie im Abschnitt [Definieren von XDM-Feldtypen](api/appendix.md#field-types) [!DNL Schema Registry] im API-Entwicklerhandbuch.

### Wie definiere ich Identitäten für mein Schema?

In [!DNL Experience Platform]diesem Fall werden Identitäten unabhängig von den zu interpretierenden Datenquellen zur Identifizierung eines Subjekts (in der Regel einer einzelnen Person) verwendet. Sie werden in Schemas definiert, indem Sie Schlüsselfelder als &quot;Identität&quot;markieren. Häufig verwendete Identitätsfelder sind E-Mail-Adresse, Telefonnummer, [[!DNL-Experience Cloud-ID (ECID)]](https://docs.adobe.com/content/help/de-DE/id-service/using/home.html), CRM-ID und andere eindeutige ID-Felder.

Felder können entweder über die API oder die Benutzeroberfläche als Identitäten gekennzeichnet werden.

#### Definieren von Identitäten in der API

In der API werden Identitäten durch Erstellen von Identitätsdeskriptoren festgelegt. Identitätsdeskriptoren signalisieren, dass eine bestimmte Eigenschaft für ein Schema ein eindeutiger Bezeichner ist.

Identitätsdeskriptoren werden durch eine POST an den /descriptors-Endpunkt erstellt. Bei erfolgreichem Abschluss erhalten Sie einen HTTP-Status 201 (Erstellt) und ein Antwortobjekt mit den Details des neuen Deskriptors.

Weitere Informationen zum Erstellen von Identitätsdeskriptoren in der API finden Sie im Dokument zu [Deskriptoren](api/descriptors.md) im [!DNL Schema Registry] Entwicklerhandbuch.

#### Definieren von Identitäten in der Benutzeroberfläche

Wenn Ihr Schema im Schema-Editor geöffnet ist, klicken Sie auf das Feld im Bereich &quot; **[!UICONTROL Struktur]** &quot;des Editors, das Sie als Identität markieren möchten. Klicken Sie unter **[!UICONTROL Feldeigenschaften]** auf der rechten Seite auf das Kontrollkästchen **[!UICONTROL Identität]** .

Weitere Informationen zum Verwalten von Identitäten in der Benutzeroberfläche finden Sie im Abschnitt zum [Definieren von Identitätsfeldern](./tutorials/create-schema-ui.md#identity-field) im Schema-Editor-Lernprogramm.

### Braucht mein Schema eine primäre Identität?

Primär-IDs sind optional, da Schema 0 oder 1 davon haben können. Ein Schema muss jedoch über eine primäre Identität verfügen, damit das Schema zur Verwendung in aktiviert werden kann [!DNL Real-time Customer Profile]. Weitere Informationen finden Sie im Schema-Editor-Tutorial im [Identitätsbereich](./tutorials/create-schema-ui.md#identity-field) .

### Wie aktiviere ich ein Schema zur Verwendung in [!DNL Real-time Customer Profile]?

Schema sind für die Verwendung im [[!DNL Echtzeit-Kundenkonto]](../profile/home.md) durch das Hinzufügen eines &quot;Vereinigung&quot;-Tags aktiviert, das sich im `meta:immutableTags` Attribut des Schemas befindet. Die Aktivierung eines Schemas zur Verwendung mit [!DNL Profile] kann über die API oder die Benutzeroberfläche erfolgen.

#### Aktivieren eines vorhandenen Schemas zur [!DNL Profile] Verwendung der API

Führen Sie eine PATCH-Anforderung durch, um das Schema zu aktualisieren und das `meta:immutableTags` Attribut als Array mit dem Wert &quot;Vereinigung&quot;hinzuzufügen. Wenn die Aktualisierung erfolgreich ist, zeigt die Antwort das aktualisierte Schema an, das jetzt das Vereinigung-Tag enthält.

Weitere Informationen zur Verwendung der API zum Aktivieren eines Schemas für die Verwendung in [!DNL Real-time Customer Profile]finden Sie im Dokument [Vereinigungen](./api/unions.md) im Entwicklerhandbuch [!DNL Schema Registry] .

#### Aktivieren eines vorhandenen Schemas zur [!DNL Profile] Verwendung der Benutzeroberfläche

Klicken Sie [!DNL Experience Platform]im linken Navigationsbereich auf **[!UICONTROL Schema]** und wählen Sie den Namen des Schemas aus, das Sie in der Liste der Schema aktivieren möchten. Klicken Sie dann auf der rechten Seite des Editors unter **[!UICONTROL Schema Properties]** auf **[!UICONTROL Profil]** , um es einzuschalten.


Weitere Informationen finden Sie im Abschnitt zur [Verwendung im Echtzeit-Profil](./tutorials/create-schema-ui.md#profile) des [!UICONTROL Schema-Editors] .

### Kann ich ein Vereinigung-Schema direkt bearbeiten?

Vereinigung-Schema sind schreibgeschützt und werden automatisch vom System generiert. Sie können nicht direkt bearbeitet werden. Vereinigung-Schema werden für eine bestimmte Klasse erstellt, wenn dem Schema, das diese Klasse implementiert, ein &quot;Vereinigung&quot;-Tag hinzugefügt wird.

Weitere Informationen zu Vereinigungen in XDM finden Sie im Abschnitt zu [Vereinigungen](./api/unions.md) im [!DNL Schema Registry] API-Entwicklerhandbuch.

### Wie formatiere ich meine Datendatei, um Daten in mein Schema zu erfassen?

[!DNL Experience Platform] akzeptiert Datendateien im JSON- [!DNL Parquet] oder JSON-Format. Der Inhalt dieser Dateien muss mit dem Schema übereinstimmen, auf das der Datensatz verweist. Weitere Informationen zu den Best Practices für die Datafile-Erfassung finden Sie in der Übersicht über die [Stapelverarbeitung](../ingestion/home.md).

## Fehler und Fehlerbehebung

Im Folgenden finden Sie eine Liste von Fehlermeldungen, auf die Sie bei der Arbeit mit der [!DNL Schema Registry] API stoßen können.

### Objekt nicht gefunden

```json
{
    "type": "/placeholder/type/uri",
    "status": 404,
    "title": "NotFoundError",
    "detail": "Object https://ns.adobe.com/incorrectTenantId/schemas/ee067e31b08514d21e2b82577813409d 
      with version 1 not found"
}
```

Dieser Fehler wird angezeigt, wenn das System eine bestimmte Ressource nicht finden konnte. Die Ressource wurde möglicherweise gelöscht oder der Pfad im API-Aufruf ist ungültig. Vergewissern Sie sich, dass Sie einen gültigen Pfad für Ihren API-Aufruf eingegeben haben, bevor Sie ihn erneut versuchen. Sie können überprüfen, ob Sie die richtige ID für die Ressource eingegeben haben und ob der Pfad mit dem entsprechenden Container (global oder mieter) richtig benannt wurde.

Weitere Informationen zum Erstellen von Nachschlagetpfaden in der API finden Sie in den Abschnitten zur Identifizierung von [Containern](./api/getting-started.md#container) und [Schemas](api/getting-started.md#schema-identification) im Entwicklerhandbuch [!DNL Schema Registry] .

### Titel muss eindeutig sein

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "Title must be unique. An object 
      https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d 
      already exists with the same title."
}
```

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, eine Ressource mit einem Titel zu erstellen, der bereits von einer anderen Ressource verwendet wird. Titel müssen für alle Ressourcentypen eindeutig sein. Wenn Sie beispielsweise versuchen, eine Mischung mit einem Titel zu erstellen, der bereits von einem Schema verwendet wird, erhalten Sie diese Fehlermeldung.

### Benutzerdefinierte Felder müssen ein Feld der obersten Ebene verwenden

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For custom fields, you must use a top level field named _{TENANT_ID}
       and all the other fields must be defined under it"
}
```

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, eine neue Mischung mit falsch benannten Feldern zu erstellen. Mixins, die von Ihrer IMS-Organisation definiert werden, müssen ihre Felder mit einem Namensraum versehen, `TENANT_ID` um Konflikte mit anderen Branchen- und Händlerressourcen zu vermeiden. Ausführliche Beispiele für ordnungsgemäße Datenstrukturen für Mixins finden Sie im Dokument zum [Erstellen eines Mixins](api/create-mixin.md) im [!DNL Schema Registry] API-Entwicklerhandbuch.


### [!DNL Real-time Customer Profile] Fehler

Die folgenden Fehlermeldungen sind mit Vorgängen verknüpft, die an der Aktivierung von Schemas für [!DNL Real-time Customer Profile]. Weitere Informationen finden Sie im Abschnitt [Vereinigungen](./api/unions.md) im Handbuch [!DNL Schema Registry] für API-Entwickler.

#### Um Profil-Datensätze zu aktivieren, sollte das Schema gültig sein

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, einen Profil-Datensatz für ein Schema zu aktivieren, für das nicht aktiviert wurde [!DNL Real-time Customer Profile]. Stellen Sie sicher, dass das Schema ein Vereinigung-Tag enthält, bevor Sie den Datensatz aktivieren.

#### Es muss einen Referenz-Identitätsdeskriptor geben

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For a schema to be able to participate in union, if any of its 
      property is associated with a xdm:descriptorOneToOne descriptor, there must 
      be a xdm:descriptorReferenceIdentity descriptor for that property"
}
```

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, ein Schema für zu aktivieren, [!DNL Profile] und eine seiner Eigenschaften einen Beziehungsdeskriptor ohne Referenz-Identitätsdeskriptor enthält. hinzufügen Sie einen Identitätsdeskriptor für den Verweis auf das betreffende Schema-Feld, um diesen Fehler zu beheben.

#### Der Namensraum des Schemas für den Identitäts-Deskriptor und das Ziel-Identitätsdeskriptor muss übereinstimmen mit dem

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "If both schemas from an already defined xdm:descriptorOneToOne 
      descriptor are promoted to union, and if there is a primary identity on one of 
      the schemas from the xdm:descriptorOneToOne descriptor, the 
      xdm:identityNamespace of the sourceSchema's descriptorReferenceIdentity and the 
      xdm:namespace field of the xdm:descriptorIdentity for the destinationSchema must 
      match"
}
```

Damit Schema mit Beziehungsdeskriptoren zur Verwendung in aktiviert werden können, müssen [!DNL Profile]der Namensraum des Quellfelds und der primäre Namensraum des Felds &quot;Zielgruppe&quot;identisch sein. Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, ein Schema zu aktivieren, das einen nicht übereinstimmenden Namensraum für den Identitätsdeskriptor enthält. Stellen Sie sicher, dass der `xdm:namespace` Wert des Identitätsfelds des Ziel-Schemas mit dem Wert der `xdm:identityNamespace` Eigenschaft im Referenz-Identitätsdeskriptor des Quellfelds übereinstimmt, um dieses Problem zu beheben.

Eine Liste der unterstützten Identitäts-Namensraum-Codes finden Sie im Abschnitt zu [Standard-Namensräumen](../identity-service/namespaces.md) in der Übersicht über den Identitäts-Namensraum.

### Kopfzeilenfehler akzeptieren

Die meisten GET in der [!DNL Schema Registry] API benötigen einen Accept-Header, damit das System festlegt, wie die Antwort formatiert werden soll. Im Folgenden finden Sie eine Liste häufiger Fehler im Zusammenhang mit der Accept-Kopfzeile. Listen kompatibler Accept-Header für verschiedene API-Anforderungen finden Sie in den entsprechenden Abschnitten im [Schema Registry Developer Guide](api/getting-started.md).

#### Accept-Header-Parameter erforderlich

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Accept header parameter is required"
}
```

Diese Fehlermeldung wird angezeigt, wenn in einer API-Anforderung ein Accept-Header fehlt. Stellen Sie sicher, dass ein Accept-Header enthalten ist, bevor Sie es erneut versuchen.

#### Unbekannte bereitgestellte Akzeptanzmedien

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept media supplied: xed+json"
}
```

Diese Fehlermeldung wird angezeigt, wenn ein Accept-Header ungültig ist. Vergewissern Sie sich, dass Sie einen Accept-Header korrekt eingegeben haben, der mit der API-Anforderung kompatibel ist, die Sie ausführen möchten, bevor Sie es erneut versuchen.

#### Unbekanntes Accept-Format verfügbar

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept format available "
}
```

Diese Fehlermeldung wird angezeigt, wenn die Kopfzeile &quot;Akzeptieren&quot;beim Suchen eines Deskriptors falsch angegeben wurde. Vergewissern Sie sich, dass Sie einen der [unterstützten Accept-Header für Deskriptoren](./api/descriptors.md) korrekt eingegeben haben, bevor Sie es erneut versuchen.

#### Version muss im Accept-Header bereitgestellt werden

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full-notext+json; version=1"
}
```

Diese Fehlermeldung wird angezeigt, wenn eine Versionsnummer nicht in der Kopfzeile des Akzeptierten Dokuments enthalten ist. Bestimmte Elemente wie Schema erfordern eine Angabe, wenn nach einzelnen Instanzen gesucht wird. Ein Accept-Header mit einer Versionsnummer sieht wie folgt aus:

```plaintext
application/vnd.adobe.xed+json; version=1
```

Eine Liste der unterstützten Accept-Kopfzeilen finden Sie im Abschnitt [Accept-Kopfzeile](api/getting-started.md#accept) im [!DNL Schema Registry] Entwicklerhandbuch.

#### Version darf nicht im Accept-Header bereitgestellt werden

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must not be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full+json"
}
```

Wenn Sie versuchen, beim Auflisten von Ressourcen (GET) eine Version in Ihren Accept-Header aufzunehmen, erhalten Sie diese Fehlermeldung. Versionen sind nur erforderlich, wenn eine Suchanfrage für eine einzelne Ressource ausgeführt wird. Entfernen Sie die Version aus dem Accept-Header, um den Fehler zu beheben.