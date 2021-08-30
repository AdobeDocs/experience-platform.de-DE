---
keywords: Experience Platform;home;popular topics;PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: Erstellen einer PostgreSQL-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service-API eine Verbindung zwischen Adobe Experience Platform und PostgreSQL herstellen.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 11%

---

# Erstellen einer [!DNL PostgreSQL]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL PostgreSQL] mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API erfolgreich eine Verbindung zu [!DNL PostgreSQL] herstellen zu können.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung mit [!DNL PostgreSQL] herstellen kann, müssen Sie die folgende Verbindungseigenschaft angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die Verbindungszeichenfolge, die Ihrem [!DNL PostgreSQL]-Konto zugeordnet ist. Das Verbindungszeichenfolgenmuster [!DNL PostgreSQL] lautet: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL PostgreSQL] ist `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

Weitere Informationen zum Abrufen einer Verbindungszeichenfolge finden Sie in diesem [[!DNL PostgreSQL] Dokument](https://www.postgresql.org/docs/9.2/app-psql.html).

### Verwenden von Platform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe an Platform-APIs durchführen können, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL PostgreSQL]-Authentifizierungsdaten als Teil der Anfrageparameter an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL PostgreSQL]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for PostgreSQL",
        "description": "Test connection for PostgreSQL",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| ------------- | --------------- |
| `auth.params.connectionString` | Die Verbindungszeichenfolge, die Ihrem [!DNL PostgreSQL]-Konto zugeordnet ist. Das Verbindungszeichenfolgenmuster [!DNL PostgreSQL] lautet: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Die Verbindungsspezifikations-IDs [!DNL PostgreSQL]: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Basisverbindung zurück. Diese ID ist erforderlich, um Ihre [!DNL PostgreSQL]-Datenbank im nächsten Tutorial zu untersuchen.

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL PostgreSQL]-Verbindung mit der [!DNL Flow Service]-API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Verbindungs-ID im nächsten Tutorial verwenden, wenn Sie erfahren, wie Sie mit der Flow Service-API](../../explore/database-nosql.md)Datenbanken oder NoSQL-Systeme analysieren können.[
