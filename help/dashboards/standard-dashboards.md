---
title: Standard-Dashboards
description: Erfahren Sie, wie Sie benutzerdefinierte Dashboards erstellen und verwalten, in denen Sie maßgeschneiderte Widgets erstellen, hinzufügen und bearbeiten können, um Schlüsselmetriken zu visualisieren.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 1%

---

# Standard-Dashboards

Verwenden Sie Adobe Experience Platform-Dashboards, um mithilfe der Dashboards-Funktion Einblicke zu beschleunigen und die Visualisierung anzupassen. Mit dieser Funktion können Sie benutzerdefinierte Dashboards erstellen und verwalten, in denen Sie maßgeschneiderte Widgets erstellen, hinzufügen und bearbeiten können, um für Ihr Unternehmen relevante Schlüsselmetriken zu visualisieren.


<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Erstellen eines benutzerdefinierten Dashboards

Um ein benutzerdefiniertes Dashboard zu erstellen, navigieren Sie zunächst zum Dashboard-Inventar. Wählen Sie **[!UICONTROL Dashboards]** aus dem linken Navigationsbereich der Benutzeroberfläche von Experience Platform und anschließend **[!UICONTROL Create dashboard]** aus.

![Das Dashboard-Inventar mit Dashboards im linken Navigationsbereich und hervorgehobener Option „Dashboard erstellen“.](./images/standard-dashboards/create-dashboard.png)

Bevor Sie ein benutzerdefiniertes Dashboard hinzufügen, ist das Dashboard-Inventar leer und zeigt „Keine Dashboards gefunden“ an. Nachricht. Nach der Erstellung werden alle Ihre Dashboards im Dashboard-Inventar aufgelistet.

<!-- >[!NOTE]
>
>To edit an existing dashboard, select the dashboard name from the inventory list followed by the pencil icon (![A pencil icon.](/help/images/icons/edit.png))
>![A custom inventory listed in the dashboard inventory.](./images/standard-dashboards/dashbaord-inventory.png "A custom inventory listed in the dashboard inventory."){width="100" zoomable="yes"} -->

Das Dialogfeld [!UICONTROL Create dashboard] wird angezeigt. Geben Sie einen benutzerfreundlichen, beschreibenden Namen für die Sammlung von Widgets ein, die Sie erstellen möchten, und wählen Sie **[!UICONTROL Save]** aus.

![Das Dialogfeld „Dashboard erstellen“](./images/standard-dashboards/create-dashboard-dialog.png)

Benutzende, die die Data Distiller SKU erworben haben, haben die Möglichkeit, benutzerdefinierte SQL-Abfragen zu verwenden, um ihre Einblicke zu erstellen. Anweisungen zu diesem Workflow finden [&#x200B; in der &#x200B;](./sql-insights-query-pro-mode/overview.md)Query Pro-Modus - Übersicht“.

Das neu erstellte leere Dashboard wird mit dem ausgewählten Namen oben links in der Ansicht angezeigt.

## Erstellen eines Widgets {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Maximale Anzahl an Widgets"
>abstract="Dashboard-Service unterstützt bis zu zehn Widgets. Nachdem Sie zehn Widgets zu Ihrem Dashboard hinzugefügt haben, ist die Option [!UICONTROL Add new widget] deaktiviert und wird grau angezeigt."

Wählen Sie in Ihrer neuen Dashboard-Ansicht die Option **[!UICONTROL Add new widget]** aus, um mit der Erstellung des Widgets zu beginnen.

>[!IMPORTANT]
>
>Jedes Dashboard unterstützt bis zu zehn Widgets. Nachdem Sie zehn Widgets zu Ihrem Dashboard hinzugefügt haben, ist die Option [!UICONTROL Add new widget] deaktiviert und wird grau angezeigt.

![Das neue leere Dashboard mit hervorgehobener Option „Neues Widget hinzufügen“.](./images/standard-dashboards/add-new-widget.png)

### Widget-Composer

Der Widget-Composer-Arbeitsbereich wird angezeigt. Wählen Sie als Nächstes **[!UICONTROL Select data]** aus, um das Datenmodell auszuwählen, aus dem Sie Ihren Widgets Attribute hinzufügen möchten.

![Der Widget-Composer-Arbeitsbereich.](./images/standard-dashboards/widget-composer.png)

#### Datenmodell auswählen {#select-data-model}

Das Dialogfeld [!UICONTROL Select data model] wird angezeigt. Wählen Sie ein Datenmodell aus der linken Spalte aus, um eine Vorschauliste aller verfügbaren Tabellen anzuzeigen. Das vorkonfigurierte Datenmodell für Real-Time Customer Data Platform heißt [!UICONTROL CDPInsights].

>[!TIP]
>
>Wählen Sie das Informationssymbol (![Informationssymbol) aus.](/help/images/icons/info.png)), um den vollständigen Datenmodellnamen anzuzeigen, wenn er für die Anzeige in der Datenleiste zu lang ist.

