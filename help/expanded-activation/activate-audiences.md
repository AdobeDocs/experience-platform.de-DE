---
title: Aktivieren von Audience Manager-Zielgruppen durch erweiterte Aktivierung
description: Erfahren Sie, wie Sie Audience Manager-Zielgruppen über Audience Manager Extended Activation für Social- und Werbeziele aktivieren.
source-git-commit: 19fb369a7faa0c5ac27a34db7b848b0332cb8695
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# Aktivieren von Zielgruppen über die erweiterte Aktivierung des Audience Managers

Auf dieser Seite wird der durchgängige Workflow beschrieben, den Sie ausführen müssen, um Zielgruppen vom Audience Manager zu den von &quot;Erweiterte Aktivierung&quot;unterstützten Zielplattformen zu aktivieren.

## Voraussetzungen {#before-you-begin}

Die in diesem Handbuch beschriebenen Schritte setzen voraus, dass Sie die [Erweiterte Aktivierungsübersichtsseite](overview.md) und Sie haben bestätigt, dass Sie die Voraussetzungen für die Aktivierung der Zielgruppe erfüllen.

>[!IMPORTANT]
>
>So aktivieren Sie Zielgruppen durch [!DNL Expanded Activation], stellen Sie sicher, dass Ihre Audience Manager-Zielgruppen auf **Hash-E-Mail-Adressen**. Siehe [Voraussetzungen](overview.md#prerequisites) für weitere Details.

## Schritt 1: Konfigurieren der Quellverbindung des Audience Managers {#configure-source}

Die [Quell-Connector für Audience Manager](../sources/connectors/adobe-applications/audience-manager.md) sendet in Adobe Audience Manager erfasste Zielgruppendaten zur Aktivierung in den von &quot;Erweiterte Aktivierung&quot;unterstützten Zielplattformen.

Befolgen Sie das Handbuch zum [Erstellen einer Audience Manager-Quellverbindung](../sources/tutorials/ui/create/adobe-applications/audience-manager.md) , um Ihren Quell-Connector zu konfigurieren.

![Abbildung der Platform-Benutzeroberfläche, die die Registerkarte Quellen mit der Quellverbindung des Audience Managers anzeigt.](assets/sources-tab.png)

>[!TIP]
>
>Der Adobe Audience Manager-Quell-Connector ist der einzige Quell-Connector, der unter Erweiterte Aktivierung verfügbar ist.
>
>Wenn Sie Zielgruppen basierend auf zusätzlichen Kennungen erfassen möchten, müssen Sie eine Ausgabe von [Real-Time CDP](../rtcdp/overview.md). Weitere Informationen erhalten Sie von Ihrem Adobe-Support-Mitarbeiter.

### Aufgenommene Zielgruppen anzeigen und überwachen {#view-audiences}

Die Zielgruppen, die Sie in die erweiterte Aktivierung von Audience Manager einbeziehen, können Sie im **[!UICONTROL Zielgruppen]** Dashboard.

Um Ihre Zielgruppen anzuzeigen, gehen Sie zu **[!UICONTROL Kunde]** -> **[!UICONTROL Zielgruppen]** -> **[!UICONTROL Durchsuchen]**.

![Platform-UI-Bild mit der Seite &quot;Zielgruppen&quot;.](assets/audiences-browse.png)

>[!IMPORTANT]
>
>* Es kann bis zu 48 Stunden dauern, bis Zielgruppen vollständig in &quot;Erweiterte Aktivierung&quot;gefüllt sind. Dies gilt auch für Aktualisierungen bestehender Audience Manager-Zielgruppen.
>* Neu erstellte Audience Manager-Zielgruppen werden nicht automatisch in der erweiterten Aktivierung angezeigt. Um neue Segmente in erweiterter Aktivierung zu erfassen, müssen Sie sie über den Quell-Connector des Audience Managers hinzufügen.

Nachdem Sie den Quell-Connector für Audience Manager konfiguriert haben, wechseln Sie zu [Schritt 2](#create-destination-connection).

## Schritt 2: Erstellen einer neuen Zielverbindung {#create-destination-connection}

Bevor Sie Ihre Audience Manager-Zielgruppen an Ihre Zielplattform Ihrer Wahl senden können, müssen Sie zunächst eine Verbindung zu einer Zielplattform herstellen.

Navigieren Sie in der linken Seitenleiste zu **[!UICONTROL Verbindungen]** -> **[!UICONTROL Ziele]** -> **[!UICONTROL Katalog]**.

Die verfügbaren Zielkategorien für [!DNL Expanded Activation] are [Werbung](../destinations/catalog/advertising/overview.md) und [social](../destinations/catalog/social/overview.md).

![Platform-UI-Bild, das den Zielkatalog für die erweiterte Aktivierung anzeigt.](assets/destination-catalog.png)

Um eine neue Verbindung zu einer Zielplattform zu erstellen, befolgen Sie das Handbuch zu [Erstellen einer neuen Zielverbindung](../destinations/ui/connect-destination.md). Navigieren Sie dann zu [Schritt 3](#activate-audiences).

## Schritt 3: Aktivieren von Zielgruppen für Ihr Ziel {#activate-audiences}

Nach erfolgreichem Abschluss [Aufgenommene Audience Manager-Zielgruppen](#configure-source) und [eine neue Zielverbindung erstellt hat](#create-destination-connection)können Sie nun Ihre Zielgruppen für die gewünschte Zielplattform aktivieren.

![Platform-UI-Bild, das den Zielkatalog für die erweiterte Aktivierung anzeigt.](assets/activate-audiences.png)

Um Zielgruppen für Ihr Ziel zu aktivieren, folgen Sie dem Handbuch zu [So aktivieren Sie Zielgruppen für Streaming-Ziele](../destinations/ui/activate-segment-streaming-destinations.md).

## Überprüfung der Zielgruppenaktivierung {#verify}

Überprüfen Sie die [Zielüberwachungsdokumentation](../dataflows/ui/monitor-destinations.md) für detaillierte Informationen zur Überwachung des Datenflusses zu Ihren Zielen.