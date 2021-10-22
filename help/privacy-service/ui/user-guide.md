---
keywords: Experience Platform;Home;beliebte Themen;Exportieren;Exportieren
solution: Experience Platform
title: Datenschutzaufträge in der Benutzeroberfläche des Privacy Service verwalten
topic-legacy: UI guide
description: Erfahren Sie, wie Sie die Benutzeroberfläche von Privacy Service verwenden, um Datenschutzanforderungen in verschiedenen Experience Cloud-Anwendungen zu koordinieren und zu überwachen.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 0%

---

# Datenschutzaufträge in der Benutzeroberfläche des Privacy Service verwalten

In diesem Dokument werden Schritte zum Erstellen und Verwalten von Datenschutzanfragen mithilfe der [!DNL Privacy Service] Benutzeroberfläche.

## Durchsuchen der [!DNL Privacy Service] UI-Dashboard

Das Dashboard für [!DNL Privacy Service] UI stellt zwei Widgets zur Verfügung, mit denen Sie den Status Ihrer Datenschutzaufträge Ansicht haben: &quot;[!UICONTROL Statusbericht]&quot; und &quot;[!UICONTROL Auftragsersuchen]&quot;. Das Dashboard zeigt auch die aktuell ausgewählte Regel für die angezeigten Aufträge an.

![UI-Dashboard](../images/user-guide/dashboard.png)

### Regeltyp

[!DNL Privacy Service] unterstützt Aufträge für mehrere Datenschutzbestimmungen:

* Die [!DNL California Consumer Privacy Act] ([!UICONTROL CCPA])
* Die Europäische Vereinigung [!DNL General Data Protection Regulation] ([!UICONTROL GDPR])
* Thailands [!DNL Personal Data Protection Act] ([!UICONTROL PDPA_THA])
* Brasiliens [!DNL Lei Geral de Proteção de Dados] ([!UICONTROL LGPD_BRA])
* Neuseeland [!DNL Privacy Act] ([!UICONTROL NZPA_NZL])

Aufträge für jeden Regelungstyp werden separat verfolgt. Um zwischen Regeltypen zu wechseln, wählen Sie **[!UICONTROL Regeltyp]** und wählen Sie die gewünschte Regelung aus der Liste aus.

![Dropdown für Regeltyp](../images/user-guide/regulation.png)

Beim Ändern des Regeltyps wird das Dashboard aktualisiert, um alle Vorgänge, Filter, Widgets und Dialoge zur Schaffung von Arbeitsplätzen anzuzeigen, die für die ausgewählte Verordnung gelten.

![Aktualisiertes Dashboard](../images/user-guide/dashboard-update.png)

### Statusbericht

Das Diagramm auf der linken Seite des Statusbericht-Widgets verfolgt gesendete Aufträge anhand von Aufträgen, die möglicherweise mit Fehlern zurückgemeldet wurden. Das Diagramm auf der rechten Seite verfolgt Jobs, die sich dem Ende des 30-Tage-Compliance-Fensters nähern.

Wählen Sie eine der beiden Schaltflächen über dem Diagramm aus, um die jeweiligen Metriken ein- oder auszublenden.

![](../images/user-guide/hide-errors.png)

Sie können die exakte Anzahl von Aufträgen, die mit einem Datenpunkt auf den Diagrammen verbunden sind, durch Bewegen der Maus über den betreffenden Datenpunkt Ansicht werden.

![Mauszeiger-Datenpunkte](../images/user-guide/mouse-over.png)

Um weitere Details über einen bestimmten Datenpunkt Ansicht, wählen Sie den betreffenden Datenpunkt aus, um die zugehörigen Aufträge im Widget &quot;Auftragsersuchen&quot;anzuzeigen. Beachten Sie den Filter, der direkt über der Liste des Auftrags angewendet wird.

