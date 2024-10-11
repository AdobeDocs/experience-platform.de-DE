---
keywords: Experience Platform;home;popular topics;export;export
solution: Experience Platform
title: Verwalten von Datenschutzaufträgen in der Privacy Service-Benutzeroberfläche
description: Erfahren Sie, wie Sie mit der Privacy Service-Benutzeroberfläche Datenschutzanfragen in verschiedenen Experience Cloud-Applikationen koordinieren und überwachen können.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: 25c173e22f2aa4922aed89f7c9721e2303d5d4b9
workflow-type: tm+mt
source-wordcount: '1765'
ht-degree: 19%

---

# Verwalten von Datenschutzaufträgen in der Privacy Service-Benutzeroberfläche {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="Berücksichtigen von Datenschutzanträgen betroffener Personen"
>abstract="<h2>Beschreibung</h2><p>Mit Adobe Experience Platform Privacy Service können Sie Datenschutzanfragen für Kundinnen und Kunden erstellen und verwalten, die ihre personenbezogenen Daten gemäß den gesetzlichen Datenschutzbestimmungen aufrufen oder löschen möchten.</p>"

In diesem Dokument werden Schritte zum Erstellen und Verwalten von Datenschutzanfragen mithilfe der Benutzeroberfläche von [!DNL Privacy Service] beschrieben.

>[!IMPORTANT]
>
>Privacy Service ist nur für Anfragen der betroffenen Person und für Verbraucherrechtsanfragen vorgesehen. Jegliche andere Verwendung von Privacy Service für die Datenbereinigung oder -wartung wird nicht unterstützt und ist nicht zulässig. Adobe ist gesetzlich verpflichtet, diese rechtzeitig zu erfüllen. Daher sind Lasttests auf Privacy Service nicht zulässig, da es sich um eine reine Produktionsumgebung handelt und ein unnötiger Rückstand gültiger Datenschutzanfragen erzeugt wird.
>
>Es gibt jetzt eine feste tägliche Upload-Grenze, um einen Missbrauch des Dienstes zu verhindern. Für Benutzende, bei denen ein Missbrauch des Systems festgestellt wurde, wird der Zugriff auf den Dienst deaktiviert. Anschließend wird mit ihnen ein Meeting abgehalten, bei dem ihr Handeln und die akzeptable Verwendung von Privacy Service erörtert wird.

## Durchsuchen des Dashboards für die Benutzeroberfläche von [!DNL Privacy Service]

Das Dashboard für die Benutzeroberfläche [!DNL Privacy Service] enthält zwei Widgets, mit denen Sie den Status Ihrer Datenschutzaufträge anzeigen können: &quot;[!UICONTROL Statusbericht]&quot;und &quot;[!UICONTROL Auftragsanfragen]&quot;. Im Dashboard wird auch die aktuell ausgewählte Regel für die angezeigten Aufträge angezeigt.

![UI-Dashboard](../images/user-guide/dashboard.png)

### Typ der Regelung

[!DNL Privacy Service] unterstützt Auftragsanfragen für verschiedene Datenschutzbestimmungen. In der folgenden Tabelle sind die unterstützten Verordnungen und die entsprechende Beschriftung in der Benutzeroberfläche aufgeführt:

