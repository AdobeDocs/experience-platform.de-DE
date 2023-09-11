---
title: Amazon S3-Verbindung
description: Erstellen Sie eine aktive ausgehende Verbindung zu Ihrem S3-Speicher in Amazon Web Services (AWS), um in regelmäßigen Abständen CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Behälter zu exportieren.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 950370683f648771d91689e84c3d782824fb01f4
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 69%

---

# [!DNL Amazon S3]-Verbindung {#s3-connection}

## Ziel-Änderungsprotokoll {#changelog}

Mit der Experience Platform-Version vom Juli 2023 wird die [!DNL Amazon S3] Das Ziel bietet neue Funktionen, wie unten aufgeführt:

* [!BADGE Beta]{type=Informative}[Unterstützung für den Datensatzexport](/help/destinations/ui/export-datasets.md).
* Zusätzliche [Dateibenennungsoptionen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Möglichkeit zum Festlegen benutzerdefinierter Datei-Kopfzeilen in exportierten Dateien durch den [verbesserten Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Möglichkeit zum Anpassen der Formatierung exportierter CSV-Datendateien](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Verbinden Sie Ihre [!DNL Amazon S3] Speicher über API oder Benutzeroberfläche {#connect-api-or-ui}

* So stellen Sie eine Verbindung zu Ihrer [!DNL Amazon S3] Speicherort mithilfe der Platform-Benutzeroberfläche, lesen Sie die Abschnitte . [Mit Ziel verbinden](#connect) und [Aktivieren von Zielgruppen für dieses Ziel](#activate) unten.
* So stellen Sie eine Verbindung zu Ihrer [!DNL Amazon S3] Speicherort programmgesteuert, lesen Sie die [Aktivieren von Zielgruppen für dateibasierte Ziele mithilfe des Tutorials zur Flow Service-API](../../api/activate-segments-file-based-destinations.md).

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
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Auf dem Amazon S3-Profil basierender Exporttyp](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="Öffentlicher RSA-Schlüssel"
>abstract="Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Schlüssel finden Sie im folgenden Dokumentations-Link."

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und klicken Sie auf **[!UICONTROL Mit Ziel verbinden]**.

* **[!DNL Amazon S3]-Zugriffsschlüssel** und geheimer **[!DNL Amazon S3]-Schlüssel**: Generieren Sie in [!DNL Amazon S3] ein `access key - secret access key`-Paar, um Platform Zugriff auf Ihr [!DNL Amazon S3]-Konto zu gewähren. Weitere Informationen finden Sie in der [Amazon Web Services-Dokumentation](https://docs.aws.amazon.com/de_de/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Verschlüsselungsschlüssel]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der folgenden Abbildung.

  ![Abbildung eines Beispiels für einen korrekt formatierten PGP-Schlüssel in der Benutzeroberfläche](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Behältername"
>abstract="Muss zwischen 3 und 63 Zeichen lang sein. Muss mit einem Buchstaben oder einer Zahl beginnen und enden. Darf nur Kleinbuchstaben, Zahlen oder Bindestriche ( - ) enthalten. Darf nicht als IP-Adresse formatiert sein (z. B. 192.100.1.1)."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Ordnerpfad"
>abstract="Darf nur die Zeichen A-Z, a-z, 0-9 und die folgenden Sonderzeichen enthalten: `/!-_.'()"^[]+$%.*"`. Um einen Ordner pro Zielgruppendatei zu erstellen, fügen Sie das Makro `/%SEGMENT_NAME%` oder `/%SEGMENT_ID%` oder `/%SEGMENT_NAME%/%SEGMENT_ID%` in das Textfeld ein. Makros können nur am Ende des Ordnerpfads eingefügt werden. Sehen Sie sich Beispiele für Makros in der Dokumentation an."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=de#use-macros" text="Verwenden von Makros zum Erstellen eines Ordners an Ihrem Speicherort"

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung dieses Ziels ein.
* **[!UICONTROL Behältername]**: Geben Sie den Namen des [!DNL Amazon S3]-Behälters ein, der von diesem Ziel verwendet werden soll.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, in dem die exportierten Dateien gespeichert werden.
* **[!UICONTROL Dateityp]**: Wählen Sie das Format aus, das Experience Platform für die exportierten Dateien verwenden soll. Wenn Sie [!UICONTROL CSV] können Sie auch [Dateiformatierungsoptionen konfigurieren](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Komprimierungsformat]**: Wählen Sie den Komprimierungstyp aus, den Experience Platform für die exportierten Dateien verwenden soll.
* **[!UICONTROL Manifestdatei einschließen]**: Schalten Sie diese Option ein, wenn Sie möchten, dass die Exporte eine JSON-Manifestdatei mit Informationen zum Exportspeicherort, zur Exportgröße und mehr enthalten. Das Manifest wird im Format `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Anzeigen von [Beispielmanifestdatei](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Die Manifestdatei enthält die folgenden Felder:
   * `flowRunId`: Die [dataflow run](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) die die exportierte Datei generiert hat.
   * `scheduledTime`: Die Uhrzeit in UTC, zu der die Datei exportiert wurde.
   * `exportResults.sinkPath`: Der Pfad in Ihrem Speicherort, unter dem die exportierte Datei abgelegt wird.
   * `exportResults.name`: Der Name der exportierten Datei.
   * `size`: Die Größe der exportierten Datei in Byte.

>[!TIP]
>
>Im Zielverbindungs-Workflow können Sie einen benutzerdefinierten Ordner in Ihrem Amazon S3-Speicher pro exportierter Zielgruppendatei erstellen. Anweisungen finden Sie unter [Verwenden von Makros zum Erstellen eines Ordners an Ihrem Speicherort](overview.md#use-macros).

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

### Erforderliche [!DNL Amazon S3]-Berechtigungen {#required-s3-permission}

Um Daten erfolgreich mit Ihrem [!DNL Amazon S3]-Speicherort zu verbinden und dorthin zu exportieren, erstellen Sie ein Benutzerprofil für Identitäts- und Zugriffsverwaltung (IAM) für [!DNL Platform] in [!DNL Amazon S3] und weisen Berechtigungen für die folgenden Aktionen zu:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Siehe [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel.

## (Beta) Exportieren von Datensätzen {#export-datasets}

Dieses Ziel unterstützt Datensatzexporte. Vollständige Informationen zum Einrichten von Datensatzexporten finden Sie in den Tutorials:

* Anleitung [Datensätze mithilfe der Benutzeroberfläche von Platform exportieren](/help/destinations/ui/export-datasets.md).
* Anleitung [Datensätze programmgesteuert mit der Flow Service-API exportieren](/help/destinations/api/export-datasets.md).

## Exportierte Daten {#exported-data}

Für [!DNL Amazon S3]-Ziele erstellt [!DNL Platform] eine Datendatei an dem von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md) im Tutorial zur Aktivierung der Zielgruppe.
