---
keywords: Experience Platform;Startseite;beliebte Themen;Datenverwaltung;Datenverwendungsbeschriftung API;Policy-Dienst-API
solution: Experience Platform
title: 'Verwalten von Datenverwendungsbezeichnungen mithilfe von APIs '
topic-legacy: developer guide
description: Mit der DataSet-Dienst-API können Sie Nutzungsbezeichnungen für Datensätze anwenden und bearbeiten. Es gehört zu den Funktionen des Adobe Experience Platform-Datenkatalogs, ist jedoch von der Katalogdienst-API getrennt, die die Metadaten des Datensatzes verwaltet.
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 4%

---


# Verwalten von Datenverwendungsbeschriftungen mit APIs

In diesem Dokument wird beschrieben, wie Sie Datenverwendungsbeschriftungen mit der API [!DNL Policy Service] und der [!DNL Dataset Service]-API verwalten.

Das [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) stellt mehrere Endpunkte bereit, mit denen Sie Datenverwendungsbeschriftungen für Ihr Unternehmen erstellen und verwalten können.

Mit der API [!DNL Dataset Service] können Sie Nutzungsbezeichnungen für Datensätze anwenden und bearbeiten. Es gehört zu den Datenkatalogfunktionen von Adobe Experience Platform, ist jedoch von der [!DNL Catalog Service]-API getrennt, die DataSet-Metadaten verwaltet.

## Erste Schritte

Bevor Sie dieses Handbuch lesen, führen Sie die Schritte aus, die im Abschnitt [Erste Schritte](../../catalog/api/getting-started.md) im Catalog Developer-Handbuch beschrieben sind, um die erforderlichen Anmeldeinformationen für Aufrufe an [!DNL Platform]-APIs zu sammeln.

Um die in diesem Dokument beschriebenen [!DNL Dataset Service]-Endpunkte aufzurufen, müssen Sie über den eindeutigen `id`-Wert für einen bestimmten Datensatz verfügen. Wenn Sie diesen Wert nicht haben, finden Sie im Handbuch [Auflistung der Katalogobjekte](../../catalog/api/list-objects.md) die IDs der vorhandenen Datensätze.

## Liste aller Bezeichnungen {#list-labels}

Mit der API [!DNL Policy Service] können Sie alle `core`- oder `custom`-Beschriftungen durch eine GET an `/labels/core` bzw. `/labels/custom` Liste durchführen.

**API-Format**

```http
GET /labels/core
GET /labels/custom
```

**Anfrage**

Die folgende Anforderung Liste alle benutzerdefinierten Beschriftungen, die im Rahmen Ihres Unternehmens erstellt wurden.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von benutzerdefinierten Beschriftungen zurück, die vom System abgerufen werden. Da die obige Beispielanforderung an `/labels/custom` erfolgte, zeigt die unten stehende Antwort nur benutzerdefinierte Bezeichnungen an.

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

## Suchen Sie eine Beschriftung {#look-up-label}

Sie können eine bestimmte Beschriftung nachschlagen, indem Sie die `name`-Eigenschaft dieser Beschriftung in den Pfad einer GET-Anforderung zur [!DNL Policy Service]-API aufnehmen.

**API-Format**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{LABEL_NAME}` | Die `name`-Eigenschaft der benutzerdefinierten Beschriftung, die Sie nachschlagen möchten. |

**Anfrage**

Die folgende Anforderung ruft die benutzerdefinierte Beschriftung `L2` ab, wie im Pfad angegeben.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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

## Erstellen oder aktualisieren Sie eine benutzerdefinierte Beschriftung {#create-update-label}

Um eine benutzerdefinierte Bezeichnung zu erstellen oder zu aktualisieren, müssen Sie eine PUT an die [!DNL Policy Service]-API anfordern.

**API-Format**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{LABEL_NAME}` | Die `name`-Eigenschaft einer benutzerdefinierten Bezeichnung. Wenn keine benutzerdefinierte Bezeichnung mit diesem Namen vorhanden ist, wird eine neue Bezeichnung erstellt. Wenn eine vorhanden ist, wird diese Bezeichnung aktualisiert. |

**Anfrage**

Mit der folgenden Anforderung wird ein neues Etikett (`L3`) erstellt, das Daten beschreiben soll, die Informationen zu den ausgewählten Zahlungsplänen der Kunden enthalten.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Eine eindeutige Zeichenfolgenkennung für die Bezeichnung. Dieser Wert wird für Nachschlagezwecke und die Anwendung der Beschriftung auf Datensätze und Felder verwendet. Es wird daher empfohlen, kurz und knapp zu sein. |
| `category` | Die Kategorie des Etiketts. Sie können zwar eigene Kategorien für benutzerdefinierte Beschriftungen erstellen, es wird jedoch dringend empfohlen, `Custom` zu verwenden, wenn die Beschriftung in der Benutzeroberfläche angezeigt werden soll. |
| `friendlyName` | Ein benutzerfreundlicher Name für die Beschriftung, der zu Anzeigezwecken verwendet wird. |
| `description` | (Optional) Eine Beschreibung der Beschriftung, um einen weiteren Kontext bereitzustellen. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der benutzerdefinierten Beschriftung zurück, wobei HTTP-Code 200 (OK) bei einer Aktualisierung einer bestehenden Beschriftung oder 201 (Erstellt) bei einer neuen Beschriftung.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{IMS_ORG}",
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

## Suchen Sie nach Beschriftungen für einen Datensatz {#look-up-dataset-labels}

Sie können die Datenverwendungsbeschriftungen nachschlagen, die auf einen vorhandenen Datensatz angewendet wurden, indem Sie eine GET an die API [!DNL Dataset Service] anfordern.

