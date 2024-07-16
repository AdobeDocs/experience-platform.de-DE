---
title: Query Pro-Modus
description: Erfahren Sie, wie Sie mit SQL-Abfragen in der Adobe Experience Platform-Benutzeroberfläche Diagramme für Ihre benutzerdefinierten Dashboards erstellen können.
exl-id: 15c664c4-8546-4e04-b81d-c78bf83500d3
source-git-commit: 5bb954da7c1e05922a4e0f8d0bc7d3ab5c8e0e58
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---

# Abfrage pro Modus {#query-pro-mode}

Query pro mode ist ein auf SQL Editor basierender Workflow, der Sie durch den Prozess der Generierung von Einblicken mit benutzerdefinierten SQL-Abfragen in der Adobe Experience Platform-Benutzeroberfläche führt. Bevor Sie Einblicke mit benutzerdefinierten SQL-Abfragen generieren können, müssen Sie zunächst [ein Dashboard erstellen](./overview.md#create-custom-dashboard).

## SQL erstellen {#compose-sql}

Nachdem Sie sich dafür entschieden haben, ein Dashboard mit Query Pro-Modus zu erstellen, wird das Dialogfeld **[!UICONTROL SQL eingeben]** angezeigt. Wählen Sie eine Datenbank (Insight-Datenmodell) aus, die aus dem Dropdown-Menü abgefragt werden soll, und geben Sie eine geeignete Abfrage für Ihren Datensatz im Abfragepro-Editor ein.

>[!NOTE]
>
>Der Pro-Modus &quot;Abfrage&quot;steht nur Benutzern zur Verfügung, die die Data Distiller-SKU erworben haben. Der Designmodus [[!UICONTROL Geführter Entwurf]](../../user-defined-dashboards.md) steht allen Benutzern zur Verfügung, um Einblicke aus einem vorhandenen Datenmodell zu erstellen.

Informationen zu den Benutzeroberflächen-Elementen finden Sie im [Benutzerhandbuch zum Abfrage-Editor](../../../query-service/ui/user-guide.md#query-authoring) .

![Das Dialogfeld [!UICONTROL SQL eingeben] mit dem Dropdown-Menü &quot;Datensatz&quot;und dem Ausführungssymbol wird hervorgehoben. Das Dialogfeld enthält eine ausgefüllte SQL-Abfrage und die Registerkarte &quot;Abfrageparameter&quot;wird angezeigt.](../../images/customizable-insights/enter-sql-database-dropdown.png)

### Abfrageparameter {#query-parameters}

Um [global](./filters/global-filter.md) oder [Datumsfilter](./filters/date-filter.md) einzubeziehen, muss Ihre Abfrage **** Abfrageparameter verwenden. Beim Erstellen Ihrer Anweisung im Abfragepro-Modus müssen Sie Beispielwerte angeben, wenn Ihre Abfrage Abfrageparameter verwendet. Mit den Beispielwerten können Sie die SQL-Anweisung ausführen und das Diagramm erstellen. Beachten Sie, dass die Beispielwerte, die Sie beim Erstellen Ihrer Anweisung angeben, durch die tatsächlichen Werte ersetzt werden, die Sie für den Datums- oder globalen Filter zur Laufzeit auswählen.



>[!IMPORTANT]
>
>Wenn Sie einen globalen Filter verwenden möchten, müssen Sie einen Abfrageparameter in Ihrer SQL platzieren und diesen Abfrageparameter dann mit dem globalen Filter im Widget Composer verknüpfen. Im folgenden Screenshot wird `CONSENT_VALUE_FILTER` in der SQL als Abfrageparameter für einen globalen Filter verwendet. Weitere Informationen dazu finden Sie in der Dokumentation zu [globalen Filtern](./filters/global-filter.md#enable-global-filter) .

Um Ihre Abfrage auszuführen, wählen Sie das Ausführungssymbol (![Ausführungssymbol) aus.](../../images/customizable-insights/run-icon.png)). Der Abfrage-Editor zeigt die Registerkarte Ergebnisse an. Wählen Sie als Nächstes **[!UICONTROL Auswählen]** aus, um die Konfiguration zu bestätigen und den Widget Composer zu öffnen.

>[!TIP]
>
>Wenn Ihre Abfrage Abfrageparameter verwendet, führen Sie die Abfrage einmal aus, um alle verwendeten Abfrageparameterschlüssel vorab auszufüllen. Die Abfrage schlägt fehl, aber die Benutzeroberfläche zeigt automatisch die Registerkarte Abfrageparameter an und listet alle enthaltenen Schlüssel auf. Fügen Sie die entsprechenden Werte für Ihre Schlüssel hinzu.

![Das Dialogfeld [!UICONTROL SQL eingeben] mit SQL-Eingabe, die Registerkarte &quot;Ergebnisse&quot;wird angezeigt und die Option &quot;Auswählen&quot;wurde hervorgehoben.](../../images/customizable-insights/enter-sql-select.png)

## Widget befüllen {#populate-widget}

Der Widget Composer wird jetzt mit den Spalten aus der ausgeführten SQL gefüllt. Der Typ des Dashboards wird oben links angezeigt, in diesem Fall ist er [!UICONTROL Manueller SQL-Eintrag]. Wählen Sie das Stiftsymbol (![Ein Stiftsymbol) aus.](../../images/customizable-insights/edit-icon.png)), um die SQL an jedem Punkt zu bearbeiten.

>[!TIP]
>
>Die verfügbaren Attribute sind Spalten, die aus der ausgeführten SQL entnommen werden.

Verwenden Sie zum Erstellen Ihres Widgets die in der Spalte [!UICONTROL Attribute] aufgelisteten Attribute. Sie können die Suchleiste verwenden, um nach Attributen zu suchen oder in der Liste einen Bildlauf durchzuführen.

![Der Widget Composer mit der Erstellungsmethode und der Attributspalte hervorgehoben.](../../images/customizable-insights/creation-method-and-attribute-column.png)

### Attribute hinzufügen {#add-attributes}

Um Ihrem Widget ein Attribut hinzuzufügen, wählen Sie das Pluszeichen (![A Pluszeichen) aus.](../../images/customizable-insights/add-icon.png)) neben einem Attributnamen. Im angezeigten Dropdown-Menü können Sie der Grafik aus den von Ihrer SQL bestimmten Optionen ein Attribut hinzufügen. Verschiedene Diagrammtypen haben unterschiedliche Optionen, z. B. ein Dropdown-Menü für die X- und Y-Achse.

