---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: Dokumentationsvorlage für Self-Service
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit YOURSOURCE verbinden.
exl-id: c6927a71-3721-461e-9752-8ebc0b7b1cca
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 51%

---

# Erstellen einer *YOURSOURCE*-Verbindung mithilfe der [!DNL Flow Service]-API

*Wenn Sie diese Vorlage durchlaufen, ersetzen oder löschen Sie alle kursiv gedruckten Absätze (beginnend mit diesem).*

*Aktualisieren Sie zunächst die Metadaten (Titel und Beschreibung) oben auf der Seite. Alle Instanzen von DNL auf dieser Seite ignorieren. Dieses Tag hilft unseren maschinellen Übersetzungsprozessen dabei, die Seite korrekt in die verschiedenen Sprachen zu übersetzen, die wir unterstützen. Wir fügen Ihrer Dokumentation nach dem Absenden Tags hinzu.*

## Überblick

*Geben Sie einen kurzen Überblick über Ihr Unternehmen, einschließlich des Nutzens, den es für Kunden bietet. Fügen Sie einen Link zu Ihrer Startseite der Produktdokumentation für weitere Informationen hinzu.*

>[!IMPORTANT]
>
>Dieser Quell-Connector und die Dokumentationsseite werden vom Team *YourSource* erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an *Link oder E-Mail-Adresse einfügen, unter der Sie für Aktualisierungen erreichbar sind*.

## Voraussetzungen

*Fügen Sie in diesem Abschnitt Informationen zu allen Dingen hinzu, die Kundinnen und Kunden beachten müssen, bevor Sie die -Quelle in der Benutzeroberfläche von Adobe Experience Platform einrichten. Dies kann sein über:*

* auf die Zulassungsliste setzen *muss zu einer hinzugefügt werden*
* *Anforderungen für E-Mail-Hashing*
* *Alle Kontospezifikationen auf Ihrer Seite*
* *So erhalten Sie einen API-Schlüssel für die Verbindung mit Ihrer Plattform*

### Sammeln erforderlicher Anmeldedaten

Um eine Verbindung zwischen *YOURSOURCE* und Experience Platform herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| *Anmeldedaten eins* | *Bitte fügen Sie hier eine kurze Beschreibung zu den Authentifizierungsdaten Ihrer Quelle hinzu* | *Bitte fügen Sie hier ein Beispiel für die Authentifizierungsdaten Ihrer Quelle hinzu* |
| *Berechtigung zwei* | *Bitte fügen Sie hier eine kurze Beschreibung zu den Authentifizierungsdaten Ihrer Quelle hinzu* | *Bitte fügen Sie hier ein Beispiel für die Authentifizierungsdaten Ihrer Quelle hinzu* |
| *Berechtigung 3* | *Bitte fügen Sie hier eine kurze Beschreibung zu den Authentifizierungsdaten Ihrer Quelle hinzu* | *Bitte fügen Sie hier ein Beispiel für die Authentifizierungsdaten Ihrer Quelle hinzu* |

Weitere Informationen zu diesen Anmeldeinformationen finden Sie in der Dokumentation zur *YOURSOURCE*-Authentifizierung . *Fügen Sie hier einen Link zur Authentifizierungsdokumentation Ihrer Plattform hinzu*.

## Verbinden von *YOURSOURCE* mit Experience Platform mithilfe der [!DNL Flow Service]-API

Das folgende Tutorial führt Sie durch die Schritte zum Erstellen einer *YOURSOURCE*-Quellverbindung und zum Erstellen eines Datenflusses, um *YOURSOURCE*-Daten mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) an Experience Platform zu übertragen.

