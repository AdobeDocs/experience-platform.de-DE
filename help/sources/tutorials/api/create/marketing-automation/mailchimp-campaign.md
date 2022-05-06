---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
solution: Experience Platform
title: Erstellen eines Datenflusses für eine Mailchimp-Kampagne mithilfe der Flow Service-API
topic-legacy: tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit einer Mailchimp-Kampagne verbinden.
exl-id: fd4821c7-6fe1-4cad-8e13-3549dbe0ce98
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '2319'
ht-degree: 100%

---

# Erstellen eines Datenflusses für [!DNL Mailchimp Campaign] mithilfe der Flow Service-API

Das folgende Tutorial führt Sie durch die Schritte zum Erstellen einer Quellverbindung und eines Datenflusses, um [!DNL Mailchimp Campaign]-Daten mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/) an Platform zu übermitteln.

## Voraussetzungen

Bevor Sie eine Verbindung von [!DNL Mailchimp] zu Adobe Experience Platform mit OAuth 2-Aktualisierungs-Code herstellen können, müssen Sie zunächst Ihr Zugriffs-Token für [!DNL MailChimp.] abrufen. Ausführliche Anweisungen zum Ermitteln Ihres Zugriffs-Tokens finden Sie im [[!DNL Mailchimp] OAuth 2-Leitfaden](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/).

## Erstellen einer Basisverbindung {#base-connection}

Nachdem Sie Ihre [!DNL Mailchimp]-Authentifizierungsdaten abgerufen haben, können Sie jetzt mit dem Erstellen des Datenflusses beginnen, um [!DNL Mailchimp Campaign]-Daten in Platform zu bringen. Der erste Schritt bei der Erstellung eines Datenflusses besteht darin, eine Basisverbindung zu erstellen.

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

[!DNL Mailchimp] unterstützt sowohl einfache Authentifizierung als auch OAuth 2-Aktualisierungs-Code. In den folgenden Beispielen finden Sie Anleitungen zum Authentifizieren mit beiden Authentifizierungstypen.

### Erstellen einer [!DNL Mailchimp]-Basisverbindung mit einfacher Authentifizierung

Um eine [!DNL Mailchimp]-Basisverbindung mit einfacher Authentifizierung zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt der [!DNL Flow Service]-API und geben dabei die Anmeldeinformationen für Ihre `host`, `authorizationTestUrl`, `username` und `password` an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Mailchimp base connection with basic authentication",
      "description": "Mailchimp Campaign base connection with basic authentication",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Basisverbindung. Stellen Sie sicher, dass der Name Ihrer Basisverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Basisverbindung nachschlagen können. |
| `description` | (Optional) Eine Eigenschaft, die Sie einbeziehen können, um weitere Informationen zu Ihrer Basisverbindung bereitzustellen. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID Ihrer Quelle. Diese ID kann abgerufen werden, nachdem Ihre Quelle registriert und über die [!DNL Flow Service]-API genehmigt wurde. |
| `auth.specName` | Der Authentifizierungstyp, mit dem Sie Ihre Quelle mit Platform verbinden. |
| `auth.params.host` | Die Stamm-URL, die zum Herstellen einer Verbindung mit der [!DNL Mailchimp]-API verwendet wird. Das Format für die Stamm-URL ist `https://{DC}.api.mailchimp.com`, wobei `{DC}` das Rechenzentrum darstellt, das Ihrem Konto entspricht. |
| `auth.params.authorizationTestUrl` | (Optional) Die URL für den Autorisierungstest wird verwendet, um Anmeldeinformationen beim Erstellen einer Basisverbindung zu überprüfen. Wenn die Anmeldeinformationen nicht angegeben sind, werden sie stattdessen während des Erstellungsschritts der Quellverbindung automatisch überprüft. |
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL Mailchimp]-Konto entspricht. Dies ist für die einfache Authentifizierung erforderlich. |
| `auth.params.password` | Das Passwort, das Ihrem [!DNL Mailchimp]-Konto entspricht. Dies ist für die einfache Authentifizierung erforderlich. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Basisverbindung zurück, einschließlich ihrer eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um die Dateistruktur und Inhalte Ihrer Quelle im nächsten Schritt zu untersuchen.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

### Erstellen einer [!DNL Mailchimp]-Basisverbindung mit OAuth 2-Aktualisierungs-Code

