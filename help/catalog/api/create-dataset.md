---
keywords: Experience Platform; Startseite; beliebte Themen; Datensatz; Datensatz; Datensatz; Datensatz erstellen; Datensatz erstellen; Datensatz erstellen; Datensatz aktivieren
solution: Experience Platform
title: Erstellen eines Datensatzes in der API
topic-legacy: developer guide
description: In diesem Dokument wird beschrieben, wie Sie ein Datensatzobjekt in der Catalog Service-API erstellen.
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 57%

---

# Datensatz in der API erstellen

Um einen Datensatz mit der API [!DNL Catalog] zu erstellen, müssen Sie den Wert `$id` des [!DNL Experience Data Model] (XDM)-Schemas kennen, auf dem der Datensatz basieren soll. Sobald Sie über die Schema-ID verfügen, können Sie einen Datensatz erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/datasets` in der API [!DNL Catalog] senden.

>[!NOTE]
>
>In diesem Dokument wird nur die Erstellung eines Datensatzobjekts in [!DNL Catalog] beschrieben. Ausführliche Anweisungen zum Erstellen, Füllen und Überwachen eines Datensatzes finden Sie im folgenden [Tutorial](../datasets/create.md).

**API-Format**

```HTTP
POST /dataSets
```

**Anfrage**

Die folgende Anfrage erstellt einen Datensatz, der auf ein zuvor definiertes Schema verweist.

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name des zu erstellenden Datensatzes. |
| `schemaRef.id` | Der URI-`$id`-Wert für das XDM-Schema, auf dem der Datensatz basieren soll. |
| `schemaRef.contentType` | Gibt das Format und die Version des Schemas an. Weitere Informationen finden Sie im Abschnitt zur [Schemaversionierung](../../xdm/api/getting-started.md#versioning) im XDM-API-Handbuch. |

>[!NOTE]
>
>In diesem Beispiel wird das Dateiformat [Apache Parquet](https://parquet.apache.org/documentation/latest/) für die Eigenschaft `containerFormat` verwendet. Ein Beispiel zur Nutzung des JSON-Dateiformats finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](../../ingestion/batch-ingestion/api-overview.md).

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und ein Antwortobjekt zurück, das aus einem Array mit der Kennung des neu erstellten Datensatzes im Format `"@/datasets/{DATASET_ID}"` besteht. Die Datensatz-ID ist eine schreibgeschützte, vom System generierte Zeichenfolge, mit der in API-Aufrufen auf den Datensatz verwiesen wird.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
