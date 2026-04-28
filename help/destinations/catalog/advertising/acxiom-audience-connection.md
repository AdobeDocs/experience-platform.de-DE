---
title: Verbindung mit Acxiom-Zielgruppe
description: Verwenden Sie das  [!DNL Acxiom Audience Connection] -Ziel, um Zielgruppen mit  [!DNL Acxiom]'s [!DNL Real ID] -Technologie anzureichern und sie über Anzeigenplattformen hinweg zu aktivieren.
source-git-commit: 71e655be2bdae3c89bd1652e2f83ab7bcc8c18fa
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 16%

---


# [!DNL Acxiom Audience Connection]

Verwenden Sie das [!DNL Acxiom Audience Connection]-Ziel, um Zielgruppen mit der [Real ID™-](https://www.acxiom.com/real-id/real-id/) von [!DNL Acxiom] zu erweitern. Aktivieren Sie diese Zielgruppen dann plattformübergreifend, z. B. für [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] und mehr.

>[!NOTE]
>
>Dieser Ziel-Connector und diese Dokumentationsseite werden vom [!DNL Acxiom]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich direkt an [!DNL Acxiom] unter [acxiom-adobe-help@acxiom.com](mailto:acxiom-adobe-help@acxiom.com).

Führen Sie die folgenden Schritte aus, um mithilfe der [!DNL Adobe Experience Platform]-Benutzeroberfläche einen [!DNL Acxiom Audience Connection]-Ziel-Connector zu erstellen. Verwenden Sie diesen Connector, um Zielgruppen zu erstellen und an ausgewählte Ziele zu verteilen.

## Anwendungsfälle {#use-cases}

Die folgenden Anwendungsfälle zeigen, wie Sie das [!DNL Acxiom Audience Connection] verwenden.

### Senden von Zielgruppen von [!DNL Experience Platform] an Ihr [!DNL Acxiom] {#send-audiences}

Verwenden Sie diesen Ziel-Connector, um Zielgruppen von [!DNL Experience Platform] zur kanalübergreifenden Akquise an Ihr [!DNL Acxiom]-Konto zu senden.

So ist beispielsweise die Marketing Operations-Abteilung einer globalen Finanzdienstleistungsmarke an einer kanalübergreifenden Kundenakquise über mehrere Werbeplattformen interessiert. Sie können den [!DNL Acxiom Audience Connection]-Ziel-Connector verwenden, um Zielgruppen von [!DNL Experience Platform] an [!DNL Acxiom] zu senden, die Zielgruppen mit der [!DNL Real ID]-Technologie von [!DNL Acxiom] zu verbessern und die Zielgruppen für mehrere Plattformen zu aktivieren, z. B. [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] und mehr.

## Voraussetzungen {#prerequisites}

Bevor Sie das [!DNL Acxiom Audience Connection]-Ziel konfigurieren, müssen Sie die folgenden Voraussetzungen erfüllen.

* **Nutzungsbedingungen bestätigen:** Lesen und Signieren der Nutzungsbedingungen von [!DNL Acxiom]. Sie erhalten den Link zum Vertrag, sobald Ihr ausgeführter Auftrag abgeschlossen ist. Bis zum Unterzeichnen der Vereinbarung wird die [!DNL Acxiom Audience Connection] Zielkarte nicht im [!DNL Experience Platform] Zielkatalog angezeigt. Nachdem Sie die Vereinbarung akzeptiert und unterzeichnet haben, schließt [!DNL Adobe] Ihre Einrichtung ab, und die [!DNL Acxiom Audience Connection] Zielkarte wird angezeigt.
* **Kennen Sie Ihre [!DNL Adobe] Organisations-ID:** Zum Ausfüllen Ihrer Nutzungsbedingungen ist Ihre [!DNL Adobe] Organisations-ID erforderlich. Weitere Informationen zum Anzeigen *Organisations-ID finden Sie unter* von [!DNL Adobe]Organisationen in [Experience Cloud](https://experienceleague.adobe.com/de/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
| --------- | ---------- | ---------- |
| [!DNL Segmentation Service] | Ja | Zielgruppen, die über den [!DNL Experience Platform]Segmentierungs[Service) generiert ](/help/segmentation/home.md). |
| Alle anderen Ursprünge der Zielgruppe | Ja | Diese Kategorie enthält alle Ursprünge der Zielgruppe außerhalb der Zielgruppen, die durch die [!DNL Segmentation Service] generiert wurden. Lesen Sie mehr über [verschiedene Ursprünge von Audiences](/help/segmentation/ui/audience-portal.md#customize). Einige Beispiele: <ul><li>benutzerdefinierte Upload-[ (importiert](/help/segmentation/ui/audience-portal.md#import-audience) in [!DNL Experience Platform] aus CSV-Dateien,</li><li>Lookalike-Zielgruppen,</li><li>Federated Audiences,</li><li>in anderen [!DNL Experience Platform]-Apps generierte Zielgruppen wie [!DNL Adobe Journey Optimizer],</li><li>und mehr.</li></ul> |

{style="table-layout:auto"}

### Unterstützte Zielgruppen nach Datentyp {#supported-audiences-data-type}

In der folgenden Tabelle wird beschrieben, welche Zielgruppen-Datentypen Sie an dieses Ziel exportieren können.

| Datentyp der Zielgruppe | Unterstützt | Beschreibung | Anwendungsfälle |
| -------------------- | ----------- | ------------- | ----------- |
| [Personen-Zielgruppen](/help/segmentation/types/people-audiences.md) | Ja | Basierend auf Kundenprofilen. Verwenden Sie sie, um bestimmte Personengruppen für Marketing-Kampagnen anzusprechen. | Häufige Käufer, Warenkorbabbrüche |
| [Konto-Zielgruppen](/help/segmentation/types/account-audiences.md) | Nein | Targeting von Personen in bestimmten Organisationen für Account-basierte Marketing-Strategien. | B2B-Marketing |
| [Interessenten-Zielgruppen](/help/segmentation/types/prospect-audiences.md) | Nein | Targeting von Personen, die noch keine Kunden sind, aber Merkmale mit Ihrer Zielgruppe teilen. | Akquise mit Drittanbieterdaten |
| [Datensatzexporte](/help/catalog/datasets/overview.md) | Nein | Sammlungen strukturierter Daten, die im Data Lake von [!DNL Adobe Experience Platform] gespeichert sind. | Reporting, Datenwissenschaft-Workflows |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Die folgende Tabelle beschreibt den Zielexporttyp und die Häufigkeit des Exports.

| Element | Typ | Anmerkungen |
| ---- | ---- | ----- |
| Exporttyp | **[!UICONTROL Audience export]** | Exportiert alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder sonstiges), die im [!DNL Acxiom Audience Connection] verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Unterstützte Ziele {#supported-destinations}

Aktivieren Sie Zielgruppen für die folgenden Plattformen über das [!DNL Acxiom Audience Connection] .

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

[!DNL Experience Platform] verarbeitet die Authentifizierung für Ihr [!DNL Acxiom Audience Connection]-Ziel automatisch.

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

## Zielspezifische Einstellungen {#destination-settings}

Für einige [!DNL Acxiom Audience Connection]-Ziele sind zusätzliche Informationen erforderlich. Die folgenden Abschnitte enthalten detaillierte Anleitungen zum Konfigurieren dieser Optionen.

### [!DNL Amazon] {#amazon}

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

* **[!UICONTROL Publisher Account ID]**: Geben Sie die ID des Herausgeberkontos ein, das mit diesem Ziel verknüpft ist.

  ![Screenshot des Bedienfelds mit [!DNL Amazon] Zieldetails, auf dem das Feld für die Herausgeberkonto-ID angezeigt wird.](../../assets/catalog/advertising/acxiom-audience-distribution/amazon_destination_details.png){zoomable="yes"}

### [!DNL Facebook] {#facebook}

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

* **[!UICONTROL Destination Account ID]**: Geben Sie die Zielkonto-ID für dieses Ziel ein.

  ![Screenshot des Bedienfelds [!DNL Facebook] Zieldetails mit dem Feld „Zielkonto-ID“.](../../assets/catalog/advertising/acxiom-audience-distribution/facebook_destination_details.png){zoomable="yes"}

### [!DNL LG Ads] {#lg-ads}

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

* **[!UICONTROL Segment Category]**: Die Zielkategorie oder die Vertikale, in die Ihr Segment fällt. Beispiel: Finanzdienstleistungen, Automobil oder Gesundheit.

  ![Screenshot des Bedienfelds [!DNL LG Ads] Zieldetails mit dem Feld „Segmentkategorie“.](../../assets/catalog/advertising/acxiom-audience-distribution/lg_ads_destination_details.png){zoomable="yes"}

### [!DNL Pinterest] {#pinterest}

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

* **[!UICONTROL Destination Account ID]**: Geben Sie die Zielkonto-ID für dieses Ziel ein.

  ![Screenshot des Bedienfelds [!DNL Pinterest] Zieldetails mit dem Feld „Zielkonto-ID“.](../../assets/catalog/advertising/acxiom-audience-distribution/pinterest_destination_details.png){zoomable="yes"}

### [!DNL Vizio] {#vizio}

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

* **[!UICONTROL Advertiser Name]**: Geben Sie den Namen des Advertisers für dieses Ziel ein.

  ![Screenshot des Bedienfelds mit [!DNL Vizio] Zieldetails, auf dem das Feld „Advertiser-Name“ angezeigt wird.](../../assets/catalog/advertising/acxiom-audience-distribution/vizio_destination_details.png){zoomable="yes"}

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md).

>[!IMPORTANT]
>
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png){width="100" zoomable="yes"}

