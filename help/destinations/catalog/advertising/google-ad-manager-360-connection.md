---
title: (Beta) [!DNL Google Ad Manager 360] connection
description: Google Ad Manager 360 ist eine Adserving-Plattform von Google, mit der Herausgeber die Anzeige von Werbung auf ihren Websites, über Videos und in Apps verwalten können.
source-git-commit: 60ae86ed6e741bd7739086105bfe70952841d454
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 15%

---

# (Beta) [!DNL Google Ad Manager 360] connection

## Übersicht {#overview}

Die [!DNL Google Ad Manager 360] Verbindung aktiviert Batch-Upload für [!DNL publisher provided identifiers] (PPID) nach [!DNL Google Ad Manager 360]über [!DNL Google Cloud Storage].

Weitere Informationen dazu, wie vom Publisher bereitgestellte IDs in Google Ad Manager 360 funktionieren, finden Sie im Abschnitt [Offizielle Google-Dokumentation](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>Dieses Ziel befindet sich derzeit in der Betaversion und steht nur einer begrenzten Anzahl von Kunden zur Verfügung. So fordern Sie Zugriff auf die [!DNL Google Ad Manager 360] Verbindung herstellen, kontaktieren Sie Ihren Kundenbetreuer und geben Sie Ihre [!DNL IMS Organization ID].

Die [!DNL Google Ad Manager 360] Zielexporte [!DNL CSV] -Dateien [!DNL Google Cloud Storage] Eimer. Nachdem Sie die [!DNL CSV] -Dateien, müssen Sie sie in Ihre [!DNL Google Ad Manager 360] -Konto.

## Zielspezifikationen {#specifics}

Beachten Sie die folgenden Details, die spezifisch für [!DNL Google Ad Manager 360] Ziele.

* Aktivierte Zielgruppen werden programmgesteuert in der Google-Plattform erstellt und in die CSV-Datei eingefügt.

## Unterstützte Identitäten {#supported-identities}

[!DNL This integration] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten.

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Wählen Sie diese Zielidentität aus, an die Zielgruppen gesendet werden sollen [!DNL Google Ad Manager 360] |

{style=&quot;table-layout:auto&quot;}

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm Profilattribute im [Zielaktivierungs-Workflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Mehr dazu [Batch-dateibasierte Ziele](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Voraussetzungen {#prerequisites}

### Zulassungsauflistung {#allow-listing}

>[!NOTE]
>
>Die Zulassungsliste ist vor der Einrichtung der ersten [!DNL Google Ad Manager] Ziel in Platform. Vergewissern Sie sich, dass die unten beschriebene Zulassungsliste durch [!DNL Google] vor dem Erstellen eines Ziels.

Vor der Erstellung [!DNL Google Ad Manager 360] Ziel in Platform müssen Sie [!DNL Google] , damit die Adobe in die Liste der zugelassenen Datenanbieter aufgenommen und Ihr Konto zur Zulassungsliste hinzugefügt werden kann. Kontakt [!DNL Google] und geben Sie die folgenden Informationen an:

* **Konto-ID**: Kontokennung der Adobe mit Google. Konto-ID: 87933855.
* **Kunden-ID**: Kundenkonto-ID von Adobe mit Google. Kunden-ID: 89690775.
* **Netzwerkkennung**: Dies ist Ihr Konto bei [!DNL Google Ad Manager]
* **Zielgruppenverknüpfungskennung**: Dies ist Ihr Konto bei [!DNL Google Ad Manager]
* Ihr Kontotyp. DFP von Google oder AdX Buyer.

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie den gewünschten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Bucket-Name]**: den Namen der [!DNL Google Cloud Storage] -Bucket, der von diesem Ziel verwendet werden soll.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, der die exportierten Dateien hosten soll.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

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
