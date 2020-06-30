---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Richtlinien
topic: developer guide
translation-type: tm+mt
source-git-commit: d4964231ee957349f666eaf6b0f5729d19c408de
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 1%

---


# Richtlinien

Data usage policies are rules your organization adopts that describe the kinds of marketing actions that you are allowed to, or restricted from, performing on data within [!DNL Experience Platform].

Der `/policies` Endpunkt wird für alle API-Aufrufe zum Anzeigen, Erstellen, Aktualisieren oder Löschen von Datenverwendungsrichtlinien verwendet.

## Liste aller Richtlinien

Zur Ansicht einer Liste von Richtlinien kann eine GET-Anforderung an alle Richtlinien für den angegebenen Container gesendet werden `/policies/core` oder `/policies/custom` die alle Richtlinien zurückgibt.

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

Die Antwort enthält eine &quot;Anzahl&quot;, die die Gesamtanzahl der Richtlinien im angegebenen Container sowie die Details der einzelnen Richtlinien einschließlich ihrer `id`anzeigt. Das `id` Feld dient zum Durchführen von Suchanfragen zur Ansicht bestimmter Richtlinien sowie zum Durchführen von Aktualisierungs- und Löschvorgängen.

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

Jede Richtlinie enthält ein `id` Feld, mit dem die Details einer bestimmten Richtlinie angefordert werden können. Wenn der Wert `id` einer Richtlinie unbekannt ist, können Sie sie mithilfe der Auflistungsanforderung (GET) finden, um alle Richtlinien in einem bestimmten Container (`core` oder `custom`) wie im vorherigen Schritt dargestellt Liste.

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

Die Antwort enthält die Details der Richtlinie, einschließlich der Schlüsselfelder `id` (dieses Feld sollte mit der `id` gesendeten Anforderung übereinstimmen), `name`, `status`und `description`sowie einen Verweis auf die Marketingaktion, auf der die Richtlinie basiert (`marketingActionRefs`).

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

## Eine Richtlinie erstellen {#create-policy}

Die Erstellung einer Richtlinie erfordert die Aufnahme einer Marketingaktion mit einem Ausdruck der DULE-Etiketten, die diese Marketingaktion verbieten. Richtliniendefinitionen müssen eine `deny` Eigenschaft enthalten, bei der es sich um einen booleschen Ausdruck in Bezug auf das Vorhandensein von DULE-Beschriftungen handelt.

Dieser Ausdruck wird als Objekt bezeichnet `PolicyExpression` und enthält _entweder_ eine Beschriftung _oder_ einen Operator und Operanden, jedoch nicht beide. Jeder Operand ist wiederum ein `PolicyExpression` Objekt. So könnte beispielsweise eine Richtlinie über den Export von Daten an Dritte verboten werden, wenn `C1 OR (C3 AND C7)` Etiketten vorhanden sind. Dieser Ausdruck würde wie folgt definiert:

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

## Richtlinie aktualisieren

Möglicherweise müssen Sie eine Datenverwendungsrichtlinie nach deren Erstellung aktualisieren. Dies geschieht durch eine PUT-Anforderung an die Richtlinie `id` mit einer Nutzlast, die das aktualisierte Formular der Richtlinie in seiner Gesamtheit enthält. Mit anderen Worten, die PUT-Anforderung ist im Wesentlichen eine _Neufassung_ der Richtlinie, daher muss der Text alle erforderlichen Informationen enthalten, wie im Beispiel unten dargestellt.

**API-Format**

```http
PUT /policies/custom/{id}
```

**Anfrage**

In diesem Beispiel haben sich die Bedingungen für den Export von Daten an einen Drittanbieter geändert. Jetzt benötigen Sie die von Ihnen erstellte Richtlinie, um diese Marketingaktion zu verweigern, wenn `C1 AND (C3 OR C7)` Datenbeschriftungen vorhanden sind. Mit dem folgenden Aufruf können Sie die vorhandene Richtlinie aktualisieren.

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

Bei einer erfolgreichen Updateanforderung wird ein HTTP-Status 200 (OK) zurückgegeben, und der Antworttext zeigt die aktualisierte Richtlinie an. Der Wert `id` sollte mit dem in der Anforderung gesendeten `id` übereinstimmen.

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

## Einen Teil einer Richtlinie aktualisieren

Ein bestimmter Teil einer Richtlinie kann mithilfe einer PATCH-Anforderung aktualisiert werden. Im Gegensatz zu PUT-Anforderungen, die die Richtlinie _umschreiben_ , aktualisieren PATCH-Anforderungen nur den im Anforderungstext angegebenen Pfad. Dies ist besonders hilfreich, wenn Sie eine Richtlinie aktivieren oder deaktivieren möchten, da Sie nur den spezifischen Pfad, den Sie aktualisieren möchten (`/status`), und dessen Wert (`ENABLE` oder `DISABLE`) senden müssen.

Die [!DNL Policy Service] API unterstützt derzeit PATCH-Vorgänge &quot;Hinzufügen&quot;, &quot;Ersetzen&quot;und &quot;Entfernen&quot;und ermöglicht es Ihnen, mehrere Aktualisierungen zu einem einzigen Aufruf zu kombinieren, indem Sie sie als Objekt im Array hinzufügen, wie in den folgenden Beispielen dargestellt.

**API-Format**

```http
PATCH /policies/custom/{id}
```

**Anfrage**

In diesem Beispiel verwenden wir den Vorgang &quot;Ersetzen&quot;, um den Richtlinienstatus von &quot;ENTWURF&quot;in &quot;AKTIVIERT&quot;zu ändern und das Beschreibungsfeld mit einer neuen Beschreibung zu aktualisieren. Das Beschreibungsfeld hätte auch aktualisiert werden können, indem der Vorgang &quot;Löschen&quot;zum Entfernen der Richtlinienbeschreibung verwendet und dann der Vorgang &quot;Hinzufügen&quot;verwendet wird, um ein neues Mal hinzuzufügen, z. B.:

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

Denken Sie beim Senden mehrerer PATCH-Vorgänge in einer einzigen Anforderung daran, dass diese in der Reihenfolge verarbeitet werden, in der sie im Array erscheinen. Achten Sie daher darauf, dass Sie die Anforderungen bei Bedarf in der richtigen Reihenfolge senden.

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

Bei einer erfolgreichen Updateanforderung wird ein HTTP-Status 200 (OK) zurückgegeben, und der Antworttext zeigt die aktualisierte Richtlinie an (&quot;Status&quot;ist jetzt &quot;AKTIVIERT&quot;und &quot;Beschreibung&quot;wurde geändert). Die Richtlinie `id` sollte mit der `id` gesendeten Anforderung übereinstimmen.


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

## Eine Richtlinie löschen

Wenn Sie eine von Ihnen erstellte Richtlinie entfernen müssen, können Sie dazu eine DELETE-Anforderung an die Seite `id` der Richtlinie senden, die Sie löschen möchten. Es empfiehlt sich, zuerst eine GET-Anforderung (Lookup) durchzuführen, um die Richtlinie Ansicht und zu bestätigen, dass sie die richtige Richtlinie ist, die Sie entfernen möchten. **Nach dem Löschen können Richtlinien nicht wiederhergestellt werden.**

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

Sie können den Löschvorgang bestätigen, indem Sie versuchen, die Richtlinie erneut nachzuschlagen (GET). Sie sollten eine Fehlermeldung zum HTTP-Status 404 (Nicht gefunden) zusammen mit der Fehlermeldung &quot;Nicht gefunden&quot;erhalten, da die Richtlinie entfernt wurde.
