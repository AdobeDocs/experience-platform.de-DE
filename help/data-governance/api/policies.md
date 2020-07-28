---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Richtlinien
topic: developer guide
translation-type: tm+mt
source-git-commit: d4964231ee957349f666eaf6b0f5729d19c408de
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 92%

---


# Richtlinien

Data usage policies are rules your organization adopts that describe the kinds of marketing actions that you are allowed to, or restricted from, performing on data within [!DNL Experience Platform].

Der `/policies`-Endpunkt wird für alle API-Aufrufe zum Anzeigen, Erstellen, Aktualisieren oder Löschen von Datennutzungsrichtlinien verwendet.

## Liste aller Richtlinien

Um eine Liste von Richtlinien anzuzeigen, kann eine GET-Anfrage an `/policies/core` oder `/policies/custom` gesendet werden, die alle Richtlinien für den angegebenen Container zurückgibt.

**API-Format**

```http
GET /policies/core
GET /policies/custom
```

**Anfrage**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die Antwort enthält eine „Anzahl“, die die Gesamtanzahl der Richtlinien im angegebenen Container sowie die Details der einzelnen Richtlinien einschließlich ihrer `id` anzeigt. Das `id`-Feld wird verwendet, um Suchanfragen zur Ansicht bestimmter Richtlinien sowie Aktualisierungs- und Löschvorgänge durchzuführen.

```JSON
{
    "_page": {
        "start": "5c6dacdf685a4913dc48937c",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/policies/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "Export Data to Third Party",
            "status": "DRAFT",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "OR",
                        "operands": [
                            {
                                "label": "C3"
                            },
                            {
                                "label": "C7"
                            }
                        ]
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1550691551888,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550701472910,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
                }
            },
            "id": "5c6dacdf685a4913dc48937c"
        },
        {
            "name": "Combine Data",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
            ],
            "description": "Data that meets these conditions cannot be combined.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "I1"
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1550703519823,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714340335,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb9f5c404513dc2dc454"
                }
            },
            "id": "5c6ddb9f5c404513dc2dc454"
        }
    ]
}
```

## Eine Richtlinie nachschlagen

Jede Richtlinie enthält ein `id`-Feld, mit dem die Details einer bestimmten Richtlinie angefordert werden können. Wenn die `id` einer Richtlinie unbekannt ist, können Sie sie mithilfe der Auflistungsanfrage (GET) finden, die alle Richtlinien in einem bestimmten Container (`core` oder `custom`) auflistet, wie im vorherigen Schritt gezeigt.

**API-Format**

```http
GET /policies/core/{id}
GET /policies/custom/{id}
```

**Anfrage**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die Antwort enthält die Details der Richtlinie, einschließlich der Schlüsselfelder `id` (dieses Feld sollte mit der in der Anfrage gesendeten `id` übereinstimmen), `name`, `status` und `description`, sowie einen Verweis-Link zur Marketing-Aktion, auf der die Richtlinie basiert (`marketingActionRefs`).

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "C7"
                    }
                ]
            }
        ]
    },
    "imsOrg": "{IMS_ORG}",
    "created": 1550691551888,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Erstellen einer Richtlinie {#create-policy}

Die Erstellung einer Richtlinie erfordert die Einbeziehung einer Marketing-Aktion mit einem Ausdruck der DULE-Bezeichnung, die diese Marketing-Aktion verbieten. Richtliniendefinitionen müssen eine `deny`-Eigenschaft enthalten, bei der es sich um einen booleschen Ausdruck in Bezug auf das Vorhandensein von DULE-Bezeichnungen handelt.

Dieser Ausdruck wird als `PolicyExpression` bezeichnet und ist ein Objekt, das _entweder_ eine Bezeichnung _oder_ einen Operator und Operanden, jedoch nicht beide, enthält. Jeder Operand ist auch ein `PolicyExpression`-Objekt. So könnte beispielsweise eine Richtlinie über den Export von Daten an Dritte verboten werden, wenn `C1 OR (C3 AND C7)`-Bezeichnungen vorhanden sind. Dieser Ausdruck würde wie folgt definiert:

```JSON
"deny": {
  "operator": "OR",
  "operands": [
    {"label": "C1"},
    {
      "operator": "AND",
      "operands": [
        {"label": "C3"},
        {"label": "C7"}
      ]
    }
  ]
}
```

**API-Format**

```http
POST /policies/custom
```

**Anfrage**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "../marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "OR",
          "operands": [
            {"label": "C1"},
            {
              "operator": "AND",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

**Antwort**

Bei erfolgreicher Erstellung erhalten Sie einen HTTP-Status 201 (Erstellt) und der Antworttext enthält die Details der neu erstellten Richtlinie einschließlich ihrer `id`. Dieser Wert ist schreibgeschützt und wird beim Erstellen der Richtlinie automatisch zugewiesen.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "OR",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "C7"
                    }
                ]
            }
        ]
    },
    "imsOrg": "{IMS_ORG}",
    "created": 1550691551888,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550691551888,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Aktualisieren einer Richtlinie

