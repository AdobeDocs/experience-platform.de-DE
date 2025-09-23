---
title: Verbinden von Capillary mit Experience Platform mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Capillary mithilfe von APIs mit Experience Platform verbinden.
badge: Beta
exl-id: 763792d0-d5dc-40ac-b86a-6a0d26463b71
source-git-commit: 91d6206c6ce387fde365fa72dc79ca79fc0e46fa
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 9%

---

# Verbinden von [!DNL Capillary Streaming Events] mit Experience Platform mithilfe der [!DNL Flow Service]-API

>[!AVAILABILITY]
>
>Die [!DNL Capillary Streaming Events]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../../../home.md#terms-and-conditions) den „Nutzungsbedingungen“ in der Quellenübersicht .

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie mit dem [!DNL Capillary Streaming Events] und der [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) Daten von Ihrem [!DNL Capillary] an Adobe Experience Platform streamen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

### Sammeln erforderlicher Anmeldedaten

Informationen zur Authentifizierung [[!DNL Capillary Streaming Events]  Sie in ](../../../../connectors/loyalty/capillary.md)Übersicht“.

### Verwenden von Experience Platform-APIs

Lesen Sie das Handbuch [Erste Schritte mit Experience Platform-APIs](../../../../../landing/api-guide.md) um Informationen darüber zu erhalten, wie Sie Experience Platform-APIs erfolgreich aufrufen können.

>[!BEGINSHADEBOX]

## Checkliste für Entwicklerprozesse

1. Erstellen oder wählen Sie Ihr Ziel **Experience-Datenmodell (XDM)-Schema** der Schemaregistrierung. Verwenden Sie dieses XDM-Schema, um **Katalog-Service einen** zu erstellen.
2. Erstellen Sie eine **Basisverbindung** um Ihre [!DNL Capillary] Anmeldedaten zu speichern.
3. Erstellen Sie eine **Quellverbindung**, um eine Bindung an Ihre `baseConnectionId` herzustellen.
4. Erstellen Sie eine **Zielverbindung** um sicherzustellen, dass Ihre Daten im Data Lake landen.
5. Verwenden Sie die Datenvorbereitung, um Zuordnungen zu erstellen, die Ihre [!DNL Capillary] Quellfelder den richtigen XDM-Feldern zuordnen.
6. Erstellen eines Datenflusses mit Ihren `sourceConnectionId`, `targetConnectionId` und `mappingID`
7. Testen Sie mit einzelnen Beispielprofilen/Transaktionsereignissen , um Ihren Datenfluss zu überprüfen.

>[!ENDSHADEBOX]

## Erstellen einer Basisverbindung {#base-connection}

Eine Basisverbindung behält Anmeldeinformationen und Verbindungsdetails bei. Um eine Basisverbindung für [!DNL Capillary] zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt der [!DNL Flow Service]-API und geben Sie im Anfragetext Ihre [!DNL Capillary]-Anmeldeinformationen an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Capillary]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary base connection",
    "description": "Base connection to authenticate the [!DNL Capillary] source.",
    "connectionSpec": {
      "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
      "version": "1.0"
    },
    "auth": {
      "specName": "OAuth generic-rest-connector",
      "params": {
        "clientId": "{CLIENT_ID}",
        "clientSecret": "{CLIENT_SECRET}",
        "accessToken": "{ACCESS_TOKEN}"
      }
    }
  }'
```

**Antwort**

```
A successful response returns the newly created base connection, including its unique connection identifier (id). This ID is required to explore your source's file structure and contents in the next step.

{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### Erstellen einer Quellverbindung

Um eine Quellverbindung zu erstellen, stellen Sie eine POST-Anfrage an den `/sourceConnections`-Endpunkt, während Sie Ihre Basisverbindungs-ID angeben.

**API-Format**

```http
POST /flowservice/sourceConnections
```

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Capillary Streaming",
      "description": "Capillary Streaming",
      "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
      "connectionSpec": {
          "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
          "version": "1.0"
      }
    }'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Details zur neu erstellten Quellverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`).

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

### Schemakonfigurationen

>[!BEGINTABS]

>[!TAB Profilaufnahme]

Profile enthalten Identitäts- und Treueattribute. Sehen Sie sich die folgende Payload für ein Beispiel an, das auf dem [!DNL Capillary]-Profilschema basiert. Sie können dieses Schema konfigurieren und einem individuellen XDM-Profil zuordnen.

**Anfrage**

```json
{
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john.doe@capillarytech.com",
        "primary": true
      }
    ]
  },
  "loyalty": {
    "tier": "gold",
    "points": 1250,
    "lifetimePoints": 122,
    "expiredPoints": 12,
    "pointsRedeemed": 500,
    "program": "loyalty program name",
    "status": "active"
  }
}
```

**Antwort**

```json
{
  "id": "8c19f1c3-4b91-47cd-8cb5-b152a93f7349",
  "status": "success",
  "message": "Profile record ingested successfully"
}
```

>[!TAB Transaktionserfassung]

