---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Übersicht über die JavaScript-Bibliothek zum Datenschutz in der Adobe
topic-legacy: overview
description: Die Adobe Privacy JavaScript Library ermöglicht das Abrufen von Daten Betreff Identitäten zur Verwendung in Privacy Service.
exl-id: 757bf69e-25bf-4ef9-9787-3e74b213908a
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 66%

---

# Übersicht über die Adobe Privacy JavaScript Library

Als Datenverarbeiter verarbeitet Adobe personenbezogene Daten gemäß den Berechtigungen und Anweisungen Ihres Unternehmens. Als Datenverantwortlicher legen Sie fest, welche personenbezogenen Daten Adobe in Ihrem Namen verarbeitet und speichert. Je nach den Informationen, die Sie über Adobe Experience Cloud-Lösungen versenden, kann die Adobe private Informationen speichern, die für Datenschutzbestimmungen wie die [!DNL General Data Protection Regulation] (GDPR) und [!DNL California Consumer Privacy Act] (CCPA). Weiterführende Informationen zur Datenerfassung durch Experience Cloud-Lösungen finden Sie im Dokument zum [Datenschutz in Adobe Experience Cloud](https://www.adobe.com/de/privacy/experience-cloud.html).

Die **JavaScript Library zum Datenschutz der Adobe** ermöglicht es den Datenkontrolleuren, den Abruf aller von [!DNL Experience Cloud] Lösungen für eine bestimmte Domäne. Mithilfe der vom [Adobe Experience Platform Privacy Service](home.md) bereitgestellten API können diese Identitäten dann zum Erstellen von Zugriffs- und Löschanfragen für personenbezogene Daten der betroffenen Personen verwendet werden.

>[!NOTE]
>
>Die [!DNL Privacy JS Library] In der Regel muss nur auf datenschutzbezogenen Seiten installiert werden und muss nicht auf allen Seiten einer Website oder Domäne installiert werden.

## Funktionen

Die [!DNL Privacy JS Library] bietet mehrere Funktionen zum Verwalten von Identitäten in [!DNL Privacy Service]. Diese Funktionen können nur zur Verwaltung der Identitäten verwendet werden, die im Browser für einen bestimmten Besucher gespeichert sind. Sie können nicht dazu verwendet werden, Informationen an die [!DNL Experience Cloud Central Service] direkt.

In der folgenden Tabelle sind die verschiedenen Funktionen der Bibliothek aufgeführt:

| Funktion | Beschreibung |
| --- | --- |
| `retrieveIdentities` | Gibt ein Array mit übereinstimmenden Identitäten zurück (`validIds`), die abgerufen wurden von [!DNL Privacy Service], sowie eine Reihe von nicht gefundenen Identitäten (`failedIds`). |
| `removeIdentities` | Entfernt jede übereinstimmende (gültige) Identität aus dem Browser. Gibt eine Gruppe mit übereinstimmenden Identitäten (`validIds`) zurück, wobei jede Identität einen booleschen `isDeletedClientSide`-Wert enthält, der angibt, ob die Kennung gelöscht wurde. |
| `retrieveThenRemoveIdentities` | Ruft eine Gruppe mit übereinstimmenden Identitäten (`validIds`) ab und entfernt diese dann aus dem Browser. Diese Funktion ähnelt zwar `removeIdentities`, eignet sich jedoch am besten, wenn die von Ihnen verwendete Adobe-Lösung eine Zugriffsanfrage erfordert, bevor Löschen möglich ist (wenn z. B. eine eindeutige Kennung abgerufen werden muss, bevor sie in einer Löschanfrage bereitgestellt wurde). |

>[!NOTE]
>
>`removeIdentities`  und `retrieveThenRemoveIdentities` entfernen Identitäten aus dem Browser nur bei bestimmten Adobe-Lösungen, die sie unterstützen. Adobe Audience Manager löscht beispielsweise keine demdex-Kennungen, die in Drittanbieter-Cookies gespeichert werden, während Adobe Target alle Cookies löscht, die ihre Kennungen speichern.

Da alle drei Funktionen asynchrone Prozesse sind, müssen abgerufene Identitäten mit Callbacks oder Zusagen behandelt werden.


## Installation

Zum Beginn mit [!DNL Privacy JS Library], müssen Sie es mit einer der folgenden Methoden auf Ihrem Computer installieren:

* Installieren Sie die Software mithilfe von npm, indem Sie den folgenden Befehl ausführen: `npm install @adobe/adobe-privacy`
* Installieren Sie [Adobe-Datenschutztag-Erweiterung](../tags/extensions/web/privacy/overview.md) unter dem Namen `AdobePrivacy`
* Von [Experience Cloud-GitHub-Repository](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

## Instantieren der [!DNL Privacy JS Library]

Alle Apps, die die [!DNL Privacy JS Library] muss eine neue `AdobePrivacy` -Objekt, das auf eine bestimmte Adobe konfiguriert werden muss. Eine Instanziierung für Adobe Analytics würde beispielsweise wie folgt aussehen:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Eine vollständige Liste der unterstützten Parameter für verschiedene Adobe-Lösungen finden Sie im Anhang zu den unterstützten [Konfigurationsparametern für Adobe-Lösungen](#adobe-solution-configuration-parameters).

## Code-Beispiele

Die folgenden Codebeispiele veranschaulichen die Verwendung der [!DNL Privacy JS Library] für mehrere häufige Szenarien, sofern Sie keine Tags verwenden.

### Identitäten abrufen

In diesem Beispiel wird veranschaulicht, wie eine Liste von Identitäten abgerufen wird von [!DNL Experience Cloud].

#### JavaScript

Der folgende Code definiert eine Funktion (`handleRetrievedIDs`), die zur Verarbeitung der von `retrieveIdentities` abgerufenen Identitäten als Callback oder Zusage verwendet wird.

```javascript
function handleRetrievedIDs(ids) {
    const validIDs = ids.validIDs;
    const failedIDs = ids.failedIDs;
}

// If using callbacks:
adobePrivacy.retrieveIdentities(handleRetrievedIDs);

// If using promises:
adobePrivacy.retrieveIdentities().then(handleRetrievedIDs);
```

| Variable | Beschreibung |
| --- | --- |
| `validIds` | Ein JSON-Objekt, das alle Kennungen enthält, die erfolgreich abgerufen wurden. |
| `failedIDs` | Ein JSON-Objekt, das alle IDs enthält, von denen nicht abgerufen wurden [!DNL Privacy Service], oder auf andere Weise nicht gefunden werden konnte. |

#### Ergebnis

Wenn der Code erfolgreich ausgeführt wird, wird `validIDs` mit einer Liste der abgerufenen Identitäten ausgefüllt.

```json
{
    "company": "adobe",
    "namespace": "ECID",
    "namespaceId": 4,
    "type": "standard",
    "name": "Experience Cloud ID",
    "description": "This is the ID generated by the ID Service.",
    "value": "79352169365966186342525781172209986543"
},
{
    "company": "adobe",
    "namespace": "gsurfer_id",
    "namespaceId": 411,
    "type": "standard",
    "value": "WqmIJQAAB669Ciao"
}
```

### Identitäten entfernen

Dieses Beispiel zeigt, wie Sie eine Liste von Identitäten aus dem Browser entfernen.

#### JavaScript

Der folgende Code definiert eine Funktion (`handleRemovedIDs`), die zur Verarbeitung der von `removeIdentities` abgerufenen Identitäten als Callback oder Zusage verwendet wird, nachdem die Identitäten aus dem Browser entfernt wurden.

```javascript
function handleRemovedIDs(ids) {
    const validIDs = ids.validIDs;
    const failedIDs = ids.failedIDs;
}

// If using callbacks:
adobePrivacy.removeIdentities(handleRemovedIDs);

// If using promises:
adobePrivacy.removeIdentities().then(handleRemovedIDs)…
```

| Variable | Beschreibung |
| --- | --- |
| `validIds` | Ein JSON-Objekt, das alle Kennungen enthält, die erfolgreich abgerufen wurden. |
| `failedIDs` | Ein JSON-Objekt, das alle IDs enthält, von denen nicht abgerufen wurden [!DNL Privacy Service], oder auf andere Weise nicht gefunden werden konnte. |

#### Ergebnis

Wenn der Code erfolgreich ausgeführt wird, wird `validIDs` mit einer Liste der abgerufenen Identitäten ausgefüllt.

```json
{
    "company": "adobe",
    "namespace": "ECID",
    "namespaceId": 4,
    "type": "standard",
    "name": "Experience Cloud ID",
    "description": "This is the ID generated by the ID Service.",
    "value": "79352169365966186342525781172209986543",
    "isDeletedClientSide": false
},
{
    "company": "adobe",
    "namespace": "AMO",
    "namespaceId": 411,
    "type": "standard",
    "value": "WqmIJQAAB669Ciao",
    "isDeletedClientSide": true
}
```

## Nächste Schritte

Durch das Lesen dieses Dokuments wurden Sie in die Kernfunktionalitäten der [!DNL Privacy JS Library]. Nachdem Sie die Bibliothek zum Abrufen einer Liste von Identitäten verwendet haben, können Sie mithilfe dieser Identitäten Datenzugriff erstellen und Anforderungen an die [!DNL Privacy Service] API. Siehe [Privacy Service-API-Handbuch](api/overview.md) für weitere Informationen.

## Anhang

Dieser Abschnitt enthält ergänzende Informationen zur Anwendung der [!DNL Privacy JS Library].

### Konfigurationsparameter für Adobe-Lösungen

Im Folgenden finden Sie eine Liste der zulässigen Konfigurationsparameter für unterstützte Adobe-Lösungen, die beim [Instanziieren eines AdobePrivacy-Objekts](#instantiate-the-privacy-js-library) verwendet werden können.

**Adobe Analytics**

| Parameter | Beschreibung |
| --- | --- |
| `cookieDomainPeriods` | Die Zahlenperioden in einer Domain für das Cookie-Tracking (Standard ist 2). |
| `dataCenter` | Adobe-Rechenzentrum für die Datenerfassung. Dies sollte nur berücksichtigt werden, wenn es im JavaScript-Webbeacon angegeben ist. Mögliche Werte sind: <ul><li>„d1“: Rechenzentrum in San Jose.</li><li>„d2“: Rechenzentrum in Dallas.</li></ul> |
| `reportSuite` | Report Suite-ID, wie in Ihrem JavaScript-Webbeacon angegeben (z. B. „s_code.js“ oder „dtm“). |
| `trackingServer` | Datenerfassungs-Domain (nicht SSL). Dies sollte nur berücksichtigt werden, wenn es im JavaScript-Webbeacon angegeben ist. |
| `trackingServerSecure` | Datenerfassungs-Domain (SSL). Dies sollte nur berücksichtigt werden, wenn es im JavaScript-Webbeacon angegeben ist. |
| `visitorNamespace` | Namespace zur Gruppierung von Besuchern. Dies sollte nur berücksichtigt werden, wenn es im JavaScript-Webbeacon angegeben ist. |

**Adobe Target**

| Parameter | Beschreibung |
| --- | --- |
| `clientCode` | Client-Code, der einen Client im Adobe Target-System identifiziert. |

**Adobe Audience Manager**

| Parameter | Beschreibung |
| --- | --- |
| `aamUUIDCookieName` | Name des Erstanbieter-Cookies mit der eindeutigen Benutzer-ID, die von Adobe Audience Manager zurückgegeben wird. |

**Adobe ID Service (ECID)**

| Parameter | Beschreibung |
| --- | --- |
| `imsOrgID` | Die Kennung Ihrer IMS-Organisation. |
