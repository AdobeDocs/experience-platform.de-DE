---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Übersicht über die Adobe Privacy JavaScript Library
description: Mit der Adobe Privacy JavaScript Library können Sie die Identität der betroffenen Person zur Verwendung im Privacy Service abrufen.
exl-id: 757bf69e-25bf-4ef9-9787-3e74b213908a
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 55%

---

# Übersicht über die Adobe Privacy JavaScript Library

Als Datenverarbeiter verarbeitet Adobe personenbezogene Daten gemäß den Berechtigungen und Anweisungen Ihres Unternehmens. Als Datenverantwortlicher legen Sie fest, welche personenbezogenen Daten Adobe in Ihrem Namen verarbeitet und speichert. Je nach den Informationen, die Sie über Adobe Experience Cloud-Lösungen senden, kann Adobe private Informationen speichern, die für Datenschutzbestimmungen wie die [!DNL General Data Protection Regulation] (DSGVO) und den [!DNL California Consumer Privacy Act] (CCPA) gelten. Weiterführende Informationen zur Datenerfassung durch Experience Cloud-Lösungen finden Sie im Dokument zum [Datenschutz in Adobe Experience Cloud](https://www.adobe.com/de/privacy/experience-cloud.html).

Mit der **Adobe Privacy JavaScript Library** können Datenverantwortliche den Abruf aller von [!DNL Experience Cloud] Lösungen für eine bestimmte Domain generierten Identitäten von betroffenen Personen automatisieren. Mithilfe der vom [Adobe Experience Platform Privacy Service](home.md) bereitgestellten API können diese Identitäten dann zum Erstellen von Zugriffs- und Löschanfragen für personenbezogene Daten der betroffenen Personen verwendet werden.

>[!NOTE]
>
>Die [!DNL Privacy JS Library] muss in der Regel nur auf datenschutzbezogenen Seiten installiert werden. Sie muss nicht auf allen Seiten einer Website oder Domain installiert werden.

## Funktionen

Die [!DNL Privacy JS Library] bietet mehrere Funktionen zum Verwalten von Identitäten in [!DNL Privacy Service]. Diese Funktionen können nur zur Verwaltung der Identitäten verwendet werden, die im Browser für einen bestimmten Besucher gespeichert sind. Sie können nicht verwendet werden, um Informationen direkt an die [!DNL Experience Cloud Central Service] zu senden.

In der folgenden Tabelle sind die verschiedenen Funktionen der Bibliothek aufgeführt:

| Funktion | Beschreibung |
| --- | --- |
| `retrieveIdentities` | Gibt ein Array von übereinstimmenden Identitäten (`validIds`), die von [!DNL Privacy Service] abgerufen wurden, sowie ein Array von Identitäten zurück, die nicht gefunden wurden (`failedIds`). |
| `removeIdentities` | Entfernt jede übereinstimmende (gültige) Identität aus dem Browser. Gibt eine Gruppe mit übereinstimmenden Identitäten (`validIds`) zurück, wobei jede Identität einen booleschen `isDeletedClientSide`-Wert enthält, der angibt, ob die Kennung gelöscht wurde. |
| `retrieveThenRemoveIdentities` | Ruft eine Gruppe mit übereinstimmenden Identitäten (`validIds`) ab und entfernt diese dann aus dem Browser. Diese Funktion ähnelt zwar `removeIdentities`, eignet sich jedoch am besten, wenn die von Ihnen verwendete Adobe-Lösung eine Zugriffsanfrage erfordert, bevor Löschen möglich ist (wenn z. B. eine eindeutige Kennung abgerufen werden muss, bevor sie in einer Löschanfrage bereitgestellt wurde). |

>[!NOTE]
>
>`removeIdentities` und `retrieveThenRemoveIdentities` entfernen Identitäten nur aus dem Browser für bestimmte Adobe-Lösungen, die sie unterstützen. Adobe Audience Manager löscht beispielsweise keine demdex-Kennungen, die in Drittanbieter-Cookies gespeichert werden, während Adobe Target alle Cookies löscht, die ihre Kennungen speichern.

Da alle drei Funktionen asynchrone Prozesse sind, müssen abgerufene Identitäten mit Callbacks oder Zusagen behandelt werden.


## Installation

Um den [!DNL Privacy JS Library] verwenden zu können, müssen Sie ihn mit einer der folgenden Methoden auf Ihrem Computer installieren:

* Installieren Sie die Software mithilfe von npm, indem Sie den folgenden Befehl ausführen: `npm install @adobe/adobe-privacy`
* Herunterladen aus dem [Experience Cloud-GitHub-Repository](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

Sie können die Bibliothek auch über eine Tag-Erweiterung installieren. Weitere Informationen finden Sie in der Übersicht zur [Adobe-Datenschutz](../tags/extensions/client/privacy/overview.md)Tag-Erweiterung.

## Instanziieren des [!DNL Privacy JS Library]

Alle Apps, die das [!DNL Privacy JS Library] verwenden, müssen ein neues `AdobePrivacy` instanziieren, das für eine bestimmte Adobe-Lösung konfiguriert sein muss. Eine Instanziierung für Adobe Analytics würde beispielsweise wie folgt aussehen:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{ORG_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Eine vollständige Liste der unterstützten Parameter für verschiedene Adobe-Lösungen finden Sie im Anhang zu den unterstützten [Konfigurationsparametern für Adobe-Lösungen](#adobe-solution-configuration-parameters).

## Code-Beispiele {#samples}

In den folgenden Codebeispielen wird veranschaulicht, wie die [!DNL Privacy JS Library] für mehrere gängige Szenarien verwendet wird, sofern Sie keine Tags verwenden.

### Identitäten abrufen

Dieses Beispiel zeigt, wie eine Liste von Identitäten aus [!DNL Experience Cloud] abgerufen wird.

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
| `failedIDs` | Ein JSON-Objekt, das alle IDs enthält, die nicht von [!DNL Privacy Service] abgerufen wurden oder anderweitig nicht gefunden wurden. |

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
| `failedIDs` | Ein JSON-Objekt, das alle IDs enthält, die nicht von [!DNL Privacy Service] abgerufen wurden oder anderweitig nicht gefunden wurden. |

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

In diesem Dokument haben Sie eine Einführung in die Kernfunktionen des [!DNL Privacy JS Library] erhalten. Nachdem Sie die -Bibliothek zum Abrufen einer Liste von Identitäten verwendet haben, können Sie diese Identitäten verwenden, um Datenzugriffs- und Löschanfragen an die [!DNL Privacy Service]-API zu erstellen. Weitere Informationen finden Sie im [Privacy Service ](api/overview.md)API-Handbuch.

## Anhang

Dieser Abschnitt enthält zusätzliche Informationen zur Verwendung des [!DNL Privacy JS Library].

### Konfigurationsparameter für Adobe-Lösungen {#config-params}

Im Folgenden finden Sie eine Liste der zulässigen Konfigurationsparameter für unterstützte Adobe-Lösungen, die beim [Instanziieren eines AdobePrivacy-Objekts](#instantiate-the-privacy-js-library) verwendet werden können.

**Alle Lösungen**

| Parameter | Beschreibung |
| --- | --- |
| `key` | Eine eindeutige ID, die den Benutzer oder die betroffene Person identifiziert. Diese Eigenschaft ist für Ihre eigenen internen Tracking-Zwecke vorgesehen und wird nicht von Adobe verwendet. |

**Adobe Analytics**

| Parameter | Beschreibung |
| --- | --- |
| `cookieDomainPeriods` | Die Anzahl der Punkte in einer Domain, die für das Cookie-Tracking verwendet werden (standardmäßig `2`, z. B. `.domain.com`). Definieren Sie sie hier nur, wenn sie in Ihrem JavaScript-Web-Beacon angegeben ist. |
| `dataCenter` | Das Datenerfassungs-Datenzentrum von Adobe. Dies sollte nur berücksichtigt werden, wenn es im JavaScript-Webbeacon angegeben ist. Mögliche Werte sind: <ul><li>`d1`: Rechenzentrum in San Jose</li><li>`d2`: Rechenzentrum in Dallas</li></ul> |
| `reportSuite` | Die Report Suite-ID, wie in Ihrem JavaScript Web-Beacon angegeben (z. B. `s_code.js` oder `dtm`). |
| `trackingServer` | Eine Nicht-SSL-Datenerfassungsdomäne. Dies sollte nur berücksichtigt werden, wenn es im JavaScript-Webbeacon angegeben ist. |
| `trackingServerSecure` | Eine SSL-Datenerfassungs-Domain. Dies sollte nur berücksichtigt werden, wenn es im JavaScript-Webbeacon angegeben ist. |
| `visitorNamespace` | Der Namespace, der zum Gruppieren von Besuchern verwendet wird. Dies sollte nur berücksichtigt werden, wenn es im JavaScript-Webbeacon angegeben ist. |

**Adobe Audience Manager**

| Parameter | Beschreibung |
| --- | --- |
| `aamUUIDCookieName` | Name des Erstanbieter-Cookies mit der eindeutigen Benutzer-ID, die von Adobe Audience Manager zurückgegeben wird. |

**Adobe Experience Cloud Identity Service (ECID)**

| Parameter | Beschreibung |
| --- | --- |
| `imsOrgID` | Ihre Organisations-ID. |

**Adobe Target**

| Parameter | Beschreibung |
| --- | --- |
| `clientCode` | Client-Code, der einen Client im Adobe Target-System identifiziert. |
