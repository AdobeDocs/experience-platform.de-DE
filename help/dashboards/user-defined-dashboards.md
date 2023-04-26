---
title: Benutzerdefinierte Dashboards
description: Erfahren Sie, wie Sie benutzerdefinierte Dashboards erstellen und verwalten, in denen Sie maßgeschneiderte Widgets erstellen, hinzufügen und bearbeiten können, um wichtige Metriken zu visualisieren.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: 8507ecceca47fac3d321b89e4fed018ee9784777
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 4%

---

# Benutzerdefinierte Dashboards

Adobe Experience Platform-Dashboards helfen Ihnen, Einblicke zu beschleunigen und die Visualisierung über die benutzerdefinierte Dashboards-Funktion anzupassen. Mit dieser Funktion können Sie benutzerdefinierte Dashboards erstellen und verwalten, in denen Sie benutzerspezifische Widgets erstellen, hinzufügen und bearbeiten können, um für Ihr Unternehmen relevante Schlüsselmetriken zu visualisieren.

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Benutzerdefiniertes Dashboard erstellen

Um ein benutzerdefiniertes Dashboard zu erstellen, navigieren Sie zunächst zum Dashboard-Inventar. Auswählen **[!UICONTROL Dashboards]** aus der linken Navigation der Platform-Benutzeroberfläche gefolgt von **[!UICONTROL Dashboard erstellen]**.

![Das Dashboard-Inventar mit Dashboards im linken Navigationsbereich und &quot;Dashboard erstellen&quot;hervorgehoben.](./images/user-defined-dashboards/create-dashboard.png)

Bevor Sie ein benutzerdefiniertes Dashboard hinzufügen, ist der Dashboards-Bestand leer und zeigt die Meldung &quot;Keine Dashboards gefunden&quot;an. angezeigt. Nach der Erstellung werden alle benutzerdefinierten Dashboards im Dashboard-Inventar aufgelistet.

>[!NOTE]
>
>Um ein vorhandenes Dashboard zu bearbeiten, wählen Sie den Dashboard-Namen aus der Liste der Bestände und danach das Stiftsymbol (![Ein Bleistiftsymbol.](./images/user-defined-dashboards/edit-icon.png))

Die [!UICONTROL Dashboard erstellen] angezeigt. Geben Sie einen benutzerfreundlichen, beschreibenden Namen für die Sammlung von Widgets ein, die Sie erstellen möchten, und wählen Sie **[!UICONTROL Speichern]**.

![Das Dialogfeld Dashboard erstellen .](./images/user-defined-dashboards/create-dashboard-dialog.png)

Das neu erstellte leere Dashboard wird mit Ihrem Namen in der oberen linken Ecke der Ansicht angezeigt.

## Widget erstellen {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Maximale Anzahl an Widgets"
>abstract="Benutzerdefinierte Dashboards unterstützen bis zu zehn Widgets. Nachdem Sie zehn Widgets zu Ihrem Dashboard hinzugefügt haben, wird die Option [!UICONTROL Neues Widget hinzufügen] deaktiviert und ausgegraut."

Wählen Sie in der neuen Dashboard-Ansicht **[!UICONTROL Neues Widget hinzufügen]** , um den Erstellungsprozess für Widgets zu starten.

>[!IMPORTANT]
>
>Benutzerdefinierte Dashboards unterstützen bis zu zehn Widgets. Nachdem Sie zehn Widgets zu Ihrem Dashboard hinzugefügt haben, wird die Option [!UICONTROL Neues Widget hinzufügen] deaktiviert und ausgegraut.

![Das neue leere Dashboard mit hervorgehobenem Add new widget .](./images/user-defined-dashboards/add-new-widget.png)

### Widget Composer

Der Arbeitsbereich des Widget Composers wird angezeigt. Wählen Sie als Nächstes **[!UICONTROL Daten auswählen]** , um das Datenmodell auszuwählen, aus dem Sie Ihren Widgets Attribute hinzufügen möchten.

![Der Arbeitsbereich des Widget Composers.](./images/user-defined-dashboards/widget-composer.png)

#### Datenmodell auswählen {#select-data-model}

Die [!UICONTROL Datenmodell auswählen] angezeigt. Wählen Sie in der linken Spalte ein Datenmodell aus, um eine Vorschauliste aller verfügbaren Tabellen anzuzeigen. Das vorkonfigurierte Datenmodell für Real-time Customer Data Platform heißt [!UICONTROL CDPInsights].

>[!TIP]
>
>Wählen Sie das Informationssymbol (![Ein Informationssymbol.](./images/user-defined-dashboards/info-icon.png)), um den vollständigen Namen des Datenmodells anzuzeigen, wenn es für die Anzeige in der Datenleiste zu lang ist.

