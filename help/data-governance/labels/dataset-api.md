---
keywords: Experience Platform;Startseite;beliebte Themen;Datensatz-API;Datenverwendung verwalten;Datenverwendungs-API
solution: Experience Platform
title: 'Verwalten von Datennutzungskennzeichnungen für Datensätze mithilfe von APIs '
topic-legacy: developer guide
description: Mit der Datensatz-Service-API können Sie Nutzungsbezeichnungen für Datensätze anwenden und bearbeiten. Sie gehört zu den Datenkatalogfunktionen von Adobe Experience Platform, ist jedoch von der Katalog-Service-API getrennt, die Datensatz-Metadaten verwaltet.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 937225ff08e2e02c5840f86d6ed50644e05bdfe5
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 100%

---

# Verwalten von Datennutzungskennzeichnungen für Datensätze mithilfe von APIs

Mit [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) können Sie Nutzungskennzeichnungen für Datensätze anwenden und bearbeiten. Sie gehört zu den Datenkatalogfunktionen von Adobe Experience Platform, ist jedoch von der [!DNL Catalog Service]-API getrennt, die Datensatz-Metadaten verwaltet.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Datennutzungsbeschriftungen zurück, die auf den Datensatz angewendet wurden.

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
| `labels` | Eine Liste von Datennutzungsbeschriftungen, die auf den Datensatz angewendet wurden. |
| `optionalLabels` | Eine Liste einzelner Felder im Datensatz, auf die Datennutzungsbeschriftungen angewendet werden bzw. wurden. |

## Anwenden von Kennzeichnungen auf einen Datensatz {#apply}

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

Mit der folgenden PUT-Anfrage werden die vorhandenen Kennzeichnungen für einen Datensatz sowie ein bestimmtes Feld in diesem Datensatz aktualisiert. Die in der Payload bereitgestellten Felder entsprechen den Feldern, die für eine POST-Anfrage erforderlich wären.

>[!IMPORTANT]
>
>Es muss eine gültige `If-Match`-Kopfzeile bereitgestellt werden, wenn PUT-Anfragen an den `/datasets/{DATASET_ID}/labels`-Endpunkt gesendet werden. Weitere Informationen zur Verwendung der erforderlichen Kopfzeile finden Sie im Abschnitt [Anhang](#if-match).

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
| `labels` | Eine Liste von Datennutzungsbeschriftungen, die Sie dem Datensatz hinzufügen möchten. |
| `optionalLabels` | Eine Liste der einzelnen Felder im Datensatz, denen Sie Beschriftungen hinzufügen möchten. Jedes Element in diesem Array muss die folgenden Eigenschaften aufweisen:<br/><br/>`option`Ein Objekt, das die [!DNL Experience Data Model] (XDM)-Attribute des Felds enthält. Die folgenden drei Eigenschaften sind erforderlich:<ul><li>id</code>: Der URI-$id</code>-Wert des Schemas, das dem Feld zugeordnet ist.</li><li>contentType</code>: Der Content-Typ und die Versionsnummer des Schemas. Dies sollte in Form eines der gültigen <a href="../../xdm/api/getting-started.md#accept">Accept-Header</a> für eine XDM-Suchanfrage erfolgen.</li><li>schemaPath</code>: Der Pfad zum Feld im Schema des Datensatzes.</li></ul>`labels`: Eine Liste von Datennutzungskennzeichnungen, die Sie zu dem Feld hinzufügen möchten. |

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

## Entfernen von Kennzeichnungen aus einem Datensatz {#remove}

Sie können die auf einen Datensatz angewendeten Kennzeichnungen entfernen, indem Sie eine DELETE-Anfrage an die [!DNL Dataset Service]-API stellen.

**API-Format**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der eindeutige `id`-Wert des Datensatzes, dessen Kennzeichnungen Sie entfernen möchten. |

**Anfrage**

Die folgende Anfrage entfernt die Kennzeichnungen für den Datensatz, der im Pfad angegeben ist.

>[!IMPORTANT]
>
>Es muss eine gültige `If-Match`-Kopfzeile bereitgestellt werden, wenn DELETE-Anfragen an den `/datasets/{DATASET_ID}/labels`-Endpunkt gesendet werden. Weitere Informationen zur Verwendung der erforderlichen Kopfzeile finden Sie im Abschnitt [Anhang](#if-match).

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

HTTP-Status 200 (OK) einer erfolgreichen Antwort, der angibt, dass die Kennzeichnungen entfernt wurden. Sie können die vorhandenen Bezeichnungen für den Datensatz in einem separaten Aufruf [nachschlagen](#look-up), um dies zu bestätigen.

## Nächste Schritte

Durch das Lesen dieses Dokuments haben Sie gelernt, wie Sie mit der [!DNL Dataset Service]-API Datennutzungskennzeichnungen für Datensätze und Felder verwalten können.

Nachdem Sie Datennutzungskennzeichnungen auf der Datensatz- und Feldebene hinzugefügt haben, können Sie beginnen, Daten in [!DNL Experience Platform] aufzunehmen. Um mehr darüber zu erfahren, lesen Sie zunächst die [Dokumentation zur Datenaufnahme](../../ingestion/home.md).

Sie können jetzt auch Datennutzungsrichtlinien auf Basis der von Ihnen angewendeten Kennzeichnungen definieren. Weitere Informationen finden Sie unter [Datennutzungsrichtlinien – Übersicht](../policies/overview.md).

Weitere Informationen zum Verwalten von Datensätzen in [!DNL Experience Platform] finden Sie unter [Datensätze – Übersicht](../../catalog/datasets/overview.md).

## Anhang {#appendix}

Der folgende Abschnitt enthält weitere Informationen zum Arbeiten mit Kennzeichnungen mithilfe der Dataset Service-API.

### [!DNL If-Match]-Kopfzeile {#if-match}

Wenn API-Aufrufe durchgeführt werden, die die vorhandenen Kennzeichnungen eines Datensatzes aktualisieren (PUT und DELETE), muss eine `If-Match`-Kopfzeile eingefügt werden, die die aktuelle Version der Entität für die Datensatzkennzeichnung in Dataset Service angibt. Um Datenkollisionen zu vermeiden, aktualisiert der Dienst die Datensatzentität nur, wenn die enthaltene `If-Match`-Zeichenfolge mit dem neuesten vom System für diesen Datensatz generierten Versions-Tag übereinstimmt.

>[!NOTE]
>
>Wenn für den betreffenden Datensatz derzeit keine Kennzeichnungen vorhanden sind, können neue Kennzeichnungen nur über eine POST-Anfrage hinzugefügt werden, wofür keine `If-Match`-Kopfzeile erforderlich ist. Nachdem Kennzeichnungen zu einem Datensatz hinzugefügt wurden, wird ihm ein `etag`-Wert zugewiesen, mit dem die Kennzeichnungen zu einem späteren Zeitpunkt aktualisiert oder entfernt werden können.

Um die neueste Version der Datensatzkennzeichnungsentität abzurufen, stellen Sie eine [GET-Anfrage](#look-up) an den `/datasets/{DATASET_ID}/labels`-Endpunkt. Der aktuelle Wert wird in der Antwort unter einer `etag`-Kopfzeile zurückgegeben. Beim Aktualisieren vorhandener Datensatzkennzeichnungen sollten Sie zunächst eine Suchanfrage für den Datensatz durchführen, um den neuesten `etag`-Wert abzurufen, bevor Sie diesen Wert in der `If-Match`-Kopfzeile Ihrer nachfolgenden PUT- oder DELETE-Anfrage verwenden.
