---
keywords: Experience Platform;home;popular topics;Policy enforcement;API-based enforcement;data governance
solution: Experience Platform
title: Richtlinien
topic: developer guide
description: Datennutzungsrichtlinien sind von Ihrem Unternehmen angewandte Regeln, die die Arten von Marketing-Aktionen beschreiben, die Sie für Daten in der Experience Platform ausführen bzw. nicht ausführen dürfen. Der Endpunkt /policies wird für alle API-Aufrufe verwendet, die sich auf das Anzeigen, Erstellen, Aktualisieren oder Löschen von Datenverwendungsrichtlinien beziehen.
translation-type: tm+mt
source-git-commit: a362b67cec1e760687abb0c22dc8c46f47e766b7
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 9%

---


# Endpunkt der Richtlinien

Data usage policies are rules that describe the kinds of marketing actions that you are allowed to, or restricted from, performing on data within [!DNL Experience Platform]. Der `/policies` Endpunkt im [!DNL Policy Service API] ermöglicht Ihnen die programmatische Verwaltung von Datenverwendungsrichtlinien für Ihr Unternehmen.

## Erste Schritte

The API endpoint used in this guide is part of the [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Bevor Sie fortfahren, lesen Sie bitte die [Anleitung](getting-started.md) zu den ersten Schritten für Links zur zugehörigen Dokumentation, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu den erforderlichen Kopfzeilen, die zum erfolgreichen Aufrufen einer beliebigen [!DNL Experience Platform] API erforderlich sind.

## Retrieve a list of policies {#list}

Sie können alle `core` oder `custom` Richtlinien durch eine GET an `/policies/core` bzw. `/policies/custom`anfordern.

**API-Format**

```http
GET /policies/core
GET /policies/custom
```

**Anfrage**

Die folgende Anforderung ruft eine Liste von benutzerdefinierten Richtlinien ab, die von Ihrem Unternehmen definiert wurden.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort enthält ein `children` Array, das die Details der einzelnen abgerufenen Richtlinien einschließlich ihrer `id` Werte Liste. Sie können das `id` Feld einer bestimmten Richtlinie verwenden, um [Suchen](#lookup), [Aktualisieren](#update)und [Löschen](#delete) von Anforderungen für diese Richtlinie durchzuführen.

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
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550701472910,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
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
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550714340335,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
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

| Eigenschaft | Beschreibung |
| --- | --- |
| `_page.count` | Die Gesamtzahl der abgerufenen Richtlinien. |
| `name` | Der Anzeigename für eine Richtlinie. |
| `status` | Der aktuelle Status einer Richtlinie. Es gibt drei mögliche Status: `DRAFT`, `ENABLED`oder `DISABLED`. By default, only `ENABLED` policies participate in evaluation. Weitere Informationen finden Sie in der Übersicht zur [Richtlinienbewertung](../enforcement/overview.md) . |
| `marketingActionRefs` | Ein Array, das die URIs aller für eine Richtlinie geltenden Marketingaktionen Liste. |
| `description` | Eine optionale Beschreibung, die weiteren Kontext zum Anwendungsfall der Richtlinie bietet. |
| `deny` | Ein Objekt, das die spezifischen Datenverwendungsbeschriftungen beschreibt, an denen die zugeordnete Marketingaktion einer Richtlinie nicht ausgeführt werden kann. Weitere Informationen zu dieser Eigenschaft finden Sie im Abschnitt zum [Erstellen einer Richtlinie](#create-policy) . |

## Eine Richtlinie nachschlagen {#look-up}

Sie können eine bestimmte Richtlinie nachschlagen, indem Sie die `id` Eigenschaft dieser Richtlinie in den Pfad einer GET-Anforderung aufnehmen.

**API-Format**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{POLICY_ID}` | The `id` of the policy you want to look up. |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Richtlinie zurück.

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
    "created": 1550703519823,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550714340335,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Anzeigename für die Richtlinie. |
| `status` | Der aktuelle Status der Richtlinie. Es gibt drei mögliche Status: `DRAFT`, `ENABLED`oder `DISABLED`. By default, only `ENABLED` policies participate in evaluation. Weitere Informationen finden Sie in der Übersicht zur [Richtlinienbewertung](../enforcement/overview.md) . |
| `marketingActionRefs` | Ein Array, das die URIs aller für die Richtlinie geltenden Marketingaktionen Liste. |
| `description` | Eine optionale Beschreibung, die weiteren Kontext zum Anwendungsfall der Richtlinie bietet. |
| `deny` | Ein Objekt, das die spezifischen Datenverwendungsbeschriftungen beschreibt, an denen die zugeordnete Marketingaktion der Richtlinie nicht ausgeführt werden darf. Weitere Informationen zu dieser Eigenschaft finden Sie im Abschnitt zum [Erstellen einer Richtlinie](#create-policy) . |

## Create a custom policy {#create-policy}

In der [!DNL Policy Service] API wird eine Richtlinie wie folgt definiert:

* Ein Verweis auf eine bestimmte Marketingaktion
* Ein Ausdruck, der die Datenverwendungsbeschriftungen beschreibt, die die Marketingaktion von der Ausführung gegen

Um diese Anforderung zu erfüllen, müssen Richtliniendefinitionen einen booleschen Ausdruck zum Vorhandensein von Datenverwendungsbeschriftungen enthalten. Dieser Ausdruck wird als Ausdruck für Richtlinien bezeichnet.

Richtlinien-Ausdruck werden in jeder Richtliniendefinition in Form einer `deny` Eigenschaft bereitgestellt. Ein Beispiel für ein einfaches `deny` Objekt, das nur das Vorhandensein einer einzelnen Beschriftung überprüft, würde wie folgt aussehen:

```json
"deny": {
    "label": "C1"
}
```

In vielen Richtlinien werden jedoch komplexere Bedingungen für das Vorhandensein von Datenverwendungsbeschriftungen festgelegt. Um diese Anwendungsfälle zu unterstützen, können Sie auch boolesche Vorgänge zur Beschreibung Ihrer Richtlinien-Ausdruck einschließen. Das policy Ausdruck-Objekt muss entweder eine Beschriftung oder einen Operator und Operanden enthalten, jedoch nicht beides. Jeder Operand ist wiederum ein Richtlinienausdrucksobjekt.

Um beispielsweise eine Richtlinie zu definieren, die verhindert, dass eine Marketingaktion für Daten ausgeführt wird, in denen `C1 OR (C3 AND C7)` Beschriftungen vorhanden sind, wird die Eigenschaft der Richtlinie `deny` wie folgt angegeben:

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

| Eigenschaft | Beschreibung |
| --- | --- |
| `operator` | Gibt die bedingte Beziehung zwischen den im Geschwisterarray bereitgestellten Beschriftungen `operands` an. Akzeptierte Werte sind: <ul><li>`OR`: Der Ausdruck wird in &quot;true&quot;aufgelöst, wenn eine der Beschriftungen im `operands` Array vorhanden ist.</li><li>`AND`: Der Ausdruck wird nur dann auf &quot;true&quot;aufgelöst, wenn alle Beschriftungen im `operands` Array vorhanden sind.</li></ul> |
| `operands` | Ein Array von Objekten, wobei jedes Objekt entweder eine einzelne Beschriftung oder ein zusätzliches Paar `operator` und `operands` Eigenschaften darstellt. Das Vorhandensein der Beschriftungen und/oder Vorgänge in einem `operands` Array wird basierend auf dem Wert der zugehörigen `operator` Eigenschaft &quot;Geschwister&quot;zu &quot;true&quot;oder &quot;false&quot;aufgelöst. |
| `label` | Der Name einer einzelnen Datenverwendungsbeschriftung, die für die Richtlinie gilt. |

You can create a new custom policy by making a POST request to the `/policies/custom` endpoint.

**API-Format**

```http
POST /policies/custom
```

**Anfrage**

Die folgende Anforderung erstellt eine neue Richtlinie, die die Ausführung der Marketingaktion `exportToThirdParty` auf Daten mit Beschriftungen einschränkt `C1 OR (C3 AND C7)`.

```shell
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
          "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Anzeigename für die Richtlinie. |
| `status` | Der aktuelle Status der Richtlinie. Es gibt drei mögliche Status: `DRAFT`, `ENABLED`oder `DISABLED`. By default, only `ENABLED` policies participate in evaluation. Weitere Informationen finden Sie in der Übersicht zur [Richtlinienbewertung](../enforcement/overview.md) . |
| `marketingActionRefs` | Ein Array, das die URIs aller für die Richtlinie geltenden Marketingaktionen Liste. Der URI für eine Marketingaktion wird `_links.self.href` in der Antwort für die [Suche nach einer Marketingaktion](./marketing-actions.md#look-up)bereitgestellt. |
| `description` | Eine optionale Beschreibung, die weiteren Kontext zum Anwendungsfall der Richtlinie bietet. |
| `deny` | Der Ausdruck der Richtlinie, der die spezifischen Datenverwendungsbeschriftungen beschreibt, mit denen die verknüpfte Marketingaktion der Richtlinie gekennzeichnet ist, ist von der Ausführung ausgeschlossen. |

**Antwort**

A successful response returns the details of the newly created policy, including its `id`. Dieser Wert ist schreibgeschützt und wird beim Erstellen der Richtlinie automatisch zugewiesen.

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
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550691551888,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Eine benutzerdefinierte Richtlinie aktualisieren {#update}

>[!IMPORTANT]
>
>Sie können nur benutzerdefinierte Richtlinien aktualisieren. Wenn Sie die Kernrichtlinien aktivieren oder deaktivieren möchten, lesen Sie den Abschnitt zur [Aktualisierung der Liste der aktivierten Hauptrichtlinien](#update-enabled-core).

Sie können eine vorhandene benutzerdefinierte Richtlinie aktualisieren, indem Sie ihre ID im Pfad einer PUT-Anforderung mit einer Nutzlast angeben, die das aktualisierte Formular der Richtlinie vollständig enthält. Mit anderen Worten, die PUT-Anforderung schreibt die Richtlinie im Wesentlichen um.

>[!NOTE]
>
>Siehe Abschnitt zum [Aktualisieren eines Teils einer benutzerdefinierten Richtlinie](#patch) , wenn Sie nur ein oder mehrere Felder für eine Richtlinie aktualisieren möchten, anstatt sie zu überschreiben.

**API-Format**

```http
PUT /policies/custom/{POLICY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{POLICY_ID}` | The `id` of the policy you want to update. |

**Anfrage**

In diesem Beispiel haben sich die Bedingungen für den Export von Daten an einen Drittanbieter geändert. Daher muss die von Ihnen erstellte Richtlinie diese Marketing-Aktion jetzt ablehnen, wenn `C1 AND C5`-Datenbezeichnungen vorhanden sind.

Mit der folgenden Anforderung wird die vorhandene Richtlinie aktualisiert und der neue Richtlinien-Ausdruck eingefügt. Beachten Sie, dass, da diese Anforderung die Richtlinie im Wesentlichen umschreibt, alle Felder in die Nutzlast einbezogen werden müssen, auch wenn einige ihrer Werte nicht aktualisiert werden.

```shell
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
            {"label": "C5"}
          ]
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Anzeigename für die Richtlinie. |
| `status` | Der aktuelle Status der Richtlinie. Es gibt drei mögliche Status: `DRAFT`, `ENABLED`oder `DISABLED`. By default, only `ENABLED` policies participate in evaluation. Weitere Informationen finden Sie in der Übersicht zur [Richtlinienbewertung](../enforcement/overview.md) . |
| `marketingActionRefs` | Ein Array, das die URIs aller für die Richtlinie geltenden Marketingaktionen Liste. Der URI für eine Marketingaktion wird `_links.self.href` in der Antwort für die [Suche nach einer Marketingaktion](./marketing-actions.md#look-up)bereitgestellt. |
| `description` | Eine optionale Beschreibung, die weiteren Kontext zum Anwendungsfall der Richtlinie bietet. |
| `deny` | Der Ausdruck der Richtlinie, der die spezifischen Datenverwendungsbeschriftungen beschreibt, mit denen die verknüpfte Marketingaktion der Richtlinie gekennzeichnet ist, ist von der Ausführung ausgeschlossen. Weitere Informationen zu dieser Eigenschaft finden Sie im Abschnitt zum [Erstellen einer Richtlinie](#create-policy) . |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der aktualisierten Richtlinie zurück.

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
                "label": "C5"
            }
        ]
    },
    "imsOrg": "{IMS_ORG}",
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550701472910,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Update a portion of a custom policy {#patch}

>[!IMPORTANT]
>
>Sie können nur benutzerdefinierte Richtlinien aktualisieren. Wenn Sie die Kernrichtlinien aktivieren oder deaktivieren möchten, lesen Sie den Abschnitt zur [Aktualisierung der Liste der aktivierten Hauptrichtlinien](#update-enabled-core).

Ein bestimmter Teil einer Richtlinie kann mithilfe einer PATCH-Anfrage aktualisiert werden. Im Gegensatz zu PUT-Anforderungen, die die Richtlinie umschreiben, aktualisieren PATCH-Anfragen nur die im Anforderungstext angegebenen Eigenschaften. Dies ist besonders hilfreich, wenn Sie eine Richtlinie aktivieren oder deaktivieren möchten, da Sie nur den Pfad zur entsprechenden Eigenschaft (`/status`) und deren Wert (`ENABLED` oder `DISABLED`) angeben müssen.

>[!NOTE]
>
>Nutzlasten für PATCH-Anfragen folgen der JSON-Patch-Formatierung. Weitere Informationen zur verwendeten Syntax finden Sie im Leitfaden [zu den](../../landing/api-fundamentals.md) API-Grundlagen.

Die [!DNL Policy Service] API unterstützt die JSON Patch-Vorgänge `add`, `remove`und `replace`ermöglicht Ihnen, mehrere Updates zu einem einzigen Aufruf zusammenzufassen, wie im folgenden Beispiel gezeigt.

**API-Format**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{POLICY_ID}` | Die `id` Richtlinie, deren Eigenschaften Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anforderung verwendet zwei `replace` Vorgänge, um den Richtlinienstatus von `DRAFT` in zu ändern `ENABLED`und das `description` Feld mit einer neuen Beschreibung zu aktualisieren.

>[!IMPORTANT]
>
>Wenn mehrere PATCH-Vorgänge in einer einzigen Anforderung gesendet werden, werden sie in der Reihenfolge verarbeitet, in der sie im Array angezeigt werden. Vergewissern Sie sich, dass Sie die Anfragen bei Bedarf in der richtigen Reihenfolge senden.

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

Eine erfolgreiche Antwort gibt die Details der aktualisierten Richtlinie zurück.


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
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550712163182,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Eine benutzerdefinierte Richtlinie löschen {#delete}

You can delete a custom policy by including its `id` in the path of a DELETE request.

>[!WARNING]
>
>Nach dem Löschen können Richtlinien nicht wiederhergestellt werden. It is best practice to [perform a lookup (GET) request](#lookup) first to view the policy and confirm it is the correct policy you wish to remove.

**API-Format**

```http
DELETE /policies/custom/{POLICY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{POLICY_ID}` | Die ID der Richtlinie, die Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 (OK) mit einem leeren Text zurück.

Sie können den Löschvorgang bestätigen, indem Sie versuchen, die Richtlinie erneut nachzuschlagen (GET). Sie sollten den HTTP 404-Fehler (Nicht gefunden) erhalten, wenn die Richtlinie erfolgreich gelöscht wurde.

## Eine Liste der aktivierten Hauptrichtlinien abrufen {#list-enabled-core}

Standardmäßig werden nur aktivierte Datenverwendungsrichtlinien an der Auswertung beteiligt. Sie können eine Liste der derzeit von Ihrem Unternehmen aktivierten Kernrichtlinien abrufen, indem Sie eine GET an den `/enabledCorePolicies` Endpunkt anfordern.

**API-Format**

```http
GET /enabledCorePolicies
```

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Liste der aktivierten Core-Richtlinien unter einem `policyIds` Array zurück.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0003",
    "corepolicy_0004",
    "corepolicy_0005",
    "corepolicy_0006",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{IMS_ORG}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## Liste der aktivierten Hauptrichtlinien aktualisieren {#update-enabled-core}

Standardmäßig werden nur aktivierte Datenverwendungsrichtlinien an der Auswertung beteiligt. Wenn Sie eine PUT-Anforderung an den `/enabledCorePolicies` Endpunkt stellen, können Sie die Liste der aktivierten Core-Richtlinien für Ihr Unternehmen mit einem einzigen Aufruf aktualisieren.

>[!NOTE]
>
>Nur Kernrichtlinien können von diesem Endpunkt aktiviert oder deaktiviert werden. Informationen zum Aktivieren oder Deaktivieren benutzerdefinierter Richtlinien finden Sie im Abschnitt zum [Aktualisieren eines Teils einer Richtlinie](#patch).

**API-Format**

```http
PUT /enabledCorePolicies
```

**Anfrage**

Die folgende Anforderung aktualisiert die Liste der aktivierten Core-Richtlinien auf der Grundlage der in der Nutzlast bereitgestellten IDs.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "policyIds": [
          "corepolicy_0001",
          "corepolicy_0002",
          "corepolicy_0007",
          "corepolicy_0008"
        ]
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `policyIds` | Eine Liste der zu aktivierenden Hauptrichtlinien-IDs. Sämtliche nicht einbezogenen Kernrichtlinien sind auf den `DISABLED` Status eingestellt und werden nicht an der Evaluierung teilnehmen. |

**Antwort**

Eine erfolgreiche Antwort gibt die aktualisierte Liste der aktivierten Core-Richtlinien unter einem `policyIds` Array zurück.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{IMS_ORG}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1595876052649,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## Nächste Schritte

Nachdem Sie neue Richtlinien oder aktualisierte vorhandene Richtlinien definiert haben, können Sie mit der [!DNL Policy Service] API Marketingaktionen für bestimmte Beschriftungen oder Datensätze testen und feststellen, ob Ihre Richtlinien zu erwartenden Verstößen führen. Weitere Informationen finden Sie im Handbuch zu den Endpunkten [der](./evaluation.md) Richtlinienbewertung.