Um eine [!DNL Mailchimp]-Basisverbindung mit OAuth 2-Aktualisierungs-Code zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt, während Sie Anmeldeinformationen für `host`, `authorizationTestUrl` und `accessToken` bereitstellen.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Mailchimp base connection with OAuth 2 refresh code",
      "description": "Mailchimp Campaign base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Basisverbindung. Stellen Sie sicher, dass der Name Ihrer Basisverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Basisverbindung nachschlagen können. |
| `description` | (Optional) Eine Eigenschaft, die Sie einbeziehen können, um weitere Informationen zu Ihrer Basisverbindung bereitzustellen. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID Ihrer Quelle. Diese ID kann abgerufen werden, nachdem Sie Ihre Quelle mit der [!DNL Flow Service]-API registriert haben. |
| `auth.specName` | Der Authentifizierungstyp, mit dem Sie Ihre Quelle für Platform authentifizieren. |
| `auth.params.host` | Die Stamm-URL, mit der die Verbindung zur [!DNL Mailchimp]-API hergestellt wird. Das Format für die Stamm-URL ist `https://{DC}.api.mailchimp.com`, wobei `{DC}` das Rechenzentrum darstellt, das Ihrem Konto entspricht. |
| `auth.params.authorizationTestUrl` | (Optional) Die URL für den Autorisierungstest wird verwendet, um Anmeldeinformationen beim Erstellen einer Basisverbindung zu überprüfen. Wenn die Anmeldeinformationen nicht angegeben sind, werden sie stattdessen während des Erstellungsschritts der Quellverbindung automatisch überprüft. |
| `auth.params.accessToken` | Das entsprechende Zugriffs-Token, das zum Authentifizieren Ihrer Quelle verwendet wird. Dies ist für die OAuth-basierte Authentifizierung erforderlich. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Basisverbindung zurück, einschließlich ihrer eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um die Dateistruktur und Inhalte Ihrer Quelle im nächsten Schritt zu untersuchen.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## Durchsuchen der Quelle {#explore}

Mithilfe der im vorherigen Schritt generierten Basisverbindungs-ID können Sie Dateien und Ordner durch Ausführen von GET-Anfragen untersuchen. Bei der Durchführung von GET-Anfragen zur Analyse der Dateistruktur und des Inhalts Ihrer Quelle müssen Sie die in der folgenden Tabelle aufgeführten Abfrageparameter einbeziehen:

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Die im vorherigen Schritt generierte Basisverbindungs-ID. |
| `{OBJECT_TYPE}` | Der Typ des Objekts, das Sie untersuchen möchten. Für REST-Quellen ist dieser Wert standardmäßig `rest`. |
| `{OBJECT}` | Das Objekt, das Sie untersuchen möchten. |
| `{FILE_TYPE}` | Dieser Parameter ist nur beim Anzeigen eines bestimmten Ordners erforderlich. Der Wert stellt den Pfad des Ordners dar, den Sie untersuchen möchten. |
| `{PREVIEW}` | Ein boolescher Wert, der definiert, ob der Inhalt der Verbindung die Vorschau unterstützt. |
| `{SOURCE_PARAMS}` | Eine base64-kodierte Zeichenfolge Ihrer `campaign_id`. |

>[!TIP]
>
>Um den akzeptierten Formattyp für `{SOURCE_PARAMS}` abzurufen, müssen Sie die gesamte `campaignId`-Zeichenfolge in base64 kodieren. Beispielsweise entspricht `{"campaignId": "c66a200cda"}` in base64 kodiert `eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9`.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&objectType={OBJECT_TYPE}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**Anfrage**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/05c595e5-edc3-45c8-90bb-fcf556b57c4b/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Struktur der abgefragten Datei zurück.

```json
{
    "data": [
        {
            "emails": [
                {
                    "campaign_id": "c66a200cda",
                    "list_id": "10c097ca71",
                    "list_is_active": true,
                    "email_id": "cff65fb4c5f5828666ad846443720efd",
                    "email_address": "kendall2134@gmail.com",
                    "_links": [
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/CollectionResponse.json"
                        },
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/Response.json"
                        },
                        {
                            "rel": "member",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        }
                    ]
                },
                {
                    "campaign_id": "c66a200cda",
                    "list_id": "10c097ca71",
                    "list_is_active": true,
                    "email_id": "a16b82774b211afaf60902d1afd8abc5",
                    "email_address": "logan9935890967@gmail.com",
                    "_links": [
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/CollectionResponse.json"
                        },
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity/a16b82774b211afaf60902d1afd8abc5",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/Response.json"
                        },
                        {
                            "rel": "member",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/a16b82774b211afaf60902d1afd8abc5",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        }
                    ]
                },
            ]
        }
    ]    
}
```

