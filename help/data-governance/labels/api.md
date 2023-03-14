---
keywords: Experience Platform;Home;beliebte Themen;Datenverwaltung;API für Datennutzungsbeschriftungen API;Richtlinien-Service-API
solution: Experience Platform
title: Verwalten von Datennutzungsbeschriftungen mit APIs
description: Mit der Datensatz-Service-API können Sie Nutzungsbezeichnungen für Datensätze anwenden und bearbeiten. Sie gehört zu den Datenkatalogfunktionen von Adobe Experience Platform, ist jedoch von der Katalog-Service-API getrennt, die Datensatz-Metadaten verwaltet.
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 100%

---


# Verwalten von Datennutzungsbeschriftungen mit APIs

In diesem Dokument wird beschrieben, wie Sie Datennutzungsbeschriftungen mit der [!DNL Policy Service]-API und der [!DNL Dataset Service]-API verwalten.

Die [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) stellt mehrere Endpunkte bereit, mit denen Sie Datennutzungsbeschriftungen für Ihr Unternehmen erstellen und verwalten können.

Mit der [!DNL Dataset Service]-API können Sie Nutzungsbezeichnungen für Datensätze anwenden und bearbeiten. Sie gehört zu den Datenkatalogfunktionen von Adobe Experience Platform, ist jedoch von der [!DNL Catalog Service]-API getrennt, die Datensatz-Metadaten verwaltet.

## Erste Schritte

Bevor Sie dieses Handbuch lesen, führen Sie die Schritte aus, die im [Abschnitt „Erste Schritte“](../../catalog/api/getting-started.md) im Katalogentwickler-Handbuch beschrieben sind, damit Sie über die erforderlichen Anmeldeinformationen für Aufrufe an [!DNL Platform]-APIs verfügen.

Um die in diesem Dokument beschriebenen [!DNL Dataset Service]-Endpunkte aufzurufen, müssen Sie über den eindeutigen `id`-Wert für einen bestimmten Datensatz verfügen. Wenn Sie diesen Wert nicht haben, finden Sie im Handbuch [Auflistung der Catalog-Objekte](../../catalog/api/list-objects.md) die IDs der vorhandenen Datensätze.

## Auflisten aller Bezeichnungen {#list-labels}

Mit der [!DNL Policy Service]-API können Sie alle `core`- oder `custom`-Beschriftungen durch eine GET-Anfrage an `/labels/core` bzw. `/labels/custom` auflisten.

**API-Format**

```http
GET /labels/core
GET /labels/custom
```

**Anfrage**

Mit der folgenden Anfrage werden alle benutzerdefinierten Beschriftungen aufgelistet, die im Rahmen Ihres Unternehmens erstellt wurden.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von benutzerdefinierten Beschriftungen zurück, die vom System abgerufen werden. Da die obige Beispielanforderung an `/labels/custom` erfolgte, zeigt die unten stehende Antwort nur benutzerdefinierte Beschriftungen an.

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## Nachschlagen einer Kennzeichnung {#look-up-label}

Sie können eine bestimmte Kennzeichnung nachschlagen, indem Sie die Eigenschaft `name` dieser Kennzeichnung in den Pfad einer GET-Anfrage an die [!DNL Policy Service]-API aufnehmen.

**API-Format**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{LABEL_NAME}` | Die Eigenschaft `name` der benutzerdefinierten Kennzeichnung, die Sie nachschlagen möchten. |

**Anfrage**

Die folgende Anfrage ruft die benutzerdefinierte Kennzeichnung `L2` ab, wie im Pfad angegeben.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der benutzerdefinierten Beschriftung zurück.

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{ORG_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## Erstellen oder Aktualisieren einer benutzerdefinierten Kennzeichnung {#create-update-label}

Um eine benutzerdefinierte Kennzeichnung zu erstellen oder zu aktualisieren, müssen Sie eine PUT-Anfrage an die [!DNL Policy Service]-API richten.

**API-Format**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{LABEL_NAME}` | Die Eigenschaft `name` einer benutzerdefinierten Kennzeichnung. Wenn keine benutzerdefinierte Beschriftung mit diesem Namen vorhanden ist, wird eine neue Beschriftung erstellt. Wenn eine vorhanden ist, wird diese Beschriftung aktualisiert. |

