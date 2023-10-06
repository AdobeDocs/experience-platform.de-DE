---
keywords: Experience Platform;home;popular topics;export;export
solution: Experience Platform
title: Verwalten von Datenschutzaufträgen in der Privacy Service-Benutzeroberfläche
description: Erfahren Sie, wie Sie mit der Privacy Service-Benutzeroberfläche Datenschutzanfragen in verschiedenen Experience Cloud-Applikationen koordinieren und überwachen können.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: 9d05752f3db78d9d10fd91fd0d3fed924217199c
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 23%

---

# Verwalten von Datenschutzaufträgen in der Privacy Service-Benutzeroberfläche {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="Berücksichtigen von Datenschutzanträgen betroffener Personen"
>abstract="<h2>Beschreibung</h2><p>Mit Adobe Experience Platform Privacy Service können Sie Datenschutzanfragen für Kundinnen und Kunden erstellen und verwalten, die ihre personenbezogenen Daten gemäß den gesetzlichen Datenschutzbestimmungen aufrufen oder löschen möchten.</p>"

In diesem Dokument werden die Schritte zum Erstellen und Verwalten von Datenschutzanfragen mithilfe des [!DNL Privacy Service] -Benutzeroberfläche.

>[!IMPORTANT]
>
>Privacy Service ist nur für Anfragen der betroffenen Person und für Verbraucherrechtsanfragen vorgesehen. Jegliche andere Verwendung von Privacy Service für die Datenbereinigung oder -wartung wird nicht unterstützt und ist nicht zulässig. Adobe ist gesetzlich verpflichtet, diese rechtzeitig zu erfüllen. Daher sind Lasttests auf Privacy Service nicht zulässig, da es sich um eine reine Produktionsumgebung handelt und ein unnötiger Rückstau gültiger Datenschutzanfragen erzeugt wird.
>
>Es gibt jetzt eine feste tägliche Upload-Grenze, um einen Missbrauch des Dienstes zu verhindern. Für Benutzende, bei denen ein Missbrauch des Systems festgestellt wurde, wird der Zugriff auf den Dienst deaktiviert. Anschließend wird mit ihnen ein Meeting abgehalten, bei dem ihr Handeln und die akzeptable Verwendung von Privacy Service erörtert wird.

## Durchsuchen Sie die [!DNL Privacy Service] UI-Dashboard

Das Dashboard für die [!DNL Privacy Service] Die Benutzeroberfläche bietet zwei Widgets, mit denen Sie den Status Ihrer Datenschutzaufträge anzeigen können: &quot;[!UICONTROL Statusbericht]&quot; und &quot;[!UICONTROL Auftragsanforderungen]&quot;. Im Dashboard wird auch die aktuell ausgewählte Regel für die angezeigten Aufträge angezeigt.

![UI-Dashboard](../images/user-guide/dashboard.png)

### Regelungstyp

[!DNL Privacy Service] unterstützt Auftragsanfragen für verschiedene Datenschutzbestimmungen. In der folgenden Tabelle sind die unterstützten Verordnungen und die entsprechende Beschriftung in der Benutzeroberfläche aufgeführt:

| UI-Bezeichnung | Verordnung |
| --- | --- |
| [!UICONTROL APA_AUS] | Die Menüauswahlmöglichkeiten für die [!DNL Australia Privacy Act (Privacy Act)] |
| [!UICONTROL CPA] | Die Menüauswahlmöglichkeiten für die [!DNL Colorado Privacy Act] |
| [!UICONTROL CCPA] | Die Menüauswahlmöglichkeiten für die [!DNL California Consumer Privacy Act] |
| [!UICONTROL CPRA_USA] | Die Menüauswahlmöglichkeiten für die [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL CTDPA] | Die Menüauswahlmöglichkeiten für die [!DNL Connecticut Data Privacy Act] |
| [!UICONTROL DSGVO] | Die [!DNL General Data Protection Regulation] |
| [!UICONTROL HIPAA_AUS] | Die Menüauswahlmöglichkeiten für die [!DNL Health Insurance Portability and Accountability Act] |
| [!UICONTROL LGPD_BRA] | Brasiliens [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL NZPA_NZL] | Neuseeland [!DNL Privacy Act] |
| [!UICONTROL PDPA_THA] | Thailands [!DNL Personal Data Protection Act] |
| [!UICONTROL UCPA] | Die Menüauswahlmöglichkeiten für die [!DNL Utah Consumer Privacy Act] |
| [!UICONTROL VCDPA_USA] | Die Menüauswahlmöglichkeiten für die [!DNL Virginia Consumer Data Protection Act] |

{style="table-layout:auto"}

<!--Not released yet:
| [!UICONTROL PDPA_VNM] | Vietnam's [!DNL Personal Data Protection Decree] |
 -->

>[!NOTE]
>
>Siehe Übersicht unter [Unterstützte Datenschutzbestimmungen](../regulations/overview.md) für weitere Informationen über den rechtlichen Kontext der einzelnen Verordnungen.

