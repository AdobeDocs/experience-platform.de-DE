---
title: Aktivieren von Audience Manager-Zielgruppen durch erweiterte Aktivierung
description: Erfahren Sie, wie Sie Audience Manager-Zielgruppen über Audience Manager Extended Activation für Social- und Werbeziele aktivieren.
exl-id: 4105f5c5-db69-414f-9ee4-8630b0a86da7
source-git-commit: 2222e9fbf75f3082d331868f820247e0c0ce3ba2
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Aktivieren von Zielgruppen über die erweiterte Aktivierung des Audience Managers

Auf dieser Seite wird der durchgängige Workflow beschrieben, den Sie ausführen müssen, um Zielgruppen vom Audience Manager zu den von &quot;Erweiterte Aktivierung&quot;unterstützten Zielplattformen zu aktivieren.

## Voraussetzungen {#before-you-begin}

Die in diesem Handbuch beschriebenen Schritte setzen voraus, dass Sie die Übersichtsseite [Erweiterte Aktivierung](overview.md) gelesen und bestätigt haben, dass Sie die Voraussetzungen für die Aktivierung der Zielgruppe erfüllt haben.

>[!IMPORTANT]
>
>Um Zielgruppen über [!DNL Expanded Activation] zu aktivieren, stellen Sie sicher, dass Ihre Audience Manager-Zielgruppen auf **Hash-E-Mail-Adressen** basieren. Weitere Informationen finden Sie unter [Voraussetzungen](overview.md#prerequisites) .

## Schritt 1: Konfigurieren der Quellverbindung des Audience Managers {#configure-source}

Der [Audience Manager-Quell-Connector](../sources/connectors/adobe-applications/audience-manager.md) sendet in Adobe Audience Manager erfasste Zielgruppendaten zur Aktivierung auf den von der erweiterten Aktivierung unterstützten Zielplattformen.

Befolgen Sie die Anleitung zum [Erstellen einer Quellverbindung des Audience Managers](../sources/tutorials/ui/create/adobe-applications/audience-manager.md), um Ihren Quell-Connector zu konfigurieren.

![Bild der Platform-Benutzeroberfläche, das die Registerkarte &quot;Quellen&quot;mit der Quellverbindung des Audience Managers anzeigt.](assets/sources-tab.png)

>[!TIP]
>
>Der Adobe Audience Manager-Quell-Connector ist der einzige Quell-Connector, der unter Erweiterte Aktivierung verfügbar ist.
>
>Wenn Sie Zielgruppen basierend auf zusätzlichen Kennungen erfassen möchten, müssen Sie eine Ausgabe von [Real-Time CDP](../rtcdp/overview.md) erwerben. Weitere Informationen erhalten Sie von Ihrem Adobe-Support-Mitarbeiter.

### Aufgenommene Zielgruppen anzeigen und überwachen {#view-audiences}

Die Zielgruppen, die Sie in die erweiterte Aktivierung von Audience Manager integrieren, können Sie im Dashboard **[!UICONTROL Zielgruppen]** anzeigen.

Um Ihre Zielgruppen anzuzeigen, gehen Sie zu **[!UICONTROL Kunde]** -> **[!UICONTROL Zielgruppen]** -> **[!UICONTROL Durchsuchen]**.

![Bild der Platform-Benutzeroberfläche, das die Seite &quot;Zielgruppen&quot;anzeigt.](assets/audiences-browse.png)

>[!IMPORTANT]
>
>* Es kann bis zu 48 Stunden dauern, bis Zielgruppen vollständig in &quot;Erweiterte Aktivierung&quot;gefüllt sind. Dies gilt auch für Aktualisierungen bestehender Audience Manager-Zielgruppen.
>* Neu erstellte Audience Manager-Zielgruppen werden nicht automatisch in der erweiterten Aktivierung angezeigt. Um neue Segmente in erweiterter Aktivierung zu erfassen, müssen Sie sie über den Quell-Connector des Audience Managers hinzufügen.

Nachdem Sie den Quell-Connector für den Audience Manager konfiguriert haben, wechseln Sie zu [Schritt 2](#create-destination-connection).

## Schritt 2: Erstellen einer neuen Zielverbindung {#create-destination-connection}

Bevor Sie Ihre Audience Manager-Zielgruppen an Ihre Zielplattform Ihrer Wahl senden können, müssen Sie zunächst eine Verbindung zu einer Zielplattform herstellen.

Wechseln Sie in der linken Seitenleiste zu **[!UICONTROL Verbindungen]** -> **[!UICONTROL Ziele]** -> **[!UICONTROL Katalog]**.

Die verfügbaren Zielkategorien für [!DNL Expanded Activation] sind [Werbung](../destinations/catalog/advertising/overview.md) und [Social](../destinations/catalog/social/overview.md).

![Bild der Platform-Benutzeroberfläche, das den Zielkatalog für erweiterte Aktivierung anzeigt.](assets/destination-catalog.png)

Um eine neue Verbindung zu einer Zielplattform zu erstellen, befolgen Sie das Handbuch [Erstellen einer neuen Zielverbindung](../destinations/ui/connect-destination.md). Wechseln Sie dann zu [Schritt 3](#activate-audiences).

## Schritt 3: Aktivieren von Zielgruppen für Ihr Ziel {#activate-audiences}

Nachdem Sie die [ aufgenommenen Audience Manager-Zielgruppen](#configure-source) erfolgreich [ und eine neue Zielverbindung erstellt haben](#create-destination-connection), können Sie Ihre Zielgruppen jetzt für die Zielplattform Ihrer Wahl aktivieren.

![Bild der Platform-Benutzeroberfläche, das den Zielkatalog für erweiterte Aktivierung anzeigt.](assets/activate-audiences.png)

Um Zielgruppen für Ihr Ziel zu aktivieren, folgen Sie dem Handbuch [So aktivieren Sie Zielgruppen für Streaming-Ziele](../destinations/ui/activate-segment-streaming-destinations.md).

## Überprüfung der Zielgruppenaktivierung {#verify}

Detaillierte Informationen zur Überwachung des Datenflusses zu Ihren Zielen finden Sie in der Dokumentation zur [Zielüberwachung](../dataflows/ui/monitor-destinations.md) .
