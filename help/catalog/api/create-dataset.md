---
keywords: Experience Platform; home; beliebte Themen; Datensatz; Datensatz; Datensatz; Datensatz erstellen; Datensatz erstellen; Datensatz erstellen; Datensatz aktivieren
solution: Experience Platform
title: Erstellen eines Datensatzes in der API
description: In diesem Dokument wird beschrieben, wie Sie ein Datensatzobjekt in der Catalog Service-API erstellen.
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 53%

---

# Datensatz in der API erstellen

Um einen Datensatz mit der API [!DNL Catalog] zu erstellen, müssen Sie den Wert `$id` des Schemas [!DNL Experience Data Model] (XDM) kennen, auf dem der Datensatz basieren soll. Sobald Sie über die Schema-ID verfügen, können Sie einen Datensatz erstellen, indem Sie eine POST-Anfrage an den `/datasets` -Endpunkt in der [!DNL Catalog] -API richten.

>[!NOTE]
>
>In diesem Dokument wird nur die Erstellung eines Datensatzobjekts in [!DNL Catalog] behandelt. Ausführliche Anweisungen zum Erstellen, Füllen und Überwachen eines Datensatzes finden Sie im folgenden [Tutorial](../datasets/create.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>In diesem Beispiel wird das Dateiformat [Apache Parquet](https://parquet.apache.org/docs/) für die Eigenschaft `containerFormat` verwendet. Ein Beispiel zur Nutzung des JSON-Dateiformats finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](../../ingestion/batch-ingestion/api-overview.md).

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und ein Antwortobjekt zurück, das aus einem Array mit der Kennung des neu erstellten Datensatzes im Format `"@/datasets/{DATASET_ID}"` besteht. Die Datensatz-ID ist eine schreibgeschützte, vom System generierte Zeichenfolge, mit der in API-Aufrufen auf den Datensatz verwiesen wird.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
