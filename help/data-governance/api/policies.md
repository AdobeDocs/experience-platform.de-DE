---
keywords: Experience Platform;Startseite;beliebte Themen;Richtliniendurchsetzung;API-basierte Durchsetzung;Datenverwaltung
solution: Experience Platform
title: Richtlinien-API-Endpunkt
topic-legacy: developer guide
description: Datennutzungsrichtlinien sind von Ihrem Unternehmen angewandte Regeln, die die Arten von Marketing-Aktionen beschreiben, die Sie für Daten in der Experience Platform ausführen bzw. nicht ausführen dürfen. Der Endpunkt „/policies“ wird für alle API-Aufrufe zum Anzeigen, Erstellen, Aktualisieren oder Löschen von Datennutzungsrichtlinien verwendet.
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1813'
ht-degree: 100%

---

# Richtlinien-Endpunkt

Datennutzungsrichtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, die Sie für Daten in [!DNL Experience Platform] ausführen bzw. nicht ausführen dürfen. Mit dem `/policies`-Endpunkt in der [!DNL Policy Service API] können Sie Datennutzungsrichtlinien für Ihr Unternehmen programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Bevor Sie fortfahren, lesen Sie im Handbuch [Erste Schritte](getting-started.md) die Links zu entsprechenden Dokumentationen, den Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Abrufen einer Liste von Richtlinien {#list}

Sie können alle `core`- oder `custom`-Richtlinien durch eine GET-Anfrage an `/policies/core` bzw. `/policies/custom` auflisten.

**API-Format**

```http
GET /policies/core
GET /policies/custom
```

**Anfrage**

Die folgende Anfrage ruft eine Liste von benutzerdefinierten Richtlinien ab, die von Ihrem Unternehmen definiert wurden.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort enthält ein `children`-Array, das die Details der einzelnen abgerufenen Richtlinien einschließlich ihrer `id`-Werte auflistet. Sie können das Feld `id` einer bestimmten Richtlinie verwenden, um [Such](#lookup)-, [Aktualisierungs](#update)- und [Löschanfragen](#delete) für diese Richtlinie auszuführen.

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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `status` | Der aktuelle Status einer Richtlinie. Es gibt drei mögliche Status: `DRAFT`, `ENABLED` oder `DISABLED`. Standardmäßig werden nur Richtlinien vom Typ `ENABLED` in die Auswertung einbezogen. Weitere Informationen finden Sie in der Übersicht zur [Richtlinienauswertung](../enforcement/overview.md). |
| `marketingActionRefs` | Ein Array, das die URIs aller für eine Richtlinie möglichen Marketing-Aktionen auflistet. |
| `description` | Eine optionale Beschreibung, die zusätzlichen Kontext zum Anwendungsfall der Richtlinie bietet. |
| `deny` | Ein Objekt, das die spezifischen Datennutzungskennzeichnungen beschreibt, bei denen die einer Richtlinie zugeordnete Marketing-Aktion nicht ausgeführt werden darf. Weitere Informationen zu dieser Eigenschaft finden Sie im Abschnitt [Erstellen einer Richtlinie](#create-policy). |

## Suchen einer Richtlinie {#look-up}

Sie können eine bestimmte Richtlinie suchen, indem Sie die Eigenschaft `id` dieser Richtlinie in den Pfad einer GET-Anfrage einbeziehen.

**API-Format**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{POLICY_ID}` | Die `id` der Richtlinie, die Sie suchen möchten. |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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
| `status` | Der aktuelle Status der Richtlinie. Es gibt drei mögliche Status: `DRAFT`, `ENABLED` oder `DISABLED`. Standardmäßig werden nur Richtlinien vom Typ `ENABLED` in die Auswertung einbezogen. Weitere Informationen finden Sie in der Übersicht zur [Richtlinienauswertung](../enforcement/overview.md). |
| `marketingActionRefs` | Ein Array, das die URIs aller für die Richtlinie geltenden Marketing-Aktionen auflistet. |
| `description` | Eine optionale Beschreibung, die zusätzlichen Kontext zum Anwendungsfall der Richtlinie bietet. |
| `deny` | Ein Objekt, das die spezifischen Datennutzungskennzeichnungen beschreibt, bei denen die der Richtlinie zugeordnete Marketing-Aktion nicht ausgeführt werden darf. Weitere Informationen zu dieser Eigenschaft finden Sie im Abschnitt [Erstellen einer Richtlinie](#create-policy). |

## Erstellen einer benutzerdefinierten Richtlinie {#create-policy}

In der [!DNL Policy Service]-API wird eine Richtlinie wie folgt definiert:

* Ein Verweis auf eine bestimmte Marketing-Aktion
* Ein Ausdruck, der die Datennutzungskennzeichnungen beschreibt, bei denen die Marketing-Aktion nicht ausgeführt werden darf.

Um diese Anforderung zu erfüllen, müssen Richtliniendefinitionen einen booleschen Ausdruck zum Vorhandensein von Datennutzungskennzeichnungen enthalten. Dieser Ausdruck wird als Richtlinienausdruck bezeichnet.

Richtlinienausdrücke werden in jeder Richtliniendefinition in Form einer `deny`-Eigenschaft bereitgestellt. Ein Beispiel für ein einfaches `deny`-Objekt, das nur das Vorhandensein einer einzelnen Kennzeichnung prüft, würde wie folgt aussehen:

```json
"deny": {
    "label": "C1"
}
```

In vielen Richtlinien werden jedoch komplexere Bedingungen für das Vorhandensein von Datennutzungskennzeichnungen spezifiziert. Um diese Anwendungsfälle zu unterstützen, können Sie auch boolesche Operationen zur Beschreibung Ihrer Richtlinienausdrücke einschließen. Das Objekt des Richtlinienausdrucks muss entweder eine Kennzeichnung oder einen Operator und Operanden enthalten, jedoch nicht beides. Jeder Operand ist wiederum ein Richtlinienausdrucksobjekt.

Um beispielsweise eine Richtlinie zu definieren, die die Ausführung einer Marketing-Aktion in Bezug auf Daten verbietet, bei denen `C1 OR (C3 AND C7)`-Kennzeichnungen vorhanden sind, wird die `deny`-Eigenschaft der Richtlinie wie folgt angegeben:

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
| `operator` | Gibt die bedingte Beziehung zwischen den Kennzeichnungen an, die im gleichrangigen `operands`-Array bereitgestellt werden. Akzeptierte Werte sind: <ul><li>`OR`: Der Ausdruck wird in „true“ aufgelöst, wenn eine der Kennzeichnungen im `operands`-Array vorhanden ist.</li><li>`AND`: Der Ausdruck wird nur dann in „true“ aufgelöst, wenn alle Kennzeichnungen im `operands`-Array vorhanden sind.</li></ul> |
| `operands` | Ein Array von Objekten, wobei jedes Objekt entweder eine einzelne Kennzeichnung oder ein zusätzliches Paar der Eigenschaften `operator` und `operands` darstellt. Das Vorhandensein der Kennzeichnungen und/oder Operationen in einem `operands`-Array wird je nach dem Wert der zugehörigen `operator`-Eigenschaft in „true“ oder „false“ aufgelöst. |
| `label` | Der Name einer einzelnen Datenverwendungskennzeichnung, die für die Richtlinie gilt. |

Sie können eine neue benutzerdefinierte Richtlinie erstellen, indem Sie eine POST-Anfrage an den `/policies/custom`-Endpunkt senden.

**API-Format**

```http
POST /policies/custom
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Richtlinie, die die Ausführung der Marketing-Aktion `exportToThirdParty` auf Daten mit den Kennzeichnungen `C1 OR (C3 AND C7)` einschränkt.

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
| `status` | Der aktuelle Status der Richtlinie. Es gibt drei mögliche Status: `DRAFT`, `ENABLED` oder `DISABLED`. Standardmäßig werden nur Richtlinien vom Typ `ENABLED` in die Auswertung einbezogen. Weitere Informationen finden Sie in der Übersicht zur [Richtlinienauswertung](../enforcement/overview.md). |
| `marketingActionRefs` | Ein Array, das die URIs aller für die Richtlinie geltenden Marketing-Aktionen auflistet. Der URI für eine Marketing-Aktion wird unter `_links.self.href` in der Antwort für [Suchen einer Marketing-Aktion](./marketing-actions.md#look-up) bereitgestellt. |
| `description` | Eine optionale Beschreibung, die zusätzlichen Kontext zum Anwendungsfall der Richtlinie bietet. |
| `deny` | Der Richtlinienausdruck, der die spezifischen Datenverwendungskennzeichnungen beschreibt, bei denen die der Richtlinie zugeordnete Marketing-Aktion nicht ausgeführt werden darf. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Richtlinie zurück, darunter auch die `id`. Dieser Wert ist schreibgeschützt und wird beim Erstellen der Richtlinie automatisch zugewiesen.

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
    "imsOrg": "{ORG_ID}",
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
>Sie können nur benutzerdefinierte Richtlinien aktualisieren. Wenn Sie Kernrichtlinien aktivieren oder deaktivieren möchten, lesen Sie den Abschnitt [Aktualisieren der Liste der aktivierten Kernrichtlinien](#update-enabled-core).

Sie können eine vorhandene benutzerdefinierte Richtlinie aktualisieren, indem Sie ihre ID im Pfad einer PUT-Anfrage mit einer Payload angeben, die die vollständige aktualisierte Form der Richtlinie enthält. Mit anderen Worten, wird die Richtlinie durch die PUT-Anfrage neu geschrieben.

>[!NOTE]
>
>Siehe Abschnitt [Aktualisieren eines Teils einer benutzerdefinierten Richtlinie](#patch), wenn Sie nur eines oder mehrere Felder für eine Richtlinie aktualisieren möchten, anstatt sie zu überschreiben.

**API-Format**

```http
PUT /policies/custom/{POLICY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{POLICY_ID}` | Der `id` der Richtlinie, die Sie aktualisieren möchten. |

**Anfrage**

In diesem Beispiel haben sich die Bedingungen für den Export von Daten an einen Drittanbieter geändert. Daher muss die von Ihnen erstellte Richtlinie diese Marketing-Aktion jetzt ablehnen, wenn `C1 AND C5`-Datenbezeichnungen vorhanden sind.

Mit der folgenden Anfrage wird die vorhandene Richtlinie so aktualisiert, dass sie den neuen Richtlinienausdruck enthält. Beachten Sie, dass alle Felder in die Payload einbezogen werden müssen, da diese Anfrage die Richtlinie im Wesentlichen neu schreibt, auch wenn einige ihrer Werte nicht aktualisiert werden.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
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
| `status` | Der aktuelle Status der Richtlinie. Es gibt drei mögliche Status: `DRAFT`, `ENABLED` oder `DISABLED`. Standardmäßig werden nur Richtlinien vom Typ `ENABLED` in die Auswertung einbezogen. Weitere Informationen finden Sie in der Übersicht zur [Richtlinienauswertung](../enforcement/overview.md). |
| `marketingActionRefs` | Ein Array, das die URIs aller für die Richtlinie geltenden Marketing-Aktionen auflistet. Der URI für eine Marketing-Aktion wird unter `_links.self.href` in der Antwort für [Suchen einer Marketing-Aktion](./marketing-actions.md#look-up) bereitgestellt. |
| `description` | Eine optionale Beschreibung, die zusätzlichen Kontext zum Anwendungsfall der Richtlinie bietet. |
| `deny` | Der Richtlinienausdruck, der die spezifischen Datenverwendungskennzeichnungen beschreibt, bei denen die der Richtlinie zugeordnete Marketing-Aktion nicht ausgeführt werden darf. Weitere Informationen zu dieser Eigenschaft finden Sie im Abschnitt [Erstellen einer Richtlinie](#create-policy). |

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
    "imsOrg": "{ORG_ID}",
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

## Aktualisieren eines Teils einer benutzerdefinierten Richtlinie {#patch}

>[!IMPORTANT]
>
>Sie können nur benutzerdefinierte Richtlinien aktualisieren. Wenn Sie Kernrichtlinien aktivieren oder deaktivieren möchten, lesen Sie den Abschnitt über das [Aktualisieren der Liste der aktivierten Kernrichtlinien](#update-enabled-core).

Ein bestimmter Teil einer Richtlinie kann mithilfe einer PATCH-Anfrage aktualisiert werden. Im Gegensatz zu PUT-Anfragen, die die Richtlinie neu schreiben, aktualisieren PATCH-Anfragen nur die in der Anfrage angegebenen Eigenschaften. Dies ist besonders hilfreich, wenn Sie eine Richtlinie aktivieren oder deaktivieren möchten, da Sie nur den Pfad zur entsprechenden Eigenschaft (`/status`) und deren Wert (`ENABLED` oder `DISABLED`) angeben müssen.

>[!NOTE]
>
>Payloads für PATCH-Anfragen müssen das JSON-Patch-Format besitzen. Weitere Informationen zur verwendeten Syntax finden Sie im [Handbuch zu den API-Grundlagen](../../landing/api-fundamentals.md).

Die [!DNL Policy Service]-API unterstützt die JSON-Patch-Vorgänge `add`, `remove` und `replace` und ermöglicht Ihnen, mehrere Updates zu einem einzigen Aufruf zusammenzufassen, wie im Beispiel unten dargestellt.

**API-Format**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{POLICY_ID}` | Die `id` der Richtlinie, deren Eigenschaften Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage verwendet zwei `replace`-Vorgänge, um den Richtlinienstatus von `DRAFT` in `ENABLED` zu ändern und das Feld `description` mit einer neuen Beschreibung zu aktualisieren.

>[!IMPORTANT]
>
>Wenn mehrere PATCH-Vorgänge in einer einzigen Anfrage gesendet werden, werden sie in der Reihenfolge verarbeitet, in der sie im Array angezeigt werden. Vergewissern Sie sich, dass Sie gegebenenfalls die Anfragen in der richtigen Reihenfolge senden.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

Sie können eine benutzerdefinierte Richtlinie löschen, indem Sie deren `id` im Pfad einer DELETE-Anfrage angeben.

>[!WARNING]
>
>Nach dem Löschen können Richtlinien nicht wiederhergestellt werden. Es empfiehlt sich, zuerst [eine Suchanfrage (GET) durchzuführen](#lookup), um die Richtlinie anzuzeigen und zu bestätigen, dass es sich um die richtige Richtlinie handelt, die Sie entfernen möchten.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 (OK) mit einem leeren Text zurück.

Sie können den Löschvorgang überprüfen, indem Sie erneut versuchen, nach der Richtlinie zu suchen (GET). Sie sollten den HTTP-404-Fehler (Nicht gefunden) erhalten, wenn die Richtlinie erfolgreich gelöscht wurde.

## Eine Liste von aktivierten Kernrichtlinien abrufen {#list-enabled-core}

Standardmäßig werden nur aktivierte Datennutzungsrichtlinien in die Auswertung einbezogen. Sie können eine Liste der derzeit von Ihrem Unternehmen aktivierten Kernrichtlinien abrufen, indem Sie eine GET-Anfrage an den `/enabledCorePolicies`-Endpunkt stellen.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Liste der aktivierten Kernrichtlinien unter einem `policyIds`-Array zurück.

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
  "imsOrg": "{ORG_ID}",
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

## Aktualisieren der Liste der aktivierten Kernrichtlinien {#update-enabled-core}

Standardmäßig werden nur aktivierte Datennutzungsrichtlinien in die Auswertung einbezogen. Wenn Sie eine PUT-Anfrage an den `/enabledCorePolicies`-Endpunkt stellen, können Sie die Liste der aktivierten Kernrichtlinien für Ihr Unternehmen mit einem einzigen Aufruf aktualisieren.

>[!NOTE]
>
>Nur Kernrichtlinien können von diesem Endpunkt aktiviert oder deaktiviert werden. Informationen zum Aktivieren oder Deaktivieren benutzerdefinierter Richtlinien finden Sie im Abschnitt [Aktualisieren eines Teils einer Richtlinie](#patch).

**API-Format**

```http
PUT /enabledCorePolicies
```

**Anfrage**

Die folgende Anfrage aktualisiert die Liste der aktivierten Kernrichtlinien auf der Grundlage der in der Payload enthaltenen IDs.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `policyIds` | Eine Liste der IDs der zu aktivierenden Kernrichtlinien. Alle nicht eingeschlossenen Kernrichtlinien sind auf den Status `DISABLED` gesetzt und werden bei der Auswertung nicht berücksichtigt. |

**Antwort**

Eine erfolgreiche Antwort gibt die aktualisierte Liste der aktivierten Kernrichtlinien unter einem `policyIds`-Array zurück.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{ORG_ID}",
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

Nachdem Sie neue Richtlinien definiert oder vorhandene aktualisiert haben, können Sie die [!DNL Policy Service]-API verwenden, um Marketing-Aktionen mit bestimmten Kennzeichnungen oder Datensätzen zu testen und festzustellen, ob Ihre Richtlinien zu erwarteten Verstößen führen. Weitere Informationen finden Sie im Handbuch zu den [Endpunkten der Richtlinienauswertung](./evaluation.md).
