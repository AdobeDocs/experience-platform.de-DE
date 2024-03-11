---
title: Ziel der Data Landing Zone
description: Erfahren Sie, wie Sie eine Verbindung zur Data Landing Zone herstellen, um Zielgruppen zu aktivieren und Datensätze zu exportieren.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 8771aa0df001e8ef81d4ad712f4d1f9661b405b2
workflow-type: tm+mt
source-wordcount: '1586'
ht-degree: 45%

---

# Ziel der Data Landing Zone

>[!IMPORTANT]
>
>Diese Dokumentationsseite bezieht sich auf die [!DNL Data Landing Zone] *Ziel*. Es gibt auch eine [!DNL Data Landing Zone] *source* im Quellkatalog. Weitere Informationen finden Sie im Abschnitt [[!DNL Data Landing Zone] source](/help/sources/connectors/cloud-storage/data-landing-zone.md) Dokumentation.


## Übersicht {#overview}

[!DNL Data Landing Zone] ist eine von Adobe Experience Platform bereitgestellte [!DNL Azure Blob]-Speicherschnittstelle, die Ihnen Zugriff auf eine sichere, Cloud-basierte Dateispeichereinrichtung gewährt, um Dateien aus Platform zu exportieren. Sie haben Zugriff auf einen [!DNL Data Landing Zone]-Container pro Sandbox, und das gesamte Datenvolumen über alle Container hinweg ist auf die Gesamtdaten beschränkt, die mit Ihrer Produkt- und Services-Lizenz von Platform bereitgestellt werden. Alle Kundinnen und Kunden von Platform sowie die zugehörigen Anwendungs-Services wie [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] und [!DNL Real-Time Customer Data Platform] erhalten einen [!DNL Data Landing Zone]-Container pro Sandbox. Sie können Dateien in Ihrem Container lesen und schreiben, indem Sie [!DNL Azure Storage Explorer] oder die Befehlszeilenschnittstelle verwenden.

[!DNL Data Landing Zone] unterstützt die SAS-basierte Authentifizierung, und die Daten werden im Ruhezustand und bei der Übertragung mit standardmäßigen [!DNL Azure Blob]-Speichersicherheitsmechanismen geschützt. Mit der SAS-basierten Authentifizierung können Sie sicher über eine öffentliche Internetverbindung auf Ihren [!DNL Data Landing Zone]-Container zugreifen. Für die Verwendung Ihres [!DNL Data Landing Zone]-Containers sind keine Netzwerkänderungen erforderlich. Sie müssen also keine Zulassungslisten oder regionenübergreifende Setups für Ihr Netzwerk konfigurieren.

Platform erzwingt eine strikte sieben Tage lange Lebensdauer („time-to-live“, TTL) für alle Dateien, die in einen [!DNL Data Landing Zone]-Container hochgeladen werden. Alle Dateien werden nach sieben Tagen gelöscht.

## Verbinden Sie Ihre [!UICONTROL Data Landing Zone] Speicher über API oder Benutzeroberfläche {#connect-api-or-ui}

