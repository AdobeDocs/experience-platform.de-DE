---
keywords: Ziele;Ziel;Ziel;Detailseite der Ziele;Detailseite der Ziele
title: Ansichten-Zieldetails
description: 'Die Detailseite für ein einzelnes Ziel bietet einen Überblick über die Zieldetails. Zu den Zieldetails gehören der Zielname, die ID, die dem Ziel zugeordneten Segmente und die Steuerelemente zum Bearbeiten der Aktivierung sowie zum Aktivieren und Deaktivieren des Datenflusses. '
seo-description: Die Detailseite für ein einzelnes Ziel bietet einen Überblick über die Zieldetails. Zu den Zieldetails gehören der Zielname, die ID, die dem Ziel zugeordneten Segmente und die Steuerelemente zum Bearbeiten der Aktivierung sowie zum Aktivieren und Deaktivieren des Datenflusses.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
translation-type: tm+mt
source-git-commit: cc432f7c07f0f82deec653864154016638ec8138
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 5%

---

# Ansichten-Zieldetails

## Übersicht {#overview}

In der Adobe Experience Platform-Benutzeroberfläche können Sie die Attribute und Aktivitäten Ihrer Ziele Ansichten und überwachen. Zu diesen Details gehören der Name und die ID des Ziels, Steuerelemente zum Aktivieren oder Deaktivieren der Ziele und mehr. Zu den Details zu Stapelzielen gehören auch Metriken für aktivierte Profil-Datensätze und eine Übersicht über die Datenflaumenausführung.

>[!NOTE]
>
>Die Seite mit den Details zu Zielen ist Teil des Arbeitsbereichs [!UICONTROL Ziele] im [!DNL Platform] [!DNL UI]. Weitere Informationen finden Sie unter [[!UICONTROL Ziele] Arbeitsbereichübersicht](./destinations-workspace.md).

## Ansicht-Zieldetails {#view-details}

Gehen Sie wie folgt vor, um weitere Informationen zu einem vorhandenen Ziel Ansicht.

1. Melden Sie sich bei [Experience Platform UI](https://platform.adobe.com/) an und wählen Sie **[!UICONTROL Ziele]** in der linken Navigationsleiste aus. Wählen Sie **[!UICONTROL Durchsuchen]** aus der oberen Kopfzeile, um Ihre bestehenden Ziele Ansicht.

   ![Ziele durchsuchen](../assets/ui/details-page/browse-destinations.png)

1. Wählen Sie oben links das Filtersymbol ![Filtersymbol](../assets/ui/details-page/filter.png) aus, um das Sortierfeld zu starten. Der Bereich &quot;Sortieren&quot;enthält eine Liste aller Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl an Datenflüssen anzuzeigen, die mit dem ausgewählten Ziel verknüpft sind.

   ![Ziele filtern](../assets/ui/details-page/filter-destinations.png)

1. Wählen Sie den Namen des Ziels aus, das Sie Ansichten vornehmen möchten.

   ![Ziel auswählen](../assets/ui/details-page/destination-select.png)

1. Die Detailseite für das Ziel wird mit den verfügbaren Steuerelementen angezeigt. Wenn Sie die Details eines Stapelziels anzeigen, wird auch ein Dashboard zur Überwachung angezeigt.

   ![Zieldetails](../assets/ui/details-page/destination-details.png)

## Rechte Leiste

Die rechte Leiste zeigt die grundlegenden Informationen zum ausgewählten Ziel an.

![rechte Schiene](../assets/ui/details-page/right-sidebar.png)

Die folgende Tabelle enthält die Kontrollen und Einzelheiten der rechten Leiste:

| Rechte Leiste | Beschreibung |
| --- | --- |
| [!UICONTROL Aktivieren] | Wählen Sie dieses Steuerelement aus, um zu bearbeiten, welche Segmente dem Ziel zugeordnet werden. Weitere Informationen finden Sie im Handbuch [Aktivieren von Segmenten in ein Ziel](./activate-destinations.md). |
| [!UICONTROL Löschen] | Ermöglicht das Löschen dieses Datenflusses und die Aufhebung der Zuordnung der zuvor aktivierten Segmente, sofern vorhanden. |
| [!UICONTROL Zielname] | Dieses Feld kann bearbeitet werden, um den Namen des Ziels zu aktualisieren. |
| [!UICONTROL Beschreibung] | Dieses Feld kann bearbeitet werden, um eine optionale Beschreibung zu aktualisieren oder dem Ziel hinzuzufügen. |
| [!UICONTROL Ziel] | Die Zielplattform, an die Zielgruppen gesendet werden. Weitere Informationen finden Sie im Katalog [Ziele](../catalog/overview.md). |
| [!UICONTROL Status] | Gibt an, ob das Ziel aktiviert oder deaktiviert ist. |
| [!UICONTROL Marketing-Aktionen] | Zeigt die Marketingaktionen (Anwendungsfälle) an, die für dieses Ziel zu Zwecken der Datenverwaltung gelten. |
| [!UICONTROL Kategorie] | Gibt den Zieltyp an. Weitere Informationen finden Sie im Katalog [Ziele](../catalog/overview.md). |
| [!UICONTROL Verbindungstyp] | Gibt das Formular an, mit dem Ihre Audiencen an das Ziel gesendet werden. Mögliche Werte sind [!UICONTROL Cookie] und [!UICONTROL Profil-basiert]. |
| [!UICONTROL Häufigkeit] | Gibt an, wie oft die Zielgruppen an das Ziel gesendet werden. Mögliche Werte sind [!UICONTROL Streaming] und [!UICONTROL Stapel]. |
| [!UICONTROL Identität] | Stellt den vom Ziel akzeptierten Identitäts-Namensraum dar, z. B. `GAID`, `IDFA` oder `email`. Weitere Informationen zu akzeptierten Identitäts-Namensräumen finden Sie unter [Übersicht über Identitäts-Namensraum](../../identity-service/namespaces.md). |
| [!UICONTROL Erstellt von] | Gibt den Benutzer an, der dieses Ziel erstellt hat. |
| [!UICONTROL Erstellt] | Gibt die UTC-Zeit an, zu der dieses Ziel erstellt wurde. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Aktiviert]/ Deaktiviert

Sie können den Umschalter **[!UICONTROL Aktiviert]/[!UICONTROL Deaktiviert]** verwenden und alle Datenexporte an das Ziel anhalten.

![Deaktivieren](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Datenaflow-Ausführung]

Die Registerkarte [!UICONTROL Datenaflow-Ausführung] enthält Metrikdaten zu Ihren Datenaflow-Aufrufen zu Stapelzielen. Weitere Informationen finden Sie unter [Monitordataflows](monitor-dataflows.md).

## [!UICONTROL Aktivierungen] {#activation-data}

Auf der Registerkarte [!UICONTROL Aktivierung data] wird eine Liste von Segmenten angezeigt, die dem Ziel zugeordnet wurden, einschließlich des Beginn- und Enddatums (falls zutreffend). Um die Details zu einem bestimmten Segment Ansicht, wählen Sie dessen Namen in der Liste aus.

![Aktivierungen](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Weitere Informationen zum Erforschen der Detailseite eines Segments finden Sie in der [Übersicht über die Segmentierungsoberfläche](../../segmentation/ui/overview.md#segment-details).