Aufträge für jeden Regulierungstyp werden separat nachverfolgt. Um zwischen Regeltypen zu wechseln, wählen Sie die **[!UICONTROL Regelungstyp]** und wählen Sie die gewünschte Regel aus der Liste aus.

![Die Privacy Service-Konsole mit dem Dropdown-Menü &quot;Regulierungstyp&quot;.](../images/user-guide/regulation.png)

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
>Wenn ein Filter auf das Widget Auftragsanforderungen angewendet wurde, können Sie den Filter entfernen, indem Sie die **X** auf der Filtertablette. Auftragsanfragen kehren dann zur standardmäßigen Tracking-Liste zurück.

### Auftragsanforderungen

Das Widget Auftragsanfragen listet alle in Ihrem Unternehmen verfügbaren Auftragsanfragen auf, einschließlich Details zum Anfragetyp, aktuellen Status, Fälligkeitsdatum und E-Mail-Adresse des Anfragenden.

>[!NOTE]
>
>Auf die Daten für zuvor erstellte Aufträge kann erst 30 Tage nach dem Abschlussdatum zugegriffen werden.

Sie können die Liste filtern, indem Sie Suchbegriffe in die Suchleiste unter dem Titel Auftragsanfragen eingeben. Die Liste filtert automatisch bei der Eingabe und zeigt Anforderungen an, die Werte enthalten, die Ihren Suchbegriffen entsprechen. Sie können auch die **[!UICONTROL Beantragen am]** Dropdown-Menü, um einen Zeitraum für die aufgelisteten Aufträge auszuwählen.

![Suchoptionen für Auftragsanfragen](../images/user-guide/job-search.png)

Um die Details einer bestimmten Auftragsanfrage anzuzeigen, wählen Sie die Auftrags-ID der Anfrage aus der Liste aus, um die **[!UICONTROL Auftragsdetails]** Seite.

![DSGVO-UI-Auftragsdetails](../images/user-guide/job-details.png)

Dieses Dialogfeld enthält Statusinformationen zu jedem [!DNL Experience Cloud] Lösung und deren aktueller Status in Bezug auf den Gesamtauftrag. Da jeder Datenschutzauftrag asynchron ausgeführt wird, zeigt die Seite das aktuelle Kommunikationsdatum und die aktuelle Uhrzeit (GMT) jeder Lösung an, da einige für die Verarbeitung der Anfrage mehr Zeit als andere benötigen.

Wenn eine Lösung zusätzliche Daten bereitgestellt hat, ist dies in diesem Dialogfeld sichtbar. Sie können diese Daten durch Auswahl einzelner Produktzeilen anzeigen.

Um die vollständigen Auftragsdaten als CSV-Datei herunterzuladen, wählen Sie **[!UICONTROL Exportieren in CSV]** oben rechts im Dialogfeld.

## Neue Datenschutzauftragsanforderung erstellen {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="Anweisungen"
>abstract="<ul><li>Wählen Sie <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=de#logging-in-from-experience-platform">Anfragen</a> in der linken Navigation aus, um die Datenschutz-URL zu öffnen, und wählen Sie dann <b>Anfrage erstellen</b> aus.</li><li>Von hier aus können Sie entweder den Anfrage-Builder verwenden oder eine JSON-Datei mit betroffenen Personen hochladen.</li><li>Wenn Sie den Anfrage-Builder verwenden, wählen Sie den Auftragstyp (Zugriff und/oder Löschen) aus und wählen Sie dann den Typ der von Ihnen bereitgestellten Identität (E-Mail, ECID oder AAID) aus oder geben Sie einen benutzerdefinierten Identity-Namespace ein. Geben Sie die entsprechenden Identitätswerte für die Kundinnen bzw. Kunden ein und klicken Sie auf <b>Erstellen</b>, wenn Sie fertig sind.</li><li>Wählen Sie beim Hochladen einer JSON-Datei den Pfeil neben „Anfrage erstellen“ aus. Wählen Sie aus der Liste der Optionen <b>JSON hochladen</b> aus und laden Sie Ihre Datei hoch. Wenn Sie keine JSON-Datei zum Hochladen haben, wählen Sie <b>Adobe-GDPR-Request.json herunterladen</b> aus, um eine Vorlage herunterzuladen, die Sie ausfüllen können. Laden Sie die JSON-Datei hoch und klicken Sie auf <b>Erstellen</b>, wenn Sie fertig sind.</li><li>Weitere Informationen zu dieser Funktion finden Sie im <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html?lang=de">Benutzerhandbuch zum Privacy Service</a> auf Experience League.</li></ul>"

>[!NOTE]
>
>Um eine Datenschutzanfrage zu erstellen, müssen Sie Identitätsinformationen für die spezifischen Kunden bereitstellen, deren Daten aufgerufen oder gelöscht werden sollen. Lesen Sie das Dokument unter [Identitätsdaten für Datenschutzanfragen](../identity-data.md) bevor Sie mit diesem Abschnitt fortfahren.

