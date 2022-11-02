---
title: (Beta) [!DNL Google Ad Manager 360] connection
description: Google Ad Manager 360 ist eine Adserving-Plattform von Google, mit der Herausgeber die Anzeige von Werbung auf ihren Websites, über Videos und in Apps verwalten können.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: 97a39e12d916e4fbd048c0fb9ddfa9bdfa10d438
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 31%

---

# (Beta) [!DNL Google Ad Manager 360] connection

## Übersicht {#overview}

Die [!DNL Google Ad Manager 360] Verbindung aktiviert Batch-Upload für [!DNL publisher provided identifiers] (PPID) nach [!DNL Google Ad Manager 360]über [!DNL Google Cloud Storage].

Weitere Informationen dazu, wie vom Publisher bereitgestellte IDs in Google Ad Manager 360 funktionieren, finden Sie im Abschnitt [Offizielle Google-Dokumentation](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>Dieses Ziel befindet sich derzeit in der Betaversion und steht nur einer begrenzten Anzahl von Kunden zur Verfügung. Um Zugang zur [!DNL Google Ad Manager 360]-Verbindung zu erhalten, wenden Sie sich an Ihre Kontaktperson beim Adobe-Support und geben Sie Ihre [!DNL IMS Organization ID] an.

Die [!DNL Google Ad Manager 360] Zielexporte [!DNL CSV] -Dateien [!DNL Google Cloud Storage] Eimer. Nachdem Sie die [!DNL CSV] -Dateien, müssen Sie sie in Ihre [!DNL Google Ad Manager 360] -Konto.

## Zielspezifikationen {#specifics}

Beachten Sie die folgenden Details, die spezifisch für [!DNL Google Ad Manager 360] Ziele.

* Aktivierte Zielgruppen werden programmgesteuert in der Google-Plattform erstellt und in die CSV-Datei eingefügt.

## Unterstützte Identitäten {#supported-identities}

[!DNL This integration] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Wählen Sie diese Zielidentität aus, an die Zielgruppen gesendet werden sollen [!DNL Google Ad Manager 360] |

{style=&quot;table-layout:auto&quot;}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den entsprechenden Schemafeldern (z. B. Ihre PPID), wie im Bildschirm Profilattribute auswählen der [Zielaktivierungs-Workflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Mehr dazu [Batch-dateibasierte Ziele](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Voraussetzungen {#prerequisites}

### Zulassungsauflistung {#allow-listing}

>[!NOTE]
>
>Die Zulassungsliste ist vor der Einrichtung der ersten [!DNL Google Ad Manager] Ziel in Platform. Vergewissern Sie sich, dass die unten beschriebene Zulassungsliste durch [!DNL Google] vor dem Erstellen eines Ziels.

>[!IMPORTANT]
>
>Google hat die Anbindung von externen Zielgruppen-Management-Plattformen an Google Ad Manager 360 vereinfacht. Sie können jetzt den Vorgang zum selbstständigen Verknüpfen mit Google Ad Manager 360 durchführen. Lesen [Segmente aus Datenverwaltungsplattformen](https://support.google.com/admanager/answer/3289669?hl=en) in der Google-Dokumentation. Sie sollten über die unten aufgeführten IDs verfügen.

* **Konto-ID**: Kontokennung der Adobe mit Google. Konto-ID: 87933855.
* **Kunden-ID**: Kundenkonto-ID der Adobe mit Google. Kunden-ID: 89690775.
* **Netzwerkcode**: Dies ist Ihr [!DNL Google Ad Manager] Netzwerkkennung, gefunden unter **[!UICONTROL Admin > Globale Einstellungen]** in der Google-Benutzeroberfläche sowie in der URL.
* **Zielgruppenverknüpfungskennung**: Dies ist eine spezifische Kennung, die mit Ihrem [!DNL Google Ad Manager] Netzwerk (nicht [!DNL Network code]), auch gefunden unter **[!UICONTROL Admin > Globale Einstellungen]** in der Google-Benutzeroberfläche.
* Ihr Kontotyp. DFP von Google oder AdX Buyer.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**.

* **[!UICONTROL Zugriffsschlüssel-ID]**: Eine 61-stellige alphanumerische Zeichenfolge, die zur Authentifizierung Ihrer [!DNL Google Cloud Storage] -Konto auf Platform.
* **[!UICONTROL Geheimer Zugriffsschlüssel]**: Eine base64-kodierte Zeichenfolge mit 40 Zeichen, die zum Authentifizieren Ihrer [!DNL Google Cloud Storage] -Konto auf Platform.

Weitere Informationen zu diesen Werten finden Sie unter [HMAC-Schlüssel für Google Cloud-Speicher](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) Handbuch. Anweisungen zum Generieren Ihrer eigenen Zugriffsschlüssel-ID und Ihres geheimen Zugriffsschlüssels finden Sie im Abschnitt [[!DNL Google Cloud Storage] Quellübersicht](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Bucket-Name]**: Geben Sie den Namen der [!DNL Google Cloud Storage] -Bucket, der von diesem Ziel verwendet werden soll.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, der die exportierten Dateien hosten soll.
* **[!UICONTROL Konto-ID]**: Füllen Sie Ihre Zielgruppen-Link-ID mit [!DNL Google].
* **[!UICONTROL Kontotyp]**: Wählen Sie je nach Konto bei Google eine Option aus:
   * Verwenden Sie `DFP by Google` für for Publishers.[!DNL DoubleClick]
   * Verwendung `AdX buyer` für [!DNL Google AdX]

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Siehe [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

Im Schritt zur Identitätszuordnung sehen Sie die folgenden vorausgefüllten Zuordnungen:

| Vorausgefüllte Zuordnung | Beschreibung |
|---------|----------|
| `ECID` -> `ppid` | Dies ist die einzige vom Benutzer bearbeitbare vorausgefüllte Zuordnung. Sie können beliebige Attribute oder Identitäts-Namespaces aus Platform auswählen und sie `ppid`. |
| `metadata.segment.alias` -> `list_id` | Ordnet Segmentnamen der Experience Platform Segmentkennungen in der Google-Plattform zu. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Teilt der Google-Plattform mit, wann disqualifizierte Benutzer aus Segmenten entfernt werden sollen. |

Diese Zuordnungen sind erforderlich für [!DNL Google Ad Manager 360] und von Adobe Experience Platform automatisch für alle erstellt werden [!DNL Google Ad Manager 360] Verbindungen.

![UI-Bild mit dem Zuordnungsschritt für Google Ad Manager 360.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Exportierte Daten {#exported-data}

Überprüfen Sie, ob die Daten erfolgreich exportiert wurden, indem Sie Ihre [!DNL Google Cloud Storage] und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.
