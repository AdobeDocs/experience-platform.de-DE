---
title: Benutzerdefinierte Dashboards
description: Erfahren Sie, wie Sie benutzerdefinierte Dashboards erstellen und verwalten, in denen Sie maßgeschneiderte Widgets erstellen, hinzufügen und bearbeiten können, um wichtige Metriken zu visualisieren.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: 8e5df8b3e38197520c6e15f7c6639c62527c086e
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 1%

---

# Benutzerdefinierte Dashboards

Adobe Experience Platform-Dashboards helfen Ihnen, Einblicke zu beschleunigen und die Visualisierung über die benutzerdefinierte Dashboards-Funktion anzupassen. Mit dieser Funktion können Sie benutzerdefinierte Dashboards erstellen und verwalten, in denen Sie benutzerspezifische Widgets erstellen, hinzufügen und bearbeiten können, um für Ihr Unternehmen relevante Schlüsselmetriken zu visualisieren.

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Benutzerdefinierte Dashboards erstellen

Um ein benutzerdefiniertes Dashboard zu erstellen, navigieren Sie zunächst zum Dashboard-Inventar. Auswählen **[!UICONTROL Dashboards]** aus der linken Navigation der Platform-Benutzeroberfläche gefolgt von **[!UICONTROL Dashboard erstellen]**.

![Das Dashboard-Inventar mit Dashboards im linken Navigationsbereich und &quot;Dashboard erstellen&quot;hervorgehoben.](./images/user-defined-dashboards/create-dashboard.png)

Bevor Sie ein benutzerdefiniertes Dashboard hinzufügen, ist der Dashboards-Bestand leer und zeigt die Meldung &quot;Keine Dashboards gefunden&quot;an. angezeigt. Nach der Erstellung werden alle benutzerdefinierten Dashboards im Dashboard-Inventar aufgelistet.

Die [!UICONTROL Dashboard erstellen] angezeigt. Geben Sie einen benutzerfreundlichen, beschreibenden Namen für die Sammlung von Widgets ein, die Sie erstellen möchten, und wählen Sie **[!UICONTROL Speichern]**.

![Das Dialogfeld Dashboard erstellen .](./images/user-defined-dashboards/create-dashboard-dialog.png)

Das neu erstellte leere Dashboard wird mit Ihrem Namen in der oberen linken Ecke der Ansicht angezeigt.

## Widget erstellen {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Maximale Anzahl von Widgets"
>abstract="Benutzerdefinierte Dashboards unterstützen bis zu zehn Widgets. Nachdem Sie zehn Widgets zu Ihrem Dashboard hinzugefügt haben, wird die [!UICONTROL Neues Widget hinzufügen] deaktiviert ist und grau angezeigt wird."

Wählen Sie in der neuen Dashboard-Ansicht **[!UICONTROL Neues Widget hinzufügen]** , um den Erstellungsprozess für Widgets zu starten.

>[!IMPORTANT]
>
>Benutzerdefinierte Dashboards unterstützen bis zu zehn Widgets. Nachdem Sie zehn Widgets zu Ihrem Dashboard hinzugefügt haben, wird die [!UICONTROL Neues Widget hinzufügen] deaktiviert ist und grau angezeigt wird.

![Das neue leere Dashboard mit hervorgehobenem Add new widget .](./images/user-defined-dashboards/add-new-widget.png)

### Widget Composer

Der Arbeitsbereich des Widget Composers wird angezeigt. Wählen Sie als Nächstes **[!UICONTROL Daten auswählen]** , um das Datenmodell auszuwählen, aus dem Sie Ihren Widgets Attribute hinzufügen möchten.

![Der Arbeitsbereich des Widget Composers.](./images/user-defined-dashboards/widget-composer.png)

Die [!UICONTROL Daten auswählen] angezeigt. Wählen Sie in der linken Spalte ein Datenmodell aus, um eine Vorschauliste aller verfügbaren Tabellen anzuzeigen.

>[!NOTE]
>
>Benutzerdefinierte Dashboards unterstützen derzeit nur das Profildatenmodell. Weitere Optionen werden unterstützt.

![Das Dialogfeld Daten auswählen .](./images/user-defined-dashboards/select-data-dialog.png)

Die Vorschauliste enthält Details zu den im Datenmodell enthaltenen Tabellen. Die nachstehende Tabelle enthält Beschreibungen der Spaltenfelder und ihrer potenziellen Werte.

| Spaltenfeld | Beschreibung |
|---|---|
| [!UICONTROL Titel] | Der Name der Tabelle. |
| [!UICONTROL Tabellenart] | Der Typ der Tabelle. Mögliche Typen sind: `fact`, `dimension`und `none`. |
| [!UICONTROL Suchen] | Die Anzahl der Tabellen, die mit der ausgewählten Tabelle verbunden sind. |

Auswählen **[!UICONTROL Nächste]** zur Bestätigung Ihrer Wahl des Datenmodells. In der nächsten Ansicht wird eine Liste der verfügbaren Tabellen in der linken Leiste angezeigt. Wählen Sie eine Tabelle aus, um eine umfassende Aufschlüsselung der in der ausgewählten Tabelle enthaltenen Daten anzuzeigen.

