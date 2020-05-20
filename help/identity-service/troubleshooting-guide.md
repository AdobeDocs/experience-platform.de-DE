---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbuch zum Identitätsdienst für Adobe Experience Platform
topic: troubleshooting
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53
workflow-type: tm+mt
source-wordcount: '2276'
ht-degree: 1%

---


# Handbuch zur Fehlerbehebung beim Identitätsdienst

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zum Identitätsdienst für Adobe Experience Platform sowie eine Anleitung zur Fehlerbehebung für häufige Fehler. Fragen und Fehlerbehebung zu Plattform-APIs im Allgemeinen finden Sie im Handbuch zur Fehlerbehebung für die [Adobe Experience Platform-APIs](../landing/troubleshooting.md).

Daten, die einen einzelnen Kunden identifizieren, werden häufig über die verschiedenen Geräte und Systeme, die sie zur Interaktion mit Ihrer Marke verwenden, fragmentiert. **Der Identitätsdienst** sammelt diese fragmentierten Identitäten zusammen, was ein vollständiges Verständnis des Kundenverhaltens ermöglicht, sodass Sie in Echtzeit wirkungsvolle digitale Erlebnisse bereitstellen können. Weitere Informationen finden Sie in der Übersicht über den [Identitätsdienst](./home.md).

## FAQs

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zum Identitätsdienst.

## Was sind Identitätsdaten?

Identitätsdaten sind alle Daten, die zur Identifizierung einer einzelnen Person verwendet werden können. Je nach Kontext, in dem die Daten in Ihrem Unternehmen verwendet werden, können Identitätsdaten Benutzernamen, E-Mail-Adressen und IDs aus CRM-Systemen umfassen. Identitätsdaten sind nicht auf registrierte Benutzer Ihrer Website oder Ihres Dienstes beschränkt, da anonyme Benutzer auch anhand ihrer Geräte- oder Cookie-ID identifiziert werden können.

## Welchen Nutzen hat die Kennzeichnung von Datenfeldern als Identitäten?

Durch die Kennzeichnung bestimmter Datenfelder als Identitäten in den Daten zu Datensatz und Zeitreihen können Sie Identitätsbeziehungen innerhalb der natürlichen Datenstruktur zuordnen und Duplikat-Daten über Kanäle hinweg miteinander in Einklang zu bringen. See the [Identity Service overview](./home.md) for more information.

## Was sind bekannte und anonyme Identitäten?

Eine **bekannte Identität** bezieht sich auf einen Identitätswert, der allein oder mit anderen Informationen zur Identifizierung, zum Kontakt oder zur Suche einer einzelnen Person verwendet werden kann. Beispiele für bekannte Identitäten sind E-Mail-Adressen, Telefonnummern und CRM-IDs.

Eine **anonyme Identität** bezieht sich auf einen Identitätswert, der nicht allein oder mit anderen Informationen zur Identifizierung, Kontaktaufnahme oder zur Suche nach einer bestimmten Person (z. B. einer Cookie-ID) verwendet werden kann.

## Was ist ein Diagramm für eine private Identität?

Ein &quot;Private Identity Graph&quot;ist eine private Zuordnung von Beziehungen zwischen verbundenen und verknüpften Identitäten, die nur für Ihr Unternehmen sichtbar ist.

Wenn mehr als eine Identität in Daten enthalten ist, die von einem Streaming-Endpunkt erfasst oder an einen für den Identitätsdienst aktivierten Datensatz gesendet werden, werden diese Identitäten im Diagramm für die private Identität verknüpft. Der Identitätsdienst nutzt dieses Diagramm, um Identitäten für einen bestimmten Verbraucher oder eine bestimmte Entität zu erfassen, was eine Identitätszuordnung und das Zusammenführen von Profilen ermöglicht.

## Wie erstelle ich mehrere Identitätsfelder in einem XDM-Schema?

[Experience Data Model (XDM)](../xdm/home.md) -Schema unterstützen mehrere Identitätsfelder. Jedes Datenfeld vom Typ `string` in einem Schema, das das XDM Individual-Profil oder die XDM ExperienceEvent-Klasse implementiert, kann als Identitätsfeld bezeichnet werden. Nach der Beschriftung werden alle in diesen Feldern enthaltenen Daten der Identitätskarte des Profils hinzugefügt.

