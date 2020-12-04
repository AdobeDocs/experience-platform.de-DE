---
keywords: Experience Platform;home;popular topics;data governance;data usage policy
solution: Experience Platform
title: Datennutzungsrichtlinie erstellen
topic: policies
type: Tutorial
description: Mit der Policy Service-API können Sie Datenverwendungsrichtlinien erstellen und verwalten, um zu bestimmen, welche Marketingaktionen für Daten mit bestimmten Datenverwendungsbeschriftungen durchgeführt werden können. Dieses Dokument bietet eine schrittweise Anleitung zum Erstellen einer Richtlinie mithilfe der Policy Service API.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 50%

---


# Eine Datenverwendungsrichtlinie in der API erstellen

The [Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) allows you to create and manage data usage policies to determine what marketing actions can be taken against data that contains certain data usage labels.

This document provides a step-by-step tutorial for creating a policy using the [!DNL Policy Service] API. Eine genauere Anleitung zu den verschiedenen in der API verfügbaren Vorgängen finden Sie im [Entwicklerhandbuch für Policy Service](../api/getting-started.md).

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Schlüsselkonzepte, die beim Erstellen und Evaluieren von Richtlinien zum Einsatz kommen:

* [[!DNL Data Governance]](../home.md): Das Framework, mit dem die Einhaltung der Datenverwendung [!DNL Platform] erzwungen wird.
* [Datennutzungsbezeichnungen](../labels/overview.md): Datennutzungsbezeichnungen werden auf XDM-Datenfelder angewendet und geben Einschränkungen für den Zugriff auf diese Daten an.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.
* [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Before starting this tutorial, please review the [developer guide](../api/getting-started.md) for important information that you need to know in order to successfully make calls to the [!DNL Policy Service] API, including required headers and how to read example API calls.

## Marketing-Aktion definieren {#define-action}

In the [!DNL Data Governance] framework, a marketing action is an action that an [!DNL Experience Platform] data consumer takes, for which there is a need to check for violations of data usage policies.

Der erste Schritt bei der Erstellung einer Datenverwendungsrichtlinie besteht darin, zu bestimmen, welche Marketingaktion die Richtlinie auswerten wird. Dies kann mit einer der folgenden Optionen erledigt werden:

* [Vorhandene Marketing-Aktion nachschlagen](#look-up)
* [Neue Marketing-Aktion erstellen](#create-new)

### Vorhandene Marketing-Aktion nachschlagen {#look-up}

You can look up existing marketing actions to be evaluated by your policy by making a GET request to one of the `/marketingActions` endpoints.

**API-Format**

Depending on whether you are looking up a marketing action provided by [!DNL Experience Platform] or a custom marketing action created by your organization, use the `marketingActions/core` or `marketingActions/custom` endpoints, respectively.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Anfrage**

Die folgende Anfrage nutzt den `marketingActions/custom`-Endpunkt, der eine Liste aller von Ihrer IMS-Organisation definierten Marketing-Aktionen abruft.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Gesamtanzahl der gefundenen Marketing-Aktionen zurück (`count`) und listet im `children`-Array die Details der Marketing-Aktionen auf.

```json
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
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714012088,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550793833224,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550793833224,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `_links.self.href` | Jedes Element im `children`-Array enthält eine URI-ID für die aufgelistete Marketing-Aktion. |

Wenn Sie die Marketing-Aktion gefunden haben, die Sie verwenden möchten, notieren Sie sich den Wert seiner `href`-Eigenschaft. This value is used during the next step of [creating a policy](#create-policy).

### Neue Marketing-Aktion erstellen {#create-new}

Sie können eine neue Marketing-Aktion erstellen, indem Sie eine PUT-Anfrage an den `/marketingActions/custom/`-Endpunkt senden und am Ende des Anfragepfads einen Namen für die Marketing-Aktion angeben.

**API-Format**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der neuen Marketing-Aktion, die Sie erstellen möchten. Dieser Name dient als primäre Kennung der Marketing-Aktion und muss daher eindeutig sein. Best Practice ist es, der Marketing-Aktion einen beschreibenden, aber knappen Namen zu geben. |

**Anfrage**

Die folgende Anfrage erstellt eine neue benutzerdefinierte Marketing-Aktion mit dem Namen „exportToThirdParty“. Beachten Sie, dass der `name` in der Anfrage-Payload identisch mit dem im Anfragepfad angegebenen Namen ist.

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "exportToThirdParty",
      "description": "Export data to a third party"
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name der Marketing-Aktion, die Sie erstellen möchten. Dieser Name muss mit dem im Anfragepfad angegebenen Namen übereinstimmen; andernfalls tritt der Fehler 400 (Ungültige Anfrage) auf. |
| `description` | Eine für Menschen lesbare Beschreibung der Marketing-Aktion. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) sowie die Details der neu erstellten Marketing-Aktion zurück.

```json
{
    "name": "exportToThirdParty",
    "description": "Export data to a third party",
    "imsOrg": "{IMS_ORG}",
    "created": 1550713341915,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1550713856390,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        }
    }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `_links.self.href` | Die URI-ID der Marketing-Aktion. |

Zeichnen Sie die URI-ID der neu erstellten Marketingaktion auf, wie sie im nächsten Schritt der Erstellung einer Richtlinie verwendet wird.

## Erstellen einer Richtlinie {#create-policy}

Zum Erstellen einer neuen Richtlinie müssen Sie die URI-ID einer Marketingaktion mit einem Ausdruck der Gebrauchsbeschriftungen versehen, die diese Marketingaktion verbieten.

Dieser Ausdruck wird als Policy-Ausdruck bezeichnet und ist ein Objekt, das entweder (A) eine Beschriftung oder (B) einen Operator und Operanden, aber nicht beides enthält. Jeder Operand ist wiederum ein Richtlinienausdrucksobjekt. So könnte beispielsweise eine Richtlinie für den Export von Daten an eine Drittpartei verboten werden, wenn `C1 OR (C3 AND C7)`-Kennzeichnungen vorhanden sind. Dieser Ausdruck würde wie folgt definiert:

```json
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
}
```

>[!NOTE]
>
>Nur OR- und AND-Operatoren werden unterstützt.

Once you have configured your policy expression, you can create a new policy by making a POST request to the `/policies/custom` endpoint.

**API-Format**

```http
POST /policies/custom
```

**Anfrage**

Mit der folgenden Anforderung wird eine Richtlinie mit dem Namen &quot;Daten an Dritte exportieren&quot;erstellt, indem eine Marketingaktion und ein Richtlinien-Ausdruck in der Anforderungs-Nutzlast bereitgestellt werden.

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

| Eigenschaft | Beschreibung |
| --- | --- |
| `marketingActionRefs` | Ein Array, das den `href`-Wert einer Marketing-Aktion enthält, der im [vorherigen Schritt](#define-action) abgerufen wurde. Im obigen Beispiel wird zwar nur eine Marketing-Aktion aufgelistet, es können aber auch mehrere Aktionen angegeben werden. |
| `deny` | Das Richtlinienausdrucksobjekt. Defines the usage labels and conditions that would cause the policy to reject the marketing action referenced in `marketingActionRefs`. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) sowie die Details der neu erstellten Richtlinie zurück.

```json
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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
    "created": 1565651746693,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1565651746693,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
    },
    "id": "5d51f322e553c814e67af1a3"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Ein schreibgeschützter, systemgenerierter Wert, der die Richtlinie eindeutig identifiziert. |

Zeichnen Sie die URI-ID der neu erstellten Richtlinie auf, wie sie im nächsten Schritt zum Aktivieren der Richtlinie verwendet wird.

## Richtlinie aktivieren

>[!NOTE]
>
>While this step is optional if you wish to leave your policy in `DRAFT` status, please note that by default a policy must have its status set to `ENABLED` in order to participate in evaluation. See the guide on [policy enforcement](../enforcement/api-enforcement.md) for information on how to make exceptions for policies in `DRAFT` status.

By default, policies that have their `status` property set to `DRAFT` do not participate in evaluation. Sie können Ihre Richtlinie für die Bewertung aktivieren, indem Sie eine PATCH-Anfrage an den `/policies/custom/`-Endpunkt senden und am Ende des Anfragepfads die eindeutige Kennung für die Richtlinie angeben.

**API-Format**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{POLICY_ID}` | Der `id`-Wert der Richtlinie, die aktiviert werden soll. |

**Anfrage**

The following request performs a PATCH operation on the `status` property of the policy, changing its value from `DRAFT` to `ENABLED`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    {
      "op": "replace",
      "path": "/status",
      "value": "ENABLED"
    }
  ]'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `op` | Der Typ des auszuführenden PATCH-Vorgangs. Diese Anfrage führt einen „replace“-Vorgang aus. |
| `path` | Der Pfad zu dem zu aktualisierenden Feld. Beim Aktivieren einer Richtlinie muss der Wert auf „/status“ gesetzt werden. |
| `value` | Der neue Wert, der der Eigenschaft zugewiesen werden soll, die in `path` angegeben ist. Diese Anfrage setzt die `status`-Eigenschaft der Richtlinie auf „AKTIVIERT“. |

**Antwort**

Bei einer erfolgreichen Antwort werden der HTTP-Status 200 (OK) und die Details der aktualisierten Richtlinie zurückgegeben, wobei ihr `status` nun `ENABLED` lautet.

```json
{
    "name": "Export Data to Third Party",
    "status": "ENABLED",
    "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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
    "created": 1565651746693,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER}",
    "updated": 1565723012139,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
    },
    "id": "5d51f322e553c814e67af1a3"
}
```

## Nächste Schritte

In dieser Anleitung haben Sie für eine Marketing-Aktion erfolgreich eine Datennutzungsrichtlinie erstellt. Sie können nun mit der Anleitung zum [Durchsetzen von Datennutzungsrichtlinien](../enforcement/api-enforcement.md) fortfahren, um zu erfahren, wie Sie in Ihrer Erlebnisanwendung Richtlinienverletzungen erkennen und behandeln können.

For more information on the different available operations in the [!DNL Policy Service] API,  see the [Policy Service developer guide](../api/getting-started.md). For information on how to enforce policies for [!DNL Real-time Customer Profile] data, see the tutorial on [enforcing data usage compliance for audience segments](../../segmentation/tutorials/governance.md).

To learn how to manage usage policies in the [!DNL Experience Platform] user interface, see the [policy user guide](user-guide.md).