---
title: Aktivieren von potenziellen Zielgruppen für Ziele
type: Tutorial
description: Erfahren Sie, wie Sie potenzielle Zielgruppen für Ziele aktivieren
exl-id: 3e034a14-09d0-4b08-b171-5afb62ae4b62
source-git-commit: fbc2a6c81682797af4674adabff358a62d973007
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 25%

---

# Interessenten-Zielgruppen aktivieren

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die das Prime- oder das Ultimate-Paket von Real-Time CDP erworben haben. Wenden Sie sich für weitere Informationen an Ihren Adobe-Support-Mitarbeiter.

In diesem Artikel wird der Workflow erläutert, der zum Exportieren erforderlich ist [Interessenten-Zielgruppen](/help/segmentation/ui/prospect-audience.md) von Adobe Experience Platform zu Ihrem bevorzugten Ziel.

## Unterstützte Ziele {#supported-destinations}

Navigieren Sie zu **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]** aus. Verwenden Sie die **[!UICONTROL Datentypen]** filtern und auswählen **[!UICONTROL Perspektiven]** um die Ziele anzuzeigen, die die Aktivierung von potenziellen Zielgruppen unterstützen. Derzeit ist der Export von potenziellen Zielgruppen nur für Cloud-Speicher-Ziele verfügbar.

![Ziele, die potenzielle Zielgruppen unterstützen.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## Voraussetzungen {#prerequisites}

* Du musst zuerst aufnehmen [Interessenten-Profile](/help/profile/ui/prospect-profile.md) und erstellen [Interessenten-Zielgruppen](/help/segmentation/ui/prospect-audience.md) bevor Sie sie für nachgelagerte Ziele aktivieren können.
* Um potenzielle Zielgruppen für Ziele aktivieren zu können, müssen Sie eine erfolgreiche Verbindung zu einem Ziel hergestellt haben. Wenn Sie das noch nicht getan haben, gehen Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten. Tutorial zur Benutzeroberfläche lesen [Verbindung zu Zielen](./connect-destination.md) für weitere Informationen.

### Erforderliche Berechtigungen {#permissions}

Um potenzielle Zielgruppen zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele aktivieren]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Um sicherzustellen, dass Sie über die erforderlichen Berechtigungen zum Aktivieren potenzieller Zielgruppen verfügen, durchsuchen Sie den Zielkatalog. Wenn ein Ziel **[!UICONTROL Aktivieren]** und Sie über die entsprechenden Berechtigungen verfügen.

## Auswählen des Ziels {#select-destination}

Befolgen Sie die Anweisungen zum Auswählen eines Ziels, an das Sie Ihre Datensätze exportieren können:

1. Navigieren Sie zu **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]**.

   ![Registerkarte „Zielkatalog“ mit hervorgehobenem Katalog-Steuerelement.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. Auswählen **[!UICONTROL Aktivieren]** auf der Karte, die dem Ziel entspricht, an das Sie Datensätze exportieren möchten.

>[!TIP]
>
>Die Ziele, die Zielgruppen aus Profilen exportieren können, werden mit einem Symbol oben rechts auf der Karte angezeigt, das dem unten hervorgehobenen Ziel ähnelt. Alternativ können Sie den Datentypfilter verwenden, um nur Ziele anzuzeigen, die Zielgruppen exportieren können, z. B. [höher auf der Seite angezeigt](#supported-destinations).

![Amazon S3-Zielseite, die hervorgehobene Profilzielgruppen exportieren kann.](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. Auswählen **[!UICONTROL Datentypperspektiven]**, gefolgt von der Zielverbindung, in die Sie Datensätze exportieren möchten, und wählen Sie **[!UICONTROL Nächste]**.

>[!TIP]
> 
>Wenn Sie ein neues Ziel einrichten möchten, um potenzielle Zielgruppen zu aktivieren, wählen Sie **[!UICONTROL Neues Ziel konfigurieren]** zum Trigger [Mit Ziel verbinden](/help/destinations/ui/connect-destination.md) Arbeitsablauf.

![Zielaktivierungs-Workflow mit hervorgehobener Kontrolle über die Perspektiven.](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. Fahren Sie mit dem nächsten Abschnitt fort, um [Profil-Audiences auswählen](#select-profile-audiences) für den Export.

## Zielgruppen auswählen {#select-prospect-audiences}

Aktivieren Sie die Kontrollkästchen links neben den Namen der potenziellen Zielgruppen, um die Zielgruppen auszuwählen, die Sie zum Ziel exportieren möchten, und wählen Sie dann **[!UICONTROL Nächste]**. Beachten Sie, dass in dieser Ansicht nur die potenziellen Zielgruppen und keine anderen Zielgruppen angezeigt werden.

![Workflow für den Datensatzexport , der den Schritt Zielgruppen auswählen zeigt, in dem Sie auswählen können, welche potenziellen Zielgruppen exportiert werden sollen.](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## Planung und nächste Schritte

Den Rest des Aktivierungs-Workflows zum Exportieren von Interessenten-Zielgruppen finden Sie im Tutorial zum Aktivieren von Daten für dateibasierte Ziele. Fahren Sie mit dem [Schritt zum Planen des Zielgruppenexports](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).

>[!NOTE]
>
>Beachten Sie, dass der Workflow zur Aktivierung potenzieller Zielgruppen im Planungsschritt nur Folgendes ermöglicht: [vollständige Dateien exportieren](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files). Inkrementelle Dateiexporte werden nicht unterstützt.

<!--

Note that we will need to add links to other destination types here as more destinations become supported 

-->

## Andere durch Partnerdatenunterstützung ermöglichte Anwendungsfälle {#other-use-cases}

Erkunden Sie weitere Anwendungsfälle, die durch die Unterstützung von Partnerdaten in Real-Time CDP ermöglicht werden:

* [Ergänzen Sie Erstanbieterprofile mit Attributen von vertrauenswürdigen Datenpartnern, um Ihre Datengrundlage zu verbessern, neue Einblicke in Ihre Kundenbasis zu gewinnen und eine bessere Zielgruppenoptimierung zu erzielen.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Verwenden Sie die Unterstützung von Drittanbieterdaten in Real-Time CDP, damit Sie [Ihre Profilbasis mit potenziellen Profilen von Datenpartnern erweitern und mit ihnen interagieren können, um neue Kundinnen und Kunden zu gewinnen oder zu erreichen](/help/rtcdp/partner-data/prospecting.md).
* [Nutzen Sie die von Partnern unterstützte Erkennung für die Personalisierung von On-site-Erlebnissen](/help/rtcdp/partner-data/onsite-personalization.md) während des Besuchs, ohne dass sich der Benutzer authentifiziert oder über einen früheren Verlauf mit Ihrer Marke verfügt.
