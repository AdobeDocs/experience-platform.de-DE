---
title: Erfassen von Analysen und Anwenden von Personalisierung in ChatGPT-Apps (MCP-Datenerfassung)
description: Verwenden Sie ein hybrides MCP-Server- und Web-SDK-applyResponse-Muster, um Ereignisse an den Adobe Experience Platform-Edge Network zu senden und in einer Benutzeroberfläche der ChatGPT-App eine Personalisierung zu rendern.
keywords: Adobe Experience Platform, Web SDK, Edge Network, MCP, ChatGPT Apps, applyResponse, Interact Endpoint, Personalisierung, Analytics
source-git-commit: c848f821ea911c82531c6784a17df0116572cd86
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---

# Erfassen von Analysen und Anwenden von Personalisierung in ChatGPT-Apps (MCP-Datenerfassung)

Dieser Anwendungsfall zeigt, wie Sie eine ChatGPT-App (Model Context Protocol Server + optionale UI-Komponenten) mit der Adobe Experience Platform Edge Network verbinden. Diese Art der Datenerfassung ermöglicht es Ihnen, Analysen für Gesprächsinteraktionen aufzuzeichnen, die Ihre Tools aufrufen und Personalisierungsentscheidungen aus der Edge Network in ein von ChatGPT gerendertes Widget liefern.

>[!NOTE]
>
>Dieses Dokument wird auf der Grundlage der neuesten verfügbaren Aktualisierungen sowohl von Adobe-Datenerfassungsteams als auch der neuesten Technologieaktualisierungen von OpenAI gepflegt. Daher geht Adobe davon aus, dass sich dieses Dokument im Laufe der Zeit weiterentwickeln wird, und empfiehlt, nach Updates zu suchen.

In diesem Anwendungsfall wird ein hybrider Ansatz bevorzugt, bei dem sowohl eine Server-seitige Implementierung zum Erfassen von Daten als auch eine Client-seitige Implementierung zum Rendern personalisierter Inhalte verwendet werden. Dieser Ansatz ist ideal, da der Aufruf des MCP-Tools der zuverlässigste Zeitpunkt für die Erfassung von Analysen ist. Das Widget wird im Browser-Kontext ausgeführt und ist der richtige Ort, um Identitäten (in einem Cookie) zu speichern und Personalisierungsentscheidungen anzuwenden.

Dieser Anwendungsfall enthält ein begleitendes voll funktionsfähiges Code-Beispiel. Unter [ChatGPT-App + Adobe Experience Platform Edge](https://github.com/adobe/alloy-samples/tree/main/chatgpt-app) im `alloy-samples`-Repository auf GitHub finden Sie Beispiel-Code und Implementierungsanweisungen.

>[!IMPORTANT]
>
>Auf dieser Seite wird eine Referenzimplementierung beschrieben, die ein Integrationsmuster veranschaulichen soll. Überprüfen Sie die Sicherheits-, Datenschutz-, Einverständnis- und Produktionsanforderungen, bevor Sie den -Ansatz in Ihrer Anwendung anwenden.

## Architektur

Insgesamt gibt es fünf bewegliche Teile:

1. **MCP-Host (ChatGPT)**: ChatGPT ruft Tools auf, die von Ihrem MCP-Server bereitgestellt werden, und stellt eine stabile pseudonyme Benutzerkennung in Anfragemetadaten bereit.
1. **MCP-Server (Backend)**: Ist Eigentum Ihres Unternehmens. Sie implementiert Tools wie das Auflisten von Elementen, das Abrufen von Details oder das Senden von Anfragen.
1. **Adobe IMS**: Gibt Zugriffstoken aus, die von Ihrem MCP-Server zum Aufrufen von Adobe-Datenerfassungs-APIs verwendet werden.
1. **Adobe Experience Platform Edge Network**: Empfängt Erlebnisereignisse, die von Ihrem MCP-Server gesendet werden, und gibt Analytics-Bestätigungen, Statusaktualisierungen (z. B. Identität) und Personalisierungsentscheidungen zurück.
1. **Eingebettete Web-Benutzeroberfläche (Frontend-Widget, das vom MCP-Host gerendert wird)**: Zeigt strukturierte Ergebnisse an und wendet Adobe-Metadaten an, die vom MCP-Server-Backend empfangen wurden.

## Datenfluss

1. **Benutzer** fordert **ChatGPT** mithilfe Ihres MCP-Servers auf.
1. **ChatGPT** interpretiert die Eingabeaufforderungsabsicht und ruft das entsprechende **Backend-MCP-Tool)**.
1. **Backend-MCP-Server** verwendet die Datenerfassungs-APIs (`interact`-Endpunkt), um ein Erlebnisereignis zur Analytics-Erfassung und optionalen Personalisierung an **** Edge Network zu senden.
1. **Edge Network** gibt Antwort-Handles, einschließlich Statusaktualisierungen und Personalisierungsentscheidungen, an das **Backend-MCP-Tool“**.
1. **Backend-MCP-Tool** gibt ein Tool-Ergebnis zurück, das Geschäftsdaten in `structuredContent` und Adobe-Metadaten in `_meta` zu **ChatGPT** enthält.
1. **ChatGPT** stellt das Tool-Ergebnis für das **Frontend-Widget** bereit, das die Geschäftsdaten rendert und die Adobe-Metadaten mithilfe des `applyResponse`-Befehls der Web-SDK-JavaScript-Bibliothek anwendet. Dieser Befehl hydriert den Client-seitigen Status und rendert geeignete Personalisierungsentscheidungen in der Benutzeroberfläche.

