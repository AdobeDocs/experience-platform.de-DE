---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über die Adobe Privacy JavaScript Library
topic: overview
translation-type: tm+mt
source-git-commit: 3b916ac5529db6ca383bf8bad56961bb1b8a0b0c
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 5%

---


# Übersicht über die Adobe Privacy JavaScript Library

Als Datenverarbeiter verarbeitet Adobe personenbezogene Daten gemäß den Anweisungen und Genehmigungen Ihrer Firma. Als Datenverantwortlicher legen Sie fest, welche personenbezogenen Daten Adobe in Ihrem Namen verarbeitet und speichert. Je nach den Informationen, die Sie über Adobe Experience Cloud-Lösungen senden, kann Adobe private Informationen speichern, die für Datenschutzbestimmungen wie die Allgemeine Datenschutzverordnung (GDPR) und das California Consumer Privacy Act (CCPA) gelten. Weitere Informationen zur Datenerfassung durch Experience Cloud-Lösungen finden Sie im Dokument zum [Datenschutz in Adobe Experience Cloud](https://www.adobe.com/de/privacy/marketing-cloud.html) .

Die JavaScript-Bibliothek **zum Schutz der Privatsphäre in** Adobe ermöglicht es Datenverarbeitungs-Controllern, den Abruf aller von Experience Cloud-Lösungen generierten Identitäten der betroffenen Personen für eine bestimmte Domäne zu automatisieren. Mithilfe der vom [Adobe Experience Platform Privacy Service](home.md)bereitgestellten API können diese Identitäten dann zum Erstellen und Löschen von Anforderungen für private Daten dieser betroffenen Personen verwendet werden.

>[!NOTE] Die JS-Datenschutzbibliothek muss in der Regel nur auf datenschutzrelevanten Seiten installiert werden und muss nicht auf allen Seiten einer Website oder Domäne installiert werden.

## Funktionen

Die Privacy JS Library bietet verschiedene Funktionen zum Verwalten von Identitäten im Datenschutzdienst. Diese Funktionen können nur zur Verwaltung der Identitäten verwendet werden, die im Browser für einen bestimmten Besucher gespeichert werden. Sie können nicht verwendet werden, um Informationen direkt an den Experience Cloud Central-Dienst zu senden.

In der folgenden Tabelle sind die verschiedenen Funktionen der Bibliothek aufgeführt:

| Funktion | Beschreibung |
| --- | --- |
| `retrieveIdentities` | Gibt ein Array mit übereinstimmenden Identitäten (`validIds`) zurück, die vom Datenschutzdienst abgerufen wurden, sowie ein Array mit nicht gefundenen Identitäten (`failedIds`). |
| `removeIdentities` | Entfernt jede übereinstimmende (gültige) Identität aus dem Browser. Gibt ein Array mit übereinstimmenden Identitäten (`validIds`) zurück, wobei jede Identität einen `isDeleteClientSide` booleschen Wert enthält, der angibt, ob diese ID gelöscht wurde. |
| `retrieveThenRemoveIdentities` | Ruft ein Array mit übereinstimmenden Identitäten (`validIds`) ab und entfernt diese dann aus dem Browser. Diese Funktion ähnelt zwar der Funktion, `removeIdentities`wird jedoch am besten verwendet, wenn die von Ihnen verwendete Adobe-Lösung eine Zugriffsanfrage erfordert, bevor das Löschen möglich ist (z. B. wenn eine eindeutige ID abgerufen werden muss, bevor sie in einer Löschanforderung bereitgestellt wird). |

>[!NOTE] `removeIdentities` und entfernen Sie `retrieveThenRemoveIdentities` nur Identitäten aus dem Browser für bestimmte Adobe-Lösungen, die diese unterstützen. Adobe Audience Manager löscht beispielsweise nicht die demdex-IDs, die in Drittanbieter-Cookies gespeichert sind, während Adobe Zielgruppe alle Cookies löscht, die ihre IDs speichern.

Da alle drei Funktionen asynchrone Prozesse darstellen, müssen alle abgerufenen Identitäten mit Rückrufen oder Versprechungen behandelt werden.


## Installation

Um Beginn mit der Privacy JS Library ausführen zu können, müssen Sie diese auf Ihrem Computer mit einer der folgenden Methoden installieren:

* Installieren Sie die Software mithilfe von npm, indem Sie den folgenden Befehl ausführen: `npm install @adobe/adobe-privacy`
* Verwenden Sie die Adobe Launch Extension unter dem Namen `AdobePrivacy`
* Von [https://github.com/Adobe-Marketing-Cloud/adobe-privacy herunterladen](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

## Datenschutzbibliothek instanziieren

Alle Apps, die die Datenschutz-JS-Bibliothek verwenden, müssen ein neues `AdobePrivacy` Objekt instanziieren, das für eine bestimmte Adobe-Lösung konfiguriert werden muss. Eine Instanziierung für Adobe Analytics würde beispielsweise wie folgt aussehen:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    key: "{DATA_SUBJECT_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Eine vollständige Liste der unterstützten Parameter für verschiedene Adobe-Lösungen finden Sie im Anhang zu den unterstützten [Adobe-Lösungskonfigurationsparametern](#adobe-solution-configuration-parameters).

## Codebeispiele

Die folgenden Codebeispiele zeigen, wie Sie die Datenschutz-JS-Bibliothek für verschiedene gängige Szenarien verwenden, sofern Sie nicht Launch oder DTM verwenden.

### Identitäten abrufen

Dieses Beispiel zeigt, wie eine Liste von Identitäten aus Experience Cloud abgerufen wird.

#### JavaScript

Der folgende Code definiert eine Funktion, `handleRetrievedIDs`die als Rückruf oder Versprechen zur Verarbeitung der von `retrieveIdentities`Ihnen abgerufenen Identitäten verwendet wird.

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
| `validIds` | Ein JSON-Objekt, das alle IDs enthält, die erfolgreich abgerufen wurden. |
| `failedIDs` | Ein JSON-Objekt, das alle IDs enthält, die nicht vom Datenschutzdienst abgerufen wurden oder anderweitig nicht gefunden werden konnten. |

#### Ergebnis

Wird der Code erfolgreich ausgeführt, `validIDs` wird eine Liste der abgerufenen Identitäten angezeigt.

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

Dieses Beispiel zeigt, wie eine Liste von Identitäten aus dem Browser entfernt wird.

#### JavaScript

Der folgende Code definiert eine Funktion, `handleRemovedIDs`die als Rückruf oder Versprechen zur Verarbeitung der Identitäten verwendet werden soll, die vom Browser abgerufen `removeIdentities` wurden.

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
| `validIds` | Ein JSON-Objekt, das alle IDs enthält, die erfolgreich abgerufen wurden. |
| `failedIDs` | Ein JSON-Objekt, das alle IDs enthält, die nicht vom Datenschutzdienst abgerufen wurden oder anderweitig nicht gefunden werden konnten. |

#### Ergebnis

Wird der Code erfolgreich ausgeführt, `validIDs` wird eine Liste der abgerufenen Identitäten angezeigt.

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

Durch das Lesen dieses Dokuments wurden Sie mit den Kernfunktionen der Privacy JS Library vertraut gemacht. Nachdem Sie die Bibliothek zum Abrufen einer Liste von Identitäten verwendet haben, können Sie mit diesen Identitäten Datenzugriff erstellen und Anforderungen an die Datenschutzdienst-API löschen. Weitere Informationen finden Sie im Entwicklerhandbuch für den [Datenschutzdienst](api/getting-started.md) .

## Anhang

Dieser Abschnitt enthält zusätzliche Informationen zur Verwendung der Privacy JS Library.

### Konfigurationsparameter für Adobe-Lösungen

Im Folgenden finden Sie eine Liste der zulässigen Konfigurationsparameter für unterstützte Adobe-Lösungen, die beim [Instanziieren eines AdobePrivacy-Objekts](#instantiate-the-privacy-js-library)verwendet werden.

**Adobe Analytics**

| Parameter | Beschreibung |
| --- | --- |
| `cookieDomainPeriods` | Die Zahlenräume in einer Domäne für die Cookie-Verfolgung (Standard ist 2). |
| `dataCenter` | Adobe Datenerfassungsdatencenter. Dies sollte nur berücksichtigt werden, wenn es im JavaScript-Web-Beacon angegeben ist. Mögliche Werte sind: <ul><li>&quot;d1&quot;: San Jose Rechenzentrum.</li><li>&quot;d2&quot;: Dallas Rechenzentrum.</li></ul> |
| `reportSuite` | Report Suite-ID, wie im JavaScript-Web-Beacon angegeben (z. B. &quot;s_code.js&quot;oder &quot;dtm&quot;). |
| `trackingServer` | Datenerfassungsdomäne (nicht SSL). Dies sollte nur berücksichtigt werden, wenn es im JavaScript-Web-Beacon angegeben ist. |
| `trackingServerSecure` | Datenerfassungsdomäne (SSL). Dies sollte nur berücksichtigt werden, wenn es im JavaScript-Web-Beacon angegeben ist. |
| `visitorNamespace` | Namensraum zur Gruppierung von Besuchern. Dies sollte nur berücksichtigt werden, wenn es im JavaScript-Web-Beacon angegeben ist. |

**Adobe Target**

| Parameter | Beschreibung |
| --- | --- |
| `clientCode` | Client-Code, der einen Client im Adobe Zielgruppe System identifiziert. |

**Adobe Audience Manager**

| Parameter | Beschreibung |
| --- | --- |
| `aamUUIDCookieName` | Name des Erstanbieter-Cookies mit der eindeutigen Benutzer-ID, die von Adobe Audience Manager zurückgegeben wird. |

**Adobe ID-Dienst (ECID)**

| Parameter | Beschreibung |
| --- | --- |
| `imsOrgID` | Ihre IMS-Organisations-ID. |