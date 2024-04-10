---
keywords: Experience Platform;Startseite;beliebte Themen;Export;Export
solution: Experience Platform
title: Verwalten von Datenschutzaufträgen in der Privacy Service-Benutzeroberfläche
description: Erfahren Sie, wie Sie die Privacy Service-Benutzeroberfläche verwenden, um Datenschutzanfragen in verschiedenen Experience Cloud-Anwendungen zu koordinieren und zu überwachen.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: 8ba06a5d572310e2822a5b3c9f82ff0721540f69
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 19%

---

# Verwalten von Datenschutzaufträgen in der Privacy Service-Benutzeroberfläche {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="Berücksichtigen von Datenschutzanträgen betroffener Personen"
>abstract="<h2>Beschreibung</h2><p>Mit Adobe Experience Platform Privacy Service können Sie Datenschutzanfragen für Kundinnen und Kunden erstellen und verwalten, die ihre personenbezogenen Daten gemäß den gesetzlichen Datenschutzbestimmungen aufrufen oder löschen möchten.</p>"

In diesem Dokument werden die Schritte zum Erstellen und Verwalten von Datenschutzanfragen mithilfe der [!DNL Privacy Service] -Benutzeroberfläche.

>[!IMPORTANT]
>
>Privacy Service ist nur für Anfragen der betroffenen Person und für Verbraucherrechtsanfragen vorgesehen. Jegliche andere Verwendung von Privacy Service für die Datenbereinigung oder -wartung wird nicht unterstützt und ist nicht zulässig. Adobe ist gesetzlich verpflichtet, diese rechtzeitig zu erfüllen. Daher sind Lasttests auf Privacy Service nicht zulässig, da es sich um eine reine Produktionsumgebung handelt und ein unnötiger Rückstand gültiger Datenschutzanfragen erzeugt wird.
>
>Es gibt jetzt eine feste tägliche Upload-Grenze, um einen Missbrauch des Dienstes zu verhindern. Für Benutzende, bei denen ein Missbrauch des Systems festgestellt wurde, wird der Zugriff auf den Dienst deaktiviert. Anschließend wird mit ihnen ein Meeting abgehalten, bei dem ihr Handeln und die akzeptable Verwendung von Privacy Service erörtert wird.

## Durchsuchen Sie die [!DNL Privacy Service] UI-Dashboard

Das Dashboard für die [!DNL Privacy Service] Die -Benutzeroberfläche bietet zwei Widgets, mit denen Sie den Status Ihrer Datenschutzaufträge anzeigen können: &quot;[!UICONTROL Statusbericht]&quot; und &quot;[!UICONTROL Vorgangsanfragen]„. Das Dashboard zeigt auch die aktuell ausgewählte Verordnung für die angezeigten Aufträge an.

![UI-Dashboard](../images/user-guide/dashboard.png)

### Regelungstyp

[!DNL Privacy Service] unterstützt Vorgangsanfragen für mehrere Datenschutzbestimmungen. In der folgenden Tabelle sind die unterstützten Verordnungen und die entsprechende Beschriftung aufgeführt, wie sie in der Benutzeroberfläche dargestellt werden:

| UI-Bezeichnung | Verordnung |
| --- | --- |
| [!UICONTROL APA_AUS] | Die [!DNL Australia Privacy Act (Privacy Act)] |
| [!UICONTROL CPA] | Die [!DNL Colorado Privacy Act] |
| [!UICONTROL CCPA] | Die [!DNL California Consumer Privacy Act] |
| [!UICONTROL CPRA_USA] | Die [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL CTDPA] | Die [!DNL Connecticut Data Privacy Act] |
| [!UICONTROL DSGVO] | Die Europäische Union [!DNL General Data Protection Regulation] |
| [!UICONTROL HIPAA_AUS] | Die [!DNL Health Insurance Portability and Accountability Act] |
| [!UICONTROL LGPD_BRA] | Brasiliens [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL MHMDA] | Die [!DNL Washington My Health My Data Act] |
| [!UICONTROL NZPA_NZL] | Neuseeland [!DNL Privacy Act] |
| [!UICONTROL PDPA_THA] | Thailands [!DNL Personal Data Protection Act] |
| [!UICONTROL UCPA] | Die [!DNL Utah Consumer Privacy Act] |
| [!UICONTROL VCDPA_USA] | Die [!DNL Virginia Consumer Data Protection Act] |

{style="table-layout:auto"}

<!--Not released yet:
| [!UICONTROL PDPA_VNM] | Vietnam's [!DNL Personal Data Protection Decree] |
 -->

>[!NOTE]
>
>Siehe die Übersicht zu [Unterstützte Datenschutzbestimmungen](../regulations/overview.md) Weitere Informationen zum rechtlichen Kontext jeder Verordnung.