| UI-Bezeichnung | Regelung |
|-------------------------------------|------------------------|
| [!UICONTROL APA_AUS (Australien)] | Der [!DNL Australia Privacy Act] |
| [!UICONTROL CCPA (Kalifornien)] | Der [!DNL California Consumer Privacy Act] |
| [!UICONTROL CPA_USA (Colorado)] | Der [!DNL Colorado Privacy Act] |
| [!UICONTROL CPRA_USA (Kalifornien)] | Der [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL CTDPA_USA (Connecticut)] | Der [!DNL Connecticut Data Privacy Act] |
| [!UICONTROL FDBR_USA (Florida)] | Der [!DNL Florida Digital Bill of Rights] |
| [!UICONTROL DSGVO (Europäische Union)] | Die [!DNL General Data Protection Regulation] der Europäischen Union |
| [!UICONTROL HIPPA_USA (Vereinigte Staaten)] | Der [!DNL Health Insurance Portability and Accountability Act] |
| [!UICONTROL ICDPA_USA] (Iowa) | Der [!DNL Iowa Consumer Data Protection Act] |
| [!UICONTROL LGPD_BRA (Brasilien)] | Brasiliens &quot;[!DNL General Data Protection Law]&quot; [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL MHMDA_USA (Washington)] | Der [!DNL Washington My Health My Data Act] |
| [!UICONTROL MCDPA_USA (Montana)] | Der [!DNL Montana Consumer Data Privacy Act] |
| [!UICONTROL NDPA_USA (Nebraska)] | Der [!DNL Nebraska Data Protection Act] |
| [!UICONTROL NZPA_NZL (Neuseeland)] | Neuseelands [!DNL Privacy Act] |
| [!UICONTROL NHPA_USA (New Hampshire)] | Der [!DNL New Hampshire Data Privacy Act] |
| [!UICONTROL NJDPA_USA (New Jersey)] | Der [!DNL New Jersey Data Protection Act] |
| [!UICONTROL OCPA USA (Oregon)] | Der [!DNL Oregon Consumer Privacy Act] |
| [!UICONTROL PDPA_THA (Thailand)] | Thailands [!DNL Personal Data Protection Act] |
| [!UICONTROL TDPSA USA (Texas)] | Der [!DNL Texas Data Privacy and Security Act] |
| [!UICONTROL UCPA_USA (Utah)] | Der [!DNL Utah Consumer Privacy Act] |
| [!UICONTROL VCDPA_USA (Virginia)] | Der [!DNL Virginia Consumer Data Protection Act] |

{style="table-layout:auto"}

<!-- 
Waiting:
| **[!UICONTROL PIPA_KOR]**  ?        | South Korea [!DNL Personal Information Privacy Act] |
 -->

>[!NOTE]
>
>Weitere Informationen zum rechtlichen Kontext der einzelnen Verordnungen finden Sie in der Übersicht zu [unterstützten Datenschutzbestimmungen](../regulations/overview.md) .

Aufträge für jeden Regulierungstyp werden separat nachverfolgt. Um zwischen Regeltypen zu wechseln, wählen Sie das Dropdown-Menü **[!UICONTROL Regulierungstyp]** aus und wählen Sie die gewünschte Vorschrift aus der Liste aus.

![Die Privacy Service-Konsole mit dem Dropdown-Menü &quot;Regulierungstyp&quot;](../images/user-guide/regulation.png).

Nach Änderung des Regulierungstyps wird das Dashboard aktualisiert, um alle Vorgänge, Filter, Widgets und Dialogfelder zur Schaffung von Arbeitsplätzen anzuzeigen, die für die ausgewählte Verordnung gelten.

![Aktualisiertes Dashboard](../images/user-guide/dashboard-update.png)

### Statusbericht

Das Diagramm auf der linken Seite des Widgets &quot;Statusbericht&quot;verfolgt gesendete Aufträge für alle Aufträge, die möglicherweise mit Fehlern gemeldet wurden. Das Diagramm auf der rechten Seite verfolgt Aufträge, die sich dem Ende des 30-Tage-Compliance-Fensters nähern.

Wählen Sie eine der beiden Umschalter-Schaltflächen über dem Diagramm aus, um die entsprechenden Metriken ein- oder auszublenden.

![](../images/user-guide/hide-errors.png)

Sie können die genaue Anzahl der Aufträge anzeigen, die mit einem Datenpunkt in den Diagrammen verbunden sind, indem Sie den Mauszeiger über den betreffenden Datenpunkt bewegen.

![Mauszeiger-Datenpunkte](../images/user-guide/mouse-over.png)

Um weitere Details zu einem bestimmten Datenpunkt anzuzeigen, wählen Sie den betreffenden Datenpunkt aus, um die zugehörigen Aufträge im Widget Auftragsanfragen anzuzeigen. Beachten Sie den Filter, der direkt über der Auftragsliste angewendet wird.