Die [!DNL Privacy Service] Die Benutzeroberfläche bietet zwei Methoden zum Erstellen neuer Auftragsanfragen:

* [Verwenden des Anforderungs-Builders](#request-builder)
* [Hochladen einer JSON-Datei](#json)

Die Schritte zur Verwendung dieser Methoden finden Sie in den folgenden Abschnitten.

### Verwenden des Anforderungs-Builders {#request-builder}

Mit dem Request Builder können Sie in der Benutzeroberfläche manuell eine neue Datenschutzauftragsanforderung erstellen. Der Request Builder eignet sich am besten für einfachere und kleinere Anforderungsgruppen, da der Request Builder die Anforderungen so beschränkt, dass sie nur einen ID-Typ pro Benutzer haben. Bei komplexeren Anforderungen kann es besser sein, [JSON-Datei hochladen](#json) anstatt.

Um mit der Verwendung des Anforderungs-Builders zu beginnen, wählen Sie **[!UICONTROL Anforderung erstellen]** unter dem Widget Statusbericht auf der rechten Seite des Bildschirms.

![Anforderung erstellen](../images/user-guide/create-request.png)

Die **[!UICONTROL Anforderung erstellen]** wird geöffnet, in dem die verfügbaren Optionen zum Senden einer Datenschutzauftragsanforderung für den derzeit ausgewählten Regulierungstyp angezeigt werden.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Wählen Sie die **[!UICONTROL Auftragstyp]** der Anforderung (&quot;Löschen&quot;oder &quot;Zugriff&quot;) und eines oder mehrerer verfügbarer Produkte aus der Liste.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

under **[!UICONTROL Namespace-Typ]** wählen Sie den entsprechenden Namespace-Typ für die Kunden-IDs aus, die an gesendet werden. [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Wählen Sie bei Verwendung des Standard-Namespace-Typs einen Namespace aus dem Dropdown-Menü (E-Mail, ECID oder AAID) aus, geben Sie dann die ID-Werte in das Textfeld rechts ein und drücken Sie die Eingabetaste. **\&lt;enter>** für jede ID, um sie der Liste hinzuzufügen.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Bei Verwendung des benutzerdefinierten Namespace-Typs müssen Sie den Namespace manuell eingeben, bevor Sie die unten stehenden ID-Werte angeben.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Klicken Sie abschließend auf **[!UICONTROL Erstellen]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

Das Dialogfeld wird ausgeblendet und der neue Auftrag (oder die neuen Aufträge) wird im Widget Auftragsanfragen zusammen mit dem aktuellen Verarbeitungsstatus aufgeführt.

### Hochladen einer JSON-Datei {#json}

Beim Erstellen komplexerer Anforderungen, z. B. Anforderungen, die mehrere ID-Typen für jedes verarbeitete Datensubjekt verwenden, können Sie eine Anforderung erstellen, indem Sie eine JSON-Datei hochladen.

Wählen Sie den Pfeil neben **[!UICONTROL Anforderung erstellen]**, unter dem Widget Statusbericht auf der rechten Seite des Bildschirms. Wählen Sie in der angezeigten Optionsliste die Option **[!UICONTROL JSON hochladen]**.

![Erstellungsoptionen von Anforderungen](../images/user-guide/create-options.png)

Die **[!UICONTROL JSON hochladen]** angezeigt. Es wird ein Fenster angezeigt, in das Sie Ihre JSON-Datei per Drag-and-Drop ziehen können.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Wenn Sie keine JSON-Datei zum Hochladen haben, wählen Sie **[!UICONTROL Adobe-DSGVO-Request.json herunterladen]** , um eine Vorlage herunterzuladen, die Sie entsprechend den Werten füllen können, die Sie von Ihren Datensubjekten gesammelt haben.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Suchen Sie die JSON-Datei auf Ihrem Computer und ziehen Sie sie in das Dialogfenster. Wenn der Upload erfolgreich war, wird der Dateiname im Dialogfeld angezeigt. Sie können bei Bedarf weitere JSON-Dateien hinzufügen, indem Sie sie per Drag-and-Drop in das Dialogfeld ziehen.

Klicken Sie abschließend auf **[!UICONTROL Erstellen]**. Das Dialogfeld wird ausgeblendet und der neue Auftrag (oder die neuen Aufträge) wird im Widget Auftragsanfragen zusammen mit dem aktuellen Verarbeitungsstatus aufgeführt.

### Nächste Schritte

Durch Lesen dieses Dokuments haben Sie gelernt, wie Sie die [!DNL Privacy Service] Benutzeroberfläche zum Erstellen eines Datenschutzauftrags, zum Anzeigen der Details eines Auftrags, zum Überwachen des Verarbeitungsstatus und zum Herunterladen der Ergebnisse nach Abschluss.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mit dem [!DNL Privacy Service] API, siehe Abschnitt [API-Handbuch](../api/overview.md).
