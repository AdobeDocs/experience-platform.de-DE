---
title: Azure Data Lake Storage Gen2-Verbindung
description: Erfahren Sie, wie Sie eine Verbindung zu Azure Data Lake Storage Gen2 herstellen, um Zielgruppen zu aktivieren und Datensätze zu exportieren.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: d265a02d-c901-4b39-8714-fe9ecdbb5bb1
source-git-commit: 8771aa0df001e8ef81d4ad712f4d1f9661b405b2
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 55%

---

# [!DNL Azure Data Lake Storage Gen2]-Verbindung

## Übersicht {#overview}

Auf dieser Seite erfahren Sie, wie Sie eine ausgehende Live-Verbindung zu Ihrem [[!DNL Azure Data Lake Storage Gen2]](https://learn.microsoft.com/de-de/azure/storage/blobs/data-lake-storage-introduction) ([!DNL ADLS Gen2]) Data Lake herstellen, um regelmäßig Datendateien aus Experience Platform zu exportieren.

## Verbinden Sie Ihre [!DNL ADLS Gen2] Speicher über API oder Benutzeroberfläche {#connect-api-or-ui}

* So stellen Sie eine Verbindung zu Ihrer [!DNL ADLS Gen2] Speicherort mithilfe der Platform-Benutzeroberfläche, lesen Sie die Abschnitte . [Mit Ziel verbinden](#connect) und [Aktivieren von Zielgruppen für dieses Ziel](#activate) unten.
* So stellen Sie eine Verbindung zu Ihrer [!DNL ADLS Gen2] Speicherort programmgesteuert, lesen Sie die [Aktivieren von Zielgruppen für dateibasierte Ziele mithilfe des Tutorials zur Flow Service-API](../../api/activate-segments-file-based-destinations.md).

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

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](/help/destinations/ui/connect-destination.md) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

* **[!UICONTROL URL]**: Der Endpunkt für [!DNL Azure Data Lake Storage Gen2]. Das Endpunktmuster ist: `abfss://<container>@<accountname>.dfs.core.windows.net`.
* **[!UICONTROL Mandant]**: Die Mandanteninformationen, die Ihre Anwendung enthalten.
* **[!UICONTROL Service-Prinzipal-ID]**: Die Client-ID der Anwendung.
* **[!UICONTROL Service-Prinzipal-Schlüssel]**: Der Schlüssel der Anwendung.
* **[!UICONTROL Verschlüsselungsschlüssel]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der folgenden Abbildung.

  ![Abbildung eines Beispiels für einen korrekt formatierten PGP-Schlüssel in der Benutzeroberfläche](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

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

### Planung {#scheduling}

Im Schritt **[!UICONTROL Planung]** können Sie für Ihr [!DNL Azure Data Lake Storage Gen2]-Ziel den [Exportplan einrichten](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling), und Sie können dort auch [den Namen Ihrer exportierten Dateien konfigurieren](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Zuordnen von Attributen und Identitäten {#map}

Im Schritt **[!UICONTROL Zuordnung]** können Sie festlegen, welche Attribute und Identitätsfelder für Ihre Profile exportiert werden sollen. Sie können auch festlegen, dass die Kopfzeilen in der exportierten Datei in einen beliebigen Anzeigenamen geändert werden. Weitere Informationen finden Sie im [Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) im Tutorial zur Benutzeroberfläche der Aktivierung von Batch-Zielen.

## Überprüfen auf einen erfolgreichen Datenexport {#exported-data}

Überprüfen Sie, ob die Daten erfolgreich exportiert wurden, indem Sie Ihren [!DNL Azure Data Lake Storage Gen2]-Speicher überprüfen, und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.
