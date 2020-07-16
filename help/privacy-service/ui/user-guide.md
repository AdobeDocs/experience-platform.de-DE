---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Benutzerhandbuch zum Privacy Service
topic: UI guide
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 1%

---


# [!DNL Privacy Service] Benutzerhandbuch

In diesem Dokument werden Schritte zum Erstellen und Verwalten von Datenschutzanforderungen mithilfe der [!DNL Privacy Service] Benutzeroberfläche beschrieben.

## Dashboard der [!DNL Privacy Service] Benutzeroberfläche

Das Dashboard für die [!DNL Privacy Service] Benutzeroberfläche enthält zwei Widgets, mit denen Sie den Status Ihrer Datenschutzaufträge Ansicht haben: **[!UICONTROL Statusbericht]** und **[!UICONTROL Auftragsanforderungen]**. Das Dashboard zeigt auch die aktuell ausgewählte Regel für die angezeigten Aufträge an.

![UI-Dashboard](../images/user-guide/dashboard.png)

### Regeltyp

[!DNL Privacy Service] unterstützt Aufträge für drei Regeltypen:

* Die Europäische Vereinigung [!DNL General Data Protection Regulation] (GDPR)
* Die [!DNL California Consumer Privacy Act] (CCPA)
* Thailands [!DNL Personal Data Protection Act] (PDPA_THA)

Aufträge für jeden Regelungstyp werden separat verfolgt. Um zwischen Regelungstypen zu wechseln, klicken Sie auf das Dropdown-Menü **[!UICONTROL Regelungstyp]** und wählen Sie die gewünschte Regelart aus der Liste aus.

![Dropdownliste Regeltyp](../images/user-guide/regulation.png)

Beim Ändern des Regeltyps wird das Dashboard aktualisiert, um alle Vorgänge, Filter, Widgets und Dialoge zur Schaffung von Arbeitsplätzen anzuzeigen, die für die ausgewählte Regel gelten.

![Aktualisiertes Dashboard](../images/user-guide/dashboard-update.png)

### Statusbericht

Das Diagramm auf der linken Seite des Statusbericht-Widgets verfolgt gesendete Aufträge mit allen Aufträgen, die möglicherweise mit Fehlern zurückgemeldet wurden. Das Diagramm auf der rechten Seite verfolgt Aufträge, die sich am Ende des 30-Tage-Compliance-Fensters befinden.

Klicken Sie auf eine der beiden Schaltflächen über dem Diagramm, um die jeweiligen Metriken ein- oder auszublenden.

![](../images/user-guide/hide-errors.png)

Sie können die exakte Anzahl der Aufträge, die mit einem Datenpunkt auf den Diagrammen verbunden sind, durch Bewegen der Maus über den betreffenden Datenpunkt Ansicht werden.

![Mauszeiger-Datenpunkte](../images/user-guide/mouse-over.png)

Um weitere Details zu einem bestimmten Datenpunkt Ansicht, klicken Sie auf den betreffenden Datenpunkt, um die zugehörigen Aufträge im Widget &quot;Auftragsanforderungen&quot;anzuzeigen. Beachten Sie den Filter, der direkt über der Auftrags-Liste angewendet wird.

