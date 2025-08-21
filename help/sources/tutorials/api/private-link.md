---
title: Azure Private Link für Quellen in der API verwenden
description: Erfahren Sie, wie Sie private Links für Adobe Experience Platform-Quellen erstellen und verwenden
badge: Beta
exl-id: 9b7fc1be-5f42-4e29-b552-0b0423a40aa1
source-git-commit: 52365851aef0e0e0ad532ca19a8e0ddccacf7af7
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 8%

---

# Verwenden von [!DNL Azure Private Link] für Quellen in der API

>[!AVAILABILITY]
>
>Diese Funktion ist nur eingeschränkt verfügbar und wird derzeit nur von den folgenden Quellen unterstützt:
>
>* [[!DNL Azure Blob]](../../connectors/cloud-storage/blob.md)
>* [[!DNL Azure Data Lake Gen2]](../../connectors/cloud-storage/adls-gen2.md)
>* [[!DNL Azure File Storage]](../../connectors/cloud-storage/azure-file-storage.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)

Sie können die [!DNL Azure Private Link]-Funktion verwenden, um private Endpunkte zu erstellen, mit denen sich Ihre Adobe Experience Platform-Quellen verbinden können. Verbinden Sie Ihre Quellen sicher mit einem virtuellen Netzwerk, indem Sie private IP-Adressen verwenden. Dadurch entfallen öffentliche IP-Adressen, und die Angriffsfläche wird reduziert.Vereinfachen Sie die Netzwerkeinrichtung, indem Sie komplexe Konfigurationen für die Übersetzung von Firewall- oder Netzwerkadressen überflüssig machen und gleichzeitig sicherstellen, dass der Datenverkehr nur genehmigte Services erreicht.

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie mit APIs einen privaten Endpunkt erstellen und verwenden können.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).

## Erstellen eines privaten Endpunkts {#create-private-endpoint}

Um einen privaten Endpunkt zu erstellen, stellen Sie eine POST-Anfrage an `/privateEndpoints`.

**API-Format**

```http
POST /privateEndpoints
```

**Anfrage**

Die folgende Anfrage erstellt einen privaten Endpunkt:

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Private Endpoint",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [],
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
    }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihres privaten Endpunkts. |
