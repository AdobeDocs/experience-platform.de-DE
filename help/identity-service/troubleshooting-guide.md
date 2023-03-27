---
keywords: Experience Platform;Startseite;beliebte Themen;Identity Namespace;Identity-Namespace
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei Identity Service
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zum Adobe Experience Platform Identity Service sowie eine Anleitung zur Behebung gängiger Fehler.
exl-id: dac31bc3-7003-46d6-9d41-9f6fd3645c2c
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '2180'
ht-degree: 98%

---

# Handbuch zur Fehlerbehebung bei Identity Service

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Adobe Experience Platform [!DNL Identity Service] sowie eine Anleitung zur Behebung gängiger Fehler. Antworten zu Fragen und allgemeine Informationen zur Fehlerbehebung bei [!DNL Platform]-APIs finden Sie im [Handbuch zur Fehlerbehebung bei Adobe Experience Platform-APIs](../landing/troubleshooting.md).

Daten, die eine Identifizierung einzelner Kundinnen und Kunden erlauben, sind häufig auf die verschiedenen Geräte und Systeme verteilt, die Kundinnen und Kunden zur Interaktion mit Ihrer Marke verwenden. [!DNL Identity Service] sammelt diese fragmentierten Identitäten und fasst sie zusammen, um eine vollständige Übersicht über Kundenverhalten zu liefern, sodass Sie in Echtzeit für effektive digitale Erlebnisse sorgen können. Weiterführende Informationen finden Sie in der [Identity Service – Übersicht](./home.md).

## FAQs

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zu [!DNL Identity Service].

## Was sind Identitätsdaten?

Identitätsdaten sind alle Daten, anhand derer sich einzelne Personen identifizieren lassen. Je nach Kontext, in dem solche Daten in Ihrer Organisation genutzt werden, können Identitätsdaten Benutzernamen, E-Mail-Adressen und Kennungen aus CRM-Systemen umfassen. Identitätsdaten sind nicht auf registrierte Benutzer Ihrer Website oder Ihres Dienstes beschränkt, da sich anonyme Benutzer anhand ihrer Geräte- oder Cookie-Kennungen ebenfalls identifizieren lassen.

## Welchen Nutzen bietet eine Kennzeichnung von Datenfeldern als Identitäten?

Durch Kennzeichnung bestimmter Datenfelder in Ihren Datensatz- und Zeitreihendaten als Identitäten können Sie innerhalb der natürlichen Struktur Ihrer Daten Identitätsbeziehungen zuordnen und Duplikatdaten kanalübergreifend aufeinander abstimmen. Weiterführende Informationen dazu finden Sie unter [Identity Service – Übersicht](./home.md).

## Was sind bekannte und anonyme Identitäten?

Eine bekannte Identität bezieht sich auf einen Identitätswert, der allein oder mit anderen Daten zum Identifizieren, Kontaktieren oder Finden einer bestimmten Person verwendet werden kann. Beispiele für bekannte Identitäten sind E-Mail-Adressen, Telefonnummern und CRM-Kennungen.

Eine anonyme Identität bezieht sich auf einen Identitätswert, der sich nicht allein oder mit anderen Daten zum Identifizieren, Kontaktieren oder Finden einer bestimmten Person nutzen lässt (z. B. eine Cookie-Kennung).

## Was ist ein privates Identitätsdiagramm?

Ein privates Identitätsdiagramm ist eine private Zuordnung von Beziehungen zwischen zusammengefügten und verknüpften Identitäten, die nur für Ihre Organisation sichtbar ist.

Wenn in Daten, die von einem Streaming-Endpunkt aufgenommen oder an einen für [!DNL Identity Service] aktivierten Datensatz gesendet werden, mehr als eine Identität enthalten ist, werden diese Identitäten im privaten Identitätsdiagramm miteinander verknüpft. [!DNL Identity Service] nutzt dieses Diagramm, um Identitäten für eine bestimmte Verbraucherin oder einen bestimmten Verbraucher oder eine Entität zu ermitteln, und ermöglicht so Identitätsabgleich und Profilzusammenführung.

## Wie erstelle ich in einem XDM-Schema mehrere Identitätsfelder?

