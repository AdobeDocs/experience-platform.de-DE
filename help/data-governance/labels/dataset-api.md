---
keywords: Experience Platform;Startseite;beliebte Themen;Datensatz-API;Datenverwendung verwalten;Datenverwendungs-API
solution: Experience Platform
title: Verwalten von Datennutzungskennzeichnungen für Datensätze mithilfe von APIs
description: Mit der Datensatz-Service-API können Sie Nutzungsbezeichnungen für Datensätze anwenden und bearbeiten. Sie gehört zu den Datenkatalogfunktionen von Adobe Experience Platform, ist jedoch von der Katalog-Service-API getrennt, die Datensatz-Metadaten verwaltet.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 1f7a1bcf5aaf694ca2d3416c9c98f37b66adc69f
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 52%

---

# Verwalten von Datennutzungskennzeichnungen für Datensätze mithilfe von APIs

Mit [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) können Sie Nutzungskennzeichnungen für Datensätze anwenden und bearbeiten. Sie gehört zu den Datenkatalogfunktionen von Adobe Experience Platform, ist jedoch von der [!DNL Catalog Service]-API getrennt, die Datensatz-Metadaten verwaltet.

<!-- >[!IMPORTANT]
>
>Applying labels at the dataset level is only supported for data governance use cases. If you are trying to create access policies for the data, you must [apply labels to the schema](../../xdm/tutorials/labels.md) that the dataset is based on. See the overview on [attribute-based access control](../../access-control/abac/overview.md) for more information. -->

In diesem Dokument wird beschrieben, wie Sie Kennzeichnungen für Datensätze und Felder mit der [!DNL Dataset Service API] verwalten. Anweisungen zum Verwalten von Datennutzungskennzeichnungen selbst mithilfe von API-Aufrufen finden Sie im [Handbuch zu Endpunktkennzeichnungen](../api/labels.md) für die [!DNL Policy Service API].

## Erste Schritte

Bevor Sie dieses Handbuch lesen, führen Sie die Schritte aus, die im Abschnitt [Erste Schritte](../../catalog/api/getting-started.md) im Catalog-Entwicklerhandbuch beschrieben sind, um die erforderlichen Anmeldeinformationen für Aufrufe an [!DNL Platform]-APIs zu sammeln.

Um die in diesem Dokument beschriebenen Endpunkte aufrufen zu können, müssen Sie über den eindeutigen `id`-Wert für einen bestimmten Datensatz verfügen. Wenn Sie diesen Wert nicht haben, finden Sie im Handbuch [Auflistung der Catalog-Objekte](../../catalog/api/list-objects.md) die IDs der vorhandenen Datensätze.

## Suchen nach Kennzeichnungen für einen Datensatz {#look-up}

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
| `optionalLabels` | Eine Liste einzelner Felder im Datensatz, auf die Datennutzungsbeschriftungen angewendet werden bzw. wurden. |

## Anwenden von Kennzeichnungen auf einen Datensatz {#apply}

Sie können einen Satz von Bezeichnungen für einen gesamten Datensatz anwenden, indem Sie sie in der Payload einer POST- oder PUT-Anfrage an die [!DNL Dataset Service] API. Der Anfrageinhalt ist für beide Aufrufe identisch. Sie können einzelnen Datensatzfeldern keine Bezeichnungen hinzufügen.

**API-Format**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige `id`-Wert des Datensatzes, für den Sie Kennzeichnungen erstellen. |

**Anfrage**

Die nachstehende Beispielanfrage zur POST aktualisiert den gesamten Datensatz mit einer `C1` Beschriftung. Die in der Payload bereitgestellten Felder entsprechen den Feldern, die für eine PUT-Anfrage erforderlich sind.

<!-- When making API calls that update the existing labels of a dataset (PUT), an `If-Match` header that indicates the current version of the dataset-label entity in Dataset Service must be included. In order to prevent data collisions, the service will only update the dataset entity if the included `If-Match` string matches the latest version tag generated by the system for that dataset. -->

