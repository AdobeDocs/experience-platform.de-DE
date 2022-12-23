---
keywords: Azure Blob;Blob-Ziel;s3;Azure Blob-Ziel
title: Azure Blob-Verbindung
description: Stellen Sie eine aktive ausgehende Verbindung mit Ihrem Azure Blob-Speicher her, um regelmäßig CSV-Datendateien aus Adobe Experience Platform zu exportieren.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: a07557ec398631ece0c8af6ec7b32e0e8593e24b
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 90%

---

# [!DNL Azure Blob]-Verbindung

## Ziel-Änderungsprotokoll {#changelog}

>[!IMPORTANT]
>
>Mit der Beta-Version der Funktionalität zum Exportieren von Datensätzen und der verbesserten Dateiexportfunktion werden jetzt möglicherweise zwei [!DNL Azure Blob]-Karten im Zielkatalog angezeigt.
>* Falls Sie bereits Dateien in das **[!UICONTROL Azure Blob]**-Ziel exportieren, erstellen Sie bitte neue Datenflüsse zum neuen **[!UICONTROL Azure Blob Beta]**-Ziel.
>* Falls Sie noch keinen Datenfluss zum **[!UICONTROL Azure Blob]**-Ziel erstellt haben, verwenden Sie bitte die neue Karte **[!UICONTROL Azure Blob-Beta]** zum Exportieren von Dateien in **[!UICONTROL Azure Blob]**.


![Abbildung der beiden Azure Blob-Zielkarten, die diese nebeneinander in einer Ansicht zeigt.](../../assets/catalog/cloud-storage/blob/two-azure-blob-destination-cards.png)

Zu den Verbesserungen bei der neuen [!DNL Azure Blob]-Zielkarte gehören:

* [Unterstützung für den Datensatzexport](/help/destinations/ui/export-datasets.md).
* Zusätzliche [Dateibenennungsoptionen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Möglichkeit zum Festlegen benutzerdefinierter Datei-Kopfzeilen in exportierten Dateien durch den [verbesserten Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Möglichkeit zum Anpassen der Formatierung exportierter CSV-Datendateien](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Übersicht {#overview}

[!DNL Azure Blob] (nachstehend: [!DNL Blob]) ist die Objektspeicherlösung von Microsoft für die Cloud. In diesem Tutorial finden Sie die Schritte zum Erstellen eines [!DNL Blob]-Ziels mithilfe der [!DNL Platform]-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-time Customer Profile]](../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein gültiges [!DNL Blob]-Ziel verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Aktivieren von Segmenten für Ihr Ziel](../../ui/activate-batch-profile-destinations.md) fortfahren.

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Unterstützte Dateiformate {#file-formats}

[!DNL Experience Platform] unterstützt das folgende Dateiformat für den Export in [!DNL Azure Blob]:

* Kommagetrennte Werte (CSV): Die Unterstützung für exportierte Datendateien ist derzeit auf kommagetrennte Werte beschränkt.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="Öffentlicher RSA-Schlüssel"
>abstract="Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Schlüssel finden Sie im folgenden Dokumentations-Link."

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**.

* **[!UICONTROL Verbindungszeichenfolge]**: Die Verbindungszeichenfolge ist für den Zugriff auf Daten in Ihrem Blob-Speicher erforderlich. Das [!DNL Blob]-Verbindungszeichenfolgenmuster beginnt mit: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Weitere Informationen zur Konfiguration der [!DNL Blob]-Verbindungszeichenfolge finden Sie unter [Konfigurieren der Verbindungszeichenfolge für ein Azure-Speicherkonto](https://docs.microsoft.com/de-de/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) in der Microsoft-Dokumentation.
* **[!UICONTROL Verschlüsselungsschlüssel]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der Abbildung unten.

   ![Bild, das ein Beispiel eines korrekt formatierten PGP-Schlüssels in der Benutzeroberfläche anzeigt](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für dieses Ziel ein.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, in dem die exportierten Dateien gespeichert werden.
* **[!UICONTROL Container]**: Geben Sie den Namen des [!DNL Azure Blob Storage]-Containers ein, der von diesem Ziel verwendet werden soll.
* **[!UICONTROL Dateityp]**: Wählen Sie die Format-Experience Platform aus, die für die exportierten Dateien verwendet werden soll. Diese Option steht nur für die **[!UICONTROL Azure Blob beta]** Ziel. Bei der Auswahl der [!UICONTROL CSV] können Sie auch [Dateiformatierungsoptionen konfigurieren](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Komprimierungsformat]**: Wählen Sie den Komprimierungstyp aus, den die Experience Platform für die exportierten Dateien verwenden soll. Diese Option steht nur für die **[!UICONTROL Azure Blob beta]** Ziel.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../../ui/activate-batch-profile-destinations.md).

## (Beta) Exportieren von Datensätzen {#export-datasets}

Dieses Ziel unterstützt Datensatzexporte. Umfassende Informationen zum Einrichten von Datensatzexporten finden Sie im [Tutorial zum Exportieren von Datensätzen](/help/destinations/ui/export-datasets.md).

## Exportierte Daten {#exported-data}

Für [!DNL Azure Blob Storage]-Ziele erstellt [!DNL Platform] eine `.csv`-Datei an dem von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../../ui/activate-batch-profile-destinations.md) im Tutorial zur Segmentaktivierung.