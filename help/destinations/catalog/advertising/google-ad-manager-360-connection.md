---
title: (Beta)  [!DNL Google Ad Manager 360] -Verbindung
description: Google Ad Manager 360 ist eine Adserving-Plattform von Google, die Publishern die Möglichkeit gibt, das Anzeigen von Werbung auf ihren Websites, über Videos und in Mobile Apps zu verwalten.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: 21b76877e8b36d6b844d9c0726a2347b1fab170e
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 60%

---

# (Beta) [!DNL Google Ad Manager 360]-Verbindung

>[!IMPORTANT]
>
> Google veröffentlicht Änderungen an der [Google Ads API](https://developers.google.com/google-ads/api/docs/start), der [Kundenabgleich](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) und der [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview), um die Compliance- und Zustimmungsanforderungen zu unterstützen, die im [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) in der Europäischen Union ([EU-Benutzerzustimmungsrichtlinie](https://www.google.com/about/company/user-consent-policy/)) definiert sind. Die Durchsetzung dieser Änderungen an den Zustimmungsanforderungen ist ab 6. März 2024 verfügbar.
><br/>
>Um die EU-Politik zur Einwilligung von Nutzern einzuhalten und im Europäischen Wirtschaftsraum (EWR) weiterhin Zielgruppenlisten für Benutzer zu erstellen, müssen Werbetreibende und Partner sicherstellen, dass sie beim Hochladen von Zielgruppendaten die Einwilligung der Endnutzer weitergeben. Als Google-Partner bietet Ihnen Adobe die nötigen Tools, um diese Zustimmungsanforderungen gemäß DMA in der Europäischen Union zu erfüllen.
><br/>
>Kunden, die Adobe Privacy &amp; Security Shield erworben und eine [Zustimmungsrichtlinie](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) konfiguriert haben, um Profile ohne Zustimmung herauszufiltern, müssen keine Maßnahmen ergreifen.
><br/>
>Kunden, die keine Adobe Privacy &amp; Security Shield erworben haben, müssen die Funktion [Segmentdefinition](../../../segmentation/home.md#segment-definitions) in [Segment Builder](../../../segmentation/ui/segment-builder.md) verwenden, um Profile ohne Zustimmung herauszufiltern, damit sie die bestehenden Real-Time CDP Google-Ziele ohne Unterbrechung weiterhin verwenden können.

Die [!DNL Google Ad Manager 360]-Verbindung aktiviert den Batch-Upload für [!DNL publisher provided identifiers] (PPID) in [!DNL Google Ad Manager 360] über [!DNL Google Cloud Storage].

Weitere Informationen dazu, wie vom Publisher bereitgestellte IDs in Google Ad Manager 360 funktionieren, finden Sie in der [offiziellen Google-Dokumentation](https://support.google.com/admanager/answer/2880055?hl=de).

>[!IMPORTANT]
>
>Diese Funktion befindet sich derzeit in der Beta-Phase und steht nur einer bestimmten Anzahl von Kunden zur Verfügung. Um Zugang zur [!DNL Google Ad Manager 360]-Verbindung zu erhalten, wenden Sie sich an Ihre Kontaktperson beim Adobe-Support-Mitarbeiter und geben Sie Ihre [!DNL organization ID] an.

Das [!DNL Google Ad Manager 360]-Ziel exportiert [!DNL CSV]-Dateien zu Ihrem [!DNL Google Cloud Storage]-Behälter. Nachdem Sie die [!DNL CSV]-Dateien exportiert haben, müssen Sie sie in Ihr [!DNL Google Ad Manager 360]-Konto importieren.

## Zielspezifikationen {#specifics}

Beachten Sie folgende Details, die speziell für [!DNL Google Ad Manager 360]-Ziele gelten.

* Die Funktion [Dateien On-Demand exportieren](../../ui/export-file-now.md) wird von diesem Ziel derzeit nicht unterstützt.
* Aktivierte Zielgruppen werden programmgesteuert in der Google-Plattform erstellt und in die CSV-Datei eingefügt.

## Unterstützte Identitäten {#supported-identities}

[!DNL This integration] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Wählen Sie diese Zielidentität aus, um Zielgruppen an [!DNL Google Ad Manager 360] zu senden. |

{style="table-layout:auto"}

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

## Voraussetzungen {#prerequisites}

### Zulassungsauflistung {#allow-listing}

Die Zulassungsauflistung ist obligatorisch, bevor Sie Ihr erstes [!DNL Google Ad Manager 360]-Ziel in Platform einrichten. Stellen Sie sicher, dass Sie den unten beschriebenen Zulassungsauflistungsprozess abgeschlossen haben, bevor Sie Ihr Ziel erstellen.

>[!NOTE]
>
>Die Ausnahme von dieser Regel betrifft bestehende [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=de) -Kunden. Wenn Sie bereits eine Verbindung zu diesem Google-Ziel in Audience Manager erstellt haben, ist es nicht erforderlich, den Zulassungsauflistungsprozess erneut zu durchlaufen. Sie können mit den nächsten Schritten fortfahren.

1. Führen Sie die in der Dokumentation zu Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=de) beschriebenen Schritte aus, um Adobe als verknüpfte Data Management Platform (DMP) hinzuzufügen.[
2. Wechseln Sie in der Benutzeroberfläche von [!DNL Google Ad Manager] zu **[!UICONTROL Admin]** > **[!UICONTROL Globale Einstellungen]** > **[!UICONTROL Netzwerkeinstellungen]** und aktivieren Sie den Regler **[!UICONTROL API-Zugriff]** .


## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=de) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

* **[!UICONTROL Zugriffsschlüssel-ID]**: Eine 61-stellige alphanumerische Zeichenfolge, die zur Authentifizierung Ihres [!DNL Google Cloud Storage]-Kontos bei Platform verwendet wird.
* **[!UICONTROL Geheimer Zugriffsschlüssel]**: Eine mit Base64 verschlüsselte Zeichenfolge mit 40 Zeichen, die zum Authentifizieren Ihres [!DNL Google Cloud Storage]-Kontos bei Platform verwendet wird.

Weitere Informationen zu diesen Werten finden Sie im Handbuch [HMAC-Schlüssel für Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Anweisungen zum Generieren Ihrer eigenen Zugriffsschlüssel-ID und Ihres geheimen Zugriffsschlüssels finden Sie in der [[!DNL Google Cloud Storage] Übersicht zu Quellen](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="Anhängen der Zielgruppen-ID an Zielgruppennamen"
>abstract="Wählen Sie diese Option aus, damit der Zielgruppenname an diesem Speicherort die Zielgruppen-ID aus Experience Platform wie folgt enthält: `Audience Name (Audience ID)`"

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, in dem die exportierten Dateien gespeichert werden.
* **[!UICONTROL Behältername]**: Geben Sie den Namen des [!DNL Google Cloud Storage]-Behälters ein, der von diesem Ziel verwendet werden soll.
* **[!UICONTROL Konto-ID]**: Geben Sie Ihren [!DNL Audience Link ID] aus Ihrem [!DNL Google]-Konto ein. Dies ist eine bestimmte Kennung, die mit Ihrem [!DNL Google Ad Manager] -Netzwerk (nicht Ihrem [!DNL Network code]) verknüpft ist. Sie finden dies unter **[!UICONTROL Admin > Globale Einstellungen]** in der Benutzeroberfläche [!DNL Google Ad Manager] .
* **[!UICONTROL Kontotyp]**: Wählen Sie je nach Ihrem [!DNL Google]-Konto eine Option aus:
   * Verwenden von `AdX buyer` für [!DNL Google AdX]
   * Verwenden von `DFP by Google` für [!DNL DoubleClick] for Publishers
* **[!UICONTROL Zielgruppen-ID an Zielgruppennamen anhängen]**: Wählen Sie diese Option aus, damit der Zielgruppenname in Google Ad Manager 360 die Zielgruppen-ID von Experience Platform wie folgt enthält: `Audience Name (Audience ID)`.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profilexportziele](../../ui/activate-batch-profile-destinations.md) .

Im Schritt zur Identitätszuordnung sehen Sie die folgenden vorausgefüllten Zuordnungen:

| Vorausgefüllte Zuordnung | Beschreibung |
|---------|----------|
| `ECID` -> `ppid` | Dies ist die einzige vorausgefüllte Zuordnung, die von Benutzenden bearbeitet werden kann. Sie können beliebige Attribute oder Identitäts-Namespaces aus Platform auswählen und sie `ppid` zuordnen. |
| `metadata.segment.alias` -> `list_id` | Ordnet Experience Platform-Zielgruppennamen Zielgruppen-IDs in der Google-Plattform zu. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Teilt der Google-Plattform mit, wann disqualifizierte Benutzende aus Segmenten entfernt werden sollen. |

Diese Zuordnungen sind erforderlich für [!DNL Google Ad Manager 360] und werden von Adobe Experience Platform automatisch für alle [!DNL Google Ad Manager 360]-Verbindungen erstellt.

![Abbildung der Benutzeroberfläche mit dem Zuordnungsschritt für Google Ad Manager 360.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Exportierte Daten {#exported-data}

Um festzustellen, ob die Daten erfolgreich exportiert wurden, überprüfen Sie Ihren [!DNL Google Cloud Storage]-Behälter und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.

## Fehlerbehebung {#troubleshooting}

Sollten bei der Verwendung dieses Ziels Fehler auftreten und Sie sich an Adobe oder Google wenden müssen, halten Sie die folgenden IDs bereit.

Dies sind Adobe-Google-Konto-IDs:

* **[!UICONTROL Konto-ID]**: 87933855
* **[!UICONTROL Kunden-ID]**: 89690775