![Das Dialogfeld Daten auswählen .](./images/user-defined-dashboards/select-data-model-dialog.png)

Die Vorschauliste enthält Details zu den im Datenmodell enthaltenen Tabellen. Die nachstehende Tabelle enthält Beschreibungen der Spaltenfelder und ihrer potenziellen Werte.

| Spaltenfeld | Beschreibung |
|---|---|
| [!UICONTROL Titel] | Der Name der Tabelle. |
| [!UICONTROL Tabellentyp] | Der Typ der Tabelle. Mögliche Typen sind: `fact`, `dimension`und `none`. |
| [!UICONTROL Datensätze] | Die Anzahl der der ausgewählten Tabelle zugeordneten Datensätze. |
| [!UICONTROL Suchen] | Die Anzahl der Tabellen, die mit der ausgewählten Tabelle verbunden sind. |
| [!UICONTROL Attribute] | Die Anzahl der Attribute für die ausgewählte Tabelle. |

Auswählen **[!UICONTROL Nächste]** zur Bestätigung Ihrer Wahl des Datenmodells. In der nächsten Ansicht wird eine Liste der verfügbaren Tabellen in der linken Leiste angezeigt. Wählen Sie eine Tabelle aus, um eine umfassende Aufschlüsselung der in der ausgewählten Tabelle enthaltenen Daten anzuzeigen.

### Widget befüllen {#populate-widget}

Die [!UICONTROL Vorschau] Bereich enthält Registerkarten für [!UICONTROL Beispieldatensätze] und [!UICONTROL Attribute]. Die [!UICONTROL Beispieldatensätze] bietet eine Teilmenge der Datensätze aus der ausgewählten Tabelle in einer tabellarischen Ansicht. Die [!UICONTROL Attribute] tab stellt den Attributnamen, den Datentyp und die Quelltabelle für jedes Attribut bereit, das mit der ausgewählten Tabelle verknüpft ist.

Wählen Sie eine Tabelle aus der Liste in der linken Leiste aus, um Daten für Ihr Widget bereitzustellen, und wählen Sie **[!UICONTROL Auswählen]** , um zum Widget Composer zurückzukehren.

![Das Dialogfeld &quot;Daten auswählen&quot;mit hervorgehobener Auswahl.](./images/user-defined-dashboards/select-a-table.png)

Der Widget Composer enthält jetzt Daten aus Ihrer ausgewählten Tabelle.

Das Datenmodell und die derzeit ausgewählte Tabelle werden oben in der linken Leiste angezeigt. Die zum Erstellen des Widgets verfügbaren Attribute werden im [!UICONTROL Attribute] Spalte. Sie können die Suchleiste verwenden, um nach Attributen zu suchen, anstatt in der Liste zu scrollen oder das ausgewählte Datenmodell zu ändern, indem Sie das Stiftsymbol (![Bleistiftsymbol.](./images/user-defined-dashboards/edit-icon.png)) in der linken Leiste.

![Ein Widget, das mit Daten im Widget Composer gefüllt ist.](./images/user-defined-dashboards/populated-widget-composer.png)

#### Hinzufügen und Filtern von Attributen {#add-and-filter-attributes}

Wählen Sie das Symbol zum Hinzufügen aus (![Ein Symbol zum Hinzufügen.](./images/user-defined-dashboards/add-icon.png)) neben einem Attributnamen, um Ihrem Widget ein Attribut hinzuzufügen. Über das angezeigte Dropdown-Menü können Sie ein Attribut als X-Achse, Y-Achse, Farbe oder Filter für Ihr Widget hinzufügen. Die [!UICONTROL Farbe] -Attribut ermöglicht es Ihnen, die Ergebnisse der X- und Y-Achsenmarkierungen nach Farbe zu unterscheiden. Dies geschieht durch die Aufteilung der Ergebnisse in verschiedene Farben basierend auf ihrer Zusammensetzung eines dritten Attributs.

>[!TIP]
>
>Wenn Sie die Anordnung der X- und Y-Achse spiegeln möchten, wählen Sie das Pfeilsymbol nach oben und nach unten (![Das Pfeilsymbol nach oben und unten.](./images/user-defined-dashboards/switch-axis-icon.png)), um ihre Anordnung zu wechseln.

![Der Widget Composer mit dem Dropdown-Menü für das Add-Symbol wurde hervorgehoben.](./images/user-defined-dashboards/attributes-dropdown.png)

