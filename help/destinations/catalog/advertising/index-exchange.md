---
title: Indexaustausch
description: Verbinden Sie sich mit Index Exchange (Index) und aktivieren Sie Ihre Daten, damit Ihre Zielgruppensegmente von Angeboten angesprochen werden können, die in der Index-Benutzeroberfläche erstellt wurden.
source-git-commit: 4ecd3b60a6b45a94285785049fd4dee99d7c9bdf
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 17%

---


# [!DNL Index Exchange] {#index-exchange}

## Übersicht {#overview}

[!DNL Index] ist eine globale Plattform für Werbeangebote, mit der Medieninhaber den Wert ihrer Inhalte auf jedem Bildschirm maximieren können. Mit über 20 Jahren Branchenführerschaft verbindet [!DNL Index] die weltweit größten Marken mit erstklassigen Experience Makers, um hochwertige Kundenerlebnisse zu schaffen.

Verwenden Sie diesen Ziel-Connector, um Zielgruppensegmente aus Adobe Experience Platform direkt in die programmgesteuerte Werbeplattform von [!DNL Index Exchange] zu exportieren.

Nach dem Export können diese Zielgruppensegmente verwendet werden, um Angebote von Medieninhabern und Marketplace-Partnern anzusprechen oder von Marketplace-Anbietern mit Herausgebern und Kuratoren geteilt werden.

>[!IMPORTANT]
>
>Der Ziel-Connector und die Dokumentationsseite werden vom [!DNL Index]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an [technical_am_marketplace@indexexchange.com](mailto:technical_am_marketplace@indexexchange.com).

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Index Exchange]-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Kundinnen und Kunden von Experience Platform mit diesem Ziel bewältigen können.

### Ansprechen von Benutzern auf mobilen, Web- und Videoüberwachungsplattformen {#targeting-users}

Medieneigentümer, Marketplace-Partner oder Marketplace-Anbieter, die Zielgruppen von Experience Platform an [!DNL Index] senden möchten, um Benutzende auf Mobil-, Web- und TV-Plattformen mithilfe einer großen Auswahl an Kennungen anzusprechen.

### Targeting bestimmter Inhalte auf mobilen, Web- und CTV-Plattformen {#targeting-content}

Medieninhaber, Marketplace-Partner oder Marketplace-Anbieter, die Zielgruppen von Experience Platform an [!DNL Index] senden möchten, um Benutzende anzusprechen, die bestimmte Inhalte über Mobil-, Web- und CTV-Plattformen mithilfe bestimmter URLs, App-Bundles oder Inhalts-IDs ansehen.

## Voraussetzungen {#prerequisites}

Zielgruppensegmente müssen bei [!DNL Index] über einen zusätzlichen Prozess registriert werden, wenn Sie dieses Ziel verwenden, bevor sie in Ihrem Konto angezeigt werden. Wenden Sie sich an Ihren [!DNL Index Exchange]-Kundenbetreuer, um Unterstützung bei diesem Prozess zu erhalten.

## Unterstützte Identitäten {#supported-identities}

[!DNL Index] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

