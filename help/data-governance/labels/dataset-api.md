---
keywords: Experience Platform;Startseite;beliebte Themen;Datensatz-API;Datenverwendung verwalten;Datenverwendungs-API
solution: Experience Platform
title: Verwalten von Datennutzungskennzeichnungen für Datensätze mithilfe von APIs
description: Mit der Datensatz-Service-API können Sie Nutzungsbezeichnungen für Datensätze anwenden und bearbeiten. Sie gehört zu den Datenkatalogfunktionen von Adobe Experience Platform, ist jedoch von der Katalog-Service-API getrennt, die Datensatz-Metadaten verwaltet.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 319bcc742b09f979cd744c8d66f032886427ea9e
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 93%

---

# Verwalten von Datennutzungskennzeichnungen für Datensätze mithilfe von APIs

Mit [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) können Sie Nutzungskennzeichnungen für Datensätze anwenden und bearbeiten. Sie gehört zu den Datenkatalogfunktionen von Adobe Experience Platform, ist jedoch von der [!DNL Catalog Service]-API getrennt, die Datensatz-Metadaten verwaltet.

>[!IMPORTANT]
>
>Das Anwenden von Kennzeichnungen auf Datensatzebene wird nur für Data-Governance-Anwendungsfälle unterstützt. Wenn Sie Zugriffsrichtlinien für die Daten erstellen möchten, müssen Sie [Kennzeichnungen auf das Schema anwenden](../../xdm/tutorials/labels.md), auf dem der Datensatz basiert. Weitere Informationen finden Sie in der Übersicht zur [attributbasierten Zugriffssteuerung](../../access-control/abac/overview.md).

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

Sie können einen Satz von Kennzeichnungen für einen kompletten Datensatz erstellen, indem Sie diese in der Payload einer POST- oder PUT-Anfrage an die [!DNL Dataset Service]-API bereitstellen. Der Anfragetext ist für beide Aufrufe identisch. Sie können einzelnen Datensatzfeldern keine Kennzeichnungen hinzufügen.

**API-Format**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige `id`-Wert des Datensatzes, für den Sie Kennzeichnungen erstellen. |

**Anfrage**

Mit der nachstehenden POST-Beispielanfrage wird der komplette Datensatz mit einer `C1`-Kennzeichnung aktualisiert. Die in der Payload bereitgestellten Felder entsprechen den Feldern, die für eine PUT-Anfrage erforderlich sind.

Wenn API-Aufrufe durchgeführt werden, die die vorhandenen Kennzeichnungen eines Datensatzes aktualisieren (PUT), muss eine `If-Match`-Kopfzeile eingefügt werden, die die aktuelle Version der Entität für die Datensatzkennzeichnung in Dataset Service angibt. Um Datenkollisionen zu vermeiden, aktualisiert der Service die Datensatzentität nur, wenn die enthaltene `If-Match`-Zeichenfolge mit dem neuesten vom System für diesen Datensatz generierten Versions-Tag übereinstimmt.

>[!NOTE]
>
>Wenn für den betreffenden Datensatz derzeit Kennzeichnungen vorhanden sind, können neue Kennzeichnungen nur über eine PUT-Anfrage hinzugefügt werden, wofür ein `If-Match`-Header erforderlich ist. Nachdem einem Datensatz Beschriftungen hinzugefügt wurden, wird die neueste `etag` -Wert erforderlich, um die Beschriftungen zu einem späteren Zeitpunkt zu aktualisieren oder zu entfernen<br>Bevor Sie die PUT-Methode ausführen, müssen Sie eine GET-Anfrage für die Datensatzbezeichnungen ausführen. Stellen Sie sicher, dass Sie nur die spezifischen Felder aktualisieren, die für Änderungen in der Anfrage vorgesehen sind, wobei der Rest unverändert bleibt. Stellen Sie außerdem sicher, dass beim PUT-Aufruf dieselben übergeordneten Entitäten wie beim GET-Aufruf beibehalten werden. Jede Diskrepanz würde zu einem Fehler für den Kunden führen.

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
        "parents": [
            {
              "id": "_ddgduleint.schemas.4a95cdba7d560e3bca7d8c5c7b58f00ca543e2bb1e4137d6",
              "type": "schema",
              "namespace": "AEP"
            }
        ]
      } '
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `entityId` | Hierdurch wird eine bestimmte zu aktualisierende Datensatzentität identifiziert. |
| `entityId.namespace` | Dieser Wert wird verwendet, um ID-Konflikte zu vermeiden. Der `namespace`-Wert lautet `AEP`. |
| `entityId.id` | Die ID der zu aktualisierenden Ressource. Dies bezieht sich auf `datasetId`. |
| `entityId.type` | Der Typ der zu aktualisierenden Ressource. Als Wert wird immer `dataset` verwendet. |
| `labels` | Eine Liste von Datennutzungskennzeichnungen, die dem kompletten Datensatz hinzugefügt werden sollen. |
| `parents` | Das Array `parents` enthält eine Liste von `entityId`-Elementen, von denen dieser Datensatz Kennzeichnungen übernimmt. Datensätze können Kennzeichnungen von Schemata und/oder Datensätzen übernehmen. |

