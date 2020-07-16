---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Marketing-Aktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 3%

---


# Marketing-Aktionen

A marketing action, in the context of the Adobe Experience Platform [!DNL Data Governance], is an action that an [!DNL Experience Platform] data consumer takes, for which there is a need to check for violations of data usage policies.

Zum Arbeiten mit Marketingaktionen in der API müssen Sie den `/marketingActions` Endpunkt verwenden.

## Liste aller Marketingaktionen

To view a list of all marketing actions, a GET request can be made to `/marketingActions/core` or `/marketingActions/custom` that returns all policies for the specified container.

**API-Format**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Anfrage**

Die folgende Anforderung gibt eine Liste aller benutzerdefinierten Marketingaktionen zurück, die von der IMS-Organisation definiert wurden.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Das Antwortobjekt stellt die Gesamtanzahl der Marketingaktionen im Container (`count`) bereit und das `children` Array enthält die Details zu jeder Marketingaktion, einschließlich der `name` und einer `href` für die Marketingaktion. Dieser Pfad (`_links.self.href`) wird verwendet, um das `marketingActionsRefs` Array beim [Erstellen einer Datenverwendungsrichtlinie](policies.md#create-policy)abzuschließen.

```JSON
{
    "_page": {
        "start": "sampleMarketingAction",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550714012088,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714012088,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550793833224,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550793833224,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

## Suchen Sie nach einer bestimmten Marketingaktion

Sie können auch eine GET-Anforderung (Lookup) ausführen, um die Details einer bestimmten Marketingaktion Ansicht. Dies geschieht mithilfe `name` der Marketingaktion. Wenn der Name unbekannt ist, kann er mithilfe der zuvor angezeigten Liste (GET) gefunden werden.

**API-Format**

```http
GET /marketingActions/core/{marketingActionName}
GET /marketingActions/custom/{marketingActionName}
```

**Anfrage**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Das Antwortobjekt enthält die Details zur Marketingaktion, einschließlich des Pfads (`_links.self.href`), der zum Verweisen auf die Marketingaktion beim Definieren einer Datenverwendungsrichtlinie (`marketingActionsRefs`) erforderlich ist.

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{IMS_ORG}",
    "created": 1550793805590,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550793805590,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
        }
    }
}
```

## Erstellen oder Aktualisieren einer Marketingaktion

Mit der [!DNL Policy Service] API können Sie Ihre eigenen Marketingaktionen definieren und bestehende aktualisieren. Die Erstellung und Aktualisierung erfolgt jeweils mit einem PUT-Vorgang zum Namen der Marketingaktion.

**API-Format**

```http
PUT /marketingActions/custom/{marketingActionName}
```

**Anfrage**

Beachten Sie in der folgenden Anforderung, dass die `name` in der Anforderungs-Nutzlast mit der `{marketingActionName}` im API-Aufruf identisch ist. Anders als bei `id` einer Richtlinie, die schreibgeschützt und systemgeneriert ist, müssen Sie bei der Erstellung einer Marketingaktion den _beabsichtigten_ Namen der Marketingaktion angeben.

>[!NOTE]
>
>Wenn Sie den `{marketingActionName}` im Aufruf nicht angeben, wird ein Fehler von 405 ausgegeben (Methode nicht zulässig), da es Ihnen nicht gestattet ist, direkt eine PUT zum `/marketingActions/custom` Endpunkt durchzuführen. Wenn die `name` in der Nutzlast nicht mit der `{marketingActionName}` im Pfad übereinstimmt, erhalten Sie einen 400-Fehler (Fehlerhafte Anforderung).

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

**Antwort**

Bei erfolgreicher Erstellung erhalten Sie einen HTTP-Status 201 (Erstellt) und der Antworttext enthält die Details der neu erstellten Marketingaktion. The `name` in the response should match what was sent in the request.

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{IMS_ORG}",
    "created": 1550713341915,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550713856390,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
        }
    }
}
```

## Löschen einer Marketingaktion

Sie können Marketingaktionen löschen, indem Sie eine DELETE-Anfrage an die Stelle `{marketingActionName}` der Marketingaktion senden, die Sie entfernen möchten.

>[!NOTE]
>
>Sie können keine Marketingaktionen löschen, auf die durch vorhandene Richtlinien verwiesen wird. Der Versuch, dies zu tun, führt zu einem 400-Fehler (Fehlerhafte Anforderung) zusammen mit einer Fehlermeldung, die die `id` (oder mehrere IDs) einer Richtlinie (oder Richtlinien) enthält, die einen Verweis auf die Marketingaktion enthält, die Sie löschen möchten.

**API-Format**

```http
DELETE /marketingActions/custom/{marketingActionName}
```

**Anfrage**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Wenn die Marketingaktion erfolgreich gelöscht wurde, ist der Antworttext mit einem HTTP-Status 200 (OK) leer.

Sie können den Löschvorgang bestätigen, indem Sie versuchen, die Marketingaktion nachzuschlagen (GET). Sie sollten einen HTTP-Status 404 (Nicht gefunden) zusammen mit einer Fehlermeldung &quot;Nicht gefunden&quot;erhalten, da die Marketingaktion entfernt wurde.
