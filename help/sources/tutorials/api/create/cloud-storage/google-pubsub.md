---
keywords: Experience Platform;Home;beliebte Themen;Google PubSub;Google-Publikum
solution: Experience Platform
title: Erstellen einer Google PubSub-Quellverbindung mit der Flow Service API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mit der Flow Service API mit einem Google PubSub-Konto verbinden.
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 32%

---

# Erstellen einer [!DNL Google PubSub]-Quellverbindung mit der Flow Service API

>[!NOTE]
>
>Der [!DNL Google PubSub]-Anschluss befindet sich in der Betaversion. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../../../home.md#terms-and-conditions).

Dieses Lernprogramm verwendet die API[[!DNL Flow Service] um Sie durch die Schritte zu führen, die notwendig sind, um [!DNL Google PubSub] (nachfolgend &quot;a3/>&quot;) mit Adobe Experience Platform zu verbinden.](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)[!DNL PubSub]

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu kennzeichnen und zu verbessern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mit der [!DNL Flow Service]-API eine [!DNL PubSub]-Quellverbindung erfolgreich zu erstellen.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung zu [!DNL PubSub] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `projectId` | Die Projekt-ID, die zum Authentifizieren von [!DNL PubSub] erforderlich ist. |
| `credentials` | Die Berechtigung oder der Schlüssel, die für die Authentifizierung von [!DNL PubSub] erforderlich ist. |

Weitere Informationen zu diesen Werten finden Sie im folgenden Dokument [PubSub authentication](https://cloud.google.com/pubsub/docs/authentication). Wenn Sie die dienstkontobasierte Authentifizierung verwenden, finden Sie im folgenden Handbuch [PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) Anweisungen zum Generieren Ihrer Anmeldeinformationen.

>[!TIP]
>
>Wenn Sie die kontobasierte Authentifizierung eines Dienstes verwenden, stellen Sie sicher, dass Sie ausreichend Benutzerzugriff auf Ihr Dienstkonto gewährt haben und dass keine zusätzlichen Leerzeichen im JSON vorhanden sind, wenn Sie Ihre Anmeldeinformationen kopieren und einfügen.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Sammeln von Werten für erforderliche Kopfzeilen

Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in Experience Platform, einschließlich der Ressourcen von [!DNL Flow Service], werden zu bestimmten virtuellen Sandboxen isoliert. Bei allen Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Verbindung erstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro [!DNL PubSub]-Konto ist nur eine Verbindung erforderlich, da sie zum Erstellen mehrerer Datenflüsse verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```http
POST /connections
```

**Anfrage**

Um eine [!DNL PubSub]-POST zu erstellen, müssen die Anbieter-ID und die Verbindungs-ID als Teil der Anforderung angegeben werden. Die Anbieter-ID ist `521eee4d-8cbe-4906-bb48-fb6bd4450033` und die Verbindungs-ID ist `70116022-a743-464a-bbfe-e226a7f8210c`.

**API-Format**

```http
POST /connections
```

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google PubSub connection",
        "description": "Google PubSub connection",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Google PubSub authentication credentials",
            "params": {
                "projectId": "{PROJECT_ID}",
                "credentials": "{CREDENTIALS}"
            }
        },
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.projectId` | Die Projekt-ID, die zum Authentifizieren von [!DNL PubSub] erforderlich ist. |
| `auth.params.credentials` | Die Berechtigung oder der Schlüssel, die für die Authentifizierung von [!DNL PubSub] erforderlich ist. |
| `connectionSpec.id` | Die [!DNL PubSub]-Verbindungs-Spec-ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

**Antwort**

Eine erfolgreiche Antwort gibt die Verbindungs-ID der neu erstellten [!DNL PubSub]-Verbindung zurück. Diese ID ist erforderlich, um Ihre Cloud-Datenspeicherung-Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine [!DNL PubSub]-Verbindung mit der [!DNL Flow Service]-API erstellt und die eindeutige Verbindungs-ID erhalten. Sie können diese Verbindungs-ID verwenden, um Streaming-Daten mit der Flow Service API](../../collect/streaming.md) zu erfassen.[