* So stellen Sie eine Verbindung zu Ihrer [!UICONTROL Data Landing Zone] Speicherort mithilfe der Platform-Benutzeroberfläche, lesen Sie die Abschnitte . [Mit Ziel verbinden](#connect) und [Aktivieren von Zielgruppen für dieses Ziel](#activate) unten.
* So stellen Sie eine Verbindung zu Ihrer [!UICONTROL Data Landing Zone] Speicherort programmgesteuert, lesen Sie die [Aktivieren von Zielgruppen für dateibasierte Ziele mithilfe des Tutorials zur Flow Service-API](../../api/activate-segments-file-based-destinations.md).

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Über die Experience Platform generierte Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Teile eines Segments zusammen mit den entsprechenden Schemafeldern (wie etwa Ihre PPID), gemäß der Auswahl im Bildschirm „Profilattribute auswählen“ des [Zielaktivierungs-Workflows](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Exportieren von Datensätzen {#export-datasets}

Dieses Ziel unterstützt Datensatzexporte. Vollständige Informationen zum Einrichten von Datensatzexporten finden Sie in den Tutorials:

* Anleitung [Datensätze mithilfe der Benutzeroberfläche von Platform exportieren](/help/destinations/ui/export-datasets.md).
* Anleitung [Datensätze programmgesteuert mit der Flow Service-API exportieren](/help/destinations/api/export-datasets.md).

## Dateiformat der exportierten Daten {#file-format}

Beim Exportieren *Zielgruppendaten*, erstellt Platform eine `.csv`, `parquet`oder `.json` -Datei an dem Speicherort gespeichert, den Sie bereitgestellt haben. Weitere Informationen zu den Dateien finden Sie unter [unterstützte Dateiformate für den Export](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) im Tutorial zur Aktivierung der Zielgruppe.

Beim Exportieren *Datensätze*, erstellt Platform eine `.parquet` oder `.json` -Datei an dem Speicherort gespeichert, den Sie bereitgestellt haben. Weitere Informationen zu den Dateien finden Sie unter [Überprüfen des erfolgreichen Datensatzexports](../../ui/export-datasets.md#verify) im Tutorial zum Exportieren von Datensätzen .

## Voraussetzungen {#prerequisites}

Beachten Sie die folgenden Voraussetzungen, die erfüllt sein müssen, bevor Sie die [!DNL Data Landing Zone] Ziel.

### Verbinden Sie [!DNL Data Landing Zone] Container zu [!DNL Azure Storage Explorer]

Sie können [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) die Inhalte Ihrer [!DNL Data Landing Zone] Container. Zu Beginn der Verwendung von [!DNL Data Landing Zone], müssen Sie zunächst Ihre Anmeldedaten abrufen und sie in [!DNL Azure Storage Explorer]und verbinden Sie Ihre [!DNL Data Landing Zone] Container zu [!DNL Azure Storage Explorer].

Wählen Sie in der Benutzeroberfläche von [!DNL Azure Storage Explorer] in der linken Navigationsleiste das Verbindungssymbol aus. Das Fenster **Ressource auswählen** wird angezeigt, in dem Sie Optionen für das Verbinden finden. Wählen Sie **[!DNL Blob container]** aus, um eine Verbindung zu Ihrem [!DNL Data Landing Zone]-Speicher herzustellen.

![Wählen Sie eine Ressource aus, die in der Azure-Benutzeroberfläche hervorgehoben ist.](/help/sources/images/tutorials/create/dlz/select-resource.png)

Wählen Sie als Nächstes **Shared Access Signature URL (SAS)** als Verbindungsmethode und klicken Sie dann auf **Weiter**.

![Wählen Sie die Verbindungsmethode aus, die in der Azure-Benutzeroberfläche hervorgehoben ist.](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Nachdem Sie Ihre Verbindungsmethode ausgewählt haben, müssen Sie einen **Anzeigenamen** und die **[!DNL Blob]Container-SAS-URL** angeben, die mit Ihrem [!DNL Data Landing Zone]-Container übereinstimmt.

>[!BEGINSHADEBOX]

### Rufen Sie die Anmeldeinformationen für Ihre [!DNL Data Landing Zone] {#retrieve-dlz-credentials}

Sie müssen die Platform-APIs zum Abrufen Ihrer [!DNL Data Landing Zone] Anmeldedaten. Der API-Aufruf zum Abrufen Ihrer Anmeldedaten wird unten beschrieben. Informationen zum Abrufen der erforderlichen Werte für Ihre Kopfzeilen finden Sie im Abschnitt [Erste Schritte mit Adobe Experience Platform-APIs](/help/landing/api-guide.md) Handbuch.

**API-Format**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| `dlz_destination` | Die `dlz_destination` Mit type kann die API einen Zielcontainer für die Einstiegszone von den anderen Behältertypen unterscheiden, die Ihnen zur Verfügung stehen. |

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

Die folgende Antwort gibt die Anmeldeinformationen für Ihre Landingzone zurück, einschließlich Ihrer aktuellen `SASToken` und `SASUri`und die `storageAccountName` , der Ihrem Landingzone-Container entspricht.

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

### Aktualisieren [!DNL Data Landing Zone] Anmeldeinformationen {#update-dlz-credentials}

Sie können Ihre Anmeldedaten bei Bedarf auch aktualisieren. Sie können Ihre `SASToken` , indem Sie eine POST an die `/credentials` Endpunkt der [!DNL Connectors] API.

**API-Format**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| `dlz_destination` | Die `dlz_destination` Mit type kann die API einen Zielcontainer für die Einstiegszone von den anderen Behältertypen unterscheiden, die Ihnen zur Verfügung stehen. |
| `refresh` | Die `refresh` Mit dieser Aktion können Sie Ihre Landingzone-Anmeldedaten zurücksetzen und automatisch eine neue `SASToken`. |

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

Die folgende Antwort gibt aktualisierte Werte für Ihre `SASToken` und `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

Geben Sie Ihren Anzeigenamen (`containerName`) und [!DNL Data Landing Zone] SAS-URL, wie im oben beschriebenen API-Aufruf zurückgegeben, und wählen Sie dann **Nächste**.

![Geben Sie Verbindungsinformationen ein, die in der Azure-Benutzeroberfläche hervorgehoben sind.](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

Das Fenster **Zusammenfassung** wird angezeigt. Es gibt Ihnen einen Überblick über Ihre Einstellungen, einschließlich Informationen zu Ihrem [!DNL Blob]-Endpunkt und Berechtigungen. Wenn Sie bereit sind, klicken Sie auf **Verbinden**.

![Zusammenfassung der in der Azure-Benutzeroberfläche angezeigten Einstellungen.](/help/sources/images/tutorials/create/dlz/summary.png)

Eine erfolgreiche Verbindung aktualisiert Ihre Benutzeroberfläche von [!DNL Azure Storage Explorer] mit Ihrem [!DNL Data Landing Zone]-Container.

![Zusammenfassung des DLZ-Benutzercontainers, der in der Azure-Benutzeroberfläche hervorgehoben wurde.](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Da Ihr [!DNL Data Landing Zone]-Container jetzt mit [!DNL Azure Storage Explorer] verbunden ist, können Sie damit beginnen, Dateien von Experience Platform in Ihren [!DNL Data Landing Zone]-Container zu exportieren. Um Dateien zu exportieren, müssen Sie eine Verbindung zum [!DNL Data Landing Zone] Ziel in der Experience Platform-Benutzeroberfläche, wie im folgenden Abschnitt beschrieben.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=de) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Stellen Sie sicher, dass Sie Ihre [!DNL Data Landing Zone] Container zu [!DNL Azure Storage Explorer] wie in [Voraussetzungen](#prerequisites) Abschnitt. weil [!DNL Data Landing Zone] ist ein von Adobe bereitgestellter Speicher, müssen Sie keine weiteren Schritte in der Experience Platform-Benutzeroberfläche ausführen, um sich beim Ziel zu authentifizieren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, in dem die exportierten Dateien gespeichert werden.
* **[!UICONTROL Dateityp]**: Wählen Sie das Format aus, das Experience Platform für die exportierten Dateien verwenden soll. Wenn Sie [!UICONTROL CSV] können Sie auch [Dateiformatierungsoptionen konfigurieren](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Komprimierungsformat]**: Wählen Sie den Komprimierungstyp aus, den Experience Platform für die exportierten Dateien verwenden soll.
* **[!UICONTROL Manifestdatei einschließen]**: Schalten Sie diese Option ein, wenn Sie möchten, dass die Exporte eine JSON-Manifestdatei mit Informationen zum Exportspeicherort, zur Exportgröße und mehr enthalten. Das Manifest wird im Format `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Anzeigen von [Beispielmanifestdatei](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Die Manifestdatei enthält die folgenden Felder:
   * `flowRunId`: Die [dataflow run](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) die die exportierte Datei generiert hat.
   * `scheduledTime`: Die Uhrzeit in UTC, zu der die Datei exportiert wurde.
   * `exportResults.sinkPath`: Der Pfad in Ihrem Speicherort, unter dem die exportierte Datei abgelegt wird.
   * `exportResults.name`: Der Name der exportierten Datei.
   * `size`: Die Größe der exportierten Datei in Byte.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Siehe [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel.

### Planung

Im Schritt **[!UICONTROL Planung]** können Sie für Ihr [!DNL Data Landing Zone]-Ziel den [Exportplan einrichten](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling), und Sie können dort auch [den Namen Ihrer exportierten Dateien konfigurieren](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Zuordnen von Attributen und Identitäten {#map}

Im Schritt **[!UICONTROL Zuordnung]** können Sie festlegen, welche Attribute und Identitätsfelder für Ihre Profile exportiert werden sollen. Sie können auch festlegen, dass die Kopfzeilen in der exportierten Datei in einen beliebigen Anzeigenamen geändert werden. Weitere Informationen finden Sie im [Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) im Tutorial zur Benutzeroberfläche der Aktivierung von Batch-Zielen.

## Überprüfen auf einen erfolgreichen Datenexport {#exported-data}

Überprüfen Sie, ob die Daten erfolgreich exportiert wurden, indem Sie Ihren [!DNL Data Landing Zone]-Speicher überprüfen, und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.
