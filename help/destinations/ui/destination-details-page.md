---
keywords: Ziele;Ziel;Ziel;Detailseite der Ziele;Detailseite der Ziele
title: Ansichten-Zieldetails
description: 'Die Detailseite für ein einzelnes Ziel bietet einen Überblick über die Zieldetails. Zu den Zieldetails gehören der Zielname, die ID, die dem Ziel zugeordneten Segmente und die Steuerelemente zum Bearbeiten der Aktivierung sowie zum Aktivieren und Deaktivieren des Datenflusses. '
seo-description: 'Die Detailseite für ein einzelnes Ziel bietet einen Überblick über die Zieldetails. Zu den Zieldetails gehören der Zielname, die ID, die dem Ziel zugeordneten Segmente und die Steuerelemente zum Bearbeiten der Aktivierung sowie zum Aktivieren und Deaktivieren des Datenflusses. '
translation-type: tm+mt
source-git-commit: 49905060a18fc94fe524401fb3cf86f212b639ce
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 5%

---


# Ansichten-Zieldetails

## Übersicht {#overview}

In der Adobe Experience Platform-Benutzeroberfläche können Sie die Attribute und Aktivitäten Ihrer Ziele Ansichten und überwachen. Zu diesen Details gehören der Name und die ID des Ziels, Steuerelemente zum Aktivieren oder Deaktivieren der Ziele und mehr. Zu den Details zu Stapelzielen gehören auch Metriken für aktivierte Profil-Datensätze und eine Übersicht über die Datenflaumenausführung.

>[!NOTE]
>
>Die Seite mit den Details zu Zielen ist Teil des Arbeitsbereichs [!UICONTROL Ziele] in der Plattform-Benutzeroberfläche. Weitere Informationen finden Sie unter [[!UICONTROL Ziele] Arbeitsbereichübersicht](./destinations-workspace.md).

Navigieren Sie im Arbeitsbereich **[!UICONTROL Ziele]** der Plattform-Benutzeroberfläche zur Registerkarte **[!UICONTROL Durchsuchen]** und wählen Sie den Namen des Ziels aus, das Sie Ansicht haben möchten.

![](../assets/ui/details-page/select-destination.png)

Die Detailseite für das Ziel wird mit den verfügbaren Steuerelementen angezeigt. Wenn Sie die Details eines Stapelziels anzeigen, wird auch ein Dashboard zur Überwachung angezeigt.

![](../assets/ui/details-page/details.png)

Darüber hinaus können Sie auf der Registerkarte &quot;Durchsuchen&quot;den ausgewählten Datenfluss löschen, indem Sie das Symbol ![Papierkorb](../assets/ui/details-page/trash-icon.png) auswählen. Alle Segmente, die für Ziele aktiviert wurden, werden vor dem Löschen des Datenflusses nicht zugeordnet.

![](../assets/ui/details-page/delete-flow.png)

## Rechte Leiste

Die rechte Leiste zeigt die grundlegenden Informationen zum Ziel an.

![](../assets/ui/details-page/right-rail.png)

Die folgende Tabelle enthält die Kontrollen und Einzelheiten der rechten Leiste:

| Rechtsschiene | Beschreibung |
| --- | --- |
| [!UICONTROL Aktivieren] | Wählen Sie dieses Steuerelement aus, um zu bearbeiten, welche Segmente dem Ziel zugeordnet werden. Weitere Informationen finden Sie im Handbuch [Aktivieren von Segmenten in ein Ziel](./activate-destinations.md). |
| [!UICONTROL Löschen] | Ermöglicht das Löschen dieses Datenflusses und die Aufhebung der Zuordnung der zuvor aktivierten Segmente, sofern vorhanden. |
| [!UICONTROL Zielname] | Dieses Feld kann bearbeitet werden, um den Namen des Ziels zu aktualisieren. |
| [!UICONTROL Beschreibung] | Dieses Feld kann bearbeitet werden, um eine optionale Beschreibung zu aktualisieren oder dem Ziel hinzuzufügen. |
| [!UICONTROL Ziel] | Die Zielplattform, an die Zielgruppen gesendet werden. Weitere Informationen finden Sie im Katalog [Ziele](../catalog/overview.md). |
| [!UICONTROL Status] | Gibt an, ob das Ziel aktiviert oder deaktiviert ist. |
| [!UICONTROL Marketing-Aktionen] | Zeigt die Marketingaktionen (Anwendungsfälle) an, die für dieses Ziel zu Zwecken der Datenverwaltung gelten. |
| [!UICONTROL Kategorie] | Gibt den Zieltyp an. Weitere Informationen finden Sie im Katalog [Ziele](../catalog/overview.md). |
| [!UICONTROL Verbindungstyp] | Gibt das Formular an, mit dem Ihre Audiencen an das Ziel gesendet werden. Mögliche Werte sind &quot;[!UICONTROL Cookie]&quot;und &quot;[!UICONTROL Profil-basiert]&quot;. |
| [!UICONTROL Häufigkeit] | Gibt an, wie oft die Zielgruppen an das Ziel gesendet werden. Mögliche Werte sind &quot;[!UICONTROL Streaming]&quot;und &quot;[!UICONTROL Batch]&quot;. |
| [!UICONTROL Identität] | Stellt den vom Ziel akzeptierten Identitäts-Namensraum dar, z. B. `GAID`, `IDFA` oder `email`. Weitere Informationen zu akzeptierten Identitäts-Namensräumen finden Sie unter [Übersicht über Identitäts-Namensraum](../../identity-service/namespaces.md). |
| [!UICONTROL Erstellt von] | Gibt den Benutzer an, der dieses Ziel erstellt hat. |
| [!UICONTROL Erstellt] | Gibt die UTC-Zeit an, zu der dieses Ziel erstellt wurde. |

## [!UICONTROL Aktiviert]/ Deaktiviert

Sie können den Umschalter **[!UICONTROL Aktiviert]/[!UICONTROL Deaktiviert]** verwenden und alle Datenexporte an das Ziel anhalten.

![](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Datenaflow-Ausführung]

Die Registerkarte [!UICONTROL Datenaflow-Ausführung] enthält Metrikdaten zu Ihren Datenaflow-Aufrufen zu Stapelzielen. Es wird eine Liste der einzelnen Vorgänge und der zugehörigen Metriken sowie die folgenden Summen für Profil-Datensätze angezeigt:

* **[!UICONTROL Profil-Datensätze aktiviert]**: Die Gesamtanzahl der Profil-Datensätze, die zur Aktivierung erstellt oder aktualisiert wurden.
* **[!UICONTROL Profil-Datensätze übersprungen]**: Die Gesamtanzahl der Profil-Datensätze, die aufgrund von Profil-Ausstiegen oder fehlenden Attributen für die Aktivierung übersprungen werden.

![](../assets/ui/details-page/dataflow-runs.png)

>[!NOTE]
>
>Dataflow-Ausläufe werden basierend auf der Häufigkeit des Planvorgangs des Zieldatafloms generiert. Für jede auf ein Segment angewendete Zusammenführungsrichtlinie wird ein separater Datendurchlauf ausgeführt.

Um die Details eines bestimmten Datenflusses Ansicht, wählen Sie die Ausführungszeit des Beginns aus der Liste aus. Die Detailseite für einen Datenfluss enthält weitere Informationen, wie z. B. die Größe der verarbeiteten Daten und eine Liste der Fehler, die bei der Fehlerdiagnose aufgetreten sind.

![](../assets/ui/details-page/dataflow.png)

## [!UICONTROL Aktivierungen] {#activation-data}

Auf der Registerkarte [!UICONTROL Aktivierung data] wird eine Liste von Segmenten angezeigt, die dem Ziel zugeordnet wurden, einschließlich des Beginn- und Enddatums (falls zutreffend). Um die Details zu einem bestimmten Segment Ansicht, wählen Sie dessen Namen in der Liste aus.

![](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Weitere Informationen zum Erforschen der Detailseite eines Segments finden Sie in der [Übersicht über die Segmentierungsoberfläche](../../segmentation/ui/overview.md#segment-details).

## Nächste Schritte

In diesem Dokument wurden die Funktionen der Seite mit den Zieldetails behandelt. Weitere Informationen zum Verwalten von Zielen in der Benutzeroberfläche finden Sie in der Übersicht auf der Arbeitsfläche [[!UICONTROL Ziele].](./destinations-workspace.md)