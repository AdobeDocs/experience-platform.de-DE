---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Verwalten von Datenverwendungsbeschriftungen mit APIs '
topic: developer guide
translation-type: tm+mt
source-git-commit: 1fce86193bc1660d0f16408ed1b9217368549f6c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 3%

---


# Verwalten von Datenverwendungsbeschriftungen mit APIs

Mit der DataSet-Dienst-API können Sie Nutzungsbeschriftungen für Datensätze programmgesteuert verwalten. Es gehört zu den Datenkatalogfunktionen der Adobe Experience Platform, ist jedoch von der Katalogdienst-API getrennt, die die Metadaten des Datensatzes verwaltet.

In diesem Dokument wird beschrieben, wie Sie mit der DataSet-Dienst-API Datenverwendungsbeschriftungen auf Dataset- und Feldebene verwalten.

## Erste Schritte

Bevor Sie dieses Handbuch lesen, führen Sie die Schritte aus, die im Abschnitt [&quot;](../../catalog/api/getting-started.md) Erste Schritte&quot;im Handbuch für den Katalogentwickler beschrieben sind, um die erforderlichen Anmeldeinformationen für Aufrufe von [!DNL Platform] APIs zu sammeln.

Um die in den folgenden Abschnitten beschriebenen Endpunkte aufrufen zu können, müssen Sie über den eindeutigen `id` Wert für einen bestimmten Datensatz verfügen. Wenn Sie diesen Wert nicht haben, finden Sie im Handbuch zur [Auflistung von Katalogobjekten](../../catalog/api/list-objects.md) die IDs der vorhandenen Datensätze.

## Suchen von Beschriftungen für einen Datensatz {#lookup}

Sie können die Datenverwendungsbeschriftungen nachschlagen, die auf einen vorhandenen Datensatz angewendet wurden, indem Sie eine GET-Anforderung stellen.

**API-Format**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige `id` Wert des Datensatzes, dessen Beschriftungen Sie nachschlagen möchten. |

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
| `optionalLabels` | Eine Liste einzelner Felder im Datensatz, auf die Datenverwendungsbeschriftungen angewendet wurden. |

## Anwenden von Beschriftungen auf einen Datensatz

Sie können einen Satz von Bezeichnungen für einen Datensatz erstellen, indem Sie diese in der Nutzlast einer POST- oder PUT-Anforderung bereitstellen. Wenn Sie eine dieser Methoden verwenden, werden vorhandene Beschriftungen überschrieben und durch die in der Payload bereitgestellten ersetzt.

**API-Format**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige `id` Wert des Datensatzes, für den Sie Beschriftungen erstellen. |

**Anfrage**

Mit der folgenden POST-Anforderung wird dem Datensatz eine Reihe von Beschriftungen sowie ein spezifisches Feld in diesem Datensatz hinzugefügt. Die in der Payload bereitgestellten Felder entsprechen den Feldern, die für eine PUT-Anforderung erforderlich sind.

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
| `optionalLabels` | Eine Liste der einzelnen Felder im Datensatz, denen Sie Beschriftungen hinzufügen möchten. Jedes Element in diesem Array muss die folgenden Eigenschaften aufweisen: <br/><br/>`option`: Ein Objekt, das die XDM-Attribute (Experience Data Model) des Felds enthält. Die folgenden drei Eigenschaften sind erforderlich:<ul><li>id</code>: Der URI $id</code> -Wert des Schemas, das dem Feld zugeordnet ist.</li><li>contentType</code>: Der Inhaltstyp und die Versionsnummer des Schemas. Dies sollte in Form eines der gültigen <a href="../../xdm/api/look-up-resource.md">Accept-Header</a> für eine XDM-Suchanfrage erfolgen.</li><li>schemaPath</code>: Der Pfad zum Feld im Schema des Datensatzes.</li></ul>`labels`: Eine Liste von Datenverwendungsbeschriftungen, die Sie dem Feld hinzufügen möchten. |

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

## Löschen von Bezeichnungen für einen Datensatz

Sie können die auf einen Datensatz angewendeten Beschriftungen löschen, indem Sie eine DELETE-Anforderung ausführen.

**API-Format**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige `id` Wert des Datensatzes, dessen Beschriftungen Sie löschen möchten. |

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

Eine erfolgreiche Antwort HTTP-Status 200 (OK), der angibt, dass die Beschriftungen gelöscht wurden. Sie können die vorhandenen Bezeichnungen [für den Datensatz in einem separaten Aufruf](#lookup) nachschlagen, um dies zu bestätigen.

## Nächste Schritte

Nachdem Sie nun Datenverwendungsbeschriftungen auf der Dataset- und Feldebene hinzugefügt haben, können Sie beginnen, Daten in Experience Platform zu erfassen. Weitere Informationen erhalten Sie im Beginn in der [Datenerhebungsdokumentation](../../ingestion/home.md).

Sie können jetzt auch Datenverwendungsrichtlinien auf Basis der von Ihnen angewendeten Beschriftungen definieren. Weitere Informationen finden Sie in der Übersicht über die [Datenverwendungsrichtlinien](../policies/overview.md).

Weitere Informationen zum Verwalten von Datensätzen in [!DNL Experience Platform]finden Sie in der Übersicht über [Datensätze](../../catalog/datasets/overview.md).