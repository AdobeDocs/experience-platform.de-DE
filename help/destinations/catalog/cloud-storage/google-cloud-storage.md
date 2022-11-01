---
title: (Beta) Google Cloud Storage-Verbindung
description: Erfahren Sie, wie Sie eine Verbindung zu Google Cloud Storage herstellen und Segmente aktivieren oder Datensätze exportieren.
source-git-commit: 56fd7a5ab58186367c729cb4ca8c3b4213c44900
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 28%

---

# (Beta) [!DNL Google Cloud Storage] connection

>[!IMPORTANT]
>
>Dieses Ziel befindet sich derzeit in der Betaversion und steht nur einer begrenzten Anzahl von Kunden zur Verfügung. Um Zugang zur [!DNL Google Cloud Storage]-Verbindung zu erhalten, wenden Sie sich an Ihre Kontaktperson beim Adobe-Support und geben Sie Ihre [!DNL Organization ID] an.

## Übersicht {#overview}

Erstellen Sie eine ausgehende Live-Verbindung zu [!DNL Google Cloud Storage] , um Datendateien aus Adobe Experience Platform regelmäßig in Ihre eigenen Buckets zu exportieren.

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den entsprechenden Schemafeldern, wie im Bildschirm Profilattribute auswählen der [Zielaktivierungs-Workflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Mehr dazu [Batch-dateibasierte Ziele](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Voraussetzungen für die Einrichtung der [!DNL Google Cloud Storage] account {#prerequisites}

So verbinden Sie Platform mit [!DNL Google Cloud Storage]müssen Sie zunächst die Interoperabilität für Ihre [!DNL Google Cloud Storage] -Konto. Um auf die Interoperabilitätseinstellung zuzugreifen, öffnen Sie [!DNL Google Cloud Platform] und wählen Sie **[!UICONTROL Einstellungen]** von **[!UICONTROL Cloud-Speicher]** im Navigationsbereich.

![Google Cloud Platform-Dashboard mit hervorgehobenen Cloud-Speicher- und -Einstellungen.](/help/sources/images/tutorials/create/google-cloud-storage/nav.png)

Die **[!UICONTROL Einstellungen]** angezeigt. Von hier aus können Sie Informationen zu Ihrer [!DNL Google] Projekt-ID und Details zu Ihrer [!DNL Google Cloud Storage] -Konto. Um auf die Interoperabilitätseinstellungen zuzugreifen, wählen Sie **[!UICONTROL Interoperabilität]** aus der oberen Kopfzeile.

![Die Registerkarte Interoperabilität wurde im Dashboard der Google Cloud Platform hervorgehoben.](/help/sources/images/tutorials/create/google-cloud-storage/project-access.png)

Die **[!UICONTROL Interoperabilität]** Seite enthält Informationen zur Authentifizierung, zu Zugriffsschlüsseln und zum Standardprojekt, das mit Ihrem Dienstkonto verknüpft ist. Um eine neue Zugriffsschlüssel-ID und einen geheimen Zugriffsschlüssel für Ihr Dienstkonto zu generieren, wählen Sie **[!UICONTROL Erstellen eines Schlüssels für ein Dienstkonto]**.

![Die Option Schlüssel für ein Dienstkonto-Steuerelement erstellen , die im Dashboard der Google Cloud-Plattform hervorgehoben ist.](/help/sources/images/tutorials/create/google-cloud-storage/interoperability.png)

Sie können die neu generierte Zugriffsschlüssel-ID und den geheimen Zugriffsschlüssel verwenden, um Ihre [!DNL Google Cloud Storage] -Konto auf Platform.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](/help/destinations/ui/connect-destination.md) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**.

* **[!UICONTROL Zugriffsschlüssel-ID]**: Eine 61-stellige alphanumerische Zeichenfolge, die zur Authentifizierung Ihrer [!DNL Google Cloud Storage] -Konto auf Platform. Informationen zum Abrufen dieses Werts finden Sie in der [Voraussetzungen](#prerequisites) Abschnitt weiter oben.
* **[!UICONTROL Geheimer Zugriffsschlüssel]**: Eine Base-64-kodierte Zeichenfolge mit 40 Zeichen, die zum Authentifizieren Ihrer [!DNL Google Cloud Storage] -Konto auf Platform. Informationen zum Abrufen dieses Werts finden Sie in der [Voraussetzungen](#prerequisites) Abschnitt weiter oben.
* **[!UICONTROL Verschlüsselungsschlüssel]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien Verschlüsselung hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64-encoded] Zeichenfolge. Ein Beispiel für einen korrekt formatierten base64-kodierten Schlüssel finden Sie im folgenden Dokumentationslink. Der mittlere Teil ist aus Gründen der Kürze gekürzt.

   ![Bild, das ein Beispiel eines korrekt formatierten und base64-verschlüsselten PGP-Schlüssels in der Benutzeroberfläche zeigt](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Weitere Informationen zu diesen Werten finden Sie im Abschnitt [HMAC-Schlüssel für Google Cloud-Speicher](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) Handbuch. Anweisungen zum Generieren Ihrer eigenen Zugriffsschlüssel-ID und Ihres geheimen Zugriffsschlüssels finden Sie im Abschnitt [[!DNL Google Cloud Storage] Quellübersicht](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Bucket-Name]**: Geben Sie den Namen der [!DNL Google Cloud Storage] -Bucket, der von diesem Ziel verwendet werden soll.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, der die exportierten Dateien hosten soll.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Siehe [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

### Zeitplan

Im **[!UICONTROL Planung]** Schritt, können Sie [Exportplan einrichten](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) für Ihre [!DNL Google Cloud Storage] Ziel und Sie können auch [den Namen Ihrer exportierten Dateien konfigurieren](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Zuordnen von Attributen und Identitäten {#map}

Im **[!UICONTROL Zuordnung]** auswählen, können Sie festlegen, welche Attribute und Identitätsfelder für Ihre Profile exportiert werden sollen. Sie können auch auswählen, ob die Header in der exportierten Datei in einen beliebigen Anzeigenamen geändert werden sollen. Weitere Informationen finden Sie unter [Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) im Tutorial zur Aktivierung der Batch-Ziele-Benutzeroberfläche .

## (Beta) Exportieren von Datensätzen {#export-datasets}

Dieses Ziel unterstützt Datensatzexporte. Umfassende Informationen zum Einrichten von Datensatzexporten finden Sie in der [Tutorial zum Exportieren von Datensätzen](/help/destinations/ui/export-datasets.md).

## Validieren eines erfolgreichen Datenexports {#exported-data}

Überprüfen Sie, ob die Daten erfolgreich exportiert wurden, indem Sie Ihre [!DNL Google Cloud Storage] und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.
