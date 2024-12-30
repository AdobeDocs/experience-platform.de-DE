---
title: Erstellen einer Google BigQuery-Basisverbindung mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit Google BigQuery verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 1fa79b31b5a257ebb3cbd60246b757d8a4a63d7c
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 53%

---

# Erstellen einer [!DNL Google BigQuery]-Basisverbindung mithilfe der [!DNL Flow Service]-API

>[!IMPORTANT]
>
>Die [!DNL Google BigQuery] ist im Quellkatalog für Benutzende verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie eine Basisverbindung für [!DNL Google BigQuery] mithilfe der [[!DNL Flow Service] API) ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API eine Verbindung zu [!DNL Google BigQuery] herstellen zu können.

### Sammeln erforderlicher Anmeldedaten

Ausführliche Schritte zum Sammeln [[!DNL Google BigQuery]  erforderlichen Anmeldeinformationen finden Sie ](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) Authentifizierungshandbuch .

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungs-Anmeldedaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Google BigQuery]-Authentifizierungs-Anmeldedaten als Teil der Anfrageparameter an.

**API-Format**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung verwenden]

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Google BigQuery] mit einfacher Authentifizierung:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection with basic authentication",
        "description": "Google BigQuery connection with basic authentication",
        "auth": {
            "specName": "Basic Authentication",
            "type": "OAuth2.0",
            "params": {
                    "project": "{PROJECT}",
                    "clientId": "{CLIENT_ID},
                    "clientSecret": "{CLIENT_SECRET}",
                    "refreshToken": "{REFRESH_TOKEN}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `auth.params.project` | Die Projekt-ID des abzufragenden [!DNL Google BigQuery]. gegen. |
| `auth.params.clientId` | Der zum Generieren des Aktualisierungstokens verwendete ID-Wert. |
| `auth.params.clientSecret` | Der zum Generieren des Aktualisierungstokens verwendete Client-Wert. |
| `auth.params.refreshToken` | Das von [!DNL Google] erhaltene Aktualisierungstoken, das zum Autorisieren des Zugriffs auf [!DNL Google BigQuery] verwendet wird. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Google BigQuery]-Verbindung: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

>[!TAB Service-Authentifizierung verwenden]


**Anfrage**

Die folgende Anfrage erstellt eine -Basisverbindung für [!DNL Google BigQuery] unter Verwendung der -Service-Authentifizierung:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery base connection with service account",
        "description": "Google BigQuery connection with service account",
        "auth": {
            "specName": "Service Authentication",
            "params": {
                    "projectId": "{PROJECT_ID}",
                    "keyFileContent": "{KEY_FILE_CONTENT},
                    "largeResultsDataSetId": "{LARGE_RESULTS_DATASET_ID}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `auth.params.projectId` | Die Projekt-ID des abzufragenden [!DNL Google BigQuery]. gegen. |
| `auth.params.keyFileContent` | Die Schlüsseldatei, die zum Authentifizieren des Service-Kontos verwendet wird. Sie müssen den Inhalt der Schlüsseldatei in [!DNL Base64] kodieren. |
| `auth.params.largeResultsDataSetId` | (Optional) Die vorab erstellte [!DNL Google BigQuery]-Datensatz-ID, die erforderlich ist, um Unterstützung für große Ergebnismengen zu ermöglichen. |

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

>[!ENDTABS]


## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Google BigQuery]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um Datenbankdaten mithilfe der -API  [!DNL Flow Service]  Platform zu übertragen](../../collect/database-nosql.md)
