---
title: Ziel der Data Landing Zone
description: Erfahren Sie, wie Sie eine Verbindung zur Data Landing Zone herstellen, um Zielgruppen zu aktivieren und Datensätze zu exportieren.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: ce78e320e78a67cd744fdf1c49b34f6fcddf4f15
workflow-type: tm+mt
source-wordcount: '1592'
ht-degree: 44%

---

# Ziel der Data Landing Zone

>[!IMPORTANT]
>
>Diese Dokumentationsseite bezieht sich auf das [!DNL Data Landing Zone] *Ziel*. Es gibt auch eine [!DNL Data Landing Zone] *Quelle* im Quellkatalog. Weitere Informationen finden Sie in der Dokumentation zur [[!DNL Data Landing Zone] Quelle](/help/sources/connectors/cloud-storage/data-landing-zone.md) .


## Übersicht {#overview}

[!DNL Data Landing Zone] ist eine von Adobe Experience Platform bereitgestellte [!DNL Azure Blob]-Speicherschnittstelle, die Ihnen Zugriff auf eine sichere, Cloud-basierte Dateispeichereinrichtung gewährt, um Dateien aus Platform zu exportieren. Sie haben Zugriff auf einen [!DNL Data Landing Zone]-Container pro Sandbox, und das gesamte Datenvolumen über alle Container hinweg ist auf die Gesamtdaten beschränkt, die mit Ihrer Produkt- und Services-Lizenz von Platform bereitgestellt werden. Alle Kunden von Platform und deren Anwendungen wie [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] und [!DNL Real-Time Customer Data Platform] erhalten einen [!DNL Data Landing Zone] -Container pro Sandbox. Sie können Dateien in Ihrem Container lesen und schreiben, indem Sie [!DNL Azure Storage Explorer] oder die Befehlszeilenschnittstelle verwenden.

[!DNL Data Landing Zone] unterstützt die SAS-basierte Authentifizierung, und die Daten werden im Ruhezustand und bei der Übertragung mit standardmäßigen [!DNL Azure Blob]-Speichersicherheitsmechanismen geschützt. SAS steht für [gemeinsame Zugriffssignatur](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/how-to-guides/create-sas-tokens?tabs=Containers).

Mit der SAS-basierten Authentifizierung können Sie sicher über eine öffentliche Internetverbindung auf Ihren [!DNL Data Landing Zone]-Container zugreifen. Für die Verwendung Ihres [!DNL Data Landing Zone]-Containers sind keine Netzwerkänderungen erforderlich. Sie müssen also keine Zulassungslisten oder regionenübergreifende Setups für Ihr Netzwerk konfigurieren.

Platform erzwingt eine strikte sieben Tage lange Lebensdauer („time-to-live“, TTL) für alle Dateien, die in einen [!DNL Data Landing Zone]-Container hochgeladen werden. Alle Dateien werden nach sieben Tagen gelöscht.

## Verbindung zu Ihrem [!UICONTROL Data Landing Zone]-Speicher über API oder Benutzeroberfläche herstellen {#connect-api-or-ui}

