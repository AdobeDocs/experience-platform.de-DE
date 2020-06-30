---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Microsoft Dynamics Connectors mithilfe der Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 5839e4695589455bd32b6e3e33a7c377343f920d
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 1%

---


# Erstellen eines [!DNL Microsoft Dynamics] Connectors mit der [!DNL Flow Service] API

[!DNL Flow Service] dient zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb der Adobe Experience Platform. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die [!DNL Flow Service] API, um Sie durch die Schritte zur Verbindung [!DNL Platform] mit einem [!DNL Microsoft Dynamics] (nachfolgend &quot;Dynamics&quot;) Konto zur Erfassung von CRM-Daten zu führen.

Wenn Sie lieber die Benutzeroberfläche in verwenden möchten, [!DNL Experience Platform]bietet das [Dynamics source Connector-UI-Tutorial](../../../ui/create/crm/dynamics.md) eine schrittweise Anleitung zum Durchführen ähnlicher Aktionen.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): E[!DNL xperience Platform] stellt virtuelle Sandboxes zur Verfügung, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

In den folgenden Abschnitten finden Sie zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Platform] API erfolgreich eine Verbindung [!DNL Flow Service] zu einem Dynamics-Konto herzustellen.

### Erforderliche Berechtigungen erfassen

Damit eine Verbindung [!DNL Flow Service] zu [!DNL Dynamics]hergestellt werden kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `serviceUri` | Die Dienst-URL Ihrer [!DNL Dynamics] Instanz. |
| `username` | Der Benutzername für Ihr [!DNL Dynamics] Benutzerkonto. |
| `password` | Das Kennwort für Ihr [!DNL Dynamics] Konto. |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem Dynamics Dokument](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur [!DNL Experience Platform] Fehlerbehebung.

### Werte für erforderliche Kopfzeilen sammeln

Um [!DNL Platform] APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../../../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen [!DNL Experience Platform] API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform]und auch die der [!DNL Flow Service], werden zu bestimmten virtuellen Sandboxen isoliert. Alle Anforderungen an [!DNL Platform] APIs erfordern einen Header, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

* x-sandbox-name: `{SANDBOX_NAME}`

Für alle Anforderungen, die eine Payload enthalten (POST, PUT, PATCH), ist ein zusätzlicher Medientyp-Header erforderlich:

* Content-Type: `application/json`

## Verbindungsspezifikationen nachschlagen

Bevor Sie eine Verbindung [!DNL Platform] zu einem [!DNL Dynamics] Konto herstellen, müssen Sie sicherstellen, dass die Verbindungsspezifikationen für dieses Konto vorhanden sind [!DNL Dynamics]. Wenn keine Verbindungsspezifikationen vorhanden sind, kann keine Verbindung hergestellt werden.

Jede verfügbare Quelle verfügt über einen eigenen Satz von Verbindungsspezifikationen, um Verbindungseigenschaften wie Authentifizierungsanforderungen zu beschreiben. Sie können Verbindungsspezifikationen nachschlagen, [!DNL Dynamics] indem Sie eine GET-Anforderung ausführen und Abfragen-Parameter verwenden.

**API-Format**

Beim Senden einer GET-Anforderung ohne Abfrage-Parameter werden Verbindungsspezifikationen für alle verfügbaren Quellen zurückgegeben. Sie können die Abfrage einbeziehen, `property=name=="dynamics-online"` um Informationen speziell für [!DNL Dynamics]Sie zu erhalten.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="dynamics-online"
```

**Anfrage**

Die folgende Anforderung ruft die Verbindungsspezifikationen für [!DNL Dynamics]ab.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="dynamics-online"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Verbindungsspezifikationen für [!DNL Dynamics]einschließlich der eindeutigen Kennung (`id`) zurück. Diese ID ist im nächsten Schritt erforderlich, um eine Basisverbindung zu erstellen.

```json
{
    "items": [
        {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "name": "dynamics-online",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for Dynamics-Online",
                    "settings": {
                        "authenticationType": "Office365",
                        "deploymentType": "Online"
                    },
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to dynamics-online",
                        "properties": {
                            "serviceUri": {
                                "type": "string",
                                "description": "The service URL of your Dynamics instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "serviceUri"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Basisverbindung erstellen

Eine Basisverbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro [!DNL Dynamics] Konto ist nur eine Basisverbindung erforderlich, da diese zum Erstellen mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

Führen Sie die folgende POST-Anforderung aus, um eine Basisverbindung zu erstellen.

**API-Format**

```http
POST /connections
```

**Anfrage**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics Base Connection",
        "description": "Base connection for Dynamics account",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.serviceUri` | Der Dienst-URI, der Ihrer [!DNL Dynamics] Instanz zugeordnet ist. |
| `auth.params.username` | Der mit Ihrem [!DNL Dynamics] Konto verknüpfte Benutzername. |
| `auth.params.password` | Das Ihrem [!DNL Dynamics] Konto zugeordnete Kennwort. |
| `connectionSpec.id` | Die Verbindungsspezifikation `id` Ihres [!DNL Dynamics] Kontos, die im vorherigen Schritt abgerufen wurde. |

**Antwort**

Eine erfolgreiche Antwort enthält die eindeutige Kennung der Basisverbindung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine Basisverbindung für Ihr [!DNL Dynamics] Konto mithilfe von APIs erstellt und eine eindeutige ID als Teil des Antwortkörpers erhalten. Sie können diese Basis-Verbindungs-ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie CRM-Systeme mithilfe der Flow Service API [erkunden](../../explore/crm.md).