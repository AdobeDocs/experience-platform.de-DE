---
title: SQL Insights für erweiterte App-Berichte
description: Erfahren Sie, wie Sie mit SQL-Abfragen Einblicke für Ihre benutzerdefinierten Dashboards generieren können.
exl-id: c60a9218-4ac0-4638-833b-bdbded36ddf5
source-git-commit: 9f4ce2a3a8af72342683c859caa270662b161b7d
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 0%

---

# SQL Insights für erweiterte App-Berichte

Verwenden Sie benutzerdefinierte SQL-Abfragen, um effektiv Einblicke aus verschiedenen strukturierten Datensätzen zu extrahieren. Technische Mitarbeiter können den Abfragemodus verwenden, um komplexe Analysen mit SQL durchzuführen und diese Analyse dann über Diagramme in Ihrem benutzerdefinierten Dashboard oder CSV-Dateien für nicht-technische Benutzer freizugeben. Diese Methode der insight-Erstellung eignet sich gut für Tabellen mit klaren Beziehungen und ermöglicht einen größeren Grad der Anpassung Ihrer Einblicke und Filter, die für Nischenanwendungsfälle geeignet sind.

>[!IMPORTANT]
>
>Der Query Pro-Modus ist nur für Benutzer verfügbar, die die [Data Distiller SKU) ](../../query-service/data-distiller/overview.md) haben.

Um Insights aus SQL zu generieren, müssen Sie zunächst ein Dashboard erstellen.

## Erstellen eines benutzerdefinierten Dashboards {#create-custom-dashboard}

Um ein benutzerdefiniertes Dashboard zu erstellen, wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Dashboards]** aus, um den Arbeitsbereich Dashboards zu öffnen. Wählen Sie als Nächstes **[!UICONTROL Create dashboard]**.

![Das Dashboard-Inventar mit hervorgehobener Option „Dashboard erstellen“.](../images/sql-insights-query-pro-mode/create-dashboard.png)

Das Dialogfeld **[!UICONTROL Create dashboard]** wird angezeigt. Es gibt zwei Optionen, aus denen Sie Ihre Methode zur Dashboard-Erstellung auswählen können. Um Ihre Insights zu erstellen, können Sie entweder ein vorhandenes Datenmodell mit dem [[!UICONTROL Guided design mode]](../standard-dashboards.md) oder Ihre eigene SQL mit dem [!UICONTROL Query pro mode] verwenden.

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

