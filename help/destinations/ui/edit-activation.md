---
keywords: Aktivierung bearbeiten, Ziel bearbeiten, Ziel bearbeiten
title: Bearbeiten von Aktivierungsdatenflüssen
type: Tutorial
description: Gehen Sie wie in diesem Artikel beschrieben vor, um einen vorhandenen Aktivierungsdatenfluss in Adobe Experience Platform zu bearbeiten.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: ec87cb1c8755f52233a5725aa3bb0c80a135d60c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Bearbeiten von Aktivierungsdatenflüssen {#edit-activation-flows}

In Adobe Experience Platform können Sie verschiedene Komponenten vorhandener Aktivierungsdatenflüsse für Ziele konfigurieren, z. B.:

* [Aktivieren oder Deaktivieren](#enable-disable-dataflows) von Aktivierungsdatenflüssen
* [Hinzufügen zusätzlicher Zielgruppen](#add-audiences) zu Aktivierungsdatenflüssen
* [Zugeordnete Attribute und Identitäten bearbeiten](#edit-mapped-attributes)
* [Bearbeiten des Aktivierungsplans und der Exporthäufigkeit](#edit-schedule-frequency)
* [Hinzufügen zusätzlicher Datensätze](#add-datasets) zum Aktivierungs-Workflow
* [Marketing-Aktionen bearbeiten](#edit-marketing-actions) für Ihre Aktivierungsdatenflüsse
* [Zugriffskennzeichnungen anwenden](#apply-access-labels) auf exportierte Daten
* [Namen und Beschreibungen &#x200B;](#edit-names-descriptions) Aktivierungsdatenflüsse bearbeiten)

## Durchsuchen von Aktivierungsdatenflüssen {#browse-activation-dataflows}

Gehen Sie wie folgt vor, um Ihre vorhandenen Aktivierungsdatenflüsse zu durchsuchen und den Datenfluss zu identifizieren, den Sie bearbeiten möchten.

1. Melden Sie sich bei der [Experience Platform-Benutzeroberfläche](https://platform.adobe.com/) an und wählen Sie **[!UICONTROL Ziele]** über die linke Navigationsleiste aus. Wählen Sie **[!UICONTROL Durchsuchen]** in der oberen Kopfzeile aus, um Ihre vorhandenen Ziel-Datenflüsse anzuzeigen.

   ![Ziele durchsuchen](../assets/ui/edit-activation/browse-destinations.png)

2. Wählen Sie das Symbol ![Filter](../../images/icons/filter.png) oben links, um das Sortier-Bedienfeld zu öffnen. Das Sortier-Bedienfeld bietet eine Liste aller Ihrer Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl von Datenflüssen anzuzeigen, die mit dem ausgewählten Ziel verknüpft sind.

   ![Ziele filtern](../assets/ui/edit-activation/filter-destinations.png)

3. Wählen Sie den Namen des Ziel-Datenflusses aus, den Sie bearbeiten möchten.

   ![Auswählen des Ziels](../assets/ui/edit-activation/destination-select.png)

4. Die **[!UICONTROL Datenflussausführungen]** für das Ziel wird mit den verfügbaren Steuerelementen angezeigt. Je nach Zieltyp können Sie verschiedene Datenflussvorgänge ausführen. Siehe die nächsten Abschnitte für jede unterstützte Datenflussoperation.

## Aktivieren oder Deaktivieren von Aktivierungsdatenflüssen {#enable-disable-dataflows}

Verwenden Sie den Umschalter **[!UICONTROL Aktiviert]/[!UICONTROL Deaktiviert]**, um alle Datenexporte an das Ziel zu starten oder anzuhalten.

![Bild der Experience Platform-Benutzeroberfläche mit dem Umschalter für die Ausführung eines aktivierten/deaktivierten Datenflusses.](../assets/ui/edit-activation/enable-toggle.png)

## Hinzufügen von Zielgruppen zu einem Aktivierungsdatenfluss {#add-audiences}

Wählen **[!UICONTROL Zielgruppen aktivieren]** in der rechten Leiste aus, um zu ändern, welche Zielgruppen an das Ziel gesendet werden sollen. Diese Aktion führt Sie zum Aktivierungs-Workflow.

![Bild der Experience Platform-Benutzeroberfläche mit der Option zum Aktivieren von Zielgruppen-Datenflüssen.](../assets/ui/edit-activation/activate-audiences.png)

Im Schritt **[!UICONTROL Auswählen]** Zielgruppen“ des Aktivierungs-Workflows können Sie vorhandene Zielgruppen entfernen oder neue Zielgruppen zum Aktivierungs-Workflow hinzufügen.

Der Aktivierungs-Workflow unterscheidet sich je nach Zieltyp geringfügig. Weitere Informationen zu den Aktivierungs-Workflows für die einzelnen Zieltypen finden Sie in den folgenden Handbüchern:

* [Aktivieren von Zielgruppen für Streaming](./activate-segment-streaming-destinations.md)Ziele (z. B. Facebook oder Twitter);
* [Aktivieren von Zielgruppen für Batch-Profil-](./activate-batch-profile-destinations.md) (z. B. Amazon S3 oder Oracle Eloqua);
* [Aktivieren von Zielgruppen für Exportziele von Streaming-Profilen](./activate-streaming-profile-destinations.md) (z. B. HTTP-API oder Amazon Kinesis).

## Bearbeiten des Aktivierungsplans und der Exporthäufigkeit {#edit-schedule-frequency}

Wählen **[!UICONTROL Zielgruppen aktivieren]** in der rechten Leiste aus. Diese Aktion führt Sie zum Aktivierungs-Workflow.

![Bild der Experience Platform-Benutzeroberfläche mit der Option zum Aktivieren von Zielgruppen-Datenflüssen.](../assets/ui/edit-activation/activate-audiences.png)

Wählen Sie **[!UICONTROL Schritt]** Planung“ im Aktivierungs-Workflow aus, um den Aktivierungsplan zu bearbeiten und die Exportfrequenz für Ihren Datenfluss festzulegen. In diesem Schritt können Sie konfigurieren, wie oft Daten an das Ziel exportiert werden.

Im Schritt **[!UICONTROL Planung]** des Aktivierungs-Workflows haben Sie folgende Möglichkeiten:
* Anpassen der Exportfrequenz.
* Festlegen oder Ändern des Start- und Enddatums für den Aktivierungsdatenfluss und mehr.

Die Planungsvorgänge, die Sie ausführen können, variieren geringfügig je nach Zieltyp. Weitere Informationen zu den Aktivierungs-Workflows für die einzelnen Zieltypen finden Sie in den folgenden Handbüchern:

* [Aktivieren von Zielgruppen für Streaming](./activate-segment-streaming-destinations.md)Ziele (z. B. Facebook oder Twitter);
* [Aktivieren von Zielgruppen für Batch-Profil-](./activate-batch-profile-destinations.md) (z. B. Amazon S3 oder Oracle Eloqua);
* [Aktivieren von Zielgruppen für Exportziele von Streaming-Profilen](./activate-streaming-profile-destinations.md) (z. B. HTTP-API oder Amazon Kinesis).

## Zugeordnete Attribute und Identitäten bearbeiten {#edit-mapped-attributes}

Wählen **[!UICONTROL Zielgruppen aktivieren]** in der rechten Leiste aus. Diese Aktion führt Sie zum Aktivierungs-Workflow.

![Bild der Experience Platform-Benutzeroberfläche mit der Option zum Aktivieren von Zielgruppen-Datenflüssen.](../assets/ui/edit-activation/activate-audiences.png)

Wählen Sie im Aktivierungs **[!UICONTROL Workflow den Schritt]** Zuordnung“ aus, um die zugeordneten Attribute und Identitäten für Ihren Aktivierungsdatenfluss zu bearbeiten. Auf diese Weise können Sie anpassen, welche Profilattribute und Identitäten an das Ziel exportiert werden sollen.

Im Schritt **[!UICONTROL Zuordnung]** des Aktivierungs-Workflows haben Sie folgende Möglichkeiten:

* Hinzufügen neuer Attribute oder Identitäten zur Zuordnung.
* Entfernen vorhandener Attribute oder Identitäten aus der Zuordnung.
* Passen Sie die Reihenfolge der Zuordnungen an, um die Spaltenreihenfolge in exportierten Dateien zu definieren.

Der Aktivierungs-Workflow unterscheidet sich je nach Zieltyp geringfügig. Weitere Informationen zu den Aktivierungs-Workflows für die einzelnen Zieltypen finden Sie in den folgenden Handbüchern:

* [Aktivieren von Zielgruppen für Streaming](./activate-segment-streaming-destinations.md)Ziele (z. B. Facebook oder Twitter);
* [Aktivieren von Zielgruppen für Batch-Profil-](./activate-batch-profile-destinations.md) (z. B. Amazon S3 oder Oracle Eloqua);
* [Aktivieren von Zielgruppen für Exportziele von Streaming-Profilen](./activate-streaming-profile-destinations.md) (z. B. HTTP-API oder Amazon Kinesis).

## Hinzufügen von Datensätzen zu einem Aktivierungsdatenfluss {#add-datasets}

Wählen **[!UICONTROL Datensätze exportieren]** in der rechten Leiste aus, um zusätzliche Datensätze auszuwählen, die an Ihr Ziel exportiert werden sollen. Diese Option führt Sie zum [Workflow für den Datensatzexport](export-datasets.md).

>[!NOTE]
>
>Diese Option ist nur für (Ziele[&#x200B; die den Datensatzexport unterstützen](export-datasets.md#supported-destinations) sichtbar.

![Bild der Experience Platform-Benutzeroberfläche mit der Option zur Ausführung des Datenflusses für Datensätze exportieren.](../assets/ui/edit-activation/export-datasets.png)

## [!BADGE Beta]{type=Informative} Marketing-Aktionen bearbeiten {#edit-marketing-actions}

>[!NOTE]
>
>Diese Funktion befindet sich derzeit in der **Betaversion**. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff zu erhalten.

Sie können Marketing-Aktionen hinzufügen oder entfernen, die Sie beim erstmaligen Herstellen einer Verbindung mit dem Ziel eingerichtet haben.

Wählen Sie **[!UICONTROL Marketing-Aktionen bearbeiten]** in der rechten Leiste aus, um den Auswahlbildschirm für Marketing-Aktionen zu öffnen.

![Bild der Experience Platform-Benutzeroberfläche mit der Option „Marketing-Aktionen bearbeiten“.](../assets/ui/edit-activation/edit-marketing-actions.png)

Wählen Sie die entsprechenden Marketing-Aktionen aus und klicken Sie dann auf **[!UICONTROL Speichern]**, um die Änderungen anzuwenden.

![Bild der Experience Platform-Benutzeroberfläche mit dem Bildschirm „Marketing-Aktionen bearbeiten“.](../assets/ui/edit-activation/edit-marketing-actions-screen.png)


## Anwenden von Zugriffs-Labels {#apply-access-labels}

Wählen Sie **[!UICONTROL Zugriffskennzeichnungen anwenden]** aus, um die Datennutzungskennzeichnungen für die exportierten Daten zu bearbeiten. Weitere Informationen finden [&#x200B; in der Dokumentation &#x200B;](../../data-governance/labels/overview.md) Datennutzungskennzeichnungen .

![Bild der Experience Platform-Benutzeroberfläche mit der Option zur Ausführung des Datenflusses für Datensätze exportieren.](../assets/ui/edit-activation/apply-access-labels.png)

## Namen und Beschreibungen von Aktivierungsdatenflüssen bearbeiten {#edit-names-descriptions}

Um den Namen und die Beschreibung des Aktivierungsdatenflusses zu bearbeiten, verwenden Sie die Felder **[!UICONTROL Zielname]** und **[!UICONTROL Beschreibung]**.

![Zieldetails](../assets/ui/edit-activation/edit-destination-name-description.png)

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie erfolgreich den Arbeitsbereich **[!UICONTROL Ziele]** verwendet, um vorhandene Zieldatenflüsse zu aktualisieren.

Weitere Informationen zu Zielen finden Sie unter [Ziele - Übersicht](../catalog/overview.md).
