---
title: Verbinden von Google BigQuery mit Experience Platform mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit Google BigQuery verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 1900a8c6a3f3119c8b9049b12f5660cc9fd181a2
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 39%

---

# Verbinden von [!DNL Google BigQuery] mit Experience Platform mithilfe der [!DNL Flow Service]-API

>[!IMPORTANT]
>
>Die [!DNL Google BigQuery] ist im Quellkatalog für Benutzende verfügbar, die Real-Time Customer Data Platform Ultimate erworben haben.

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihre [!DNL Google BigQuery]-Datenbank mithilfe der [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

### Sammeln erforderlicher Anmeldedaten

Lesen Sie das [[!DNL Google BigQuery] Authentifizierungshandbuch](../../../../connectors/databases/bigquery.md#prerequisites), um ausführliche Schritte zum Abrufen Ihrer [!DNL Google BigQuery]-Anmeldeinformationen zu erhalten.

## Verbinden von [!DNL Google BigQuery] mit Experience Platform auf Azure {#azure}

Lesen Sie die folgenden Schritte, um Informationen zum Verbinden Ihrer [!DNL Google BigQuery] mit Experience Platform auf Azure zu erhalten.

### Erstellen einer Basisverbindung für [!DNL Google BigQuery] auf Experience Platform auf Azure {#azure-base}

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungs-Anmeldedaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Google BigQuery]-Authentifizierungs-Anmeldedaten als Teil der Anfrageparameter an.

**API-Format**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung verwenden]

+++Anfrage

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Google BigQuery] mit einfacher Authentifizierung.

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

+++

+++Antwort

Eine erfolgreiche Antwort gibt Details der neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

>[!TAB Service-Authentifizierung verwenden]


+++Anfrage

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

+++

+++Antwort

Eine erfolgreiche Antwort gibt Details der neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

>[!ENDTABS]

## Verbinden von [!DNL Google BigQuery] mit Experience Platform auf Amazon Web Services (AWS) {#aws}

Lesen Sie die folgenden Schritte, um Informationen zum Verbinden Ihrer [!DNL Google BigQuery]-Datenbank mit Experience Platform auf AWS zu erhalten.

### Erstellen einer Basisverbindung für [!DNL Google BigQuery] auf Experience Platform auf AWS

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../../../landing/multi-cloud.md).

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung zum Verbinden von [!DNL Google BigQuery] mit Experience Platform auf AWS.

+++Beispiel auswählen, um es anzuzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google BigQuery base connection on AWS",
      "description": "Google BigQuery base connection on AWS",
      "auth": {
          "specName": "Service Authentication",
          "params": {
                  "projectId": "{PROJECT_ID}",
                  "keyFileContent": "{KEY_FILE_CONTENT},
                  "datasetId": "{DATASET_ID}"
      },
      "connectionSpec": {
          "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `auth.params.projectId` | Die Projekt-ID des abzufragenden [!DNL Google BigQuery]. gegen. |
| `auth.params.keyFileContent` | Die Schlüsseldatei, die zum Authentifizieren des Service-Kontos verwendet wird. Sie müssen den Inhalt der Schlüsseldatei in [!DNL Base64] kodieren. |
| `auth.params.datasetId` | Die Datensatz-ID, die Ihrer [!DNL Google BigQuery] entspricht. Diese ID stellt dar, wo sich die Datentabellen befinden. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihren -Speicher im nächsten Tutorial zu untersuchen.

+++Beispiel auswählen, um es anzuzeigen

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Google BigQuery]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um Datenbankdaten mithilfe der -API  [!DNL Flow Service]  Platform zu übertragen](../../collect/database-nosql.md)