In diesem Ringdiagramm-Beispiel sind die Optionen Größe und Farbe. Farbe unterteilt die Ringdiagrammergebnisse und die Größe ist die tatsächlich verwendete Metrik. Fügen Sie dem Feld [!UICONTROL Farbe] ein Attribut hinzu, um die Ergebnisse basierend auf ihrer Zusammensetzung in verschiedene Farben zu unterteilen.

>[!TIP]
>
>Wählen Sie das Pfeilsymbol nach oben und unten (![Das Pfeilsymbol nach oben und unten) aus.](../../images/customizable-insights/switch-axis-icon.png)), um die Anordnung der X- und Y-Achse in Balken- oder Liniendiagrammen zu ändern.

![Der Widget Composer mit dem Dropdown-Menü &quot;Add-Symbol&quot;und hervorgehobenen Umschalt-Pfeilen.](../../images/customizable-insights/add-icon-and-switch-arrows.png)

Um den Diagrammtyp oder das Diagramm Ihres Widgets zu ändern, wählen Sie aus den verfügbaren Optionen der Dropdown-Liste [!UICONTROL Markierungen] aus. Zu den Optionen gehören [!UICONTROL Linie], [!UICONTROL Donut], [!UICONTROL Big number] und [!UICONTROL Balken]. Nach der Auswahl wird eine Vorschau-Visualisierung der aktuellen Einstellungen Ihres Widgets generiert.

![Der Widget Composer mit hervorgehobener Widget-Vorschau.](../../images/customizable-insights/widget-preview.png)

## Widget-Eigenschaften {#properties}

