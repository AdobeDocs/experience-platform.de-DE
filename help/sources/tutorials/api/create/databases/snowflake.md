---
keywords: Experience Platform;Home;beliebte Themen;Snowflake;snowflake
solution: Experience Platform
title: Erstellen einer Snowflake-Basisverbindung mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mit der Flow Service-API mit Snowflake verbinden.
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 76b3e3e9bcb27eb2bd6981ae6eb109410ae16336
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 10%

---

# Erstellen Sie eine [!DNL Snowflake] Basisverbindung mit [!DNL Flow Service] API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Snowflake] mit [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu kennzeichnen und zu verbessern, indem Sie [!DNL Platform] Dienstleistungen.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Plattform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe von Plattform-APIs durchführen, finden Sie im Handbuch zu [Erste Schritte mit Plattform-APIs](../../../../../landing/api-guide.md).

Im folgenden Abschnitt finden Sie weitere Informationen, die Sie benötigen, um eine Verbindung zu [!DNL Snowflake] mit [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

In der Reihenfolge [!DNL Flow Service] Verbindung herstellen mit [!DNL Snowflake], müssen Sie die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `account` | Der vollständige Kontoname, der Ihrem [!DNL Snowflake] Konto. Eine vollqualifizierte [!DNL Snowflake] Der Kontoname enthält Ihren Kontonamen, Ihre Region und Ihre Cloud-Plattform. Beispiel: `cj12345.east-us-2.azure`. Weitere Informationen zu Kontonamen finden Sie in dieser [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| `warehouse` | Die [!DNL Snowflake] warehouse verwaltet den Ausführungsprozess der Abfrage für die Anwendung. Jeden [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss einzeln aufgerufen werden, wenn Daten an Platform übertragen werden. |
| `database` | Die [!DNL Snowflake] -Datenbank enthält die Daten, die Sie zur Übertragung der Plattform benötigen. |
| `username` | Der Benutzername für [!DNL Snowflake] Konto. |
| `password` | Das Kennwort für die [!DNL Snowflake] Benutzerkonto. |
| `connectionString` | Die Verbindungszeichenfolge, die für die Verbindung mit Ihrem [!DNL Snowflake] Instanz. Das Muster der Verbindungszeichenfolge für [!DNL Snowflake] ist `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Verbindungseigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für das Erstellen der Basis- und Quellverbindungen. Verbindungsspezifikations-ID für [!DNL Snowflake] ist `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [[!DNL Snowflake] Dokument](https://docs.snowflake.com/en/user-guide/oauth-custom.html).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Plattform gespeichert, einschließlich der Authentifizierungsinformationen Ihrer Quelle, des aktuellen Zustands der Verbindung und Ihrer eindeutigen Basis-Verbindungs-ID. Die Basis-Verbindungs-ID ermöglicht es Ihnen, Dateien von der Quelle aus zu erkunden und zu navigieren und die spezifischen Elemente zu identifizieren, die Sie aufnehmen möchten, einschließlich Informationen zu den Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST an `/connections` Endpunkt beim Bereitstellen von [!DNL Snowflake] Authentifizierungsdaten als Teil des Auftrags.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anforderung erstellt eine Basisverbindung für [!DNL Snowflake]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Snowflake base connection",
        "description": "Snowflake base connection",
        "auth": {
            "specName": "Basic Authentication for Snowflake,
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.connectionString` | Die Verbindungszeichenfolge, die für die Verbindung mit Ihrem [!DNL Snowflake] Instanz. Das Muster der Verbindungszeichenfolge für [!DNL Snowflake] ist `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | Die [!DNL Snowflake] Verbindungsspezifikations-ID: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung einschließlich der eindeutigen Verbindungskennung zurück (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Durch Befolgen dieses Tutorials haben Sie eine [!DNL Snowflake] Verbindung mit [!DNL Flow Service] API und den eindeutigen ID-Wert der Verbindung erhalten haben. Sie können diese Verbindungs-ID im nächsten Tutorial verwenden, während Sie lernen, wie Sie diese Verbindung-ID lernen können. [Datenbanken mithilfe der Flow Service API untersuchen](../../explore/database-nosql.md).