## Erstellen einer Quellverbindung {#source-connection}

Sie können eine Quellverbindung herstellen, indem Sie eine POST-Anfrage an die [!DNL Flow Service]-API senden. Eine Quellverbindung besteht aus einer Verbindungs-ID, einem Pfad zur Quelldatendatei und einer Verbindungsspezifikations-ID.

Um eine Quellverbindung zu erstellen, müssen Sie auch einen Aufzählungswert für das Datenformat-Attribut definieren.

Verwenden Sie die folgenden Aufzählungswerte für dateibasierte Quellen:

| Datenformat | Aufzählungswert |
| ----------- | ---------- |
| Durch Trennzeichen getrennt | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Setzen Sie für alle tabellenbasierten Quellen den Wert auf `tabular`.

**API-Format**

```https
POST /sourceConnections
```

**Anfrage**

Die folgende Anfrage erstellt eine Quellverbindung für [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp source connection to ingest campaign ID",
      "description": "MailChimp Campaign source connection to ingest campaign ID",
      "baseConnectionId": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "campaignId": "c66a200cda"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Quellverbindung. Stellen Sie sicher, dass der Name Ihrer Quellverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Quellverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie angeben können, um weitere Informationen über Ihre Quellverbindung bereitzustellen. |
| `baseConnectionId` | Die Basisverbindungs-ID von [!DNL Mailchimp]. Diese ID wurde in einem früheren Schritt generiert. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die Ihrer Quelle entspricht. |
| `data.format` | Das Format der [!DNL Mailchimp]-Daten, die Sie aufnehmen möchten. |
| `params.campaignId` | Die [!DNL Mailchimp]-Kampagnen-ID identifiziert eine bestimmte [!DNL Mailchimp]-Kampagne, mit der Sie dann E-Mails an Ihre Listen/Zielgruppen senden können. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Diese ID ist in einem späteren Schritt erforderlich, um einen Datenfluss zu erstellen.

```json
{
    "id": "d6557bf1-7347-415f-964c-9316bd4cbf56",
    "etag": "\"e205c206-0000-0200-0000-615b5c070000\""
}
```

## Erstellen eines XDM-Zielschemas {#target-schema}

Damit die Quelldaten in Platform verwendet werden können, muss ein Zielschema erstellt werden, das die Quelldaten entsprechend Ihren Anforderungen strukturiert. Das Zielschema wird dann verwendet, um einen Platform-Datensatz zu erstellen, in dem die Quelldaten enthalten sind.

Ein Ziel-XDM-Schema kann erstellt werden, indem eine POST-Anfrage an die [Schema-Registrierungs-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/) durchgeführt wird.

Ausführliche Schritte zum Erstellen eines XDM-Zielschemas finden Sie im Tutorial zum [Erstellen eines Schemas mithilfe der API](../../../../../xdm/api/schemas.md).

### Erstellen eines Zieldatensatzes {#target-dataset}

Ein Zieldatensatz kann erstellt werden, indem eine POST-Anfrage an die [Catalog Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) durchgeführt wird, wodurch die ID des Zielschemas in der Payload angegeben wird.

Ausführliche Anweisungen zum Erstellen eines Zieldatensatzes finden Sie im Tutorial zu [Erstellen eines Datensatzes mithilfe der API](../../../../../catalog/api/create-dataset.md).

## Erstellen einer Zielverbindung {#target-connection}

Eine Zielverbindung stellt die Verbindung zum Ziel dar, in das die aufgenommenen Daten übernommen werden. Um eine Zielverbindung zu erstellen, müssen Sie die feste Verbindungsspezifikations-ID angeben, die [!DNL Data Lake] entspricht. Diese ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Sie haben jetzt die eindeutigen Kennungen, ein Zielschema, einen Zieldatensatz und die Verbindungsspezifikations-ID für [!DNL Data Lake]. Anhand dieser Kennungen können Sie mit der [!DNL Flow Service]-API eine Zielverbindung erstellen, um den Datensatz anzugeben, der die eingehenden Quelldaten enthalten wird.

**API-Format**

```https
POST /targetConnections
```

**Anfrage**

Die folgende Anfrage erstellt eine Zielverbindung für [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp target connection",
      "description": "MailChimp Campaign target connection",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6155e3a9bd13651949515f14"
      }
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Der Name Ihrer Zielverbindung. Stellen Sie sicher, dass der Name Ihrer Zielverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Zielverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie für weitere Informationen zu Ihrer Zielverbindung angeben können. |
| `connectionSpec.id` | Die Spezifikations-ID der Verbindung, die [!DNL Data Lake] entspricht. Diese feste ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Das Format der [!DNL Mailchimp]-Daten, die Sie an Platform übermitteln möchten. |
| `params.dataSetId` | Die Zieldatensatz-ID, die in einem vorherigen Schritt abgerufen wurde. |


**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung der neuen Zielverbindung an (`id`). Diese ID ist in späteren Schritten erforderlich.

```json
{
    "id": "9463fe9c-027d-4347-a423-894fcd105647",
    "etag": "\"b902e822-0000-0200-0000-615b5c370000\""
}
```

>[!IMPORTANT]
>
>Funktionen zu Datenvorbereitung werden für [!DNL Mailchimp Campaign] derzeit nicht unterstützt.

<!--
## Create a mapping {#mapping}

In order for the source data to be ingested into a target dataset, it must first be mapped to the target schema that the target dataset adheres to. This is achieved by performing a POST request to Conversion Service with data mappings defined within the request payload.

**API format**

```http
POST /conversion/mappingSets
```

**Request**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "_{TENANT_ID}.schemas.570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
      "xdmVersion": "1.0",
      "mappings": [
      {
        "destinationXdmPath": "person.name.firstName",
        "sourceAttribute": "merge_fields.FNAME",
        "identity": false,
        "version": 0
      },
      {
        "destinationXdmPath": "person.name.lastName",
        "sourceAttribute": "merge_fields.LNAME",
        "identity": false,
        "version": 0
      }
    ]
  }'
