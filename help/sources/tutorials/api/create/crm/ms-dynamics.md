---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Microsoft Dynamics Connectors mithilfe der Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 72c1d53295d5c4204c02959c857edc06f246534c
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 1%

---


# Erstellen eines Microsoft Dynamics Connectors mithilfe der Flow Service API

Mit dem Flow-Dienst werden Kundendaten aus verschiedenen Quellen innerhalb der Adobe Experience Platform erfasst und zentralisiert. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die Flow Service API, um Sie durch die Schritte zu führen, die Plattform mit einem Microsoft Dynamics-Konto (im Folgenden &quot;Dynamics&quot; genannt) zu verbinden, um CRM-Daten zu erfassen.

Wenn Sie die Benutzeroberfläche in Experience Platform lieber verwenden möchten, enthält das Lernprogramm [für die Benutzeroberfläche des](../../../ui/create/crm/dynamics.md) Dynamics-Quell-Connectors eine schrittweise Anleitung zum Durchführen ähnlicher Aktionen.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Quellen](../../../../home.md): Mit Experience Platform können Daten aus verschiedenen Quellen erfasst werden, während Sie gleichzeitig die Möglichkeit haben, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Plattforminstanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der Flow Service API eine Verbindung zwischen Plattform und Dynamikkonto herzustellen.

### Erforderliche Berechtigungen erfassen

Damit der Flow-Dienst eine Verbindung zu Dynamics herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften bereitstellen:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `serviceUri` | Die Dienst-URL Ihrer Dynamics-Instanz. |
| `username` | Der Benutzername für Ihr Dynamics-Benutzerkonto. |
| `password` | Das Kennwort für Ihr Dynamics-Konto. |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem Dynamics Dokument](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche Kopfzeilen sammeln

Um Aufrufe an Plattform-APIs durchzuführen, müssen Sie zunächst das [Authentifizierungstraining](../../../../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform, einschließlich der Ressourcen des Flow-Dienstes, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

* x-sandbox-name: `{SANDBOX_NAME}`

Für alle Anforderungen, die eine Payload enthalten (POST, PUT, PATCH), ist ein zusätzlicher Medientyp-Header erforderlich:

* Content-Type: `application/json`

## Verbindungsspezifikationen nachschlagen

Bevor Sie Platform mit einem Dynamics-Konto verbinden, müssen Sie überprüfen, ob die Verbindungsspezifikationen für Dynamics vorhanden sind. Wenn keine Verbindungsspezifikationen vorhanden sind, kann keine Verbindung hergestellt werden.

Jede verfügbare Quelle verfügt über einen eigenen Satz von Verbindungsspezifikationen, um Verbindungseigenschaften wie Authentifizierungsanforderungen zu beschreiben. Sie können Verbindungsspezifikationen für Dynamics nachschlagen, indem Sie eine GET-Anforderung ausführen und Abfragen-Parameter verwenden.

**API-Format**

Beim Senden einer GET-Anforderung ohne Abfrage-Parameter werden Verbindungsspezifikationen für alle verfügbaren Quellen zurückgegeben. Sie können die Abfrage einbeziehen, um Informationen speziell für Dynamics `property=name=="dynamics-online"` zu erhalten.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="dynamics-online"
```

**Anfrage**

Die folgende Anforderung ruft die Verbindungsspezifikationen für Dynamics ab.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="dynamics-online"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Verbindungsspezifikationen für Dynamics zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Basisverbindung zu erstellen.

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

Eine Basisverbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro Dynamics-Konto ist nur eine Basisverbindung erforderlich, da sie zur Erstellung mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

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
| `auth.params.serviceUri` | Der Dienst-URI, der Ihrer Dynamics-Instanz zugeordnet ist. |
| `auth.params.username` | Der mit Ihrem Dynamics-Konto verknüpfte Benutzername. |
| `auth.params.password` | Das Ihrem Dynamics-Konto zugeordnete Kennwort. |
| `connectionSpec.id` | Die Verbindungsspezifikation `id` Ihres Dynamics-Kontos, die im vorherigen Schritt abgerufen wurde. |

**Antwort**

Eine erfolgreiche Antwort enthält die eindeutige Kennung der Basisverbindung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine Basisverbindung für Ihr Dynamics-Konto mithilfe von APIs erstellt und eine eindeutige ID als Teil des Antwortkörpers erhalten. Sie können diese Basis-Verbindungs-ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie CRM-Systeme mithilfe der Flow Service API [erkunden](../../explore/crm.md).