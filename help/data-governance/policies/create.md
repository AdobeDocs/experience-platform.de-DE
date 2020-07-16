---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datennutzungsrichtlinie erstellen
topic: policies
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 83%

---


# Datennutzungsrichtlinie erstellen in der API

Data Usage Labeling and Enforcement (DULE) ist der Kernmechanismus von Adobe Experience Platform [!DNL Data Governance]. Mit der [DULE Policy Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) können Sie DULE-Richtlinien erstellen und verwalten, um festzulegen, welche Marketing-Aktionen für Daten mit bestimmten DULE-Bezeichnungen ausgeführt werden können.

This document provides a step-by-step tutorial for creating a DULE policy using the [!DNL Policy Service] API. Eine genauere Anleitung zu den verschiedenen in der API verfügbaren Vorgängen finden Sie im [Entwicklerhandbuch für Policy Service](../api/getting-started.md).

## Erste Schritte

Diese Anleitung setzt ein Verständnis der folgenden Schlüsselkonzepte voraus, die beim Erstellen und Evaluieren von DULE-Richtlinien zum Einsatz kommen:

* [!DNL Data Governance](../home.md): Das Framework, mit dem die Einhaltung der Datenverwendung [!DNL Platform] erzwungen wird.
* [Datennutzungsbezeichnungen](../labels/overview.md): Datennutzungsbezeichnungen werden auf XDM-Datenfelder angewendet und geben Einschränkungen für den Zugriff auf diese Daten an.
* [!DNL Experience Data Model (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Platform] organisiert werden.
* [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Before starting this tutorial, please review the [developer guide](../api/getting-started.md) for important information that you need to know in order to successfully make calls to the DULE [!DNL Policy Service] API, including required headers and how to read example API calls.

## Marketing-Aktion definieren {#define-action}

In the [!DNL Data Governance] framework, a marketing action is an action that an [!DNL Experience Platform] data consumer takes, for which there is a need to check for violations of data usage policies.

Der erste Schritt bei der Erstellung einer DULE-Richtlinie besteht darin, zu bestimmen, welche Marketing-Aktion die Richtlinie bewerten soll. Dies kann mit einer der folgenden Optionen erledigt werden:

* [Vorhandene Marketing-Aktion nachschlagen](#look-up)
* [Neue Marketing-Aktion erstellen](#create-new)

### Vorhandene Marketing-Aktion nachschlagen {#look-up}

Sie können vorhandene Marketing-Aktionen nachschlagen, die von Ihrer DULE-Richtlinie bewertet werden sollen, indem Sie eine GET-Anfrage an einen der `/marketingActions`-Endpunkte senden.

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

Wenn Sie die Marketing-Aktion gefunden haben, die Sie verwenden möchten, notieren Sie sich den Wert seiner `href`-Eigenschaft. Dieser Wert wird im nächsten Schritt zum [Erstellen einer DULE-Richtlinie](#create-policy) benötigt.

### Neue Marketing-Aktion erstellen{#create-new}

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

Notieren Sie sich die URI-ID der neu erstellten Marketing-Aktion, da Sie sie im nächsten Schritt beim Erstellen einer DULE-Richtlinie benötigen werden.

## DULE-Richtlinie erstellen {#create-policy}

Für das Erstellen einer neuen Richtlinie müssen Sie die URI-ID einer Marketing-Aktion mit einem Ausdruck der DULE-Bezeichnungen angeben, die diese Marketing-Aktion verbieten.

Dieser Ausdruck wird als **Richtlinienausdruck** bezeichnet und ist ein Objekt, das entweder (A) eine DULE-Bezeichnung oder (B) einen Operator und Operanden enthält, aber nicht beide. Jeder Operand ist wiederum ein Richtlinienausdrucksobjekt. So könnte beispielsweise eine Richtlinie für den Export von Daten an eine Drittpartei verboten werden, wenn `C1 OR (C3 AND C7)`-Kennzeichnungen vorhanden sind. Dieser Ausdruck würde wie folgt definiert:

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

Nachdem Sie Ihren Richtlinienausdruck konfiguriert haben, können Sie eine neue DULE-Richtlinie erstellen, indem Sie eine POST-Anfrage an den `/policies/custom`-Endpunkt senden.

**API-Format**

```http
POST /policies/custom
```

**Anfrage**

Mit der folgenden Anfrage wird eine DULE-Richtlinie mit dem Namen „Daten an Dritte exportieren“ erstellt, indem in der Anfrage-Payload eine Marketing-Aktion und ein Richtlinienausdruck angegeben werden.

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
| `deny` | Das Richtlinienausdrucksobjekt. Definiert die DULE-Bezeichnungen und -Bedingungen, die dazu führen würden, dass die Richtlinie die in `marketingActionRefs` referenzierte Marketing-Aktion ablehnt. |

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
| `id` | Ein schreibgeschützter, systemgenerierter Wert, der die DULE-Richtlinie eindeutig identifiziert. |

Notieren Sie sich die URI-ID der neu erstellten DULE-Richtlinie, da Sie sie im nächsten Schritt zum Aktivieren der Richtlinie benötigen werden.

## DULE-Richtlinie aktivieren

>[!NOTE]
>
>Dieser Schritt ist optional, wenn Sie Ihre DULE-Richtlinie im Status `DRAFT` belassen möchten; beachten Sie jedoch, dass für eine Richtlinie der Status standardmäßig auf `ENABLED` festgelegt sein muss, damit sie Teil der Bewertung wird. Informationen zur Verwendung von Ausnahmen für Richtlinien mit dem Status `DRAFT` finden Sie in der Anleitung zum [Durchsetzen von DULE-Richtlinien](../enforcement/api-enforcement.md).

Standardmäßig sind DULE-Richtlinien, deren `status`-Eigenschaft auf `DRAFT` gesetzt ist, nicht Teil der Bewertung. Sie können Ihre Richtlinie für die Bewertung aktivieren, indem Sie eine PATCH-Anfrage an den `/policies/custom/`-Endpunkt senden und am Ende des Anfragepfads die eindeutige Kennung für die Richtlinie angeben.

**API-Format**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{POLICY_ID}` | Der `id`-Wert der Richtlinie, die aktiviert werden soll. |

**Anfrage**

Die folgende Anfrage führt einen PATCH-Vorgang für die `status`-Eigenschaft der DUL-Richtlinie aus und ändert deren Wert von `DRAFT` in `ENABLED`.

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