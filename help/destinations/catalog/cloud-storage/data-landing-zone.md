---
title: Ziel der Data Landing Zone
description: Erfahren Sie, wie Sie eine Verbindung zur Data Landing Zone herstellen, um Zielgruppen zu aktivieren und Datensätze zu exportieren.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1976'
ht-degree: 28%

---

# Ziel der Data Landing Zone

>[!IMPORTANT]
>
>Diese Dokumentationsseite verweist auf das [!DNL Data Landing Zone] *Ziel*. Es gibt auch eine [!DNL Data Landing Zone] *Quelle* im Quellkatalog. Weitere Informationen finden Sie in der Dokumentation [[!DNL Data Landing Zone] Quelle](/help/sources/connectors/cloud-storage/data-landing-zone.md) .


## Überblick {#overview}

[!DNL Data Landing Zone] ist eine von Adobe Experience Platform bereitgestellte Cloud-Speicherschnittstelle, die Ihnen Zugriff auf eine sichere, Cloud-basierte Dateispeichereinrichtung gewährt, um Dateien aus Experience Platform zu exportieren. Sie haben Zugriff auf einen [!DNL Data Landing Zone]-Container pro Sandbox, und das gesamte Datenvolumen über alle Container hinweg ist auf die Gesamtdaten beschränkt, die mit Ihrer Experience Platform-Produkt- und -Services-Lizenz bereitgestellt werden. Alle Kundinnen und Kunden von Experience Platform und seinen Programmen wie [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] und [!DNL Real-Time Customer Data Platform] erhalten einen [!DNL Data Landing Zone]-Container pro Sandbox.

Experience Platform erzwingt eine strikte sieben Tage lange Lebensdauer („time-to-live“, TTL) für alle Dateien, die in einen [!DNL Data Landing Zone]-Container hochgeladen werden. Alle Dateien werden nach sieben Tagen gelöscht.

