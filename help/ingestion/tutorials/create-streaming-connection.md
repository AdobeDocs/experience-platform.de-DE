---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen einer Streaming-Verbindung mit der API
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 2%

---


# Erstellen einer Streaming-Verbindung mit der API

In diesem Lernprogramm erfahren Sie, wie Sie mit der Verwendung von Streaming-Ingestion-APIs, die Teil der Data Ingestion Service-APIs der Adobe Experience Platform sind, beginnen können.

## Erste Schritte

Die Registrierung der Streaming-Verbindung ist erforderlich, damit Beginn-Streaming-Daten in die Adobe Experience Platform übertragen werden können. Bei der Registrierung einer Streaming-Verbindung müssen Sie einige wichtige Details wie die Quelle der Streaming-Daten angeben.

Nach der Registrierung einer Streaming-Verbindung haben Sie als Datenproduzent eine eindeutige URL, die zum Streamen von Daten an die Platform verwendet werden kann.

Dieses Tutorial erfordert auch ein Fachwissen über verschiedene Adobe Experience Platformen-Services. Bevor Sie mit diesem Lernprogramm beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [Erlebnisdatenmodell (XDM)](../../xdm/home.md): Der standardisierte Rahmen, nach dem Platform Erlebnisdaten organisiert.
- [Echtzeit-Profil](../../profile/home.md): Bietet ein einheitliches, benutzerdefiniertes Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen müssen, um erfolgreich Aufrufe von Streaming-Erfassungsschnittstelle-APIs durchführen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt [zum Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung bei Experience Platformen.

### Werte für erforderliche Kopfzeilen sammeln

Um Platformen-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in der Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Platform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in der Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

## Verbindung herstellen

Eine Verbindung gibt die Quelle an und enthält die Informationen, die erforderlich sind, um den Fluss mit Streaming-APIs kompatibel zu machen.

**API-Format**

```http
POST /flowservice/connections
```

**Anfrage**

>[!NOTE]
>
>Die Werte für die aufgelisteten `providerId` und die `connectionSpec` müssen **** wie im Beispiel gezeigt verwendet werden, da sie der API entsprechen, über die Sie eine Streaming-Verbindung für die Streaming-Erfassung erstellen.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 201 mit Details zur neu erstellten Verbindung zurück.

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Die `id` neu erstellte Verbindung. Dies wird hier als `{CONNECTION_ID}`. |
| `etag` | Eine der Verbindung zugewiesene Kennung, die die Revision der Verbindung angibt. |

## Abrufen der Datenerfassungs-URL

Mit der erstellten Verbindung können Sie jetzt Ihre Datenerfassungs-URL abrufen.

**API-Format**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der `id` Wert der zuvor erstellten Verbindung. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit detaillierten Informationen zur angeforderten Verbindung zurück. Die Datenerfassungs-URL wird automatisch mit der Verbindung erstellt und kann mit dem `inletUrl` Wert abgerufen werden.

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## Nächste Schritte

Nachdem Sie jetzt eine Streaming-Verbindung erstellt haben, können Sie entweder Zeitreihen- oder Datensatzdaten streamen, um Daten innerhalb der Platform zu erfassen. Informationen zum Streamen von Zeitreihendaten in die Platform finden Sie im Lernprogramm zu [Streaming-Zeitreihen](./streaming-time-series-data.md). Informationen zum Streamen von Datensatzdaten in die Platform finden Sie im Tutorial [Streaming-Datensatzdaten](./streaming-record-data.md).

## Anhang

Dieser Abschnitt enthält zusätzliche Informationen zum Erstellen von Streaming-Verbindungen mit der API.

### Authentifizierte Streaming-Verbindungen

Die authentifizierte Datenerfassung ermöglicht es Adobe Experience Platformen-Diensten, z. B. Echtzeit-Kundendaten und -Identitäten, zwischen Datensätzen aus vertrauenswürdigen Quellen und nicht vertrauenswürdigen Quellen zu unterscheiden. Kunden, die persönliche identifizierbare Informationen (PII) senden möchten, können dies tun, indem sie IMS-Zugriffstoken als Teil der POST-Anforderung senden - wenn das IMS-Token gültig ist, werden die Datensätze als von vertrauenswürdigen Quellen erfasst markiert.

Weitere Informationen zum Erstellen einer authentifizierten Streaming-Verbindung finden Sie im Lernprogramm zum [Erstellen einer authentifizierten Streaming-Verbindung](create-authenticated-streaming-connection.md).