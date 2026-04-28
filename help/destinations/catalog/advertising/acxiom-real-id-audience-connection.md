---
title: Acxiom Real ID&trade; Zielgruppenverbindung
description: Verwenden Sie das  [!DNL Acxiom Real ID&trade; Audience Connection] -Ziel, um Zielgruppen plattformübergreifend zu verbessern und zu aktivieren [!DNL Altice] z. B.  [!DNL Ampersand] und  [!DNL Comcast].
source-git-commit: 3aefb36bbf525a5eebe3a9330e25587501167a64
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 14%

---


# [!DNL Acxiom Real ID™ Audience Connection]

Verwenden Sie das [!DNL Acxiom Real ID Audience Connection]-Ziel, um Zielgruppen mit der [Real ID™-](https://www.acxiom.com/real-id/real-id/) von [!DNL Acxiom] zu erweitern. Aktivieren Sie diese Zielgruppen dann plattformübergreifend, z. B. für [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] und mehr.

>[!NOTE]
>
>Dieser Ziel-Connector und diese Dokumentationsseite werden vom [!DNL Acxiom]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich direkt an [!DNL Acxiom] unter [acxiom-adobe-help@acxiom.com](mailto:acxiom-adobe-help@acxiom.com).

Führen Sie die folgenden Schritte aus, um mithilfe der [!DNL Adobe Experience Platform]-Benutzeroberfläche einen [!DNL Acxiom Real ID Audience Connection]-Ziel-Connector zu erstellen. Verwenden Sie diesen Connector, um Zielgruppen zu erstellen und an ausgewählte Ziele zu verteilen.

## Anwendungsfälle {#use-cases}

Verwenden Sie dieses Ziel, wenn [!DNL Acxiom]s [!DNL Real ID] als Kennung in [!DNL Real-Time CDP] geladen haben. Die folgenden Anwendungsfälle zeigen, wie Sie das [!DNL Acxiom Real ID Audience Connection] verwenden können.

### Senden von Zielgruppen von [!DNL Experience Platform] an Ihr [!DNL Acxiom] {#send-audiences}

Verwenden Sie diesen Ziel-Connector, um Zielgruppen von [!DNL Experience Platform] zur kanalübergreifenden Akquise an Ihr [!DNL Acxiom]-Konto zu senden.

So ist beispielsweise die Marketing Operations-Abteilung einer globalen Finanzdienstleistungsmarke an einer kanalübergreifenden Kundenakquise über mehrere Werbeplattformen interessiert. Sie können den [!DNL Acxiom Real ID Audience Connection]-Ziel-Connector verwenden, um Zielgruppen von [!DNL Experience Platform] an [!DNL Acxiom] zu senden, die Zielgruppen mit der [!DNL Real ID]-Technologie von [!DNL Acxiom] zu verbessern und die Zielgruppen für mehrere Plattformen zu aktivieren, z. B. [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] und mehr.

## Voraussetzungen {#prerequisites}

Bevor Sie das [!DNL Acxiom Real ID Audience Connection]-Ziel konfigurieren, müssen Sie die folgenden Voraussetzungen erfüllen.

* **Nutzungsbedingungen bestätigen:** Lesen und Signieren der Nutzungsbedingungen von [!DNL Acxiom]. Sie erhalten den Link zum Vertrag, sobald Ihr ausgeführter Auftrag abgeschlossen ist. Bis zum Unterzeichnen der Vereinbarung wird die [!DNL Acxiom Real ID Audience Connection] Zielkarte nicht im [!DNL Experience Platform] Zielkatalog angezeigt. Nachdem Sie die Vereinbarung akzeptiert und unterzeichnet haben, schließt [!DNL Adobe] Ihre Einrichtung ab, und die [!DNL Acxiom Real ID Audience Connection] Zielkarte wird angezeigt.
* **Kennen Sie Ihre [!DNL Adobe] Organisations-ID:** Zum Ausfüllen Ihrer Nutzungsbedingungen ist Ihre [!DNL Adobe] Organisations-ID erforderlich. Weitere Informationen zum Anzeigen *Organisations-ID finden Sie unter* von [!DNL Adobe]Organisationen in [Experience Cloud](https://experienceleague.adobe.com/de/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255).
* **Erhalten einer Lizenz für das [!DNL Real ID] Produkt von [!DNL Acxiom]:** Nachdem Sie eine Lizenz erworben haben, stellen Sie die [!DNL Real ID] von [!DNL Acxiom] in [!DNL Real-Time CDP] zur Verfügung. Siehe [Acxiom Data Enhancement](/help/destinations/catalog/data-partner/acxiom-data-enhancement.md) für Details.

## Unterstützte Identitäten {#supported-identities}

Das Ziel [!DNL Real ID] Zielgruppenverbindung von [!DNL Acxiom] unterstützt die folgenden Identitätsaktivierungen. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Zielidentität | Beschreibung | Zu beachten |
| --------------- | ----------- | -------------- |
| [!DNL Real ID] | [!DNL Real ID] | Ordnen Sie dieser Zielidentität ein Quellfeld zu. Ihr Quellfeld kann entweder eine [!DNL Acxiom] [!DNL Real ID] oder eine benutzerdefinierte Kennung sein. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
| --------------- | --------- | ----------- |
| [!DNL Segmentation Service] | Ja | Zielgruppen, die über den [!DNL Experience Platform]Segmentierungs[Service) generiert ](/help/segmentation/home.md). |
| Alle anderen Ursprünge der Zielgruppe | Ja | Diese Kategorie enthält alle Ursprünge der Zielgruppe außerhalb der Zielgruppen, die durch die [!DNL Segmentation Service] generiert wurden. Lesen Sie mehr über [verschiedene Ursprünge von Audiences](/help/segmentation/ui/audience-portal.md#customize). Einige Beispiele: <ul><li>benutzerdefinierte Upload-[ (importiert](/help/segmentation/ui/audience-portal.md#import-audience) in [!DNL Experience Platform] aus CSV-Dateien,</li><li>Lookalike-Zielgruppen,</li><li>Federated Audiences,</li><li>in anderen [!DNL Experience Platform]-Apps generierte Zielgruppen wie [!DNL Adobe Journey Optimizer],</li><li>und mehr.</li></ul> |

{style="table-layout:auto"}

### Unterstützte Zielgruppen nach Datentyp {#supported-audiences-data-type}

In der folgenden Tabelle wird beschrieben, welche Zielgruppen-Datentypen Sie an dieses Ziel exportieren können.

| Datentyp der Zielgruppe | Unterstützt | Beschreibung | Anwendungsfälle |
| -------------------- | --------- | ----------- | --------- |
| [Personen-Zielgruppen](/help/segmentation/types/people-audiences.md) | Ja | Basierend auf Kundenprofilen. Verwenden Sie sie, um bestimmte Personengruppen für Marketing-Kampagnen anzusprechen. | Häufige Käufer, Warenkorbabbrüche |
| [Konto-Zielgruppen](/help/segmentation/types/account-audiences.md) | Nein | Targeting von Personen in bestimmten Organisationen für Account-basierte Marketing-Strategien. | B2B-Marketing |
| [Interessenten-Zielgruppen](/help/segmentation/types/prospect-audiences.md) | Nein | Targeting von Personen, die noch keine Kunden sind, aber Merkmale mit Ihrer Zielgruppe teilen. | Akquise mit Drittanbieterdaten |
| [Datensatzexporte](/help/catalog/datasets/overview.md) | Nein | Sammlungen strukturierter Daten, die im Data Lake von [!DNL Adobe Experience Platform] gespeichert sind. | Reporting, Datenwissenschaft-Workflows |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Die folgende Tabelle beschreibt den Zielexporttyp und die Häufigkeit des Exports.

| Element | Typ | Anmerkungen |
| ---- | ---- | ----- |
| Exporttyp | **[!UICONTROL Audience export]** | Exportiert alle Mitglieder einer Zielgruppe mit den im [!DNL Acxiom Real ID Audience Connection]-Ziel verwendeten Kennungen. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Unterstützte Ziele {#supported-destinations}

Aktivieren Sie Zielgruppen für die folgenden Plattformen über das [!DNL Acxiom Real ID Audience Connection] .

* [!DNL Altice]
* [[!DNL Amazon]](#amazon)
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL Facebook]](#facebook)
* [[!DNL LG Ads]](#lg-ads)
* [[!DNL Pinterest]](#pinterest)
* [!DNL Spectrum]
* [!DNL Viant]
* [[!DNL Vizio]](#vizio)

## Herstellen einer Verbindung mit dem Ziel {#connect}

[!DNL Experience Platform] verarbeitet die Authentifizierung für Ihr [!DNL Acxiom Real ID Audience Connection]-Ziel automatisch.

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

## Zielspezifische Einstellungen {#destination-settings}

Für einige [!DNL Acxiom Real ID Audience Connection]-Ziele sind zusätzliche Informationen erforderlich. Die folgenden Abschnitte enthalten detaillierte Anleitungen zum Konfigurieren dieser Optionen.

### [!DNL Amazon] {#amazon}

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

* **[!UICONTROL Publisher Account ID]**: Geben Sie die ID des Herausgeberkontos ein, das mit diesem Ziel verknüpft ist.

  ![Screenshot des Bedienfelds mit [!DNL Amazon] Zieldetails, auf dem das Feld für die Herausgeberkonto-ID angezeigt wird.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_amazon_destination_details.png){zoomable="yes"}

### [!DNL Facebook] {#facebook}

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

* **[!UICONTROL Destination Account ID]**: Geben Sie die Zielkonto-ID für dieses Ziel ein.

  ![Screenshot des Bedienfelds [!DNL Facebook] Zieldetails mit dem Feld „Zielkonto-ID“.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_facebook_destination_details.png){zoomable="yes"}

### [!DNL LG Ads] {#lg-ads}

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

* **[!UICONTROL Segment Category]**: Die Zielkategorie oder die Vertikale, in die Ihr Segment fällt. Beispiel: Finanzdienstleistungen, Automobil oder Gesundheit.

  ![Screenshot des Bedienfelds [!DNL LG Ads] Zieldetails mit dem Feld „Segmentkategorie“.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_lg_ads_destination_details.png){zoomable="yes"}

### [!DNL Pinterest] {#pinterest}

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

* **[!UICONTROL Destination Account ID]**: Geben Sie die Zielkonto-ID für dieses Ziel ein.

  ![Screenshot des Bedienfelds [!DNL Pinterest] Zieldetails mit dem Feld „Zielkonto-ID“.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_pinterest_destination_details.png){zoomable="yes"}

### [!DNL Vizio] {#vizio}

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

* **[!UICONTROL Advertiser Name]**: Geben Sie den Namen des Advertisers für dieses Ziel ein.

  ![Screenshot des Bedienfelds mit [!DNL Vizio] Zieldetails, auf dem das Feld „Advertiser-Name“ angezeigt wird.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_vizio_destination_details.png){zoomable="yes"}

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md).

>[!IMPORTANT]
>
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png){width="100" zoomable="yes"}

>[!NOTE]
>
>Das [!DNL Acxiom Real ID Audience Connection] unterstützt nur vollständige Dateiexporte.

### Zuordnen von Attributen und Identitäten {#map}

Damit das [!DNL Acxiom Real ID Audience Connection] Ziel die Zielgruppendaten korrekt erhält, ordnen Sie das Quellfeld von [!DNL Experience Platform] dem richtigen [!DNL Acxiom Real ID Audience Connection] Zielfeld zu.

Das **[!UICONTROL Real ID]** Zielfeld wird im Zuordnungsschritt automatisch vorausgefüllt. Ordnen Sie Ihr Quellfeld zu: Entweder ein benutzerdefinierter Namespace für die Kennung oder ein tatsächlicher [!DNL Acxiom] [!DNL Real ID] in Ihrem Profilschema gespeichert.

| Feldname | Beschreibung | Erforderlich |
| ---------- | ----------- | -------- |
| [!DNL Real ID] | Ein [!DNL Real ID] ist eine eindeutige alphanumerische Kennung mit 36 Byte aus dem proprietären Identitätsauflösungsdiagramm von [!DNL Acxiom]. Dabei handelt es sich um eine Kennung, die eine Person, einen Haushalt oder eine Adresse repräsentiert. | Ja |

{style="table-layout:auto"}

Geben Sie in der Spalte **[!UICONTROL Source Field]** den Namen des Quellattributs ein, das Sie dem **[!UICONTROL Real ID]** Zielfeld zuordnen möchten. Oder wählen Sie **[!UICONTROL Select source field]** aus, um verfügbare Quellfelder zu durchsuchen. Wählen Sie dann **[!UICONTROL Next]** aus.

![Screenshot des Zuordnungsbildschirms mit der [!UICONTROL Source Field] und dem [!UICONTROL Select source field] Panel.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_mapping_screen.png){zoomable="yes"}

Wenn Sie das Standardschema von [!DNL Adobe] nicht verwenden, finden Sie weitere Informationen im [Handbuch zur Query Service-](/help/query-service/ui/overview.md)), um das [!DNL Adobe] Standardschema mit Ihren Feldnamen zu füllen.

### Überprüfen Ihres Ziels {#review}

Überprüfen Sie nach Abschluss aller Schritte den Status Ihrer Zielverbindung und die Details Ihrer Zielgruppe, bevor Sie sie aktivieren. Die ausgewählten Zielgruppen werden in einer Liste angezeigt. Jede Zielgruppe ist ein separater Aufruf der [!DNL Acxiom Real ID Audience Connection]-API.

Wenn die Ergebnisse korrekt aussehen, wählen Sie **[!UICONTROL Finish]** aus, um Ihr Ziel zu aktivieren.

![Screenshot des Bildschirms Überprüfung mit dem Status der Zielverbindung und den ausgewählten Zielgruppen vor der Aktivierung.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_review_audience.png){zoomable="yes"}

## Fehlerbehebung {#troubleshooting}

Wenn Ihr Zielvertreter Ihre Zielgruppe nicht finden kann, wenden Sie sich an Ihren [!DNL Adobe].

Geben Sie die folgenden Informationen an Ihren [!DNL Adobe] weiter:

* Zielgruppenname
* Name des Ziels
* Datum der Zielgruppenaktivierung
* Name der exportierten Datei

## Nächste Schritte {#next-steps}

Sie haben eine Zielgruppe erfolgreich für die ausgewählte Zielplattform aktiviert. Wenden Sie sich anschließend an den für Ihre Zielplattform zuständigen Support, um mit der Einrichtung Ihrer Kampagne zu beginnen.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
