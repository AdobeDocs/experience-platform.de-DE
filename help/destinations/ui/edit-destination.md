---
title: Ziele bearbeiten
type: Tutorial
description: Erfahren Sie, wie Sie vorhandene Zielkonten in der Adobe Experience Platform-Benutzeroberfläche bearbeiten und aktualisieren
exl-id: f3298836-668b-43fb-b4f3-85a650766f05
source-git-commit: f91551c460c7d6fd4f98111210f29cf16ec5b565
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 5%

---

# Ziele bearbeiten

Erfahren Sie, wie Sie verschiedene Komponenten einer vorhandenen Zielverbindung bearbeiten, einschließlich der Aktualisierung der Authentifizierungsdaten, des Exportspeicherorts und mehr mithilfe der Experience Platform-Benutzeroberfläche.

>[!NOTE]
>
> Die in diesem Tutorial beschriebenen Bearbeitungsvorgänge werden auch über API-Vorgänge unterstützt. Weitere Informationen finden Sie im Tutorial [ Bearbeiten von Zielen in ](/help/destinations/api/edit-destination.md) API .

## Voraussetzungen {#prerequisites}

Zum Bearbeiten von Zielverbindungen benötigen Sie die **[!UICONTROL Manage Destinations]** [Zugriffssteuerungsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

## Bearbeiten von Zielverbindungen {#edit}

So bearbeiten Sie verschiedene Komponenten einer vorhandenen Zielverbindung:

1. Navigieren Sie zu **[!UICONTROL Destinations]** > **[!UICONTROL Browse]**.
2. Wählen Sie das gewünschte Ziel aus, das Sie bearbeiten möchten.
3. Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Name] und verwenden Sie das Steuerelement ![Steuerung „Ziel bearbeiten ](/help/images/icons/edit.png)**[!UICONTROL Edit destination]**zum Bearbeiten vorhandener Zielverbindungen.
4. Bearbeiten Sie im modalen Fenster die gewünschten Einstellungen. Wählen Sie abschließend **[!UICONTROL Save]** aus.

Im Fenster Ziel bearbeiten können Sie alle Einstellungen aktualisieren, die Sie beim erstmaligen Herstellen einer Verbindung mit dem Ziel konfiguriert haben. Diese Einstellungen unterscheiden sich je nach Zielplattform, die Sie aktualisieren.

Je nachdem, wie das Ziel konfiguriert wurde, sind einige Felder möglicherweise schreibgeschützt und können nicht bearbeitet werden. Um den Wert von schreibgeschützten Feldern zu ändern, müssen Sie [eine neue Zielverbindung erstellen](../ui/connect-destination.md) mit den neuen Feldwerten verwenden.

![Screenshot mit einem schreibgeschützten Feld.](../assets/ui/edit-destinations/read-only.png)

Im Folgenden finden Sie einige Beispiele für die Einstellungen, die Sie für [Ziele von Amazon S3](../catalog/cloud-storage/amazon-s3.md), [Azure Event Hubs](../catalog/cloud-storage/azure-event-hubs.md) und [Google Ads](../catalog/advertising/google-ads-destination.md) aktualisieren können.

<div style="display: flex; gap: 12px; justify-content: flex-start; align-items: flex-start;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-amazon-s3-connection.png" alt="Bildschirm „Ziel bearbeiten“ für das Amazon S3-Ziel." style="max-width: 200px; height: auto; border: 1px solid #ccc;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-eventhubs-connection.png" alt="Bildschirm „Ziel bearbeiten“ für das Azure EventHubs-Ziel." style="max-width: 200px; height: auto; border: 1px solid #ccc;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-google-ads-connection.png" alt="Bildschirm „Ziel bearbeiten“ für das Google Ads-Ziel." style="max-width: 200px; height: auto; border: 1px solid #ccc;">
</div>

>[!SUCCESS]
>
>Die Einstellungen für Ihre Zielverbindung wurden aktualisiert.

## Weitere Bearbeitungsoptionen

Mithilfe der Experience Platform-Benutzeroberfläche oder der Flow Service-API können Sie verschiedene Zielkonfigurationen bearbeiten, wie in den folgenden Links beschrieben:

| Verwenden der Experience Platform-Benutzeroberfläche | Verwenden der Flow Service-API |
|---------|----------|
| Bearbeiten von Zielverbindungen (diese Seite) | [Bearbeiten der Zielverbindungskomponenten (Speicherort und andere Komponenten)](/help/destinations/api/edit-destination.md#patch-target-connection) |
| [Konten bearbeiten](/help/destinations/ui/update-accounts.md) | [Bearbeiten von Basisverbindungskomponenten (Authentifizierungsparameter und andere Komponenten)](/help/destinations/api/edit-destination.md#patch-base-connection) |
| [Bearbeiten von Aktivierungsdatenflüssen](/help/destinations/ui/edit-activation.md) | [Aktualisieren von Ziel-Datenflüssen](/help/destinations/api/update-destination-dataflows.md) |

## Nächste Schritte

In diesem Tutorial haben Sie den **[!UICONTROL destinations]** Workspace erfolgreich verwendet, um vorhandene Zielverbindungen zu aktualisieren.

Weitere Informationen zu Zielen finden Sie unter [Ziele - Übersicht](../catalog/overview.md).