Die Verwendung eines vorhandenen Datenmodells bietet die Vorteile eines strukturierten, effizienten und skalierbaren Frameworks, das auf Ihre spezifischen Geschäftsanforderungen zugeschnitten ist. Informationen zum [ (Erstellen von Einblicken aus einem vorhandenen Datenmodell](../standard-dashboards.md#create-widget) finden Sie im Handbuch zum benutzerdefinierten Dashboard .

Erkenntnisse, die aus SQL-Abfragen generiert werden, bieten eine viel größere Flexibilität und Anpassung. Technische Mitarbeiter können den Abfragemodus verwenden, um komplexe Analysen zu SQL durchzuführen und diese Analyse dann über diese Dashboard-Funktion für nicht-technische Benutzer freizugeben. Wählen Sie **[!UICONTROL Query pro mode]** und dann **[!UICONTROL Save]** aus.

>[!NOTE]
>
>Nachdem Sie eine Auswahl getroffen haben, können Sie diese Auswahl in diesem Dashboard nicht mehr ändern. Stattdessen müssen Sie ein neues Dashboard mit einer anderen Methode zur Dashboard-Erstellung erstellen.

![Das Dialogfeld &quot;[!UICONTROL Create dashboard]&quot; mit hervorgehobenem „Query Pro-Modus“ und „Speichern“.](../images/sql-insights-query-pro-mode/query-pro-mode.png)

## Query Pro-Modus - Übersicht {#query-pro-mode}

Query Pro-Modus ist ein SQL-Editor-basierter Workflow, der Sie durch den Prozess der Generierung von Insights mit benutzerdefinierten SQL-Abfragen in der Adobe Experience Platform-Benutzeroberfläche führt. Bevor Sie Insights mit benutzerdefinierten SQL-Abfragen generieren können, müssen Sie zunächst ein Dashboard erstellen.

## SQL erstellen {#compose-sql}

Nachdem Sie sich entschieden haben, ein Dashboard mit dem Abfrage-Pro-Modus zu erstellen, wird das **[!UICONTROL Enter SQL]**-Dialogfeld angezeigt. Wählen Sie aus dem Dropdown-Menü eine Datenbank (Insights-Datenmodell) aus, die Sie abfragen möchten, und geben Sie im Abfrage-Editor eine geeignete Abfrage für Ihren Datensatz ein.

>[!NOTE]
>
>Der Pro-Modus „Abfrage“ ist nur für Benutzende verfügbar, die die Data Distiller SKU erworben haben. Die [[!UICONTROL Guided design mode]](../standard-dashboards.md) steht allen Benutzern zur Verfügung, um Einblicke aus einem vorhandenen Datenmodell zu erstellen.

Weitere Informationen [ Benutzeroberflächenelemente finden Sie ](../../query-service/ui/user-guide.md#query-authoring) Benutzerhandbuch zum Abfrage-Editor .

![Das Dialogfeld &quot;[!UICONTROL Enter SQL]&quot; mit hervorgehobenem Dropdown-Menü „Datensatz“ und dem Symbol „Ausführen“. Das Dialogfeld enthält eine ausgefüllte SQL-Abfrage und die Registerkarte „Abfrageparameter“ wird angezeigt.](../images/sql-insights-query-pro-mode/enter-sql-database-dropdown.png)

### Abfrageparameter {#query-parameters}

Um [globale](./filters/global-filter.md) oder [Datumsfilter einzuschließen](./filters/date-filter.md) muss **Abfrage**. Wenn Sie Ihre Anweisung im Abfragemodus erstellen, müssen Sie Beispielwerte angeben, wenn Ihre Abfrage Abfrageparameter verwendet. Anhand der Beispielwerte können Sie die SQL-Anweisung ausführen und das Diagramm erstellen. Beachten Sie, dass die Beispielwerte, die Sie beim Erstellen Ihrer Anweisung angeben, durch die tatsächlichen Werte ersetzt werden, die Sie zur Laufzeit für den Datums- oder globalen Filter auswählen.

>[!IMPORTANT]
>
>Wenn Sie einen globalen Filter verwenden möchten, müssen Sie einen Abfrageparameter in Ihrer SQL platzieren und diesen Abfrageparameter dann mit dem globalen Filter im Widget-Composer verknüpfen. Im folgenden Screenshot wird `CONSENT_VALUE_FILTER` in SQL als Abfrageparameter für einen globalen Filter verwendet. Weitere Informationen dazu finden [ in ](./filters/global-filter.md#enable-global-filter) Dokumentation zum globalen Filter .

Um Ihre Abfrage auszuführen, wählen Sie das Symbol „Ausführen“ (![das Symbol „Ausführen„).](/help/images/icons/play.png)). Der Abfrage-Editor zeigt die Registerkarte Ergebnisse an. Wählen Sie als Nächstes **[!UICONTROL Select]** aus, um Ihre Konfiguration zu bestätigen und den Widget-Composer zu öffnen.

>[!TIP]
>
>Wenn Ihre Abfrage Abfrageparameter verwendet, führen Sie die Abfrage einmal aus, um alle verwendeten Abfrageparameterschlüssel vorauszufüllen. Die Abfrage schlägt fehl, aber die Benutzeroberfläche zeigt automatisch die Registerkarte Abfrageparameter an und listet alle enthaltenen Schlüssel auf. Fügen Sie die entsprechenden Werte für Ihre Schlüssel hinzu.

![Das Dialogfeld &quot;[!UICONTROL Enter SQL]&quot; mit SQL-Eingabe, die Registerkarte „Ergebnisse“ wird angezeigt, und „Auswählen“ ist hervorgehoben.](../images/sql-insights-query-pro-mode/enter-sql-select.png)

## Widget befüllen {#populate-widget}

Der Widget-Composer wird jetzt mit den Spalten aus der ausgeführten SQL gefüllt. Der Typ des Dashboards wird oben links angezeigt. In diesem Fall ist er [!UICONTROL Manual SQL Entry]. Wählen Sie das Stiftsymbol (![Bleistiftsymbol) aus.](/help/images/icons/edit.png)), um die SQL jederzeit zu bearbeiten.

>[!TIP]
>
>Die verfügbaren Attribute sind Spalten, die aus der ausgeführten SQL übernommen werden.

Um Ihr Widget zu erstellen, verwenden Sie die in der Spalte [!UICONTROL Attributes] aufgeführten Attribute. Sie können die Suchleiste verwenden, um nach Attributen zu suchen oder durch die Liste zu scrollen.

![Der Widget-Composer mit der hervorgehobenen Erstellungsmethode und Attributspalte.](../images/sql-insights-query-pro-mode/creation-method-and-attribute-column.png)

### Attribute hinzufügen {#add-attributes}

Um ein Attribut zu Ihrem Widget hinzuzufügen, wählen Sie das Pluszeichen (![A Pluszeichen) aus.](/help/images/icons/add-circle.png)) neben einem Attributnamen. Im angezeigten Dropdown-Menü können Sie dem Diagramm aus den von Ihrer SQL bestimmten Optionen ein Attribut hinzufügen. Verschiedene Diagrammtypen haben unterschiedliche Optionen, z. B. eine Dropdown-Liste für die X- und Y-Achse.

In diesem Beispiel für ein Ringdiagramm sind die Optionen Größe und Farbe. Farbe schlüsselt die Ergebnisse des Ringdiagramms auf und die Größe ist die tatsächlich verwendete Metrik. Fügen Sie dem Feld [!UICONTROL Color] ein Attribut hinzu, um die Ergebnisse je nach ihrer Zusammensetzung dieses Attributs in verschiedene Farben aufzuteilen.

>[!TIP]
>
>Wählen Sie die Pfeile nach oben und unten aus ![Das Pfeilsymbol nach oben und unten.](/help/images/icons/switch.png)), um die Anordnung der X- und Y-Achse auf Balken- oder Liniendiagrammen zu ändern.

