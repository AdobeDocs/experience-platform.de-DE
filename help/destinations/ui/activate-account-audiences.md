---
title: Kontozielgruppen für Ziele aktivieren
type: Tutorial
description: Erfahren Sie, wie Sie Kontozielgruppen für Ziele aktivieren.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: 1c31dd978298191dd10500b60eb446d2ca37139c
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 7%

---

# Kontozielgruppen aktivieren

>[!AVAILABILITY]
>
>Die Funktion zum Aktivieren von Kontozielgruppen für Ziele ist für Unternehmen verfügbar, die die Editionen [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) und [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) von Real-time Customer Data Platform erwerben.

In diesem Artikel wird der Workflow erläutert, der zum Exportieren von [Konto-Zielgruppen](/help/segmentation/ui/account-audiences.md) aus Adobe Experience Platform in Ihr bevorzugtes Ziel erforderlich ist.

## Unterstützte Ziele {#supported-destinations}

Navigieren Sie zu **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]** aus. Verwenden Sie den Filter **[!UICONTROL Datentypen]** und wählen Sie **[!UICONTROL Konten]** aus, um die Ziele anzuzeigen, die die Aktivierung von Kontozielgruppen unterstützen. Derzeit ist der Export von Kontozielgruppen nur für bestimmte Cloud-Speicher-Ziele verfügbar ([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Azure Blob Storage](/help/destinations/catalog/cloud-storage/azure-blob.md), [Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md) und [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)) und die LinkedIn-Matches [Demandbase](/help/destinations/catalog/advertising/demandbase.md) und [ (Unternehmen) Zielgruppen](/help/destinations/catalog/social/linkedin-b2b.md)-Streaming-Ziel.