**Anfrage**

Mit der folgenden Anfrage wird eine neue Kennzeichnung (`L3`) erstellt, die Daten beschreiben soll, die Informationen zu den ausgewählten Zahlungsplänen der Kunden enthalten.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Eine eindeutige Zeichenfolgenkennung für die Beschriftung. Dieser Wert wird für Nachschlagezwecke und zum Anwenden der Beschriftung auf Datensätze und Felder verwendet. Es wird daher empfohlen, einen kurzen und knappen Wert zu wählen. |
| `category` | Die Kategorie der Beschriftung. Sie können zwar eigene Kategorien für benutzerdefinierte Kennzeichnungen erstellen, es wird jedoch dringend empfohlen, `Custom` zu verwenden, wenn die Kennzeichnung in der Benutzeroberfläche angezeigt werden soll. |
| `friendlyName` | Ein benutzerfreundlicher Name für die Beschriftung, der zu Anzeigezwecken verwendet wird. |
| `description` | (Optional) Eine Beschreibung der Beschriftung, um mehr Kontext bereitzustellen. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der benutzerdefinierten Beschriftung zurück, wobei HTTP-Code 200 (OK) bei einer Aktualisierung einer bestehenden Beschriftung oder 201 (Erstellt) bei einer neuen Beschriftung angezeigt wird.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{ORG_ID}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## Suchen nach Kennzeichnungen für einen Datensatz {#look-up-dataset-labels}

Sie können die Datennutzungskennzeichnungen nachschlagen, die auf einen vorhandenen Datensatz angewendet wurden, indem Sie eine GET-Anfrage an die [!DNL Dataset Service]-API stellen.

**API-Format**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige `id`-Wert des Datensatzes, dessen Kennzeichnungen Sie nachschlagen möchten. |

