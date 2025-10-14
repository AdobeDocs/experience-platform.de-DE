---
title: Kontozielgruppen für Ziele aktivieren
type: Tutorial
description: Erfahren Sie, wie Sie Konto-Zielgruppen für Ziele aktivieren
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=de#rtcdp-editions newtab=true"
badgeB2P: label="B2P-Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=de#rtcdp-editions newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: 4afb2c76f2022423e8f1fa29c91d02b43447ba90
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 7%

---

# Konto-Zielgruppen aktivieren

>[!AVAILABILITY]
>
>Die Funktion zum Aktivieren von Account-Zielgruppen für Ziele ist für Unternehmen verfügbar, die die [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b)- und [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p)-Editionen von Real-Time Customer Data Platform erwerben.

In diesem Artikel wird der Workflow erläutert, der zum Exportieren [Account-Zielgruppen](/help/segmentation/types/account-audiences.md) von Adobe Experience Platform an Ihr bevorzugtes Ziel erforderlich ist.

## Unterstützte Ziele {#supported-destinations}

Navigieren Sie zu **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]** aus. Verwenden Sie den Filter **[!UICONTROL Datentypen]** und wählen Sie **[!UICONTROL Konten]** aus, um die Ziele anzuzeigen, die die Aktivierung von Konto-Zielgruppen unterstützen. Derzeit ist der Export von Konto-Zielgruppen nur für bestimmte Cloud-Speicher-Ziele ([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Azure Blob Storage](/help/destinations/catalog/cloud-storage/azure-blob.md), [Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md) und [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)) und das [Demandbase](/help/destinations/catalog/advertising/demandbase.md) und [(Firmen) LinkedIn Matched Audiences](/help/destinations/catalog/social/linkedin-b2b.md) Streaming-Ziel verfügbar.

