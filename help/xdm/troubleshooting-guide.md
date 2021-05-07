---
keywords: Experience Platform;Home;beliebte Themen;XDM;XDM-System;XDM-Profil;XDM ExperienceEvent;XDM Experience-Ereignis;experienceEvent;experience eventExperience-Ereignis;XDM-Experience-Ereignis;XDM-Erlebnis-Datenmodell;Erlebnis-Datenmodell;Datenmodell;Datenmodell;Schema;Fehlerbehebung;FAQ;Vereinigung-Schema;VEREINIGUNG-PROFIL;Vereinigung
solution: Experience Platform
title: XDM-System - Fehlerbehebungshandbuch
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Experience Data Model (XDM) und XDM System in Adobe Experience Platform sowie eine Anleitung zur Fehlerbehebung für häufige Fehler.
topic-legacy: troubleshooting
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
translation-type: tm+mt
source-git-commit: 3985ba8f46a62e8d9ea8b1f084198b245318a24f
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 1%

---

# Handbuch zur Fehlerbehebung im XDM-System

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu [!DNL Experience Data Model] (XDM) und XDM System in Adobe Experience Platform sowie eine Anleitung zur Fehlerbehebung für häufige Fehler. Fragen und Fehlerbehebungen für andere Platform-Dienste finden Sie im [Handbuch zur Fehlerbehebung in Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** ist eine Open-Source-Spezifikation, die standardisierte Schema für das Kundenerlebnis-Management definiert. Die Methodik, auf der [!DNL Experience Platform] erstellt wird, **XDM-System**, setzt [!DNL Experience Data Model]-Schema für die Verwendung durch [!DNL Platform]-Dienste ein. Das **[!DNL Schema Registry]** stellt eine Benutzeroberfläche und eine RESTful-API für den Zugriff auf das **[!DNL Schema Library]** innerhalb von [!DNL Experience Platform] bereit. Weitere Informationen finden Sie in der [XDM-Dokumentation](home.md).

## FAQs

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zum XDM-System und zur Verwendung der [!DNL Schema Registry]-API.

### Wie füge ich einem Schema Felder hinzu?

Sie können Felder zu einem Schema hinzufügen, indem Sie eine Schema-Feldgruppe verwenden. Jede Feldgruppe ist mit einer oder mehreren Klassen kompatibel, sodass die Feldgruppe in allen Schemas verwendet werden kann, die eine dieser kompatiblen Klassen implementieren. Adobe Experience Platform stellt mehrere Branchenfeldgruppen mit eigenen vordefinierten Feldern zur Verfügung. Sie können jedoch eigene Felder zu einem Schema hinzufügen, indem Sie neue Feldgruppen mit der API oder der Benutzeroberfläche erstellen.

Weitere Informationen zum Erstellen neuer Feldgruppen in der API finden Sie im Handbuch [!DNL Schema Registry] für Feldgruppen-Endpunkte](api/field-groups.md#create). [ Wenn Sie die Benutzeroberfläche verwenden, lesen Sie das Tutorial [Schema-Editor](./tutorials/create-schema-ui.md).

### Welches sind die besten Verwendungen für Feldgruppen oder Datentypen?

[Feldgruppen ](./schema/composition.md#field-group) sind Komponenten, die ein oder mehrere Felder in einem Schema definieren. Feldgruppen erzwingen, wie ihre Felder in der Hierarchie des Schemas angezeigt werden, und weisen daher in jedem Schema dieselbe Struktur auf, in dem sie enthalten sind. Feldgruppen sind nur mit bestimmten Klassen kompatibel, die durch ihr `meta:intendedToExtend`-Attribut gekennzeichnet sind.

[Datentypen ](./schema/composition.md#data-type) können auch ein oder mehrere Felder für ein Schema bereitstellen. Im Gegensatz zu Feldgruppen sind Datentypen jedoch nicht auf eine bestimmte Klasse beschränkt. Dadurch werden Datentypen flexibler, um häufig verwendete Datenstrukturen zu beschreiben, die über mehrere Schema mit potenziell unterschiedlichen Klassen hinweg wiederverwendet werden können.

### Was ist die eindeutige ID für ein Schema?

Alle [!DNL Schema Registry]-Ressourcen (Schema, Feldgruppen, Datentypen, Klassen) verfügen über einen URI, der als eindeutige ID für Referenz- und Nachschlagezwecke dient. Wenn Sie ein Schema in der API anzeigen, finden Sie es in den Attributen `$id` und `meta:altId` der obersten Ebene.

Weitere Informationen finden Sie im Abschnitt [Ressourcenidentifizierung](api/getting-started.md#resource-identification) im API-Entwicklerhandbuch.[!DNL Schema Registry]

### Wann verhindert ein Schema-Beginn Umbrüche?

Umbrüchige Änderungen können an einem Schema vorgenommen werden, solange es noch nie bei der Erstellung eines Datensatzes verwendet oder für die Verwendung in [[!DNL Real-time Customer Profile]](../profile/home.md) aktiviert wurde. Sobald ein Schema bei der Erstellung eines Datensatzes verwendet oder für die Verwendung mit [!DNL Real-time Customer Profile] aktiviert wurde, werden die Regeln von [Schema Evolution](schema/composition.md#evolution) vom System strikt durchgesetzt.

### Wie hoch ist die maximale Größe eines langen Feldtyps?

Ein langer Feldtyp ist eine Ganzzahl mit einer maximalen Größe von 53 (+1) Bit, wodurch ein potenzieller Bereich zwischen -9007199254740992 und 9007199254740992 liegt. Dies liegt daran, dass JavaScript-Implementierungen von JSON keine langen Ganzzahlen darstellen.

Weitere Informationen zu Feldtypen finden Sie im Dokument zu [XDM-Feldtypbeschränkungen](./schema/field-constraints.md).

### Wie definiere ich Identitäten für mein Schema?

In [!DNL Experience Platform] werden Identitäten verwendet, um ein Subjekt (normalerweise eine einzelne Person) unabhängig von den Quellen der zu interpretierenden Daten zu identifizieren. Sie werden in Schemas definiert, indem Sie Schlüsselfelder als &quot;Identität&quot;markieren. Häufig verwendete Identitätsfelder sind E-Mail-Adresse, Telefonnummer, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), CRM-ID und andere eindeutige ID-Felder.

Felder können entweder über die API oder die Benutzeroberfläche als Identitäten gekennzeichnet werden.

#### Definieren von Identitäten in der API

In der API werden Identitäten durch Erstellen von Identitätsdeskriptoren festgelegt. Identitätsdeskriptoren signalisieren, dass eine bestimmte Eigenschaft für ein Schema ein eindeutiger Bezeichner ist.

Identitätsdeskriptoren werden durch eine POST an den /descriptors-Endpunkt erstellt. Bei erfolgreichem Abschluss erhalten Sie einen HTTP-Status 201 (Erstellt) und ein Antwortobjekt mit den Details des neuen Deskriptors.

Weitere Informationen zum Erstellen von Identitätsdeskriptoren in der API finden Sie im Dokument zu [deskriptoren](api/descriptors.md) im [!DNL Schema Registry]-Entwicklerhandbuch.

#### Definieren von Identitäten in der Benutzeroberfläche

Wenn Ihr Schema im Schema-Editor geöffnet ist, wählen Sie das Feld im Bereich **[!UICONTROL Struktur]** des Editors aus, das Sie als Identität markieren möchten. Aktivieren Sie unter **[!UICONTROL Feldeigenschaften]** auf der rechten Seite das Kontrollkästchen **[!UICONTROL Identität]**.

Weitere Informationen zum Verwalten von Identitäten in der Benutzeroberfläche finden Sie im Abschnitt [Definieren von Identitätsfeldern](./tutorials/create-schema-ui.md#identity-field) im Schema-Editor-Lernprogramm.

### Braucht mein Schema eine primäre Identität?

Primär-IDs sind optional, da Schema 0 oder 1 davon haben können. Ein Schema muss jedoch über eine primäre Identität verfügen, damit das Schema für die Verwendung in [!DNL Real-time Customer Profile] aktiviert werden kann. Weitere Informationen finden Sie im Abschnitt [identity](./tutorials/create-schema-ui.md#identity-field) des Schema-Editor-Tutorials.

### Wie aktiviere ich ein Schema zur Verwendung in [!DNL Real-time Customer Profile]?

Schema sind für die Verwendung in [[!DNL Real-time Customer Profile]](../profile/home.md) durch das Hinzufügen eines &quot;Vereinigung&quot;-Tags aktiviert, das sich im `meta:immutableTags`-Attribut des Schemas befindet. Die Aktivierung eines Schemas zur Verwendung mit [!DNL Profile] kann über die API oder die Benutzeroberfläche erfolgen.

#### Aktivieren eines vorhandenen Schemas für [!DNL Profile] mithilfe der API

Führen Sie eine PATCH-Anforderung durch, um das Schema zu aktualisieren und das `meta:immutableTags`-Attribut als Array mit dem Wert &quot;Vereinigung&quot;hinzuzufügen. Wenn die Aktualisierung erfolgreich ist, zeigt die Antwort das aktualisierte Schema an, das jetzt das Vereinigung-Tag enthält.

Weitere Informationen zur Verwendung der API zum Aktivieren eines Schemas für die Verwendung in [!DNL Real-time Customer Profile] finden Sie im Dokument [Vereinigungen](./api/unions.md) des [!DNL Schema Registry]-Entwicklerhandbuchs.

#### Aktivieren eines vorhandenen Schemas für [!DNL Profile] mithilfe der Benutzeroberfläche

Wählen Sie in [!DNL Experience Platform] in der linken Navigation **[!UICONTROL Schema]** und wählen Sie den Namen des Schemas aus, das Sie in der Liste der Schema aktivieren möchten. Wählen Sie dann auf der rechten Seite des Editors unter **[!UICONTROL Schema Properties]** **[!UICONTROL Profil]** aus, um es einzuschalten.


Weitere Informationen finden Sie im Abschnitt [Verwenden Sie in Echtzeit Customer Profil](./tutorials/create-schema-ui.md#profile) im Lehrgang [!UICONTROL Schema Editor].

### Kann ich ein Vereinigung-Schema direkt bearbeiten?

Vereinigung-Schema sind schreibgeschützt und werden automatisch vom System generiert. Sie können nicht direkt bearbeitet werden. Vereinigung-Schema werden für eine bestimmte Klasse erstellt, wenn dem Schema, das diese Klasse implementiert, ein &quot;Vereinigung&quot;-Tag hinzugefügt wird.

Weitere Informationen zu Vereinigungen in XDM finden Sie im Abschnitt [Vereinigungen](./api/unions.md) im API-Entwicklerhandbuch.[!DNL Schema Registry]

### Wie formatiere ich meine Datendatei, um Daten in mein Schema zu erfassen?

[!DNL Experience Platform] Akzeptiert Datendateien im JSON-  [!DNL Parquet] oder JSON-Format. Der Inhalt dieser Dateien muss mit dem Schema übereinstimmen, auf das der Datensatz verweist. Weitere Informationen zu den Best Practices für die Datafile-Erfassung finden Sie unter [Überblick über die Stapelverarbeitung](../ingestion/home.md).

## Fehler und Fehlerbehebung

Im Folgenden finden Sie eine Liste von Fehlermeldungen, auf die Sie bei der Arbeit mit der [!DNL Schema Registry]-API stoßen können.

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

Weitere Informationen zum Erstellen von Nachschlagepfaden in der API finden Sie in den Abschnitten [Container](./api/getting-started.md#container) und [Ressourcenidentifizierung](api/getting-started.md#resource-identification) im [!DNL Schema Registry]-Entwicklerhandbuch.

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

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, eine Ressource mit einem Titel zu erstellen, der bereits von einer anderen Ressource verwendet wird. Titel müssen für alle Ressourcentypen eindeutig sein. Wenn Sie z. B. versuchen, eine Feldgruppe mit einem Titel zu erstellen, der bereits von einem Schema verwendet wird, erhalten Sie diese Fehlermeldung.

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

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, eine neue Feldgruppe mit falsch benannten Feldern zu erstellen. Feldgruppen, die von Ihrer IMS-Organisation definiert werden, müssen ihre Felder mit einem `TENANT_ID` Namensraum versehen, um Konflikte mit anderen Branchen- und Händlerressourcen zu vermeiden. Ausführliche Beispiele für ordnungsgemäße Datenstrukturen für Feldgruppen finden Sie im Endpunktleitfaden [Feldgruppen](./api/field-groups.md#create).


### [!DNL Real-time Customer Profile] Fehler

Die folgenden Fehlermeldungen sind mit Vorgängen verknüpft, die an der Aktivierung von Schemas für [!DNL Real-time Customer Profile] beteiligt sind. Weitere Informationen finden Sie im Abschnitt [Vereinigungen](./api/unions.md) im API-Entwicklerhandbuch.[!DNL Schema Registry]

#### Um Profil-Datensätze zu aktivieren, sollte das Schema gültig sein

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, einen Profil-Datensatz für ein Schema zu aktivieren, das nicht für [!DNL Real-time Customer Profile] aktiviert wurde. Stellen Sie sicher, dass das Schema ein Vereinigung-Tag enthält, bevor Sie den Datensatz aktivieren.

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

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, ein Schema für [!DNL Profile] zu aktivieren, und eine seiner Eigenschaften einen Beziehungsdeskriptor ohne Referenz-Identitätsdeskriptor enthält. hinzufügen Sie einen Identitätsdeskriptor für den Verweis auf das betreffende Schema-Feld, um diesen Fehler zu beheben.

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

Um Schema mit Beziehungsdeskriptoren für die Verwendung in [!DNL Profile] zu aktivieren, müssen der Namensraum des Quellfelds und der primäre Namensraum des Felds &quot;Zielgruppe&quot;identisch sein. Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, ein Schema zu aktivieren, das einen nicht übereinstimmenden Namensraum für den Identitätsdeskriptor enthält. Stellen Sie sicher, dass der `xdm:namespace`-Wert des Identitätsfelds des Zielfelds mit dem Wert der `xdm:identityNamespace`-Eigenschaft im Referenz-Identitätsdeskriptor des Quellfelds übereinstimmt, um dieses Problem zu beheben.

Eine Liste der unterstützten Identitäts-Namensraum-Codes finden Sie im Abschnitt [Standard-Namensraum](../identity-service/namespaces.md) in der Übersicht über den Identitäts-Namensraum.

### Kopfzeilenfehler akzeptieren

Die meisten GET in der API erfordern einen Accept-Header, damit das System festlegt, wie die Antwort formatiert werden soll. [!DNL Schema Registry] Im Folgenden finden Sie eine Liste häufiger Fehler im Zusammenhang mit der Accept-Kopfzeile. Listen kompatibler Accept-Kopfzeilen für verschiedene API-Anforderungen finden Sie in den entsprechenden Abschnitten im [Schema Registry-Entwicklerhandbuch](api/getting-started.md).

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

Eine Liste der unterstützten Accept-Kopfzeilen finden Sie im Abschnitt [Accept header](api/getting-started.md#accept) im [!DNL Schema Registry] Entwicklerhandbuch.

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
