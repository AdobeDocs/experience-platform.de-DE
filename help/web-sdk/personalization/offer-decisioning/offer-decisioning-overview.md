---
title: Verwenden von Offer decisioning mit dem Platform Web SDK
description: Das Adobe Experience Platform Web SDK kann personalisierte Angebote bereitstellen und rendern, die unter Offer decisioning verwaltet werden. Sie können Ihre Angebote und andere verwandte Objekte mithilfe der Offer decisioning-Benutzeroberfläche oder -API erstellen.
keywords: offer decisioning; Entscheidungsfindung; Web SDK; Platform Web SDK; personalisierte Angebote; Angebote bereitstellen; Angebotsversand; Angebotspersonalisierung;
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: 22477c11a977059849d9b47871a5c2aef1da4b24
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 12%

---

# Verwenden von Offer decisioning mit dem Platform Web SDK

>[!NOTE]
>
>Die Verwendung von Offer decisioning im Adobe Experience Platform Web SDK ist für ausgewählte Benutzer in einem frühen Stadium verfügbar. Diese Funktion ist nicht für alle Organisationen verfügbar.

Adobe Experience Platform [!DNL Web SDK] kann personalisierte Angebote bereitstellen und rendern, die in Offer Decisioning verwaltet werden. Sie können Ihre Angebote und andere verwandte Objekte mithilfe der Offer decisioning-Benutzeroberfläche (UI) oder APIs erstellen.

## Voraussetzungen

* Die Organisation ist für die Edge-Entscheidung aktiviert.
* Erstellte Angebote, Aktivitäten
* Datenspeicher wird veröffentlicht

## Terminologie

Bei der Arbeit mit Offer decisioning ist es wichtig, die folgende Terminologie zu verstehen. Weitere Informationen und zusätzliche Begriffe finden Sie im [Offer decisioning-Glossar](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html).

* **Entscheidungsbereiche:** Für Offer decisioning sind Entscheidungsbereiche die Base64-kodierten Zeichenfolgen von JSON, die die Aktivitäts- und Platzierungs-IDs enthalten, die der offer decisioning-Dienst zum Anbieten von Angeboten verwenden soll.

  *Entscheidungsbereich-JSON:*

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
  >Sie können den Wert für den Entscheidungsbereich von der Seite **Aktivitätsübersicht** in der Benutzeroberfläche kopieren.

  ![Einstellungen zum Kopieren von Entscheidungen.](assets/decision-scope-copy.png)

* **Datenspeicher:** Weitere Informationen finden Sie in der Dokumentation zu [datastreams](/help/datastreams/overview.md) .

* **Identität**: Weitere Informationen dazu, wie [Platform Web SDK Identity Service verwendet](../../identity/overview.md), finden Sie in dieser Dokumentation.

## Aktivieren von Offer decisioning

Führen Sie die folgenden Schritte aus, um Offer decisioning zu aktivieren:

1. Adobe Experience Platform in Ihrem [Datastream](/help/datastreams/overview.md) aktiviert und das Kontrollkästchen &quot;Offer decisioning&quot;aktiviert

   ![offer-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)

1. Befolgen Sie die Anweisungen unter [Installieren des SDK](/help/web-sdk/install/overview.md) (Das SDK kann eigenständig oder über die Benutzeroberfläche installiert werden. Weitere Informationen finden Sie in der Schnellstartanleitung ](/help/tags/quick-start/quick-start.md) für [Tags .
1. Konfigurieren Sie das SDK für die Offer decisioning mit `personalization.decisionScopes`. Weitere Offer decisioning-spezifische Schritte finden Sie unten.

   * Installieren des eigenständigen SDK

      1. Konfigurieren der Aktion &quot;sendEvent&quot;mit `personalization.decisionScopes`

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

   * SDK über Tags installieren

      1. [Tag-Eigenschaft erstellen](/help/tags/ui/administration/companies-and-properties.md)
      1. [Fügen Sie den Einbettungs-Code hinzu](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html?lang=de)
      1. Installieren und konfigurieren Sie die Platform Web SDK-Erweiterung mit dem von Ihnen erstellten Datastream, indem Sie die Konfiguration aus der Dropdown-Liste &quot;Datastream&quot;auswählen. Weitere Informationen zu Datensätzen finden Sie in der Dokumentation zu [Erweiterungen](/help/tags/ui/managing-resources/extensions/overview.md).

         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)

      1. Erstellen Sie die erforderlichen [Datenelemente](/help/tags/ui/managing-resources/data-elements.md). Sie müssen zumindest eine Platform Web SDK Identity Map und ein Platform Web SDK XDM Object-Datenelement erstellen.

         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)

      1. Erstellen Sie Ihre [Regeln](/help/tags/ui/managing-resources/rules.md).

         * Fügen Sie die Aktion &quot;Ereignis senden&quot;des Platform Web SDK hinzu und fügen Sie die relevante `decisionScopes` zur Konfiguration dieser Aktion hinzu.

         ![send-event-action-decisionScopes](./assets/send-event-action-decisionScopes.png)

      1. [Erstellen und veröffentlichen Sie eine Bibliothek](/help/tags/ui/publishing/libraries.md), die alle von Ihnen konfigurierten relevanten Regeln, Datenelemente und Erweiterungen enthält.

