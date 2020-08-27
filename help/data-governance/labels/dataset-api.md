---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Verwalten von Datenverwendungsbeschriftungen für Datasets mithilfe von APIs '
topic: developer guide
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 3%

---


# Verwalten von Datenverwendungsbeschriftungen für Datasets mithilfe von APIs

Mit der [[!DNL Dataset Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) können Sie Nutzungsbezeichnungen für Datasets anwenden und bearbeiten. Es gehört zu den Datenkatalogfunktionen von Adobe Experience Platform, ist jedoch von der [!DNL Catalog Service] API, die DataSet-Metadaten verwaltet, getrennt.

In diesem Dokument wird beschrieben, wie Sie Beschriftungen für Datasets und Felder mit dem [!DNL Dataset Service API]Operator verwalten. Anweisungen zum Verwalten von Datenverwendungsbeschriftungen selbst mithilfe von API-Aufrufen finden Sie in der [Beschreibungen-Endpunktanleitung](../api/labels.md) für die [!DNL Policy Service API].

## Erste Schritte

Bevor Sie dieses Handbuch lesen, führen Sie die Schritte aus, die im Abschnitt [&quot;](../../catalog/api/getting-started.md) Erste Schritte&quot;im Handbuch für den Katalogentwickler beschrieben sind, um die erforderlichen Anmeldeinformationen für Aufrufe von [!DNL Platform] APIs zu sammeln.

Um die in diesem Dokument beschriebenen Endpunkte aufrufen zu können, müssen Sie über den eindeutigen `id` Wert für einen bestimmten Datensatz verfügen. Wenn Sie diesen Wert nicht haben, finden Sie im Handbuch zur [Auflistung von Katalogobjekten](../../catalog/api/list-objects.md) die IDs der vorhandenen Datensätze.

## Suchen von Beschriftungen für einen Datensatz {#look-up}

Sie können die Datenverwendungsbeschriftungen nachschlagen, die auf einen vorhandenen Datensatz angewendet wurden, indem Sie eine GET an die [!DNL Dataset Service] API anfordern.

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

## Anwenden von Beschriftungen auf einen Datensatz {#apply}

Sie können einen Satz von Bezeichnungen für ein Dataset erstellen, indem Sie sie in der Nutzlast einer POST oder einer PUT-Anforderung an die [!DNL Dataset Service] API bereitstellen. Wenn Sie eine dieser Methoden verwenden, werden vorhandene Beschriftungen überschrieben und durch die in der Payload bereitgestellten ersetzt.

**API-Format**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige `id` Wert des Datensatzes, für den Sie Beschriftungen erstellen. |

**Anfrage**

Mit der folgenden PUT-Anforderung werden die vorhandenen Bezeichnungen für einen Datensatz sowie ein bestimmtes Feld in diesem Datensatz aktualisiert. Die in der Payload bereitgestellten Felder entsprechen den Feldern, die für eine Anforderung der POST erforderlich sind.

>[!IMPORTANT]
>
>Bei PUT-Anfragen an den `If-Match` `/datasets/{DATASET_ID}/labels` Endpunkt muss eine gültige Kopfzeile angegeben werden. Weitere Informationen zur Verwendung der erforderlichen Kopfzeile finden Sie im [Anhang](#if-match) .

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000' \
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
| `optionalLabels` | Eine Liste der einzelnen Felder im Datensatz, denen Sie Beschriftungen hinzufügen möchten. Jedes Element in diesem Array muss die folgenden Eigenschaften aufweisen: <br/><br/>`option`: Ein Objekt, das die [!DNL Experience Data Model] (XDM-)Attribute des Felds enthält. Die folgenden drei Eigenschaften sind erforderlich:<ul><li>id</code>: Der URI $id</code> -Wert des Schemas, das dem Feld zugeordnet ist.</li><li>contentType</code>: Der Inhaltstyp und die Versionsnummer des Schemas. Dies sollte in Form eines der gültigen <a href="../../xdm/api/look-up-resource.md">Accept-Header</a> für eine XDM-Suchanfrage erfolgen.</li><li>schemaPath</code>: Der Pfad zum Feld im Schema des Datensatzes.</li></ul>`labels`: Eine Liste von Datenverwendungsbeschriftungen, die Sie dem Feld hinzufügen möchten. |

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

## Entfernen von Bezeichnungen aus einem Datensatz {#remove}

Sie können die auf einen Datensatz angewendeten Beschriftungen entfernen, indem Sie eine DELETE-Anforderung an die [!DNL Dataset Service] API senden.

**API-Format**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige `id` Wert des Datensatzes, dessen Beschriftungen Sie entfernen möchten. |

**Anfrage**

Die folgende Anforderung entfernt die Beschriftungen für den Datensatz, der im Pfad angegeben ist.

>[!IMPORTANT]
>
>Eine gültige `If-Match` Kopfzeile muss bereitgestellt werden, wenn DELETE-Anforderungen an den `/datasets/{DATASET_ID}/labels` Endpunkt gesendet werden. Weitere Informationen zur Verwendung der erforderlichen Kopfzeile finden Sie im [Anhang](#if-match) .

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000'
```

**Antwort**

Ein erfolgreicher HTTP-Status 200 (OK), der angibt, dass die Beschriftungen entfernt wurden. Sie können die vorhandenen Bezeichnungen [für den Datensatz in einem separaten Aufruf](#look-up) nachschlagen, um dies zu bestätigen.

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie gelernt, wie Sie mit der [!DNL Dataset Service] API Datenverwendungsbeschriftungen für Datensätze und Felder verwalten können.

Nachdem Sie Datenverwendungsbeschriftungen auf der Dataset- und Feldebene hinzugefügt haben, können Sie beginnen, Daten zu erfassen [!DNL Experience Platform]. Weitere Informationen erhalten Sie im Beginn in der [Datenerhebungsdokumentation](../../ingestion/home.md).

Sie können jetzt auch Datenverwendungsrichtlinien auf Basis der von Ihnen angewendeten Beschriftungen definieren. Weitere Informationen finden Sie in der Übersicht über die [Datenverwendungsrichtlinien](../policies/overview.md).

Weitere Informationen zum Verwalten von Datensätzen in [!DNL Experience Platform]finden Sie in der Übersicht über [Datensätze](../../catalog/datasets/overview.md).

## Anhang {#appendix}

Der folgende Abschnitt enthält weitere Informationen zum Arbeiten mit Beschriftungen mithilfe der DataSet-Dienst-API.

### [!DNL If-Match]-Kopfzeile{#if-match}

Bei API-Aufrufen, die die vorhandenen Bezeichnungen eines Datensatzes (PUT und DELETE) aktualisieren, muss eine `If-Match` Kopfzeile mit der aktuellen Version der Entität für die Datenbeschriftung im DataSet-Dienst eingefügt werden. Um Datenkollisionen zu vermeiden, aktualisiert der Dienst die Datensatzentität nur, wenn die enthaltene `If-Match` Zeichenfolge mit dem neuesten vom System für diesen Datensatz generierten Version-Tag übereinstimmt.

>[!NOTE]
>
>Wenn für den betreffenden Datensatz derzeit keine Beschriftungen vorhanden sind, können neue Beschriftungen nur über eine Anforderung zur POST hinzugefügt werden, für die keine `If-Match` Kopfzeile erforderlich ist. Nachdem einem Datensatz Beschriftungen hinzugefügt wurden, wird ein `etag` Wert zugewiesen, mit dem die Beschriftungen zu einem späteren Zeitpunkt aktualisiert oder entfernt werden können.

Um die neueste Version der Entität für die Datenbeschriftung abzurufen, stellen Sie eine [GET-Anforderung](#look-up) an den `/datasets/{DATASET_ID}/labels` Endpunkt. Der aktuelle Wert wird in der Antwort unter einer `etag` Kopfzeile zurückgegeben. Beim Aktualisieren vorhandener Datensatzbeschriftungen empfiehlt es sich, zunächst eine Suchanfrage für den Datensatz durchzuführen, um den neuesten `etag` Wert abzurufen, bevor dieser Wert in der `If-Match` Kopfzeile Ihrer nachfolgenden PUT- oder DELETE-Anforderung verwendet wird.