Die [!UICONTROL Vorschau] Bereich enthält Registerkarten für [!UICONTROL Beispieldatensätze] und [!UICONTROL Attribute]. Die [!UICONTROL Beispieldatensätze] bietet eine Teilmenge der Datensätze aus der ausgewählten Tabelle in einer tabellarischen Ansicht. Die [!UICONTROL Attribute] tab stellt den Attributnamen, den Datentyp und die Quelltabelle für jedes Attribut bereit, das mit der ausgewählten Tabelle verknüpft ist.

Wählen Sie eine Tabelle aus der Liste in der linken Leiste aus, um Daten für Ihr Widget bereitzustellen, und wählen Sie **[!UICONTROL Auswählen]** , um zum Widget Composer zurückzukehren.

![Das Dialogfeld &quot;Daten auswählen&quot;mit hervorgehobener Auswahl.](./images/user-defined-dashboards/select-a-table.png)

Der Widget Composer enthält jetzt Daten aus Ihrer ausgewählten Tabelle.

Das Datenmodell und die aktuell ausgewählte Tabelle werden oben in der linken Leiste angezeigt und die zum Erstellen Ihres Widgets verfügbaren Attribute werden in der Spalte &quot;Attribute&quot;aufgeführt.

![Ein Widget, das mit Daten im Widget Composer gefüllt ist.](./images/user-defined-dashboards/populated-widget-composer.png)

>[!TIP]
>
>Sie können das ausgewählte Datenmodell ändern, indem Sie das Stiftsymbol (![Bleistiftsymbol.](./images/user-defined-dashboards/edit-icon.png)) in der linken Leiste.

Wählen Sie das Symbol zum Hinzufügen aus (./images/user-defined-dashboards/add-icon.png) neben einem Attributnamen, um der X- oder Y-Achse ein Attribut hinzuzufügen.

![Der Widget Composer mit dem Dropdown-Menü zum Hinzufügen von Symbolen wird hervorgehoben, um Attribute zu einer Widget-Achse hinzuzufügen.](./images/user-defined-dashboards/attributes-dropdown.png)

Wählen Sie als Nächstes den Diagrammtyp aus der [!UICONTROL Marken] Dropdown-Liste, um eine Vorschau der aktuellen Einstellungen Ihres Widgets zu erzeugen. Im [!UICONTROL Eigenschaften] auf der rechten Seite des Bildschirms einen Namen für das Widget in der [!UICONTROL Widget title] Textfeld.

![Der Widget Composer mit dem Dropdown-Menü Markierungen und dem Textfeld für den Widget-Titel hervorgehoben.](./images/user-defined-dashboards/marks-dropdown-widget-title.png)

Wenn Sie mit Ihrem Widget zufrieden sind, wählen Sie **[!UICONTROL Speichern]**. Ein Häkchen-Symbol unter dem Widget-Namen zeigt an, dass das Widget gespeichert wurde.

>[!NOTE]
>
>Durch das Speichern im Widget Composer wird das Widget lokal in Ihrem Dashboard gespeichert. Wenn Sie den Dashboard-Editor beenden, ohne das Dashboard zu speichern, wird das Widget nicht im Dashboard gespeichert.

![Neue Widget-Speicherbestätigung.](./images/user-defined-dashboards/save-confirmation.png)

Auswählen **[!UICONTROL Abbrechen]** , um zu Ihrem benutzerdefinierten Dashboard zurückzukehren.

![Der Widget Composer mit einem erstellten Beispiel-Widget.](./images/user-defined-dashboards/composed-widget.png)

>[!TIP]
>
>Wählen Sie das Einstellungssymbol neben dem Dashboard-Namen aus, um Details zur Erstellung anzuzeigen. Sie können den Namen Ihres Dashboards im angezeigten Dialogfeld ändern.

Widgets können in diesem Arbeitsbereich neu angeordnet und in der Größe angepasst werden. Auswählen **[!UICONTROL Speichern]** um Ihren Dashboard-Namen und Ihr konfiguriertes Layout beizubehalten.

![Das benutzerdefinierte Dashboard mit einem benutzerdefinierten Widget und die Schaltfläche zum Speichern hervorgehoben.](./images/user-defined-dashboards/user-defined-dashboard.png)

Um sicherzustellen, dass jede Abfrage für ein Real-time Customer Data Platform Insights-Dashboard über genügend Ressourcen verfügt, um effizient auszuführen, verfolgt die API die Ressourcennutzung, indem sie jeder Abfrage Gleichzeitigkeitsfenster zuweist. Das System kann bis zu vier gleichzeitige Abfragen verarbeiten. Daher stehen vier gleichzeitige Abfrageplätze jederzeit zur Verfügung. Abfragen werden basierend auf gleichzeitigen Slots in eine Warteschlange gestellt und dann in der Warteschlange gewartet, bis genügend gleichzeitige Slots verfügbar sind.

## Nächste Schritte

Durch Lesen dieses Dokuments können Sie besser verstehen, wie Sie ein benutzerdefiniertes Dashboard erstellen und benutzerdefinierte Widgets für dieses Dashboard erstellen, bearbeiten und aktualisieren.

So ermitteln Sie die verfügbaren vorkonfigurierten Metriken und Visualisierungen für die [profiles](./guides/profiles.md#standard-widgets), [Segmente](./guides/segments.md#standard-widgets)und [Ziele](./guides/destinations.md#standard-widgets) -Dashboards finden Sie in der entsprechenden Dokumentation eine Liste der Standard-Widgets.
