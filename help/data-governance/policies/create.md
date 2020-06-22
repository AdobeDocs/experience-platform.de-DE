---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Eine Datenverwendungsrichtlinie erstellen
topic: policies
translation-type: tm+mt
source-git-commit: ba9d4b31cfc3b7924879a91bd125f72159e55fc4
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 3%

---


# Eine Datenverwendungsrichtlinie in der API erstellen

Die Datenverwendung - Kennzeichnung und Durchsetzung (DULE) ist der Kernmechanismus der Datenverwaltung in der Adobe Experience Platform. Mit der [DULE Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) können Sie DULE-Richtlinien erstellen und verwalten, um zu bestimmen, welche Marketingaktionen für Daten mit bestimmten DULE-Beschriftungen durchgeführt werden können.

Dieses Dokument bietet eine schrittweise Anleitung zum Erstellen einer DULE-Richtlinie mithilfe der Policy Service API. Eine umfassendere Anleitung zu den verschiedenen in der API verfügbaren Operationen finden Sie im Entwicklerhandbuch für [Policy Service](../api/getting-started.md).

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Schlüsselkonzepte, die beim Erstellen und Evaluieren von DUL-Richtlinien zum Einsatz kommen:

* [Datenverwaltung](../home.md): Das Framework, mit dem die Platform die Einhaltung der Datenverwendungskonformität erzwingt.
* [Datenverwendungsbeschriftungen](../labels/overview.md): Datenverwendungsbeschriftungen werden auf XDM-Datenfelder angewendet und geben Einschränkungen für den Zugriff auf diese Daten an.
* [Erlebnisdatenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.
* [Sandboxen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxen, die eine Instanz einer Platform in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte das [Entwicklerhandbuch](../api/getting-started.md) , um wichtige Informationen zu erhalten, die Sie für die erfolgreiche Durchführung von Aufrufen an die API für den DUL-Policy-Dienst benötigen, einschließlich der erforderlichen Kopfzeilen und Anleitungen zum Lesen von Beispiel-API-Aufrufen.

## Definieren einer Marketingaktion {#define-action}

Im Rahmen der Datenverwaltung handelt es sich bei einer Marketingaktion um eine Experience Platform, die von einem Datenbenutzer ausgeführt wird und bei der überprüft werden muss, ob die Datenverwendungsrichtlinien verletzt wurden.

Der erste Schritt bei der Erstellung einer DULE-Richtlinie besteht darin, zu bestimmen, welche Marketingaktion die Richtlinie bewerten soll. Dies kann mit einer der folgenden Optionen durchgeführt werden:

* [Vorhandene Marketingaktionen nachschlagen](#look-up)
* [Neue Marketingaktion erstellen](#create-new)

### Vorhandene Marketingaktionen nachschlagen {#look-up}

Sie können vorhandene Marketingaktionen nachschlagen, die von Ihrer DULE-Richtlinie ausgewertet werden sollen, indem Sie eine GET-Anforderung an einen der `/marketingActions` Endpunkte senden.

**API-Format**

Je nachdem, ob Sie eine Marketingaktion, die durch Experience Platform bereitgestellt wird, oder eine benutzerdefinierte Marketingaktion Ihres Unternehmens suchen, verwenden Sie die `marketingActions/core` bzw. die `marketingActions/custom` Endpunkte.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Anfrage**

Die folgende Anforderung verwendet den `marketingActions/custom` Endpunkt, der eine Liste aller von Ihrer IMS-Organisation definierten Marketingaktionen abruft.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Gesamtanzahl der gefundenen Marketingaktionen (`count`) zurück und Liste die Details der Marketingaktionen selbst innerhalb des `children` Arrays.

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
| `_links.self.href` | Jedes Element im `children` Array enthält eine URI-ID für die aufgelistete Marketingaktion. |

Wenn Sie die Marketingaktion finden, die Sie verwenden möchten, zeichnen Sie den Wert seiner `href` Eigenschaft auf. Dieser Wert wird im nächsten Schritt der [Erstellung einer DULE-Richtlinie](#create-policy)verwendet.

### Create a new marketing action {#create-new}

Sie können eine neue Marketingaktion erstellen, indem Sie eine PUT-Anforderung an den `/marketingActions/custom/` Endpunkt senden und am Ende des Anforderungspfads einen Namen für die Marketingaktion angeben.

**API-Format**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der neuen Marketingaktion, die Sie erstellen möchten. Dieser Name dient als primäre Kennung der Marketingaktion und muss daher eindeutig sein. Best Practice ist, der Marketingaktion einen beschreibenden, aber knappen Namen zu geben. |

**Anfrage**

Die folgende Anforderung erstellt eine neue benutzerdefinierte Marketingaktion mit dem Namen &quot;exportToThirdParty&quot;. Beachten Sie, dass die `name` in der Anforderungs-Nutzlast identisch mit dem im Anforderungspfad angegebenen Namen ist.

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
| `name` | Der Name der Marketingaktion, die Sie erstellen möchten. Dieser Name muss mit dem im Anforderungspfad angegebenen Namen übereinstimmen, andernfalls tritt der Fehler 400 (Fehlerhafte Anforderung) auf. |
| `description` | Eine für Menschen lesbare Beschreibung der Marketingaktion. |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 201 (Erstellt) und die Details der neu erstellten Marketingaktion zurück.

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
| `_links.self.href` | Die URI-ID der Marketingaktion. |

Zeichnen Sie die URI-ID der neu erstellten Marketingaktion auf, wie sie im nächsten Schritt der Erstellung einer DUL-Richtlinie verwendet wird.

## Eine DULE-Richtlinie erstellen {#create-policy}

Für das Erstellen einer neuen Richtlinie müssen Sie die URI-ID einer Marketingaktion mit einem Ausdruck der DULE-Beschriftungen angeben, die diese Marketingaktion verbieten.

Dieser Ausdruck wird als **Policy-Ausdruck** bezeichnet und ist ein Objekt, das entweder (A) eine DULE-Beschriftung oder (B) einen Operator und Operanden, aber nicht beide enthält. Jeder Operand ist wiederum ein Policy-Ausdruck-Objekt. So könnte beispielsweise eine Richtlinie über den Export von Daten an Dritte verboten werden, wenn `C1 OR (C3 AND C7)` Etiketten vorhanden sind. Dieser Ausdruck würde wie folgt definiert:

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

>[!NOTE] Nur OR- und AND-Operatoren werden unterstützt.

Nachdem Sie Ihren Policy Ausdruck konfiguriert haben, können Sie eine neue DULE-Richtlinie erstellen, indem Sie eine POST-Anforderung an den `/policies/custom` Endpunkt senden.

**API-Format**

```http
POST /policies/custom
```

**Anfrage**

Mit der folgenden Anforderung wird eine DULE-Richtlinie mit dem Namen &quot;Daten an Dritte exportieren&quot;erstellt, indem eine Marketingaktion und ein Richtlinien-Ausdruck in der Anforderungsnutzlast bereitgestellt werden.

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
| `marketingActionRefs` | Ein Array, das den `href` Wert einer Marketingaktion enthält, die im [vorherigen Schritt](#define-action)abgerufen wurde. Im obigen Beispiel wird zwar nur eine Marketingaktion Liste, es können aber auch mehrere Aktionen bereitgestellt werden. |
| `deny` | Das policy-Ausdruck-Objekt. Definiert die DULE-Beschriftungen und -Bedingungen, die dazu führen würden, dass die Richtlinie die in `marketingActionRefs`referenzierte Marketingaktion ablehnt. |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 201 (Erstellt) und die Details der neu erstellten Richtlinie zurück.

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

Zeichnen Sie die URI-ID der neu erstellten DUL-Richtlinie auf, wie sie im nächsten Schritt zum Aktivieren der Richtlinie verwendet wird.

## DULE-Richtlinie aktivieren

>[!NOTE] Dieser Schritt ist zwar optional, wenn Sie Ihre DULE-Richtlinie im `DRAFT` Status belassen möchten, beachten Sie jedoch, dass für eine Richtlinie der Status standardmäßig auf festgelegt sein muss, damit sie an der Auswertung teilnimmt. `ENABLED` Informationen zum Ausnehmen von Ausnahmen für Richtlinien im [Status finden Sie im Lernprogramm zum](../enforcement/api-enforcement.md) Erzwingen von DULE-Richtlinien `DRAFT` .

Standardmäßig beteiligen sich DULE-Richtlinien, deren `status` Eigenschaft auf &quot; `DRAFT` nicht bewerten&quot;eingestellt ist. Sie können Ihre Richtlinie zur Evaluierung aktivieren, indem Sie eine PATCH-Anforderung an den `/policies/custom/` Endpunkt senden und die eindeutige Kennung für die Richtlinie am Ende des Anforderungspfads angeben.

**API-Format**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{POLICY_ID}` | Der `id` Wert der Richtlinie, die aktiviert werden soll. |

**Anfrage**

Die folgende Anforderung führt einen PATCH-Vorgang für die `status` Eigenschaft der DUL-Richtlinie durch und ändert deren Wert von `DRAFT` in `ENABLED`.

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
| `op` | Der Typ des auszuführenden PATCH-Vorgangs. Diese Anforderung führt einen &quot;replace&quot;-Vorgang aus. |
| `path` | Der Pfad zum zu dem zu aktualisierenden Feld. Beim Aktivieren einer Richtlinie muss der Wert auf &quot;/status&quot;gesetzt werden. |
| `value` | Der neue Wert, der der Eigenschaft zugewiesen werden soll, die in `path`. Diese Anforderung setzt die `status` Eigenschaft der Richtlinie auf &quot;AKTIVIERT&quot;. |

**Antwort**

Bei einer erfolgreichen Antwort werden HTTP-Status 200 (OK) und die Details der aktualisierten Richtlinie zurückgegeben, wobei die `status` nun auf `ENABLED`eingestellt ist.

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

In diesem Lernprogramm haben Sie erfolgreich eine Datenverwendungsrichtlinie für eine Marketingaktion erstellt. Sie können nun das Lernprogramm zum [Erzwingen von Datenverwendungsrichtlinien](../enforcement/api-enforcement.md) fortsetzen, um zu erfahren, wie Sie in Ihrer Erlebnisanwendung nach Richtlinienverletzungen suchen und diese behandeln können.

Weitere Informationen zu den verschiedenen verfügbaren Vorgängen in der Policy Service API finden Sie im Entwicklerhandbuch für [Policy Service](../api/getting-started.md). Informationen zum Erzwingen von Richtlinien für Echtzeit-Kundendaten finden Sie im Lernprogramm zur [Erzwingung der Einhaltung von Datennutzungsregeln für Audiencen-Profil](../../segmentation/tutorials/governance.md).

Informationen zum Verwalten von Nutzungsrichtlinien in der Benutzeroberfläche der Experience Platform finden Sie im [Richtlinien-Benutzerhandbuch](user-guide.md).