Anweisungen zum Bezeichnen eines XDM-Felds als Identitätsfeld mithilfe der Benutzeroberfläche finden Sie im Abschnitt [Identität](../xdm/tutorials/create-schema-ui.md) im Schema-Editor-Lernprogramm. Wenn Sie die API verwenden, finden Sie weitere Informationen zum [Identitätsdeskriptor](../xdm/tutorials/create-schema-api.md) im Schema Registry API-Lernprogramm.

## Gibt es Kontexte, in denen einige Felder nicht als Identitäten gekennzeichnet werden sollten?

Identitätsfelder sollten für Werte reserviert werden, die für jede einzelne Person eindeutig sind. Betrachten Sie beispielsweise einen Datensatz für ein Programm zur Kundentreue. Das Feld &quot;Treuestufe&quot;(Gold, Silber, Bronze) wäre kein nützliches Identitätsfeld, während die Loyalität-ID - ein einzigartiger Wert - dies wäre.

Felder wie Postleitzahlen und IP-Adressen sollten nicht als Identitäten für Einzelpersonen gekennzeichnet werden, da diese Werte für mehrere Personen gelten können. Diese Arten von Feldern sollten nur als Identitäten für Marketingstrategien auf Haushaltsebene gekennzeichnet werden.

## Warum werden meine Identitätsfelder nicht so verknüpft, wie ich es erwartet habe?

Mithilfe des [`/cluster/members` Endpunkts](./api/list-cluster-identites.md) in der Identitätsdienst-API können Sie die zugehörigen Identitäten für ein oder mehrere Identitätsfelder Ansicht haben. Wenn die Antwort nicht die erwarteten verknüpften Identitäten zurückgibt, stellen Sie sicher, dass Sie die entsprechenden Identitätsdaten in Ihren XDM-Daten angeben. Weitere Informationen finden Sie im Abschnitt zur [Bereitstellung von XDM-Daten für den Identitätsdienst](./home.md) in der Übersicht über den Identitätsdienst.

## Was ist ein Identitäts-Namensraum?

Ein Identitäts-Namensraum gibt Kontext an, wie Identitätsfelder mit der Identität eines Kunden zusammenhängen. Beispielsweise sollten Identitätsfelder im Namensraum &quot;E-Mail&quot;einem standardmäßigen E-Mail-Format entsprechen (name<span>@emailprovider.com), während Felder, die den Namensraum &quot;Phone&quot;verwenden, einer Standardtelefonnummer entsprechen sollten (z. B. 987-555-1234 in Nordamerika).

Namensraum unterscheiden ähnliche Identitätswerte zwischen verschiedenen CRM-Systemen. Angenommen, ein Profil enthält eine numerische Loyalität-ID, die mit dem Belohnungs-Programm Ihrer Firma verknüpft ist. Der Namensraum &quot;Loyalität&quot;würde diesen Wert von einer ähnlichen numerischen ID für Ihr E-Commerce-System trennen, die auch im selben Profil angezeigt wird.

See the [identity namespace overview](./home.md) for more information.

## Wie verknüpfe ich eine Identität mit einem Identitäts-Namensraum?