Möglicherweise müssen Sie eine Datennutzungsrichtlinie nach deren Erstellung aktualisieren. Dies geschieht durch eine PUT-Anfrage an die Richtlinien-`id` mit einer Payload, die das aktualisierte Formular der Richtlinie in seiner Gesamtheit enthält. Mit anderen Worten, die PUT-Anfrage _schreibt die Richtlinie im Wesentlichen neu_. Daher muss der Text alle erforderlichen Informationen enthalten, wie im folgenden Beispiel gezeigt.

**API-Format**

```http
PUT /policies/custom/{id}
```

**Anfrage**

In diesem Beispiel haben sich die Bedingungen für den Export von Daten an einen Drittanbieter geändert. Daher muss die von Ihnen erstellte Richtlinie diese Marketing-Aktion jetzt ablehnen, wenn `C1 AND (C3 OR C7)`-Datenbezeichnungen vorhanden sind. Mit dem folgenden Aufruf können Sie die vorhandene Richtlinie aktualisieren.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "../marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "AND",
          "operands": [
            {"label": "C1"},
            {
              "operator": "OR",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

**Antwort**

Bei einer erfolgreichen Aktualisierungsanfrage wird ein HTTP-Status 200 (OK) zurückgegeben, und der Antworttext zeigt die aktualisierte Richtlinie an. Die `id` sollte mit der in der Anfrage gesendeten `id` übereinstimmen.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/core/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "C7"
                    }
                ]
            }
        ]
    },
    "imsOrg": "{IMS_ORG}",
    "created": 1550691551888,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Aktualisieren eines Teils einer Richtlinie

Ein bestimmter Teil einer Richtlinie kann mithilfe einer PATCH-Anfrage aktualisiert werden. Im Gegensatz zu PUT-Anfragen, die die Richtlinie _umschreiben_, aktualisieren PATCH-Anfragen nur den im Anfrageinhalt angegebenen Pfad. Dies ist besonders hilfreich, wenn Sie eine Richtlinie aktivieren oder deaktivieren möchten, da Sie nur den zu aktualisierenden Pfad (`/status`) und dessen Wert (`ENABLE` oder `DISABLE`) senden müssen.

The [!DNL Policy Service] API currently supports &quot;add&quot;, &quot;replace&quot;, and &quot;remove&quot; PATCH operations, and allows you to combine several updates together into a single call by adding each as an object within the array, as shown in the following examples.

**API-Format**

```http
PATCH /policies/custom/{id}
```

**Anfrage**

In diesem Beispiel verwenden wir den Vorgang „Ersetzen“, um den Richtlinienstatus von „ENTWURF“ in „AKTIVIERT“ zu ändern und das Beschreibungsfeld mit einer neuen Beschreibung zu aktualisieren. Wir hätten auch das Beschreibungsfeld aktualisieren können, indem wir die Richtlinienbeschreibung mit „Löschen“ entfernen und dann mit „Hinzufügen“ eine neue hinzufügen. Beispiel:

```SHELL
[
    {
        "op": "remove",
        "path": "/description"
    },
    {
        "op": "add",
        "path": "/description",
        "value": "New policy description."
    }
]
```

Denken Sie beim Senden mehrerer PATCH-Vorgänge in einer einzigen Anfrage daran, dass diese in der Reihenfolge verarbeitet werden, in der sie im Array erscheinen. Achten Sie daher darauf, dass Sie die Anfragen bei Bedarf in der richtigen Reihenfolge senden.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' [
          {
            "op": "replace",
            "path": "/status",
            "value": "ENABLED"
          },
          {
            "op": "replace",
            "path": "/description",
            "value": "New policy description."
          }
        ]'
```

**Antwort**

Eine erfolgreiche Aktualisierungsanfrage gibt einen HTTP-Status 200 (OK) zurück und der Antworttext zeigt die aktualisierte Richtlinie an („Status“ ist jetzt „AKTIVIERT“ und „Beschreibung“ wurde geändert). Die `id` der Richtlinie sollte mit der in der Anfrage gesendeten `id` übereinstimmen.


```JSON
{
    "name": "Export Data to Third Party",
    "status": "ENABLED",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "New policy description.",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "C7"
                    }
                ]
            }
        ]
    },
    "imsOrg": "{IMS_ORG}",
    "created": 1550703519823,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550712163182,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Löschen einer Richtlinie

Wenn Sie eine von Ihnen erstellte Richtlinie entfernen müssen, können Sie dazu eine DELETE-Anfrage an die `id` der Richtlinie senden, die Sie löschen möchten. Es empfiehlt sich, zuerst eine Suchanfrage (GET) durchzuführen, um die Richtlinie anzuzeigen und zu bestätigen, dass es sich um die richtige Richtlinie handelt, die Sie entfernen möchten. **Nach dem Löschen können Richtlinien nicht wiederhergestellt werden.**

**API-Format**

```http
DELETE /policies/custom/{id}
```

**Anfrage**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Wenn die Richtlinie erfolgreich gelöscht wurde, ist der Antworttext mit einem HTTP-Status 200 (OK) leer.

Sie können den Löschvorgang bestätigen, indem Sie erneut versuchen, nach der Richtlinie zu suchen (GET). Sie sollten den HTTP-Status 404 (Nicht gefunden) zusammen mit der Fehlermeldung „Nicht gefunden“ erhalten, da die Richtlinie entfernt wurde.
