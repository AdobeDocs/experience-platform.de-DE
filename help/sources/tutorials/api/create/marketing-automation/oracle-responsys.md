---
keywords: Experience Platform;Startseite;beliebte Themen;oracle;
title: (Beta) Erstellen einer Oracle Responsys-Basisverbindung mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit Oracle Responsys verbinden.
hide: true
hidefromtoc: true
exl-id: 76659f5a-c923-488c-88f6-1919bc6a7bb5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 76%

---

# (Beta) Erstellen einer [!DNL Oracle Responsys]-Basisverbindung mithilfe der [!DNL Flow Service]-API

>[!NOTE]
>
>Die [!DNL Oracle Responsys]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Connectoren finden Sie ](../../../../home.md#terms-and-conditions) „Quellen - Übersicht“ .

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Oracle Responsys] mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform] in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie für eine erfolgreiche Verbindung mit [!DNL Oracle Responsys] unter Verwendung der [!DNL Flow Service]-API benötigen.

### Sammeln erforderlicher Anmeldedaten

Damit [!DNL Flow Service] eine Verbindung mit [!DNL Oracle Responsys] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `endpoint` | Die REST-Authentifizierungsendpunkt-URL Ihrer [!DNL Oracle Responsys]-Instanz. |
| `clientId` | Die Client-ID Ihrer [!DNL Oracle Responsys]-Instanz. |
| `clientSecret` | Das Client-Geheimnis Ihrer [!DNL Oracle Responsys]-Instanz. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Der Wert für die Verbindungsspezifikations-ID der [!DNL Oracle Responsys]-Quelle ist wie folgt festgelegt: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

Weitere Informationen zu Authentifizierungs-Anmeldedaten für [!DNL Oracle Responsys] finden Sie im [[!DNL Oracle Responsys] Authentifizierungshandbuch](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Experience Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen ID der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Oracle Responsys]-Authentifizierungs-Anmeldedaten als Teil der Anfrageparameter an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Oracle Responsys]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Responsys Base Connection",
      "description": "Base Connection for Oracle Responsys",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
          }
      },
      "connectionSpec": {
          "id": "ff4274f2-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parameter | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer [!DNL Oracle Responsys]-Basisverbindung. Es wird empfohlen, einen beschreibenden Namen anzugeben, da Sie diesen Wert zum Nachschlagen Ihrer Basisverbindung verwenden können. |
| `description` | (Optional) Eine Eigenschaft, die Sie einbeziehen können, um ergänzende Informationen zu Ihrer Basisverbindung bereitzustellen. |
| `auth.specName` | Der Authentifizierungstyp, der für die Verbindung verwendet wird. |
| `auth.params.endpoint` | Die REST-Authentifizierungsendpunkt-URL Ihres [!DNL Oracle Responsys]-Servers. |
| `auth.params.clientId` | Die Client-ID Ihrer [!DNL Oracle Responsys]-Instanz. |
| `auth.params.clientSecret` | Das Client-Geheimnis Ihrer [!DNL Oracle Responsys]-Instanz. |
| `connectionSpec.id` | Der Wert für die Verbindungsspezifikations-ID der [!DNL Oracle Responsys]-Quelle ist wie folgt festgelegt: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

**Antwort**

Bei einer erfolgreichen Antwort werden Details zu der neu erstellten Basisverbindung zurückgegeben, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Oracle Responsys]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um Daten zur Marketing-Automatisierung mithilfe der API  [!DNL Flow Service]  Experience Platform zu übertragen](../../collect/marketing-automation.md)
