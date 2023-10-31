---
title: Kontozielgruppen für Ziele aktivieren
type: Tutorial
description: Erfahren Sie, wie Sie Kontozielgruppen für Ziele aktivieren.
badgeLimitedAvailability: label="Eingeschränkte Verfügbarkeit" type="Caution"
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: 0a572c5fe612b8e0cc866b4e2287ea53a4022b1a
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 10%

---

# Kontozielgruppen aktivieren

>[!AVAILABILITY]
>
>Die Funktion zum Aktivieren von Kontozielgruppen für Ziele ist nur im Abschnitt [B2B Edition von Real-time Customer Data Platform](../../rtcdp/b2b-overview.md). Darüber hinaus befindet sich die Funktion für die Zielgruppe von Konten derzeit in **begrenzte Verfügbarkeit**. Wenden Sie sich an die Adobe-Kundenunterstützung oder Ihren Adobe-Support-Mitarbeiter, um Zugriff auf diese Funktion anzufordern.

In diesem Artikel wird der Workflow erläutert, der zum Exportieren erforderlich ist [Kontozielgruppen](/help/segmentation/ui/account-audiences.md) von Adobe Experience Platform zu Ihrem bevorzugten Ziel.

## Unterstützte Ziele {#supported-destinations}

Navigieren Sie zu **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]** aus. Verwenden Sie die **[!UICONTROL Datentypen]** filtern und auswählen **[!UICONTROL Konten]** um die Ziele anzuzeigen, die die Aktivierung von Kontozielgruppen unterstützen. Derzeit ist der Export von Kontozielgruppen nur für bestimmte Cloud-Speicher-Ziele verfügbar ([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Azure Blob Storage](/help/destinations/catalog/cloud-storage/azure-blob.md), [Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md), und [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)) und der [(Unternehmen) LinkedIn Matched Audiences](/help/destinations/catalog/social/linkedin.md) Ziel.