![Das Dialogfeld „Daten auswählen“](./images/standard-dashboards/select-data-model-dialog.png)

Die Vorschauliste enthält Details zu den im Datenmodell enthaltenen Tabellen. Die nachstehende Tabelle enthält Beschreibungen der Spaltenfelder und ihrer potenziellen Werte.

| Spaltenfeld | Beschreibung |
|---|---|
| [!UICONTROL Title] | Der Name der Tabelle. |
| [!UICONTROL Table type] | Der Typ der Tabelle. Mögliche Typen sind: `fact`, `dimension` und `none`. |
| [!UICONTROL Records] | Die Anzahl der Datensätze, die mit der ausgewählten Tabelle verknüpft sind. |
| [!UICONTROL Lookups] | Die Anzahl der mit der ausgewählten Tabelle verbundenen Tabellen. |
| [!UICONTROL Attributes] | Die Anzahl der Attribute für die ausgewählte Tabelle. |

Wählen Sie **[!UICONTROL Next]** aus, um Ihre Auswahl des Datenmodells zu bestätigen. Die nächste Ansicht zeigt eine Liste der verfügbaren Tabellen in der linken Leiste an. Wählen Sie eine Tabelle aus, um eine umfassende Aufschlüsselung der in Ihrer ausgewählten Tabelle enthaltenen Daten anzuzeigen.

### Widget befüllen {#populate-widget}

Das Bedienfeld [!UICONTROL Preview] enthält Registerkarten für [!UICONTROL Sample records] und [!UICONTROL Attributes]. Die Registerkarte [!UICONTROL Sample records] stellt eine Teilmenge der Datensätze aus der ausgewählten Tabelle in einer Tabellenansicht bereit. Die Registerkarte [!UICONTROL Attributes] enthält den Attributnamen, den Datentyp und die Quelltabelle für jedes Attribut, das mit der ausgewählten Tabelle verknüpft ist.

Wählen Sie eine Tabelle aus der Liste in der linken Leiste aus, um Daten für Ihr Widget bereitzustellen, und wählen Sie **[!UICONTROL Select]** aus, um zum Widget-Composer zurückzukehren.

![Das Dialogfeld „Daten auswählen“ mit hervorgehobener Option „Auswählen“](./images/standard-dashboards/select-a-table.png)

Der Widget-Composer wird jetzt mit Daten aus der ausgewählten Tabelle gefüllt.

Das Datenmodell und die aktuell ausgewählte Tabelle werden oben in der linken Leiste angezeigt. Die zum Erstellen Ihres Widgets verfügbaren Attribute werden in der Spalte [!UICONTROL Attributes] aufgeführt. Sie können über die Suchleiste nach Attributen suchen, anstatt in der Liste zu scrollen, oder das ausgewählte Datenmodell ändern, indem Sie das Stiftsymbol (![) auswählen.](/help/images/icons/edit.png)) in der linken Leiste.

![Ein Widget, das mit Daten im Widget-Composer gefüllt wird.](./images/standard-dashboards/populated-widget-composer.png)

#### Hinzufügen und Filtern von Attributen {#add-and-filter-attributes}

Wählen Sie das Symbol zum Hinzufügen (![Symbol zum Hinzufügen) aus.](/help/images/icons/add-circle.png)) neben einem Attributnamen, um Ihrem Widget ein Attribut hinzuzufügen. Im angezeigten Dropdown-Menü können Sie ein Attribut für Ihr Widget als X-Achse, Y-Achse, Farbe oder Filter hinzufügen. Mit dem Attribut [!UICONTROL Color] können Sie die Ergebnisse der X- und Y-Achsenmarkierungen anhand der Farbe unterscheiden. Dies erfolgt, indem die Ergebnisse basierend auf ihrer Zusammensetzung eines dritten Attributs in verschiedene Farben aufgeteilt werden.

>[!TIP]
>
>Wenn Sie die Anordnung der X- und Y-Achse umkehren möchten, klicken Sie auf das Pfeilsymbol nach oben und unten (![Nach-oben- bzw. Nach-unten-Pfeilsymbol).](/help/images/icons/switch.png)), um ihre Anordnung zu ändern.

![Der Widget-Composer mit hervorgehobener Dropdown-Liste mit dem Add-Symbol.](./images/standard-dashboards/attributes-dropdown.png)

