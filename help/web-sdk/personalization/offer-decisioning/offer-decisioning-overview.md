---
title: Verwenden von Offer Decisioning mit dem Experience Platform Web SDK
description: Die Adobe Experience Platform Web SDK kann personalisierte Angebote bereitstellen und rendern, die in Offer Decisioning verwaltet werden. Sie können Ihre Angebote und andere verwandte Objekte mithilfe der Offer Decisioning-Benutzeroberfläche oder -API erstellen.
keywords: Offer Decisioning;Entscheidungsfindung;Web SDK;Experience Platform Web SDK;personalisierte Angebote;Angebote bereitstellen;Angebotsbereitstellung;Personalisierung von Angeboten;
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 8%

---

# Verwenden von Offer Decisioning mit dem Experience Platform Web SDK

Adobe Experience Platform [!DNL Web SDK] kann personalisierte Angebote bereitstellen und rendern, die in Offer Decisioning verwaltet werden. Sie können Ihre Angebote und andere verwandte Objekte mithilfe der Offer Decisioning-Benutzeroberfläche oder von APIs erstellen.

## Voraussetzungen

* Organisation ist für Edge Decisioning aktiviert
* Erstellte Angebote und Aktivitäten
* Datenstrom wird veröffentlicht

## Terminologie

Bei der Arbeit mit Offer Decisioning ist es wichtig, die folgende Terminologie zu verstehen. Weitere Informationen und zusätzliche Begriffe finden Sie im [Offer Decisioning-Glossar](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html?lang=de).

* **Entscheidungsumfänge:** Für Offer Decisioning sind Entscheidungsumfänge die Base64-kodierten JSON-Zeichenfolgen, die die Aktivitäts- und Platzierungs-IDs enthalten, die der Offer Decisioning-Service zum Unterbreiten von Angeboten verwenden soll.

  *Entscheidungsumfang JSON:*

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
  >Sie können den Wert des Entscheidungsumfangs von der Seite **Aktivitätsübersicht** in der Benutzeroberfläche kopieren.

  ![Einstellungen für Entscheidungskopien.](assets/decision-scope-copy.png)

* **Datenströme:** Weitere Informationen finden Sie in der Dokumentation [Datenströme](/help/datastreams/overview.md).

* **Identität**: Weitere Informationen dazu, wie [Experience Platform Web SDK Identity Service verwendet, finden Sie in dieser Dokumentation](../../identity/overview.md).

## Aktivieren von Offer Decisioning

Um Offer Decisioning zu aktivieren, führen Sie die folgenden Schritte aus:

1. Adobe Experience Platform in Ihrem [Datenstrom“ aktiviert &#x200B;](/help/datastreams/overview.md) das Kontrollkästchen &quot;Offer Decisioning&quot; aktiviert

   ![offer-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)

1. Befolgen Sie die Anweisungen zum [Installieren des SDK](/help/web-sdk/install/overview.md) (SDK kann eigenständig oder über die Benutzeroberfläche installiert werden. Weitere Informationen finden Sie [&#x200B; Tags-Schnellstartanleitung &#x200B;](/help/tags/quick-start/quick-start.md).
1. Konfigurieren Sie die SDK für Offer Decisioning mithilfe von `personalization.decisionScopes`. Weitere Offer Decisioning-spezifische Schritte sind unten aufgeführt.

   * Installieren des eigenständigen SDKS

      1. Konfigurieren der Aktion „sendEvent“ mit `personalization.decisionScopes`

     ```javascript
     alloy("sendEvent", {
       ...
       "personalization": {
         "decisionScopes": [
           "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
           "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
         ]
       }
     });
     ```

   * Installieren von SDK über Tags

      1. [Erstellen einer Tag-Eigenschaft](/help/tags/ui/administration/companies-and-properties.md)
      1. [Fügen Sie den Einbettungs-Code hinzu](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html?lang=de)
      1. Installieren und konfigurieren Sie die Experience Platform Web SDK-Erweiterung mit dem von Ihnen erstellten Datenstrom, indem Sie die Konfiguration aus der Dropdown-Liste „Datenstrom“ auswählen. Weitere Informationen zu Datensätzen finden Sie in der Dokumentation zu [Erweiterungen](/help/tags/ui/managing-resources/extensions/overview.md).

         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)

      1. Erstellen Sie die erforderlichen [Datenelemente](/help/tags/ui/managing-resources/data-elements.md). Sie müssen zumindest eine Experience Platform Web SDK Identity Map und ein Experience Platform Web SDK XDM Object-Datenelement erstellen.

         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)

      1. Erstellen Sie Ihre [Regeln](/help/tags/ui/managing-resources/rules.md).

         * Fügen Sie eine Experience Platform Web SDK Send Event-Aktion hinzu und fügen Sie der Konfiguration dieser Aktion die entsprechenden `decisionScopes` hinzu

         ![send-event-action-decisionScopes](./assets/send-event-action-decisionScopes.png)

      1. [Erstellen und veröffentlichen Sie eine &#x200B;](/help/tags/ui/publishing/libraries.md) mit allen relevanten Regeln, Datenelementen und Erweiterungen, die Sie konfiguriert haben

## Beispielanfragen und -antworten

### Ein `decisionScopes`

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
| `identityMap` | Ja | Weitere Informationen finden Sie [Identity Service-Dokumentation](../../identity/overview.md). | Eine Identität pro Anfrage. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Hinweis: Benutzer müssen den `ECID` nicht in den API-Aufruf einbeziehen. Dieser Parameter wird dem Aufruf bei Bedarf automatisch hinzugefügt. |
| `decisionScopes` | Ja | Ein Array von Base64-codierten JSON-Zeichenfolgen, das die Aktivitäts- und Platzierungs-IDs enthält. | Maximal 30 `decisionScopes` pro Anfrage. | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

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
| `scope` | Der Entscheidungsumfang, der zu den vorgeschlagenen Angeboten geführt hat. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | Die eindeutige ID der Angebotsaktivität. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | Die eindeutige ID der Angebotsplatzierung. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | Die ID des vorgeschlagenen Angebots. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Das Schema des Inhalts, der mit dem vorgeschlagenen Angebot verknüpft ist. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | Die ID des vorgeschlagenen Angebots. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | Das Format des Inhalts, der mit dem vorgeschlagenen Angebot verknüpft ist. | `"format": "text/html"` |
| `language` | Eine Reihe von Sprachen, die mit dem Inhalt des vorgeschlagenen Angebots verknüpft sind. | `"language": [ "en-US" ]` |
| `content` | Dem vorgeschlagenen Angebot im Zeichenfolgenformat entsprechender Inhalt | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Bildinhalt im Zusammenhang mit dem vorgeschlagenen Angebot im Format einer URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Merkmale, die mit dem vorgeschlagenen Angebot im Format eines JSON-Objekts verknüpft sind. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### Mehrere `decisionScopes`

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
| `identityMap` | Ja | Weitere Informationen finden Sie [Identity Service-Dokumentation](../../identity/overview.md). | Eine Identität pro Anfrage. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Hinweis: Benutzer müssen den `ECID` nicht in den API-Aufruf einbeziehen. Dieser Parameter wird dem Aufruf bei Bedarf automatisch hinzugefügt. |
| `decisionScopes` | Ja | Ein Array von Base64-codierten JSON-Zeichenfolgen, das die Aktivitäts- und Platzierungs-IDs enthält. | Maximal 30 `decisionScopes` pro Anfrage. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

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
| `scope` | Der Entscheidungsumfang, der zu den vorgeschlagenen Angeboten geführt hat. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | Die eindeutige ID der Angebotsaktivität. | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | Die eindeutige ID der Angebotsplatzierung. | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | Die ID des vorgeschlagenen Angebots. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | Das Schema des Inhalts, der mit dem vorgeschlagenen Angebot verknüpft ist. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | Die ID des vorgeschlagenen Angebots. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | Das Format des Inhalts, der mit dem vorgeschlagenen Angebot verknüpft ist. | `"format": "text/text"` |
| `language` | Eine Reihe von Sprachen, die mit dem Inhalt des vorgeschlagenen Angebots verknüpft sind. | `"language": [ "en-US" ]` |
| `content` | Dem vorgeschlagenen Angebot im Zeichenfolgenformat entsprechender Inhalt | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Bildinhalt im Zusammenhang mit dem vorgeschlagenen Angebot im Format einer URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Merkmale, die mit dem vorgeschlagenen Angebot im Format eines JSON-Objekts verknüpft sind. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

## Einschränkungen

Einige Angebotsbeschränkungen werden derzeit nicht mit den mobilen Edge Network-Workflows unterstützt, z. B. die Begrenzung. Der Wert des Feldes „Begrenzung“ gibt an, wie oft ein Angebot allen Benutzern angezeigt werden kann. Weitere Informationen finden Sie in der [Dokumentation zu Angebotseignungsregeln und Einschränkungen](https://experienceleague.adobe.com/docs/offer-decisioning/using/managing-offers-in-the-offer-library/creating-personalized-offers.html?lang=de#eligibility).