Um den Diagrammtyp oder Diagrammtyp Ihres Widgets zu ändern, wählen Sie die [!UICONTROL Marken] und wählen Sie aus den verfügbaren Optionen aus. Zu den Optionen gehören Balken, Punkte, Zecken, Linien oder Bereiche. Nach der Auswahl wird eine Vorschau-Visualisierung der aktuellen Einstellungen Ihres Widgets generiert.

![Der Widget-Composer mit hervorgehobenem Dropdown-Menü &quot;Marks&quot;.](./images/user-defined-dashboards/marks-dropdown.png)

Durch Hinzufügen eines Attributs als Filter können Sie auswählen, welche Werte aus dem Widget ein- oder ausgeschlossen werden sollen. Nachdem Sie einen Filter aus der Attributliste hinzugefügt haben, wird die [!UICONTROL Filter] angezeigt, in dem Sie Werte mithilfe ihres Kontrollkästchens auswählen oder deren Auswahl aufheben können.

![Das Dialogfeld &quot;Filter&quot;, um Werte aus Ihrem Widget zu filtern.](./images/user-defined-dashboards/filter-dialog.png)

#### Filtern von historischen Daten {#filter-historical-data}

Um historische Daten aus den von Ihrem Widget generierten Einblicken herauszufiltern, fügen Sie die `date_key` Attribut als Filter auswählen und **[!UICONTROL Letztes Datum]** gefolgt von **[!UICONTROL Anwenden]**. Dieser Filter stellt sicher, dass die Daten, die zum Ableiten von Einblicken verwendet werden, aus dem neuesten Systemabbild übernommen werden.

![Die [!UICONTROL Filter: date_key] Dialogfeld mit [!UICONTROL Letztes Datum] und [!UICONTROL Anwenden] hervorgehoben.](./images/user-defined-dashboards/recent-date.png)

Alternativ können Sie einen benutzerdefinierten Zeitraum erstellen, nach dem Ihre Daten gefiltert werden sollen. Auswählen **[!UICONTROL Datumsangaben auswählen]** , um das Dialogfeld mit einer Liste der verfügbaren Daten zu erweitern. Verwenden Sie die **[!UICONTROL Alle auswählen]** aktivieren, um alle verfügbaren Optionen zu aktivieren bzw. zu deaktivieren, oder aktivieren Sie das Kontrollkästchen für jeden Tag einzeln. Wählen Sie abschließend **[!UICONTROL Anwenden]** um Ihre Auswahl zu bestätigen.

>[!NOTE]
>
>Wenn die Variable `date_key` -Attribut bereits als Filter hinzugefügt wurde, wählen Sie die Auslassungspunkte gefolgt von **[!UICONTROL Bearbeiten]** aus den Dropdown-Optionen, um den Filterzeitraum zu ändern.

![Die [!UICONTROL Filter: date_key] mit einzelnen Tag-Checkboxes sowohl aktiviert als auch deaktiviert.](./images/user-defined-dashboards/select-dates.png)

### Widget-Eigenschaften

Wählen Sie das Eigenschaftensymbol (![Das Symbol &quot;Eigenschaften&quot;.](./images/user-defined-dashboards/properties-icon.png)) in der rechten Leiste, um den Eigenschaftenbereich zu öffnen. Im [!UICONTROL Eigenschaften] -Bedienfeld ein, geben Sie einen Namen für das Widget im [!UICONTROL Widget title] Textfeld.

![Das Eigenschaftenbedienfeld mit dem Eigenschaftensymbol und dem Feld Widget-Titel hervorgehoben.](./images/user-defined-dashboards/properties-panel.png)

Über das Bedienfeld &quot;Widget-Eigenschaften&quot;können Sie verschiedene Aspekte Ihres Widgets bearbeiten. Sie haben die vollständige Kontrolle, um den Speicherort der Widget-Legende zu bearbeiten. Um die Legende zu verschieben, wählen Sie die [!UICONTROL Legendenplatzierung] und wählen Sie aus der Liste der verfügbaren Optionen die gewünschte Position aus. Sie können auch die mit der Legende verknüpfte Bezeichnung sowie die X- oder Y-Achse umbenennen, indem Sie einen neuen Namen in die [!UICONTROL Legendentitel] Textfeld oder [!UICONTROL Achsenbeschriftung] Textfeld.

#### Widget speichern {#save-widget}