![Angewandter Filter aus Widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Wenn ein Filter auf das Widget &quot;Auftragsanforderungen&quot;angewendet wurde, können Sie den Filter entfernen, indem Sie auf das **[!UICONTROL X]** in der Filtertablette klicken. Auftragsanforderungen kehren dann zur standardmäßigen Tracking-Liste zurück.

### Auftragsanforderungen

Das Widget &quot;Auftragsanforderungen&quot;Liste alle in Ihrem Unternehmen verfügbaren Auftragsanforderungen, einschließlich Angaben zum Anforderungstyp, aktuellen Status, Fälligkeitsdatum und E-Mail-Anfrage.

>[!NOTE]
>
>Die Daten für zuvor erstellte Aufträge sind erst 30 Tage nach dem Abschlussdatum verfügbar.

Sie können die Liste filtern, indem Sie Suchbegriffe in die Suchleiste unterhalb des Titels &quot;Auftragsanforderungen&quot;eingeben. Die Liste wird beim Eingeben automatisch Filter und zeigt Anforderungen mit Werten an, die mit Ihren Suchbegriffen übereinstimmen. Sie können auch im Dropdown-Menü &quot; **[!UICONTROL Angefordert am]** &quot;einen Zeitraum für die aufgelisteten Aufträge auswählen.

![Suchoptionen für Auftragsanfragen](../images/user-guide/job-search.png)

Um die Details einer bestimmten Auftragsanforderung Ansicht, klicken Sie in der Liste auf die Auftrags-ID der Anforderung, um die Seite &quot; *[!UICONTROL Auftragsdetails]* &quot;zu öffnen.

![GDPR-UI-Auftragsdetails](../images/user-guide/job-details.png)

Dieser Dialog enthält Statusinformationen zu den einzelnen [!DNL Experience Cloud] Lösungen und ihren aktuellen Status im Verhältnis zum Gesamtauftrag. Da jeder Datenschutzauftrag asynchron ausgeführt wird, zeigt die Seite das aktuelle Kommunikationsdatum und die aktuelle Uhrzeit (GMT) jeder Lösung an, da einige mehr Zeit benötigen als andere, um die Anforderung zu verarbeiten.

Wenn eine Lösung zusätzliche Daten bereitgestellt hat, ist sie in diesem Dialogfeld sichtbar. Sie können diese Daten durch Klicken auf die einzelnen Produktzeilen Ansicht.

Um die vollständigen Auftragsdaten als CSV-Datei herunterzuladen, klicken Sie oben rechts im Dialogfeld auf &quot;In CSV **** exportieren&quot;.

## Neue Datenschutzauftragsanforderung erstellen

>[!NOTE]
>
>Um eine Datenschutzauftragsanforderung zu erstellen, müssen Sie Identitätsinformationen für bestimmte Kunden bereitstellen, deren Daten abgerufen oder gelöscht werden sollen. Bitte lesen Sie das Dokument zu [Identitätsdaten für Datenschutzanforderungen](../identity-data.md) , bevor Sie mit diesem Abschnitt fortfahren.

Die [!DNL Privacy Service] Benutzeroberfläche bietet zwei Methoden zum Erstellen neuer Auftragsanforderungen:

* [Anforderungs-Builder verwenden](#request-builder)
* [JSON-Datei hochladen](#json)

Die Schritte zur Verwendung dieser Methoden sind in den folgenden Abschnitten beschrieben.

### Anforderungs-Builder verwenden {#request-builder}

Mit dem Anforderungs-Builder können Sie in der Benutzeroberfläche manuell eine neue Datenschutzauftragsanforderung erstellen. Der Anforderungs-Builder eignet sich am besten für einfachere und kleinere Anforderungsgruppen, da der Anforderungs-Builder die Anforderungen auf den ID-Typ pro Benutzer beschränkt. Bei komplizierteren Anforderungen ist es möglicherweise besser, stattdessen eine JSON-Datei [hochzuladen](#json) .

Um Beginn mit dem Anforderungs-Builder zu verwenden, klicken Sie auf Anforderung **[!UICONTROL erstellen]** unter dem Statusbericht-Widget auf der rechten Seite des Bildschirms.

![Klicken Sie auf Anforderung erstellen](../images/user-guide/create-request.png)

Das Dialogfeld Anforderung *[!UICONTROL erstellen]* wird geöffnet und zeigt die verfügbaren Optionen zum Senden einer Anforderung zum Schutz der Privatsphäre für den derzeit ausgewählten Regeltyp an.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Wählen Sie den **[!UICONTROL Auftragstyp]** der Anforderung (&quot;Löschen&quot;oder &quot;Zugriff&quot;) und eines oder mehrere verfügbare **[!UICONTROL Produkte]** aus der Liste.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

Wählen Sie unter &quot; *[!UICONTROL Namensraum-Typ]*&quot;den entsprechenden Namensraum-Typ für die Kunden-IDs aus, an die gesendet wird [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Wählen Sie bei Verwendung des _standardmäßigen_ Namensraums einen Namensraum aus dem Dropdown-Menü (E-Mail, ECID oder AAID) und geben Sie dann die ID-Werte in das Textfeld rechts ein. Drücken Sie dann **\&lt;enter>** für jede ID, um sie der Liste hinzuzufügen.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Bei Verwendung des _benutzerdefinierten_ Namensraums müssen Sie den Namensraum manuell eingeben, bevor Sie die unten stehenden ID-Werte eingeben.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Klicken Sie abschließend auf **[!UICONTROL Erstellen]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

Das Dialogfeld wird ausgeblendet und der neue Auftrag (oder die neuen Aufträge) wird zusammen mit dem aktuellen Verarbeitungsstatus im Widget &quot;Auftragsanforderungen&quot;aufgeführt.

### JSON-Datei hochladen {#json}

Wenn Sie komplexere Anforderungen erstellen, z. B. Anforderungen, die mehrere ID-Typen für jede verarbeitete Person verwenden, können Sie eine Anforderung erstellen, indem Sie eine JSON-Datei hochladen.

Klicken Sie auf den Pfeil neben Anforderung **[!UICONTROL erstellen]**, unter dem Statusbericht-Widget auf der rechten Seite des Bildschirms. Wählen Sie in der Liste der angezeigten Optionen die Option JSON **[!UICONTROL hochladen]**.

![Optionen zur Anforderungserstellung](../images/user-guide/create-options.png)

Das Dialogfeld &quot;JSON ** hochladen&quot;wird angezeigt. Es wird ein Fenster angezeigt, in das Sie die JSON-Datei per Drag &amp; Drop verschieben können.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Wenn Sie keine JSON-Datei zum Hochladen haben, klicken Sie auf &quot;Adobe-GDPR-Request.json **** herunterladen&quot;, um eine Vorlage herunterzuladen, die Sie entsprechend den Werten füllen können, die Sie von Ihren betroffenen Personen gesammelt haben.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Suchen Sie die JSON-Datei auf Ihrem Computer und ziehen Sie sie in das Dialogfeld. Wenn der Upload erfolgreich war, wird der Dateiname im Dialogfeld angezeigt. Sie können bei Bedarf weitere JSON-Dateien hinzufügen, indem Sie sie in das Dialogfeld ziehen und dort ablegen.

Klicken Sie abschließend auf **[!UICONTROL Erstellen]**. Das Dialogfeld wird ausgeblendet und der neue Auftrag (oder die neuen Aufträge) wird zusammen mit dem aktuellen Verarbeitungsstatus im Widget &quot; _Auftragsanforderungen_ &quot;aufgeführt.

### Nächste Schritte

Durch Lesen dieses Dokuments haben Sie gelernt, wie Sie mithilfe der [!DNL Privacy Service] Benutzeroberfläche einen Datenschutzauftrag erstellen, die Details eines Auftrags Ansicht geben und dessen Verarbeitungsstatus überwachen und die Ergebnisse nach Abschluss des Vorgangs herunterladen können.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mit der [!DNL Privacy Service] API finden Sie im [Entwicklerhandbuch](../api/getting-started.md).