![Ziele, die Kontozielgruppen unterstützen.](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## Voraussetzungen {#prerequisites}

* Du musst zuerst aufnehmen [Kontoprofile](/help/rtcdp/accounts/account-profile-overview.md) und erstellen [Kontozielgruppen](/help/segmentation/ui/account-audiences.md) bevor Sie sie für nachgelagerte Ziele aktivieren können.
* Um Kontozielgruppen für Ziele zu aktivieren, müssen Sie eine erfolgreiche Verbindung zu einem Ziel hergestellt haben. Wenn Sie es noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten. Tutorial zur Benutzeroberfläche lesen [Verbindung zu Zielen](./connect-destination.md) für weitere Informationen.

### Erforderliche Berechtigungen {#permissions}

Um Kontozielgruppen zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Um sicherzustellen, dass Sie über die erforderlichen Berechtigungen zum Aktivieren von Kontozielgruppen verfügen, durchsuchen Sie den Zielkatalog. Wenn ein Ziel **[!UICONTROL Aktivieren]** und Sie über die entsprechenden Berechtigungen verfügen.

## Auswählen des Ziels {#select-destination}

Befolgen Sie die Anweisungen zum Auswählen eines Ziels, an das Sie Ihre Datensätze exportieren können:

1. Navigieren Sie zu **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]**.

   ![Registerkarte „Zielkatalog“ mit hervorgehobenem Katalog-Steuerelement.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Auswählen **[!UICONTROL Aktivieren]** auf der Karte, die dem Ziel entspricht, an das Sie Datensätze exportieren möchten.

>[!TIP]
>
>Die Ziele, die Zielgruppen von Konten exportieren können, werden mit einem Symbol oben rechts auf der Karte angezeigt, das dem unten hervorgehobenen Ziel ähnelt. Alternativ können Sie den Datentypfilter verwenden, um nur Ziele anzuzeigen, die Zielgruppen von Konten exportieren können, wie z. B. [höher auf der Seite angezeigt](#supported-destinations).

![Amazon S3-Zielseite, die hervorgehobene Profilzielgruppen exportieren kann.](/help/destinations/assets/ui/activate-account-audiences/amazon-s3-icon-activate-account-audiences.png)

1. Auswählen **[!UICONTROL Datentypkonten]**, gefolgt von der Zielverbindung, in die Sie Datensätze exportieren möchten, und wählen Sie **[!UICONTROL Nächste]**.

>[!TIP]
> 
>Wenn Sie ein neues Ziel einrichten möchten, um Kontozielgruppen zu aktivieren, wählen Sie **[!UICONTROL Neues Ziel konfigurieren]** zum Trigger [Mit Ziel verbinden](/help/destinations/ui/connect-destination.md) Arbeitsablauf und [Konten als Datentyp auswählen](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![Zielaktivierungs-Workflow mit hervorgehobener Kontosteuerung.](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. Fahren Sie mit dem nächsten Abschnitt fort, um [Zielgruppen Ihres Kontos auswählen](#select-profile-audiences) für den Export.

## Zielgruppen für Ihr Konto auswählen {#select-account-audiences}

Aktivieren Sie die Kontrollkästchen links neben den Namen der Zielgruppen des Kontos, um die Zielgruppen auszuwählen, die Sie zum Ziel exportieren möchten, und wählen Sie **[!UICONTROL Nächste]**. Beachten Sie, dass nur *Kontozielgruppen* werden in dieser Ansicht angezeigt und es werden keine anderen Zielgruppentypen angezeigt.

![Workflow für den Datensatzexport , der den Schritt Zielgruppen auswählen zeigt, in dem Sie auswählen können, welche Zielgruppen exportiert werden sollen.](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## Planung und nächste Schritte

Den Rest des Aktivierungs-Workflows zum Exportieren von Kontozielgruppen finden Sie im Tutorial zum Aktivieren von Daten für dateibasierte Ziele. Fahren Sie mit dem [Schritt zum Planen des Zielgruppenexports](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling). Wenn Sie Kontozielgruppen für die **[!UICONTROL (Unternehmen) LinkedIn Matched Audiences]** Ziel, lesen Sie das Tutorial zum Aktivieren von Streaming-Zielen. Fahren Sie mit dem [Zuordnungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

>[!NOTE]
>
>Beachten Sie, dass im Planungsschritt beim Export von Kontozielgruppen in Cloud-Speicher-Ziele der Workflow zum Aktivieren von Kontozielgruppen nur den Export von Zielgruppen ermöglicht [Vollständige Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) und [inkrementelle Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _auf Tagesplan_. Stündliche Exporte werden nicht unterstützt. Beachten Sie auch Folgendes: **[!UICONTROL Nach Zielgruppenbewertung]** ist der einzige unterstützte Auswertungstyp.

## Wichtige Hinweise und bekannte Einschränkungen {#important-callouts-known-limitations}

Beachten Sie die folgenden wichtigen Hinweisen und bekannten Einschränkungen für die eingeschränkte Verfügbarkeit der Funktion zum Aktivieren von Kontozielgruppen.

### Erforderliche Zuordnungspaare im Zuordnungsschritt bei der Aktivierung von Kontozielgruppen für die **[!UICONTROL (Unternehmen) LinkedIn Matched Audiences]** Ziel {#required-mappings}

Beim Aktivieren von Kontozielgruppen für die **[!UICONTROL (Unternehmen) LinkedIn Matched Audiences]** Ziel angeben, beachten Sie, dass die folgenden beiden Zuordnungspaare für den erfolgreichen Export von Daten obligatorisch sind:

![Für die linkedIn-Zuordnung sind erforderliche Felder erforderlich.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Quellfeld | Zielfeld |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (Wählen Sie dieses Feld im **[!UICONTROL Identitäts-Namespace auswählen]** Ansicht bei Auswahl der **[!UICONTROL Zielfeld]**). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Kontozielgruppen für Ziele zu aktivieren.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Kontozielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"} |

### Data Governance-Durchsetzung {#data-governance-enforcement}

Die Zustimmung wird auf der Personen- oder Profilebene für *Kunden- und Interessensgruppen*. Daher  [Bewertung der Einwilligungsrichtlinie](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) wird derzeit nicht unterstützt, wenn Zielgruppen für Konten für Ziele aktiviert werden. Im Überprüfungsschritt des Aktivierungs-Workflows sehen Sie ein ausgegrautes Steuerelement für **[!UICONTROL Gültige Zustimmungsrichtlinien anzeigen]**.

![Überprüfen Sie den Schritt des Workflows Zielgruppen für das Konto aktivieren , wobei die Kontrolle der Einwilligungsdurchsetzung ausgegraut ist.](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

Andere Data-Governance-Mechanismen in Real-Time CDP, z. B. [Datennutzungsrichtlinien-Prüfungen](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) und [attributbasierte Zugriffssteuerung](/help/destinations/home.md#attribute-based-access) werden unterstützt.