![Ziele, die Kontozielgruppen unterstützen.](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## Videoüberblick

Im folgenden Video erhalten Sie einen Überblick über das Erstellen und Aktivieren von Zielgruppen für Konten sowie über die unterstützten Anwendungsfälle beim Aktivieren von Zielgruppen für Konten.

>[!VIDEO](https://video.tv.adobe.com/v/338252/?learn=on)

## Voraussetzungen {#prerequisites}

* Sie müssen zunächst [Kontoprofile](/help/rtcdp/accounts/account-profile-overview.md) erfassen und [Kontozielgruppen](/help/segmentation/ui/account-audiences.md) erstellen, bevor Sie sie für nachgelagerte Ziele aktivieren können.
* Um Kontozielgruppen für Ziele zu aktivieren, müssen Sie eine erfolgreiche Verbindung zu einem Ziel hergestellt haben. Wenn Sie dies noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten. Weitere Informationen finden Sie im Tutorial zur Benutzeroberfläche für das [Verbinden mit Zielen](./connect-destination.md) .

### Erforderliche Berechtigungen {#permissions}

Um Kontozielgruppen zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele aktivieren]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Um sicherzustellen, dass Sie über die erforderlichen Berechtigungen zum Aktivieren von Kontozielgruppen verfügen, durchsuchen Sie den Zielkatalog. Wenn ein Ziel über ein Steuerelement vom Typ **[!UICONTROL Aktivieren]** verfügt, verfügen Sie über die entsprechenden Berechtigungen.

## Auswählen des Ziels {#select-destination}

Befolgen Sie die Anweisungen zum Auswählen eines Ziels, an das Sie Ihre Datensätze exportieren können:

1. Navigieren Sie zu **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]**.

   ![Registerkarte „Zielkatalog“ mit hervorgehobenem Katalog-Steuerelement.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Wählen Sie **[!UICONTROL Aktivieren]** auf der Karte aus, die dem Ziel entspricht, in das Sie Datensätze exportieren möchten.

>[!TIP]
>
>Die Ziele, die Zielgruppen für Konten exportieren können, werden mit einem Symbol oben rechts auf der Karte angezeigt, das dem unten hervorgehobenen Ziel ähnelt. Alternativ können Sie den Datentypfilter verwenden, um nur Ziele anzuzeigen, die Zielgruppen für Konten exportieren können, wie oben auf der Seite ](#supported-destinations) gezeigt.[

![Demandbase-Zielseite, die hervorgehobene Profilzielgruppen exportieren kann.](/help/destinations/assets/ui/activate-account-audiences/demandbase-icon-activate-account-audiences.png)

1. Wählen Sie **[!UICONTROL Datentypkonten]**, gefolgt von der Zielverbindung, in die Sie Datensätze exportieren möchten, und wählen Sie dann **[!UICONTROL Weiter]** aus.

>[!TIP]
> 
>Wenn Sie ein neues Ziel einrichten möchten, um Kontozielgruppen zu aktivieren, wählen Sie **[!UICONTROL Neues Ziel konfigurieren]** aus, um den Workflow [Mit Ziel verbinden](/help/destinations/ui/connect-destination.md) Trigger, und [wählen Sie Konten als Datentyp aus](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![Zielaktivierungs-Workflow mit hervorgehobener Kontosteuerung.](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. Fahren Sie mit dem nächsten Abschnitt [Auswählen Ihrer Kontozielgruppen](#select-profile-audiences) für den Export fort.

## Zielgruppen für Ihr Konto auswählen {#select-account-audiences}

Verwenden Sie die Kontrollkästchen links neben den Namen der Zielgruppen des Kontos, um die Zielgruppen auszuwählen, die Sie zum Ziel exportieren möchten, und wählen Sie dann **[!UICONTROL Weiter]** aus. Beachten Sie, dass in dieser Ansicht nur *Konto-Zielgruppen* angezeigt werden und keine anderen Zielgruppentypen angezeigt werden.

![Workflow für den Datensatzexport , der den Schritt Zielgruppen auswählen zeigt, in dem Sie auswählen können, welche Zielgruppen exportiert werden sollen.](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## Planung und nächste Schritte

Den Rest des Aktivierungs-Workflows zum Exportieren von Kontozielgruppen finden Sie im Tutorial zum Aktivieren von Daten für dateibasierte Ziele. Fahren Sie mit dem Schritt [Zielgruppenexport planen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) fort. Wenn Sie Kontozielgruppen für das Ziel &quot;**[!UICONTROL (Unternehmen) LinkedIn Matched Audiences]**&quot;aktivieren, lesen Sie das Tutorial zum Aktivieren von Streaming-Zielen. Fahren Sie mit dem Schritt [Zuordnen](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) fort.

>[!NOTE]
>
>Beachten Sie, dass im Planungsschritt beim Exportieren von Kontozielgruppen in Cloud-Speicher-Ziele der Workflow zum Aktivieren von Kontozielgruppen nur den Export von [vollständigen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) und [inkrementellen Dateien](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _nach einem täglichen Zeitplan ermöglicht._ Stündliche Exporte werden nicht unterstützt. Beachten Sie außerdem, dass **[!UICONTROL Nach der Zielgruppenauswertung]** der einzige unterstützte Auswertungstyp ist.

## Wichtige Hinweise und bekannte Einschränkungen {#important-callouts-known-limitations}

Beachten Sie die folgenden wichtigen Hinweisen und bekannten Einschränkungen für die allgemeine Verfügbarkeit der Funktion zum Aktivieren von Kontozielgruppen.

### Erforderliche Zuordnungspaare im Zuordnungsschritt bei der Aktivierung von Kontozielgruppen für das Ziel **[!UICONTROL (Unternehmen) LinkedIn Matched Audiences]** {#required-mappings}

Beachten Sie beim Aktivieren von Kontozielgruppen für das Ziel &quot;**[!UICONTROL (Unternehmen) LinkedIn Matched Audiences]**&quot;, dass die folgenden beiden Zuordnungspaare für den erfolgreichen Export von Daten obligatorisch sind:

![Erforderliche Felder für die LinkedIn-Zuordnung.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Quellfeld | Zielfeld |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (Wählen Sie dieses Feld in der Ansicht **[!UICONTROL Identitäts-Namespace auswählen]** aus, wenn Sie das **[!UICONTROL Zielfeld]** auswählen). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Kontozielgruppen für Ziele zu aktivieren.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Kontozielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"} |

### Data Governance-Durchsetzung {#data-governance-enforcement}

Die Zustimmung wird auf Personen- oder Profilebene für *Kunden- und Interessensgruppen* erzwungen. Daher wird die Bewertung von [Einwilligungsrichtlinien](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) derzeit nicht unterstützt, wenn Kontozielgruppen für Ziele aktiviert werden. Im Überprüfungsschritt des Aktivierungs-Workflows sehen Sie ein ausgegrautes Steuerelement für **[!UICONTROL Gültige Zustimmungsrichtlinien anzeigen]**.

![Überprüfen Sie den Schritt des Workflows &quot;Zielgruppen des Kontos aktivieren&quot;, wobei die Kontrolle der Einwilligungsdurchsetzung ausgegraut ist.](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

Andere Data Governance-Mechanismen in Real-Time CDP wie [Datennutzungsrichtlinien-Prüfungen](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) und [attributbasierte Zugriffskontrolle](/help/destinations/home.md#attribute-based-access) werden unterstützt.