>[!NOTE]
>
>Wenn derzeit Beschriftungen für den betreffenden Datensatz vorhanden sind, können neue Beschriftungen nur über eine PUT-Anfrage hinzugefügt werden. Dazu ist ein `If-Match` -Kopfzeile. Nachdem Kennzeichnungen zu einem Datensatz hinzugefügt wurden, wird ihm ein `etag`-Wert zugewiesen, mit dem die Kennzeichnungen zu einem späteren Zeitpunkt aktualisiert oder entfernt werden können.

Um die neueste Version der Datensatzkennzeichnungsentität abzurufen, stellen Sie eine [GET-Anfrage](#look-up) an den `/datasets/{DATASET_ID}/labels`-Endpunkt. Der aktuelle Wert wird in der Antwort unter einer `etag`-Kopfzeile zurückgegeben. Beim Aktualisieren vorhandener Datensatzkennzeichnungen sollten Sie zunächst eine Suchanfrage für den Datensatz durchführen, um den neuesten `etag`-Wert abzurufen, bevor Sie diesen Wert in der `If-Match`-Kopfzeile Ihrer nachfolgenden PUT-Anfrage verwenden.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "entityId": {
          "namespace": "AEP",
          "id": "test-ds-id",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": []
      } '
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `entityId` | Dadurch wird die spezifische zu aktualisierende Datensatz-Entität identifiziert. |
| `entityId.namespace` | Dies wird verwendet, um ID-Kollisionen zu vermeiden. Die `namespace` is `AEP`. |
| `entityId.id` | Die Kennung der zu aktualisierenden Ressource. Dies bezieht sich auf die `datasetId`. |
| `entityId.type` | Der Typ der zu aktualisierenden Ressource. Dies wird immer `dataset`. |
| `labels` | Eine Liste der Datennutzungsbezeichnungen, die Sie dem gesamten Datensatz hinzufügen möchten. |
| `parents` | Die `parents` -Array enthält eine Liste von `entityId`bedeutet, dass dieser Datensatz Beschriftungen von übernimmt. Datensätze können Beschriftungen von Schemas und/oder Datensätzen übernehmen. |

**Antwort**

Eine erfolgreiche Antwort gibt den aktualisierten Satz von Kennzeichnungen für den Datensatz zurück.

