---
keywords: Ziele; Ziel; Zieldetailseite; Zieldetailseite; Zieldetailseite
title: Zieldetails anzeigen
description: 'Die Detailseite für ein einzelnes Ziel bietet einen Überblick über die Zieldetails. Zu den Zieldetails gehören der Zielname, die ID, die dem Ziel zugeordneten Segmente und die Steuerelemente zum Bearbeiten der Aktivierung und zum Aktivieren und Deaktivieren des Datenflusses. '
seo-description: The details page for an individual destination provides an overview of the destination details. Destination details include the destination name, ID, segments mapped to the destination, and controls to edit the activation and to enable and disable the data flow.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 6%

---

# Zieldetails anzeigen

## Übersicht {#overview}

In der Adobe Experience Platform-Benutzeroberfläche können Sie die Attribute und Aktivitäten Ihrer Ziele anzeigen und überwachen. Zu diesen Details gehören der Name und die ID des Ziels, Steuerelemente zum Aktivieren oder Deaktivieren der Ziele und mehr. Details zu Batch-Zielen umfassen auch Metriken für aktivierte Profildatensätze und einen Verlauf der Datenfluss-Vorgänge.

>[!NOTE]
>
>Die Detailseite für Ziele ist Teil des Arbeitsbereichs [!UICONTROL Ziele] im Arbeitsbereich [!DNL Platform] [!DNL UI] . Weitere Informationen finden Sie unter [[!UICONTROL Ziele] Workspace - Übersicht](./destinations-workspace.md) .

## Zieldetails anzeigen {#view-details}

Gehen Sie wie folgt vor, um weitere Details zu einem vorhandenen Ziel anzuzeigen.

1. Melden Sie sich bei [Experience Platform UI](https://platform.adobe.com/) an und wählen Sie **[!UICONTROL Ziele]** aus der linken Navigationsleiste aus. Wählen Sie **[!UICONTROL Browse]** aus der oberen Kopfzeile aus, um Ihre vorhandenen Ziele anzuzeigen.

   ![Ziele durchsuchen](../assets/ui/details-page/browse-destinations.png)

1. Wählen Sie oben links das Filtersymbol ![Filtersymbol](../assets/ui/details-page/filter.png) aus, um das Sortierungsfenster zu öffnen. Das Sortierungsfenster bietet eine Liste aller Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl von Datenflüssen anzuzeigen, die mit dem ausgewählten Ziel verknüpft sind.

   ![Ziele filtern](../assets/ui/details-page/filter-destinations.png)

1. Wählen Sie den Namen des Ziels aus, das Sie anzeigen möchten.

   ![Ziel auswählen](../assets/ui/details-page/destination-select.png)

1. Die Detailseite für das Ziel wird mit den verfügbaren Steuerelementen angezeigt. Wenn Sie die Details eines Batch-Ziels anzeigen, wird auch ein Monitoring-Dashboard angezeigt.

   ![Zieldetails](../assets/ui/details-page/destination-details.png)

## rechte Leiste

In der rechten Leiste werden die grundlegenden Informationen zum ausgewählten Ziel angezeigt.

![rechte Leiste](../assets/ui/details-page/right-sidebar.png)

Die folgende Tabelle enthält die von der rechten Leiste bereitgestellten Steuerelemente und Details:

| Element in der rechten Leiste | Beschreibung |
| --- | --- |
| [!UICONTROL Aktivieren] | Wählen Sie dieses Steuerelement aus, um zu bearbeiten, welche Segmente dem Ziel zugeordnet werden. Weitere Informationen finden Sie in den Handbüchern zu [Aktivieren von Zielgruppendaten für Segment-Streaming-Ziele](./activate-segment-streaming-destinations.md), [Aktivieren von Zielgruppendaten für Batch-profilbasierte Ziele](./activate-batch-profile-destinations.md) und [Aktivieren von Zielgruppendaten für Streaming profilbasierter Ziele](./activate-streaming-profile-destinations.md) . |
| [!UICONTROL Löschen] | Ermöglicht das Löschen dieses Datenflusses und die Aufhebung der Zuordnung der zuvor aktivierten Segmente, falls vorhanden. |
| [!UICONTROL Zielname] | Dieses Feld kann bearbeitet werden, um den Zielnamen zu aktualisieren. |
| [!UICONTROL Beschreibung] | Dieses Feld kann bearbeitet werden, um eine optionale Beschreibung zum Ziel zu aktualisieren oder hinzuzufügen. |
| [!UICONTROL Ziel] | Die Zielplattform, an die Zielgruppen gesendet werden. Weitere Informationen finden Sie im [Zielkatalog](../catalog/overview.md). |
| [!UICONTROL Status] | Gibt an, ob das Ziel aktiviert oder deaktiviert ist. |
| [!UICONTROL Marketing-Aktionen] | Gibt die Marketing-Aktionen (Anwendungsfälle) an, die für dieses Ziel aus Data-Governance-Gründen gelten. |
| [!UICONTROL Kategorie] | Gibt den Zieltyp an. Weitere Informationen finden Sie im [Zielkatalog](../catalog/overview.md). |
| [!UICONTROL Verbindungstyp] | Gibt das Formular an, mit dem Ihre Zielgruppen an das Ziel gesendet werden. Mögliche Werte sind [!UICONTROL Cookie] und [!UICONTROL Profil-based]. |
| [!UICONTROL Häufigkeit] | Gibt an, wie oft die Zielgruppen an das Ziel gesendet werden. Mögliche Werte sind [!UICONTROL Streaming] und [!UICONTROL Batch]. |
| [!UICONTROL Identität] | Stellt den vom Ziel akzeptierten Identitäts-Namespace dar, z. B. `GAID`, `IDFA` oder `email`. Weitere Informationen zu akzeptierten Identitäts-Namespaces finden Sie unter [Übersicht über Identitäts-Namespaces](../../identity-service/namespaces.md). |
| [!UICONTROL Erstellt von] | Gibt den Benutzer an, der dieses Ziel erstellt hat. |
| [!UICONTROL Erstellt] | Gibt den UTC-Datum an, zu dem dieses Ziel erstellt wurde. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Aktiviert]/ DeaktiviertUmschalter

Mit dem Umschalter **[!UICONTROL Aktiviert]/[!UICONTROL Deaktiviert]** können Sie alle Datenexporte an das Ziel starten und anhalten.

![Umschalten aktivieren](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Datenfluss-Abläufe]

Die Registerkarte [!UICONTROL Datenfluss-Ausführung] enthält Metrikdaten zu Ihren Datenflüssen, die an Batch-Ziele ausgeführt werden. Weitere Informationen finden Sie unter [Überwachen von Datenflüssen](monitor-dataflows.md) .

## [!UICONTROL Aktivierungsdaten] {#activation-data}

Der Tab [!UICONTROL Aktivierungsdaten] enthält eine Liste der dem Ziel zugeordneten Segmente, einschließlich des Anfangs- und Enddatums (falls zutreffend). Um die Details zu einem bestimmten Segment anzuzeigen, wählen Sie dessen Namen aus der Liste aus.

![Aktivierungsdaten](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Weitere Informationen zum Erkunden der Detailseite eines Segments finden Sie unter [Übersicht über die Segmentierungsbenutzeroberfläche](../../segmentation/ui/overview.md#segment-details).