>[!NOTE]
>
>Das [!DNL Acxiom Audience Connection] unterstützt nur vollständige Dateiexporte.

### Zuordnen von Attributen und Identitäten {#map}

Um Zielgruppendaten korrekt zu empfangen, ordnen Sie die Quellfelder von [!DNL Experience Platform] den richtigen [!DNL Acxiom Audience Connection] Zielfeldern zu.

Die folgenden Zielfelder werden automatisch in der [!DNL Acxiom] erforderlichen Reihenfolge vorausgefüllt. Sie müssen jedem Zielfeld ein Quellfeld zuordnen, um den Aktivierungsfluss abzuschließen.

>[!IMPORTANT]
>
>Alle Zielfelder müssen in der Benutzeroberfläche zugeordnet werden. Allerdings benötigen nur **[!UICONTROL Last Name]**, **[!UICONTROL Address Line 1]**, **[!UICONTROL City]**, **[!UICONTROL State]** und **[!UICONTROL Zip Code]** tatsächliche Daten in Ihrem Profilschema. Ordnen Sie jedes verfügbare Quellfeld den verbleibenden Zielfeldern zu, um die Benutzeroberflächenanforderung zu erfüllen.

| Feldname | Beschreibung | Für die Benutzeroberfläche erforderlich | Für die Verarbeitung erforderliche Daten | Reihenfolge der Felder | Max. Länge |
| -------------------- | ------------ | ------------------ | ---------------------------- | ----------- | ---------- |
| Vorname | Vorname der Person | Ja | Nein | 1 | 255 |
| Mitte | Zweiter Vorname oder Initiale der Person | Ja | Nein | 2 | 50 |
| Nachname | Nachname der Einzelperson | Ja | **Ja** | 3 | 255 |
| Generationssuffix | Suffix des Individuums | Ja | Nein | 4 | 10 |
| Adresszeile 1 | Adresse 1 Feld des Hauptwohnsitzes | Ja | **Ja** | 5 | 255 |
| Adresszeile 2 | Adresse 2 Feld des Erstwohnsitzes | Ja | Nein | 6 | 255 |
| Stadt | Stadt mit Erstwohnsitz | Ja | **Ja** | 7 | 255 |
| Land | Landesabkürzung für Hauptwohnsitz | Ja | **Ja** | 8 | 2 |
| Postleitzahl | Postleitzahl des Hauptwohnsitzes | Ja | **Ja** | 9 | 10 |
| E-Mail | Primäre E-Mail. Standardmäßig wird dieses Feld als Deduplizierungsschlüssel verwendet, um die Datensätze eindeutig zu machen. | Ja | Nein | 10 | 255 |
| Telefon | Telefonnummer der Person (Vorwahl + Nummer). Standardmäßig wird dieses Feld als Deduplizierungsschlüssel verwendet, um die Datensätze eindeutig zu machen. | Ja | Nein | 11 | 10 |