| `subscriptionId` | Die ID, die Ihrem [!DNL Azure]-Abonnement zugeordnet ist. Weitere Informationen finden Sie im [!DNL Azure] unter [Abrufen Ihrer Abonnement- und Mandanten-IDs aus der [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id). |
| `resourceGroupName` | Der Name Ihrer Ressourcengruppe auf [!DNL Azure]. Eine Ressourcengruppe enthält zugehörige Ressourcen für eine [!DNL Azure]. Weitere Informationen finden Sie im [!DNL Azure] Handbuch unter [Verwalten von Ressourcengruppen](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal). |
| `resourceName` | Der Name Ihrer Ressource. In [!DNL Azure] bezieht sich eine Ressource auf Instanzen wie virtuelle Maschinen, Web-Anwendungen und Datenbanken. Weitere Informationen finden Sie im [!DNL Azure] Handbuch unter [Grundlegendes zum Ressourcen [!DNL Azure] Manager](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview). |
| `fqdns` | Die vollqualifizierten Domain-Namen für Ihre Quelle. Diese Eigenschaft ist nur bei Verwendung der [!DNL Snowflake] erforderlich. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID der Quelle, die Sie verwenden. |
| `connectionSpec.version` | Die Version der Verbindungsspezifikations-ID, die Sie verwenden. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt Folgendes zurück:

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

```json
{
  "id": "2c7f6574-299a-4832-aec5-886e875872e2",
  "name": "ACME Private Endpoint",
  "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
  "resourceGroupName": "acme-sources-experience-platform",
  "resourceName": "acmeexperienceplatform",
  "fqdns": [],
  "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
  },
  "state": "Pending"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die ID Ihres neu erstellten privaten Endpunkts. |
| `name` | Der Name Ihres privaten Endpunkts. |
| `subscriptionId` | Die ID, die Ihrem [!DNL Azure]-Abonnement zugeordnet ist. Weitere Informationen finden Sie im [!DNL Azure] unter [Abrufen Ihrer Abonnement- und Mandanten-IDs aus der [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id). |
| `resourceGroupName` | Der Name Ihrer Ressourcengruppe auf [!DNL Azure]. Eine Ressourcengruppe enthält zugehörige Ressourcen für eine [!DNL Azure]. Weitere Informationen finden Sie im [!DNL Azure] Handbuch unter [Verwalten von Ressourcengruppen](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal). |
| `resourceName` | Der Name Ihrer Ressource. In [!DNL Azure] bezieht sich eine Ressource auf Instanzen wie virtuelle Maschinen, Web-Anwendungen und Datenbanken. Weitere Informationen finden Sie im [!DNL Azure] Handbuch unter [Grundlegendes zum Ressourcen [!DNL Azure] Manager](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview). |
| `fqdns` | Die vollqualifizierten Domain-Namen für Ihre Quelle. Diese Eigenschaft ist nur bei Verwendung der [!DNL Snowflake] erforderlich. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID der Quelle, die Sie verwenden. |
| `connectionSpec.version` | Die Version der Verbindungsspezifikations-ID, die Sie verwenden. |
| `state` | Der aktuelle Status Ihres privaten Endpunkts. Gültige Status sind: <ul><li>`Pending`</li><li>`Failed`</li><li>`Approved`</li><li>`Rejected`</li></ul> |

+++

## Abrufen einer Liste von privaten Endpunkten {#retrieve-private-endpoints}

Um eine Liste privater Endpunkte aus einer bestimmten Sandbox in Ihrer Organisation abzurufen, stellen Sie eine GET-Anfrage an `/privateEndpoints`.

**API-Format**

```http
GET /privateEndpoints
```

**Anfrage**

Die folgende Anfrage ruft eine Liste aller privaten Endpunkte ab, die in Ihrer Organisation vorhanden sind.

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von privaten Endpunkten in Ihrer Organisation zurück.

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinking",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
          {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## Abrufen einer Liste privater Endpunkte für eine bestimmte Quelle {#retrieve-private-endpoints-by-source}

Um eine Liste privater Endpunkte abzurufen, die einer bestimmten Quelle entsprechen, stellen Sie eine GET-Anfrage an den `/privateEndpoints`-Endpunkt und geben Sie die `connectionSpec.id` der Quelle an.

**API-Format**

```http
GET /privateEndpoints?property=connectionSpec.id=={CONNECTION_SPEC_ID}
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | Die Verbindungsspezifikations-ID der Quelle, nach der Sie private Endpunkte suchen möchten. |

**Anfrage**

Die folgende Anfrage ruft eine Liste aller privaten Endpunkte ab, die der Quelle mit der Verbindungsspezifikations-ID entsprechen: `4c10e202-c428-4796-9208-5f1f5732b1cf`.

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?property=connectionSpec.id==4c10e202-c428-4796-9208-5f1f5732b1cf' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste aller privaten Endpunkte zurück, die der Quelle mit der Verbindungsspezifikations-ID `4c10e202-c428-4796-9208-5f1f5732b1cf` entsprechen.

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
    {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## Abrufen eines privaten Endpunkts {#retrieve-specific-private-endpoint}

Um einen bestimmten privaten Endpunkt abzurufen, stellen Sie eine GET-Anfrage an `/privateEndpoints` und geben Sie die ID des privaten Endpunkts an, den Sie abrufen möchten.

**API-Format**

```http
GET /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | Die ID des privaten Endpunkts, den Sie abrufen möchten. |

**Anfrage**

Die folgende Anfrage ruft den privaten Endpunkt mit der ID `2c5699b0-b9b6-486f-8877-ee5e21fe9a9d` ab.

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/2c5699b0-b9b6-486f-8877-ee5e21fe9a9d' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den privaten Endpunkt mit der ID `2c5699b0-b9b6-486f-8877-ee5e21fe9a9d` zurück

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

```json
{
  "items": [
       {
      "id": "2c5699b0-b9b6-486f-8877-ee5e21fe9a9d",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    }
  ]
}
```

+++

## Auflösen eines privaten Endpunkts {#resolve-private-endpoint}

**API-Format**

```http
GET /privateEndpoints?op=autoResolve
```

**Anfrage**

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?op=autoResolve' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "usePrivateLink": true,
              "connectionString": "{CONNECTION_STRING}"
          }
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

+++

**Antwort**

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

```json
{
  "items": [
        {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      } 
    }
  ]
}
```

+++

## Interaktives Authoring aktivieren {#enable-interactive-authoring}

Die interaktive Bearbeitung wird für Funktionen wie das Untersuchen einer Verbindung oder eines Kontos und die Vorschau von Daten verwendet. Um das interaktive Authoring zu aktivieren, stellen Sie eine POST-Anfrage an `/privateEndpoints/interactiveAuthoring` und geben Sie `enable` als Operator in Ihren Abfrageparametern an.

**API-Format**

```http
POST /privateEndpoints/interactiveAuthoring?op=enable
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| `op` | Der Vorgang, den Sie ausführen möchten. Um das interaktive Authoring zu aktivieren, setzen Sie den `op` auf `enable`. |

**Anfrage**

Die folgende Anfrage ermöglicht interaktives Authoring für Ihren privaten Endpunkt und setzt die TTL auf 60 Minuten.

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring?op=enable' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "autoTerminationMinutes": 60
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `autoTerminationMinutes` | Die interaktive Authoring-TTL (Time-to-Live) in Minuten. Die interaktive Bearbeitung wird für Funktionen wie das Untersuchen einer Verbindung oder eines Kontos und die Vorschau von Daten verwendet. Sie können eine TTL von maximal 120 Minuten festlegen. Die Standard-TTL beträgt 60 Minuten. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) zurück.

## Abrufen des Status der interaktiven Inhaltserstellung {#retrieve-interactive-authoring-status}