**Antwort**

Eine erfolgreiche Antwort gibt den aktualisierten Satz von Kennzeichnungen für den Datensatz zurück.

>[!IMPORTANT]
>
>Die Eigenschaft `optionalLabels` wird für die Verwendung bei POST-Anfragen nicht mehr unterstützt. Es ist nicht mehr möglich, Datenkennzeichnungen zu Datensatzfeldern hinzuzufügen. Bei einem POST-Vorgang wird ein Fehler ausgegeben, wenn ein `optionalLabel`-Wert vorhanden ist. Sie können Kennzeichnungen jedoch mithilfe einer PUT-Anfrage und der Eigenschaft `optionalLabels` aus einzelnen Feldern löschen. Weitere Informationen finden Sie im Abschnitt [Entfernen von Kennzeichnungen aus einem Datensatz](#remove).

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

Sie können alle zuvor angewendeten Feldkennzeichnungen vollständig entfernen, indem Sie entweder vorhandene `optionalLabels`-Werte mit einer Teilmenge der vorhandenen Feldkennzeichnungen oder einer leeren Liste aktualisieren. Stellen Sie eine PUT-Anfrage an die [!DNL Dataset Service]-API, um zuvor angewendete Kennzeichnungen zu aktualisieren oder zu entfernen.

**API-Format**

```http
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige `id`-Wert des Datensatzes, für den Sie Kennzeichnungen erstellen. |

**Anfrage**

Der folgende Datensatz, auf den der PUT-Vorgang angewendet wird, enthielt „C1 optionalLabel“ für das Feld „properties/person/properties/address“ und „C1, C2 optionalLabels“ für das Feld „/properties/person/properties/name/properties/fullName“. Nach dem PUT-Vorgang weist das erste Feld keine Kennzeichnung auf (C1-Kennzeichnung wurde entfernt) und das zweite Feld nur die C1-Kennzeichnung (C2-Kennzeichnung wurde entfernt)

Im folgenden Beispielszenario wird eine PUT-Anfrage verwendet, um zu einzelnen Feldern hinzugefügte Kennzeichnungen zu entfernen. Vor Stellen der Anfrage wurden auf das Feld `fullName` die Kennzeichnungen `C1` und `C2` angewendet und auf das Feld `address` war bereits die Kennzeichnung `C1` angewandt worden. Die PUT-Anfrage überschreibt mithilfe des Parameters `optionalLabels.labels` vorhandene Kennzeichnungen `C1, C2` des Felds `fullName` mit der Kennzeichnung `C1`. Mit der Anfrage wird ebenfalls die Kennzeichnung `C1` des Felds `address` mit einem leeren Satz von Feldkennzeichnungen überschrieben.

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
| `entityId` | Hierdurch wird eine bestimmte zu aktualisierende Datensatzentität identifiziert. `entityId` muss die drei folgenden Werte enthalten:<br/><br/>`namespace`: Dieser Wert wird verwendet, um ID-Konflikte zu vermeiden. Der `namespace`-Wert lautet `AEP`.<br/>`id`: Die ID der zu aktualisierenden Ressource. Dies bezieht sich auf `datasetId`.<br/>`type`: Der Typ der zu aktualisierenden Ressource. Als Wert wird immer `dataset` verwendet. |
| `labels` | Eine Liste von Datennutzungskennzeichnungen, die dem kompletten Datensatz hinzugefügt werden sollen. |
| `parents` | Das Array `parents` enthält eine Liste von `entityId`-Elementen, von denen dieser Datensatz Kennzeichnungen übernimmt. Datensätze können Kennzeichnungen von Schemata und/oder Datensätzen übernehmen. |
| `optionalLabels` | Dieser Parameter wird zum Entfernen von Kennzeichnungen verwendet, die zuvor auf ein Datensatzfeld angewendet wurden. Eine Liste der einzelnen Felder im Datensatz, von denen Kennzeichnungen entfernt werden sollen. Jedes Element in diesem Array muss die folgenden Eigenschaften aufweisen:<br/><br/>`option`Ein Objekt, das die [!DNL Experience Data Model] (XDM)-Attribute des Felds enthält. Die folgenden drei Eigenschaften sind erforderlich:<ul><li><code>ID</code>: Der <code>$id-URI-Wert</code> des Schemas, das dem Feld zugeordnet ist.</li><li><code>contentType</code>: Der Content-Typ und die Versionsnummer des Schemas. Dies sollte in Form eines der gültigen <a href="../../xdm/api/getting-started.md#accept">Accept-Header</a> für eine XDM-Suchanfrage erfolgen.</li><li><code>schemaPath</code>: Der Pfad zum Feld im Schema des Datensatzes.</li></ul>`labels`: Dieser Wert muss entweder eine Teilmenge der vorhandenen angewendeten Feldkennzeichnungen enthalten oder leer sein, um alle vorhandenen Feldkennzeichnungen zu entfernen. Bei PUT- oder POST-Methoden wird jetzt ein Fehler zurückgegeben, wenn das Feld `optionalLabels` neue oder geänderte Kennzeichnungen umfasst. |

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