In den folgenden Abschnitten werden die einzelnen Schritte im Detail beschrieben.

## Schritt 1: Der Benutzer fordert ChatGPT mithilfe Ihres MCP-Servers auf

Dieser Schritt ist der Einstiegspunkt für den Workflow. Der Benutzer bietet eine natürliche Sprachabsicht:

```text
"Use the Adobe Office Information Tool to show me details about which office that is the most pet-friendly."
```

Weitere Informationen finden [ in der OpenAI](https://developers.openai.com/apps-sdk/build/mcp-server/)Entwicklerdokumentation unter „MCP-Server erstellen“.

## Schritt 2: ChatGPT interpretiert Absicht und ruft ein MCP-Tool auf

Basierend auf den Metadaten Ihres MCP-Servers interpretiert ChatGPT die Absicht und ruft den entsprechenden Tool-Handler auf Ihrem MCP-Server auf. Dieser Tool-Aufruf erstellt einen Server-seitigen Wahrheitspunkt für die Interaktion, der unabhängig vom Rendering-Erfolg der Benutzeroberfläche ist. Eines Ihrer Tools enthält möglicherweise die folgenden Metadaten:

```json
{
  "name": "office_details",
  "description": "Fetch details for a single office by ID and return personalization handles for the UI.",
  "inputSchema": {
    "type": "object",
    "properties": {
      "sessionId": { "type": "string", "description": "Server-issued session identifier." },
      "officeId": { "type": "string", "description": "Office identifier." }
    },
    "required": ["sessionId", "officeId"],
    "additionalProperties": false
  },
  "_meta": {
    "ui": {
      "visibility": ["model", "app"]
    }
  }
}
```

Weitere Informationen [, wie Sie ChatGPT mitteilen, was jedes MCP-Tool tut, finden Sie ](https://developers.openai.com/apps-sdk/plan/tools/) der OpenAI Developers-Dokumentation unter „Tools definieren“.

## Schritt 3: Ihr MCP-Server sendet ein Erlebnisereignis an die Edge Network

Trigger Wenn Ihr MCP-Server eine Anfrage erhält, führt er einen Aufruf an Adobe Experience Platform Edge Network durch, um Analysedaten aufzuzeichnen und optional eine Entscheidungsfindung/Personalisierung anzufordern. Da es sich bei dieser Anfrage um eine Server-zu-Server-Anfrage handelt, verwenden Sie den authentifizierten [`interact`](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/)-Endpunkt als Teil der [Datenerfassungs-APIs](https://developer.adobe.com/data-collection-apis/docs/). Adobe empfiehlt die Verwendung eines [benutzerdefinierten Namespace](https://experienceleague.adobe.com/de/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities), um die eindeutige OpenAI-Kennung weiterzugeben. Stellen Sie sicher, dass der Namespace, den Sie in der Identities-Benutzeroberfläche erstellen, und der Identity-Namespace, den Sie in Ihrem Aufruf definieren, übereinstimmen (Groß-/Kleinschreibung beachten).

```sh
curl -X POST "https://server.adobedc.net/ee/v2/interact?datastreamId={DATASTREAM_ID}"
  -H "Authorization: Bearer {TOKEN}"
  -H "x-gw-ims-org-id: {ORG_ID}"
  -H "x-api-key: {API_KEY}"
  -H "Content-Type: application/json"
  -d '{
    "event": {
      "xdm": {
        "eventType": "office.details.view",
        "identityMap": {
          "{IDENTITY_NAMESPACE}": [
            { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
          ]
        },
        "timestamp": "YYYY-02-20T19:00:00.000Z"
      }
    },
    "query": {
      "personalization": {
        "decisionScopes": ["__view__"]
      }
    },
    "meta": {
      "state": {
        "entries": [
          { "key": "kndctr_orgid_cluster", "value": "{CLUSTER_HINT_IF_KNOWN}" },
          { "key": "kndctr_orgid_identity", "value": "{ECID_BLOB_IF_KNOWN}" }
        ]
      }
    }
  }'
```

## Schritt 4: Edge Network gibt Handles zurück

Wenn der Edge Network Ihren `interact`-Aufruf erhält, antwortet er mit einem `handle` Array. Dieses Array kann je nach Konfiguration Ihres Datenstroms Identitäts- und Personalisierungsentscheidungen enthalten. Eine Beispielantwort könnte wie folgt aussehen:

```json
{
  "requestId": "60a2f...2294d",
  "handle": [
    {
      "type": "locationHint:result",
      "payload": [
        { "scope": "EdgeNetwork", "hint": "or2", "ttlSeconds": 1800 }
      ]
    },
    {
      "type": "state:store",
      "payload": [
        { "key": "kndctr_..._identity", "value": "CiYzM...snTI=", "maxAge": 34128000 },
        { "key": "kndctr_..._cluster", "value": "or2", "maxAge": 1800 }
      ]
    }
  ]
}
```

Ihr MCP-Server kann dann Informationen aus der Edge Network-Antwort extrahieren, um Identitätsinformationen beizubehalten:

```ts
type EdgeHandle = { type: string; payload?: Array<{ key?: string; value?: string }> };

export function extractStateStore(handles: EdgeHandle[]) {
  const store = handles.find(h => h.type === "state:store");
  const entries = store?.payload ?? [];

  const identity = entries.find(e => e.key?.includes("_identity"))?.value;
  const cluster  = entries.find(e => e.key?.includes("_cluster"))?.value;

  return { identity, cluster };
}
```

## Schritt 5: Der MCP-Server gibt die strukturierte Tool-Ausgabe plus Adobe-Metadaten an ChatGPT zurück.

Ihre MCP-Tool-Antwort umfasst sowohl die strukturierte Tool-Ausgabe als auch die Personalisierung aus der Edge Network.

* Das `structuredContent`-Objekt enthält Geschäftsdaten, die ChatGPT sicher lesen und kommentieren kann.
* Das `_meta`-Objekt enthält Adobe-Antwort-Handles und die vom Server berechneten `identityMap`, sodass das Widget sie lesen kann, ohne diese Daten für ChatGPT verfügbar zu machen. Durch die Speicherung dieser Informationen in `_meta.adobe` können Sie konsistent festlegen, wo sich diese Daten befinden. Wenn Sie dieselbe `identityMap` weiterleiten, kann das Widget dieselbe benutzerdefinierte Identität für alle späteren benutzeroberflächenseitigen Ereignisse verwenden.

```json
{
  "content": "Displayed details for office seattle.",
  "structuredContent": {
    "office": {
      "id": "seattle",
      "name": "Seattle",
      "amenities": ["Pet Friendly", "Cafe", "Bike Storage"]
    }
  },
  "_meta": {
    "adobe": {
      "identityMap": {
        "{IDENTITY_NAMESPACE}": [
          { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
        ]
      },
      "handles": [
        {
          "type": "state:store",
          "payload": [
            { "key": "kndctr_..._identity", "value": "..." }
          ]
        },
        {
          "type": "personalization:decisions",
          "payload": [
            { "id": "..." }
          ]
        }
      ]
    }
  }
}
```

Weitere Informationen finden [ unter ](https://developers.openai.com/apps-sdk/reference/#tool-results) in der OpenAI-Entwicklerreferenz .

## Schritt 6: Das Widget rendert das Ergebnis und wendet `_adobe.handles` mithilfe von `applyResponse` an

Das Widget rendert die Geschäftsdaten aus `structuredContent` und liest dann die Adobe-Metadaten aus `_meta.adobe`. In ChatGPT stehen dem Widget dieselben Daten über die Kompatibilitätsebene zur Verfügung:

* `window.openai.toolOutput` enthält `structuredContent`
* `window.openai.toolResponseMetadata` enthält `_meta`

Das Widget verwendet den [`applyResponse`](../../js/commands/applyresponse.md)-Befehl der Web-SDK-JavaScript-Bibliothek, um den Client-seitigen Status einzubinden und Personalisierungsentscheidungen zu rendern, die vom Server-seitigen `interact`-Aufruf zurückgegeben werden. Stellen Sie sicher, dass Sie den [`configure`](../../js/commands/configure/overview.md)-Befehl aufrufen, bevor Sie `applyResponse` aufrufen. Da Ihr MCP-Server einen `interact`-Aufruf ausgeführt hat, müssen Sie den [`sendEvent`](../../js/commands/sendevent/overview.md)-Befehl für die Interaktion des Tool-Aufrufs nicht sofort aufrufen.

```js
// Configure the Web SDK before any other commands.
alloy("configure", {
  datastreamId: "YOUR_DATASTREAM_ID",
  orgId: "YOUR_EXPERIENCE_CLOUD_ORG_ID"
});

// Business data exposed to ChatGPT and the widget.
const { office } = window.openai?.toolOutput ?? {};

// Adobe metadata available only to the widget.
const adobe = window.openai?.toolResponseMetadata?.adobe ?? {};
const { identityMap, handles } = adobe;

// Hydrate client-side state and render personalization decisions from the
// server-side interact response.
alloy("applyResponse", {
  renderDecisions: true,
  responseBody: { handle: handles ?? [] }
});
```

Wenn das Widget später zusätzliche benutzeroberflächenseitige Ereignisse sendet, können Sie dieselben `identityMap` in diese Aufrufe einbeziehen:

```js
alloy("sendEvent", {
  xdm: {
    eventType: "office.details.widgetView",
    identityMap
  }
});
```

Dieses Muster hält die Server-seitige und die UI-seitige Identitätsnutzung in Einklang, während es weiterhin ermöglicht, dass der Server-seitige `interact`-Aufruf die Quelle der Wahrheit für die Analytics-Erfassung und -Entscheidung bleibt.

## Validierung

Sobald alle oben genannten Schritte konfiguriert sind, können Sie Folgendes überprüfen:

* **Datenerfassung:** Überprüfen Sie, ob Ereignisse den gewünschten Datensatz erreichen und ob jedes Ereignis erwartungsgemäß verarbeitet wird.
* **Personalization** Überprüfen Sie, ob Entscheidungen von Edge Network zurückgegeben werden und ob diese Entscheidungen von Ihrem Widget gerendert werden.

## Überlegungen zu Sicherheit und Datenschutz

* Behandeln Sie die Kennungen von ChatGPT als sensibel, auch wenn sie pseudonym sind.
* Stellen Sie sicher, dass Sie die Einverständnis- und Data-Governance-Praktiken Ihrer Organisation auf diesen Workflow anwenden.
* Adobe empfiehlt die Verwendung von OAuth 2.1-Workflows zur Autorisierung.
* Stellen Sie sicher, dass Zugriffstoken und Geheimnisse nie den Client oder die Benutzeroberfläche erreichen.
