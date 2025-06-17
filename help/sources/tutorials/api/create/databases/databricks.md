---
title: Verbinden von Azure DataBricks mit Experience Platform mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Azure Databricks mithilfe von APIs mit Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
exl-id: c3974bab-8e67-49a1-b1a5-d453cf7bfd1d
source-git-commit: 9df2f9cc70876834aa635d50d548a882f45e3190
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 17%

---

# Verbinden von [!DNL Azure Databricks] mit Experience Platform mithilfe der [!DNL Flow Service]-API

>[!AVAILABILITY]
>
>* Die [!DNL Azure Databricks] ist im Quellkatalog für Benutzende verfügbar, die Real-Time CDP Ultimate erworben haben.
>
>* Die [!DNL Azure Databricks]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../../../home.md#terms-and-conditions) den „Nutzungsbedingungen“ in der Quellenübersicht .

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihr [!DNL Azure Databricks]-Konto mithilfe der [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

### Verwenden von Experience Platform-APIs

Lesen Sie das Handbuch [Erste Schritte mit Experience Platform-APIs](../../../../../landing/api-guide.md) um Informationen über den erfolgreichen Aufruf von Experience Platform-APIs zu erhalten.

### Vorausgesetzte Einrichtung konfigurieren

Lesen Sie die [[!DNL Databricks] Übersicht](../../../../connectors/databases/databricks.md), um mehr über die erforderlichen Konfigurationen zu erfahren, die abgeschlossen sein müssen, bevor Sie Ihr -Konto mit Experience Platform verbinden können.

### Sammeln erforderlicher Anmeldedaten

Geben Sie Werte für die folgenden Anmeldeinformationen an, um [!DNL Databricks] mit Experience Platform zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `domain` | Die URL Ihres [!DNL Databricks]. Beispiel: `https://adb-1234567890123456.7.azuredatabricks.net`. |
| `clusterId` | Die ID Ihres Clusters in [!DNL Databricks]. Dieser Cluster muss bereits ein vorhandener Cluster sein und sollte ein interaktiver Cluster sein. |
| `accessToken` | Das Zugriffstoken, das Ihr [!DNL Databricks]-Konto authentifiziert. Sie können Ihr Zugriffs-Token mit dem [!DNL Databricks] Workspace generieren. |
| `database` | Der Name Ihrer Datenbank im Delta Lake. |
| `connectionSpec.Id` | Die Verbindungsspezifikations-ID gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen im Zusammenhang mit der Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Databricks] ist `e9d7ec6b-0873-4e57-ad21-b3a7c65e310b`. |

Weitere Informationen finden Sie in der [[!DNL Azure Databricks] Übersicht](../../../../connectors/databases/databricks.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Experience Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen ID der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie die entsprechenden Authentifizierungsdaten für Ihr [!DNL Databricks]-Konto an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für eine [!DNL Databricks] mithilfe der Zugriffstoken-Authentifizierung.

+++Beispiel für eine Anfrage anzeigen

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/connections' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d '{
    "name": "Databricks connection to Experience Platform",
    "description": "A Databricks base connection to Experience Platform",
    "auth": {
        "specName": "Access Token Authentication",
        "params": {
          "domain": "https://adb-1234567890123456.7.azuredatabricks.net",
          "clusterId": "xxxx",
          "accessToken": "xxxx",
          "database": "acme-db"
        }
    },
    "connectionSpec": {
        "id": "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b",
        "version": "1.0"
    }
}'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `auth.params.domain` | Die URL Ihres [!DNL Databricks]. |
| `auth.params.clusterId` | Die ID Ihres Clusters in [!DNL Databricks]. Dieser Cluster muss bereits ein vorhandener Cluster sein und sollte ein interaktiver Cluster sein |
| `auth.params.accessToken` | Das Zugriffstoken, das Ihr [!DNL Databricks]-Konto authentifiziert. |
| `auth.params.database` | Der Name Ihrer Datenbank im Delta Lake. |
| `connectionSpec.id` | Die [!DNL Databricks] Verbindungsspezifikations-ID. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt Ihre neu erstellte Verbindung zurück, einschließlich Ihrer Basisverbindungs-ID.

+++Beispiel für eine Antwort anzeigen

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich eine Verbindung zwischen Ihrem [!DNL Databricks]-Konto und Experience Platform hergestellt. Sie können die neu generierte Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um Datenbankdaten mithilfe der API  [!DNL Flow Service]  Experience Platform zu übertragen](../../collect/database-nosql.md)
