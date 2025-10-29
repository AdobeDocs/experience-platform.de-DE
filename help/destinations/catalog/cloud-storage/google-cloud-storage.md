---
title: Google Cloud Storage-Verbindung
description: Erfahren Sie, wie Sie eine Verbindung zum Google Cloud-Speicher herstellen und Zielgruppen aktivieren oder Datensätze exportieren.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 42%

---

# [!DNL Google Cloud Storage]-Verbindung

## Übersicht {#overview}

Erstellen Sie eine ausgehende Live-Verbindung zu [!DNL Google Cloud Storage], um Datendateien aus Adobe Experience Platform regelmäßig in Ihre eigenen Behälter zu exportieren.

## Herstellen einer Verbindung zu Ihrem [!DNL Google Cloud Storage] über API oder Benutzeroberfläche {#connect-api-or-ui}

* Um über die Experience Platform-Benutzeroberfläche eine Verbindung zu Ihrem [!DNL Google Cloud Storage]-Speicherort herzustellen, lesen Sie die Abschnitte [Mit dem Ziel verbinden](#connect) und [Zielgruppen für dieses Ziel aktivieren](#activate).
* Um programmgesteuert eine Verbindung zu Ihrem [!DNL Google Cloud Storage]-Speicherort herzustellen, lesen Sie das Tutorial [Aktivieren von Zielgruppen für dateibasierte Ziele mithilfe der Flow Service-API](../../api/activate-segments-file-based-destinations.md).

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den entsprechenden Schemafeldern, wie sie im Bildschirm „Profilattribute auswählen“ des [Zielaktivierungs-Workflows](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) ausgewählt sind. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Datensätze exportieren {#export-datasets}

Dieses Ziel unterstützt Datensatzexporte. Vollständige Informationen zum Einrichten von Datensatzexporten finden Sie in den Tutorials:

* So [&#x200B; Sie Datensätze mithilfe der Benutzeroberfläche von Experience Platform &#x200B;](/help/destinations/ui/export-datasets.md).
* So [&#x200B; Sie Datensätze mithilfe der Flow Service-API programmgesteuert &#x200B;](/help/destinations/api/export-datasets.md).

## Dateiformat der exportierten Daten {#file-format}

Beim Exportieren *Zielgruppendaten* erstellt Experience Platform eine `.csv`-, `parquet`- oder `.json`-Datei an dem von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie im Abschnitt [Unterstützte Dateiformate für den Export](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) im Tutorial zur Zielgruppenaktivierung.

Beim Exportieren *Datensätze* erstellt Experience Platform eine `.parquet`- oder `.json`-Datei an dem von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie im Abschnitt [Überprüfen eines erfolgreichen Datensatzexports](../../ui/export-datasets.md#verify) im Tutorial zum Exportieren von Datensätzen.

## Vorausgesetzte Einrichtung für das Verbinden Ihres [!DNL Google Cloud Storage]-Kontos {#prerequisites}

Um Experience Platform mit [!DNL Google Cloud Storage] zu verbinden, müssen Sie zunächst die Interoperabilität für Ihr [!DNL Google Cloud Storage]-Konto aktivieren. Um auf die Interoperabilitätseinstellung zuzugreifen, öffnen Sie [!DNL Google Cloud Platform] und wählen Sie **[!UICONTROL Settings]** aus der Option **[!UICONTROL Cloud Storage]** im Navigationsbereich aus.

![Das Dashboard der Google Cloud-Plattform mit Hervorhebung von Cloud-Speicher und Einstellungen.](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

Die Seite **[!UICONTROL Settings]** wird angezeigt. Von hier aus können Sie Informationen zu Ihrer [!DNL Google]-Projekt-ID und Details zu Ihrem [!DNL Google Cloud Storage]-Konto ansehen. Um auf die Interoperabilitätseinstellungen zuzugreifen, wählen Sie **[!UICONTROL Interoperability]** in der oberen Kopfzeile aus.

![Die hervorgehobene Registerkarte „Interoperabilität“ im Dashboard der Google Cloud-Plattform.](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

Die **[!UICONTROL Interoperability]** enthält Informationen zur Authentifizierung, zu Zugriffsschlüsseln und zum Standardprojekt, das mit Ihrem Service-Konto verknüpft ist. Um eine neue Zugriffsschlüssel-ID und einen geheimen Zugriffsschlüssel für Ihr Service-Konto zu generieren, wählen Sie **[!UICONTROL Create a Key for a Service Account]** aus.

![Das hervorgehobene Steuerelement „Schlüssel für ein Dienstkonto erstellen“ im Dashboard der Google Cloud-Plattform.](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

Sie können die neu generierte Zugriffsschlüssel-ID und den geheimen Zugriffsschlüssel verwenden, um Ihr [!DNL Google Cloud Storage]-Konto mit Experience Platform zu verbinden.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. &#x200B;](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](/help/destinations/ui/connect-destination.md) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Connect to destination]** aus.

* **[!UICONTROL Access key ID]**: Eine 61-stellige alphanumerische Zeichenfolge, die zur Authentifizierung Ihres [!DNL Google Cloud Storage]-Kontos bei Experience Platform verwendet wird. Informationen zum Abrufen dieses Werts finden Sie im Abschnitt [Voraussetzungen](#prerequisites) weiter oben.
* **[!UICONTROL Secret access key]**: Eine mit Base64 verschlüsselte Zeichenfolge mit 40 Zeichen, die zum Authentifizieren Ihres [!DNL Google Cloud Storage] bei Experience Platform verwendet wird. Informationen zum Abrufen dieses Werts finden Sie im Abschnitt [Voraussetzungen](#prerequisites) weiter oben.
* **[!UICONTROL Encryption key]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der folgenden Abbildung.

  ![Abbildung eines Beispiels für einen korrekt formatierten PGP-Schlüssel in der Benutzeroberfläche](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Weitere Informationen zu diesen Werten finden Sie im Handbuch [HMAC-Schlüssel für Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Anweisungen zum Generieren Ihrer eigenen Zugriffsschlüssel-ID und Ihres geheimen Zugriffsschlüssels finden Sie im Abschnitt [[!DNL Google Cloud Storage] Quelle – Übersicht](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Description]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Bucket name]**: Geben Sie den Namen des [!DNL Google Cloud Storage]-Behälters ein, der von diesem Ziel verwendet werden soll.
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

### Erforderliche [!DNL Google Cloud Storage]-Berechtigungen {#required-google-cloud-storage-permission}

Um Daten erfolgreich mit Ihrem [!DNL Google Cloud Storage]-Speicherort zu verbinden und dorthin zu exportieren, benötigen Sie die folgenden [!DNL Google Cloud Storage] für Ihre Buckets:

* `orgpolicy.policy.get`
* `resourcemanager.projects.get`
* `resourcemanager.projects.list`
* `storage.managedFolders.create`
* `storage.multipartUploads.abort`
* `storage.multipartUploads.create`
* `storage.multipartUploads.listParts`
* `storage.objects.create`
* `storage.objects.list`

Weitere Informationen zu [Zugriffssteuerung und Berechtigungen](https://cloud.google.com/storage/docs/access-control/iam-permissions) finden Sie in [!DNL Google Cloud Storage].

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[&#x200B; &#x200B;](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen [&#x200B; Aktivieren von Zielgruppen für dieses Ziel finden Sie &#x200B;](../../ui/activate-batch-profile-destinations.md)Aktivieren von Zielgruppendaten für Batch-Profil-).

### Planung

Im **[!UICONTROL Scheduling]** Schritt können Sie [Exportplan einrichten](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) für Ihr [!DNL Google Cloud Storage]-Ziel festlegen und [den Namen Ihrer exportierten Dateien konfigurieren](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Zuordnen von Attributen und Identitäten {#map}

Im **[!UICONTROL Mapping]** Schritt können Sie auswählen, welche Attribut- und Identitätsfelder für Ihre Profile exportiert werden sollen. Sie können auch festlegen, dass die Kopfzeilen in der exportierten Datei in einen beliebigen Anzeigenamen geändert werden. Weitere Informationen finden Sie im [Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) im Tutorial zur Benutzeroberfläche der Aktivierung von Batch-Zielen.

## Überprüfen auf einen erfolgreichen Datenexport {#exported-data}

Um festzustellen, ob die Daten erfolgreich exportiert wurden, überprüfen Sie Ihren [!DNL Google Cloud Storage]-Behälter und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.

## Zulassungsliste von IP-Adressen {#ip-address-allow-list}

Siehe den Artikel [IP-Adresse](ip-address-allow-list.md) , wenn Sie einer Zulassungsliste Adobe auf die Zulassungsliste setzen-IPs hinzufügen müssen.