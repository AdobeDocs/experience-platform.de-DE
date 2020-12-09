---
keywords: destinations;destination;destinations detail page;destinations details page
title: Zieldetailseite
seo-title: Zieldetailseite
description: 'Die Detailseite für ein einzelnes Ziel bietet einen Überblick über die Zieldetails, wie den Zielnamen, die Kennung, die dem Ziel zugeordneten Segmente und die Steuerelemente zum Bearbeiten der Aktivierung sowie zum Aktivieren und Deaktivieren des Datenflusses. '
seo-description: 'Die Detailseite für ein einzelnes Ziel bietet einen Überblick über die Zieldetails, wie den Zielnamen, die Kennung, die dem Ziel zugeordneten Segmente und die Steuerelemente zum Bearbeiten der Aktivierung sowie zum Aktivieren und Deaktivieren des Datenflusses. '
translation-type: tm+mt
source-git-commit: 8ac368081c37ca5bfc2cc3382774a912e8ad68eb
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 16%

---


# Zieldetailseite

In der Adobe Experience Platform-Benutzeroberfläche können Sie die Attribute und Aktivitäten Ihrer Ziele Ansichten und überwachen. Zu diesen Details gehören der Name und die ID des Ziels, Steuerelemente zum Aktivieren oder Deaktivieren der Ziele und mehr. Zu den Details zu Stapelzielen gehören auch Metriken für aktivierte Profil-Datensätze und eine Übersicht über die Datenflaumenausführung.

>[!NOTE]
>
>Die Seite mit den Details zu Zielen ist Teil des Arbeitsbereichs &quot; [!UICONTROL Ziele] &quot;in der Plattform-Benutzeroberfläche. See the [[!UICONTROL Destinations] workspace overview](./destinations-workspace.md) for more information.

Navigieren Sie im Arbeitsbereich &quot; **[!UICONTROL Ziele]** &quot;in der Benutzeroberfläche &quot;Plattform&quot;zur Registerkarte &quot; **[!UICONTROL Durchsuchen]** &quot;und wählen Sie den Namen des Ziels aus, das Sie Ansicht haben möchten.

![](../assets/ui/details-page/select-destination.png)

Die Detailseite für das Ziel wird mit den verfügbaren Steuerelementen angezeigt. Wenn Sie die Details eines Stapelziels anzeigen, wird auch ein Dashboard zur Überwachung angezeigt.

![](../assets/ui/details-page/details.png)

Außerdem können Sie auf der Registerkarte &quot;Durchsuchen&quot;den ausgewählten Datenfluss löschen, indem Sie auf das Symbol &quot; ![Papierkorb](../assets/ui/details-page/trash-icon.png) &quot;klicken. Alle Segmente, die für ein Ziel aktiviert wurden, werden vor dem Löschen des Datenflusses nicht zugeordnet.

![](../assets/ui/details-page/delete-flow.png)

## Rechte Leiste

Die rechte Leiste zeigt die grundlegenden Informationen zum Ziel an.

![](../assets/ui/details-page/right-rail.png)

Die folgende Tabelle enthält die Kontrollen und Einzelheiten der rechten Leiste:

| Rechtsschiene | Beschreibung |
| --- | --- |
| [!UICONTROL Aktivieren] | Wählen Sie dieses Steuerelement aus, um zu bearbeiten, welche Segmente dem Ziel zugeordnet werden. Weitere Informationen finden Sie im Handbuch zum [Aktivieren von Segmenten in ein Ziel](./activate-destinations.md) . |
| [!UICONTROL Löschen] | Ermöglicht das Löschen dieses Datenflusses und die Aufhebung der Zuordnung der zuvor aktivierten Segmente, sofern vorhanden. |
| [!UICONTROL Zielname] | Dieses Feld kann bearbeitet werden, um den Namen des Ziels zu aktualisieren. |
| [!UICONTROL Beschreibung] | Dieses Feld kann bearbeitet werden, um eine optionale Beschreibung zu aktualisieren oder dem Ziel hinzuzufügen. |
| [!UICONTROL Ziel] | Die Zielplattform, an die Zielgruppen gesendet werden. See the [destinations catalog](../catalog/overview.md) for more information. |
| [!UICONTROL Status] | Gibt an, ob das Ziel aktiviert oder deaktiviert ist. |
| [!UICONTROL Marketing-Aktionen] | Zeigt die Marketingaktionen (Anwendungsfälle) an, die für dieses Ziel zu Zwecken der Datenverwaltung gelten. |
| [!UICONTROL Kategorie] | Gibt den Zieltyp an. See the [destinations catalog](../catalog/overview.md) for more information. |
| [!UICONTROL Verbindungstyp] | Gibt das Formular an, mit dem Ihre Audiencen an das Ziel gesendet werden. Mögliche Werte sind &quot;[!UICONTROL Cookie]&quot;und &quot;[!UICONTROL Profil-basiert]&quot;. |
| [!UICONTROL Häufigkeit] | Gibt an, wie oft die Zielgruppen an das Ziel gesendet werden. Mögliche Werte sind &quot;[!UICONTROL Streaming]&quot;und &quot;[!UICONTROL Batch]&quot;. |
| [!UICONTROL Identität] | Stellt den vom Ziel akzeptierten Identitäts-Namensraum dar, z. B. `GAID`, `IDFA`oder `email`. For more information on accepted identity namespaces, see the [identity namespace overview](../../identity-service/namespaces.md). |
| [!UICONTROL Erstellt von] | Gibt den Benutzer an, der dieses Ziel erstellt hat. |
| [!UICONTROL Erstellt] | Gibt die UTC-Zeit an, zu der dieses Ziel erstellt wurde. |

## [!UICONTROL Umschalter]/[!UICONTROL Deaktiviert]

Sie können den **[!UICONTROL Umschalter &quot;Aktiviert]/[!UICONTROL Deaktiviert]** &quot;zum Beginn verwenden und alle Datenexporte an das Ziel anhalten.

![](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Datenaflow-Ausführung]

Die Registerkarte &quot; [!UICONTROL Datenaflow-Ausführung] &quot;enthält Metrikdaten zu den Datenaflow-Aufrufen zu Stapelzielen. Es wird eine Liste der einzelnen Vorgänge und der zugehörigen Metriken sowie die folgenden Summen für Profil-Datensätze angezeigt:

* **[!UICONTROL Profil-Datensätze aktiviert]**: Die Gesamtanzahl der Profil-Datensätze, die zur Aktivierung erstellt oder aktualisiert wurden.
* **[!UICONTROL Profil-Datensätze übersprungen]**:  Die Gesamtanzahl der Profil-Datensätze, die aufgrund von Profil-Ausstiegen oder fehlenden Attributen für die Aktivierung übersprungen werden.

![](../assets/ui/details-page/dataflow-runs.png)

>[!NOTE]
>
>Dataflow-Ausläufe werden basierend auf der Häufigkeit des Planvorgangs des Zieldatafloms generiert. Für jede auf ein Segment angewendete Zusammenführungsrichtlinie wird ein separater Datendurchlauf ausgeführt.

Um die Details eines bestimmten Datenflusses Ansicht, wählen Sie die Ausführungszeit des Beginns aus der Liste aus. Die Detailseite für einen Datenfluss enthält weitere Informationen, wie z. B. die Größe der verarbeiteten Daten und eine Liste der Fehler, die bei der Fehlerdiagnose aufgetreten sind.

![](../assets/ui/details-page/dataflow.png)

## [!UICONTROL Aktivierungen]

Auf der Registerkarte &quot;Daten [!UICONTROL zu] Aktivierungen&quot;wird eine Liste der dem Ziel zugeordneten Segmente angezeigt, einschließlich des Beginns- und Enddatums (falls zutreffend). Um die Details zu einem bestimmten Segment Ansicht, wählen Sie dessen Namen in der Liste aus.

![](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Weitere Informationen zum Erforschen der Detailseite eines Segments finden Sie in der Übersicht über die [Segmentierungsoberfläche](../../segmentation/ui/overview.md#segment-details).

## Nächste Schritte

In diesem Dokument wurden die Funktionen der Seite mit den Zieldetails behandelt. Weitere Informationen zum Verwalten von Zielen in der Benutzeroberfläche finden Sie in der Übersicht im Arbeitsbereich &quot; [[!UICONTROL Ziele] &quot;](./destinations-workspace.md).