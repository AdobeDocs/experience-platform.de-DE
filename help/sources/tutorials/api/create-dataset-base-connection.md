---
keywords: Experience Platform; Startseite; beliebte Themen; Datensatzverbindungsflussdienst; Flussdienst; Flussdienstverbindung
solution: Experience Platform
title: Erstellen einer Adobe Experience Platform-Datensatzbasisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service-API eine Datensatzbase-Verbindung zu Adobe Experience Platform erstellen.
exl-id: 5e829f4a-954b-4011-a003-c42c7a0d5617
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 38%

---

# Erstellen Sie eine [!DNL Experience Platform]-Datensatzbase-Verbindung mithilfe der [!DNL Flow Service]-API.

[!DNL Flow Service] wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von Adobe Experience Platform zu sammeln und zu zentralisieren. Der Dienst bietet eine Benutzeroberfläche und eine RESTful-API, über die alle unterstützten Quellen verbunden werden können.

Um Daten von einer Drittanbieterquelle mit [!DNL Platform] zu verbinden, muss zunächst eine Datensatzbase-Verbindung hergestellt werden.

In diesem Tutorial wird die [!DNL Flow Service]-API verwendet, um Sie durch die Schritte zum Erstellen einer Datensatzbase-Verbindung zu führen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)-System](../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Entwicklerhandbuch zur Schema Registry](../../../xdm/api/getting-started.md): Enthält wichtige Informationen, die Sie benötigen, um die Schema Registry-API erfolgreich aufrufen zu können. Diese umfassen Ihre `{TENANT_ID}`, das Konzept sogenannter „Container“ und die für Anfragen erforderlichen Kopfzeilen, von denen insbesondere die Accept-Kopfzeile und deren mögliche Werte wichtig sind.
* [Catalog Service](../../../catalog/home.md): Catalog ist „System of Record“ für die Position und Herkunft von Daten in [!DNL Experience Platform].
* [Batch-Erfassung](../../../ingestion/batch-ingestion/overview.md): Mit der Batch-Aufnahme-API können Sie Daten als Batch-Dateien in Experience Platform erfassen.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API erfolgreich eine Verbindung zum Data Lake herstellen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, werden in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Verbindungsspezifikationen nachschlagen

Der erste Schritt beim Erstellen einer Datensatzbase-Verbindung besteht darin, eine Reihe von Verbindungsspezifikationen aus [!DNL Flow Service] abzurufen.

**API-Format**

Jede verfügbare Quelle verfügt über einen eigenen Satz von Verbindungsspezifikationen zur Beschreibung der Connector-Eigenschaften, z. B. Authentifizierungspflichten. Sie können Verbindungsspezifikationen für eine Datensatzbase-Verbindung nachschlagen, indem Sie eine GET-Anfrage ausführen und Abfrageparameter verwenden.

Wenn Sie eine GET-Anfrage ohne Abfrageparameter senden, werden Verbindungsspezifikationen für alle verfügbaren Quellen zurückgegeben. Sie können die Abfrage `property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"` einschließen, um Informationen für Ihre Datensatzbase-Verbindung zu erhalten.

```http
GET /connectionSpecs
GET /connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"
```

**Anfrage**

Die folgende Anfrage ruft die Verbindungsspezifikationen für eine Datensatzbase-Verbindung ab.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Verbindungsspezifikationen und die eindeutige Kennung (`id`) zurück, die zum Erstellen einer Basisverbindung erforderlich sind.

```json
{
    "items": [
        {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "name": "{NAME}",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "targetSpec": {
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "dataSetId": {
                            "type": "string"
                        }
                    },
                    "required": [
                        "dataSetId"
                    ]
                }
            },
            "attributes": {
                "category": "{CATEGORY}"
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## Erstellen einer Datensatzbase-Verbindung

Eine Basisverbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Es ist nur eine Basisverbindung für Datensätze erforderlich, da sie zur Erstellung mehrerer Quell-Connectoren verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```http
POST /connections
```

**Anfrage**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dataset Base Connection",
        "description": "Dataset Base Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| ------------- | --------------- |
| `connectionSpec.id` | Die Verbindungsspezifikation `id`, die im vorherigen Schritt abgerufen wurde. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um eine Zielverbindung zu erstellen und Daten aus einem Drittanbieter-Quell-Connector zu erfassen.

```json
{
    "id": "d6c3988d-14ef-4000-8398-8d14ef000021",
    "etag": "\"d502e61b-0000-0200-0000-5e62a1f90000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie mithilfe der API [!DNL Flow Service] eine Verbindung zur Datensatzbasis-Verbindung erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Basisverbindung verwenden, um eine Zielverbindung zu erstellen. In den folgenden Tutorials werden die Schritte zum Erstellen einer Zielverbindung beschrieben, je nach verwendeter Kategorie des Quell-Connectors:

* [Cloud-Speicher](./collect/cloud-storage.md)
* [CRM](./collect/crm.md)
* [Kundenerfolg](./collect/customer-success.md)
* [Datenbank](./collect/database-nosql.md)
