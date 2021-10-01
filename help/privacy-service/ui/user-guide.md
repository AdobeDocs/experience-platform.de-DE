---
keywords: Experience Platform;Startseite;beliebte Themen;Export;Export
solution: Experience Platform
title: Verwalten von Datenschutzaufträgen in der Privacy Service-Benutzeroberfläche
topic-legacy: UI guide
description: Erfahren Sie, wie Sie mit der Privacy Service-Benutzeroberfläche Datenschutzanfragen in verschiedenen Experience Cloud-Anwendungen koordinieren und überwachen können.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 0%

---

# Verwalten von Datenschutzaufträgen in der Privacy Service-Benutzeroberfläche

Dieses Dokument enthält Schritte zum Erstellen und Verwalten von Datenschutzanfragen mithilfe der [!DNL Privacy Service]-Benutzeroberfläche.

## Durchsuchen Sie das Dashboard der Benutzeroberfläche [!DNL Privacy Service]

Das Dashboard für die [!DNL Privacy Service]-Benutzeroberfläche bietet zwei Widgets, mit denen Sie den Status Ihrer Datenschutzaufträge anzeigen können: &quot;[!UICONTROL Statusbericht]&quot;und &quot;[!UICONTROL Auftragsanfragen]&quot;. Im Dashboard wird auch die aktuell ausgewählte Regel für die angezeigten Aufträge angezeigt.

![UI-Dashboard](../images/user-guide/dashboard.png)

### Regelungstyp

[!DNL Privacy Service] unterstützt Auftragsanfragen für verschiedene Datenschutzbestimmungen:

* Die [!DNL California Consumer Privacy Act] ([!UICONTROL CCPA])
* Die [!DNL General Data Protection Regulation] der Europäischen Union ([!UICONTROL DSGVO])
* Thailändisches [!DNL Personal Data Protection Act] ([!UICONTROL PDPA_THA])
* Brasiliens [!DNL Lei Geral de Proteção de Dados] ([!UICONTROL LGPD_BRA])
* Neuseeland [!DNL Privacy Act] ([!UICONTROL NZPA_NZL])

Aufträge für jeden Regulierungstyp werden separat verfolgt. Um zwischen Regelungstypen zu wechseln, wählen Sie das Dropdown-Menü **[!UICONTROL Regulierungstyp]** aus und wählen Sie die gewünschte Vorschrift aus der Liste aus.

![Dropdown-Liste für Regelungstypen](../images/user-guide/regulation.png)

Nach Änderung des Regulierungstyps wird das Dashboard aktualisiert, um alle Vorgänge, Filter, Widgets und Dialogfelder zur Schaffung von Arbeitsplätzen anzuzeigen, die für die ausgewählte Verordnung gelten.

![Aktualisiertes Dashboard](../images/user-guide/dashboard-update.png)

### Statusbericht

Das Diagramm auf der linken Seite des Widgets &quot;Statusbericht&quot;verfolgt gesendete Aufträge für alle Aufträge, die möglicherweise mit Fehlern gemeldet wurden. Das Diagramm auf der rechten Seite verfolgt Aufträge, die sich dem Ende des 30-Tage-Compliance-Fensters nähern.

Wählen Sie eine der beiden Umschalter-Schaltflächen über dem Diagramm aus, um die entsprechenden Metriken ein- oder auszublenden.

![](../images/user-guide/hide-errors.png)

Sie können die genaue Anzahl der Aufträge anzeigen, die mit einem Datenpunkt in den Diagrammen verbunden sind, indem Sie den Mauszeiger über den betreffenden Datenpunkt bewegen.

![Überlaufdatenpunkte](../images/user-guide/mouse-over.png)

Um weitere Details zu einem bestimmten Datenpunkt anzuzeigen, wählen Sie den betreffenden Datenpunkt aus, um die zugehörigen Aufträge im Widget Auftragsanfragen anzuzeigen. Beachten Sie den Filter, der direkt über der Auftragsliste angewendet wird.

