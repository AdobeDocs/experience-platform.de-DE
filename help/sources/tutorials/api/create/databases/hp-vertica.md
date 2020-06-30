---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines HP Vertica-Connectors mit der Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 2%

---


# Erstellen eines HP- [!DNL Vertica] Connectors mithilfe der [!DNL Flow Service] API

>[!NOTE]
>Der HP [!DNL Vertica] -Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

[!DNL Flow Service] dient zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb der Adobe Experience Platform. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die [!DNL Flow Service] API, um Sie durch die Schritte zu führen, mit denen HP verbunden [!DNL Vertica] wird [!DNL Experience Platform].

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

- [Quellen](https://docs.adobe.com/content/help/en/experience-platform/source-connectors/home.html): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zuzuordnen und zu verbessern.
- [Sandboxen](https://docs.adobe.com/content/help/en/experience-platform/sandbox/home.html): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung mit HP [!DNL Vertica] mithilfe der [!DNL Flow Service] API herzustellen.

### Erforderliche Berechtigungen erfassen

Damit [!DNL Flow Service] [!DNL Vertica]eine Verbindung mit HP hergestellt werden kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die Verbindungszeichenfolge, mit der eine Verbindung zu Ihrer HP- [!DNL Vertica] Instanz hergestellt wird. Das Verbindungszeichenfolgen-Muster für HP [!DNL Vertica] ist `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |
| `connectionSpec.id` | Der zum Erstellen einer Verbindung erforderliche Bezeichner. Die spezifizierte ID für feste Verbindungen für HP [!DNL Vertica] lautet: `a8b6a1a4-5735-42b4-952c-85dce0ac38b5` |

Weitere Informationen zum Erwerb einer Verbindungszeichenfolge finden Sie in [diesem HP Vertica-Dokument](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm).

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](https://docs.adobe.com/content/help/en/experience-platform/landing/troubleshooting.html#reading-example-api-calls) im Handbuch zur [!DNL Experience Platform] Fehlerbehebung.

### Werte für erforderliche Kopfzeilen sammeln

Um [!DNL Platform] APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen [!DNL Experience Platform] API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform]einschließlich Quellschnittstellen werden zu bestimmten virtuellen Sandboxen isoliert. Alle Anforderungen an [!DNL Platform] APIs erfordern einen Header, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

Für alle Anforderungen, die eine Payload enthalten (POST, PUT, PATCH), ist ein zusätzlicher Medientyp-Header erforderlich:

- Content-Type: `application/json`

## Verbindung herstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro HP- [!DNL Vertica] Konto ist nur eine Verbindung erforderlich, da sie zur Erstellung mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```http
POST /connections
```

**Anfrage**

Um eine HP- [!DNL Vertica] Verbindung zu erstellen, muss die eindeutige Verbindungs-spec-ID als Teil der POST-Anforderung angegeben werden. Die Verbindungsspezifikations-ID für HP [!DNL Vertica] ist `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.connectionString` | Die mit Ihrem HP- [!DNL Vertica] Konto verknüpfte Verbindungszeichenfolge. Das Verbindungszeichenfolgen-Muster für HP [!DNL Vertica] lautet: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Die HP- [!DNL Vertica] Verbindungs-spec-ID: `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine HP- [!DNL Vertica] Verbindung mit der [!DNL Flow Service] API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie Datenbanken mithilfe der Flow Service API [untersuchen](../../explore/database-nosql.md).
