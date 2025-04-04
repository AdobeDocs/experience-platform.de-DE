---
title: Erstellen einer Google PubSub-Quellverbindung mit der Flow Service-API
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit einem Google PubSub-Konto verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 46%

---

# Erstellen einer [!DNL Google PubSub]-Quellverbindung mithilfe der Flow Service-API

>[!IMPORTANT]
>
>Die [!DNL Google PubSub] ist im Quellkatalog für Benutzende verfügbar, die Real-Time Customer Data Platform Ultimate erworben haben.

Dieses Tutorial führt Sie durch die Schritte zum Verbinden [!DNL Google PubSub] (nachstehend „[!DNL PubSub]“ genannt) mit Experience Platform mithilfe der [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um [!DNL PubSub] mithilfe der [!DNL Flow Service]-API erfolgreich mit Experience Platform verbinden zu können.

### Sammeln erforderlicher Anmeldedaten

Sie müssen Werte für die unten beschriebenen Verbindungseigenschaften angeben, um Ihr [!DNL PubSub]-Konto mit [!DNL Flow Service] zu verbinden. Weitere Informationen zur Authentifizierung und zur Einrichtung vorausgesetzter Komponenten finden Sie unter [[!DNL PubSub source] Übersicht](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites).

>[!BEGINTABS]

>[!TAB Projektbasierte Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `projectId` | Die zur Authentifizierung von [!DNL PubSub] erforderliche Projekt-ID. |
| `credentials` | Die zum Authentifizieren von [!DNL PubSub] erforderlichen Anmeldedaten. Sie müssen sicherstellen, dass Sie die vollständige JSON-Datei ablegen, nachdem Sie die Leerzeichen aus Ihren Anmeldeinformationen entfernt haben. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quell-Ziel-Verbindungen. Die Spezifikations-ID der [!DNL PubSub]-Verbindung lautet: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!TAB Topic- und abonnementbasierte Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `credentials` | Die zum Authentifizieren von [!DNL PubSub] erforderlichen Anmeldedaten. Sie müssen sicherstellen, dass Sie die vollständige JSON-Datei ablegen, nachdem Sie die Leerzeichen aus Ihren Anmeldeinformationen entfernt haben. |
| `topicName` | Der Name der Ressource, die einen Nachrichtenfeed darstellt. Sie müssen einen Themennamen angeben, wenn Sie Zugriff auf einen bestimmten Datenstrom in Ihrer [!DNL PubSub] gewähren möchten. Das Format des Themennamens lautet: `projects/{PROJECT_ID}/topics/{TOPIC_ID}`. |
| `subscriptionName` | Der Name Ihres [!DNL PubSub]. In [!DNL PubSub] können Sie mit Abonnements Nachrichten empfangen, indem Sie das Thema abonnieren, in dem Nachrichten veröffentlicht wurden. **Hinweis**: Ein einzelnes [!DNL PubSub] kann nur für einen Datenfluss verwendet werden. Um mehrere Datenflüsse durchzuführen, müssen Sie über mehrere Abonnements verfügen. Das Format des Abonnementnamens lautet: `projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}`. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quell-Ziel-Verbindungen. Die Spezifikations-ID der [!DNL PubSub]-Verbindung lautet: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!ENDTABS]

Weitere Informationen zu diesen Werten finden Sie in diesem Dokument [[!DNL PubSub] Authentifizierung](https://cloud.google.com/pubsub/docs/authentication). Um die auf Service-Konten basierende Authentifizierung zu verwenden, lesen Sie dieses [[!DNL PubSub] Handbuch zum Erstellen von Service](https://cloud.google.com/docs/authentication/production#create_service_account)Konten), um Anweisungen zum Generieren Ihrer Anmeldeinformationen zu erhalten.

>[!TIP]
>
>Wenn Sie die auf Service-Konten basierende Authentifizierung verwenden, stellen Sie sicher, dass Sie einen ausreichenden Benutzerzugriff auf Ihr Service-Konto gewährt haben und dass in JSON keine zusätzlichen Leerzeichen vorhanden sind, wenn Sie Ihre Anmeldedaten kopieren und einfügen.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

>[!TIP]
>
>Nach der Erstellung können Sie den Authentifizierungstyp einer [!DNL Google PubSub] Basisverbindung nicht mehr ändern. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Der erste Schritt beim Erstellen einer Quellverbindung besteht darin, Ihre [!DNL PubSub]-Quelle zu authentifizieren und eine Basisverbindungs-ID zu generieren. Mittels einer Basisverbindungs-ID können Sie Dateien aus Ihrer Quelle durchsuchen, zwischen Dateien innerhalb der Quelle navigieren und bestimmte Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt beim Bereitstellen der [!DNL PubSub]-Authentifizierungs-Anmeldedaten als Teil der Anfrageparameter.

Mit der [!DNL PubSub] können Sie den Zugriffstyp angeben, den Sie während der Authentifizierung zulassen möchten. Sie können Ihr Konto so einrichten, dass es Root-Zugriff hat oder den Zugriff auf ein bestimmtes [!DNL PubSub] und -Abonnement einschränkt.

>[!NOTE]
>
>Einem [!DNL PubSub] Projekt zugewiesene Prinzipale (Rollen) werden in allen Themen und Abonnements übernommen, die in einem [!DNL PubSub] Projekt erstellt werden. Wenn Sie möchten, dass ein Prinzipal (eine Rolle) Zugriff auf ein bestimmtes Thema hat, muss dieser Prinzipal (diese Rolle) auch zum entsprechenden Abonnement des Themas hinzugefügt werden. Weitere Informationen finden Sie in der [[!DNL PubSub] Dokumentation zur Zugriffssteuerung](<https://cloud.google.com/pubsub/docs/access-control>).

**API-Format**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Projektbasierte Authentifizierung]

Um eine Basisverbindung mit projektbasierter Authentifizierung zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie Ihre `projectId` und `credentials` im Anfragetext an.

+++Anfrage

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Project Based Authentication",
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
| `auth.params.projectId` | Die zur Authentifizierung von [!DNL PubSub] erforderliche Projekt-ID. |
| `auth.params.credentials` | Die zur Authentifizierung von [!DNL PubSub] erforderlichen Anmeldedaten bzw. der Schlüssel. |
| `connectionSpec.id` | Die [!DNL PubSub]-Verbindungsspezifikations-ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

++++

+++Antwort

Eine erfolgreiche Antwort gibt Details der neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese Basisverbindungs-ID wird im nächsten Schritt benötigt, um eine Quellverbindung zu erstellen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!TAB Topic- und abonnementbasierte Authentifizierung]

Um eine Basisverbindung mit themen- und abonnementbasierter Authentifizierung zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie Ihre `credentials`, `topicName` und `subscriptionName` im Anfragetext an.

+++Anfrage

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Topic & Subscription Based Authentication",
          "params": {
              "credentials": "{CREDENTIALS}",
              "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
              "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}"
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
| `auth.params.credentials` | Die zum Authentifizieren von [!DNL PubSub] erforderlichen Anmeldedaten bzw. der erforderliche Schlüssel. |
| `auth.params.topicName` | Das Projekt-ID- und Themen-ID-Paar für die [!DNL PubSub], auf die Sie Zugriff gewähren möchten. |
| `auth.params.subscriptionName` | Das Projekt-ID- und Abonnement-ID-Paar für die [!DNL PubSub], auf die Sie Zugriff gewähren möchten. |
| `connectionSpec.id` | Die [!DNL PubSub]-Verbindungsspezifikations-ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

+++

+++Antwort

Eine erfolgreiche Antwort gibt Details der neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese Basisverbindungs-ID wird im nächsten Schritt benötigt, um eine Quellverbindung zu erstellen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!ENDTABS]


## Erstellen einer Quellverbindung {#source}

Eine Quellverbindung erstellt und verwaltet die Verbindung zu der externen Quelle, aus der Daten erfasst werden. Eine Quellverbindung besteht aus Informationen wie Datenquelle, Datenformat und einer Quell-Verbindungs-ID, die zum Erzeugen eines Datenflusses erforderlich sind. Eine Quellverbindungsinstanz ist für einen Mandanten und eine Organisation spezifisch.

Um eine Quellverbindung zu erstellen, stellen Sie eine POST-Anfrage an den `/sourceConnections`-Endpunkt der [!DNL Flow Service]-API.

**API-Format**

```http
POST /sourceConnections
```

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Google PubSub source connection",
      "description": "A source connection for Google PubSub",
      "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
      "connectionSpec": {
          "id": "70116022-a743-464a-bbfe-e226a7f8210c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
          "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}",
          "dataType": "raw"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Quellverbindung. Stellen Sie sicher, dass der Name Ihrer Quellverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Quellverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie angeben können, um weitere Informationen zu Ihrer Quellverbindung einzuschließen. |
| `baseConnectionId` | Die ID der Basisverbindung Ihrer [!DNL PubSub]-Quelle, die im vorhergehenden Schritt generiert wurde. |
| `connectionSpec.id` | Die feste Verbindungsspezifikations-ID für [!DNL PubSub]. Diese ID lautet: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | Das Format der [!DNL PubSub]-Daten, die Sie aufnehmen möchten. Derzeit wird nur das Datenformat `json` unterstützt. |
| `params.topicName` | Der Name Ihres [!DNL PubSub]. In [!DNL PubSub] ist ein Thema eine benannte Ressource, die einen Feed von Nachrichten darstellt. |
| `params.subscriptionName` | Der Abonnementname, der einem bestimmten Thema entspricht. In [!DNL PubSub] können Sie mit Abonnements Nachrichten aus einem Thema lesen. Ein oder mehrere Abonnements können einem einzelnen Thema zugewiesen werden. |
| `params.dataType` | Dieser Parameter definiert den Typ der aufgenommenen Daten. Zu den unterstützten Datentypen gehören: `raw` und `xdm`. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Diese ID ist im nächsten Tutorial zum Erstellen eines Datenflusses erforderlich.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL PubSub]-Quellverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Quellverbindungs-ID im nächsten Tutorial verwenden, um [einen Streaming-Datenfluss mit der  [!DNL Flow Service] -API](../../collect/streaming.md) zu erstellen.