Der [!DNL Data Landing Zone]-Ziel-Connector ist für Kundinnen und Kunden verfügbar, die den Azure- oder Amazon Web Service-Cloud-Support verwenden. Der Authentifizierungsmechanismus unterscheidet sich je nach Cloud, in der das Ziel bereitgestellt wird, alle weiteren Informationen zum Ziel und zu dessen Anwendungsfällen sind identisch. Weitere Informationen zu den beiden verschiedenen Authentifizierungsmechanismen finden Sie in den Abschnitten [Authentifizieren bei der in Azure Blob bereitgestellten Data Landing Zone](#authenticate-dlz-azure) und [Authentifizieren bei der von AWS bereitgestellten Data Landing Zone](#authenticate-dlz-aws).

![Diagramm, das zeigt, wie sich die Implementierung des Data Landing Zone-Ziels je nach Cloud-Unterstützung unterscheidet.](/help/destinations/assets/catalog/cloud-storage/data-landing-zone/dlz-workflow-based-on-cloud-implementation.png "Implementierung des Data Landing Zone-Ziels durch Cloud-Support"){zoomable="yes"}

## Herstellen einer Verbindung zu Ihrem [!UICONTROL Data Landing Zone] über API oder Benutzeroberfläche {#connect-api-or-ui}

* Um über die Experience Platform-Benutzeroberfläche eine Verbindung zu Ihrem [!UICONTROL Data Landing Zone]-Speicherort herzustellen, lesen Sie die Abschnitte [Mit dem Ziel verbinden](#connect) und [Zielgruppen für dieses Ziel aktivieren](#activate).
* Um programmgesteuert eine Verbindung zu Ihrem [!UICONTROL Data Landing Zone]-Speicherort herzustellen, lesen Sie das Tutorial [Aktivieren von Zielgruppen für dateibasierte Ziele mithilfe der Flow Service-API](../../api/activate-segments-file-based-destinations.md).

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Sie exportieren alle Teile eines Segments zusammen mit den entsprechenden Schemafeldern (wie etwa Ihre PPID), gemäß der Auswahl im Bildschirm „Profilattribute auswählen“ des [Zielaktivierungs-Workflows](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Datensätze exportieren {#export-datasets}

Dieses Ziel unterstützt Datensatzexporte. Vollständige Informationen zum Einrichten von Datensatzexporten finden Sie in den Tutorials:

* So [ Sie Datensätze mithilfe der Benutzeroberfläche von Experience Platform ](/help/destinations/ui/export-datasets.md).
* So [ Sie Datensätze mithilfe der Flow Service-API programmgesteuert ](/help/destinations/api/export-datasets.md).

## Dateiformat der exportierten Daten {#file-format}

Beim Exportieren *Zielgruppendaten* erstellt Experience Platform eine `.csv`-, `parquet`- oder `.json`-Datei an dem von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie im Abschnitt [Unterstützte Dateiformate für den Export](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) im Tutorial zur Zielgruppenaktivierung.

Beim Exportieren *Datensätze* erstellt Experience Platform eine `.parquet`- oder `.json`-Datei an dem von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie im Abschnitt [Überprüfen eines erfolgreichen Datensatzexports](../../ui/export-datasets.md#verify) im Tutorial zum Exportieren von Datensätzen.

## Authentifizierung bei der in Azure Blob bereitgestellten Data Landing Zone {#authenticate-dlz-azure}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Microsoft Azure ausgeführt werden. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).

Sie können Dateien in Ihrem Container lesen und schreiben, indem Sie [!DNL Azure Storage Explorer] oder die Befehlszeilenschnittstelle verwenden.

[!DNL Data Landing Zone] unterstützt die SAS-basierte Authentifizierung, und die Daten werden im Ruhezustand und bei der Übertragung mit standardmäßigen [!DNL Azure Blob]-Speichersicherheitsmechanismen geschützt. SAS steht für [Shared Access Signature](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/how-to-guides/create-sas-tokens?tabs=Containers).

Um Ihre Daten über eine öffentliche Internetverbindung zu schützen, verwenden Sie die SAS-basierte Authentifizierung, um sicher auf Ihren [!DNL Data Landing Zone]-Container zuzugreifen. Für die Verwendung Ihres [!DNL Data Landing Zone]-Containers sind keine Netzwerkänderungen erforderlich. Sie müssen also keine Zulassungslisten oder regionenübergreifende Setups für Ihr Netzwerk konfigurieren.

### Verbinden des [!DNL Data Landing Zone] Containers mit [!DNL Azure Storage Explorer]

Sie können [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) verwenden, um den Inhalt Ihres [!DNL Data Landing Zone]-Containers zu verwalten. Um [!DNL Data Landing Zone] verwenden zu können, müssen Sie zunächst Ihre Anmeldeinformationen abrufen, sie in [!DNL Azure Storage Explorer] eingeben und Ihren [!DNL Data Landing Zone]-Container mit [!DNL Azure Storage Explorer] verbinden.

Wählen Sie in der Benutzeroberfläche von [!DNL Azure Storage Explorer] in der linken Navigationsleiste das Verbindungssymbol aus. Das Fenster **Ressource auswählen** wird angezeigt, in dem Sie Optionen für das Verbinden finden. Wählen Sie **[!DNL Blob container]** aus, um eine Verbindung zu Ihrem [!DNL Data Landing Zone]-Speicher herzustellen.

![Ressource auswählen, die in der Azure-Benutzeroberfläche hervorgehoben ist.](/help/sources/images/tutorials/create/dlz/select-resource.png)

Wählen Sie als Nächstes **Shared Access Signature URL (SAS)** als Verbindungsmethode und klicken Sie dann auf **Weiter**.

![In der Azure-Benutzeroberfläche hervorgehobene Verbindungsmethode auswählen.](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Nachdem Sie Ihre Verbindungsmethode ausgewählt haben, müssen Sie einen **Anzeigenamen** und die **[!DNL Blob]Container-SAS-URL** angeben, die mit Ihrem [!DNL Data Landing Zone]-Container übereinstimmt.

>[!BEGINSHADEBOX]

### Abrufen der Anmeldeinformationen für Ihre [!DNL Data Landing Zone] {#retrieve-dlz-credentials}

Sie müssen die Experience Platform-APIs verwenden, um Ihre [!DNL Data Landing Zone]-Anmeldedaten abzurufen. Der API-Aufruf zum Abrufen Ihrer Anmeldeinformationen wird unten beschrieben. Informationen zum Abrufen der erforderlichen Werte für Ihre Kopfzeilen finden Sie im Handbuch [Erste Schritte mit Adobe Experience Platform-APIs](/help/landing/api-guide.md).

**API-Format**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| `dlz_destination` | Der `dlz_destination` ermöglicht es der API, einen Landing Zone-Ziel-Container von den anderen Containertypen zu unterscheiden, die Ihnen zur Verfügung stehen. |

{style="table-layout:auto"}

**Anfrage**

Im folgenden Anfragebeispiel werden Anmeldeinformationen für eine vorhandene Landing Zone abgerufen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Antwort**

Die folgende Antwort gibt die Anmeldeinformationen für Ihre Landing Zone zurück, einschließlich Ihrer aktuellen `SASToken` und `SASUri` sowie der `storageAccountName`, die Ihrem Landing Zone-Container entspricht.

```json
{
    "containerName": "dlz-destination",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `containerName` | Der Name Ihrer Landing Zone. |
| `SASToken` | Das Shared Access Signature Token für Ihre Landing Zone. Diese Zeichenfolge enthält alle Informationen, die zum Autorisieren einer Anfrage erforderlich sind. |
| `SASUri` | Der Signatur-URI für den gemeinsamen Zugriff für Ihre Landing Zone. Diese Zeichenfolge ist eine Kombination aus dem URI zur Landing Zone, für die Sie authentifiziert werden, und dem entsprechenden SAS-Token, |

{style="table-layout:auto"}

### Aktualisieren [!DNL Data Landing Zone] Anmeldeinformationen {#update-dlz-credentials}

Sie können Ihre Anmeldedaten bei Bedarf auch aktualisieren. Sie können Ihre `SASToken` aktualisieren, indem Sie eine POST-Anfrage an den `/credentials`-Endpunkt der [!DNL Connectors]-API stellen.

**API-Format**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| `dlz_destination` | Der `dlz_destination` ermöglicht es der API, einen Landing Zone-Ziel-Container von den anderen Containertypen zu unterscheiden, die Ihnen zur Verfügung stehen. |
| `refresh` | Mit der `refresh` Aktion können Sie Ihre Anmeldeinformationen für die Landing Zone zurücksetzen und automatisch eine neue `SASToken` generieren. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage aktualisiert Ihre Anmeldeinformationen für die Landing Zone.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Antwort**

Die folgende Antwort gibt aktualisierte Werte für Ihre `SASToken` und `SASUri` zurück.

```json
{
    "containerName": "dlz-destination",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

Geben Sie Ihren Anzeigenamen (`containerName`) und [!DNL Data Landing Zone] SAS-URL an, wie im oben beschriebenen API-Aufruf zurückgegeben, und klicken Sie dann auf **Weiter**.

![Geben Sie Verbindungsinformationen ein, die in der Azure-Benutzeroberfläche hervorgehoben sind.](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

Das Fenster **Zusammenfassung** wird angezeigt. Es gibt Ihnen einen Überblick über Ihre Einstellungen, einschließlich Informationen zu Ihrem [!DNL Blob]-Endpunkt und Berechtigungen. Wenn Sie bereit sind, klicken Sie auf **Verbinden**.

![Zusammenfassung der in der Azure-Benutzeroberfläche angezeigten Einstellungen.](/help/sources/images/tutorials/create/dlz/summary.png)

Eine erfolgreiche Verbindung aktualisiert Ihre Benutzeroberfläche von [!DNL Azure Storage Explorer] mit Ihrem [!DNL Data Landing Zone]-Container.

![Zusammenfassung des DLZ-Benutzer-Containers, der in der Azure-Benutzeroberfläche hervorgehoben ist.](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Da Ihr [!DNL Data Landing Zone]-Container jetzt mit [!DNL Azure Storage Explorer] verbunden ist, können Sie damit beginnen, Dateien von Experience Platform in Ihren [!DNL Data Landing Zone]-Container zu exportieren. Um Dateien zu exportieren, müssen Sie eine Verbindung zum [!DNL Data Landing Zone]-Ziel in der Experience Platform-Benutzeroberfläche herstellen, wie im folgenden Abschnitt beschrieben.

## Authentifizierung bei der von AWS bereitgestellten Data Landing Zone {#authenticate-dlz-aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).

Führen Sie die folgenden Schritte aus, um Anmeldeinformationen für Ihre auf AWS bereitgestellte [!DNL Data Landing Zone]-Instanz zu erhalten. Verwenden Sie dann einen Client Ihrer Wahl, um eine Verbindung zu Ihrer [!DNL Data Landing Zone]-Instanz herzustellen.

>[!BEGINSHADEBOX]

### Abrufen der Anmeldeinformationen für Ihre [!DNL Data Landing Zone] {#retrieve-dlz-credentials-aws}

Sie müssen die Experience Platform-APIs verwenden, um Ihre [!DNL Data Landing Zone]-Anmeldedaten abzurufen. Der API-Aufruf zum Abrufen Ihrer Anmeldeinformationen wird unten beschrieben. Informationen zum Abrufen der erforderlichen Werte für Ihre Kopfzeilen finden Sie im Handbuch [Erste Schritte mit Adobe Experience Platform-APIs](/help/landing/api-guide.md).

**API-Format**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination'
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| `dlz_destination` | Fügen Sie den `dlz_destination` Abfrageparameter hinzu, um anzugeben, dass [!DNL Data Landing Zone] Container-Anmeldeinformationen vom Typ *Ziel* abgerufen werden sollen. Informationen zum Verbinden und Abrufen von Anmeldeinformationen für eine Data Landing Zone *Quelle* finden Sie in der [Quellendokumentation](/help/sources/connectors/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

**Anfrage**

Im folgenden Anfragebeispiel werden Anmeldeinformationen für eine vorhandene Landing Zone abgerufen.

```shell
curl --request GET \
  --url 'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  --header 'Authorization: Bearer ***' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: your_api_key' \
  --header 'x-gw-ims-org-id: yourorg@AdobeOrg'
```

**Antwort**

Die folgende Antwort gibt die Anmeldeinformationen für Ihre Landing Zone zurück, einschließlich Ihrer aktuellen `awsAccessKeyId`, `awsSecretAccessKey` und anderer Informationen.

```json
{
    "credentials": {
        "awsAccessKeyId": "ABCDW3MEC6HE2T73ZVKP",
        "awsSecretAccessKey": "A1B2Zdxj6y4xfR0QZGtf/phj/hNMAbOGtzM/JNeE",
        "awsSessionToken": "***"
    },
    "dlzPath": {
        "bucketName": "your-bucket-name",
        "dlzFolder": "dlz-destination"
    },
    "dlzProvider": "Amazon S3",
    "expiryTime": 1734494017
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `credentials` | Dieses Objekt enthält die `awsAccessKeyId`, `awsSecretAccessKey` und `awsSessionToken`, die Experience Platform zum Exportieren von Dateien an den von Ihnen bereitgestellten Data Landing Zone-Speicherort verwendet. |
| `dlzPath` | Dieses Objekt enthält den Pfad im von Adobe bereitgestellten AWS-Speicherort, an dem exportierte Dateien abgelegt werden. |
| `dlzProvider` | Gibt an, dass dies eine von Amazon S3 bereitgestellte Data Landing Zone ist. |
| `expiryTime` | Gibt an, wann die Anmeldeinformationen im `credentials` ablaufen. Um die Anmeldeinformationen zu aktualisieren, führen Sie die Anfrage erneut aus. |

{style="table-layout:auto"}

>[!ENDSHADEBOX]

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=de) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Stellen Sie sicher, dass Sie Ihren [!DNL Data Landing Zone]-Container mit [!DNL Azure Storage Explorer] verbunden haben, wie im Abschnitt [Voraussetzungen](#prerequisites) beschrieben. Da [!DNL Data Landing Zone] ein von Adobe bereitgestellter Speicher ist, müssen Sie keine weiteren Schritte in der Experience Platform-Benutzeroberfläche ausführen, um sich beim Ziel zu authentifizieren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Encryption key]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der folgenden Abbildung.
  ![Abbildung mit einem Beispiel für einen korrekt formatierten PGP-Schlüssel in der Benutzeroberfläche.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)
* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Description]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Folder path]**: Geben Sie den Pfad zum Zielordner ein, in dem die exportierten Dateien gespeichert werden.
* **[!UICONTROL File type]**: Wählen Sie das Format aus, das Experience Platform für die exportierten Dateien verwenden soll. Bei Auswahl der Option [!UICONTROL CSV] können Sie auch [die Dateiformatierungsoptionen konfigurieren](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Wählen Sie den Komprimierungstyp aus, den Experience Platform für die exportierten Dateien verwenden soll.
* **[!UICONTROL Include manifest file]**: Schalten Sie diese Option ein, wenn die Exporte eine JSON-Manifestdatei enthalten sollen, die Informationen zum Exportspeicherort, zur Exportgröße und mehr enthält. Das Manifest wird mit dem Format `manifest-<<destinationId>>-<<dataflowRunId>>.json` benannt. Anzeigen einer [Beispielmanifestdatei](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Die Manifestdatei enthält die folgenden Felder:
   * `flowRunId`: Die [Datenflussausführung](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) die die exportierte Datei generiert hat.
   * `scheduledTime`: Die Zeit in UTC, zu der die Datei exportiert wurde.
   * `exportResults.sinkPath`: Der Pfad an Ihrem Speicherort, an dem die exportierte Datei abgelegt wird.
   * `exportResults.name`: Der Name der exportierten Datei.
   * `size`: Die Größe der exportierten Datei in Byte.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen [ Aktivieren von Zielgruppen für dieses Ziel finden Sie ](../../ui/activate-batch-profile-destinations.md)Aktivieren von Zielgruppendaten für Batch-Profil-).

### Planung

Im **[!UICONTROL Scheduling]** Schritt können Sie [Exportplan einrichten](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) für Ihr [!DNL Data Landing Zone]-Ziel festlegen und [den Namen Ihrer exportierten Dateien konfigurieren](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Zuordnen von Attributen und Identitäten {#map}

Im **[!UICONTROL Mapping]** Schritt können Sie auswählen, welche Attribut- und Identitätsfelder für Ihre Profile exportiert werden sollen. Sie können auch festlegen, dass die Kopfzeilen in der exportierten Datei in einen beliebigen Anzeigenamen geändert werden. Weitere Informationen finden Sie im [Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) im Tutorial zur Benutzeroberfläche der Aktivierung von Batch-Zielen.

## Überprüfen auf einen erfolgreichen Datenexport {#exported-data}

Überprüfen Sie, ob die Daten erfolgreich exportiert wurden, indem Sie Ihren [!DNL Data Landing Zone]-Speicher überprüfen, und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.
