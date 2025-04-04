---
title: Verbinden von AWS Redshift mit Experience Platform mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit AWS Redshift verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 30%

---

# Verbinden von [!DNL AWS Redshift] mit Experience Platform mithilfe der [!DNL Flow Service]-API

>[!IMPORTANT]
>
>Die [!DNL AWS Redshift] ist im Quellkatalog für Benutzende verfügbar, die Real-Time Customer Data Platform Ultimate erworben haben.

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihr [!DNL AWS Redshift]-Quellkonto mithilfe der [[!DNL Flow Service] API) mit Adobe Experience Platform ](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../../landing/api-guide.md).

## Verbinden von [!DNL AWS Redshift] mit Experience Platform auf Azure {#azure}

Lesen Sie die folgenden Schritte, um Informationen zum Verbinden Ihrer [!DNL AWS Redshift] mit Experience Platform auf Azure zu erhalten.

### Sammeln erforderlicher Anmeldedaten

Damit [!DNL Flow Service] eine Verbindung mit [!DNL AWS Redshift] herstellen kann, müssen Sie die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| `server` | Der Server-Name Ihrer [!DNL AWS Redshift]. |
| `port` | Der TCP-Port, den ein [!DNL AWS Redshift]-Server verwendet, um auf Client-Verbindungen zu warten. |
| `username` | Der Benutzername, der Ihrem [!DNL AWS Redshift]-Konto zugeordnet ist. |
| `password` | Das Kennwort, das dem Benutzerkonto entspricht. |
| `database` | Die [!DNL AWS Redshift], aus der Daten abgerufen werden sollen. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL AWS Redshift] ist `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [[!DNL AWS Redshift] Dokument](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

### Erstellen einer Basisverbindung für [!DNL AWS Redshift] auf Experience Platform auf Azure [#azure-base]

>[!NOTE]
>
>Der Standardcodierungsstandard für [!DNL Redshift] ist Unicode. Dies kann nicht geändert werden.

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Experience Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen ID der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL AWS Redshift]-Authentifizierungs-Anmeldedaten als Teil der Anfrageparameter an.

**API-Format**

```https
POST /connections
```

**Anfrage**

+++Beispiel auswählen, um es anzuzeigen

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL AWS Redshift]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "AWS-redshift base connection",
      "description": "base connection for AWS-redshift,
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT},
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `auth.params.server` | Der Server-Name Ihrer [!DNL AWS Redshift]. |
| `auth.params.port` | Der TCP-Port, den ein [!DNL AWS Redshift]-Server verwendet, um auf Client-Verbindungen zu warten. |
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL AWS Redshift]-Konto zugeordnet ist. |
| `auth.params.password` | Das Kennwort, das dem Benutzerkonto entspricht. |
| `auth.params.database` | Die [!DNL AWS Redshift], aus der Daten abgerufen werden sollen. |
| `connectionSpec.id` | Die [!DNL AWS Redshift]-Verbindungsspezifikations-ID: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

+++

**Antwort**

+++Beispiel auswählen, um es anzuzeigen

Eine erfolgreiche Antwort gibt die neu erstellte Basisverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

+++

## Verbinden von [!DNL AWS Redshift] mit Experience Platform über AWS Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf AWS Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../../../landing/multi-cloud.md).

Lesen Sie die folgenden Schritte, um Informationen zum Verbinden Ihrer [!DNL AWS Redshift] mit Experience Platform auf AWS zu erhalten.

### Erstellen einer Basisverbindung für [!DNL AWS Redshift] auf Experience Platform auf AWS {#aws-base}

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL AWS Redshift]:

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
      "name": "AWS Redshift base connection for Experience Platform on AWS",
      "description": "AWS Redshift base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "5439",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `auth.params.server` | Der Server-Name Ihrer [!DNL AWS Redshift]. |
| `auth.params.port` | Der TCP-Port, den ein [!DNL AWS Redshift]-Server verwendet, um auf Client-Verbindungen zu warten. |
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL AWS Redshift]-Konto zugeordnet ist. |
| `auth.params.password` | Das Kennwort, das dem Benutzerkonto entspricht. |
| `auth.params.database` | Die [!DNL AWS Redshift], aus der Daten abgerufen werden sollen. |
| `auth.params.schema` | Der Name des Schemas, das Ihrer [!DNL AWS Redshift]-Datenbank zugeordnet ist. Sie müssen sicherstellen, dass der Benutzer, dem Sie Datenbankzugriff gewähren möchten, auch Zugriff auf dieses Schema hat. |
| `connectionSpec.id` | Die [!DNL AWS Redshift]-Verbindungsspezifikations-ID: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

+++

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihren -Speicher im nächsten Tutorial zu untersuchen.

+++Beispiel auswählen, um es anzuzeigen

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++


## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL AWS Redshift]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um Datenbankdaten mithilfe der API  [!DNL Flow Service]  Experience Platform zu übertragen](../../collect/database-nosql.md)
