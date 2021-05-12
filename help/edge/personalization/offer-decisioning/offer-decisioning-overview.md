---
title: Verwenden von Offer decisioning mit dem Platform Web SDK
description: Das Adobe Experience Platform Web SDK kann personalisierte Angebot bereitstellen und rendern, die in Offer decisioning verwaltet werden. Sie können Ihre Angebot und andere zugehörige Objekte mithilfe der Offer decisioning-Benutzeroberfläche oder -API erstellen.
keywords: offer decisioning;Entscheidungsfindung;Web-SDK;Plattform-Web-SDK;personalisierte Angebot;Angebote bereitstellen;Angebot-Versand;Angebot-Personalisierung;
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: 20adb26fbd55302ac8005978968a0d69bdda8755
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 16%

---

# Verwenden von Offer decisioning mit dem Platform Web SDK

>[!NOTE]
>
>Ausgewählten Benutzern wird derzeit vorab Zugriff auf die Verwendung von Offer Decisioning im Adobe Experience Platform Web SDK gewährt. Diese Funktion ist nicht für alle IMS-Organisationen verfügbar.

Adobe Experience Platform [!DNL Web SDK] kann personalisierte Angebot bereitstellen und rendern, die in Offer decisioning verwaltet werden. Sie können Ihre Angebot und andere zugehörige Objekte mithilfe der Offer decisioning-Benutzeroberfläche (UI) oder APIs erstellen.

## Voraussetzungen 

* IMS-Organisation für die Edge-Entscheidungsfindung aktiviert
* Angebote, erstellte Aktivitäten
* Datumsformat wird veröffentlicht

## Terminologie

Bei der Arbeit mit Offer decisioning ist es wichtig, die folgende Terminologie zu verstehen. Weitere Informationen und die Ansicht zusätzlicher Begriffe finden Sie im [Offer decisioning-Glossar](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html).

* **Container:** Ein Container ist ein Isolationsmechanismus, der unterschiedliche Anliegen voneinander trennt. Die Container-ID ist das erste Pfadelement für alle Repository-APIs. Alle Entscheidungsobjekte befinden sich in einem Container.

* **Entscheidungsfelder:** Für Offer decisioning sind dies die Base64-kodierten Zeichenfolgen von JSON, die die Aktivität- und Platzierungs-IDs enthalten, die der offer decisioning-Dienst zum Vorschlagen von Angeboten verwenden soll.

   *Entscheidungsbereich JSON:*

   ```json
   {
     "activityId":"xcore:offer-activity:11cfb1fa93381aca",
     "placementId":"xcore:offer-placement:1175009612b0100c"
   }
   ```

   *Entscheidungsumfang Base64-kodierte Zeichenfolge:*

   ```json
   "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
   ```

   >[!TIP]
   >
   >Sie können den Wert für den Entscheidungsbereich auf der Seite **Übersicht über die Aktivität** in der Benutzeroberfläche kopieren.

   ![](assets/decision-scope-copy.png)

* **Datastreams:** Weitere Informationen finden Sie in der  [](../../fundamentals/datastreams.md) Dokumentation zu Datastreams.

* **Identität**: Weitere Informationen finden Sie in dieser Dokumentation, in der erläutert wird, wie  [Platform Web SDK den Identitätsdienst](../../identity/overview.md) nutzt.

## Aktivieren von Offer decisioning

Um Offer decisioning zu aktivieren, müssen Sie die folgenden Schritte ausführen:

1. Adobe Experience Platform in Ihrem [Datastream](../../fundamentals/datastreams.md) aktiviert und das Kontrollkästchen &quot;Offer decisioning&quot;
   ![Angebot-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)