**Anfrage**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Datennutzungsbeschriftungen zurück, die auf den Datensatz angewendet wurden.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{ORG_ID}",
    "labels": [ "C1", "C2", "C3", "I1", "I2" ],
    "optionalLabels": [
      {
        "option": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
          "contentType": "application/vnd.adobe.xed-full+json;version=1",
          "schemaPath": "/properties/repositoryCreatedBy"
        },
        "labels": [ "S1", "S2" ]
      }
    ]
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `labels` | Eine Liste von Datennutzungsbeschriftungen, die auf den Datensatz angewendet wurden. |
| `optionalLabels` | Eine Liste einzelner Felder im Datensatz, auf die Datennutzungsbeschriftungen angewendet werden bzw. wurden. Folgende Untereigenschaften sind erforderlich:<br/><br/>`option`: Ein Objekt, das die [!DNL Experience Data Model] (XDM)-Attribute des Felds enthält. Die folgenden drei Eigenschaften sind erforderlich:<ul><li>`id`: Der URI-`$id`-Wert des Schemas, das dem Feld zugeordnet ist.</li><li>`contentType`: Gibt das Format und die Version des Schemas an. Weitere Informationen finden Sie im Abschnitt zur [Schemaversionierung](../../xdm/api/getting-started.md#versioning) im XDM-API-Handbuch.</li><li>`schemaPath`: Der Pfad zur betreffenden Schemaeigenschaft, geschrieben in [JSON Pointer](../../landing/api-fundamentals.md#json-pointer)-Syntax.</li></ul>`labels`: Eine Liste von Datennutzungskennzeichnungen, die Sie zu dem Feld hinzufügen möchten. |

- id: Der URI $id -Wert für das XDM-Schema, auf dem der Datensatz basiert.
- contentType: Gibt das Format und die Version des Schemas an. Weitere Informationen finden Sie im Abschnitt zur [Schemaversionierung](../../xdm/api/getting-started.md#versioning) im XDM-API-Handbuch.
- schemaPath: Der Pfad zur betreffenden Schemaeigenschaft, geschrieben in der [JSON Pointer](../../landing/api-fundamentals.md#json-pointer)-Syntax.

## Anwenden von Kennzeichnungen auf einen Datensatz {#apply-dataset-labels}

Sie können einen Satz von Kennzeichnungen für einen Datensatz erstellen, indem Sie sie in der Payload einer POST- oder PUT-Anfrage an die [!DNL Dataset Service]-API bereitstellen. Wenn Sie eine dieser Methoden verwenden, werden vorhandene Beschriftungen überschrieben und durch die in der Payload bereitgestellten ersetzt.

**API-Format**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige `id`-Wert des Datensatzes, für den Sie Kennzeichnungen erstellen. |

**Anfrage**

Mit der folgenden POST-Anfrage werden dem Datensatz sowie einem bestimmten Feld in diesem Datensatz eine Reihe von Beschriftungen hinzugefügt. Die in der Payload bereitgestellten Felder entsprechen den Feldern, die für eine PUT-Anfrage erforderlich sind.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "labels": [ "C1", "C2", "C3", "I1", "I2" ],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/repositoryCreatedBy"
            },
            "labels": [ "S1", "S2" ]
          }
        ]
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `labels` | Eine Liste von Datennutzungsbeschriftungen, die Sie dem Datensatz hinzufügen möchten. |
| `optionalLabels` | Eine Liste der einzelnen Felder im Datensatz, denen Sie Beschriftungen hinzufügen möchten. Jedes Element in diesem Array muss die folgenden Eigenschaften aufweisen:<br/><br/>`option`Ein Objekt, das die [!DNL Experience Data Model] (XDM)-Attribute des Felds enthält. Die folgenden drei Eigenschaften sind erforderlich:<ul><li>`id`: Der URI-`$id`-Wert des Schemas, das dem Feld zugeordnet ist.</li><li>`contentType`: Gibt das Format und die Version des Schemas an. Weitere Informationen finden Sie im Abschnitt zur [Schemaversionierung](../../xdm/api/getting-started.md#versioning) im XDM-API-Handbuch.</li><li>`schemaPath`: Der Pfad zur betreffenden Schemaeigenschaft, geschrieben in [JSON Pointer](../../landing/api-fundamentals.md#json-pointer)-Syntax.</li></ul>`labels`: Eine Liste von Datennutzungskennzeichnungen, die Sie zu dem Feld hinzufügen möchten. |

**Antwort**

Eine erfolgreiche Antwort gibt die Kennzeichnungen zurück, die dem Datensatz hinzugefügt wurden.

```json
{
  "labels": [ "C1", "C2", "C3", "I1", "I2" ],
  "optionalLabels": [
    {
      "option": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
        "contentType": "application/vnd.adobe.xed-full+json;version=1",
        "schemaPath": "/properties/repositoryCreatedBy"
      },
      "labels": [ "S1", "S2" ]
    }
  ]
}
```

## Entfernen von Kennzeichnungen aus einem Datensatz {#remove-dataset-labels}

Sie können die auf einen Datensatz angewendeten Kennzeichnungen entfernen, indem Sie eine DELETE-Anfrage an die [!DNL Dataset Service]-API stellen.

**API-Format**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige `id`-Wert des Datensatzes, dessen Kennzeichnungen Sie entfernen möchten. |

**Anfrage**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

HTTP-Status 200 (OK) einer erfolgreichen Antwort, der angibt, dass die Kennzeichnungen entfernt wurden. Sie können die vorhandenen Bezeichnungen für den Datensatz in einem separaten Aufruf [nachschlagen](#look-up-dataset-labels), um dies zu bestätigen.

## Nächste Schritte

In diesem Dokument haben Sie gelernt, wie Sie Datennutzungs-Kennzeichnungen mithilfe von APIs verwalten können.

Nachdem Sie Datennutzungs-Kennzeichnungen auf der Datensatz- und Feldebene hinzugefügt haben, können Sie beginnen, Daten in [!DNL Experience Platform] zu erfassen. Um mehr darüber zu erfahren, lesen Sie zunächst die [Dokumentation zur Datenaufnahme](../../ingestion/home.md).

Sie können jetzt auch Datennutzungsrichtlinien auf Basis der von Ihnen angewendeten Kennzeichnungen definieren. Weitere Informationen finden Sie unter [Datennutzungsrichtlinien – Übersicht](../policies/overview.md).

Weitere Informationen zum Verwalten von Datensätzen in [!DNL Experience Platform] finden Sie unter [Datensätze – Übersicht](../../catalog/datasets/overview.md).