Wählen Sie das Eigenschaftensymbol (![Das Eigenschaftensymbol) aus.](../../images/customizable-insights/properties-icon.png)) in der rechten Leiste, um den Eigenschaftenbereich zu öffnen. Geben Sie im Bereich [!UICONTROL Eigenschaften] im Textfeld **[!UICONTROL Widget-Titel]** einen Namen für das Widget ein. Sie können auch verschiedene Aspekte Ihres Diagramms umbenennen.

>[!NOTE]
>
>Die in der Seitenleiste der Eigenschaften verfügbaren spezifischen Felder hängen vom bearbeiteten Diagrammtyp ab.

![Der Widget Composer mit dem Eigenschaftensymbol und dem Widget-Titelfeld hervorgehoben.](../../images/customizable-insights/widget-properties-title-text.png)

## Widget speichern {#save-widget}

Durch das Speichern im Widget Composer wird das Widget lokal in Ihrem Dashboard gespeichert. Wenn Sie Ihre Arbeit speichern und später fortsetzen möchten, wählen Sie **[!UICONTROL Speichern]**. Ein Häkchen-Symbol unter dem Widget-Namen zeigt an, dass das Widget gespeichert wurde. Wenn Sie mit Ihrem Widget zufrieden sind, wählen Sie alternativ **[!UICONTROL Speichern und schließen]** , um das Widget allen anderen Benutzern mit Zugriff auf Ihr Dashboard zur Verfügung zu stellen. Wählen Sie Abbrechen aus, um Ihre Arbeit abzubrechen und zu Ihrem benutzerdefinierten Dashboard zurückzukehren.

![Der Widget Composer mit hervorgehobenem Speichern, Speichern und Schließen, Speichern und Widget.](../../images/customizable-insights/insight-saved.png)

## Dashboard und Diagramme bearbeiten {#edit}

Wählen Sie **[!UICONTROL Bearbeiten]** aus, um Ihr gesamtes Dashboard oder Ihre Einblicke zu bearbeiten. Im Bearbeitungsmodus können Sie die Größe von Widgets ändern, SQL bearbeiten oder globale und zeitliche Filter erstellen und anwenden. Diese Filter beschränken die in Ihren Dashboard-Widgets angezeigten Daten. Auf diese Weise können Sie Ihre Einblicke schnell für verschiedene Anwendungsfälle aktualisieren und anpassen.

![Ein benutzerdefiniertes Dashboard mit hervorgehobener Bearbeitung.](../../images/customizable-insights/edit-dashboard.png)

Wählen Sie **[!UICONTROL Filter hinzufügen]** aus, um einen [[!UICONTROL Datumsfilter]](#create-date-filter) oder einen [[!UICONTROL globalen Filter]](#create-global-filter) zu erstellen. Nach der Erstellung sind alle globalen Filter und Datumsfilter in [dem Filtersymbol](#select-global-filter) (![Ein Filtersymbol) verfügbar.](../../images/customizable-insights/filter.png)) Ihres Dashboards.

![Ein benutzerdefiniertes Dashboard mit hervorgehobenem Dropdown-Menü Filter hinzufügen.](../../images/customizable-insights/add-filter.png)

## Insight bearbeiten, duplizieren oder löschen

Anweisungen zum [Bearbeiten, Duplizieren oder Löschen eines vorhandenen Widgets](../../user-defined-dashboards.md#duplicate) finden Sie im Handbuch zu benutzerdefiniertem Dashboard .

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie SQL-Abfragen in die Adobe Experience Platform-Benutzeroberfläche schreiben, um Diagramme für Ihre benutzerdefinierten Dashboards zu generieren. Als Nächstes sollten Sie lernen, wie Sie Journey-Daten weiter anreichern können, indem Sie [einen Datumsfilter erstellen](./filters/date-filter.md) oder [ einen globalen Filter erstellen](./filters/global-filter.md).

Sie können auch mehr über andere benutzerdefinierte Insights-Funktionen erfahren, darunter [die verschiedenen Anzeigeoptionen für SQL-analysierte Daten](./view-more.md) oder [die Anzeige der SQL hinter Ihren benutzerdefinierten Einblicken](./view-sql.md).