Vorgänge für jeden Regulierungstyp werden separat verfolgt. Um zwischen Regulierungstypen zu wechseln, wählen Sie die **[!UICONTROL Regelungstyp]** Dropdown-Menü auswählen und die gewünschte Regelung aus der Liste auswählen.

![Die Privacy Service-Konsole mit der Dropdown-Liste „Regulierungstyp„.](../images/user-guide/regulation.png)

Nach Änderung des Regulierungstyps wird das Dashboard aktualisiert und zeigt alle Vorgänge, Filter, Widgets und Dialogfelder für die Erstellung von Aufträgen an, die für die ausgewählte Verordnung gelten.

![Aktualisiertes Dashboard](../images/user-guide/dashboard-update.png)

### Statusbericht

Das Diagramm auf der linken Seite des Widgets Statusbericht verfolgt gesendete Aufträge im Vergleich zu allen Aufträgen, die möglicherweise mit Fehlern zurückgemeldet wurden. Das Diagramm auf der rechten Seite verfolgt Aufträge, die sich dem Ende des 30-tägigen Compliance-Fensters nähern.

Wählen Sie eine der beiden Umschalter-Schaltflächen über dem Diagramm aus, um die jeweiligen Metriken ein- oder auszublenden.

![](../images/user-guide/hide-errors.png)

Sie können die genaue Anzahl der Aufträge anzeigen, die mit einem Datenpunkt in den Diagrammen verknüpft sind, indem Sie die Maus über den betreffenden Datenpunkt bewegen.

![Mouse-over-Datenpunkte](../images/user-guide/mouse-over.png)

Um weitere Details zu einem bestimmten Datenpunkt anzuzeigen, wählen Sie den betreffenden Datenpunkt aus, um die zugehörigen Aufträge im Widget Auftragsanfragen anzuzeigen. Notieren Sie sich den Filter, der direkt über der Auftragsliste angewendet wird.