[Experience-Datenmodell (XDM)](../xdm/home.md)-Schemas unterstützen die Verwendung mehrerer Identitätsfelder. Jedes Datenfeld vom Typ `string` in einem Schema, das das individuelle XDM-Profil oder die XDM ExperienceEvent-Klasse implementiert, kann als Identitätsfeld gekennzeichnet werden. Nach der Kennzeichnung werden alle in diesen Feldern enthaltenen Daten der Identitätszuordnung des Profils hinzugefügt.

Anweisungen zum Kennzeichnen eines XDM-Felds als Identitätsfeld mithilfe der Benutzeroberfläche finden Sie im Abschnitt [Identität](../xdm/tutorials/create-schema-ui.md) im Tutorial zum Schema-Editor. Wenn Sie stattdessen die API nutzen, finden Sie weiterführende Informationen im Abschnitt [Identitätsdeskriptor](../xdm/tutorials/create-schema-api.md) im Tutorial zur Schema Registry-API.

## Gibt es Fälle, in denen Felder nicht als Identitäten gekennzeichnet werden sollten?

Identitätsfelder sollten für Werte reserviert bleiben, die für jeden einzelnen Kontakt eindeutig sind. Betrachten Sie beispielsweise einen Datensatz für ein Treueprogramm für Kunden. Das Feld „Treuestufe“ (Gold, Silber, Bronze) wäre kein nützliches Identitätsfeld, die Loyalitätskennung (ein eindeutiger Wert) hingegen schon.

Felder wie Postleitzahlen und IP-Adressen sollten nicht als Identitäten für einzelne Personen gekennzeichnet werden, da diese Werte für mehr als eine Person gültig sein können. Solche Felder sollten nur bei Marketing-Strategien auf der Haushaltsebene als Identitäten gekennzeichnet werden.

## Warum werden meine Identitätsfelder nicht so miteinander verknüpft, wie ich es erwartet habe?

Mit dem [`/cluster/members`Endpunkt](./api/list-cluster-identites.md) in der Identity Service-API können Sie zugehörige Identitäten für ein oder mehrere Identitätsfelder anzeigen. Wenn die Antwort nicht die erwarteten verknüpften Identitäten zurückgibt, stellen Sie sicher, dass Sie in Ihren XDM-Daten die entsprechenden Identitätsdaten angegeben haben. Weiterführende Informationen finden Sie im Abschnitt zum [Bereitstellen von XDM-Daten für Identity Service](./home.md) in der Übersicht zu Identity Service.

## Was ist ein Identitäts-Namespace?

Ein Identitäts-Namespace liefert Kontext dazu, wie Identitätsfelder mit der Identität eines Kunden zusammenhängen. Beispielsweise sollten Identitätsfelder unter dem Namespace „E-Mail“ einem standardmäßigen E-Mail-Format entsprechen (name<span>@emailprovider.com), während Felder, die den Namespace „Telefon“ verwenden, einer Standardtelefonnummer entsprechen sollten (in Nordamerika z. B. 987-555-1234).

Namespaces unterscheiden bei verschiedenen CRM-Systemen zwischen ähnlichen Identitätswerten. Nehmen wir an, dass ein Profil eine numerische Kennung für das Treueprogramm enthält, die mit dem Belohnungsprogramm Ihres Unternehmens verknüpft ist. Der Namespace „Treueprogramm“ würde diesen Wert von einer ähnlichen numerischen Kennung für Ihr E-Commerce-System trennen, die im selben Profil ebenfalls angezeigt wird.

Weiterführende Informationen dazu finden Sie unter [Übersicht zu Identitäts-Namespaces](./home.md).

## Wie verknüpfe ich eine Identität mit einem Identitäts-Namespace?