Transaktionen erfassen Commerce-Aktivitäten. Sehen Sie sich die folgende Payload für ein Beispiel an, das auf dem Schema [!DNL Capillary] basiert. Sie können dieses Schema konfigurieren und einem XDM-Erlebnisereignis zuordnen.

**Anfrage**

```json
{
  "_id": "T0001",
  "timestamp": "2025-07-14T12:00:00-06:00",
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john@capillarytech.com",
        "primary": true
      }
    ]
  },
  "commerce": {
    "commerceScope": {
      "storeCode": "HSR"
    },
    "order": {
      "priceTotal": 90
    }
  },
  "productLineItems": [
    {
      "SKU": "sku_01",
      "quantity": 1,
      "priceTotal": 100,
      "name": "Kitkat",
      "discountAmount": 10
    }
  ]
}
```

**Antwort**

```json
{
  "id": "T0001",
  "status": "success",
  "message": "Transaction event ingested successfully"
}
```

>[!ENDTABS]

<!--### Supported Events

The [!DNL Capillary] source supports the following events:

* `pointsIssued`
* `tierDowngraded`
* `tierUpgraded`
* `pointsExpiryChange`
* `pointsExpired`
* `transactionUpdated`
* `customerAdded`
* `tierDowngradeReminder`
* `promotionEarned`
* `pointsExpiryReminder`
* `pointsRedeemed`
* `transactionAdded`
* `tierRenewed`
* `customerUpdated`-->

### Historische Datenmigration

Sie können Ihre historischen Treue- und Transaktionsdaten in Experience Platform importieren. Exportieren Sie einfach Ihre Daten als strukturierte CSV-Dateien aus [!DNL Capillary], übertragen Sie sie mithilfe von [!DNL SFTP] sicher und nehmen Sie sie in Ihre Experience Platform-Datensätze auf. Nach der ersten Migration bleiben Ihre Daten über den ereignisgesteuerten Connector in Echtzeit auf dem neuesten Stand.

### Erstellen eines XDM-Zielschemas {#target-schema}

Ein Experience-Datenmodell (XDM)-Schema bietet eine standardisierte Möglichkeit, Kundenerlebnisdaten in Experience Platform zu organisieren und zu beschreiben. Um Ihre Quelldaten in Experience Platform aufzunehmen, müssen Sie zunächst ein Ziel-XDM-Schema erstellen, das die Struktur und die Datentypen definiert, die Sie aufnehmen möchten. Dieses Schema dient als Blueprint für den Experience Platform-Datensatz, in dem sich Ihre aufgenommenen Daten befinden.

Sie können ein Ziel-XDM-Schema erstellen, indem Sie eine POST-Anfrage an die [Schema Registry-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) senden. Ausführliche Anweisungen zum Erstellen eines XDM-Zielschemas finden Sie in den folgenden Handbüchern:

* [Erstellen eines Schemas mithilfe der API](../../../../../xdm/api/schemas.md).
* [Erstellen eines Schemas über die Benutzeroberfläche](../../../../../xdm/tutorials/create-schema-ui.md).

Nach der Erstellung ist das Ziel-XDM-Schema `$id` später für Ihren Zieldatensatz und Ihre Zuordnung erforderlich.

## Erstellen eines Zieldatensatzes {#target-dataset}

Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, das typischerweise wie eine Tabelle mit Spalten (Schema) und Zeilen (Feldern) strukturiert ist. Daten, die erfolgreich in Experience Platform aufgenommen werden, werden im Data Lake als Datensätze gespeichert. In diesem Schritt können Sie entweder einen neuen Datensatz erstellen oder einen vorhandenen Datensatz verwenden.

