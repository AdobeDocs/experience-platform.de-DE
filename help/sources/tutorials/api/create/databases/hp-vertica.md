---
keywords: Experience Platform;home;popular topics;Vertica;vertica
solution: Experience Platform
title: Erstellen einer HP Vertica-Basisverbindung mit der Flow Service-API
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service-API eine Verbindung zwischen HP Vertica und Adobe Experience Platform herstellen.
exl-id: 37f831c1-7c82-462a-8338-a0bcaaf08cd1
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 56%

---

# Erstellen einer [!DNL HP Vertica]-Basisverbindung mit der [!DNL Flow Service]-API

>[!NOTE]
>
>Der [!DNL HP Vertica] -Connector befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren finden Sie in der [Übersicht über Quellen](../../../../home.md#terms-and-conditions) .

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL HP Vertica] mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform]-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform stellt virtuelle Sandboxes bereit, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service] -API erfolgreich eine Verbindung zu [!DNL HP Vertica] herstellen zu können.

### Sammeln erforderlicher Anmeldeinformationen

Damit [!DNL Flow Service] eine Verbindung mit [!DNL HP Vertica] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die Verbindungszeichenfolge, die für die Verbindung mit Ihrer [!DNL HP Vertica]-Instanz verwendet wird. Das Verbindungszeichenfolgenmuster für [!DNL HP Vertica] ist `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL HP Vertica] lautet: `a8b6a1a4-5735-42b4-952c-85dce0ac38b5` |

Weitere Informationen zum Erwerb einer Verbindungszeichenfolge finden Sie in [diesem HP Vertica-Dokument](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL HP Vertica]-Authentifizierungsdaten als Teil der Anfrageparameter an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL HP Vertica]:


```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for HP Vertica",
        "description": "Connection for HP Vertica",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `auth.params.connectionString` | Die Verbindungszeichenfolge, die Ihrem [!DNL HP Vertica]-Konto zugeordnet ist. Das Verbindungszeichenfolgenmuster für [!DNL HP Vertica] lautet: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Die [!DNL HP Vertica] Verbindungsspezifikations-ID: `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL HP Vertica]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen Sie einen Datenfluss, um Datenbankdaten mithilfe der [!DNL Flow Service] API an Platform zu übertragen.](../../collect/database-nosql.md)