Identitätsfelder müssen beim Erstellen mit einem vorhandenen Identitäts-Namespace verknüpft werden. Neue Namespaces müssen [mit der API erstellt](#how-do-i-create-a-custom-namespace-for-my-organization) werden, bevor sie mit Identitätsfeldern verknüpft werden.

Eine schrittweise Anleitung zum Definieren eines Namespace beim Erstellen eines Identitätsdeskriptors mit der API finden Sie im Abschnitt zum [Erstellen eines Deskriptors](../xdm/tutorials/create-schema-ui.md) im Entwicklerhandbuch zur Schemaregistrierung. Gehen Sie wie im Tutorial zum [Schema-Editor](../xdm/tutorials/create-schema-api.md) beschrieben vor, um in der Benutzeroberfläche ein Schema als Identität zu kennzeichnen.

## Welche Identitäts-Namespaces stellt Experience Platform standardmäßig bereit? {#standard-namespaces}

Standardmäßige Identity-Namespaces sind Namespaces, die für alle Organisationen verfügbar sind. Eine vollständige Liste der verfügbaren Standard-Namespaces finden Sie in der [Übersicht zu Identity-Namespaces](./namespaces.md).

## Wo finde ich die Liste der verfügbaren Namespaces für meine Organisation?

Mit der [Identity Service-API](https://www.adobe.io/experience-platform-apis/references/identity-service) können Sie alle für Ihre Organisation verfügbaren Identitäts-Namespaces auflisten, indem Sie eine GET-Anfrage an den `/idnamespace/identities`-Endpunkt senden. Weiterführende Informationen finden Sie im Abschnitt [Auflisten der verfügbaren Namespaces](./api/list-namespaces.md) in der Übersicht zur Identity Service-API.

## Wie erstelle ich für meine Organisation einen benutzerspezifischen Namespace?

Mit der [Identity Service-API](https://www.adobe.io/experience-platform-apis/references/identity-service) können Sie einen benutzerdefinierten Identitäts-Namespace für Ihre Organisation einrichten, indem Sie eine POST-Anfrage an den `/idnamespace/identities`-Endpunkt senden. Weiterführende Informationen finden Sie im Abschnitt [Erstellen eines benutzerdefinierten Namespace](./api/create-custom-namespace.md) in der Übersicht zur Identity Service-API.

## Was sind zusammengesetzte Identitäten und XIDs?

Identitäten werden in API-Aufrufen entweder anhand ihrer zusammengesetzten Identität oder ihrer XID referenziert. Eine zusammengesetzte Identität ist eine Darstellung einer Identität, die einen ID-Wert und einen Namespace enthält. Eine XID ist eine Kennung mit einem Wert, die dasselbe Konstrukt wie eine zusammengesetzte Identität (eine Kennung und ein Namespace) darstellt und neuen Identitäten automatisch zugewiesen wird, wenn diese von Identity Service persistiert werden. Weiterführende Informationen finden Sie in der [Übersicht zur Identity Service-API](./home.md).

## Wie geht Identity Service mit personenbezogenen Daten (PII) um?

Identity Service verfügt über Standard-Namespaces, die die Aufnahme von Hash-Identitätswerten für Telefonnummern und E-Mail-Adressen unterstützen. Sie sind jedoch für das Hashing von Werten verantwortlich. Weitere Informationen zum Hashing von Daten, die in Platform aufgenommen werden, finden Sie im [[!DNL Data Prep] Handbuch zu Zuordnungsfunktionen](../data-prep/functions.md#hashing).

## Was gilt es beim Hashing von PII-basierten Identitäten zu beachten?

Wenn Sie gehashte PII-Werte an den Identity Service senden, müssen Sie für alle Datensätze dieselbe Verschlüsselungsmethode verwenden. Dadurch wird sichergestellt, dass der gleiche Identitätswert bei allen Datensätzen dieselben Hash-Werte generiert und im Identitätsdiagramm richtig zugeordnet und verknüpft werden kann.

<!-- Documentation does not show any methods of editing the identityMap directly, and this table never overtly recommends using identityMap anyway. This should probably be removed unless PM thinks otherwise. -->
<!-- ## When should I use the Identity map rather than labeling individual XDM schema fields?

The following table describes when the recommended approach for including identity data in your XDM would be identity map and when an identity field is the better method.

>[!NOTE]
>
>An advantage `identityMap` has is the ability to include multiple identity values for a single namespace.

Write|XDM identity field|`identityMap`
---|---|---
UI|Supported|Supported
Developer|Recommended|Supported
ETL|Recommended|Avoid - While this is supported, data should be formatted naturally when using an ETL, favoring identity fields over `identityMap`.
Internal solutions|Preferred|Common

--- -->

## Warum kann ich nicht auf die Identitätsdiagramm-Seite oder APIs zugreifen?

Ihr Platform-Admin muss Ihnen die `view-identity-graph`-Berechtigung gewähren, damit Sie Identitätsdiagrammdaten anzeigen können. Ohne diese Berechtigung erhalten Sie auf der Anzeigeseite für Identitätsdiagramme und beim Aufrufen von Platform-APIs eine Meldung, dass die Berechtigung verweigert wurde. Weitere Informationen zu Berechtigungen finden Sie in der [Übersicht zur Zugriffskontrolle](../access-control/home.md).

## Fehlerbehebung

Der folgende Abschnitt enthält Empfehlungen zur Fehlerbehebung bei bestimmten Fehler-Codes und unerwarteten Verhaltensweisen, auf die Sie bei der Arbeit mit der [!DNL Identity Service]-API stoßen können.

## [!DNL Identity Service]-Fehlermeldungen

Im Folgenden finden Sie eine Liste von Fehlermeldungen, die bei Verwendung der [!DNL Identity Service]-API auftreten können.

### Erforderlicher Abfrageparameter fehlt

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

Dieser Fehler wird angezeigt, wenn ein erforderlicher Abfrageparameter im Anfragepfad nicht enthalten war. Das `detail` (Detail) der Fehlermeldung enthält den Namen des fehlenden Parameters. Zu den Varianten dieser Fehlermeldung zählen:

- Erforderlicher Abfrageparameter fehlt – nsId
- Erforderlicher Abfrageparameter fehlt – id
- Erforderlicher Abfrageparameter fehlt – xid oder (nsid,id)
- Erforderlicher Abfrageparameter fehlt – targetNs
- Erforderlicher Abfrageparameter fehlt – xids oder compositeXids

Vergewissern Sie sich, dass Sie den angegebenen Parameter im Anfragepfad ordnungsgemäß eingeschlossen haben, bevor Sie es erneut versuchen.

### Der Zeitstempel muss aus den letzten 180 Tagen stammen.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] bereinigt Daten, die älter als 180 Tage sind. Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, auf ältere Daten zuzugreifen.

### Es gilt eine Beschränkung von 1.000 XIDs in einem einzelnen Aufruf.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, Identitätsdaten für mehr als die Zahl von [XIDs](#what-are-composite-identities-and-xids) abzurufen, die in einem einzelnen API-Aufruf maximal zulässig sind. Verringern Sie die Zahl der XIDs in Ihrer Anfrage unter die angegebene Grenze, um das Problem zu beheben.


### Es gilt eine Beschränkung von 1.000 compositeXids in einem einzelnen Aufruf.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

Diese Fehlermeldung wird angezeigt, wenn Sie versuchen, Identitätsdaten für mehr als die Zahl [zusammengesetzter Identitäten](#what-are-composite-identities-and-xids) abzurufen, die in einem einzelnen API-Aufruf zulässig sind. Verringern Sie die Zahl der zusammengesetzten Identitäten in Ihrer Anfrage unter die angegebene Grenze, um das Problem zu beheben.

### Der angegebene Diagrammtyp ist ungültig.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

Diese Fehlermeldung wird angezeigt, wenn einem `graph-type`-Abfrageparameter im Anfragepfad ein ungültiger Wert zugewiesen wird. Im Abschnitt über [Identitätsdiagramme](./home.md) in der [!DNL Identity Service]-Übersicht erfahren Sie, welche Diagrammtypen unterstützt werden.

### Service-Token hat keinen gültigen Umfang.

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

Diese Fehlermeldung wird angezeigt, wenn Ihre IMS-Organisation nicht über die erforderlichen Berechtigungen für [!DNL Identity Service] verfügt. Wenden Sie sich an Ihren Systemadministrator, um das Problem zu beheben.

### Dienst-Token von Gateway ist ungültig.

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

Bei diesem Fehler ist Ihr Zugriffstoken ungültig. Zugriffstoken laufen alle 24 Stunden ab und müssen neu generiert werden, damit Sie [!DNL Platform]-APIs weiterverwenden können. Anweisungen zum Generieren neuer Zugriffstoken finden Sie im [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de).

### Token für Autorisierungsdienst ist ungültig.

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

Bei diesem Fehler ist Ihr Zugriffstoken ungültig. Zugriffstoken laufen alle 24 Stunden ab und müssen neu generiert werden, damit Sie [!DNL Platform]-APIs weiterverwenden können. Anweisungen zum Generieren neuer Zugriffstoken finden Sie im [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de).

### Anwender-Token weist keinen gültigen Produktkontext auf.

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

Diese Fehlermeldung wird angezeigt, wenn Ihr Zugriffstoken nicht von einer [!DNL Experience Platform]-Integration generiert wurde. Anweisungen zum Generieren neuer Zugriffstoken für eine [!DNL Experience Platform]-Integration finden Sie im [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de).

### Interner Fehler beim Abrufen der nativen XID aus dem Identitäts- und Namespace-Code.

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

Wenn [!DNL Identity Service] eine Identität beibehält, wird der Kennung der Identität und der Kennung des zugehörigen Namespace eine eindeutige Kennung zugewiesen, die als XID bezeichnet wird. Diese Meldung wird angezeigt, wenn bei der Suche nach einer XID für einen angegebenen ID-Wert und Namespace ein Fehler auftritt.

### Die IMS-Organisation ist nicht für die Nutzung von [!DNL Identity Service] vorgesehen.

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

Diese Fehlermeldung wird angezeigt, wenn Ihre IMS-Organisation nicht über die erforderlichen Berechtigungen für [!DNL Identity Service] verfügt. Wenden Sie sich an Ihren Systemadministrator, um das Problem zu beheben.

### Interner Server-Fehler

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

Dieser Fehler wird angezeigt, wenn bei Ausführung eines [!DNL Platform]-Service-Aufrufs eine unerwartete Ausnahme auftritt. Es empfiehlt sich, automatisierte Aufrufe so zu programmieren, dass sie bei Erhalt dieses Fehlers Anfragen in einem bestimmten Zeitintervall mehrfach wiederholen. Wenn das Problem fortbesteht, wenden Sie sich an Ihren Systemadministrator.

## Fehler-Codes zur Batch-Erfassung

[!DNL Identity Service] nimmt Identitätsdaten aus Datensatz- und Zeitreihendaten auf, die mithilfe einer Batch-Aufnahme in [!DNL Platform] hochgeladen werden. Da die Batch-Erfassung ein asynchroner Vorgang ist, müssen Sie die Details für einen Batch anzeigen, um Fehler zu prüfen. Während der Batch-Verarbeitung werden Fehler gesammelt, bis der Batch abgeschlossen ist.

Im Folgenden finden Sie eine Liste von Fehlermeldungen im Zusammenhang mit [!DNL Identity Service] Sie können bei der Verwendung von [Batch-Aufnahme-API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).

### Unbekanntes XDM-Schema

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] nutzt nur Identitäten für Datensatz- oder Zeitreihendaten, die den [!DNL Profile]- bzw. [!DNL ExperienceEvent]-Klassen entsprechen. Der Versuch, Daten für [!DNL Identity Service] aufzunehmen, die keiner der beiden Klassen angehören, löst diesen Fehler aus.

### Es gab 0 gültige Identitäten in den ersten 100 Zeilen des verarbeiteten Batch.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

Dieser Fehler wird angezeigt, wenn die ersten 100 Zeilen eines Batch keine Identitäten aufweisen. Dieser Fehler bedeutet jedoch nicht unbedingt, dass in den nachfolgenden Einträgen keine Identitäten gefunden wurden.

### Einträge übersprungen, da sie nur eine Identität pro XDM-Eintrag aufwiesen.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] verknüpft Identitäten nur dann, wenn einzelne Einträge zwei oder mehr Identitätswerte beinhalten. Diese Fehlermeldung wird bei jedem erfassten Batch einmal angezeigt und gibt die Zahl der Einträge an, in denen nur eine Identität gefunden wurde und keine Änderungen am Identitätsdiagramm vorgenommen wurden.

### Namespace-Code für diese IMS-Organisation ist nicht registriert.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

Dieser Fehler wird angezeigt, wenn ein erfasster Eintrag eine Identität enthält, deren verknüpfter Namespace nicht vorhanden ist oder für Ihre IMS-Organisation nicht zugänglich ist.

### Batch-Erfassung wird übersprungen, da für das private Identitätsdiagramm keine IMS-Organisation angegeben wurde.

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

Beim Aufnehmen von Batch-Daten wird diese Fehlermeldung angezeigt, wenn Ihre IMS-Organisation nicht über die erforderlichen Berechtigungen für [!DNL Identity Service] verfügt. Wenden Sie sich an Ihren Systemadministrator, um das Problem zu beheben.

### Interner Fehler

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

Dieser Fehler wird angezeigt, wenn bei der Batch-Erfassung eine unerwartete Ausnahme auftritt. Es empfiehlt sich, automatisierte Aufrufe so zu programmieren, dass sie bei Erhalt dieses Fehlers Anfragen in einem bestimmten Zeitintervall mehrfach wiederholen. Wenn das Problem fortbesteht, wenden Sie sich an Ihren Systemadministrator.