![Ziele, die Konto-Zielgruppen unterstützen.](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## Videoüberblick

Sehen Sie sich das folgende Video an, um einen Überblick über das Erstellen und Aktivieren von Account-Zielgruppen und die unterstützten Anwendungsfälle beim Aktivieren von Account-Zielgruppen zu erhalten.

>[!VIDEO](https://video.tv.adobe.com/v/338252/?learn=on)

## Voraussetzungen {#prerequisites}

* Sie müssen zunächst [Account-Profile](/help/rtcdp/accounts/account-profile-overview.md) aufnehmen und [Account-Zielgruppen](/help/segmentation/types/account-audiences.md) erstellen, bevor Sie sie für nachgelagerte Ziele aktivieren können.
* Um Konto-Zielgruppen für Ziele aktivieren zu können, müssen Sie erfolgreich eine Verbindung mit einem Ziel hergestellt haben. Wenn Sie es noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten. Lesen Sie das Tutorial zur Benutzeroberfläche [Herstellen einer Verbindung zu Zielen](./connect-destination.md), um weitere Informationen zu erhalten.

### Erforderliche Berechtigungen {#permissions}

Um Konto-Zielgruppen zu aktivieren, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele aktivieren]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Um sicherzustellen, dass Sie über die erforderlichen Berechtigungen zum Aktivieren von Konto-Zielgruppen verfügen, durchsuchen Sie den Zielkatalog. Wenn ein Ziel über ein **[!UICONTROL Aktivieren]**-Steuerelement verfügt, verfügen Sie über die entsprechenden Berechtigungen.

## Auswählen des Ziels {#select-destination}

Befolgen Sie die Anweisungen zum Auswählen eines Ziels, an das Sie Ihre Datensätze exportieren können:

1. Navigieren Sie zu **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]**.

   ![Registerkarte „Zielkatalog“ mit hervorgehobenem Katalog-Steuerelement.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Wählen Sie **[!UICONTROL Aktivieren]** auf der Karte aus, die dem Ziel entspricht, an das Sie Datensätze exportieren möchten.

>[!TIP]
>
>Die Ziele, die Account-Zielgruppen exportieren können, werden mit einem Symbol in der oberen rechten Ecke der Karte angezeigt, ähnlich dem unten hervorgehobenen Ziel. Alternativ können Sie den Datentypfilter verwenden, um nur Ziele anzuzeigen, die Account-Zielgruppen exportieren können, [weiter oben auf der Seite &#x200B;](#supported-destinations).

![Demandbase-Zielseite, auf der Profil-Zielgruppen exportiert werden können, hervorgehoben.](/help/destinations/assets/ui/activate-account-audiences/demandbase-icon-activate-account-audiences.png)

1. Wählen Sie **[!UICONTROL Datentypkonten]**, gefolgt von der Zielverbindung, in die Sie Datensätze exportieren möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**.

>[!TIP]
> 
>Trigger Wenn Sie ein neues Ziel zum Aktivieren von Konto-Zielgruppen einrichten möchten, wählen Sie **[!UICONTROL Neues Ziel konfigurieren]** aus, um den Workflow [Mit Ziel verbinden](/help/destinations/ui/connect-destination.md) zu und [Konten als Datentyp auswählen](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![Zielaktivierungs-Workflow mit hervorgehobenem Steuerelement „Konten“.](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. Fahren Sie mit dem nächsten Abschnitt fort[&#x200B; um Ihre Konto](#select-profile-audiences)Zielgruppen auszuwählen.

## Konto-Zielgruppen auswählen {#select-account-audiences}

Aktivieren Sie die Kontrollkästchen links neben den Namen der Konto-Zielgruppen , um die Zielgruppen auszuwählen, die Sie an das Ziel exportieren möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**. Beachten Sie, *in dieser Ansicht nur* Konto-Zielgruppen“ angezeigt werden und keine anderen Zielgruppentypen angezeigt werden.

![Workflow für den Datensatzexport, der den Schritt „Zielgruppen auswählen“ zeigt, in dem Sie auswählen können, welche Konto-Zielgruppen exportiert werden sollen.](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## Planung und nächste Schritte

Lesen Sie für den Rest des Aktivierungs-Workflows zum Exportieren von Konto-Zielgruppen das Tutorial zum Aktivieren von Daten für dateibasierte Ziele. Fahren Sie mit dem [Schritt Zielgruppenexport planen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) fort. Wenn Sie Konto-Zielgruppen für das Ziel von **[!UICONTROL (Firmen) LinkedIn Matched Audiences aktivieren,]** Sie das Tutorial zum Aktivieren von Streaming-Zielen. Fahren Sie mit dem [Zuordnungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) fort.

>[!NOTE]
>
>Beachten Sie, dass Sie im Planungsschritt beim Exportieren von Konto-Zielgruppen in Cloud-Speicher-Ziele mit dem Workflow zum Aktivieren von Konto-Zielgruppen nur [vollständige Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) und [inkrementelle Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _nach einem täglichen Zeitplan_. Stündliche Exporte werden nicht unterstützt. Beachten Sie außerdem **[!UICONTROL dass]** einzige unterstützte Auswertungstyp „Nach Zielgruppenbewertung“ ist.

## Wichtige Hinweise und bekannte Einschränkungen {#important-callouts-known-limitations}

Beachten Sie die folgenden wichtigen Hinweise und bekannten Einschränkungen für die allgemeine Verfügbarkeit der Funktion zur Aktivierung von Account-Zielgruppen.

### Erforderliche Zuordnungspaare im Zuordnungsschritt beim Aktivieren von Konto-Zielgruppen für das Ziel &quot;**[!UICONTROL (Unternehmen) LinkedIn Matched Audiences]** {#required-mappings}

Beachten Sie beim Aktivieren von Konto-Zielgruppen für das Ziel &quot;**[!UICONTROL (Unternehmen) LinkedIn Matched Audiences]**, dass die folgenden beiden Zuordnungspaare obligatorisch sind, um Daten erfolgreich zu exportieren:

![LinkedIn-Zuordnung: Erforderliche Felder.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Quellfeld | Zielfeld |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (wählen Sie dieses Feld in der Ansicht **[!UICONTROL Identity-Namespace auswählen]** bei Auswahl **[!UICONTROL Zielfeld]** aus). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Konto-Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Konto-Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"} |

### Durchsetzung von Data Governance {#data-governance-enforcement}

Das Einverständnis wird auf Personen- oder Profilebene für (Kunden- *Interessenten-Zielgruppen)*. Daher wird [Bewertung der Einverständnisrichtlinie](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) derzeit nicht unterstützt, wenn Kontozielgruppen für Ziele aktiviert werden. Im Überprüfungsschritt des Aktivierungs-Workflows wird ein ausgegrautes Steuerelement für (**[!UICONTROL Einverständnisrichtlinien anzeigen)]**.

![Überprüfungsschritt des Workflows Konto-Zielgruppen aktivieren mit ausgegrautem Steuerelement zur Einverständnisdurchsetzung.](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

Andere Data-Governance-Mechanismen in Real-Time CDP [&#x200B; z. B](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)Datenverwendungsrichtlinien-Prüfungen und [attributbasierte &#x200B;](/help/destinations/home.md#attribute-based-access)) werden unterstützt.