![Angewendeter Filter aus Widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Wenn ein Filter auf das Widget Auftragsanforderungen angewendet wurde, können Sie den Filter entfernen, indem Sie in der Filtertablette die Option **X** auswählen. Auftragsanfragen kehren dann zur standardmäßigen Tracking-Liste zurück.

### Auftragsanfragen {#job-requests}

Der Arbeitsbereich [!UICONTROL Auftragsanfragen] listet Details zu den letzten Auftragsanfragen in Ihrem Unternehmen auf. Zu den Details gehören der Anfragetyp, der aktuelle Status, das Fälligkeitsdatum, die E-Mail-Adresse des Anfragenden usw. Es werden jeweils 100 Datensätze geladen. Standardmäßig werden die zuletzt erstellten Aufträge oben angezeigt, wobei während des Bildlaufs nach unten weitere Datensätze geladen werden.

>[!NOTE]
>
>Auf die Daten für zuvor erstellte Aufträge kann erst 30 Tage nach dem Abschlussdatum zugegriffen werden.

Sie können die Liste filtern, indem Sie Suchbegriffe in die Suchleiste unter dem Titel [!UICONTROL Auftragsanfragen] eingeben. Die Liste filtert automatisch bei der Eingabe und zeigt Anforderungen an, die Werte enthalten, die Ihren Suchbegriffen entsprechen. Das Suchfeld führt eine &quot;schnelle&quot;Suche durch, die Datenschutzauftrags-IDs mit den aktuell gerenderten/geladenen Aufträgen in der Benutzeroberfläche abgleicht. Es handelt sich nicht um eine umfassende Suche aller von Ihnen eingereichten Aufträge. Vielmehr handelt es sich um einen Filter, der auf die geladenen Ergebnisse angewendet wird. Verwenden Sie die Privacy Service-API, um [Aufträge basierend auf einer bestimmten Vorschrift, Datumsbereichen oder einem einzelnen Auftrag zurückzugeben](../api/privacy-jobs.md#list).

>[!TIP]
>
>Um Datensätze aus den letzten 30 Tagen in die Benutzeroberfläche zu laden, müssen Sie einen Bildlauf in der Tabelle durchführen und weitere Datensatzstapel laden.

![Der Abschnitt zur Datenschutzkonsole-Auftragsanfrage mit hervorgehobenem Suchfeld.](../images/user-guide/job-search.png)

Verwenden Sie alternativ die Suchschaltfläche , um eine Datenschutzauftragsabfrage durchzuführen, die einen bestimmten Datumsbereich umfasst. Diese Aktion gibt alle Datenschutzaufträge zurück, die von Ihrer Organisation während des angegebenen Zeitraums gesendet wurden. Wählen Sie das Dropdown-Menü **[!UICONTROL Angefordert am]** aus, um ein Start- und Enddatum für die Abfrage auszuwählen. Zu den verfügbaren Optionen gehören [!UICONTROL Today], [!UICONTROL Last 7 Days], [!UICONTROL Last 2 Weeks], [!UICONTROL Last 30 Days] oder [!UICONTROL Custom]. Bei Verwendung mit der Option [!UICONTROL Angefordert am] zeigt die Suchfunktion nur Auftragsanfragen an, die zwischen Ihren ausgewählten Datumsbereichen gesendet wurden.

![Der Abschnitt &quot;Auftragsanfrage&quot;mit dem Suchfeld, dem Dropdown-Menü &quot;Anforderung&quot;und der Suchschaltfläche ist hervorgehoben.](../images/user-guide/requested-on-dropdown-menu.png)

Um die Details einer bestimmten Auftragsanfrage anzuzeigen, wählen Sie die Auftrags-ID der Anfrage aus der Liste aus, um die Seite **[!UICONTROL Auftragsdetails]** zu öffnen.

![DSGVO-UI-Auftragsdetails](../images/user-guide/job-details.png)

Dieses Dialogfeld enthält Statusinformationen zu den einzelnen [!DNL Experience Cloud] -Lösungen und deren aktueller Status in Bezug auf den Gesamtauftrag. Da jeder Datenschutzauftrag asynchron ausgeführt wird, zeigt die Seite das aktuelle Kommunikationsdatum und die aktuelle Uhrzeit (GMT) jeder Lösung an, da einige für die Verarbeitung der Anfrage mehr Zeit als andere benötigen.

Wenn eine Lösung zusätzliche Daten bereitgestellt hat, ist dies in diesem Dialogfeld sichtbar. Sie können diese Daten durch Auswahl einzelner Produktzeilen anzeigen.

Um die vollständigen Auftragsdaten als CSV-Datei herunterzuladen, wählen Sie oben rechts im Dialogfeld **[!UICONTROL In CSV exportieren]** aus.

## Erstellen einer neuen Anfrage für einen Datenschutzauftrag {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="Anweisungen"
>abstract="<ul><li>Wählen Sie <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=de#logging-in-from-experience-platform">Anfragen</a> in der linken Navigation aus, um die Datenschutz-URL zu öffnen, und wählen Sie dann <b>Anfrage erstellen</b> aus.</li><li>Von hier aus können Sie entweder den Anfrage-Builder verwenden oder eine JSON-Datei mit betroffenen Personen hochladen.</li><li>Wenn Sie den Anfrage-Builder verwenden, wählen Sie den Auftragstyp (Zugriff und/oder Löschen) aus und wählen Sie dann den Typ der von Ihnen bereitgestellten Identität (E-Mail, ECID oder AAID) aus oder geben Sie einen benutzerdefinierten Identity-Namespace ein. Geben Sie die entsprechenden Identitätswerte für die Kundinnen bzw. Kunden ein und klicken Sie auf <b>Erstellen</b>, wenn Sie fertig sind.</li><li>Wählen Sie beim Hochladen einer JSON-Datei den Pfeil neben „Anfrage erstellen“ aus. Wählen Sie aus der Liste der Optionen <b>JSON hochladen</b> aus und laden Sie Ihre Datei hoch. Wenn Sie keine JSON-Datei zum Hochladen haben, wählen Sie <b>Adobe-GDPR-Request.json herunterladen</b> aus, um eine Vorlage herunterzuladen, die Sie ausfüllen können. Laden Sie die JSON-Datei hoch und klicken Sie auf <b>Erstellen</b>, wenn Sie fertig sind.</li><li>Weitere Informationen zu dieser Funktion finden Sie im <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html?lang=de">Benutzerhandbuch zum Privacy Service</a> auf Experience League.</li></ul>"

>[!NOTE]
>
>Um eine Datenschutzanfrage zu erstellen, müssen Sie Identitätsinformationen für die spezifischen Kunden bereitstellen, deren Daten aufgerufen oder gelöscht werden sollen. Lesen Sie das Dokument zu [Identitätsdaten für Datenschutzanfragen](../identity-data.md) , bevor Sie mit diesem Abschnitt fortfahren.

Die Benutzeroberfläche [!DNL Privacy Service] bietet zwei Methoden zum Erstellen neuer Auftragsanfragen:

* [Verwenden des Anforderungs-Builders](#request-builder)
* [Hochladen einer JSON-Datei](#json)

Die Schritte zur Verwendung dieser Methoden finden Sie in den folgenden Abschnitten.

### Verwenden des Anforderungs-Builders {#request-builder}

Mit dem Request Builder können Sie in der Benutzeroberfläche manuell eine neue Datenschutzauftragsanforderung erstellen. Der Request Builder eignet sich am besten für einfachere und kleinere Anforderungsgruppen, da der Request Builder die Anforderungen so beschränkt, dass sie nur einen ID-Typ pro Benutzer haben. Bei komplexeren Anforderungen ist es möglicherweise besser, stattdessen [eine JSON-Datei](#json) hochzuladen.

Um mit der Verwendung des Anforderungs-Builders zu beginnen, wählen Sie auf der rechten Seite des Bildschirms unter dem Widget Statusbericht die Option **[!UICONTROL Anforderung erstellen]** aus.

![Wählen Sie Anforderung erstellen](../images/user-guide/create-request.png) aus.

Das Dialogfeld **[!UICONTROL Anfrage erstellen]** wird geöffnet und enthält die verfügbaren Optionen zum Senden einer Datenschutzauftragsanforderung für den aktuell ausgewählten Regulierungstyp.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Wählen Sie den **[!UICONTROL Auftragstyp]** der Anforderung (&quot;Löschen&quot;oder &quot;Zugriff&quot;) und ein oder mehrere verfügbare Produkte aus der Liste aus.

Privacy Service unterstützt zwei Arten von Auftragsanfragen für personenbezogene Daten: [!UICONTROL Zugriff] (Lesen) und/oder [!UICONTROL Löschen]. Sie können entweder einen Antrag auf Erhalt aller Informationen stellen, die im Produkt gespeichert sind, das sich auf den Gegenstand der Anfrage bezieht, oder die Löschung aller Informationen beantragen, die sich auf den Gegenstand der Anfrage beziehen.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

Wählen Sie unter **[!UICONTROL Namespace type]** den entsprechenden Namespace-Typ für die Kunden-IDs aus, die an [!DNL Privacy Service] gesendet werden.

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Wählen Sie bei Verwendung des Standard-Namespace-Typs einen Namespace aus dem Dropdown-Menü (E-Mail, ECID oder AAID) aus, geben Sie dann die ID-Werte in das Textfeld rechts ein und drücken Sie für jede ID **\&lt;enter>** , um sie der Liste hinzuzufügen.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Bei Verwendung des benutzerdefinierten Namespace-Typs müssen Sie den Namespace manuell eingeben, bevor Sie die unten stehenden ID-Werte angeben.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Klicken Sie abschließend auf **[!UICONTROL Erstellen]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

Das Dialogfeld wird ausgeblendet und der neue Auftrag (oder die neuen Aufträge) wird im Widget Auftragsanfragen zusammen mit dem aktuellen Verarbeitungsstatus aufgeführt.

### Hochladen einer JSON-Datei {#json}

Beim Erstellen komplexerer Anforderungen, z. B. Anforderungen, die mehrere ID-Typen für jedes verarbeitete Datensubjekt verwenden, können Sie eine Anforderung erstellen, indem Sie eine JSON-Datei hochladen.

Wählen Sie den Pfeil neben **[!UICONTROL Anforderung erstellen]** unter dem Widget Statusbericht auf der rechten Seite des Bildschirms aus. Wählen Sie in der angezeigten Optionsliste **[!UICONTROL JSON hochladen]** aus.

![Erstellungsoptionen für Anfragen](../images/user-guide/create-options.png)

Das Dialogfeld &quot;**[!UICONTROL JSON hochladen]**&quot;wird angezeigt und bietet ein Fenster, in das Sie Ihre JSON-Datei per Drag-and-Drop ziehen können.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Wenn Sie keine JSON-Datei hochladen möchten, wählen Sie **[!UICONTROL Adobe-DSGVO-Request.json herunterladen]** aus, um eine Vorlage herunterzuladen, die Sie entsprechend den von Ihren Datensubjekten erfassten Werten füllen können.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Suchen Sie die JSON-Datei auf Ihrem Computer und ziehen Sie sie in das Dialogfenster. Wenn der Upload erfolgreich war, wird der Dateiname im Dialogfeld angezeigt. Sie können bei Bedarf weitere JSON-Dateien hinzufügen, indem Sie sie per Drag-and-Drop in das Dialogfeld ziehen.

Wählen Sie abschließend **[!UICONTROL Erstellen]** aus. Das Dialogfeld wird ausgeblendet und der neue Auftrag (oder die neuen Aufträge) wird im Widget Auftragsanfragen zusammen mit dem aktuellen Verarbeitungsstatus aufgeführt.

### Nächste Schritte

Durch Lesen dieses Dokuments haben Sie gelernt, wie Sie mit der Benutzeroberfläche von [!DNL Privacy Service] einen Datenschutzauftrag erstellen, die Details eines Auftrags anzeigen, seinen Verarbeitungsstatus überwachen und die Ergebnisse nach Abschluss herunterladen können.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe der [!DNL Privacy Service] -API finden Sie im [API-Handbuch](../api/overview.md).
