---
title: Databricks
description: Erfahren Sie mehr über die erforderlichen Schritte zum Verbinden von Databricks mit Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
last-substantial-update: 2025-06-17T00:00:00Z
exl-id: 2f082898-aa0e-47a1-a4bf-077c21afdfee
source-git-commit: 96e395e3b3d977d7eb04c400f6fd290977bf1101
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 3%

---

# [!DNL Databricks]

>[!AVAILABILITY]
>
>* Die [!DNL Databricks] ist im Quellkatalog für Benutzende verfügbar, die Real-Time CDP Ultimate erworben haben.
>
>* Die [!DNL Databricks]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../home.md#terms-and-conditions) den „Nutzungsbedingungen“ in der Quellenübersicht .

[!DNL Databricks] ist eine Cloud-basierte Plattform für Datenanalyse, maschinelles Lernen und KI. Sie können [!DNL Databricks] verwenden, um eine ganzheitliche Umgebung für das Erstellen, Bereitstellen und Verwalten von Datenlösungen im benötigten Umfang zu integrieren und bereitzustellen.

Verwenden Sie die [!DNL Databricks], um Ihr Konto zu verbinden und Ihre [!DNL Databricks] Daten in Adobe Experience Platform aufzunehmen.

## Voraussetzungen

Führen Sie die erforderlichen Schritte aus, um Ihr [!DNL Databricks]-Konto erfolgreich mit Experience Platform zu verbinden.

### Abrufen Ihrer Container-Anmeldeinformationen

Rufen Sie Ihre Experience Platform [!DNL Azure Blob Storage]-Anmeldeinformationen ab, damit Ihr [!DNL Databricks]-Konto später darauf zugreifen kann.

Um Ihre Anmeldeinformationen abzurufen, stellen Sie eine GET-Anfrage an den `/credentials`-Endpunkt der [!DNL Connectors]-API.

**API-Format**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source
```

**Anfrage**

Mit der folgenden Anfrage werden die Anmeldeinformationen für Ihr Experience Platform-[!DNL Azure Blob Storage] abgerufen.

+++Beispiel für eine Anfrage anzeigen

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Anmeldeinformationen (`containerName`, `SASToken`, `storageAccountName`) zur späteren Verwendung in [!DNL Apache Spark] Konfiguration für [!DNL Databricks] bereitgestellt.

+++Beispiel für eine Anfrageantwort

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "expiryDate": "2025-07-05"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `containerName` | Der Name Ihres [!DNL Azure Blob Storage]. Sie verwenden diesen Wert später, wenn Sie die [!DNL Apache Spark] für [!DNL Databricks] fertig stellen. |
| `SASToken` | Das Shared Access Signature Token für Ihre [!DNL Azure Blob Storage]. Diese Zeichenfolge enthält alle Informationen, die zum Autorisieren einer Anfrage erforderlich sind. |
| `storageAccountName` | Der Name Ihres Speicherkontos. |
| `SASUri` | Der Shared Access Signature-URI für Ihre [!DNL Azure Blob Storage]. Diese Zeichenfolge ist eine Kombination aus dem URI zum [!DNL Azure Blob Storage], für den Sie authentifiziert werden, und dem entsprechenden SAS-Token. |
| `expiryDate` | Das Datum, an dem Ihr SAS-Token abläuft. Sie müssen Ihr Token vor dem Ablaufdatum aktualisieren, um es weiterhin in Ihrer Anwendung zum Hochladen von Daten in die [!DNL Azure Blob Storage] verwenden zu können. Wenn Sie Ihr Token nicht vor dem angegebenen Ablaufdatum manuell aktualisieren, wird es automatisch aktualisiert und ein neues Token bereitgestellt, wenn der Aufruf der GET-Anmeldeinformationen ausgeführt wird. |

+++

### Aktualisieren von Anmeldeinformationen

>[!NOTE]
>
>Ihre bestehenden Anmeldedaten werden widerrufen, sobald Sie Ihre Anmeldedaten aktualisieren. Daher müssen Sie Ihre [!DNL Spark]-Konfigurationen bei jeder Aktualisierung Ihrer -Speicheranmeldeinformationen entsprechend aktualisieren. Andernfalls schlägt Ihr Datenfluss fehl.

Um Ihre Anmeldeinformationen zu aktualisieren, stellen Sie eine POST-Anfrage und nehmen Sie `action=refresh` als Abfrageparameter auf.

**API-Format**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh
```