### Erstellen einer Basisverbindung {#base-connection}

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Experience Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen ID der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie dabei Ihre *YOURSOURCE*-Authentifizierungsdaten als Teil des Anfragetexts an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für *YOURSOURCE*:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} base connection",
        "description": "{YOURSOURCE} base connection to authenticate to Experience Platform",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "auth": {
            "specName": "OAuth generic-rest-connector",
            "params": {
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}",
                "expirationDate": "{EXPIRATION_DATE}"
            }
        }
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Basisverbindung. Stellen Sie sicher, dass der Name Ihrer Basisverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Basisverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie angeben können, um weitere Informationen zu Ihrer Basisverbindung bereitzustellen. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID Ihrer Quelle. Diese ID kann abgerufen werden, nachdem Ihre Quelle registriert und über die [!DNL Flow Service]-API genehmigt wurde. |
| `auth.specName` | Der Authentifizierungstyp, mit dem Sie Ihre Quelle für Experience Platform authentifizieren. |
| `auth.params.` | Enthält die zum Authentifizieren Ihrer Quelle erforderlichen Anmeldeinformationen. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Basisverbindung zurück, einschließlich ihrer eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um die Dateistruktur und Inhalte Ihrer Quelle im nächsten Schritt zu untersuchen.

```json
{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### Durchsuchen der Quelle {#explore}

Mithilfe der im vorherigen Schritt generierten Basisverbindungs-ID können Sie Dateien und Ordner untersuchen, indem Sie GET-Anfragen ausführen.
Verwenden Sie die folgenden Aufrufe, um den Pfad der Datei zu finden, die Sie in [!DNL Experience Platform] importieren möchten:

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

Bei der Durchführung von GET-Anfragen zur Analyse der Dateistruktur und des Inhalts Ihrer Quelle müssen Sie die in der folgenden Tabelle aufgeführten Abfrageparameter einbeziehen:


| Parameter | Beschreibung |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Die im vorherigen Schritt generierte Basisverbindungs-ID. |
| `objectType=rest` | Der Typ des Objekts, das Sie untersuchen möchten. Derzeit ist dieser Wert immer auf `rest` festgelegt. |
| `{OBJECT}` | Dieser Parameter ist nur beim Anzeigen eines bestimmten Ordners erforderlich. Der Wert stellt den Pfad des Ordners dar, den Sie untersuchen möchten. |
| `fileType=json` | Der Dateityp der Datei, die Sie an Experience Platform übermitteln möchten. Derzeit ist `json` der einzige unterstützte Dateityp. |
| `{PREVIEW}` | Ein boolescher Wert, der definiert, ob der Inhalt der Verbindung die Vorschau unterstützt. |
| `{SOURCE_PARAMS}` | Definiert Parameter für die Quelldatei, die an Experience Platform übermittelt werden soll. Um den akzeptierten Formattyp für `{SOURCE_PARAMS}` abzurufen, müssen Sie die gesamte Zeichenfolge `list_id` in base64 kodieren. Im folgenden Beispiel entspricht `"list_id": "10c097ca71"` in base64 kodierte `eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=`. |


**Anfrage**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/70383d02-2777-4be7-a309-9dd6eea1b46d/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=' \
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
      "members": [
        {
          "id": "cff65fb4c5f5828666ad846443720efd",
          "email_address": "roykent@gmail.com",
          "unique_email_id": "72c758cbf1",
          "full_name": "Roy Kent",
          "web_id": 547094062,
          "email_type": "html",
          "status": "subscribed",
          "merge_fields": {
            "FNAME": "Roy",
            "LNAME": "Kent",
            "ADDRESS": {
              "addr1": "",
              "addr2": "",
              "city": "Richmond",
              "state": "Virginia",
              "zip": "",
              "country": "US"
            },
            "PHONE": "",
            "BIRTHDAY": ""
          },
          "stats": {
            "avg_open_rate": 0,
            "avg_click_rate": 0
          },
          "ip_signup": "",
          "timestamp_signup": "",
          "ip_opt": "103.43.112.97",
          "timestamp_opt": "2021-06-01T15:31:36+00:00",
          "member_rating": 2,
          "last_changed": "2021-06-01T15:31:36+00:00",
          "language": "",
          "vip": false,
          "email_client": "",
          "location": {
            "latitude": 0,
            "longitude": 0,
            "gmtoff": 0,
            "dstoff": 0,
            "country_code": "",
            "timezone": ""
          },
          "source": "Admin Add",
          "tags_count": 0,
          "tags": [
             
          ],
          "list_id": "10c097ca71"
        }
      ],
      "list_id": "10c097ca71",
      "total_items": 2,
      "_links": [
        {
          "rel": "self",
          "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
          "method": "GET",
          "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/CollectionResponse.json",
          "schema": "https://us6.api.mailchimp.com/schema/3.0/Paths/Lists/Members/Collection.json"
        },
        {
          "rel": "parent",
          "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71",
          "method": "GET",
          "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
        },
        {
          "rel": "create",
          "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
          "method": "POST",
          "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
          "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/POST.json"
        }
      ]
    }
  ]
}
```

