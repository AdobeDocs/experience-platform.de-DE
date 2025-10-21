---
keywords: Experience Platform;Startseite;beliebte Themen;Exportieren;Exportieren
solution: Experience Platform
title: Verwalten von Datenschutzaufträgen in der Privacy Service-Benutzeroberfläche
description: Erfahren Sie, wie Sie die Benutzeroberfläche von Privacy Service verwenden, um Datenschutzanfragen in verschiedenen Experience Cloud-Programmen zu koordinieren und zu überwachen.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: b960e67789acaeb27a0a39db933a2bbb7d84f4d5
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 19%

---

# Verwalten von Datenschutzaufträgen in der Privacy Service-Benutzeroberfläche {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="Berücksichtigen von Datenschutzanträgen betroffener Personen"
>abstract="<h2>Beschreibung</h2><p>Mit Adobe Experience Platform Privacy Service können Sie Datenschutzanfragen für Kundinnen und Kunden erstellen und verwalten, die ihre personenbezogenen Daten gemäß den gesetzlichen Datenschutzbestimmungen aufrufen oder löschen möchten.</p>"

In diesem Dokument werden die Schritte zum Erstellen und Verwalten von Datenschutzanfragen mithilfe der [!DNL Privacy Service]-Benutzeroberfläche beschrieben.

>[!IMPORTANT]
>
>Privacy Service ist nur für Anfragen der betroffenen Person und für Verbraucherrechtsanfragen vorgesehen. Jegliche andere Verwendung von Privacy Service für die Datenbereinigung oder -wartung wird nicht unterstützt und ist nicht zulässig. Adobe ist gesetzlich verpflichtet, diese rechtzeitig zu erfüllen. Daher sind Lasttests auf Privacy Service nicht zulässig, da es sich um eine reine Produktionsumgebung handelt und ein unnötiger Rückstand gültiger Datenschutzanfragen erzeugt wird.
>
>Es gibt jetzt eine feste tägliche Upload-Grenze, um einen Missbrauch des Dienstes zu verhindern. Für Benutzende, bei denen ein Missbrauch des Systems festgestellt wurde, wird der Zugriff auf den Dienst deaktiviert. Anschließend wird mit ihnen ein Meeting abgehalten, bei dem ihr Handeln und die akzeptable Verwendung von Privacy Service erörtert wird.

## Durchsuchen des Dashboards der [!DNL Privacy Service]-Benutzeroberfläche

Das Dashboard für die [!DNL Privacy Service] Benutzeroberfläche bietet zwei Widgets, mit denen Sie den Status Ihrer Datenschutzaufträge anzeigen können: &quot;[!UICONTROL Status Report]&quot; und &quot;[!UICONTROL Job Requests]&quot;. Das Dashboard zeigt auch die aktuell ausgewählte Verordnung für die angezeigten Aufträge an.

![UI-Dashboard](../images/user-guide/dashboard.png)

### Regulierungstyp

[!DNL Privacy Service] unterstützt Vorgangsanfragen für mehrere Datenschutzbestimmungen. In der folgenden Tabelle sind die unterstützten Verordnungen und die entsprechende Beschriftung aufgeführt, wie in der Benutzeroberfläche dargestellt.

