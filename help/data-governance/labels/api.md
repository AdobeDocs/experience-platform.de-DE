---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Verwalten von Datenverwendungsbeschriftungen mit APIs '
topic: developer guide
translation-type: tm+mt
source-git-commit: d685f1851badf54ce1d1ac3cbacd69d62894c33f
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 3%

---


# Verwalten von Datenverwendungsbeschriftungen mit APIs

In diesem Dokument wird beschrieben, wie Sie mit der Katalogdienst-API Datenverwendungsbeschriftungen auf Dataset- und Feldebene verwalten.

## Erste Schritte

Bevor Sie dieses Handbuch lesen, sollten Sie die Übersicht über den [Katalogdienst](../../catalog/home.md) lesen, um eine solidere Einführung in den Dienst zu erhalten. Darüber hinaus müssen Sie auch die Schritte befolgen, die im Abschnitt [&quot;](../../catalog/api/getting-started.md) Erste Schritte&quot;im Entwicklerhandbuch für Kataloge beschrieben sind, um die erforderlichen Anmeldeinformationen für Aufrufe der Katalog-API zu sammeln.

Um die in den folgenden Abschnitten beschriebenen Endpunkte aufrufen zu können, müssen Sie über den eindeutigen `id` Wert für einen bestimmten Datensatz verfügen. Wenn Sie diesen Wert nicht haben, finden Sie im Abschnitt &quot;Entwicklerhandbuch&quot;Informationen zum [Auflisten von Katalogobjekten](../../catalog/api/list-objects.md) , um die IDs der vorhandenen Datensätze zu finden.

## Suchen von Beschriftungen für einen Datensatz {#lookup}

Sie können die Datenverwendungsbeschriftungen nachschlagen, die auf einen vorhandenen Datensatz angewendet wurden, indem Sie eine GET-Anforderung stellen.

**API-Format**

```http
GET /dataSets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige `id` Wert des Datensatzes, dessen Beschriftungen Sie nachschlagen möchten. |

**Anfrage**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
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
POST /dataSets/{DATASET_ID}/labels
PUT /dataSets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige `id` Wert des Datensatzes, für den Sie Beschriftungen erstellen. |

**Anfrage**

Mit der folgenden POST-Anforderung wird dem Datensatz eine Reihe von Beschriftungen sowie ein spezifisches Feld in diesem Datensatz hinzugefügt. Die in der Payload bereitgestellten Felder entsprechen den Feldern, die für eine PUT-Anforderung erforderlich sind.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
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
DELETE /dataSets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige `id` Wert des Datensatzes, dessen Beschriftungen Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
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