## Beispielanfragen und -antworten

### Ein `decisionScopes` -Wert

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
| `identityMap` | Ja | Weitere Informationen finden Sie in der Dokumentation zum [Identitätsdienst](../../identity/overview.md) . | Eine Identität pro Anfrage. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Hinweis: Benutzer müssen den Parameter `ECID` nicht in den API-Aufruf einbeziehen. Dieser Parameter wird bei Bedarf automatisch zum -Aufruf hinzugefügt. |
| `decisionScopes` | Ja | Ein Array Base64-kodierter Zeichenfolgen von JSON, die die Aktivitäts- und Platzierungs-IDs enthalten. | Maximal 30 `decisionScopes` pro Anfrage. | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

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
| `activity.id` | Die eindeutige Kennung der Angebotsaktivität. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | Die eindeutige ID der Angebotsplatzierung. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | Die Kennung des vorgeschlagenen Angebots. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Das Schema des dem vorgeschlagenen Angebot zugeordneten Inhalts. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | Die Kennung des vorgeschlagenen Angebots. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | Das Format des mit dem vorgeschlagenen Angebot verknüpften Inhalts. | `"format": "text/html"` |
| `language` | Eine Reihe von Sprachen, die mit dem Inhalt des vorgeschlagenen Angebots verknüpft sind. | `"language": [ "en-US" ]` |
| `content` | Inhalt, der mit dem vorgeschlagenen Angebot in Form einer Zeichenfolge verknüpft ist. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Bildinhalt, der mit dem vorgeschlagenen Angebot verknüpft ist, im Format einer URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Mit dem vorgeschlagenen Angebot verknüpfte Eigenschaften im Format eines JSON-Objekts. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### Mehrere `decisionScopes` Werte

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
| `identityMap` | Ja | Weitere Informationen finden Sie in der Dokumentation zum [Identitätsdienst](../../identity/overview.md) . | Eine Identität pro Anfrage. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Hinweis: Benutzer müssen den Parameter `ECID` nicht in den API-Aufruf einbeziehen. Dieser Parameter wird bei Bedarf automatisch zum -Aufruf hinzugefügt. |
| `decisionScopes` | Ja | Ein Array Base64-kodierter Zeichenfolgen von JSON, die die Aktivitäts- und Platzierungs-IDs enthalten. | Maximal 30 `decisionScopes` pro Anfrage. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

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
| `activity.id` | Die eindeutige Kennung der Angebotsaktivität. | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | Die eindeutige ID der Angebotsplatzierung. | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | Die Kennung des vorgeschlagenen Angebots. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | Das Schema des dem vorgeschlagenen Angebot zugeordneten Inhalts. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | Die Kennung des vorgeschlagenen Angebots. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | Das Format des mit dem vorgeschlagenen Angebot verknüpften Inhalts. | `"format": "text/text"` |
| `language` | Eine Reihe von Sprachen, die mit dem Inhalt des vorgeschlagenen Angebots verknüpft sind. | `"language": [ "en-US" ]` |
| `content` | Inhalt, der mit dem vorgeschlagenen Angebot in Form einer Zeichenfolge verknüpft ist. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Bildinhalt, der mit dem vorgeschlagenen Angebot verknüpft ist, im Format einer URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Mit dem vorgeschlagenen Angebot verknüpfte Eigenschaften im Format eines JSON-Objekts. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

## Einschränkungen

Einige Angebotsbegrenzungen werden derzeit nicht von den mobilen Edge Network-Workflows unterstützt, z. B. Begrenzungen. Der Wert des Feldes „Begrenzung“ gibt an, wie oft ein Angebot allen Benutzern angezeigt werden kann. Weitere Informationen finden Sie in der [Dokumentation zu Angebotseignungsregeln und Einschränkungen](https://experienceleague.adobe.com/docs/offer-decisioning/using/managing-offers-in-the-offer-library/creating-personalized-offers.html#eligibility).