Eine Beschreibung jeder [, in der die Rechte von Verbrauchern und die &#x200B;](../regulations/overview.md) Pflichten des Unternehmens erläutert werden, finden Sie unter „Übersicht über Datenschutzbestimmungen“.

>[!TIP]
>
>Der API-Regulierungstyp wurde aus Gründen der Übersichtlichkeit eingefügt.

| UI-Kennzeichnung | API `regulation_type` | Verordnung |
|-------------------------------------------|-----------------------|----------------|
| [!UICONTROL APA_AUS (Australia)] | `apa_aus` | [!DNL Australia Privacy Act] |
| [!UICONTROL CCCA (California)] | `ccpa` | [!DNL California Consumer Privacy Act] (CCPA) |
| [!UICONTROL CPA_CO_USA (Colorado)] | `cpa_co_usa` | [!DNL Colorado Privacy Act] |
| [!UICONTROL CPRA_CA_USA (California)] | `cpra_ca_usa` | [!DNL California Privacy Rights Act] (CPRA) |
| [!UICONTROL CTDPA_CT_USA (Connecticut)] | `ctdpa_ct_usa` | [!DNL Connecticut Data Privacy Act] |
| [!UICONTROL DPDPA_DE_USA (Delaware)] | `dpdpa_de_usa` | [!DNL Delaware Personal Data Privacy Act] |
| [!UICONTROL FDBR_FL_USA (Florida)] | `fdbr_fl_usa` | [!DNL Florida Digital Bill of Rights] |
| [!UICONTROL GDPR (European Union)] | `gdpr` | Die [!DNL General Data Protection Regulation] der Europäischen Union |
| [!UICONTROL HIPAA_USA (United States)] | `hipaa_usa` | [!DNL Health Insurance Portability and Accountability Act] |
| [!UICONTROL ICDPALIA_USA (Iowa)] | `icdpa_ia_usa` | [!DNL Iowa Consumer Data Protection Act] |
| [!UICONTROL LGPD_BRA (Brazil)] | `lgpd_bra` | Brasiliens &quot;[!DNL General Data Protection Law]&quot; [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL MCDPA_MN_USA (Minnesota)] | `mcdpa_mn_usa` | [!DNL Minnesota Consumer Data Privacy Act] |
| [!UICONTROL MCDPA_MT_USA (Montana)] | `mcdpa_mt_usa` | [!DNL Montana Consumer Data Privacy Act] |
| [!UICONTROL MHMDA_WA_USA (Washington)] | `mhmda_wa_usa` | [!DNL Washington My Health My Data Act] |
| [!UICONTROL MODPA_MD_USA (Maryland)] | `modpa_md_usa` | [!DNL Maryland Online Data Privacy Act] |
| [!UICONTROL NDPA_NE_USA (Nebraska)] | `ndpa_ne_usa` | [!DNL Nebraska Data Protection Act] |
| [!UICONTROL NHPA_NH_USA (New Hampshire)] | `nhpa_nh_usa` | [!DNL New Hampshire Privacy Act] |
| [!UICONTROL NJDPA_NJ_USA (New Jersey)] | `njdpa_nj_usa` | [!DNL New Jersey Data Protection Act] |
| [!UICONTROL NZPA_NZL (New Zealand)] | `nzpa_nzl` | Neuseelands [!DNL Privacy Act] (PA) |
| [!UICONTROL OCPA_OR_USA (Oregon)] | `ocpa_or_usa` | [!DNL Oregon Consumer Privacy Act] |
| [!UICONTROL PDPA_THA (Thailand)] | `pdpa_tha` | Thailands [!DNL Personal Data Protection Act] (PDPA) |
| [!UICONTROL PIPA_KOR (South Korea)] | `pipa_kor` | Südkoreas [!DNL Personal Information Privacy Act] (PIPA) |
| [!UICONTROL QL25_QC_CAN (Quebec)] | `ql25_qc_can` | [!DNL Quebec Law 25] |
| [!UICONTROL TDPSA_TX_USA (Texas)] | `tdpsa_tx_usa` | [!DNL Texas Data Privacy and Security Act] |
| [!UICONTROL TIPA_TN_USA (Tennessee)] | `tipa_tn_usa` | [!DNL Tennessee Information Protection Act] |
| [!UICONTROL UCPA_UT_USA (Utah)] | `ucpa_ut_usa` | [!DNL Utah Consumer Privacy Act] |
| [!UICONTROL VCDPA_VA_USA (Virginia)] | `vcdpa_va_usa` | [!DNL Virginia Consumer Data Protection Act] (VCDPA) |

{style="table-layout:auto"}

<!-- | [!UICONTROL ICDPA_IN_USA (Indiana)]       | `icdpa_in_usa` | [!DNL Indiana Consumer Data Protection Act]| NOT SUPP YET JAN 1st ### ... -->
<!-- | [!UICONTROL KCDPA_KY_USA (Kentucky)]      | `kcdpa_ky_usa`| [!DNL Kentucky Consumer Data Protection Act]|  NOT SUPP YET JAN 1st ### ... -->
<!-- | [!UICONTROL RIDTPPA_RI_USA (Rhode Island)]| `ridtppa_ri_usa` | [!DNL Rhode Island Data Transparency and Privacy Protection Act]|  NOT SUPP YET JAN 1st ### ... -->

>[!NOTE]
>
>Weitere Informationen zum rechtlichen Kontext [&#x200B; einzelnen Verordnungen finden Sie &#x200B;](../regulations/overview.md) der Übersicht zu (unterstützten Datenschutzbestimmungen.

Vorgänge für jeden Regulierungstyp werden separat verfolgt. Um zwischen den Regelungstypen zu wechseln, wählen Sie das Dropdown-Menü **[!UICONTROL Regulation Type]** und dann die gewünschte Regelung aus der Liste aus.

![Die Privacy Service-Konsole mit der Dropdown-Liste „Regulierungstyp“.](../images/user-guide/regulation.png)

Nach Änderung des Regulierungstyps wird das Dashboard aktualisiert und zeigt alle Vorgänge, Filter, Widgets und Dialogfelder für die Erstellung von Aufträgen an, die für die ausgewählte Verordnung gelten.

![Aktualisiertes Dashboard](../images/user-guide/dashboard-update.png)

### Statusbericht

Das Diagramm auf der linken Seite des Statusbericht-Widgets verfolgt gesendete Aufträge im Vergleich zu allen Aufträgen, die möglicherweise mit Fehlern zurückgemeldet wurden. Das Diagramm auf der rechten Seite verfolgt Aufträge, die sich dem Ende des 30-tägigen Compliance-Fensters nähern.

Wählen Sie eine der beiden Umschaltflächen oberhalb des Diagramms aus, um die jeweilige Metrik ein- oder auszublenden.

![](../images/user-guide/hide-errors.png)

Sie können die genaue Anzahl der Aufträge anzeigen, die mit einem Datenpunkt in den Diagrammen verknüpft sind, indem Sie die Maus über den betreffenden Datenpunkt bewegen.

![Mouse-over-Datenpunkte](../images/user-guide/mouse-over.png)

Um weitere Details zu einem bestimmten Datenpunkt anzuzeigen, wählen Sie den betreffenden Datenpunkt aus, um die zugehörigen Aufträge im Widget Auftragsanfragen anzuzeigen. Notieren Sie sich den Filter, der direkt über der Auftragsliste angewendet wird.

![Angewendeter Filter aus Widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Wenn ein Filter auf das Widget Auftragsanfragen angewendet wurde, können Sie den Filter entfernen, indem Sie das **X** auf der Filterpille auswählen. Vorgangsanfragen kehren dann zur Standard-Tracking-Liste zurück.

### Vorgangsanfragen {#job-requests}

Der Arbeitsbereich [!UICONTROL Job Requests] enthält Details zu den letzten Auftragsanfragen in Ihrer Organisation. Zu den Details gehören der Anfragetyp, der aktuelle Status, das Fälligkeitsdatum, die anfragende E-Mail usw. Es werden jeweils 100 Datensätze geladen. Standardmäßig werden die zuletzt erstellten Aufträge oben angezeigt, wobei beim Scrollen zum Durchsuchen mehr Datensätze geladen werden.

>[!NOTE]
>
>Die Daten für zuvor erstellte Aufträge sind nur 30 Tage nach dem Abschlussdatum verfügbar.

Sie können die Liste filtern, indem Sie Keywords in die Suchleiste unter dem [!UICONTROL Job Requests] eingeben. Die Liste wird bei der Eingabe automatisch gefiltert und zeigt Anfragen an, die Werte enthalten, die Ihren Suchbegriffen entsprechen. Das Suchfeld führt eine „Schnellsuche“ durch, die die Datenschutzauftrags-IDs mit den aktuell gerenderten/geladenen Aufträgen in der Benutzeroberfläche abgleicht. Es handelt sich nicht um eine umfassende Suche aller eingereichten Aufträge. Stattdessen handelt es sich um einen Filter, der auf die geladenen Ergebnisse angewendet wird. Verwenden Sie die Privacy Service-API[&#x200B; um Aufträge (basierend auf einer bestimmten Verordnung, Datumsbereichen oder einem einzelnen Auftrag) &#x200B;](../api/privacy-jobs.md#list).

>[!TIP]
>
>Um Datensätze aus den letzten 30 Tagen in die Benutzeroberfläche zu laden, müssen Sie die Tabelle nach unten scrollen und weitere Datensatz-Batches laden.

![Der Abschnitt „Datenschutzkonsolen-Auftragsanfrage“ mit hervorgehobenem Suchfeld.](../images/user-guide/job-search.png)

Alternativ können Sie die Suchschaltfläche verwenden, um eine Datenschutzaufgabenabfrage durchzuführen, die sich über einen bestimmten Datumsbereich erstreckt. Diese Aktion gibt alle Datenschutzaufträge zurück, die von Ihrer Organisation im angegebenen Zeitraum gesendet wurden. Wählen Sie das Dropdown-Menü **[!UICONTROL Requested on]** aus, um ein Start- und Enddatum für die Abfrage auszuwählen. Zu den verfügbaren Optionen gehören [!UICONTROL Today], [!UICONTROL Last 7 Days], [!UICONTROL Last 2 Weeks], [!UICONTROL Last 30 Days] oder [!UICONTROL Custom]. Bei Verwendung mit der Option [!UICONTROL Requested on] zeigt die Suchfunktion nur Auftragsanfragen an, die zwischen den von Ihnen ausgewählten Datumsbereichen gesendet wurden.

![Der Abschnitt „Vorgangsanfrage“ mit dem Suchfeld, dem Dropdown-Menü „Angefordert“ und der hervorgehobenen Suchschaltfläche.](../images/user-guide/requested-on-dropdown-menu.png)

Um die Details einer bestimmten Vorgangsanfrage anzuzeigen, wählen Sie die Vorgangskennung der Anfrage aus der Liste aus, um die **[!UICONTROL Job Details]** zu öffnen.

![Details zu DSGVO-UI-Aufträgen](../images/user-guide/job-details.png)

Dieses Dialogfeld enthält Statusinformationen zu den einzelnen [!DNL Experience Cloud] und deren aktuellen Status in Bezug auf den gesamten Auftrag. Da jeder Datenschutzauftrag asynchron erfolgt, zeigt die Seite das Datum und die Uhrzeit der letzten Kommunikation (GMT) jeder Lösung an, da einige mehr Zeit benötigen als andere, um die Anfrage zu verarbeiten.

Wenn eine Lösung zusätzliche Daten bereitgestellt hat, können diese in diesem Dialogfeld angezeigt werden. Sie können diese Daten anzeigen, indem Sie einzelne Produktzeilen auswählen.

Um die vollständigen Auftragsdaten als CSV-Datei herunterzuladen, wählen Sie oben rechts im Dialogfeld **[!UICONTROL Export to CSV]** aus.

## Erstellen einer neuen Anfrage für einen Datenschutzauftrag {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="Anweisungen"
>abstract="<ul><li>Wählen Sie <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=de#logging-in-from-experience-platform">Anfragen</a> in der linken Navigation aus, um die Datenschutz-URL zu öffnen, und wählen Sie dann <b>Anfrage erstellen</b> aus.</li><li>Von hier aus können Sie entweder den Anfrage-Builder verwenden oder eine JSON-Datei mit betroffenen Personen hochladen.</li><li>Wenn Sie den Anfrage-Builder verwenden, wählen Sie den Auftragstyp (Zugriff und/oder Löschen) aus und wählen Sie dann den Typ der von Ihnen bereitgestellten Identität (E-Mail, ECID oder AAID) aus oder geben Sie einen benutzerdefinierten Identity-Namespace ein. Geben Sie die entsprechenden Identitätswerte für die Kundinnen bzw. Kunden ein und klicken Sie auf <b>Erstellen</b>, wenn Sie fertig sind.</li><li>Wählen Sie beim Hochladen einer JSON-Datei den Pfeil neben „Anfrage erstellen“ aus. Wählen Sie aus der Liste der Optionen <b>JSON hochladen</b> aus und laden Sie Ihre Datei hoch. Wenn Sie keine JSON-Datei zum Hochladen haben, wählen Sie <b>Adobe-GDPR-Request.json herunterladen</b> aus, um eine Vorlage herunterzuladen, die Sie ausfüllen können. Laden Sie die JSON-Datei hoch und klicken Sie auf <b>Erstellen</b>, wenn Sie fertig sind.</li><li>Weitere Informationen zu dieser Funktion finden Sie im <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html?lang=de">Benutzerhandbuch zum Privacy Service</a> auf Experience League.</li></ul>"

>[!NOTE]
>
>Um eine Datenschutzanfrage zu erstellen, müssen Sie Identitätsinformationen für die spezifischen Kundinnen und Kunden angeben, auf deren Daten zugegriffen werden soll oder die gelöscht werden sollen. Lesen Sie das Dokument zu [Identitätsdaten für Datenschutzanfragen](../identity-data.md) bevor Sie mit diesem Abschnitt fortfahren.

Die [!DNL Privacy Service] Benutzeroberfläche bietet zwei Methoden zum Erstellen neuer Auftragsanfragen:

* [Verwenden des Anfragen-Builders](#request-builder)
* [Hochladen einer JSON-Datei](#json)

Die Schritte zur Verwendung jeder dieser Methoden werden in den folgenden Abschnitten beschrieben.

### Verwenden des Anfragen-Builders {#request-builder}

Mit dem Anfrage-Builder können Sie in der -Benutzeroberfläche manuell eine neue Datenschutzanfrage erstellen. Der Request Builder eignet sich am besten für einfachere und kleinere Anfragesätze, da der Request Builder Anfragen so einschränkt, dass sie nur einen ID-Typ pro Benutzer haben. Bei komplizierteren Anfragen ist es möglicherweise besser, stattdessen [eine JSON-Datei hochzuladen](#json).

Um mit der Verwendung des Anfrage-Builders zu beginnen, wählen Sie **[!UICONTROL Create Request]** unter dem Widget Statusbericht auf der rechten Seite des Bildschirms aus.

![Anfrage erstellen auswählen](../images/user-guide/create-request.png)

Das Dialogfeld **[!UICONTROL Create Request]** wird geöffnet und zeigt die verfügbaren Optionen zum Senden einer Datenschutzanfrage für den derzeit ausgewählten Regulierungstyp an.

![](../images/user-guide/request-builder.png){width=500}

Wählen Sie den **[!UICONTROL Job Type]** der Anfrage („Löschen“ oder „Zugriff„) und ein oder mehrere verfügbare Produkte aus der Liste aus.

Privacy Service unterstützt zwei Arten von Vorgangsanfragen für personenbezogene Daten: [!UICONTROL Access] (Lesen) und/oder [!UICONTROL Delete]. Sie können entweder eine Anfrage stellen, um alle im Produkt gespeicherten Informationen zu erhalten, die sich auf den Gegenstand der Anfrage beziehen, oder eine Löschung aller Informationen anfordern, die sich auf den Gegenstand der Anfrage beziehen.

![](../images/user-guide/type-and-products.png){width=500}

Wählen Sie unter **[!UICONTROL Namespace type]** den entsprechenden Namespace-Typ für die Kunden-IDs aus, die an [!DNL Privacy Service] gesendet werden sollen.

![](../images/user-guide/namespace-type.png){width=500}

Wenn Sie den standardmäßigen Namespace-Typ verwenden, wählen Sie aus dem Dropdown-Menü (E-Mail, ECID oder AAID) einen Namespace aus und geben Sie dann die ID-Werte in das Textfeld rechts ein. Drücken Sie dann **\&lt;enter>** für jede ID, um sie der Liste hinzuzufügen.

![](../images/user-guide/standard-namespace.png){width=500}

Bei Verwendung des benutzerdefinierten Namespace-Typs müssen Sie den Namespace manuell eingeben, bevor Sie die unten stehenden ID-Werte angeben.

![](../images/user-guide/custom-namespace.png){width=500}

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Create]** aus.

![](../images/user-guide/request-builder-create.png){width=500}

Das Dialogfeld verschwindet, und der neue Auftrag (oder die neuen Aufträge) werden im Widget Auftragsanfragen zusammen mit ihrem aktuellen Verarbeitungsstatus aufgeführt.

### Hochladen einer JSON-Datei {#json}

Bei der Erstellung komplexerer Anfragen, z. B. solche, die mehrere ID-Typen für jede verarbeitete betroffene Person verwenden, können Sie eine Anfrage erstellen, indem Sie eine JSON-Datei hochladen.

Wählen Sie den Pfeil neben **[!UICONTROL Create Request]**, unterhalb des Widgets Statusbericht auf der rechten Seite des Bildschirms. Wählen Sie aus der angezeigten Liste der Optionen **[!UICONTROL Upload JSON]** aus.

![Optionen für die Anfrageerstellung](../images/user-guide/create-options.png)

Das Dialogfeld **[!UICONTROL Upload JSON]** wird angezeigt und bietet ein Fenster, in das Sie Ihre JSON-Datei ziehen und ablegen können.

![](../images/user-guide/upload-json.png){width=500}

Wenn Sie keine JSON-Datei zum Hochladen haben, wählen Sie **[!UICONTROL Download Adobe-GDPR-Request.json]** aus, um eine Vorlage herunterzuladen, die Sie entsprechend den von Ihren betroffenen Personen erfassten Werten ausfüllen können.


![](../images/user-guide/privacy-template.png){width=500}


Suchen Sie die JSON-Datei auf Ihrem Computer und ziehen Sie sie in das Dialogfenster. Wenn der Upload erfolgreich war, wird der Dateiname im Dialogfeld angezeigt. Sie können weitere JSON-Dateien nach Bedarf hinzufügen, indem Sie sie per Drag-and-Drop in das Dialogfeld ziehen.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Create]** aus. Das Dialogfeld verschwindet, und der neue Auftrag (oder die neuen Aufträge) werden im Widget Auftragsanfragen zusammen mit ihrem aktuellen Verarbeitungsstatus aufgeführt.

### Nächste Schritte

Durch das Lesen dieses Dokuments haben Sie gelernt, wie Sie mit der [!DNL Privacy Service]-Benutzeroberfläche einen Datenschutzauftrag erstellen, die Details eines Auftrags anzeigen und dessen Verarbeitungsstatus überwachen sowie die Ergebnisse nach Abschluss herunterladen können.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe der [!DNL Privacy Service]-API finden Sie im [API-Handbuch](../api/overview.md).