![Der Widget-Composer mit hervorgehobener Dropdown-Liste mit dem Add-Symbol und hervorgehobenen Umschalt-Pfeilen.](../images/sql-insights-query-pro-mode/add-icon-and-switch-arrows.png)

Um den Typ des Diagramms oder Diagramms Ihres Widgets zu ändern, wählen Sie aus den verfügbaren Optionen der Dropdown-Liste [!UICONTROL Marks] aus. Zu den Optionen gehören [!UICONTROL Line], [!UICONTROL Donut], [!UICONTROL Big number] und [!UICONTROL Bar]. Nach der Auswahl wird eine Vorschauvisualisierung der aktuellen Einstellungen Ihres Widgets generiert.

![Der Widget-Composer mit der hervorgehobenen Widget-Vorschau.](../images/sql-insights-query-pro-mode/widget-preview.png)

## Erweiterte Tabellenattribute {#advanced-attributes}

Um automatische Sortierfunktionen auf eine oder alle Spalten in Ihren Tabellen anzuwenden, wählen Sie **[!UICONTROL Edit]** aus, um das gesamte Dashboard zu bearbeiten.

![Ein benutzerdefiniertes Dashboard mit hervorgehobener Option „Bearbeiten“.](../images/sql-insights-query-pro-mode/advanced-edit-dashboard.png)

Klicken Sie auf die Auslassungszeichen (`...`) im Tabellendiagramm, dem Sie eine Spaltensortierung hinzufügen möchten, und klicken Sie dann auf **[!UICONTROL Edit]**.

![Eine Tabelle mit dem Auslassungsmenü und hervorgehobener Option „Bearbeiten“.](../images/sql-insights-query-pro-mode/advanced-table-edit.png)

Um die Sortierung für eine beliebige Spalte zu aktivieren, aktivieren Sie die **[!UICONTROL Sortable]**.

![Seite „Tabelle bearbeiten“ mit hervorgehobenen sortierbaren Kontrollkästchen.](../images/sql-insights-query-pro-mode/advanced-table-sortable.png)

Wählen Sie das Eigenschaftensymbol (![das Eigenschaftensymbol.](/help/images/icons/properties.png)) in der rechten Leiste aus, um das [!UICONTROL Properties] zu öffnen. Wählen Sie im **[!UICONTROL Properties]**-Bereich mithilfe der Dropdown-Liste die **[!UICONTROL Default sort]** Spalte und wählen Sie dann mithilfe der Dropdown-Liste die **[!UICONTROL Sort direction]** aus. Wählen Sie abschließend **[!UICONTROL Save and close]** aus.

![Der Widget-Composer mit dem Symbol „Eigenschaften“, hervorgehobener Standardsortierung, Sortierrichtung und hervorgehobener Schaltfäche „Speichern und schließen“.](../images/sql-insights-query-pro-mode/advanced-table-properties.png)

