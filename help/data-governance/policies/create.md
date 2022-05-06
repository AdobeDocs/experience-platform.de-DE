---
keywords: Experience Platform;Startseite;beliebte Themen;Daten-Governance;Datennutzungsrichtlinie
solution: Experience Platform
title: Eine Datennutzungsrichtlinie in der API erstellen
topic-legacy: policies
type: Tutorial
description: Mit der Policy Service-API können Sie Datennutzungsrichtlinien erstellen und verwalten, die bestimmen, welche Marketing-Aktionen für Daten entsprechend deren Datennutzungskennzeichnungen durchgeführt werden können. Dieses Dokument enthält eine schrittweise Anleitung zum Erstellen einer Datennutzungsrichtlinie mithilfe der Policy Service-API.
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 100%

---

# Eine Datennutzungsrichtlinie in der API erstellen

Mit der [Policy Service-API](https://www.adobe.io/experience-platform-apis/references/policy-service/) können Sie Datennutzungsrichtlinien erstellen und verwalten, um festzulegen, welche Marketing-Aktionen für Daten mit bestimmten Datennutzungskennzeichnungen ausgeführt werden können.

Dieses Dokument enthält eine schrittweise Anleitung zum Erstellen einer Datennutzungsrichtlinie mithilfe der [!DNL Policy Service]-API. Eine genauere Anleitung zu den verschiedenen in der API verfügbaren Vorgängen finden Sie im [Entwicklerhandbuch für Policy Service](../api/getting-started.md).

## Erste Schritte

Diese Anleitung setzt ein Verständnis der folgenden Schlüsselkonzepte voraus, die beim Erstellen und Evaluieren von Datennutzungsrichtlinien zum Einsatz kommen:

* [Adobe Experience Platform-Daten-Governance](../home.md): Der Rahmen, mit dem durch [!DNL Platform] die korrekte Datenverwendung erzwungen wird.
   * [Datennutzungsbezeichnungen](../labels/overview.md): Datennutzungsbezeichnungen werden auf XDM-Datenfelder angewendet und geben Einschränkungen für den Zugriff auf diese Daten an.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Bevor Sie mit dieser Anleitung beginnen, lesen Sie das [Entwicklerhandbuch](../api/getting-started.md), um wichtige Informationen zu erhalten, die Sie für die erfolgreiche Durchführung von Aufrufen an die [!DNL Policy Service]-API benötigen, einschließlich erforderlicher Kopfzeilen und Anweisungen zum Lesen von Beispiel-API-Aufrufen.

## Marketing-Aktion definieren {#define-action}

Im Data Governance-Framework ist eine Marketing-Aktion eine Aktion, die ein [!DNL Experience Platform]-Datennutzer durchführt und bei der überprüft werden muss, ob Datennutzungsrichtlinien verletzt wurden.

Der erste Schritt bei der Erstellung einer Datennutzungsrichtlinie besteht darin, zu bestimmen, welche Marketing-Aktion durch die Richtlinie bewertet werden soll. Dies kann mit einer der folgenden Optionen erledigt werden:

* [Vorhandene Marketing-Aktion nachschlagen](#look-up)
* [Neue Marketing-Aktion erstellen](#create-new)

### Vorhandene Marketing-Aktion nachschlagen {#look-up}

Sie können vorhandene Marketing-Aktionen nachschlagen, die von Ihrer Datennutzungsrichtlinie bewertet werden sollen, indem Sie eine GET-Anfrage an einen der `/marketingActions`-Endpunkte senden.

**API-Format**

Je nachdem, ob Sie eine Marketing-Aktion von [!DNL Experience Platform] oder eine benutzerdefinierte Marketing-Aktion Ihrer Organisation nachschlagen, verwenden Sie die Endpunkte `marketingActions/core` bzw. `marketingActions/custom`.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

Wenn Sie die Marketing-Aktion gefunden haben, die Sie verwenden möchten, notieren Sie sich den Wert seiner `href`-Eigenschaft. Dieser Wert wird im nächsten Schritt zum [Erstellen einer Richtlinie](#create-policy) benötigt.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

Notieren Sie sich die URI-ID der neu erstellten Marketing-Aktion, da Sie sie im nächsten Schritt beim Erstellen einer Richtlinie benötigen werden.

## Erstellen einer Richtlinie {#create-policy}

Für das Erstellen einer neuen Richtlinie müssen Sie die URI-ID einer Marketing-Aktion mit einem Ausdruck der Datennutzungskennzeichnungen angeben, bei denen diese Marketing-Aktion verboten ist.

Dieser Ausdruck wird als Richtlinienausdruck bezeichnet und ist ein Objekt, das entweder (A) eine Kennzeichnung oder (B) einen Operator und Operanden enthält, aber nicht beides. Jeder Operand ist wiederum ein Richtlinienausdrucksobjekt. So könnte beispielsweise eine Richtlinie für den Export von Daten an eine Drittpartei verboten werden, wenn `C1 OR (C3 AND C7)`-Kennzeichnungen vorhanden sind. Dieser Ausdruck würde wie folgt definiert:

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

Nachdem Sie Ihren Richtlinienausdruck konfiguriert haben, können Sie eine neue Richtlinie erstellen, indem Sie eine POST-Anfrage an den `/policies/custom`-Endpunkt senden.

**API-Format**

```http
POST /policies/custom
```

**Anfrage**

Mit der folgenden Anfrage wird eine Richtlinie mit dem Namen „Daten an Dritte exportieren“ erstellt, indem in der Payload der Anfrage eine Marketing-Aktion und ein Richtlinienausdruck angegeben werden.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `deny` | Das Richtlinienausdrucksobjekt. Definiert die Datennutzungskennzeichnungen und -bedingungen, die dazu führen würden, dass die Richtlinie die in `marketingActionRefs` referenzierte Marketing-Aktion verbietet. |

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
    "imsOrg": "{ORG_ID}",
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

Notieren Sie sich die URI-ID der neu erstellten Richtlinie, da Sie sie im nächsten Schritt zum Aktivieren der Richtlinie benötigen.

## Richtlinie aktivieren

>[!NOTE]
>
>Dieser Schritt ist optional, wenn Sie Ihre Richtlinie im Status `DRAFT` belassen möchten; beachten Sie jedoch, dass für eine Richtlinie der Status standardmäßig auf `ENABLED` festgelegt sein muss, damit sie in die Auswertung einbezogen wird. Informationen zur Verwendung von Ausnahmen für Richtlinien mit dem Status `DRAFT` finden Sie im Handbuch zum [Durchsetzen von Richtlinien](../enforcement/api-enforcement.md).

Standardmäßig werden Richtlinien, deren `status`-Eigenschaft auf `DRAFT` gesetzt ist, nicht in die Auswertung einbezogen. Sie können Ihre Richtlinie für die Bewertung aktivieren, indem Sie eine PATCH-Anfrage an den `/policies/custom/`-Endpunkt senden und am Ende des Anfragepfads die eindeutige Kennung für die Richtlinie angeben.

**API-Format**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{POLICY_ID}` | Der `id`-Wert der Richtlinie, die aktiviert werden soll. |

**Anfrage**

Die folgende Anfrage führt einen PATCH-Vorgang für die `status`-Eigenschaft der Richtlinie aus und ändert deren Wert von `DRAFT` in `ENABLED`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

Weiterführende Informationen zu den verschiedenen verfügbaren Vorgängen in der [!DNL Policy Service]-API finden Sie im [Entwicklerhandbuch für Policy Service](../api/getting-started.md). Informationen zum Durchsetzen von Richtlinien für [!DNL Real-time Customer Profile]-Daten finden Sie im Tutorial zum [Durchsetzen der Einhaltung von Datennutzungsregeln für Zielgruppensegmente](../../segmentation/tutorials/governance.md).

Informationen zum Verwalten von Nutzungsrichtlinien in der Benutzeroberfläche von [!DNL Experience Platform] finden Sie im [Benutzerhandbuch für Richtlinien](user-guide.md).
