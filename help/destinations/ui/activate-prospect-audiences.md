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

# Zielgruppen potenzieller Kundinnen und Kunden aktivieren

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die das Prime- oder das Ultimate-Paket von Real-Time CDP erworben haben. Wenden Sie sich für weitere Informationen an Ihren Adobe-Support-Mitarbeiter.

In diesem Artikel wird der Workflow erläutert, der zum Exportieren von [Interessenten-Zielgruppen](/help/segmentation/ui/prospect-audience.md) aus Adobe Experience Platform in Ihr bevorzugtes Ziel erforderlich ist.

## Unterstützte Ziele {#supported-destinations}

Navigieren Sie zu **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]** aus. Verwenden Sie den Filter **[!UICONTROL Datentypen]** und wählen Sie **[!UICONTROL Perspektiven]** aus, um die Ziele anzuzeigen, die die Aktivierung potenzieller Zielgruppen unterstützen. Derzeit ist der Export von potenziellen Zielgruppen nur für Cloud-Speicher-Ziele verfügbar.

![Ziele, die Interessenten-Zielgruppen unterstützen.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## Voraussetzungen {#prerequisites}

* Sie müssen zunächst [Interessenten-Profile](/help/profile/ui/prospect-profile.md) erfassen und [Interessenten-Zielgruppen](/help/segmentation/ui/prospect-audience.md) erstellen, bevor Sie sie für nachgelagerte Ziele aktivieren können.
* Um potenzielle Zielgruppen für Ziele aktivieren zu können, müssen Sie eine erfolgreiche Verbindung zu einem Ziel hergestellt haben. Wenn Sie dies noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten. Weitere Informationen finden Sie im Tutorial zur Benutzeroberfläche für das [Verbinden mit Zielen](./connect-destination.md) .

### Erforderliche Berechtigungen {#permissions}

Um Interessenten-Zielgruppen zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele aktivieren]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Um sicherzustellen, dass Sie über die erforderlichen Berechtigungen zum Aktivieren potenzieller Zielgruppen verfügen, durchsuchen Sie den Zielkatalog. Wenn ein Ziel über ein Steuerelement vom Typ **[!UICONTROL Aktivieren]** verfügt, verfügen Sie über die entsprechenden Berechtigungen.

## Auswählen des Ziels {#select-destination}

Befolgen Sie die Anweisungen zum Auswählen eines Ziels, an das Sie Ihre Datensätze exportieren können:

1. Navigieren Sie zu **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]**.

   ![Registerkarte „Zielkatalog“ mit hervorgehobenem Katalog-Steuerelement.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. Wählen Sie **[!UICONTROL Aktivieren]** auf der Karte aus, die dem Ziel entspricht, in das Sie Datensätze exportieren möchten.

>[!TIP]
>
>Die Ziele, die Profilzielgruppen exportieren können, werden mit einem Symbol oben rechts auf der Karte angezeigt, das dem unten hervorgehobenen Ziel ähnelt. Alternativ können Sie den Datentypfilter verwenden, um nur Ziele anzuzeigen, die Interessenten exportieren können, wie oben auf der Seite ](#supported-destinations) gezeigt.[

![Amazon S3-Zielseite, die hervorgehobene Profilzielgruppen exportieren kann.](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. Wählen Sie **[!UICONTROL Datentypaussichten]**, gefolgt von der Zielverbindung, in die Sie Datensätze exportieren möchten, und wählen Sie dann **[!UICONTROL Weiter]** aus.

>[!TIP]
> 
>Wenn Sie ein neues Ziel einrichten möchten, um potenzielle Zielgruppen zu aktivieren, wählen Sie **[!UICONTROL Neues Ziel konfigurieren]** aus, um den Workflow [Mit Ziel verbinden](/help/destinations/ui/connect-destination.md) Trigger.

![Zielaktivierungs-Workflow mit hervorgehobenem Prospects-Steuerelement.](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. Fahren Sie mit dem nächsten Abschnitt [Wählen Sie Ihre Profilzielgruppen](#select-profile-audiences) für den Export aus.

## Zielgruppen auswählen {#select-prospect-audiences}

Aktivieren Sie die Kontrollkästchen links neben den Namen der potenziellen Zielgruppen, um die Zielgruppen auszuwählen, die Sie an das Ziel exportieren möchten, und wählen Sie dann **[!UICONTROL Weiter]** aus. Beachten Sie, dass in dieser Ansicht nur die potenziellen Zielgruppen und keine anderen Zielgruppen angezeigt werden.

![Workflow für den Datensatzexport , der den Schritt Zielgruppen auswählen zeigt, in dem Sie auswählen können, welche potenziellen Zielgruppen exportiert werden sollen.](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## Planung und nächste Schritte

Den Rest des Aktivierungs-Workflows zum Exportieren von Interessenten-Zielgruppen finden Sie im Tutorial zum Aktivieren von Daten für dateibasierte Ziele. Fahren Sie mit dem Schritt [Zielgruppenexport planen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) fort.

>[!NOTE]
>
>Beachten Sie, dass im Planungsschritt der Workflow zum Aktivieren potenzieller Zielgruppen nur den Export von vollständigen Dateien ermöglicht.](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) [ Inkrementelle Dateiexporte werden nicht unterstützt.

<!--

Note that we will need to add links to other destination types here as more destinations become supported 

-->

## Andere durch Partnerdatenunterstützung ermöglichte Anwendungsfälle {#other-use-cases}

Erkunden Sie weitere Anwendungsfälle, die durch die Unterstützung von Partnerdaten in Real-Time CDP ermöglicht werden:

* [Ergänzen Sie Erstanbieterprofile mit Attributen von vertrauenswürdigen Datenpartnern, um Ihre Datengrundlage zu verbessern, neue Einblicke in Ihre Kundenbasis zu gewinnen und eine bessere Zielgruppenoptimierung zu erzielen.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Verwenden Sie die Unterstützung von Drittanbieterdaten in Real-Time CDP, damit Sie [Ihre Profilbasis mit potenziellen Profilen von Datenpartnern erweitern und mit ihnen interagieren können, um neue Kundinnen und Kunden zu gewinnen oder zu erreichen](/help/rtcdp/partner-data/prospecting.md).
* [Nutzen Sie die partnerbezogene Erkennung für die Personalisierung von On-site-Erlebnissen](/help/rtcdp/partner-data/onsite-personalization.md) während des Besuchs, ohne dass sich der Benutzer authentifiziert oder über einen früheren Verlauf mit Ihrer Marke verfügt.