Beachten Sie, dass [!DNL Index Exchange] Ziele nur einen Identitätstyp pro Upload unterstützen. Sie müssen den entsprechenden Kennungstyp bei der Konfiguration der Zieldetails angeben (siehe [&#x200B; Abschnitt „Ausfüllen der Zieldetails](#destination-details) unten).

Um mehrere Identitätstypen hochzuladen, erstellen Sie für jeden Identitätstyp separate Instanzen des [!DNL Index Exchange].

| Ziel-Identität | Beschreibung | Zu beachten |
| --- | --- | --- |
| GAID | GOOGLE ADVERTISING ID | Wenn die Quellidentität ein GAID-Namespace ist, wählen Sie GAID als Zielidentität aus. |
| IDFA | Apple-ID für Werbetreibende | Wenn Ihre Quellidentität ein IDFA-Namespace ist, wählen Sie die IDFA-Zielidentität aus. |
| Windows AID | Windows Advertising-ID | Wenn Ihre Quellidentität ein Windows AID-Namespace ist, wählen Sie die Windows AID-Zielidentität aus. |
| extern_id | Benutzerdefinierte Benutzer-IDs | Wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist, wählen Sie diese Zielidentität aus. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird erläutert, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
| --------- | ---------- | ---------- |
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
| --------- | ---------- | --------- | 
| Exporttyp | **[!UICONTROL Segment export]** | Exportiert alle Mitglieder eines Segments (Zielgruppe) mit den IDs (IDFA, GAID oder andere), die im [!DNL Index Exchange] verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Exportiert Dateien in Intervallen von 3, 6, 8, 12 oder 24 Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigung[. &#x200B;](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Ausfüllen der Zieldetails {#destination-details}

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Zieldetails](../../assets/catalog/advertising/index-exchange/destination-details.png)

* [!UICONTROL Name]: Geben Sie einen Namen ein, damit Sie dieses Ziel später leichter erkennen können.
* [!UICONTROL Description]: Geben Sie eine Beschreibung ein, die Ihnen hilft, dieses Ziel später zu identifizieren.
* [!UICONTROL Identifier Type]: Wählen Sie den vom Index bereitgestellten Kennungstyp aus, der mit der Kennung übereinstimmt, die Sie an [!DNL Index] senden. Siehe die Tabelle der unterstützten Kennungstypen unten. Wenn Sie sich nicht sicher sind, welcher Kennungstyp verwendet werden soll, wenden Sie sich an Ihren [!DNL Index]. Um mehrere Kennungstypen zu senden, erstellen Sie separate Instanzen dieses Ziels.
* [!UICONTROL Account ID]: Geben Sie Ihre [!DNL Index] Konto-ID ein. Dies ist nicht dasselbe wie Ihre Publisher-ID. Wenn Sie sich nicht sicher sind, welche ID Sie verwenden sollen, wenden Sie sich an Ihren [!DNL Index].

#### Unterstützte Kennungstypen

| Kennungstyp | Beschreibung |
|------------------ | ------------- |
| [!DNL appbundle] | Mobile-App-Bundle |
| [!DNL contentid] | Inhalts-ID |
| [!DNL deviceid] | Geräte-ID (z. B. IDFA, GAID, WAID usw.) |
| [!DNL ip] | IP-Adresse |
| [!DNL postcode] | Postleitzahl |
| [!DNL url] | Site-URL |
| [!DNL ppid_xxx] | Für PPID-Kennungen wenden Sie sich bitte an Ihren [!DNL Index Exchange]. |

{style="table-layout:auto"}

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen über den Status Ihres Datenflusses zu diesem Ziel zu erhalten. Wählen Sie einen oder mehrere Warnhinweise aus der Liste aus, um Statusbenachrichtigungen für Ihren Datenfluss zu abonnieren. Weitere Informationen finden Sie im Handbuch zum „Abonnieren [&#x200B; Warnhinweisen zu Zielen über die Benutzeroberfläche](../../ui/alerts.md).
Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[&#x200B; &#x200B;](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Auswahl der Quellfelder:

* Wählen Sie eine Kennung aus (normalerweise Namespaces wie IDFA oder einen benutzerdefinierten ID-Namespace). Dieser muss dem bei der Konfiguration des Ziels ausgewählten Kennungstyp entsprechen. Wenn Sie beispielsweise die IDFA-Kennung als Quellfeld verwenden, muss das Ziel mit dem Bezeichnungstyp „deviceId“ eingerichtet worden sein.

Auswählen der Zielfelder:

* Namen von Zielfeldern werden ignoriert und sind nicht wichtig. Dem Ziel kommt es nur auf den Typ der gesendeten Kennung an, der durch den bei der Konfiguration des Ziels ausgewählten Kennungstyp bestimmt wird.

![Zuordnen von Attributen und Identitäten](../../assets/catalog/advertising/index-exchange/identity-mapping.png)

### Registrieren von Segmenten bei [!DNL Index] {#register-segments}

Wenden Sie sich vor oder nach der Aktivierung der Daten für das Ziel an Ihren [!DNL Index], um die Segmente zu registrieren, die Sie aktivieren möchten. Ihr Support-Mitarbeiter gibt Anweisungen zur Registrierung zusätzlicher Segmentdetails, einschließlich Namen, IDs, Beschreibungen und Preisen, falls zutreffend.

## Exportierte Daten/Datenexport validieren {#exported-data}

Nach Abschluss der Registrierung stehen die Segmente für Targeting in Ihrem [!DNL Index]-Konto zur Verfügung. Um zu bestätigen, dass die Daten korrekt empfangen werden, wenden Sie sich an Ihren [!DNL Index], der Details zum Volumen der empfangenen Segmentdaten bereitstellen kann.

## Datennutzung und -Governance {#data-usage-governance}

Alle Experience Platform-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie Experience Platform Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