```

| Property | Description |
| --- | --- |
| `xdmSchema` | The ID of the [target XDM schema](#target-schema) generated in an earlier step. |
| `mappings.destinationXdmPath` | The destination XDM path where the source attribute is being mapped to. |
| `mappings.sourceAttribute` | The source attribute that needs to be mapped to a destination XDM path. |
| `mappings.identity` | A boolean value that designates whether the mapping set will be marked for [!DNL Identity Service]. |

**Response**

A successful response returns details of the newly created mapping including its unique identifier (`id`). This value is required in a later step to create a dataflow.

```json
{
    "id": "5a365b23962d4653b9d9be25832ee5b4",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

--->

## Erstellen eines Flusses {#flow}

Der letzte Schritt, um [!DNL Mailchimp]-Daten an Platform zu senden, besteht darin, einen Datenfluss zu erstellen. Bislang haben Sie die folgenden erforderlichen Werte vorbereitet:

* [Quellverbindungs-ID](#source-connection)
* [Zielverbindungs-ID](#target-connection)

Ein Datenfluss ist für die Planung und Erfassung von Daten aus einer Quelle verantwortlich. Sie können einen Datenfluss erstellen, indem Sie eine POST-Anfrage ausführen und dabei die oben genannten Werte in der Payload angeben.

Um eine Aufnahme zu planen, legen Sie zunächst den Startzeitwert auf die Epochenzeit in Sekunden fest. Anschließend müssen Sie den Wert der Häufigkeit auf eine der folgenden fünf Optionen einstellen: `once`, `minute`, `hour`, `day` oder `week`. Der Intervallwert bezeichnet den Zeitraum zwischen zwei aufeinanderfolgenden Aufnahmen. Für die Erstellung einer einmaligen Aufnahme (`once`) ist keine Festlegung eines Intervalls erforderlich. Für alle anderen Häufigkeiten muss der Intervallwert gleich oder größer als `15` sein.


**API-Format**

```http
POST /flows
```

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp Campaign dataflow",
      "description": "MailChimp Campaign dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "d6557bf1-7347-415f-964c-9316bd4cbf56"
      ],
      "targetConnectionIds": [
          "9463fe9c-027d-4347-a423-894fcd105647"
      ],
      "scheduleParams": {
          "startTime": "1632809759",
          "frequency": "minute",
          "interval": 15
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihres Datenflusses. Stellen Sie sicher, dass der Name Ihres Datenflusses beschreibend ist, da Sie damit Informationen zu Ihrem Datenfluss suchen können. |
| `description` | (Optional) Eine Eigenschaft, die Sie einfügen können, um weitere Informationen zu Ihrem Datenfluss bereitzustellen. |
| `flowSpec.id` | Die Flussspezifikations-ID, die zum Erstellen eines Datenflusses erforderlich ist. Diese feste ID lautet: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | Die entsprechende Version der Flussspezifikations-ID. Dieser Wert ist standardmäßig auf `1.0` festgelegt. |
| `sourceConnectionIds` | Die [Quellverbindungs-ID](#source-connection), die in einem früheren Schritt generiert wurde. |
| `targetConnectionIds` | Die in einem früheren Schritt generierte [ID der Zielverbindung](#target-connection). |
| `scheduleParams.startTime` | Die vorgesehene Startzeit für den Beginn der ersten Datenaufnahme. |
| `scheduleParams.frequency` | Die Häufigkeit, mit der der Datenfluss Daten erfasst. Zulässige Werte sind: `once`, `minute`, `hour`, `day` oder `week`. |
| `scheduleParams.interval` | Das Intervall bezeichnet den Zeitraum zwischen zwei aufeinanderfolgenden Datenflussausführungen. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein. Das Intervall ist nicht erforderlich, wenn die Häufigkeit auf `once` festgelegt ist, und sollte größer oder gleich `15` für andere Frequenzwerte sein. |

**Antwort**

Bei einer erfolgreichen Antwort wird die ID (`id`) des neu erstellten Datenflusses angegeben. Mit dieser ID können Sie Ihren Datenfluss überwachen, aktualisieren oder löschen.

```json
{
    "id": "be2d5249-eeaf-4a74-bdbd-b7bf62f7b2da",
    "etag": "\"7e010621-0000-0200-0000-615b5c9b0000\""
}
```

## Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie die Datenaufnahme überwachen, um Informationen über die Datenflussausführungen, den Abschlussstatus und Fehler anzuzeigen.

**API-Format**

```http
GET /runs?property=flowId=={FLOW_ID}
```

**Anfrage**

Mit der folgenden Anfrage werden die Spezifikationen für einen vorhandenen Datenfluss abgerufen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden Details zu Ihrem Flussvorgang angegeben, einschließlich Informationen zum Erstellungsdatum, zu den Quell- und Zielverbindungen sowie zur eindeutigen Kennung des Flussvorgangs (`id`).

```json
{
    "items": [
        {
            "id": "209812ad-7bef-430c-b5b2-a648aae72094",
            "createdAt": 1633044829955,
            "updatedAt": 1633044838006,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "MailChimp Campaign dataflow",
            "description": "MailChimp Campaign dataflow",
            "flowSpec": {
                "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"7e01322c-0000-0200-0000-615b5d520000\"",
            "etag": "\"7e01322c-0000-0200-0000-615b5d520000\"",
            "sourceConnectionIds": [
                "d6557bf1-7347-415f-964c-9316bd4cbf56"
            ],
            "targetConnectionIds": [
                "9463fe9c-027d-4347-a423-894fcd105647"
            ],
            "inheritedAttributes": {
                "sourceConnections": [
                    {
                        "id": "d6557bf1-7347-415f-964c-9316bd4cbf56",
                        "connectionSpec": {
                            "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "9601747c-6874-4c02-bb00-5732a8c43086",
                            "connectionSpec": {
                                "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "9463fe9c-027d-4347-a423-894fcd105647",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "scheduleParams": {
                "startTime": "1633377385",
                "frequency": "minute",
                "interval": 15
            },
            "runs": "/flows/be2d5249-eeaf-4a74-bdbd-b7bf62f7b2da/runs",
            "lastOperation": {
                "started": 1633377421476,
                "updated": 0,
                "operation": "create"
            },
            "lastRunDetails": {
                "id": "84f95788-3e83-4ce0-8e45-c0a89117c6f1",
                "state": "failed",
                "startedAtUTC": 1633377445979,
                "completedAtUTC": 1633377487082
            }
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `items` | Enthält eine einzige Payload von Metadaten, die mit Ihrer spezifischen Datenflussausführung verknüpft sind. |
| `id` | Zeigt die ID an, die Ihrem Datenfluss entspricht. |
| `state` | Zeigt den aktuellen Status Ihres Datenflusses an. |
| `inheritedAttributes` | Enthält die Attribute, die Ihren Fluss definieren, z. B. IDs für die entsprechende Basis-, Quell- und Zielverbindung. |
| `scheduleParams` | Enthält Informationen zum Aufnahmezeitplan Ihres Datenflusses, z. B. Startzeit (in Epochenzeit), Häufigkeit und Intervall. |
| `transformations` | Enthält Informationen zu den auf Ihren Datenfluss angewendeten Transformationseigenschaften. |
| `runs` | Zeigt die entsprechende Ausführungs-ID Ihres Flusses an. Sie können diese ID verwenden, um bestimmte Flussausführungen zu überwachen. |

## Aktualisieren des Datenflusses

Um den Ausführungsplan, Namen und die Beschreibung Ihres Datenflusses zu aktualisieren, führen Sie eine PATCH-Anfrage an die [!DNL Flow Service]-API aus und geben Sie dabei Ihre Fluss-ID, Version und den neuen Zeitplan an, den Sie verwenden möchten.

>[!IMPORTANT]
>
>Die Kopfzeile `If-Match` ist bei einer PATCH-Anfrage erforderlich. Der Wert für diese Kopfzeile ist die eindeutige Version der Verbindung, die Sie aktualisieren möchten.

**API-Format**

```http
PATCH /flows/{FLOW_ID}
```

**Anfrage**

Mit der folgenden Anfrage werden Ihr Ablaufplan für den Fluss sowie der Name und die Beschreibung Ihres Datenflusses aktualisiert.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/209812ad-7bef-430c-b5b2-a648aae72094' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "2e01f11d-0000-0200-0000-615649660000"' \
  -d '[
          {
              "op": "replace",
              "path": "/scheduleParams/frequency",
              "value": "day"
          },
          {
              "op": "replace",
              "path": "/name",
              "value": "MailChimp Campaign Dataflow 2.0"
          },
          {
              "op": "replace",
              "path": "/description",
              "value": "MailChimp Campaign Dataflow Updated"
          }
      ]'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Der Pfad des zu aktualisierenden Parameters. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Fluss-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Fluss-ID angeben.

```json
{
    "id": "209812ad-7bef-430c-b5b2-a648aae72094",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Löschen des Datenflusses

Mit einer vorhandenen Fluss-ID können Sie einen Datenfluss löschen, indem Sie eine DELETE-Anfrage an die [!DNL Flow Service]-API stellen.

**API-Format**

```http
DELETE /flows/{FLOW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FLOW_ID}` | Der eindeutige `id`-Wert für den Datenfluss, den Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/flows/209812ad-7bef-430c-b5b2-a648aae72094' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück. Sie können den Löschvorgang bestätigen, indem Sie eine Suchanfrage (GET) an den Datenfluss stellen. Die API gibt den HTTP-Fehler 404 (Nicht gefunden) zurück, der angibt, dass der Datenfluss gelöscht wurde.

## Aktualisieren der Verbindung

Um den Namen, die Beschreibung und die Anmeldeinformationen Ihrer Verbindung zu aktualisieren, führen Sie eine PATCH-Anfrage an die [!DNL Flow Service]-API aus und geben Sie dabei Ihre Basisverbindungs-ID, -Version und die neuen Informationen an, die Sie verwenden möchten.

>[!IMPORTANT]
>
>Die Kopfzeile `If-Match` ist bei einer PATCH-Anfrage erforderlich. Der Wert für diese Kopfzeile ist die eindeutige Version der Verbindung, die Sie aktualisieren möchten.

**API-Format**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Der eindeutige `id`-Wert für die Verbindung, die Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage enthält einen neuen Namen und eine neue Beschreibung sowie einen neuen Satz von Anmeldeinformationen, mit denen Sie Ihre Verbindung aktualisieren können.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/connections/4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: 4000cff7-0000-0200-0000-6154bad60000' \
  -d '[
      {
          "op": "replace",
          "path": "/auth/params",
          "value": {
              "username": "mailchimp-member-activity-user",
              "password": "{NEW_PASSWORD}"
          }
      },
      {
          "op": "replace",
          "path": "/name",
          "value": "MailChimp Campaign Connection 2.0"
      },
      {
          "op": "add",
          "path": "/description",
          "value": "Updated MailChimp Campaign Connection"
      }
  ]'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `op` | Der Operationsaufruf, der für die Definition der zum Aktualisieren der Verbindung erforderlichen Aktion verwendet wird. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Der Pfad des zu aktualisierenden Parameters. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Basisverbindungs-ID und ein aktualisiertes E-Tag angegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Verbindungs-ID angeben.

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Löschen Ihrer Verbindung

Nachdem Sie über eine bestehende Basisverbindungs-ID verfügen, führen Sie eine DELETE-Anfrage an die [!DNL Flow Service]-API durch.

**API-Format**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Der eindeutige `id`-Wert für die Basisverbindung, die Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/connections/4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück.

Sie können den Löschvorgang bestätigen, indem Sie eine Suchanfrage (GET) an die Verbindung stellen.
