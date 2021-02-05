---
keywords: Experience Platform;Home;beliebte Themen;authentifizierte Streaming-Verbindung;Streaming-Verbindung;Streaming-Verbindung erstellen;Authentifizierte Streaming-Verbindung erstellen;Streaming-Verbindung;Erfassung;
solution: Experience Platform
title: Authentifizierte Streaming-Verbindung erstellen
topic: tutorial
type: Tutorial
description: Die authentifizierte Datenerfassung ermöglicht es Adobe Experience Platform-Diensten, wie z. B. Echtzeit-Kundendaten und -Identitäten, zwischen Datensätzen aus vertrauenswürdigen Quellen und nicht vertrauenswürdigen Quellen zu unterscheiden.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 67%

---


# Erstellen einer authentifizierten Streaming-Verbindung

Die authentifizierte Datenerfassung ermöglicht es Adobe Experience Platform-Diensten wie [!DNL Real-time Customer Profile] und [!DNL Identity], zwischen Datensätzen aus vertrauenswürdigen Quellen und nicht vertrauenswürdigen Quellen zu unterscheiden. Kunden, die persönliche identifizierbare Informationen (PII) senden möchten, können dies tun, indem sie Zugriffstoken als Teil der POST-Anfrage senden.

## Erste Schritte

Um mit dem Streamen von Daten an die Adobe Experience Platform zu beginnen, ist eine Registrierung der Streaming-Verbindung erforderlich. Bei der Registrierung einer Streaming-Verbindung müssen Sie einige wichtige Details wie die Quelle der Streaming-Daten angeben.

Nach der Registrierung einer Streaming-Verbindung haben Sie als Datenproduzent eine eindeutige URL, die zum Streamen von Daten an [!DNL Platform] verwendet werden kann.

Für dieses Tutorial sind auch Kenntnisse über verschiedene Adobe Experience Platform-Diensten erforderlich. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Der standardisierte Rahmen, mit dem Erlebnisdaten  [!DNL Platform] organisiert werden.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches, benutzerdefiniertes Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die APIs für die Streaming-Erfassung erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

## Verbindung erstellen

Eine Verbindung gibt die Quelle an und enthält die Informationen, die erforderlich sind, um den Fluss mit Streaming-Erfassungs-APIs kompatibel zu machen.

**API-Format**

```http
POST /flowservice/connections
```

**Anfrage**

>[!NOTE]
>
>Die Werte für die aufgelistete `providerId` und die `connectionSpec` **müssen** wie im Beispiel gezeigt verwendet werden, da diese der API anzeigen, dass Sie eine Streaming-Verbindung für die Streaming-Erfassung erstellen.

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
             "name": "Sample connection",
             "authenticationRequired": true
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
| `id` | Die `id` Ihrer neu erstellten Verbindung. Dies wird hier als `{CONNECTION_ID}` bezeichnet. |
| `etag` | Ein der Verbindung zugewiesener Identifikator, die die Revision der Verbindung angibt. |

## Abrufen der Datenerfassungs-URL

Mit der erstellten Verbindung können Sie jetzt Ihre Datenerfassungs-URL abrufen.

**API-Format**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der `id`-Wert der zuvor von Ihnen erstellten Verbindung. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit detaillierten Informationen zur angeforderten Verbindung zurück. Die Datenerfassungs-URL wird automatisch mit der Verbindung erstellt und kann mit dem `inletUrl`-Wert abgerufen werden.

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

Nachdem Sie eine authentifizierte Streaming-Verbindung erstellt haben, können Sie entweder Zeitreihen- oder Datensatzdaten streamen, um Daten innerhalb von [!DNL Platform] zu erfassen. Informationen zum Streamen von Zeitreihendaten auf [!DNL Platform] finden Sie im Datentutorial [Streaming-Zeitreihen](./streaming-time-series-data.md). Informationen zum Streamen von Datensatzdaten auf [!DNL Platform] finden Sie im Tutorial [Streaming-Datensatzdaten](./streaming-record-data.md).

## Anhang

Dieser Abschnitt enthält zusätzliche Informationen zu authentifizierten Streaming-Verbindungen.

### Senden von Nachrichten an eine authentifizierte Streaming-Verbindung

Wenn für eine Streaming-Verbindung die Authentifizierung aktiviert ist, muss der Client die `Authorization`-Kopfzeile zu seiner Anfrage hinzufügen.

Wenn die `Authorization`-Kopfzeile nicht vorhanden ist oder ein ungültiges/abgelaufenes Zugriffstoken gesendet wird, wird eine HTTP 401 Unerlaubt-Antwort zurückgegeben, mit einer ähnlichen Antwort wie folgt:

**Antwort**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```