Sie können einen Zieldatensatz erstellen, indem Sie eine POST-Anfrage an die [Catalog Service API](https://developer.adobe.com/experience-platform-apis/references/catalog/) senden und dabei die ID des Zielschemas in der Payload angeben. Ausführliche Anweisungen zum Erstellen eines Zieldatensatzes finden Sie im Handbuch unter [Erstellen eines Datensatzes mithilfe der API](../../../../../catalog/api/create-dataset.md).


## Erstellen einer Zielverbindung {#target}

Eine Zielverbindung stellt die Verbindung zum Ziel dar, in das die aufgenommenen Daten übernommen werden. Um eine Zielverbindung zu erstellen, müssen Sie die feste Verbindungsspezifikations-ID angeben, die mit dem Data Lake verknüpft ist. Diese Verbindungsspezifikations-ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**API-Format**

```http
POST /targetConnections
```

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Capillary Target Connection",
      "description": "Capillary Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

### Erstellen einer Zuordnung {#mapping}

Ordnen Sie anschließend Ihre Quelldaten dem Zielschema zu, dem Ihr Zieldatensatz entspricht. Um eine Zuordnung zu erstellen, stellen Sie eine POST-Anfrage an den `mappingSets` der [[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/). Geben Sie Ihre Ziel-XDM-Schema-ID und die Details der Zuordnungssätze an, die Sie erstellen möchten.

Ordnen Sie die Kapillarfelder den entsprechenden XDM-Schemafeldern wie folgt zu:

| Quellschema | Zielschema |
|------------------------------|-------------------------------|
| `identityMap.email.id` | `xdm:identityMap.email[0].id` |
| `loyalty.points` | `xdm:loyalty.points` |
| `loyalty.tier` | `xdm:loyalty.tier` |
| `commerce.order.priceTotal` | `xdm:commerce.order.priceTotal` |
| `productLineItems.SKU` | `xdm:productListItems.SKU` |

>[!TIP]
>
>Sie können die [Ereignisse und Profilzuordnungen](../../../../images/tutorials/create/capillary/mappings.zip) für [!DNL Capillary] herunterladen und [die Dateien in die Datenvorbereitung ](../../../../../data-prep/ui/mapping.md#import-mapping), wenn Sie für die Zuordnung Ihrer Daten bereit sind.

### Erstellen eines Datenflusses {#flow}

Nachdem Sie die Quellverbindung, die Zuordnung und die Zielverbindung erstellt haben, können Sie einen Datenfluss konfigurieren, um Daten aus [!DNL Capillary] in Experience Platform zu verschieben.

Typische Datenflüsse sind:

* **Profildatenfluss**: nimmt [!DNL Capillary] Profildaten in einen Datensatz mit XDM-Kontaktprofilen auf.
* **Transaktionsdatenfluss**: Nimmt [!DNL Capillary] Transaktionsdaten in einen XDM ExperienceEvent-Datensatz auf.

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary dataflow",
    "description": "Capillary → Experience Platform dataflow",
    "flowSpec": {
      "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
      "version": "1.0"
    },
    "sourceConnectionIds": "{SOURCE_CONNECTION_ID}",
    "targetConnectionIds": "{TARGET_CONNECTION_ID}",
    "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "{MAPPING_ID}",
          "mappingVersion": "0"
        }
      }
    ],
    "scheduleParams": {
      "startTime": "1625040887",
      "frequency": "minute",
      "interval": 15
    }
  }'
```

>[!NOTE]
>
>`startTime` befindet sich in der UNIX-Epoche Sekunden.

**Antwort**

Bei einer erfolgreichen Antwort wird Ihr Datenfluss mit der entsprechenden Datenfluss-ID zurückgegeben.

```json
{
  "id": "92f11b8c-0a9f-45a9-8239-60b4e8430a88",
  "status": "enabled",
  "message": "Dataflow created successfully"
}
```

## Umgang mit Fehlern

Der Connector umfasst eine robuste Fehlerbehandlung für die folgenden Szenarien:

* **Authentifizierungsfehler**: aktualisiert automatisch die Adobe-Anmeldeinformationen, wenn die Authentifizierung fehlschlägt.
* **Fehler bei der Ratenbeschränkung**: Implementiert weitere Zustellversuche mit exponentiellem Backoff, wenn die API-Ratenbeschränkungen erreicht sind.
* **Netzwerkfehler**: Protokolliert fehlgeschlagene Netzwerkanfragen und versucht es erneut.
* **Fehler bei der Datenvalidierung**: Protokolliert ungültige Payloads für die manuelle Überprüfung und Auflösung.

Alle Fehler werden mit Details wie Fehlertyp, Zeitstempel, Anfrage-Payload und Adobe-API-Antwort protokolliert, um die Fehlerbehebung und das Debugging zu erleichtern.

## Testen der Verbindung

Gehen Sie wie folgt vor, um zu erfahren, wie Sie Ihre Verbindung testen können:

* Stellen Sie eine GET-Anfrage an `/connections/{BASE_CONNECTION_ID}` und geben Sie Ihre Basisverbindungs-ID an, um zu überprüfen, ob Ihre Basisverbindung vorhanden ist. In diesem Schritt können Sie auch überprüfen, ob der Status Ihrer Basisverbindung auf `active` festgelegt ist.
* Stellen Sie eine GET-Anfrage an `/flowservice/sourceConnections/{SOURCE_CONNECTION_ID}` und geben Sie Ihre Quellverbindungs-ID an, um Ihre Quellverbindung zu überprüfen.
* Verwenden Sie Ihre Streaming-Endpunkt-URL, um eine Beispiel-Payload des Profils zu senden (verwenden Sie dazu die JSON-Datei zur Profilaufnahme).
* Navigieren Sie in der Experience Platform-Benutzeroberfläche zu Ihrem Datensatz und führen Sie eine Abfrage für den Datensatz aus, um Ihre Datensätze zu bestätigen.
* Verwenden Sie die Datenvorbereitungsprotokolle, um nach Fehlern zu suchen.
* Wenn Sie ein Support-Ticket öffnen müssen, stellen Sie sicher, dass Sie über Folgendes verfügen:
   * Payload anfordern
   * Antworttext
   * request-id
   * Zeitstempel
   * Ressourcen-IDs

## Anhang

In der folgenden Dokumentation finden Sie Handbücher zu zusätzlichen Vorgängen

* [Überwachen von Datenflüssen](../../../../../dataflows/ui/monitor-sources.md)
* [Aktualisieren von Datenflüssen](../../../ui/update-dataflows.md)
* [Datenflüsse löschen](../../../ui/delete.md)
* [Quellkonto aktualisieren](../../../ui/update.md)
