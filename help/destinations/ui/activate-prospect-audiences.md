---
title: Aktivieren von potenziellen Zielgruppen für Ziele
type: Tutorial
description: Erfahren Sie, wie Sie potenzielle Zielgruppen für Ziele aktivieren
exl-id: 3e034a14-09d0-4b08-b171-5afb62ae4b62
source-git-commit: e7c0551276d31d6809ace096c00e0dc2665090e6
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 25%

---

# Zielgruppen potenzieller Kundinnen und Kunden aktivieren

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die das Prime- oder das Ultimate-Paket von Real-Time CDP erworben haben. Weitere Informationen erhalten Sie vom Adobe-Support.

In diesem Artikel wird der Workflow erläutert, der zum Exportieren [potenzieller Zielgruppen](/help/segmentation/types/prospect-audiences.md) aus Adobe Experience Platform an Ihr bevorzugtes Ziel erforderlich ist.

## Unterstützte Ziele {#supported-destinations}

Navigieren Sie zu **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]** aus. Verwenden Sie den Filter **[!UICONTROL Datentypen]** und wählen Sie **[!UICONTROL Interessenten]** aus, um die Ziele anzuzeigen, die die Aktivierung potenzieller Zielgruppen unterstützen. Derzeit ist der Export von potenziellen Zielgruppen nur für Cloud-Speicher-Ziele verfügbar.

![Ziele, die Zielgruppen potenzieller Kundinnen und Kunden unterstützen.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## Voraussetzungen {#prerequisites}

* Sie müssen zunächst [Interessentenprofile](/help/profile/ui/prospect-profile.md) aufnehmen und [Interessentenzielgruppen](/help/segmentation/types/prospect-audiences.md) erstellen, bevor Sie sie für nachgelagerte Ziele aktivieren können.
* Um potenzielle Zielgruppen für Ziele aktivieren zu können, müssen Sie erfolgreich eine Verbindung zu einem Ziel hergestellt haben. Wenn Sie es noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten. Lesen Sie das Tutorial zur Benutzeroberfläche [Herstellen einer Verbindung zu Zielen](./connect-destination.md), um weitere Informationen zu erhalten.

### Erforderliche Berechtigungen {#permissions}

Um potenzielle Zielgruppen zu aktivieren, benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele aktivieren]** [Zugriffskontrolle](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Um sicherzustellen, dass Sie über die erforderlichen Berechtigungen zum Aktivieren von Zielgruppen potenzieller Kundinnen und Kunden verfügen, durchsuchen Sie den Zielkatalog. Wenn ein Ziel über ein **[!UICONTROL Aktivieren]**-Steuerelement verfügt, verfügen Sie über die entsprechenden Berechtigungen.

## Auswählen des Ziels {#select-destination}

Befolgen Sie die Anweisungen zum Auswählen eines Ziels, an das Sie Ihre Datensätze exportieren können:

1. Navigieren Sie zu **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]**.

   ![Registerkarte „Zielkatalog“ mit hervorgehobenem Katalog-Steuerelement.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. Wählen Sie **[!UICONTROL Aktivieren]** auf der Karte aus, die dem Ziel entspricht, an das Sie Datensätze exportieren möchten.

>[!TIP]
>
>Die Ziele, die Profil-Audiences exportieren können, werden mit einem Symbol oben rechts auf der Karte angezeigt, ähnlich dem unten hervorgehobenen Ziel. Alternativ können Sie den Datentypfilter verwenden, um nur Ziele anzuzeigen, die potenzielle Audiences exportieren können ([ weiter oben auf der Seite ](#supported-destinations).

![Amazon S3-Zielseite, auf der Profil-Zielgruppen exportiert werden können, hervorgehoben.](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. Wählen Sie **[!UICONTROL Datentyp Interessenten]**, gefolgt von der Zielverbindung, an die Sie Datensätze exportieren möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**.

>[!TIP]
> 
>Wenn Sie ein neues Ziel zur Aktivierung potenzieller Zielgruppen einrichten möchten, wählen Sie **[!UICONTROL Neues Ziel konfigurieren]** aus, um den Workflow [Mit Ziel verbinden](/help/destinations/ui/connect-destination.md) Trigger.

![Zielaktivierungs-Workflow mit hervorgehobenem Steuerelement „Interessenten“.](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. Fahren Sie mit dem nächsten Abschnitt fort[ um Ihre Profil-Audiences ](#select-profile-audiences) exportieren.

## Zielgruppen des potenziellen Kunden auswählen {#select-prospect-audiences}

Aktivieren Sie die Kontrollkästchen links neben den Namen der potenziellen Zielgruppen, um die Zielgruppen auszuwählen, die Sie an das Ziel exportieren möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**. Beachten Sie, dass in dieser Ansicht nur die Zielgruppen potenzieller Kundinnen und Kunden angezeigt werden. Andere Zielgruppen werden nicht angezeigt.

![Workflow für den Datensatzexport, der den Schritt „Zielgruppen auswählen“ zeigt, in dem Sie auswählen können, welche potenziellen Zielgruppen exportiert werden sollen.](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## Planung und nächste Schritte

Für den Rest des Aktivierungs-Workflows zum Exportieren von potenziellen Zielgruppen lesen Sie das Tutorial zum Aktivieren von Daten für dateibasierte Ziele. Fahren Sie mit dem [Schritt Zielgruppenexport planen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) fort.

>[!NOTE]
>
>Beachten Sie, dass Sie im Planungsschritt mit dem Workflow zur Aktivierung von Zielgruppen potenzieller Kundinnen und Kunden nur [vollständige Dateien exportieren](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files). Inkrementelle Dateiexporte werden nicht unterstützt.

<!--

Note that we will need to add links to other destination types here as more destinations become supported 

-->

## Andere durch Partnerdatenunterstützung ermöglichte Anwendungsfälle {#other-use-cases}

Erkunden Sie weitere Anwendungsfälle, die durch die Unterstützung von Partnerdaten in Real-Time CDP ermöglicht werden:

* [Ergänzen Sie Erstanbieterprofile mit Attributen von vertrauenswürdigen Datenpartnern, um Ihre Datengrundlage zu verbessern, neue Einblicke in Ihre Kundenbasis zu gewinnen und eine bessere Zielgruppenoptimierung zu erzielen.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Verwenden Sie die Unterstützung von Drittanbieterdaten in Real-Time CDP, damit Sie [Ihre Profilbasis mit potenziellen Profilen von Datenpartnern erweitern und mit ihnen interagieren können, um neue Kundinnen und Kunden zu gewinnen oder zu erreichen](/help/rtcdp/partner-data/prospecting.md).
* [Nutzen Sie die von Partnern unterstützte Erkennung zur Personalisierung von Erlebnissen vor Ort](/help/rtcdp/partner-data/onsite-personalization.md) während des Besuchs, ohne dass sich der Benutzer authentifiziert oder eine Vorgeschichte mit Ihrer Marke hat.