**Anfrage**

Die folgende Anfrage aktualisiert die Anmeldeinformationen für Ihr [!DNL Azure Blob Storage].

+++Beispiel für eine Anfrage anzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt Ihre neuen Anmeldeinformationen zurück.

+++Beispiel für eine Anfrageantwort

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "expiryDate": "2025-07-20"
}
```

+++

### Konfigurieren des Zugriffs auf Ihre [!DNL Azure Blob Storage]

>[!IMPORTANT]
>
>* Wenn Ihr Cluster beendet wurde, startet der Service ihn während einer Flussausführung automatisch neu. Sie müssen jedoch sicherstellen, dass Ihr Cluster beim Erstellen einer Verbindung oder eines Datenflusses aktiv ist. Darüber hinaus muss Ihr Cluster aktiv sein, wenn Sie Aktionen wie Datenvorschau oder Exploration durchführen, da diese Aktionen nicht zum automatischen Neustart eines beendeten Clusters führen können.
>
>* Ihr [!DNL Azure]-Container enthält einen Ordner mit dem Namen `adobe-managed-staging`. Um die nahtlose Aufnahme von Daten zu gewährleisten **(nicht** ändern Sie diesen Ordner.


Als Nächstes müssen Sie sicherstellen, dass Ihr [!DNL Databricks]-Cluster Zugriff auf das Experience Platform-[!DNL Azure Blob Storage] hat. Dabei können Sie [!DNL Azure Blob Storage] als Zwischenspeicherort zum Schreiben [!DNL delta lake] Tabellendaten verwenden.

Um Zugriff zu gewähren, müssen Sie im Rahmen Ihrer [!DNL Databricks]-Konfiguration ein SAS-Token auf dem [!DNL Apache Spark]-Cluster konfigurieren.

Wählen Sie in Ihrer [!DNL Databricks] die Option **[!DNL Advanced options]** aus und geben Sie dann Folgendes in das [!DNL Spark config] Eingabefeld ein.

```shell
fs.azure.sas.{CONTAINER_NAME}.{STORAGE-ACCOUNT}.blob.core.windows.net {SAS-TOKEN}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| Container-Name | Der Name Ihres Containers. Sie können diesen Wert abrufen, indem Sie Ihre [!DNL Azure Blob Storage] Anmeldeinformationen abrufen. |
| Speicherkonto | Der Name Ihres Speicherkontos. Sie können diesen Wert abrufen, indem Sie Ihre [!DNL Azure Blob Storage] Anmeldeinformationen abrufen. |
| SAS-Token | Das Shared Access Signature Token für Ihre [!DNL Azure Blob Storage]. Sie können diesen Wert abrufen, indem Sie Ihre [!DNL Azure Blob Storage] Anmeldeinformationen abrufen. |

![Die Databricks-Benutzeroberfläche auf Azure.](../../images/tutorials/create/databricks/databricks-ui.png)

Wenn keine Informationen bereitgestellt werden, schlägt die Kopieraktivität im Flusslauf fehl und gibt den folgenden Fehler zurück:

```shell
Unable to access container '{CONTAINER_NAME}' in account '{STORAGE_ACCOUNT}.blob.core.windows.net' using anonymous credentials. No credentials found in the configuration. Public access is not permitted on this storage account.
```

## Verbinden von [!DNL Databricks] mit Experience Platform

Nachdem Sie die erforderlichen Schritte ausgeführt haben, können Sie nun fortfahren und Ihr [!DNL Databricks]-Konto mit Experience Platform verbinden:

* [Verbinden über die API](../../tutorials/api/create/databases/databricks.md)
* [Herstellen einer Verbindung über den Arbeitsbereich Quellen in der Benutzeroberfläche](../../tutorials/ui/create/databases/databricks.md)
