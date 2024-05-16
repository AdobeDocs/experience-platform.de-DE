---
title: Erstellen einer Microsoft SQL Server-Basisverbindung mit der Flow Service-API
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit einem Microsoft SQL Server verbinden.
exl-id: 00455a61-c8c1-42f4-a962-fc16f7370cbd
source-git-commit: 1828dd76e9ff317f97e9651331df3e49e44efff5
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 61%

---

# Erstellen Sie eine [!DNL Microsoft] SQL Server-Basisverbindung mit [!DNL Flow Service] API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

In diesem Tutorial erfahren Sie, wie Sie eine Basisverbindung für [!DNL Microsoft SQL Server] mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu [!DNL Microsoft SQL Server] mithilfe der [!DNL Flow Service] API.

### Sammeln erforderlicher Anmeldeinformationen {#gather-required-credentials}

Um eine Verbindung zu [!DNL Microsoft SQL Server]müssen Sie die folgende Verbindungseigenschaft angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| `connectionString` | Die Verbindungszeichenfolge, die Ihrer [!DNL Microsoft SQL Server] -Konto. Ihr Verbindungszeichenfolgen-Muster hängt davon ab, ob Sie den Servernamen oder Instanznamen für Ihre Datenquelle verwenden:<ul><li>Verbindungszeichenfolge mit dem Servernamen: `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Verbindungszeichenfolge mit Instanzname:`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Microsoft SQL Server] is `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

Weitere Informationen zum Abrufen einer Verbindungszeichenfolge finden Sie in diesem [[!DNL Microsoft SQL Server] Dokument](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Microsoft SQL Server]-Authentifizierungsdaten als Teil der Anfrageparameter an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Microsoft SQL Server]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for sql-server",
      "description": "Base connection for sql-server",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword"
          }
      },
      "connectionSpec": {
          "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
          "version": "1.0"
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `auth.params.connectionString` | Die Verbindungszeichenfolge, die Ihrer [!DNL Microsoft SQL Server] -Konto. Lesen Sie den Abschnitt unter [Erfassen erforderlicher Anmeldeinformationen](#gather-required-credentials) für weitere Informationen. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Microsoft SQL Server]-Verbindung lautet: `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Datenbank im nächsten Tutorial zu untersuchen.

```json
{
    "id": "0b8224e4-0de8-4293-8224-e40de80293c6",
    "etag": "\"5802c519-0000-0200-0000-5e4d89520000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Microsoft SQL Server]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen Sie einen Datenfluss, um Datenbankdaten mit der [!DNL Flow Service] API](../../collect/database-nosql.md)