Durch das Speichern im Widget Composer wird das Widget lokal in Ihrem Dashboard gespeichert. Wenn Sie Ihre Arbeit speichern und zu einem späteren Zeitpunkt fortsetzen möchten, wählen Sie **[!UICONTROL Speichern]**. Ein Häkchen-Symbol unter dem Widget-Namen zeigt an, dass das Widget gespeichert wurde. Wenn Sie mit dem Widget zufrieden sind, wählen Sie alternativ **[!UICONTROL Speichern und schließen]** , um das Widget allen anderen Benutzern mit Zugriff auf Ihr Dashboard zur Verfügung zu stellen. Auswählen **[!UICONTROL Abbrechen]** um Ihre Arbeit zu beenden und zu Ihrem benutzerdefinierten Dashboard zurückzukehren.

![Neue Widget-Speicherbestätigung.](./images/user-defined-dashboards/save-confirmation.png)

>[!TIP]
>
>Wählen Sie das Eigenschaftensymbol (![Das Symbol &quot;Eigenschaften&quot;.](./images/user-defined-dashboards/properties-icon.png)) neben dem Dashboard-Namen, um Details zur Erstellung anzuzeigen. Sie können den Namen Ihres Dashboards im angezeigten Dialogfeld ändern.

Widgets können in diesem Arbeitsbereich neu angeordnet und in der Größe angepasst werden. Auswählen **[!UICONTROL Speichern]** um Ihren Dashboard-Namen und Ihr konfiguriertes Layout beizubehalten.

![Das benutzerdefinierte Dashboard mit einem benutzerdefinierten Widget und die Schaltfläche zum Speichern hervorgehoben.](./images/user-defined-dashboards/user-defined-dashboard.png)

Um sicherzustellen, dass jede Abfrage für ein Adobe Real-time Customer Data Platform Insights-Dashboard über genügend Ressourcen verfügt, um effizient auszuführen, verfolgt die API die Ressourcennutzung, indem sie jeder Abfrage Gleichzeitigkeitsfenster zuweist. Das System kann bis zu vier gleichzeitige Abfragen verarbeiten. Daher stehen vier gleichzeitige Abfrageplätze jederzeit zur Verfügung. Abfragen werden basierend auf gleichzeitigen Slots in eine Warteschlange gestellt und dann in der Warteschlange gewartet, bis genügend gleichzeitige Slots verfügbar sind.

### Widget duplizieren

Nachdem Sie ein Widget erstellt haben, können Sie das gesamte Widget duplizieren und seine Attribute anpassen, um ein eindeutiges Widget zu erstellen, ohne von Grund auf neu beginnen zu müssen. Um ein Widget zu duplizieren, navigieren Sie zunächst zum Dashboard-Inventar. Wählen Sie dann den Dashboard-Namen aus der Inventarliste aus. Ihr angepasstes Dashboard wird angezeigt.

![Die Platform-Benutzeroberfläche mit Dashboards und einem benutzerdefinierten Dashboard-Namen wird hervorgehoben.](./images/user-defined-dashboards/dashbaord-inventory.png)

Wählen Sie das Stiftsymbol (![Ein Bleistiftsymbol.](./images/user-defined-dashboards/edit-icon.png)) oben rechts im Dashboard, um in den Bearbeitungsmodus zu wechseln.

![Ein benutzerdefiniertes Dashboard mit hervorgehobenem Stiftsymbol.](./images/user-defined-dashboards/edit-mode.png)

Wählen Sie dann die Auslassungspunkte oben rechts im Widget aus, das Sie kopieren möchten, gefolgt von **[!UICONTROL Duplizieren]** aus der Liste der verfügbaren Optionen.

![Ein Widget in einem benutzerdefinierten Dashboard mit markierten Ellipsen und dupliziertem Widget.](./images/user-defined-dashboards/duplicate.png)

Ein dupliziertes Widget wird in Ihrem benutzerdefinierten Dashboard angezeigt. Wählen Sie die Auslassungszeichen Ihres neuen Widgets aus, gefolgt von **[!UICONTROL Bearbeiten]**, um Ihr neues Widget anzupassen.

## Nächste Schritte und zusätzliche Ressourcen

Durch Lesen dieses Dokuments können Sie besser verstehen, wie Sie ein benutzerdefiniertes Dashboard erstellen und benutzerdefinierte Widgets für dieses Dashboard erstellen, bearbeiten und aktualisieren.

So ermitteln Sie die verfügbaren vorkonfigurierten Metriken und Visualisierungen für die [profiles](./guides/profiles.md#standard-widgets), [Segmente](./guides/segments.md#standard-widgets)und [Ziele](./guides/destinations.md#standard-widgets) -Dashboards finden Sie in der entsprechenden Dokumentation eine Liste der Standard-Widgets.

Sehen Sie sich das folgende Video an, um Ihr Verständnis von benutzerdefinierten Dashboards in Experience Platform zu verbessern:

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