Um den Typ des Diagramms oder Diagramms Ihres Widgets zu ändern, wählen Sie die Dropdown-Liste [!UICONTROL Marks] und aus den verfügbaren Optionen aus. Zu den Optionen gehören Balken, Punkte, Häkchen, Linien oder Flächen. Nach der Auswahl wird eine Vorschauvisualisierung der aktuellen Einstellungen Ihres Widgets generiert.

![Der Widget-Composer mit hervorgehobenem Dropdown-Menü „Marken“.](./images/standard-dashboards/marks-dropdown.png)

Durch Hinzufügen eines Attributs als Filter können Sie auswählen, welche Werte in das Widget ein- oder ausgeschlossen werden sollen. Nachdem Sie einen Filter aus der Attributliste hinzugefügt haben, wird das Dialogfeld [!UICONTROL Filter] angezeigt, in dem Sie Werte mithilfe ihres Kontrollkästchens auswählen oder die Auswahl aufheben können.

![Das Filterdialogfeld zum Filtern von Werten aus Ihrem Widget.](./images/standard-dashboards/filter-dialog.png)

#### Herausfiltern historischer Daten {#filter-historical-data}

Um historische Daten aus den von Ihrem Widget generierten Einblicken herauszufiltern, fügen Sie das `date_key` als Filter hinzu und wählen Sie **[!UICONTROL Recent date]** gefolgt von **[!UICONTROL Apply]** aus. Dieser Filter stellt sicher, dass die Daten, die zur Ableitung von Einblicken verwendet werden, aus dem neuesten System-Snapshot stammen.

![Das Dialogfeld &quot;[!UICONTROL Filter: date_key]&quot; mit hervorgehobenen [!UICONTROL Recent date] und [!UICONTROL Apply].](./images/standard-dashboards/recent-date.png)

Alternativ können Sie einen benutzerdefinierten Zeitraum erstellen, nach dem Ihre Daten gefiltert werden. Wählen Sie **[!UICONTROL Select dates]** aus, um das Dialogfeld mit einer Liste der verfügbaren Daten zu erweitern. Aktivieren oder deaktivieren Sie mit dem Kontrollkästchen **[!UICONTROL Select all]** alle verfügbaren Optionen, oder aktivieren Sie das Kontrollkästchen für jeden Tag einzeln. Wählen Sie abschließend **[!UICONTROL Apply]** aus, um Ihre Auswahl zu bestätigen.

>[!NOTE]
>
>Wenn das Attribut `date_key` bereits als Filter hinzugefügt wurde, wählen Sie die Auslassungszeichen gefolgt von **[!UICONTROL Edit]** aus den Dropdown-Optionen aus, um den Filterzeitraum zu ändern.

![Das [!UICONTROL Filter: date_key]-Dialogfeld mit aktivierten und nicht aktivierten Kontrollkästchen für einzelne Tage.](./images/standard-dashboards/select-dates.png)

### Widget-Eigenschaften

Wählen Sie das Eigenschaftensymbol (![das Eigenschaftensymbol.](/help/images/icons/properties.png)) in der rechten Leiste aus, um den Bereich „Eigenschaften“ zu öffnen. Geben Sie im [!UICONTROL Properties] Bedienfeld einen Namen für das Widget in das [!UICONTROL Widget title] Textfeld ein.

![Das Eigenschaftenbedienfeld mit dem Symbol „Eigenschaften“ und dem hervorgehobenen Feld „Widget-Titel“.](./images/standard-dashboards/properties-panel.png)

Im Bedienfeld Widget-Eigenschaften können Sie verschiedene Aspekte Ihres Widgets bearbeiten. Sie haben die vollständige Kontrolle, um den Speicherort der Widget-Legende zu bearbeiten. Um die Legende zu verschieben, wählen Sie das Dropdown-Menü [!UICONTROL Legend placement] und dann die gewünschte Position aus der Liste der verfügbaren Optionen aus. Sie können die Beschriftung, die der Legende zugeordnet ist, sowie die X- oder Y-Achse auch umbenennen, indem Sie einen neuen Namen in das [!UICONTROL Legend title] bzw. [!UICONTROL Axis label] Textfeld eingeben.

#### Widget speichern {#save-widget}

Beim Speichern im Widget Composer wird das Widget lokal im Dashboard gespeichert. Wenn Sie Ihre Arbeit speichern und zu einem späteren Zeitpunkt fortsetzen möchten, wählen Sie **[!UICONTROL Save]** aus. Ein Häkchen unter dem Widget-Namen zeigt an, dass das Widget gespeichert wurde. Wenn Sie mit Ihrem Widget zufrieden sind, können Sie das Widget auch **[!UICONTROL Save and close]** auswählen, damit es allen anderen Benutzern mit Zugriff auf Ihr Dashboard zur Verfügung steht. Wählen Sie **[!UICONTROL Cancel]** aus, um Ihre Arbeit abzubrechen und zu Ihrem benutzerdefinierten Dashboard zurückzukehren.