**API-Format**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige Wert von `id` des Datensatzes, dessen Beschriftungen Sie nachschlagen möchten. |

**Anfrage**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Datenverwendungsbeschriftungen zurück, die auf den Datensatz angewendet wurden.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{IMS_ORG}",
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
| `labels` | Eine Liste von Datenverwendungsbeschriftungen, die auf den Datensatz angewendet wurden. |
| `optionalLabels` | Eine Liste einzelner Felder im Datensatz, auf die Datenverwendungsbeschriftungen angewendet wurden. Die folgenden Untereigenschaften sind erforderlich:<br/><br/>`option`: Ein Objekt, das die Attribute [!DNL Experience Data Model] (XDM) des Felds enthält. Die folgenden drei Eigenschaften sind erforderlich:<ul><li>`id`: Der URI- `$id` Wert des Schemas, das dem Feld zugeordnet ist.</li><li>`contentType`: Gibt das Format und die Version des Schemas an. Weitere Informationen finden Sie im Abschnitt zu [Schema versioning](../../xdm/api/getting-started.md#versioning) im Handbuch zur XDM-API.</li><li>`schemaPath`: Der Pfad zur fraglichen Schema-Eigenschaft, geschrieben in  [JSON ](../../landing/api-fundamentals.md#json-pointer) Pointersyntax.</li></ul>`labels`: Eine Liste von Datenverwendungsbeschriftungen, die Sie dem Feld hinzufügen möchten. |

- id: Der URI $id-Wert für das XDM-Schema, auf dem der Datensatz basiert.
- contentType: Gibt das Format und die Version des Schemas an. Weitere Informationen finden Sie im Abschnitt zu [Schema versioning](../../xdm/api/getting-started.md#versioning) im Handbuch zur XDM-API.
- schemaPath: Der Pfad zur fraglichen Schema-Eigenschaft, geschrieben in [JSON-Zeiger](../../landing/api-fundamentals.md#json-pointer)-Syntax.

## Anwenden von Beschriftungen auf einen Datensatz {#apply-dataset-labels}

Sie können einen Satz von Bezeichnungen für ein Dataset erstellen, indem Sie sie in der Nutzlast einer POST oder einer PUT-Anforderung an die [!DNL Dataset Service]-API bereitstellen. Wenn Sie eine dieser Methoden verwenden, werden vorhandene Beschriftungen überschrieben und durch die in der Payload bereitgestellten ersetzt.

**API-Format**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige Wert von `id` des Datensatzes, für den Sie Beschriftungen erstellen. |

**Anfrage**

Mit der folgenden Anforderung zur POST werden dem Datensatz eine Reihe von Bezeichnungen sowie ein bestimmtes Feld in diesem Datensatz hinzugefügt. Die in der Payload bereitgestellten Felder entsprechen den Feldern, die für eine PUT-Anforderung erforderlich sind.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `labels` | Eine Liste von Datenverwendungsbeschriftungen, die Sie dem Datensatz hinzufügen möchten. |
| `optionalLabels` | Eine Liste der einzelnen Felder im Datensatz, denen Sie Beschriftungen hinzufügen möchten. Jedes Element in diesem Array muss die folgenden Eigenschaften haben: Ein Objekt, das die Attribute [!DNL Experience Data Model] (XDM) des Felds enthält. <br/><br/>`option` Die folgenden drei Eigenschaften sind erforderlich:<ul><li>`id`: Der URI- `$id` Wert des Schemas, das dem Feld zugeordnet ist.</li><li>`contentType`: Gibt das Format und die Version des Schemas an. Weitere Informationen finden Sie im Abschnitt zu [Schema versioning](../../xdm/api/getting-started.md#versioning) im Handbuch zur XDM-API.</li><li>`schemaPath`: Der Pfad zur fraglichen Schema-Eigenschaft, geschrieben in  [JSON ](../../landing/api-fundamentals.md#json-pointer) Pointersyntax.</li></ul>`labels`: Eine Liste von Datenverwendungsbeschriftungen, die Sie dem Feld hinzufügen möchten. |

**Antwort**

Eine erfolgreiche Antwort gibt die Beschriftungen zurück, die dem Datensatz hinzugefügt wurden.

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

## Entfernen von Bezeichnungen aus einem Datensatz {#remove-dataset-labels}

Sie können die auf einen Datensatz angewendeten Beschriftungen entfernen, indem Sie eine DELETE-Anforderung an die API [!DNL Dataset Service] stellen.

**API-Format**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige Wert von `id` des Datensatzes, dessen Beschriftungen Sie entfernen möchten. |

**Anfrage**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Ein erfolgreicher HTTP-Status 200 (OK), der angibt, dass die Beschriftungen entfernt wurden. Sie können [die vorhandenen Bezeichnungen](#look-up-dataset-labels) für den Datensatz in einem separaten Aufruf nachschlagen, um dies zu bestätigen.

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie gelernt, wie Sie Datenverwendungsbeschriftungen mithilfe von APIs verwalten können.

Nachdem Sie Datenverwendungsbeschriftungen auf der Dataset- und Feldebene hinzugefügt haben, können Sie beginnen, Daten in [!DNL Experience Platform] zu erfassen. Weitere Informationen erhalten Sie im Beginn in der [Datenerhebungsdokumentation](../../ingestion/home.md).

Sie können jetzt auch Datenverwendungsrichtlinien auf Basis der von Ihnen angewendeten Beschriftungen definieren. Weitere Informationen finden Sie unter [Übersicht über Datenverwendungsrichtlinien](../policies/overview.md).

Weitere Informationen zum Verwalten von Datensätzen in [!DNL Experience Platform] finden Sie unter [Übersicht über Datensätze](../../catalog/datasets/overview.md).