![Angewendeter Filter aus Widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Wenn ein Filter auf das Auftrags-Widget angewendet wurde, können Sie den Filter entfernen, indem Sie **X** auf der Filtertablette. Auftragsanfragen kehren dann zur Standard-Tracking-Liste zurück.

### Auftragsersuchen

Das Auftragsanfrage-Widget Liste alle verfügbaren Auftragsanforderungen in Ihrem Unternehmen, einschließlich Details wie Anfragetyp, Aktueller Status, Fälligkeitsdatum und E-Mail-Adresse des Anforderers.

>[!NOTE]
>
>Auf die Daten für zuvor erstellte Aufträge kann erst 30 Tage nach dem Abschlussstichtag zugegriffen werden.

Sie können die Liste filtern, indem Sie Stichwörter in die Suchleiste unter dem Titel &quot;Auftragsersuchen&quot;eingeben. Die Liste wird während der Eingabe automatisch Filter und zeigt Anforderungen an, die Werte enthalten, die mit Ihren Suchbegriffen übereinstimmen. Sie können auch **[!UICONTROL Angefordert am]** aus dem Dropdown-Menü, um einen Zeitbereich für die aufgelisteten Aufträge auszuwählen.

![Suchoptionen für Auftragsanfragen](../images/user-guide/job-search.png)

Um die Details einer bestimmten Auftragsanfrage Ansicht, wählen Sie die Auftrags-ID der Anforderung in der Liste aus, um die **[!UICONTROL Auftragsdetails]** Seite.

![GDPR-UI-Auftragsdetails](../images/user-guide/job-details.png)

Dieses Dialogfeld enthält Statusinformationen zu jedem [!DNL Experience Cloud] -Lösung und deren aktueller Status im Verhältnis zum Gesamtauftrag. Da jeder Datenschutzauftrag asynchron ist, zeigt die Seite das aktuelle Datum und die Uhrzeit der Kommunikation (GMT) aus jeder Lösung an, da einige für die Verarbeitung der Anforderung mehr Zeit benötigen als andere.

Wenn eine Lösung zusätzliche Daten bereitgestellt hat, kann sie in diesem Dialogfeld angezeigt werden. Sie können diese Daten durch Auswahl einzelner Produktzeilen Ansicht werden.

Um die vollständigen Auftragsdaten als CSV-Datei herunterzuladen, wählen Sie **[!UICONTROL In CSV exportieren]** oben rechts im Dialog.

## Neue Datenschutzanfrage erstellen

>[!NOTE]
>
>Um eine Datenschutzanfrage zu erstellen, müssen Sie Identitätsinformationen für bestimmte Kunden bereitstellen, auf deren Daten zugegriffen oder gelöscht werden soll. Überprüfen Sie das Dokument auf [Identitätsdaten für Datenschutzanfragen](../identity-data.md) bevor Sie mit diesem Abschnitt fortfahren.

Die [!DNL Privacy Service] Die Benutzeroberfläche bietet zwei Methoden zum Erstellen neuer Auftragsersuchen:

* [Anforderungs-Builder verwenden](#request-builder)
* [JSON-Datei hochladen](#json)

Die Schritte zur Anwendung dieser Methoden sind in den folgenden Abschnitten beschrieben.

### Anforderungs-Builder verwenden {#request-builder}

Mit dem Request Builder können Sie manuell eine neue Datenschutzauftragsanfrage in der Benutzeroberfläche erstellen. Der Anforderungsaufbau wird am besten für einfachere und kleinere Gruppen von Anforderungen verwendet, da der Anforderungs-Builder Anforderungen nur einen ID-Typ pro Benutzer angibt. Bei komplizierteren Anfragen ist es unter Umständen besser, [JSON-Datei hochladen](#json) statt.

Wählen Sie zum Beginn mit dem Request-Builder **[!UICONTROL Anforderung erstellen]** unter dem Statusbericht-Widget auf der rechten Seite des Bildschirms.

![Anforderung erstellen](../images/user-guide/create-request.png)

Die **[!UICONTROL Anforderung erstellen]** öffnet sich ein Dialogfeld, in dem die verfügbaren Optionen zum Senden eines Datenschutzauftrags für den aktuell ausgewählten Regelungstyp angezeigt werden.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Wählen Sie **[!UICONTROL Auftragstyp]** der Anforderung (&quot;Löschen&quot; oder &quot;Zugriff&quot;) und eines oder mehrere verfügbare Produkte aus der Liste.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

Unter **[!UICONTROL Namensraum-Typ]** wählen Sie den entsprechenden Namensraum-Typ für die Kunden-IDs aus, an die gesendet wird [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Wenn Sie den Standardtyp eines Namensraums verwenden, wählen Sie einen Namensraum aus dem Dropdown-Menü (E-Mail, ECID oder AAID) aus, geben Sie dann die ID-Werte in das Textfeld rechts ein und drücken Sie die Eingabetaste. **\&lt;enter>** für jede ID, um sie der Liste hinzuzufügen.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Wenn Sie den benutzerdefinierten Namensraum-Typ verwenden, müssen Sie den Namensraum manuell eingeben, bevor Sie die unten stehenden ID-Werte eingeben können.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Klicken Sie abschließend auf **[!UICONTROL Erstellen]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

Der Dialog verschwindet und der neue Auftrag (oder die neuen Aufträge) werden zusammen mit dem aktuellen Verarbeitungsstatus im Widget &quot;Auftragsersuchen&quot;aufgeführt.

### JSON-Datei hochladen {#json}

Wenn Sie komplexere Anforderungen erstellen, z. B. Anforderungen, die für jede verarbeitete Person mehrere ID-Typen verwenden, können Sie eine Anforderung erstellen, indem Sie eine JSON-Datei hochladen.

Pfeil neben **[!UICONTROL Anforderung erstellen]**, unter dem Statusbericht-Widget auf der rechten Seite des Bildschirms. Wählen Sie in der Liste der angezeigten Optionen **[!UICONTROL JSON hochladen]**.

![Erstellungsoptionen anfordern](../images/user-guide/create-options.png)

Die **[!UICONTROL JSON hochladen]** erscheint und gibt Ihnen ein Fenster an, in das Sie Ihre JSON-Datei ziehen und ablegen können.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Wenn Sie keine JSON-Datei zum Hochladen haben, wählen Sie **[!UICONTROL Adobe-GDPR-Request.json herunterladen]** , um eine Vorlage herunterzuladen, die Sie entsprechend den Werten, die Sie von den betroffenen Personen gesammelt haben, ausfüllen können.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Suchen Sie die JSON-Datei auf Ihrem Computer und ziehen Sie sie in das Dialogfenster. Wenn der Upload erfolgreich war, wird der Dateiname im Dialogfeld angezeigt. Sie können weitere JSON-Dateien nach Bedarf hinzufügen, indem Sie sie in das Dialogfeld ziehen und dort ablegen.

Klicken Sie abschließend auf **[!UICONTROL Erstellen]**. Der Dialog verschwindet und der neue Auftrag (oder die neuen Aufträge) werden zusammen mit dem aktuellen Verarbeitungsstatus im Widget &quot;Auftragsersuchen&quot;aufgeführt.

### Nächste Schritte

Durch das Lesen dieses Dokuments haben Sie gelernt, wie Sie [!DNL Privacy Service] Benutzeroberfläche zum Erstellen eines Datenschutzauftrags, zur Ansicht der Auftragsdetails und zur Überwachung des Verarbeitungsstatus sowie zum Herunterladen der Ergebnisse nach Abschluss des Auftrags.

Schritte zum programmgesteuerten Ausführen dieser Operationen mit [!DNL Privacy Service] API, siehe [API-Handbuch](../api/overview.md).
