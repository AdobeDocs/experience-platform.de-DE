---
keywords: Experience Platform;home;popular topics;PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: Erstellen einer PostgreSQL-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service-API eine Verbindung zwischen Adobe Experience Platform und PostgreSQL herstellen.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: 0ca900b77275851076a13dcc4b8b4a9995ddd0be
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 52%

---

# Erstellen einer [!DNL PostgreSQL]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL PostgreSQL] mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu [!DNL PostgreSQL] mithilfe der [!DNL Flow Service] API.

### Sammeln erforderlicher Anmeldeinformationen

Zur [!DNL Flow Service] zur Verbindung mit [!DNL PostgreSQL]müssen Sie die folgende Verbindungseigenschaft angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die Verbindungszeichenfolge, die mit Ihrer [!DNL PostgreSQL] -Konto. Die [!DNL PostgreSQL] Verbindungszeichenfolgenmuster ist: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL PostgreSQL] ist `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

Weiterführende Informationen zum Abrufen einer Verbindungszeichenfolge finden Sie in diesem Abschnitt [[!DNL PostgreSQL] Dokument](https://www.postgresql.org/docs/9.2/app-psql.html).

#### Aktivieren der SSL-Verschlüsselung für Ihre Verbindungszeichenfolge

Sie können die SSL-Verschlüsselung für Ihre [!DNL PostgreSQL] Verbindungszeichenfolge, indem Sie Ihre Verbindungszeichenfolge mit den folgenden Eigenschaften anhängen:

| Eigenschaft | Beschreibung | Beispiel |
| --- | --- | --- |
| `EncryptionMethod` | Ermöglicht die Aktivierung der SSL-Verschlüsselung in der [!DNL PostgreSQL] Daten. | <uL><li>`EncryptionMethod=0`(Deaktiviert)</li><li>`EncryptionMethod=1`(Aktiviert)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Validiert das Zertifikat, das von Ihrer [!DNL PostgreSQL] Datenbank bei `EncryptionMethod` angewendet wird. | <uL><li>`ValidationServerCertificate=0`(Deaktiviert)</li><li>`ValidationServerCertificate=1`(Aktiviert)</li></ul> |

Im Folgenden finden Sie ein Beispiel für eine [!DNL PostgreSQL] Verbindungszeichenfolge an SSL-Verschlüsselung angehängt: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL PostgreSQL]-Authentifizierungsdaten als Teil der Anfrageparameter an.

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
| `auth.params.connectionString` | Die Verbindungszeichenfolge, die mit Ihrer [!DNL PostgreSQL] -Konto. Die [!DNL PostgreSQL] Verbindungszeichenfolgenmuster ist: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Die [!DNL PostgreSQL] Verbindungsspezifikations-IDs: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Basisverbindung. Diese ID ist erforderlich, um Ihre [!DNL PostgreSQL] Datenbank im nächsten Tutorial.

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL PostgreSQL] Verbindung der Basis-Verbindung mit [!DNL Flow Service] API. Sie können diese Basis-Verbindungs-ID in den folgenden Tutorials verwenden:

* [Struktur und Inhalt Ihrer Datentabellen mithilfe des [!DNL Flow Service] API](../../explore/tabular.md)
* [Erstellen Sie einen Datenfluss, um Datenbankdaten mit der [!DNL Flow Service] API](../../collect/database-nosql.md)