{style="table-layout:auto"}

Geben Sie in der Spalte **[!UICONTROL Source Field]** den Namen jedes Quellattributs ein, das Sie dem entsprechenden Zielfeld zuordnen möchten. Oder wählen Sie **[!UICONTROL Select source field]** aus, um verfügbare Quellfelder zu durchsuchen.

![Zuordnungsbildschirm, der die Spalten der Quell- und Zielfelder mit den Pflichtfeldern von [!DNL Acxiom] anzeigt, die für das [!DNL Acxiom Audience Connection]-Ziel vorausgefüllt sind.](../../assets/catalog/advertising/acxiom-audience-distribution/mapping_screen.png){zoomable="yes"}

Nachdem Sie alle Felder zugeordnet haben, wählen Sie **[!UICONTROL Next]** aus.

Informationen zur Verwendung eines nicht standardmäßigen Schemas finden Sie im [Handbuch zur Query Service-](/help/query-service/ui/overview.md)), um Ihre Feldnamen dem [!DNL Adobe] Standardschema zuzuordnen.

### Überprüfen Ihres Ziels {#review}

Überprüfen Sie nach Abschluss aller Schritte den Status Ihrer Zielverbindung und die Details Ihrer Zielgruppe, bevor Sie sie aktivieren. Die ausgewählten Zielgruppen werden in einer Liste angezeigt. Jede Zielgruppe ist ein separater Aufruf der [!DNL Acxiom Audience Connection]-API.

Wenn Sie mit den Ergebnissen zufrieden sind, wählen Sie **[!UICONTROL Finish]** aus, um Ihr Ziel zu aktivieren.

![Überprüfen Sie Ihren Zielgruppenbildschirm mit dem Status der Zielverbindung und den ausgewählten Zielgruppen.](../../assets/catalog/advertising/acxiom-audience-distribution/review_audience.png){zoomable="yes"}

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
