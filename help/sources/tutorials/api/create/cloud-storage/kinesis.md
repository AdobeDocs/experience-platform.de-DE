---
keywords: Experience Platform;Home;beliebte Themen;Kinesis;Kininsis;Amazon Kinesis;Amazonaskinese
solution: Experience Platform
title: Erstellen einer Amazon Kinesis-Quellverbindung mit der Flow Service API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service API eine Verbindung zwischen Adobe Experience Platform und einem Amazon Kinesis-Konto herstellen.
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
translation-type: tm+mt
source-git-commit: d6f1521470b8dc630060584189690545c724de6b
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 27%

---

# Erstellen einer [!DNL Amazon Kinesis]-Quellverbindung mit der Flow Service API

[!DNL Flow Service] wird zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb von Adobe Experience Platform verwendet. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die API [!DNL Flow Service], um Sie durch die Schritte zu führen, die notwendig sind, um [!DNL Experience Platform] mit einem [!DNL Amazon Kinesis]-Konto zu verbinden.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne  [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mit der API [!DNL Flow Service] eine Verbindung zu einem [!DNL Amazon Kinesis]-Konto herstellen zu können.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung mit Ihrem [!DNL Amazon Kinesis]-Konto herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `accessKeyId` | Die Zugriffsschlüssel-ID für Ihr [!DNL Kinesis]-Konto. |
| `secretKey` | Der geheime Zugriffsschlüssel für Ihr [!DNL Kinesis]-Konto. |
| `region` | Der Bereich für Ihr [!DNL Kinesis]-Konto. |
| `connectionSpec.id` | Die Verbindungs-ID [!DNL Kinesis]: `86043421-563b-46ec-8e6c-e23184711bf6` |

Weitere Informationen zu diesen Werten finden Sie in [diesem Kinesis-Dokument](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Fehlerbehebungshandbuch für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich derjenigen, die zu [!DNL Flow Service] gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Verbindung erstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro [!DNL Amazon Kinesis]-Konto ist nur eine Verbindung erforderlich, da sie zum Erstellen mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

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
        "name": "Amazon Kinesis connection",
        "description": "Connector for Amazon Kinesis",
        "auth": {
            "specName": "Aws Kinesis authentication credentials",
            "params": {
                "accessKeyId": "{ACCESS_KEY_ID}",
                "secretKey": "{SECRET_KEY}",
                "region: "{REGION}
            }
        },
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.accessKeyId` | Die Zugriffsschlüssel-ID für Ihr [!DNL Kinesis]-Konto. |
| `auth.params.secretKey` | Der geheime Zugriffsschlüssel für Ihr [!DNL Kinesis]-Konto. |
| `auth.params.region` | Der Bereich für Ihr [!DNL Kinesis]-Konto. Weitere Informationen zu Regionen finden Sie im Dokument zur Zulassungsliste [IP-Adresse](../../../../ip-address-allow-list.md) |
| `connectionSpec.id` | Die Verbindungs-ID [!DNL Kinesis]: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Cloud-Datenspeicherung-Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine [!DNL Amazon Kinesis]-Verbindung mit APIs erstellt und eine eindeutige ID als Teil des Antwortkörpers erhalten. Sie können diese Verbindungs-ID verwenden, um Streaming-Daten mit der Flow Service API](../../collect/streaming.md) zu erfassen.[