### Erstellen einer Quellverbindung {#source-connection}

Sie können eine Quellverbindung herstellen, indem Sie eine POST-Anfrage an die [!DNL Flow Service]-API senden. Eine Quellverbindung besteht aus einer Verbindungs-ID, einem Pfad zur Quelldatendatei und einer Verbindungsspezifikations-ID.

**API-Format**

```https
POST /sourceConnections
```

**Anfrage**

Die folgende Anfrage erstellt eine Quellverbindung für *YOURSOURCE*:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} Source Connection",
        "description": "{YOURSOURCE} Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "server": "us6",
            "listId": "10c097ca71"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Quellverbindung. Stellen Sie sicher, dass der Name Ihrer Quellverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Quellverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie angeben können, um weitere Informationen über Ihre Quellverbindung bereitzustellen. |
| `baseConnectionId` | Die Basisverbindungs-ID von *YOURSOURCE*. Diese ID wurde in einem früheren Schritt generiert. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die Ihrer Quelle entspricht. |
| `data.format` | Das Format der *YOURSOURCE*-Daten, die Sie aufnehmen möchten. Derzeit wird nur das Datenformat `json` unterstützt. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Diese ID ist in einem späteren Schritt erforderlich, um einen Datenfluss zu erstellen.

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### Erstellen eines XDM-Zielschemas {#target-schema}

Damit die Quelldaten in Experience Platform verwendet werden können, muss ein Zielschema erstellt werden, das die Quelldaten entsprechend Ihren Anforderungen strukturiert. Das Zielschema wird dann verwendet, um einen Experience Platform-Datensatz zu erstellen, in dem die Quelldaten enthalten sind.

Ein Ziel-XDM-Schema kann erstellt werden, indem eine POST-Anfrage an die [Schema-Registrierungs-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) durchgeführt wird.