Um den aktuellen Status des interaktiven Authorings für Ihren privaten Endpunkt anzuzeigen, stellen Sie eine GET-Anfrage an `/privateEndpoints/interactiveAuthoring`.

**API-Format**

```http
GET /privateEndpoints/interactiveAuthoring
```

**Anfrage**

Die folgende Anfrage ruft den Status der interaktiven Bearbeitung ab:

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Antwort**

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

```json
{
    "status": "Disabled"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `status` | Der Status des interaktiven Authorings. Gültige Werte sind: `disabled`, `enabling`, `enabled`. |

+++

## Privaten Endpunkt löschen {#delete-private-endpoint}

Um Ihren privaten Endpunkt zu löschen, stellen Sie eine DELETE-Anfrage an `/privateEndpoints` und geben Sie die ID des Endpunkts an, den Sie löschen möchten.

**API-Format**

```http
DELETE /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | Die ID des privaten Endpunkts, den Sie löschen möchten. |

**Anfrage**

Die folgende Anfrage löscht einen privaten Endpunkt mit der ID: `02a74b31-a566-4a86-9cea-309b101a7f24`.

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 (Erfolg) zurück. Sie können den Löschvorgang überprüfen, indem Sie eine GET-Anfrage an stellen und `/privateEndpoints` und die gelöschte ID als Abfrageparameter angeben.

## Flow Service {#flow-service}

In den folgenden Abschnitten finden Sie Informationen darüber, wie Sie private Endpunkte in Verbindung mit der [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) verwenden können.

### Erstellen einer Verbindung mit einem privaten Endpunkt {#create-base-connection}

Um eine Verbindung mit einem privaten Endpunkt in Experience Platform zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt der [!DNL Flow Service]-API.

**API-Format**

```http
POST /connections/
```

**Anfrage**

Die folgende Anfrage erstellt eine authentifizierte Basisverbindung für [!DNL Snowflake] und verwendet gleichzeitig einen privaten Endpunkt.

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "A base connection for a Snowflake source that uses a private link.",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "{CONNECTION_STRING}",
              "usePrivateLink" : true
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer -Basisverbindung. |
| `description` | (Optional) Eine Beschreibung, die zusätzliche Informationen zu Ihrer Verbindung bereitstellt. |
| `auth.specName` | Die Authentifizierung, die verwendet wird, um Ihre Quelle mit Experience Platform zu verbinden. |
| `auth.params.connectionString` | Die [!DNL Snowflake] Verbindungszeichenfolge. Weitere Informationen finden Sie im [[!DNL Snowflake] API-Authentifizierungshandbuch](../api/create/databases/snowflake.md). |
| `auth.params.usePrivateLink` | Ein boolescher Wert, der bestimmt, ob Sie einen privaten Endpunkt verwenden oder nicht. Legen Sie diesen Wert auf `true` fest, wenn Sie einen privaten Endpunkt verwenden. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID von [!DNL Snowflake]. |
| `connectionSpec.version` | Die Version Ihrer [!DNL Snowflake]-Verbindungsspezifikations-ID. |

+++

**Antwort**

Bei einer erfolgreichen Antwort werden die neu generierte Basisverbindungs-ID und das eTag zurückgegeben.

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

+++

### Abrufen von Verbindungen, die mit einem bestimmten privaten Endpunkt verknüpft sind {#retrieve-connections-by-endpoint}

Um Verbindungen abzurufen, die mit einem bestimmten privaten Endpunkt verknüpft sind, stellen Sie eine GET-Anfrage an den `/connections`-Endpunkt und geben Sie die ID des privaten Endpunkts als Abfrageparameter an.

**API-Format**

```http
GET /connections?property=auth.params.privateEndpointId=={PRIVATE_ENDPOINT_ID}
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| {PRIVATE_ENDPOINT_ID} | Die ID des privaten Endpunkts, der mit den Verbindungen verknüpft ist, die Sie abrufen möchten. |

**Anfrage**

Die folgende Anfrage ruft vorhandene Verbindungen ab, die mit dem privaten Endpunkt mit der ID verknüpft sind: `02a74b31-a566-4a86-9cea-309b101a7f24`.

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.privateEndpointId==02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Verbindungen zurück, die mit dem abgefragten privaten Endpunkt verknüpft sind.

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++

### Abrufen von Verbindungen, die mit einem privaten Endpunkt verknüpft sind {#retrieve-connections}

Um Verbindungen abzurufen, die mit einem privaten Endpunkt verknüpft sind, stellen Sie eine GET-Anfrage an den `/connections`-Endpunkt und geben Sie `property=auth.params.usePrivateLink==true` als Abfrageparameter an.

**API-Format**

```http
GET /connections?property=auth.params.usePrivateLink==true
```

**Anfrage**

Die folgende Anfrage ruft alle Verbindungen in Ihrer Organisation ab, die private Endpunkte verwenden.

+++Anfragebeispiel auswählen, um es anzuzeigen

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.usePrivateLink==true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt alle Verbindungen zurück, die mit privaten Endpunkten verknüpft sind.

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++