Identitätsfelder müssen beim Erstellen mit einem vorhandenen Identitäts-Namensraum verknüpft werden. Neue Namensraum müssen mit der API [](#how-do-i-create-a-custom-namespace-for-my-organization) erstellt werden, bevor sie mit Identitätsfeldern verknüpft werden.

Eine schrittweise Anleitung zum Definieren eines Namensraums beim Erstellen eines Identitätsdeskriptors mit der API finden Sie im Abschnitt zum [Erstellen eines Deskriptors](../xdm/tutorials/create-schema-ui.md) im Schema Registry Developer Guide. Gehen Sie wie im Lernprogramm &quot; [Schema-Editor&quot;beschrieben vor, um ein Schema als eine ID in der Benutzeroberfläche zu kennzeichnen](../xdm/tutorials/create-schema-api.md).

## Welches sind die standardmäßigen Identitäts-Namensraum, die von Experience Platform bereitgestellt werden?

Die folgenden Standard-Namensraum stehen allen Organisationen in Experience Platform zur Verfügung:

| Anzeigename | ID | Code | Beschreibung |
| ------------ | --- | --- | ----------- |
| CORE | 0 | CORE | Legacy-Name: &quot;Adobe AudienceManager&quot; |
| ECID | 4 | ECID | alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot; |
| E-Mail  | 6 | E-Mail  |  |
| E-Mail (SHA256, Kleinbuchstaben) | 11 | E-Mails | Standard-Namensraum für E-Mail mit einem Hash. Die in diesem Namensraum bereitgestellten Werte werden vor dem Hashing mit SHA-256 in Kleinbuchstaben umgewandelt. |
| Telefon | 7 | Telefon |  |
| Windows-BEIHILFE | 8 | WAID |  |
| AdCloud | 411 | AdCloud | alias: Ad Cloud |
| Adobe Target | 9 | TNTID | Zielgruppen-ID |
| Google Ad ID | 20914 | GAID | GAID |
| Apple IDFA | 20915 | IDFA | ID für Werbetreibende |

## Wo finde ich die Liste der Namensraum für meine Einrichtung?

Mithilfe der [Identitätsdienst-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)können Sie alle für Ihr Unternehmen verfügbaren Identitäts-Namensraum Liste haben, indem Sie eine GET-Anforderung an den `/idnamespace/identities` Endpunkt senden. Weitere Informationen finden Sie im Abschnitt zur [Auflistung der verfügbaren Namensraum](./api/list-namespaces.md) in der Übersicht über die Identitätsdienst-API.

## Wie erstelle ich einen benutzerspezifischen Namensraum für mein Unternehmen?

Mithilfe der [Identitätsdienst-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)können Sie einen benutzerdefinierten Identitäts-Namensraum für Ihr Unternehmen erstellen, indem Sie eine POST-Anforderung an den `/idnamespace/identities` Endpunkt senden. Weitere Informationen finden Sie im Abschnitt zum [Erstellen eines benutzerdefinierten Namensraums](./api/create-custom-namespace.md) in der Übersicht zur Identitätsdienst-API.

## Was sind Composite-Identitäten und XIDs?

Identitäten werden in API-Aufrufen entweder durch ihre zusammengesetzte Identität oder XID referenziert. Eine **zusammengesetzte Identität** ist eine Darstellung einer Identität, die einen ID-Wert und einen Namensraum enthält. Eine **XID** ist eine Kennung mit einem Wert, die dasselbe Konstrukt wie eine zusammengesetzte Identität (eine ID und ein Namensraum) darstellt und automatisch neuen Identitäten zugewiesen wird, wenn sie vom Identitätsdienst beibehalten wird. Weitere Informationen finden Sie in der [Übersicht](./home.md) zur Identitätsdienst-API.

## Wie behandelt der Identitätsdienst personenbezogene Daten (PII)?

Der Identitätsdienst erstellt einen starken, einseitigen kryptografischen Hash des PII, bevor Werte beibehalten werden. Identitätsdaten in den Namensräumen &quot;Telefon&quot;und &quot;E-Mail&quot;werden automatisch mit SHA-256 gehasht, wobei &quot;E-Mail&quot;-Werte vor dem Hashing automatisch in Kleinbuchstaben umgewandelt werden.

## Soll ich alle PII verschlüsseln, bevor ich sie an Platform schicke?

PII-Daten müssen nicht manuell verschlüsselt werden, bevor sie in die Plattform eingegeben werden. Durch Anwendung der `I1` Datenverwendungsbeschriftung auf alle entsprechenden Datenfelder wandelt Platform diese Felder bei der Erfassung automatisch in Hash-ID-Werte um.

Anweisungen zum Anwenden und Verwalten von Bezeichnungen für die Datenverwendung finden Sie im Lernprogramm [mit den Bezeichnungen zur](../data-governance/labels/user-guide.md)Datenverwendung.

## Gibt es Überlegungen beim Hashing von PII-basierten Identitäten?

Wenn Sie Hash-PII-Werte an den Identitätsdienst senden, müssen Sie dieselbe Verschlüsselungsmethode für Ihre Datensätze verwenden. Dadurch wird sichergestellt, dass der gleiche Identitätswert für alle Datensätze dieselben Hash-Werte generiert und im Identitätsdiagramm richtig zugeordnet und verknüpft werden kann.

<!-- Documentation does not show any methods of editing the identityMap directly, and this table never overtly recommends using identityMap anyway. This should probably be removed unless PM thinks otherwise. -->
<!-- ## When should I use the Identity map rather than labeling individual XDM schema fields?

The following table describes when the recommended approach for including identity data in your XDM would be identity map and when an identity field is the better method.

>[!NOTE] An advantage `identityMap` has is the ability to include multiple identity values for a single namespace.

Write|XDM identity field|`identityMap`
---|---|---
UI|Supported|Supported
Developer|Recommended|Supported
ETL|Recommended|Avoid - While this is supported, data should be formatted naturally when using an ETL, favoring identity fields over `identityMap`.
Internal solutions|Preferred|Common

--- -->

## Fehlerbehebung

Der folgende Abschnitt enthält Vorschläge zur Fehlerbehebung für bestimmte Fehlercodes und unerwartetes Verhalten, auf das Sie bei der Arbeit mit der Identitätsdienst-API stoßen können.

## Fehlermeldungen beim Identitätsdienst

Im Folgenden finden Sie eine Liste von Fehlermeldungen, die Sie möglicherweise bei der Verwendung der Identitätsdienst-API erhalten.

### Fehlender erforderlicher Parameter für die Abfrage

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

Dieser Fehler wird angezeigt, wenn kein erforderlicher Parameter für die Abfrage im Anforderungspfad enthalten war. Die `detail` Fehlermeldung enthält den Namen des fehlenden Parameters. Zu den Varianten dieser Fehlermeldung zählen:

- Fehlender erforderlicher Parameter für die Abfrage - nsId
- Fehlender erforderlicher Parameter für die Abfrage - id
- Fehlender erforderlicher Parameter für die Abfrage - xid oder (nsid,id)
- Fehlender erforderlicher Parameter für die Abfrage - targetNs
- Fehlender erforderlicher Parameter für die Abfrage - xids oder positeXids

Vergewissern Sie sich, dass Sie den angegebenen Parameter ordnungsgemäß in den Anforderungspfad einbeziehen, bevor Sie es erneut versuchen.

### Der Zeitstempel sollte innerhalb der letzten 180 Tage liegen.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

Der Identitätsdienst bereinigt Daten, die älter als 180 Tage sind. Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, auf ältere Daten zuzugreifen.

### Es gibt eine Beschränkung von 1000 XIDs in einem einzelnen Aufruf

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, Identitätsinformationen für mehr als die maximal zulässige Anzahl von [XIDs](#what-are-composite-identities-and-xids) in einem einzelnen API-Aufruf abzurufen. Reduzieren Sie die Anzahl der XIDs in Ihrer Anforderung auf unter die angezeigte Grenze, um dieses Problem zu beheben.


### Es gibt eine Beschränkung für 1000 CompositeXids in einem einzelnen Aufruf

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, Identitätsinformationen für mehr als die maximal zulässige Anzahl [zusammengesetzter Identitäten](#what-are-composite-identities-and-xids) in einem einzelnen API-Aufruf abzurufen. Reduzieren Sie die Anzahl der zusammengesetzten Identitäten in Ihrer Anforderung auf unter die angezeigte Grenze, um dieses Problem zu beheben.

### Der angegebene Diagrammtyp ist ungültig

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

Diese Fehlermeldung wird angezeigt, wenn einem `graph-type` Abfrage-Parameter im Anforderungspfad ein ungültiger Wert zugewiesen wird. Im Abschnitt zu [Identitätsdiagrammen](./home.md) in der Übersicht zum Identitätsdienst erfahren Sie, welche Diagrammtypen unterstützt werden.

### Service-Token hat keinen gültigen Gültigkeitsbereich

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

Diese Fehlermeldung wird angezeigt, wenn Ihre IMS-Organisation nicht über die erforderlichen Berechtigungen für den Identitätsdienst verfügt. Wenden Sie sich an Ihren Systemadministrator, um dieses Problem zu beheben.

### Gateway-Dienst-Token ist nicht gültig

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

Bei diesem Fehler ist Ihr Zugriffstoken ungültig. Zugriffstoken laufen alle 24 Stunden ab und müssen neu generiert werden, um weiterhin Platform-APIs verwenden zu können. Anweisungen zum Generieren neuer Zugriffstoken finden Sie im [Authentifizierungstraining](../tutorials/authentication.md) .

### Autorisierungsdienst-Token ist nicht gültig

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

Bei diesem Fehler ist Ihr Zugriffstoken ungültig. Zugriffstoken laufen alle 24 Stunden ab und müssen neu generiert werden, um weiterhin Platform-APIs verwenden zu können. Anweisungen zum Generieren neuer Zugriffstoken finden Sie im [Authentifizierungstraining](../tutorials/authentication.md) .

### Benutzertoken haben keinen gültigen Produktkontext

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

Diese Fehlermeldung wird angezeigt, wenn Ihr Zugriffstoken nicht aus einer Experience Platform-Integration generiert wurde. Anweisungen zum Generieren neuer Zugriffstoken für eine Experience Platform-Integration finden Sie im [Authentifizierungstraining](../tutorials/authentication.md) .

### Interner Fehler beim Abrufen der nativen XID aus dem Identitäts- und Namensraum-Code

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

Wenn der Identitätsdienst eine Identität beibehält, wird der ID der Identität und der zugehörigen Namensraum-ID eine eindeutige ID zugewiesen, die als XID bezeichnet wird. Diese Meldung wird angezeigt, wenn während des Suchvorgangs der XID für einen angegebenen ID-Wert und Namensraum ein Fehler auftritt.

### Das IMS-Org wird nicht für die Verwendung des Identitätsdienstes bereitgestellt

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

Diese Fehlermeldung wird angezeigt, wenn Ihre IMS-Organisation nicht über die erforderlichen Berechtigungen für den Identitätsdienst verfügt. Wenden Sie sich an Ihren Systemadministrator, um dieses Problem zu beheben.

### Interner Serverfehler

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

Dieser Fehler wird angezeigt, wenn bei der Ausführung eines Platform-Dienstaufrufs eine unerwartete Ausnahme auftritt. Es empfiehlt sich, Ihre automatisierten Aufrufe so Programm, dass sie ihre Anforderungen in einem bestimmten Zeitintervall wiederholen, wenn sie diesen Fehler erhalten. Wenn das Problem weiterhin besteht, wenden Sie sich an Ihren Systemadministrator.

## Stapeleingangsfehlercodes

Der Identitätsdienst erfasst Identitätsdaten aus Datensatz- und Zeitreihendaten, die mithilfe der Stapeleinbettung auf die Plattform hochgeladen werden. Da die Stapelverarbeitung ein asynchroner Vorgang ist, müssen Sie die Details für einen Batch-zu-Ansicht-Fehler Ansicht haben. Während der Stapelverarbeitung werden Fehler angesammelt, bis der Stapel abgeschlossen ist.

Im Folgenden finden Sie eine Liste von Fehlermeldungen im Zusammenhang mit dem Identitätsdienst, auf die Sie bei der Verwendung der [Dateneinbetungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)stoßen können.

### Unbekanntes XDM-Schema

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

Der Identitätsdienst nutzt nur Identitäten für Datensatz- oder Zeitreihendaten, die den Profil- bzw. ExperienceEvent-Klassen entsprechen. Der Versuch, Daten für den Identitätsdienst zu erfassen, die keiner der beiden Klassen entsprechen, löst diesen Fehler aus.

### Es gab 0 gültige Identitäten in den ersten 100 Zeilen des verarbeiteten Stapels

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

Dieser Fehler wird angezeigt, wenn die ersten 100 Zeilen eines Stapels keine Identitäten aufweisen. Dieser Fehler deutet jedoch nicht eindeutig darauf hin, dass in den nachfolgenden Aufzeichnungen keine Identitäten gefunden wurden.

### Übersprungene Datensätze, da sie nur eine Identität pro XDM-Datensatz hatten

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

Der Identitätsdienst verknüpft nur Identitäten, wenn einzelne Datensätze zwei oder mehr Identitätswerte enthalten. Diese Fehlermeldung tritt einmal für jeden erfassten Stapel auf. Sie zeigt die Anzahl der Datensätze an, in denen nur eine Identität gefunden wurde und keine Änderung am Identitätsdiagramm vorgenommen wurde.

### Namensraum-Code für dieses IMS-Org nicht registriert

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

Dieser Fehler wird angezeigt, wenn ein erfasster Datensatz eine Identität enthält, deren verknüpfter Namensraum nicht vorhanden ist oder für Ihre IMS-Organisation nicht zugänglich ist.

### Stapelverarbeitung überspringen, da IMS-Org nicht für das Diagramm für private Identitäten bereitgestellt wird

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

Beim Erfassen von Stapeldaten wird diese Fehlermeldung angezeigt, wenn Ihr IMS-Unternehmen nicht über die erforderlichen Berechtigungen für den Identitätsdienst verfügt. Wenden Sie sich an Ihren Systemadministrator, um dieses Problem zu beheben.

### Interner Fehler

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

Dieser Fehler wird angezeigt, wenn während der Stapelverarbeitung eine unerwartete Ausnahme auftritt. Es empfiehlt sich, Ihre automatisierten Aufrufe so Programm, dass sie ihre Anforderungen in einem bestimmten Zeitintervall wiederholen, wenn sie diesen Fehler erhalten. Wenn das Problem weiterhin besteht, wenden Sie sich an Ihren Systemadministrator.