Ausführliche Schritte zum Erstellen eines XDM-Zielschemas finden Sie im Tutorial zum [Erstellen eines Schemas mithilfe der API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html#create).

### Erstellen eines Zieldatensatzes {#target-dataset}

Ein Zieldatensatz kann erstellt werden, indem eine POST-Anfrage an die [Catalog Service API](https://developer.adobe.com/experience-platform-apis/references/catalog/) durchgeführt wird, wodurch die ID des Zielschemas in der Payload angegeben wird.

Ausführliche Anweisungen zum Erstellen eines Zieldatensatzes finden Sie im Tutorial zu [Erstellen eines Datensatzes mithilfe der API](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html).

### Erstellen einer Zielverbindung {#target-connection}

Eine Zielverbindung stellt die Verbindung zum Ziel dar, an dem die aufgenommenen Daten gespeichert werden sollen. Um eine Zielverbindung zu erstellen, müssen Sie die feste Verbindungsspezifikations-ID angeben, die [!DNL Data Lake] entspricht. Diese ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Sie haben jetzt die eindeutigen Kennungen, ein Zielschema, einen Zieldatensatz und die Verbindungsspezifikations-ID für [!DNL Data Lake]. Anhand dieser Kennungen können Sie mit der [!DNL Flow Service]-API eine Zielverbindung erstellen, um den Datensatz anzugeben, der die eingehenden Quelldaten enthalten wird.

**API-Format**

```https
POST /targetConnections
```

**Anfrage**

Die folgende Anfrage erstellt eine Zielverbindung für *YOURSOURCE*:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} Target Connection",
        "description": "{YOURSOURCE} Target Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "dataSetId": "5ef4551c52e054191a61a99f"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Der Name Ihrer Zielverbindung. Stellen Sie sicher, dass der Name Ihrer Zielverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Zielverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie für weitere Informationen zu Ihrer Zielverbindung angeben können. |
| `connectionSpec.id` | Die Spezifikations-ID der Verbindung, die [!DNL Data Lake] entspricht. Diese feste ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Das Format der *YOURSOURCE*-Daten, die Sie an Experience Platform übermitteln möchten. |
| `params.dataSetId` | Die Zieldatensatz-ID, die in einem vorherigen Schritt abgerufen wurde. |


**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung der neuen Zielverbindung an (`id`). Diese ID ist in späteren Schritten erforderlich.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### Erstellen einer Zuordnung {#mapping}

Damit die Quelldaten in einen Zieldatensatz aufgenommen werden können, müssen sie zunächst dem Zielschema zugeordnet werden, zu dem der Zieldatensatz gehört. Dies wird durch eine POST-Anfrage an [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) mit Datenzuordnungen erreicht, die in der Anfrage-Payload definiert sind.

**API-Format**

```http
POST /conversion/mappingSets
```

**Anfrage**

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `xdmSchema` | Die ID des [Ziel-XDM-Schema](#target-schema), die in einem früheren Schritt generiert wurde. |
| `mappings.destinationXdmPath` | Der Ziel-XDM-Pfad, dem das Quellattribut zugeordnet wird. |
| `mappings.sourceAttribute` | Das Quellattribut, das einem Ziel-XDM-Pfad zugeordnet werden muss. |
| `mappings.identity` | Ein boolescher Wert, der angibt, ob der Zuordnungssatz für [!DNL Identity Service] markiert wird. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Zuordnung an, einschließlich der eindeutigen Kennung (`id`). Dieser Wert ist in einem späteren Schritt zum Erstellen eines Datenflusses erforderlich.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Erstellen eines Flusses {#flow}

Der letzte Schritt, um Daten von *YOURSOURCE* nach Experience Platform zu übertragen, besteht darin, einen Datenfluss zu erstellen. Bislang haben Sie die folgenden erforderlichen Werte vorbereitet:

* [Quellverbindungs-ID](#source-connection)
* [Zielverbindungs-ID](#target-connection)
* [Zuordnungs-ID](#mapping)

Ein Datenfluss ist für die Planung und Erfassung von Daten aus einer Quelle verantwortlich. Sie können einen Datenfluss erstellen, indem Sie eine POST-Anfrage ausführen und dabei die oben genannten Werte in der Payload angeben.

Um eine Aufnahme zu planen, legen Sie zunächst den Startzeitwert auf die Epochenzeit in Sekunden fest. Anschließend müssen Sie den Frequenzwert auf eine der fünf Optionen festlegen: `once`, `minute`, `hour`, `day` oder `week`. Der Intervallwert bezeichnet den Zeitraum zwischen zwei aufeinander folgenden Aufnahmen. Für die Erstellung einer einmaligen Aufnahme ist jedoch keine Festlegung eines Intervalls erforderlich. Für alle anderen Frequenzen muss der Intervallwert auf gleich oder größer als `15` festgelegt werden.


**API-Format**

```http
POST /flows
```

**Anfrage**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} dataflow",
        "description": "{YOURSOURCE} dataflow",
        "flowSpec": {
            "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "246d052c-da4a-494a-937f-a0d17b1c6cf5"
        ],
        "targetConnectionIds": [
            "7c96c827-3ffd-460c-a573-e9558f72f263"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
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

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihres Datenflusses. Stellen Sie sicher, dass der Name Ihres Datenflusses beschreibend ist, da Sie damit Informationen zu Ihrem Datenfluss suchen können. |
| `description` | Ein optionaler Wert, den Sie angeben können, um weitere Informationen zu Ihrem Datenfluss bereitzustellen. |
| `flowSpec.id` | Die Flussspezifikations-ID, die zum Erstellen eines Datenflusses erforderlich ist. Diese feste ID lautet: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | Die entsprechende Version der Flussspezifikations-ID. Dieser Wert ist standardmäßig auf `1.0` festgelegt. |
| `sourceConnectionIds` | Die [Quellverbindungs-ID](#source-connection), die in einem früheren Schritt generiert wurde. |
| `targetConnectionIds` | Die [Zielverbindungs-ID](#target-connection), die in einem früheren Schritt generiert wurde. |
| `transformations` | Diese Eigenschaft enthält die verschiedenen Umwandlungen, die auf Ihre Daten angewendet werden müssen. Diese Eigenschaft ist erforderlich, wenn nicht-XDM-konforme Daten an Experience Platform übermittelt werden. |
| `transformations.name` | Der Name, der der Transformation zugewiesen wurde. |
| `transformations.params.mappingId` | Die [Zuordnungs-ID](#mapping), die in einem früheren Schritt generiert wurde. |
| `transformations.params.mappingVersion` | Die entsprechende Version der Zuordnungs-ID. Dieser Wert ist standardmäßig auf `0` festgelegt. |
| `scheduleParams.startTime` | Diese Eigenschaft enthält Informationen zur Aufnahmeplanung des Datenflusses. |
| `scheduleParams.frequency` | Die Häufigkeit, mit der der Datenfluss Daten erfasst. Zulässige Werte sind: `once`, `minute`, `hour`, `day` oder `week`. |
| `scheduleParams.interval` | Das Intervall bezeichnet den Zeitraum zwischen zwei aufeinanderfolgenden Datenflussausführungen. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein. Das Intervall ist nicht erforderlich, wenn die Häufigkeit auf `once` festgelegt ist, und sollte größer oder gleich `15` für andere Frequenzwerte sein. |

**Antwort**

Bei einer erfolgreichen Antwort wird die ID (`id`) des neu erstellten Datenflusses angegeben. Mit dieser ID können Sie Ihren Datenfluss überwachen, aktualisieren oder löschen.

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

## Anhang

Im folgenden Abschnitt finden Sie Informationen zu den Schritten, die Sie zum Überwachen, Aktualisieren und Löschen Ihres Datenflusses durchführen können.

### Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie die Datenaufnahme überwachen, um Informationen über die Datenflussausführungen, den Abschlussstatus und Fehler anzuzeigen. Vollständige API-Beispiele finden Sie im Handbuch unter [Überwachen Ihrer Quelldatenflüsse mithilfe der API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Aktualisieren des Datenflusses

Aktualisieren Sie die Details Ihres Datenflusses, z. B. seinen Namen und seine Beschreibung, sowie seinen Ausführungsplan und die zugehörigen Zuordnungssätze, indem Sie eine PATCH-Anfrage an den `/flows`-Endpunkt [!DNL Flow Service] -API stellen und dabei die ID Ihres Datenflusses angeben. Bei einer PATCH-Anfrage müssen Sie die eindeutige `etag` Ihres Datenflusses in der `If-Match`-Kopfzeile angeben. Vollständige API-Beispiele finden Sie im Handbuch unter [Aktualisieren von Quelldatenflüssen mithilfe der API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Konto aktualisieren

Aktualisieren Sie den Namen, die Beschreibung und die Anmeldeinformationen Ihres Quellkontos, indem Sie eine PATCH-Anfrage an die [!DNL Flow Service]-API durchführen und dabei Ihre Basisverbindungs-ID als Abfrageparameter angeben. Bei einer PATCH-Anfrage müssen Sie die eindeutige `etag` Ihres Quellkontos in der `If-Match`-Kopfzeile angeben. Vollständige API-Beispiele finden Sie im Handbuch unter [Aktualisieren Ihres Quellkontos mithilfe der API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Löschen des Datenflusses

Löschen Sie Ihren Datenfluss, indem Sie eine DELETE-Anfrage an die [!DNL Flow Service]-API stellen und dabei die ID des Datenflusses angeben, den Sie als Teil des Abfrageparameters löschen möchten. Vollständige API-Beispiele finden Sie im Handbuch unter [Löschen Ihrer Datenflüsse mithilfe der API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Konto löschen

Löschen Sie Ihr Konto, indem Sie eine DELETE-Anfrage an die [!DNL Flow Service]-API mit Angabe der Basisverbindungs-ID des Kontos ausführen, das Sie löschen möchten. Vollständige API-Beispiele finden Sie im Handbuch unter [Löschen Ihres Quellkontos mithilfe der API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).