![Bestätigung zum Speichern des neuen Widgets.](./images/standard-dashboards/save-confirmation.png)

>[!TIP]
>
>Wählen Sie das Eigenschaftensymbol (![das Eigenschaftensymbol.](/help/images/icons/properties.png)) neben dem Dashboard-Namen, um Details zu seiner Erstellung anzuzeigen. Sie können den Namen Ihres Dashboards im angezeigten Dialogfeld ändern.

Widgets können in diesem Arbeitsbereich neu angeordnet werden und ihre Größe kann geändert werden. Wählen Sie **[!UICONTROL Save]** aus, um Ihren Dashboard-Namen und das konfigurierte Layout beizubehalten.

![Das benutzerdefinierte Dashboard mit einem benutzerdefinierten Widget und der hervorgehobenen Schaltfläche „Speichern“.](./images/standard-dashboards/user-defined-dashboard.png)

Um sicherzustellen, dass jede Abfrage für ein Adobe Real-Time Customer Data Platform-Insights-Dashboard über ausreichend Ressourcen verfügt, um effizient ausgeführt zu werden, verfolgt die API die Ressourcennutzung, indem sie jeder Abfrage Slots für gleichzeitige Nutzung zuweist. Das System kann bis zu vier gleichzeitige Abfragen verarbeiten, sodass jeweils vier Slots für gleichzeitige Abfragen verfügbar sind. Abfragen werden basierend auf Parallelitätsslots in eine Warteschlange eingereiht und warten Sie dann in der Warteschlange, bis ausreichend Parallelitätsslots verfügbar sind.

### Bearbeiten, Duplizieren oder Löschen eines Widgets {#duplicate}

Nachdem Sie ein Widget erstellt haben, können Sie ganze Widgets in Ihrem benutzerdefinierten Dashboard bearbeiten, duplizieren oder löschen.

>[!TIP]
>
>Um zwischen vorhandenen benutzerdefinierten Dashboards zu wechseln, wählen Sie Dashboards in der linken Navigationsleiste und dann den Dashboard-Namen aus der Inventarliste aus.

Wählen Sie das Stiftsymbol (![Bleistiftsymbol) aus.](/help/images/icons/edit.png)) oben rechts im benutzerdefinierten Dashboard aus, um in den Bearbeitungsmodus zu wechseln.

![Ein benutzerdefiniertes Dashboard mit hervorgehobenem Stiftsymbol.](./images/standard-dashboards/edit-mode.png)

Wählen Sie als Nächstes die Auslassungszeichen oben rechts im Widget aus, die Sie bearbeiten, kopieren oder löschen möchten. Wählen Sie die entsprechende Aktion aus dem Dropdown-Menü aus.

![Ein Widget in einem benutzerdefinierten Dashboard mit Hervorhebung der Auslassungszeichen und des Duplikat-Widgets.](./images/standard-dashboards/duplicate.png)

>[!NOTE]
>
>Durch Duplizierung können Sie die Attribute einer insight anpassen, um ein eindeutiges Widget zu erstellen, ohne von Grund auf neu beginnen zu müssen. Wenn Sie ein Widget duplizieren, wird es in Ihrem benutzerdefinierten Dashboard angezeigt. Sie können dann die Auslassungszeichen für Ihr neues Widget und dann **[!UICONTROL Edit]** auswählen, um Ihre insight anzupassen.

## Nächste Schritte und zusätzliche Ressourcen

Durch das Lesen dieses Dokuments erhalten Sie ein besseres Verständnis dafür, wie Sie ein benutzerdefiniertes Dashboard erstellen und wie Sie benutzerdefinierte Widgets für dieses Dashboard erstellen, bearbeiten und aktualisieren.

Die verfügbaren vorkonfigurierten Metriken und Visualisierungen für die Dashboards [Profile](./guides/profiles.md#standard-widgets), [Segmente](./guides/audiences.md#standard-widgets) und [Ziele](./guides/destinations.md#standard-widgets) finden Sie in der Liste der Standard-Widgets in der entsprechenden Dokumentation.

Sehen Sie sich das folgende Video an, um Dashboards in Experience Platform besser zu verstehen:

>[!VIDEO](https://video.tv.adobe.com/v/3422737?captions=ger&quality=12&learn=on)