![Angewendeter Filter aus Widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Wenn ein Filter auf das Widget Auftragsanfragen angewendet wurde, können Sie den Filter entfernen, indem Sie die Variable auswählen. **X** Auf der Filterpille. Auftragsanfragen kehren dann zur Standard-Tracking-Liste zurück.

### Vorgangsanfragen {#job-requests}

Die [!UICONTROL Vorgangsanfragen] Workspace listet Details zu den letzten Auftragsanfragen in Ihrer Organisation auf. Zu den Details gehören der Anfragetyp, der aktuelle Status, das Fälligkeitsdatum, die Anforderer-E-Mail usw. Es werden jeweils 100 Datensätze geladen. Standardmäßig werden die zuletzt erstellten Aufträge oben angezeigt, wobei beim Scrollen zum Durchsuchen mehr Datensätze geladen werden.

>[!NOTE]
>
>Die Daten für zuvor erstellte Aufträge sind nur 30 Tage nach dem Abschlussdatum zugänglich.

Sie können die Liste filtern, indem Sie Keywords in die Suchleiste unter dem Feld eingeben [!UICONTROL Vorgangsanfragen] Titel. Die Liste wird während der Eingabe automatisch gefiltert und zeigt Anfragen an, die Werte enthalten, die Ihren Suchbegriffen entsprechen. Das Suchfeld führt eine „Schnellsuche“ durch, die die Datenschutzauftrags-IDs mit den aktuell gerenderten/geladenen Aufträgen in der Benutzeroberfläche abgleicht. Es handelt sich nicht um eine umfassende Suche aller eingereichten Aufträge. Stattdessen handelt es sich um einen Filter, der auf die geladenen Ergebnisse angewendet wird. Verwenden der Privacy Service-API für Folgendes [Rückgabe von Aufträgen basierend auf einer bestimmten Verordnung, Datumsbereichen oder einem einzelnen Auftrag](../api/privacy-jobs.md#list).

>[!TIP]
>
>Um Datensätze aus den letzten 30 Tagen in die Benutzeroberfläche zu laden, müssen Sie die Tabelle nach unten scrollen und weitere Datensatz-Batches laden.

![Der Abschnitt „Auftragsanfrage“ der Privacy Console mit hervorgehobenem Suchfeld.](../images/user-guide/job-search.png)

Alternativ können Sie die Suchschaltfläche verwenden, um eine Datenschutzabfrage durchzuführen, die sich über einen bestimmten Datumsbereich erstreckt. Diese Aktion gibt alle Datenschutzaufträge zurück, die von Ihrer Organisation im angegebenen Zeitraum gesendet wurden. Wählen Sie die **[!UICONTROL Angefordert am]** Dropdown-Menü, um ein Start- und Enddatum für die Abfrage auszuwählen. Zu den verfügbaren Optionen gehören [!UICONTROL Heute], [!UICONTROL Letzte 7 Tage], [!UICONTROL Letzte 2 Wochen], [!UICONTROL Letzte 30 Tage], oder [!UICONTROL Benutzerdefiniert]. Bei Verwendung mit dem [!UICONTROL Angefordert am] die Suchfunktion nur Auftragsanfragen anzeigt, die zwischen den von Ihnen ausgewählten Datumsbereichen gesendet wurden.

![Der Abschnitt „Vorgangsanfrage“ mit dem Suchfeld, dem Dropdown-Menü „Angefordert“ und der hervorgehobenen Suchschaltfläche.](../images/user-guide/requested-on-dropdown-menu.png)

Um die Details einer bestimmten Vorgangsanfrage anzuzeigen, wählen Sie die Vorgangskennung der Anfrage aus der Liste aus, um die Anfrage zu öffnen **[!UICONTROL Vorgangsdetails]** Seite.

![DSGVO-UI-Auftragsdetails](../images/user-guide/job-details.png)

Dieses Dialogfeld enthält Statusinformationen zu jedem [!DNL Experience Cloud] Lösung und ihr aktueller Status in Bezug auf den Gesamtauftrag. Da jeder Datenschutzauftrag asynchron ist, zeigt die Seite das Datum und die Uhrzeit der letzten Kommunikation (GMT) aus jeder Lösung an, da einige mehr Zeit benötigen als andere, um die Anfrage zu verarbeiten.

Wenn eine Lösung zusätzliche Daten bereitgestellt hat, können diese in diesem Dialogfeld angezeigt werden. Sie können diese Daten anzeigen, indem Sie einzelne Produktzeilen auswählen.

Um die vollständigen Auftragsdaten als CSV-Datei herunterzuladen, wählen Sie **[!UICONTROL In CSV exportieren]** Oben rechts im Dialogfeld.

## Erstellen einer neuen Anfrage für einen Datenschutzauftrag {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="Anweisungen"
>abstract="<ul><li>Wählen Sie <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=de#logging-in-from-experience-platform">Anfragen</a> in der linken Navigation aus, um die Datenschutz-URL zu öffnen, und wählen Sie dann <b>Anfrage erstellen</b> aus.</li><li>Von hier aus können Sie entweder den Anfrage-Builder verwenden oder eine JSON-Datei mit betroffenen Personen hochladen.</li><li>Wenn Sie den Anfrage-Builder verwenden, wählen Sie den Auftragstyp (Zugriff und/oder Löschen) aus und wählen Sie dann den Typ der von Ihnen bereitgestellten Identität (E-Mail, ECID oder AAID) aus oder geben Sie einen benutzerdefinierten Identity-Namespace ein. Geben Sie die entsprechenden Identitätswerte für die Kundinnen bzw. Kunden ein und klicken Sie auf <b>Erstellen</b>, wenn Sie fertig sind.</li><li>Wählen Sie beim Hochladen einer JSON-Datei den Pfeil neben „Anfrage erstellen“ aus. Wählen Sie aus der Liste der Optionen <b>JSON hochladen</b> aus und laden Sie Ihre Datei hoch. Wenn Sie keine JSON-Datei zum Hochladen haben, wählen Sie <b>Adobe-GDPR-Request.json herunterladen</b> aus, um eine Vorlage herunterzuladen, die Sie ausfüllen können. Laden Sie die JSON-Datei hoch und klicken Sie auf <b>Erstellen</b>, wenn Sie fertig sind.</li><li>Weitere Informationen zu dieser Funktion finden Sie im <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html?lang=de">Benutzerhandbuch zum Privacy Service</a> auf Experience League.</li></ul>"

>[!NOTE]
>
>Um eine Datenschutzanfrage zu erstellen, müssen Sie Identitätsinformationen für die spezifischen Kundinnen und Kunden angeben, auf deren Daten zugegriffen werden soll oder die gelöscht werden sollen. Lesen Sie das Dokument zu [Identitätsdaten für Datenschutzanfragen](../identity-data.md) Bevor Sie mit diesem Abschnitt fortfahren.

Die [!DNL Privacy Service] Die -Benutzeroberfläche bietet zwei Methoden zum Erstellen neuer Auftragsanfragen:

* [Verwenden des Request Builders](#request-builder)
* [Hochladen einer JSON-Datei](#json)

Die Schritte zur Verwendung jeder dieser Methoden werden in den folgenden Abschnitten beschrieben.

### Verwenden des Request Builders {#request-builder}

Mit dem Anfrage-Builder können Sie in der -Benutzeroberfläche manuell eine neue Datenschutzanfrage erstellen. Der Request Builder eignet sich am besten für einfachere und kleinere Anfragesätze, da der Request Builder Anfragen so einschränkt, dass sie nur einen ID-Typ pro Benutzer haben. Bei komplizierteren Anfragen ist es möglicherweise besser, [Hochladen einer JSON-Datei](#json) Stattdessen.

Um den Request Builder zu verwenden, wählen Sie aus. **[!UICONTROL Anfrage erstellen]** unter dem Widget Statusbericht auf der rechten Bildschirmseite.

![Anfrage erstellen auswählen](../images/user-guide/create-request.png)

Die **[!UICONTROL Anfrage erstellen]** Das Dialogfeld wird geöffnet und zeigt die verfügbaren Optionen zum Senden einer Datenschutzanfrage für den derzeit ausgewählten Regulierungstyp an.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Wählen Sie die **[!UICONTROL Vorgangstyp]** der Anfrage („Löschen“ oder „Zugriff„) und eines oder mehrerer verfügbarer Produkte aus der Liste.

Privacy Service unterstützt zwei Arten von Vorgangsanfragen für personenbezogene Daten: [!UICONTROL Zugriff] (Lesen) und/oder [!UICONTROL Löschen]. Sie können entweder anfordern, alle im Produkt gespeicherten Informationen zu erhalten, die sich auf den Gegenstand der Anfrage beziehen, oder anfordern, alle Informationen zu löschen, die sich auf den Gegenstand der Anfrage beziehen.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

Unter **[!UICONTROL Namespace-Typ]** Wählen Sie anschließend den entsprechenden Namespace-Typ für die Kunden-IDs aus, an die gesendet werden sollen [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Wenn Sie den standardmäßigen Namespace-Typ verwenden, wählen Sie einen Namespace aus dem Dropdown-Menü aus (E-Mail, ECID oder AAID) und geben Sie dann die ID-Werte in das Textfeld rechts ein, indem Sie drücken **\&lt;enter>** für jede ID, um sie der Liste hinzuzufügen.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Bei Verwendung des benutzerdefinierten Namespace-Typs müssen Sie den Namespace manuell eingeben, bevor Sie die unten stehenden ID-Werte angeben.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Klicken Sie abschließend auf **[!UICONTROL Erstellen]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

Das Dialogfeld wird ausgeblendet und der neue Auftrag (oder die Aufträge) werden im Widget Auftragsanfragen zusammen mit ihrem aktuellen Verarbeitungsstatus aufgeführt.

### Hochladen einer JSON-Datei {#json}

Bei der Erstellung komplexerer Anfragen, z. B. Anfragen, die mehrere ID-Typen für jede verarbeitete betroffene Person verwenden, können Sie eine Anfrage erstellen, indem Sie eine JSON-Datei hochladen.

Wählen Sie den Pfeil neben aus. **[!UICONTROL Anfrage erstellen]**, unterhalb des Widgets Statusbericht auf der rechten Seite des Bildschirms. Wählen Sie aus der angezeigten Liste der Optionen Folgendes aus **[!UICONTROL JSON hochladen]**.

![Optionen zur Anfrageerstellung](../images/user-guide/create-options.png)

Die **[!UICONTROL JSON hochladen]** wird angezeigt und bietet ein Fenster, in das Sie Ihre JSON-Datei per Drag-and-Drop ziehen können.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Wenn Sie keine JSON-Datei zum Hochladen haben, wählen Sie **[!UICONTROL Adobe-GDPR-Request.json herunterladen]** So laden Sie eine Vorlage herunter, die Sie entsprechend den von Ihren betroffenen Personen erfassten Werten ausfüllen können.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Suchen Sie die JSON-Datei auf Ihrem Computer und ziehen Sie sie in das Dialogfenster. Wenn der Upload erfolgreich war, wird der Dateiname im Dialogfeld angezeigt. Sie können weitere JSON-Dateien nach Bedarf hinzufügen, indem Sie sie per Drag-and-Drop in das Dialogfeld ziehen.

Wenn Sie fertig sind, wählen Sie aus. **[!UICONTROL Erstellen]**. Das Dialogfeld wird ausgeblendet und der neue Auftrag (oder die Aufträge) werden im Widget Auftragsanfragen zusammen mit ihrem aktuellen Verarbeitungsstatus aufgeführt.

### Nächste Schritte

In diesem Dokument haben Sie gelernt, wie Sie die [!DNL Privacy Service] Benutzeroberfläche zum Erstellen eines Datenschutzauftrags, Anzeigen der Details eines Auftrags und Überwachen seines Verarbeitungsstatus und Herunterladen der Ergebnisse nach Abschluss.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe der [!DNL Privacy Service] -API, siehe [API-Handbuch](../api/overview.md).