Weitere Informationen zur Verwendung der Funktionen zum Sortieren, Ändern der Spaltengröße und zur Paginierung finden Sie unter [Weitere Informationen](./view-more.md).

## Widget-Eigenschaften {#properties}

Wählen Sie das Eigenschaftensymbol (![das Eigenschaftensymbol.](/help/images/icons/properties.png)) in der rechten Leiste aus, um den Bereich „Eigenschaften“ zu öffnen. Geben Sie im [!UICONTROL Properties] Bedienfeld einen Namen für das Widget in das **[!UICONTROL Widget title]** Textfeld ein. Sie können auch verschiedene Aspekte Ihres Diagramms umbenennen.

>[!NOTE]
>
>Die in der Seitenleiste „Eigenschaften“ verfügbaren spezifischen Felder variieren je nach dem Diagrammtyp, den Sie bearbeiten.

![Der Widget-Composer mit dem Eigenschaftensymbol und dem hervorgehobenen Feld „Widget-Titel“.](../images/sql-insights-query-pro-mode/widget-properties-title-text.png)

## Widget speichern {#save-widget}

Beim Speichern im Widget Composer wird das Widget lokal im Dashboard gespeichert. Wenn Sie Ihre Arbeit speichern und später fortsetzen möchten, wählen Sie **[!UICONTROL Save]** aus. Ein Häkchen unter dem Widget-Namen zeigt an, dass das Widget gespeichert wurde. Wenn Sie mit Ihrem Widget zufrieden sind, können Sie das Widget auch **[!UICONTROL Save and close]** auswählen, damit es allen anderen Benutzern mit Zugriff auf Ihr Dashboard zur Verfügung steht. Wählen Sie Abbrechen aus, um Ihre Arbeit abzubrechen und zu Ihrem benutzerdefinierten Dashboard zurückzukehren.

![Der Widget-Composer mit den hervorgehobenen Optionen „Speichern“, „Widget gespeichert“ und „Speichern und schließen“.](../images/sql-insights-query-pro-mode/insight-saved.png)

## Dashboard und Diagramme bearbeiten {#edit}

Wählen Sie **[!UICONTROL Edit]** aus, um Ihr gesamtes Dashboard oder eines Ihrer Insights zu bearbeiten. Im Bearbeitungsmodus können Sie die Größe von Widgets ändern, Ihre SQL bearbeiten oder globale und zeitliche Filter erstellen und anwenden. Diese Filter schränken die Daten ein, die in Ihren Dashboard-Widgets angezeigt werden. Dies ist eine praktische Methode, um Ihre Insights schnell zu aktualisieren und für verschiedene Anwendungsfälle zu optimieren.

![Ein benutzerdefiniertes Dashboard mit hervorgehobener Option „Bearbeiten“.](../images/sql-insights-query-pro-mode/edit-dashboard.png)

Wählen Sie **[!UICONTROL Add filter]** aus, um entweder eine [[!UICONTROL Date filter]](#create-date-filter) oder eine [[!UICONTROL Global filter]](#create-global-filter) zu erstellen. Nach der Erstellung sind alle globalen Filter und Datumsfilter über das [Filtersymbol](#select-global-filter) verfügbar (![Filtersymbol.](/help/images/icons/filter.png)) Ihres Dashboards aus.

![Ein benutzerdefiniertes Dashboard mit hervorgehobenem Dropdown-Menü „Filter hinzufügen“.](../images/sql-insights-query-pro-mode/add-filter.png)

## Insight bearbeiten, duplizieren oder löschen

Anweisungen zum Bearbeiten, Duplizieren oder Löschen eines vorhandenen Widgets [ Sie im Handbuch zum benutzerdefinierten Dashboard ](../standard-dashboards.md#duplicate).

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie SQL-Abfragen in der Adobe Experience Platform-Benutzeroberfläche schreiben, um Diagramme für Ihre benutzerdefinierten Dashboards zu generieren. Als Nächstes sollten Sie lernen, wie Sie Ihre Daten durch [Erstellen eines Datumsfilters](./filters/date-filter.md) oder [Erstellen eines globalen Filters](./filters/global-filter.md) weiter anreichern können.

Sie können auch mehr über andere Custom Insights-Funktionen erfahren, darunter [die verschiedenen Anzeigeoptionen für Ihre SQL-analysierten Daten](./view-more.md) oder wie Sie [ SQL hinter Ihren benutzerdefinierten Insights ](./view-sql.md).