>[!IMPORTANT]
>
>Die `optionalLabels` -Eigenschaft für die Verwendung mit POST-Anforderungen nicht mehr unterstützt. Es ist nicht mehr möglich, Datensatzfeldern Datenbezeichnungen hinzuzufügen. Bei einem POST-Vorgang wird ein Fehler ausgegeben, wenn ein `optionalLabel` vorhanden ist. Sie können jedoch Beschriftungen aus einzelnen Feldern löschen, indem Sie eine PUT-Anfrage und die `optionalLabels` -Eigenschaft. Weitere Informationen finden Sie im Abschnitt unter [Entfernen von Bezeichnungen aus einem Datensatz](#remove).

```json
{
  "parents": [
      {
        "id": "_ddgduleint.schemas.4a95cdba7d560e3bca7d8c5c7b58f00ca543e2bb1e4137d6",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-201",
  "message": "POST Successful"
} 
```

## Entfernen von Kennzeichnungen aus einem Datensatz {#remove}

Sie können alle zuvor angewendeten Feldbezeichnungen entfernen, indem Sie entweder die vorhandene `optionalLabels` -Wert(e) mit einer Teilmenge der vorhandenen Feldbezeichnungen oder einer leeren Liste, um sie vollständig zu entfernen. Stellen Sie eine PUT-Anfrage an die [!DNL Dataset Service] API zum Aktualisieren oder Entfernen zuvor angewendeter Bezeichnungen.

**API-Format**

```http
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige `id`-Wert des Datensatzes, für den Sie Kennzeichnungen erstellen. |

**Anfrage**

Der folgende Datensatz, auf den der PUT-Vorgang angewendet wird, enthielt C1 optionalLabel für das Feld &quot;properties/person/properties/address&quot;und C1, C2 optionalLabels für das Feld /properties/person/properties/name/properties/fullName . Nach dem Put-Vorgang weist das erste Feld keine Beschriftung auf (Beschriftung C1 wurde entfernt) und das zweite Feld nur die Beschriftung C1 (Beschriftung C2 wurde entfernt).

Im folgenden Beispielszenario wird eine PUT-Anfrage verwendet, um zu einzelnen Feldern hinzugefügte Bezeichnungen zu entfernen. Bevor die Anfrage gestellt wurde, wird die `fullName` hatte das Feld `C1` und `C2` angewendete Beschriftungen und die `address` -Feld hatte bereits eine `C1` angewendetes Etikett. Die PUT-Anfrage überschreibt vorhandene Bezeichnungen `C1, C2` Beschriftungen aus `fullName` mit einem `C1` Beschriftung mithilfe der `optionalLabels.labels` Parameter. Die Anfrage überschreibt auch die `C1` aus der `address` mit einem leeren Satz von Feldbezeichnungen.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000' \
  -d '{
        "entityId": {
          "namespace": "AEP",
          "id": "646b814d52e1691c07b41032",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": [],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/name/properties/fullName"
            },
            "labels": [
              "C1"
            ]
          },
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/address"
            },
            "labels": []
          }
        ]
      }'
```

| Parameter | Beschreibung |
| --- | --- |
| `entityId` | Dadurch wird die spezifische zu aktualisierende Datensatz-Entität identifiziert. Die `entityId` muss die folgenden drei Werte enthalten:<br/><br/>`namespace`: Dies wird verwendet, um ID-Kollisionen zu vermeiden. Die `namespace` is `AEP`.<br/>`id`: Die Kennung der zu aktualisierenden Ressource. Dies bezieht sich auf die `datasetId`.<br/>`type`: Der Typ der zu aktualisierenden Ressource. Dies wird immer `dataset`. |
| `labels` | Eine Liste der Datennutzungsbezeichnungen, die Sie dem gesamten Datensatz hinzufügen möchten. |
| `parents` | Die `parents` -Array enthält eine Liste von `entityId`bedeutet, dass dieser Datensatz Beschriftungen von übernimmt. Datensätze können Beschriftungen von Schemas und/oder Datensätzen übernehmen. |
| `optionalLabels` | Dieser Parameter wird zum Entfernen von Bezeichnungen verwendet, die zuvor auf ein Datensatzfeld angewendet wurden. Eine Liste aller einzelnen Felder im Datensatz, aus denen die Beschriftungen entfernt werden sollen. Jedes Element in diesem Array muss die folgenden Eigenschaften aufweisen:<br/><br/>`option`Ein Objekt, das die [!DNL Experience Data Model] (XDM)-Attribute des Felds enthält. Die folgenden drei Eigenschaften sind erforderlich:<ul><li>id</code>: Der URI-$id</code>-Wert des Schemas, das dem Feld zugeordnet ist.</li><li>contentType</code>: Der Content-Typ und die Versionsnummer des Schemas. Dies sollte in Form eines der gültigen <a href="../../xdm/api/getting-started.md#accept">Accept-Header</a> für eine XDM-Suchanfrage erfolgen.</li><li>schemaPath</code>: Der Pfad zum Feld im Schema des Datensatzes.</li></ul>`labels`: Dieser Wert muss entweder eine Teilmenge der vorhandenen angewendeten Feldbezeichnungen enthalten oder leer sein, um alle vorhandenen Feldbezeichnungen zu entfernen. PUT- oder POST-Methoden geben jetzt einen Fehler zurück, wenn die `optionalLabels` enthält neue oder geänderte Bezeichnungen. |

**Antwort**

Eine erfolgreiche Antwort gibt den aktualisierten Satz von Kennzeichnungen für den Datensatz zurück.

```json
{
  "parents": [
      {
        "id": "_xdm.context.identity-graph-flattened-export",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-200",
  "message": "PUT Successful"
} 
```

## Nächste Schritte

Durch das Lesen dieses Dokuments haben Sie gelernt, wie Sie mit der [!DNL Dataset Service]-API Datennutzungskennzeichnungen für Datensätze und Felder verwalten können. Sie können jetzt [Datennutzungsrichtlinien](../policies/overview.md) und [Zugriffssteuerungsrichtlinien](../../access-control/abac/ui/policies.md) basierend auf den von Ihnen angewendeten Kennzeichnungen definieren.

Weitere Informationen zum Verwalten von Datensätzen in [!DNL Experience Platform] finden Sie unter [Datensätze – Übersicht](../../catalog/datasets/overview.md).