![Angewandter Filter aus Widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Wenn ein Filter auf das Widget Auftragsanforderungen angewendet wurde, können Sie den Filter entfernen, indem Sie in der Filtertablette **X** auswählen. Auftragsanfragen kehren dann zur standardmäßigen Tracking-Liste zurück.

### Auftragsanforderungen

Das Widget Auftragsanfragen listet alle in Ihrem Unternehmen verfügbaren Auftragsanfragen auf, einschließlich Details zum Anfragetyp, aktuellen Status, Fälligkeitsdatum und E-Mail-Adresse des Anfragenden.

>[!NOTE]
>
>Auf die Daten für zuvor erstellte Aufträge kann erst 30 Tage nach dem Abschlussdatum zugegriffen werden.

Sie können die Liste filtern, indem Sie Suchbegriffe in die Suchleiste unter dem Titel Auftragsanfragen eingeben. Die Liste filtert automatisch bei der Eingabe und zeigt Anforderungen an, die Werte enthalten, die Ihren Suchbegriffen entsprechen. Sie können auch das Dropdown-Menü **[!UICONTROL Angefordert für]** verwenden, um einen Zeitraum für die aufgelisteten Aufträge auszuwählen.

![Suchoptionen für Auftragsanfragen](../images/user-guide/job-search.png)

Um die Details einer bestimmten Auftragsanfrage anzuzeigen, wählen Sie die Auftrags-ID der Anfrage aus der Liste aus, um die Seite **[!UICONTROL Auftragsdetails]** zu öffnen.

![DSGVO-UI-Auftragsdetails](../images/user-guide/job-details.png)

Dieses Dialogfeld enthält Statusinformationen zu den einzelnen [!DNL Experience Cloud]-Lösungen und deren aktueller Status in Bezug auf den Gesamtauftrag. Da jeder Datenschutzauftrag asynchron ausgeführt wird, zeigt die Seite das aktuelle Kommunikationsdatum und die aktuelle Uhrzeit (GMT) jeder Lösung an, da einige für die Verarbeitung der Anfrage mehr Zeit als andere benötigen.

Wenn eine Lösung zusätzliche Daten bereitgestellt hat, ist dies in diesem Dialogfeld sichtbar. Sie können diese Daten durch Auswahl einzelner Produktzeilen anzeigen.

Um die vollständigen Auftragsdaten als CSV-Datei herunterzuladen, wählen Sie **[!UICONTROL Export in CSV]** oben rechts im Dialogfeld aus.

## Neue Datenschutzauftragsanforderung erstellen

>[!NOTE]
>
>Um eine Datenschutzanfrage zu erstellen, müssen Sie Identitätsinformationen für die spezifischen Kunden bereitstellen, deren Daten aufgerufen oder gelöscht werden sollen. Lesen Sie das Dokument zu [Identitätsdaten für Datenschutzanfragen](../identity-data.md) , bevor Sie mit diesem Abschnitt fortfahren.

Die Benutzeroberfläche [!DNL Privacy Service] bietet zwei Methoden zum Erstellen neuer Auftragsanforderungen:

* [Verwenden des Anforderungs-Builders](#request-builder)
* [JSON-Datei hochladen](#json)

Die Schritte zur Verwendung dieser Methoden finden Sie in den folgenden Abschnitten.

### Verwenden des Anforderungs-Builders {#request-builder}

Mit dem Request Builder können Sie in der Benutzeroberfläche manuell eine neue Datenschutzauftragsanforderung erstellen. Der Request Builder eignet sich am besten für einfachere und kleinere Anforderungsgruppen, da der Request Builder die Anforderungen so beschränkt, dass sie nur einen ID-Typ pro Benutzer haben. Bei komplexeren Anforderungen ist es möglicherweise besser, [stattdessen eine JSON-Datei](#json) hochzuladen.

Um mit der Verwendung des Anforderungs-Builders zu beginnen, wählen Sie **[!UICONTROL Anforderung erstellen]** unter dem Widget Statusbericht auf der rechten Seite des Bildschirms aus.

![Anforderung erstellen](../images/user-guide/create-request.png)

Das Dialogfeld **[!UICONTROL Anfrage erstellen]** wird geöffnet und enthält die verfügbaren Optionen zum Senden einer Datenschutzauftragsanforderung für den derzeit ausgewählten Regulierungstyp.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Wählen Sie den **[!UICONTROL Auftragstyp]** der Anforderung (&quot;Löschen&quot;oder &quot;Zugriff&quot;) und ein oder mehrere verfügbare Produkte aus der Liste aus.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

Wählen Sie unter **[!UICONTROL Namespace type]** den entsprechenden Namespace-Typ für die Kunden-IDs aus, die an [!DNL Privacy Service] gesendet werden.

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Wählen Sie bei Verwendung des Standard-Namespace-Typs einen Namespace aus dem Dropdown-Menü (E-Mail, ECID oder AAID) aus, geben Sie dann die ID-Werte in das Textfeld rechts ein und drücken Sie **\&lt;enter>** für jede ID, um sie der Liste hinzuzufügen.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Bei Verwendung des benutzerdefinierten Namespace-Typs müssen Sie den Namespace manuell eingeben, bevor Sie die unten stehenden ID-Werte angeben.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Klicken Sie abschließend auf **[!UICONTROL Erstellen]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

Das Dialogfeld wird ausgeblendet und der neue Auftrag (oder die neuen Aufträge) wird im Widget Auftragsanfragen zusammen mit dem aktuellen Verarbeitungsstatus aufgeführt.

### JSON-Datei hochladen {#json}

Beim Erstellen komplexerer Anforderungen, z. B. Anforderungen, die mehrere ID-Typen für jedes verarbeitete Datensubjekt verwenden, können Sie eine Anforderung erstellen, indem Sie eine JSON-Datei hochladen.

Wählen Sie den Pfeil neben **[!UICONTROL Anfrage erstellen]** unter dem Widget Statusbericht auf der rechten Seite des Bildschirms aus. Wählen Sie in der angezeigten Liste der Optionen **[!UICONTROL JSON hochladen]** aus.

![Erstellungsoptionen von Anforderungen](../images/user-guide/create-options.png)

Das Dialogfeld **[!UICONTROL JSON]** hochladen wird angezeigt und bietet ein Fenster, in das Sie Ihre JSON-Datei per Drag-and-Drop verschieben können.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Wenn Sie keine JSON-Datei hochladen möchten, wählen Sie **[!UICONTROL Adobe-DSGVO-Anfrage.json herunterladen]** aus, um eine Vorlage herunterzuladen, die Sie entsprechend den von Ihren Datensubjekten erfassten Werten füllen können.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Suchen Sie die JSON-Datei auf Ihrem Computer und ziehen Sie sie in das Dialogfenster. Wenn der Upload erfolgreich war, wird der Dateiname im Dialogfeld angezeigt. Sie können bei Bedarf weitere JSON-Dateien hinzufügen, indem Sie sie per Drag-and-Drop in das Dialogfeld ziehen.

Klicken Sie abschließend auf **[!UICONTROL Erstellen]**. Das Dialogfeld wird ausgeblendet und der neue Auftrag (oder die neuen Aufträge) wird im Widget Auftragsanfragen zusammen mit dem aktuellen Verarbeitungsstatus aufgeführt.

### Nächste Schritte

Durch Lesen dieses Dokuments haben Sie gelernt, wie Sie mit der [!DNL Privacy Service]-Benutzeroberfläche einen Datenschutzauftrag erstellen, die Details eines Auftrags anzeigen und seinen Verarbeitungsstatus überwachen und die Ergebnisse nach Abschluss herunterladen können.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mit der [!DNL Privacy Service]-API finden Sie im [Entwicklerhandbuch](../api/getting-started.md).