* Um über die Platform-Benutzeroberfläche eine Verbindung zu Ihrem Speicherort für die [!UICONTROL Dateneinstiegszone] herzustellen, lesen Sie die Abschnitte [Verbindung zum Ziel herstellen](#connect) und [Zielgruppen für dieses Ziel aktivieren](#activate) weiter unten.
* Um eine programmgesteuerte Verbindung zum Speicherort für [!UICONTROL Daten-Landing-Zone] herzustellen, lesen Sie das Tutorial [Aktivieren von Zielgruppen für dateibasierte Ziele mithilfe der Flow Service-API.](../../api/activate-segments-file-based-destinations.md)

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die durch den Experience Platform [Segmentierungsdienst](../../../segmentation/home.md) generiert wurden. |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Teile eines Segments zusammen mit den entsprechenden Schemafeldern (wie etwa Ihre PPID), gemäß der Auswahl im Bildschirm „Profilattribute auswählen“ des [Zielaktivierungs-Workflows](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Datensätze exportieren {#export-datasets}

Dieses Ziel unterstützt Datensatzexporte. Vollständige Informationen zum Einrichten von Datensatzexporten finden Sie in den Tutorials:

* Exportieren von Datensätzen mithilfe der Platform-Benutzeroberfläche](/help/destinations/ui/export-datasets.md).[
* So exportieren [Datensätze programmgesteuert mit der Flow Service-API](/help/destinations/api/export-datasets.md).

## Dateiformat der exportierten Daten {#file-format}

Beim Exportieren von *Zielgruppendaten* erstellt Platform eine `.csv`-, `parquet`- oder `.json`-Datei am von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie im Abschnitt [Unterstützte Dateiformate für den Export](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) im Tutorial zur Aktivierung der Zielgruppe.

Beim Exportieren von *Datensätzen* erstellt Platform eine `.parquet` - oder `.json` -Datei am von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie im Abschnitt [Überprüfen des erfolgreichen Datensatzexports](../../ui/export-datasets.md#verify) im Tutorial zum Exportieren von Datensätzen.

## Voraussetzungen {#prerequisites}

Beachten Sie die folgenden Voraussetzungen, die erfüllt sein müssen, bevor Sie das Ziel [!DNL Data Landing Zone] verwenden können.

### Verbinden Sie Ihren [!DNL Data Landing Zone]-Container mit [!DNL Azure Storage Explorer]

Sie können [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) verwenden, um den Inhalt Ihres [!DNL Data Landing Zone] Containers zu verwalten. Um mit der Verwendung von [!DNL Data Landing Zone] zu beginnen, müssen Sie zunächst Ihre Anmeldeinformationen abrufen, sie in [!DNL Azure Storage Explorer] eingeben und Ihren [!DNL Data Landing Zone]-Container mit [!DNL Azure Storage Explorer] verbinden.

Wählen Sie in der Benutzeroberfläche von [!DNL Azure Storage Explorer] in der linken Navigationsleiste das Verbindungssymbol aus. Das Fenster **Ressource auswählen** wird angezeigt, in dem Sie Optionen für das Verbinden finden. Wählen Sie **[!DNL Blob container]** aus, um eine Verbindung zu Ihrem [!DNL Data Landing Zone]-Speicher herzustellen.

![Wählen Sie eine Ressource aus, die in der Azure-Benutzeroberfläche hervorgehoben ist.](/help/sources/images/tutorials/create/dlz/select-resource.png)

Wählen Sie als Nächstes **Shared Access Signature URL (SAS)** als Verbindungsmethode und klicken Sie dann auf **Weiter**.

![Wählen Sie die Verbindungsmethode aus, die in der Azure-Benutzeroberfläche hervorgehoben ist.](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Nachdem Sie Ihre Verbindungsmethode ausgewählt haben, müssen Sie einen **Anzeigenamen** und die **[!DNL Blob]Container-SAS-URL** angeben, die mit Ihrem [!DNL Data Landing Zone]-Container übereinstimmt.

>[!BEGINSHADEBOX]

### Rufen Sie die Anmeldeinformationen für Ihren [!DNL Data Landing Zone] ab {#retrieve-dlz-credentials}

Sie müssen die Platform-APIs verwenden, um Ihre [!DNL Data Landing Zone] -Anmeldedaten abzurufen. Der API-Aufruf zum Abrufen Ihrer Anmeldedaten wird unten beschrieben. Informationen zum Abrufen der erforderlichen Werte für Ihre Kopfzeilen finden Sie im Handbuch [Erste Schritte mit Adobe Experience Platform-APIs](/help/landing/api-guide.md) .

**API-Format**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| `dlz_destination` | Der `dlz_destination` -Typ ermöglicht es der API, einen Zielbehälter für die Einstiegszone von den anderen Behältertypen zu unterscheiden, die Ihnen zur Verfügung stehen. |

{style="table-layout:auto"}

**Anfrage**

Im folgenden Anfragebeispiel werden Anmeldeinformationen für eine vorhandene Landingzone abgerufen.

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

Die folgende Antwort gibt die Anmeldeinformationen für Ihre Einstiegszone zurück, einschließlich Ihrer aktuellen `SASToken` und `SASUri` sowie der `storageAccountName`, die Ihrem Einstiegszonen-Container entsprechen.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `containerName` | Der Name Ihrer Landingzone. |
| `SASToken` | Das Token für die gemeinsame Zugriffssignatur für Ihre Landingzone. Diese Zeichenfolge enthält alle Informationen, die zum Autorisieren einer Anfrage erforderlich sind. |
| `SASUri` | Der URI der Freigegebenen Zugriffssignatur für Ihre Landingzone. Diese Zeichenfolge ist eine Kombination aus dem URI für die Landingzone, für die Sie authentifiziert werden, und dem zugehörigen SAS-Token. |

{style="table-layout:auto"}

### [!DNL Data Landing Zone] Anmeldedaten aktualisieren {#update-dlz-credentials}

Sie können Ihre Anmeldedaten bei Bedarf auch aktualisieren. Sie können Ihre `SASToken` aktualisieren, indem Sie eine POST-Anfrage an den `/credentials` -Endpunkt der [!DNL Connectors] -API richten.

**API-Format**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| `dlz_destination` | Der `dlz_destination` -Typ ermöglicht es der API, einen Zielbehälter für die Einstiegszone von den anderen Behältertypen zu unterscheiden, die Ihnen zur Verfügung stehen. |
| `refresh` | Mit der Aktion `refresh` können Sie Ihre Landingzone-Anmeldedaten zurücksetzen und automatisch eine neue `SASToken` generieren. |

{style="table-layout:auto"}

**Anfrage**

Mit der folgenden Anfrage werden Ihre Landingzone-Anmeldedaten aktualisiert.

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
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

Geben Sie Ihren Anzeigenamen (`containerName`) und die [!DNL Data Landing Zone] SAS-URL ein, wie im oben beschriebenen API-Aufruf zurückgegeben, und wählen Sie dann **Weiter** aus.

![Geben Sie Verbindungsinformationen ein, die in der Azure-Benutzeroberfläche hervorgehoben sind.](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

Das Fenster **Zusammenfassung** wird angezeigt. Es gibt Ihnen einen Überblick über Ihre Einstellungen, einschließlich Informationen zu Ihrem [!DNL Blob]-Endpunkt und Berechtigungen. Wenn Sie bereit sind, klicken Sie auf **Verbinden**.

![Zusammenfassung der Einstellungen, die in der Azure-Benutzeroberfläche angezeigt werden.](/help/sources/images/tutorials/create/dlz/summary.png)

Eine erfolgreiche Verbindung aktualisiert Ihre Benutzeroberfläche von [!DNL Azure Storage Explorer] mit Ihrem [!DNL Data Landing Zone]-Container.

![Zusammenfassung des DLZ-Benutzercontainers, der in der Azure-Benutzeroberfläche hervorgehoben ist.](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Da Ihr [!DNL Data Landing Zone]-Container jetzt mit [!DNL Azure Storage Explorer] verbunden ist, können Sie damit beginnen, Dateien von Experience Platform in Ihren [!DNL Data Landing Zone]-Container zu exportieren. Um Dateien zu exportieren, müssen Sie in der Experience Platform-Benutzeroberfläche eine Verbindung zum Ziel [!DNL Data Landing Zone] herstellen, wie im folgenden Abschnitt beschrieben.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=de) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Stellen Sie sicher, dass Sie Ihren [!DNL Data Landing Zone]-Container mit [!DNL Azure Storage Explorer] verbunden haben, wie im Abschnitt [Voraussetzungen](#prerequisites) beschrieben. Da [!DNL Data Landing Zone] ein von Adobe bereitgestellter Speicher ist, müssen Sie keine weiteren Schritte in der Experience Platform-Benutzeroberfläche ausführen, um sich beim Ziel zu authentifizieren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, in dem die exportierten Dateien gespeichert werden.
* **[!UICONTROL Dateityp]**: Wählen Sie das Format, das Experience Platform für die exportierten Dateien verwenden soll. Wenn Sie die Option [!UICONTROL CSV] auswählen, können Sie auch [die Dateiformatierungsoptionen konfigurieren](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Komprimierungsformat]**: Wählen Sie den Komprimierungstyp aus, den Experience Platform für die exportierten Dateien verwenden soll.
* **[!UICONTROL Manifestdatei einschließen]**: Schalten Sie diese Option ein, wenn Sie möchten, dass die Exporte eine Manifest-JSON-Datei mit Informationen zum Exportspeicherort, zur Exportgröße und mehr enthalten. Das Manifest wird mit dem Format `manifest-<<destinationId>>-<<dataflowRunId>>.json` benannt. Anzeigen einer [Beispielmanifestdatei](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Die Manifestdatei enthält die folgenden Felder:
   * `flowRunId`: Der [Datenfluss-Lauf](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) , der die exportierte Datei generiert hat.
   * `scheduledTime`: Die Uhrzeit in UTC, zu der die Datei exportiert wurde.
   * `exportResults.sinkPath`: Der Pfad in Ihrem Speicherort, an dem die exportierte Datei abgelegt wird.
   * 0: Der Name der exportierten Datei.`exportResults.name`
   * `size`: Die Größe der exportierten Datei in Byte.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profilexportziele](../../ui/activate-batch-profile-destinations.md) .

### Planung

Im Schritt **[!UICONTROL Planung]** können Sie für Ihr [!DNL Data Landing Zone]-Ziel den [Exportplan einrichten](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling), und Sie können dort auch [den Namen Ihrer exportierten Dateien konfigurieren](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Zuordnen von Attributen und Identitäten {#map}

Im Schritt **[!UICONTROL Zuordnung]** können Sie festlegen, welche Attribute und Identitätsfelder für Ihre Profile exportiert werden sollen. Sie können auch festlegen, dass die Kopfzeilen in der exportierten Datei in einen beliebigen Anzeigenamen geändert werden. Weitere Informationen finden Sie im [Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) im Tutorial zur Benutzeroberfläche der Aktivierung von Batch-Zielen.

## Überprüfen auf einen erfolgreichen Datenexport {#exported-data}

Überprüfen Sie, ob die Daten erfolgreich exportiert wurden, indem Sie Ihren [!DNL Data Landing Zone]-Speicher überprüfen, und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.
