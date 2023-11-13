---
title: Verbindung zu Google Cloud Storage
description: Erfahren Sie, wie Sie eine Verbindung zu Google Cloud Storage herstellen und Zielgruppen aktivieren oder Datensätze exportieren.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: 47197b745bebb6564d912d9dc045593bc076ae2a
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 73%

---

# [!DNL Google Cloud Storage]-Verbindung

## Übersicht {#overview}

Erstellen Sie eine ausgehende Live-Verbindung zu [!DNL Google Cloud Storage], um Datendateien aus Adobe Experience Platform regelmäßig in Ihre eigenen Behälter zu exportieren.

## Verbinden Sie Ihre [!DNL Google Cloud Storage] Speicher über API oder Benutzeroberfläche {#connect-api-or-ui}

* So stellen Sie eine Verbindung zu Ihrer [!DNL Google Cloud Storage] Speicherort mithilfe der Platform-Benutzeroberfläche, lesen Sie die Abschnitte . [Mit Ziel verbinden](#connect) und [Aktivieren von Zielgruppen für dieses Ziel](#activate) unten.
* So stellen Sie eine Verbindung zu Ihrer [!DNL Google Cloud Storage] Speicherort programmgesteuert, lesen Sie die [Aktivieren von Zielgruppen für dateibasierte Ziele mithilfe des Tutorials zur Flow Service-API](../../api/activate-segments-file-based-destinations.md).

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
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den entsprechenden Schemafeldern, wie sie im Bildschirm „Profilattribute auswählen“ des [Zielaktivierungs-Workflows](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) ausgewählt sind. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Vorausgesetzte Einrichtung für das Verbinden Ihres [!DNL Google Cloud Storage]-Kontos {#prerequisites}

Um Platform mit [!DNL Google Cloud Storage] zu verbinden, müssen Sie zunächst die Interoperabilität für Ihr [!DNL Google Cloud Storage]-Konto aktivieren. Um auf die Interoperabilitätseinstellung zuzugreifen, öffnen Sie [!DNL Google Cloud Platform] und wählen Sie **[!UICONTROL Einstellungen]** in der Option **[!UICONTROL Cloud-Speicher]** im Navigationsbereich aus.

![Das Dashboard der Google Cloud-Plattform mit Hervorhebung von Cloud-Speicher und Einstellungen.](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

Die Seite **[!UICONTROL Einstellungen]** wird angezeigt. Von hier aus können Sie Informationen zu Ihrer [!DNL Google]-Projekt-ID und Details zu Ihrem [!DNL Google Cloud Storage]-Konto ansehen. Um auf die Interoperabilitätseinstellungen zuzugreifen, wählen Sie **[!UICONTROL Interoperabilität]** aus der oberen Kopfzeile aus.

![Die hervorgehobene Registerkarte „Interoperabilität“ im Dashboard der Google Cloud-Plattform.](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

Die Seite **[!UICONTROL Interoperabilität]** enthält Informationen zur Authentifizierung, zu Zugriffsschlüsseln und zum Standardprojekt, das mit Ihrem Service-Konto verknüpft ist. Um eine neue Zugriffsschlüssel-ID und einen geheimen Zugriffsschlüssel für Ihr Service-Konto zu generieren, wählen Sie **[!UICONTROL Schlüssel für ein Service-Konto erstellen]** aus.

![Das hervorgehobene Steuerelement „Schlüssel für ein Dienstkonto erstellen“ im Dashboard der Google Cloud-Plattform.](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

Sie können die neu generierte Zugriffsschlüssel-ID und den geheimen Zugriffsschlüssel verwenden, um Ihr [!DNL Google Cloud Storage]-Konto mit Platform zu verbinden.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](/help/destinations/ui/connect-destination.md) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

* **[!UICONTROL Zugriffsschlüssel-ID]**: eine 61-stellige alphanumerische Zeichenfolge, die zur Authentifizierung Ihres [!DNL Google Cloud Storage]-Kontos bei Platform verwendet wird. Informationen zum Abrufen dieses Werts finden Sie im Abschnitt [Voraussetzungen](#prerequisites) weiter oben.
* **[!UICONTROL Geheimer Zugriffsschlüssel]**: eine mit Base64 verschlüsselte Zeichenfolge mit 40 Zeichen, die zum Authentifizieren Ihre [!DNL Google Cloud Storage]-Kontos bei Platform verwendet wird. Informationen zum Abrufen dieses Werts finden Sie im Abschnitt [Voraussetzungen](#prerequisites) weiter oben.
* **[!UICONTROL Verschlüsselungsschlüssel]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der folgenden Abbildung.

  ![Abbildung eines Beispiels für einen korrekt formatierten PGP-Schlüssel in der Benutzeroberfläche](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Weitere Informationen zu diesen Werten finden Sie im Handbuch [HMAC-Schlüssel für Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Anweisungen zum Generieren Ihrer eigenen Zugriffsschlüssel-ID und Ihres geheimen Zugriffsschlüssels finden Sie im Abschnitt [[!DNL Google Cloud Storage] Quelle – Übersicht](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Behältername]**: Geben Sie den Namen des [!DNL Google Cloud Storage]-Behälters ein, der von diesem Ziel verwendet werden soll.
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
>* Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Siehe [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel.

### Planung

Im Schritt **[!UICONTROL Planung]** können Sie für Ihr [!DNL Google Cloud Storage]-Ziel den [Exportplan einrichten](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling), und Sie können dort auch [den Namen Ihrer exportierten Dateien konfigurieren](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Zuordnen von Attributen und Identitäten {#map}

Im Schritt **[!UICONTROL Zuordnung]** können Sie festlegen, welche Attribute und Identitätsfelder für Ihre Profile exportiert werden sollen. Sie können auch festlegen, dass die Kopfzeilen in der exportierten Datei in einen beliebigen Anzeigenamen geändert werden. Weitere Informationen finden Sie im [Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) im Tutorial zur Benutzeroberfläche der Aktivierung von Batch-Zielen.

## Datensätze exportieren {#export-datasets}

Dieses Ziel unterstützt Datensatzexporte. Vollständige Informationen zum Einrichten von Datensatzexporten finden Sie in den Tutorials:

* Anleitung [Datensätze mithilfe der Benutzeroberfläche von Platform exportieren](/help/destinations/ui/export-datasets.md).
* Anleitung [Datensätze programmgesteuert mit der Flow Service-API exportieren](/help/destinations/api/export-datasets.md).

## Überprüfen auf einen erfolgreichen Datenexport {#exported-data}

Um festzustellen, ob die Daten erfolgreich exportiert wurden, überprüfen Sie Ihren [!DNL Google Cloud Storage]-Behälter und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.