2. Befolgen Sie die Anweisungen zum Installieren des SDK](../../fundamentals/installing-the-sdk.md) (Das SDK kann eigenständig oder über [Adobe Experience Platform Launch](http://launch.adobe.com/de) installiert werden. [ Hier finden Sie eine [Schnellanleitung zum Beginn zu Platform launch](https://docs.adobe.com/content/help/de-DE/launch/using/intro/get-started/quick-start.html)).
3. [Konfigurieren Sie das ](../../fundamentals/configuring-the-sdk.md) SDKfor Offer decisioning. Weitere Offer decisioning-spezifische Schritte finden Sie unten.
   * Eigenständiges installiertes SDK
      1. Konfigurieren Sie die Aktion &quot;sendEvent&quot;mit `decisionScopes`

      ```javascript
      alloy("sendEvent", {
          ...
          "decisionScopes": [
              "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
              "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
          ]
      })
      ```

   * platform launch installiertes SDK
      1. [Erstellen einer Platform launch-Eigenschaft](https://docs.adobe.com/content/help/de-DE/launch/using/reference/admin/companies-and-properties.html)
      2. [hinzufügen des Platform launch-Einbettungscodes](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      3. Installieren und konfigurieren Sie die Platform Web SDK-Erweiterung mit dem soeben erstellten Datastream, indem Sie die Konfiguration aus der Dropdownliste &quot;Datastream&quot;auswählen. Siehe die Dokumentation zu [extensions](https://docs.adobe.com/content/help/de-DE/launch/using/reference/manage-resources/extensions/overview.html).
         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)
      4. Erstellen Sie die erforderlichen [Datenelemente](https://docs.adobe.com/content/help/de-DE/launch/using/reference/manage-resources/data-elements.html). Sie müssen mindestens eine Platform Web SDK Identity Map und ein Platform Web SDK XDM Object-Datenelement erstellen.
         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)
      5. Erstellen Sie die [Regeln](https://docs.adobe.com/content/help/de-DE/launch/using/reference/manage-resources/rules.html).
         * hinzufügen einer Platform Web SDK Send-Ereignis-Aktion und fügen Sie die relevante `decisionScopes` zur Konfiguration dieser Aktion hinzu
            ![send-Ereignis-action-DecisionScopes](./assets/send-event-action-decisionScopes.png)
      6. [Erstellen und veröffentlichen Sie eine ](https://docs.adobe.com/content/help/de-DE/launch/using/reference/publish/libraries.html) Bibliothek, die alle von Ihnen konfigurierten Regeln, Datenelemente und Erweiterungen enthält



## Beispielanforderungen und Antworten

### Ein `decisionScopes`-Wert

**Anfrage**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
          ]
        }
      }
    }
  ]
}
```

| Eigenschaft | Erforderlich | Beschreibung | Beschränkungen | Beispiel |
|---|---|---|---|---|
| `identityMap` | Ja | Weitere Informationen finden Sie in der [Dokumentation zum Identitätsdienst](../../identity/overview.md). | Eine Identität pro Anforderung. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | Ja | Ein Array mit Base64-kodierten Zeichenfolgen von JSON, die die Aktivitäten- und Platzierungs-IDs enthalten. | Maximal 30 `decisionScopes` pro Anforderung. | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

**Antwort**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:124cc332095cfa74",
                "format": "text/html",
                "language": [
                  "en-US"
                ],
                "content": "<p>20% Off on shipping</p>",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| Eigenschaft | Beschreibung | Beispiel |
|---|---|---|
| `scope` | Der Entscheidungsbereich, der zu den vorgeschlagenen Angeboten führte. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | Die eindeutige ID der Angebot-Aktivität. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | Die eindeutige ID der Platzierung des Angebots. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | Die ID des vorgeschlagenen Angebots. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Das Schema des Inhalts des vorgeschlagenen Angebots. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | Die ID des vorgeschlagenen Angebots. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | Das Inhaltsformat, das mit dem vorgeschlagenen Angebot verknüpft ist. | `"format": "text/html"` |
| `language` | Eine Reihe von Sprachen, die mit dem Inhalt des vorgeschlagenen Angebots verknüpft sind. | `"language": [ "en-US" ]` |
| `content` | Mit dem vorgeschlagenen Angebot verknüpfter Inhalt im Format einer Zeichenfolge. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Bildinhalt, der mit dem vorgeschlagenen Angebot im Format einer URL verknüpft ist. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Eigenschaften, die mit dem vorgeschlagenen Angebot im Format eines JSON-Objekts verbunden sind. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### Mehrere `decisionScopes`-Werte

**Anfrage**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyYzkxMzg1Mjc2MDE4YyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMzMxZjU2MTYyYWEyZjcifQ=="
          ]
        }
      }
    }
  ]
}
```

| Eigenschaft | Erforderlich | Beschreibung | Beschränkungen | Beispiel |
|---|---|---|---|---|
| `identityMap` | Ja | Weitere Informationen finden Sie in der [Dokumentation zum Identitätsdienst](../../identity/overview.md). | Eine Identität pro Anforderung. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | Ja | Ein Array mit Base64-kodierten Zeichenfolgen von JSON, die die Aktivitäten- und Platzierungs-IDs enthalten. | Maximal 30 `decisionScopes` pro Anforderung. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

**Antwort**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MTEyMyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDExMjMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381123",
            "etag": "1"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b01123",
            "etag": "3"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a22954123",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-text",
              "etag": "2",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a22954123",
                "format": "text/text",
                "language": [
                  "en"
                ],
                "content": "20% Off on shipping",
                "characteristics": {
                  "foo2": "bar2"
                }
              }
            }
          ]
        },
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a2295415d",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a2295415d",
                "format": "image/png",
                "language": [
                  "en"
                ],
                "deliveryURL": "https://image.jpeg",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| Eigenschaft | Beschreibung | Beispiel |
|---|---|---|
| `scope` | Der Entscheidungsbereich, der zu den vorgeschlagenen Angeboten führte. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | Die eindeutige ID der Angebot-Aktivität. | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | Die eindeutige ID der Platzierung des Angebots. | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | Die ID des vorgeschlagenen Angebots. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | Das Schema des Inhalts des vorgeschlagenen Angebots. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | Die ID des vorgeschlagenen Angebots. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | Das Inhaltsformat, das mit dem vorgeschlagenen Angebot verknüpft ist. | `"format": "text/text"` |
| `language` | Eine Reihe von Sprachen, die mit dem Inhalt des vorgeschlagenen Angebots verknüpft sind. | `"language": [ "en-US" ]` |
| `content` | Mit dem vorgeschlagenen Angebot verknüpfter Inhalt im Format einer Zeichenfolge. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Bildinhalt, der mit dem vorgeschlagenen Angebot im Format einer URL verknüpft ist. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Eigenschaften, die mit dem vorgeschlagenen Angebot im Format eines JSON-Objekts verbunden sind. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
