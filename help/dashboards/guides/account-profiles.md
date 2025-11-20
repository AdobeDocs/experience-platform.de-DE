---
title: Dashboard für Kontoprofile
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zu den B2B-Kontoprofilen Ihres Unternehmens anzeigen können.
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '2249'
ht-degree: 6%

---

# Dashboard für Kontoprofile

Die Benutzeroberfläche von Adobe Experience Platform verfügt über ein Dashboard, über das Sie wichtige Informationen zu Ihren Kontoprofilen anzeigen können. Diese Informationen werden bei einem täglichen Schnappschuss erfasst. In diesem Handbuch wird beschrieben, wie Sie das [!UICONTROL Account Profiles]-Dashboard in der Benutzeroberfläche aufrufen und verwenden können. Außerdem erhalten Sie weitere Informationen zu den im Dashboard angezeigten Visualisierungen.

Dieses Dokument bietet einen Überblick über die Funktionen im [!UICONTROL Account Profiles]-Dashboard und beschreibt ausführlich die verfügbaren Standard-Einblicke. Ausführliche Informationen zu den verfügbaren Funktionen finden [[!UICONTROL Account Profiles] im Handbuch zur ](../../rtcdp/accounts/account-profile-ui-guide.md)-Benutzeroberfläche .

## Erste Schritte

Sie müssen über eine Berechtigung für [Adobe Real-Time Customer Data Platform B2B edition](../../rtcdp/b2b-overview.md) verfügen, um auf das B2B-[!UICONTROL Account Profiles]-Dashboard zugreifen zu können.

## Kontoprofildaten {#data}

Das [!UICONTROL Account Profiles]-Dashboard zeigt eine Momentaufnahme Ihrer einheitlichen Kontoinformationen an. Diese Kontoinformationen stammen aus verschiedenen Quellen in Ihren Marketing-Kanälen und den verschiedenen Systemen, die Ihr Unternehmen derzeit zum Speichern von Kundenkontoinformationen verwendet.

Die Profildaten in der Momentaufnahme zeigen die Daten exakt so an, wie sie zum Zeitpunkt der Momentaufnahme aufgetreten sind. Das heißt, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten und das [!UICONTROL Account Profiles]-Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme der Momentaufnahme an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn die nächste Momentaufnahme erstellt wird.

## Erkunden des [!UICONTROL Account Profiles]-Dashboards {#explore}

Um zum [!UICONTROL Account Profiles]-Dashboard in der Experience Platform-Benutzeroberfläche zu navigieren, wählen Sie **[!UICONTROL Profiles]** unter [!UICONTROL Accounts] im linken Navigationsbereich aus.

![Die Benutzeroberfläche von Experience Platform mit Account-Profilen im linken Navigationsbereich wurde hervorgehoben und die Registerkarte „Übersicht“ wurde angezeigt.](../images/account-profiles/account-profiles-dashboard.png)

Im [!UICONTROL Account Profiles]-Dashboard können Sie entweder [die in Ihr Unternehmen aufgenommenen Account-Profile durchsuchen](#browse-account-profiles) oder [die Gesamtheit Ihrer Account-Profildaten mithilfe von Widgets auf einen Blick einsehen](#standard-widgets).

### Datumsfilter {#date-filter}

Die Registerkarte [!UICONTROL Overview] besteht aus Widgets, die schreibgeschützte Metriken bereitstellen, um wichtige Informationen zu Ihren Kontoprofilen zu übermitteln. Wählen Sie das Kalendersymbol oder die Datumsangaben aus, um den globalen Datumsfilter für Ihre Widgets zu ändern.

>[!IMPORTANT]
>
>Der Datumsbereich, den Sie im Dropdown-Kalender auswählen, wirkt sich auf alle Insights aus, mit Ausnahme der beiden Widgets für die Prognosebewertung [Verteilung](#predictive-scoring-distribution) und [wichtigste Einflussfaktoren](#predictive-scoring-top-influential-factors).

![Die Registerkarte „Kontoprofile - Übersicht“ mit hervorgehobener Datumsauswahl und hervorgehobenem Filtersymbol.](../images/account-profiles/date-filter.png)

### Konfigurieren des Lead-Konto-Abgleichs-Service {#lead-to-account-matching-service}

Wählen Sie **[!UICONTROL Settings]** aus, um den Service Lead-Konto-Zuordnung im Dialogfeld [!UICONTROL Account settings] zu konfigurieren. Ausführliche Informationen zum Konfigurieren der Lead-Konto-Zuordnung finden Sie im [UI-Handbuch](../../rtcdp/accounts/account-profile-ui-guide.md#configure-lead-to-account-matching). Weitere Informationen zur Lead-Konto-Zuordnung finden Sie unter [Lead-Konto-Zuordnung in der Real-Time CDP B2B-Dokumentation](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

![Das Dashboard „Kontoprofile“ mit hervorgehobenen Einstellungen.](../images/account-profiles/settings.png)

## Durchsuchen von Account-Profilen {#browse-account-profiles}

Auf der Registerkarte [!UICONTROL Browse] können Sie die schreibgeschützten Kontoprofile durchsuchen und anzeigen, die in Ihre Organisation aufgenommen wurden. Verwenden Sie eine Konto-ID aus einer verbundenen Unternehmensquelle oder geben Sie Quelldetails direkt ein. In diesem Arbeitsbereich können Sie wichtige Informationen zum Kontoprofil anzeigen, darunter Name, Branche, Umsatz und Zielgruppe.

Wählen Sie die [!UICONTROL Profile ID] aus den Ergebnissen aus, die auf der Registerkarte [!UICONTROL Browse] angezeigt werden, um die Registerkarte [!UICONTROL Details] für das Kontoprofil zu öffnen.

![Die Registerkarte zum Durchsuchen von Account-Profilen mit den angezeigten Ergebnissen und der hervorgehobenen Profil-ID.](../images/account-profiles/account-profiles-browse-tab.png)

Die auf der Registerkarte [!UICONTROL Details] angezeigten Kontoprofilinformationen wurden aus mehreren Profilfragmenten zusammengeführt, um eine zentrale Ansicht des jeweiligen Kontos zu erstellen. Weitere Informationen zu den Funktionen [ Kontoprofilanzeige in der Experience Platform-Benutzeroberfläche finden ](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) in der Dokumentation unter „Durchsuchen von Kontoprofilen in Adobe Real-Time Customer Data Platform&quot;.

## Standard-Widgets {#standard-widgets}

>[!CONTEXTUALHELP]
>id="platform_dashboards_accountprofiles_customersperaccountoverview"
>title="Überblick über Kundinnen und Kunden pro Konto"
>abstract="Dieses Drillthrough-Widget bietet Einblicke in die Struktur Ihrer B2B-Daten. Sie können damit feststellen, wie viele Kontoprofile mit keinem, einem oder mehreren Kundenprofilen verknüpft sind.<ul><li>Direkte Kundschaft: Profile von Kundinnen und Kunden, die über die `personComponents`-Route direkt mit einem Konto verknüpft sind.</li><li>Indirekte Kundschaft: Profile von Kundinnen und Kunden, die über die `Account-Person`-Route mit einem Konto verknüpft sind.</li></ul>"

Adobe bietet Standard-Widgets, mit denen Sie verschiedene Metriken im Zusammenhang mit Ihren Kontoprofilen visualisieren können.

>[!IMPORTANT]
>
>Wenn Sie keinen Datumsfilter angeben, analysiert das Standardverhalten von Insights die Daten, die vom Vorjahr bis heute hinzugefügt wurden.

Um mehr über die einzelnen verfügbaren Standard-Widgets zu erfahren, wählen Sie den Namen eines Widgets aus der folgenden Liste aus:

* [Hinzugefügte Kontoprofile](#account-profiles-added)
* [Überblick über Kundinnen und Kunden pro Konto](#customers-per-account-overview)
   * [Vertriebschancen pro Konto - Übersicht](#opportunities-per-account-overview)
   * [Vertriebschancen nach Kontodetails](#opportunities-per-account-detail)
   * [Kunden pro Kontodetails](#customers-per-account-detail)
* [Neue Konten nach Branche](#accounts-by-industry)
* [Neue Konten nach Typ](#accounts-by-type)
* [Neue Opportunitys nach Personenrolle](#opportunities-by-person-role)
* [Neue Chancen nach Umsatz](#opportunities-by-revenue)
* [Neue Opportunities nach Status und Phase](#opportunities-by-status-&-stage)
* [Neue gewonnene Gelegenheiten](#opportunities-won)
* [Hinzugefügte Opportunities](#opportunities-added)
* [Verteilung der prädiktiven Bewertung](#predictive-scoring-distribution)
* [Prädiktive Bewertung - wichtigste Einflussfaktoren](#predictive-scoring-top-influential-factors)

### Hinzugefügte Kontoprofile {#account-profiles-added}

Das [!UICONTROL Account profiles added]-Widget verwendet ein Liniendiagramm, um die Anzahl der Kontoprofile anzuzeigen, die jeden Tag über einen bestimmten Zeitraum hinzugefügt werden. Verwenden Sie den globalen Datumsfilter oben in Ihrem Dashboard, um den Analysezeitraum zu bestimmen. Wenn kein Datumsfilter angegeben ist, listet das Standardverhalten die Kontoprofile auf, die für das Jahr vor dem heutigen Tag hinzugefügt wurden. Die Ergebnisse können verwendet werden, um einen Trend in der Anzahl der hinzugefügten Kontoprofile abzuleiten.

![Das Widget „Hinzugefügte Kontoprofile“.](../images/account-profiles/account-profiles-added.png)

### Überblick über Kundinnen und Kunden pro Konto {#customers-per-account-overview}

>[!NOTE]
>
>Die [!UICONTROL Customers per account overview] insight und ihre Drill-Through-Diagramme ([!UICONTROL Customers per account detail], [!UICONTROL Opportunities per account overview], [!UICONTROL Opportunities per account detail]) sind von keinen globalen Datumsfiltern betroffen, die Sie möglicherweise festgelegt haben.

Das [!UICONTROL Customers per account overview] Diagramm bietet eine Zusammenfassung der Konten basierend auf ihren Kundentypen. Es wird eine vierzeilige Tabelle angezeigt, die Konten als mit direkten oder indirekten Kunden oder als Konten ohne Kunden kategorisiert. Sie enthält die Gesamtzahl der Konten für jede Kategorie. Das Diagramm hilft bei der Identifizierung der Verteilung von Konten, die direkte und indirekte Kunden haben.

Direktkunden sind Kundenprofile, die über die `personComponents` Route direkt mit einem Konto verknüpft sind. Diese Beziehung ist einfacher und beinhaltet eine direkte, explizite Verbindung zwischen dem Kunden und dem Konto.

Indirekte Kunden sind Kundenprofile, die über die `Account-Person` Route mit einem Konto verknüpft sind. Diese Beziehung ist weniger einfach und beinhaltet eine Zwischenentität oder eine komplexere Verbindung zwischen dem Kunden und dem Konto, in der Regel über andere Konten oder Beziehungen.

![Das Widget „Kunden pro Konto - Übersicht“.](../images/account-profiles/customers-per-account-overview-widget.png)

Um auf detailliertere Einblicke zuzugreifen, wählen Sie die Auslassungspunkte (**…**) im [!UICONTROL Customers per account overview] Diagramm aus und wählen Sie **[!UICONTROL Drill through]** aus dem Dropdown-Menü aus.

![Das Widget Kunden pro Konto - Übersicht mit dem Dropdown-Menü mit den Auslassungspunkten und hervorgehobener Drill-Through-Funktion.](../images/account-profiles/customers-per-account-overview-dropdown.png)

Die Drill-Through-Ansicht wird angezeigt. Als Nächstes sehen Sie sich die verfügbaren Drill-Through-Diagramme an, um ein tieferes Verständnis der Struktur Ihrer B2B-Daten zu erhalten. Anhand dieser Drill-Through-Diagramme können Sie ermitteln, mit wie vielen Account-Profilen keine Kundenprofile verknüpft sind oder mit welchen ein oder mehrere Kundenprofile verknüpft sind. Sie können damit auch ermitteln, wie viele direkte oder indirekte Kunden mit Ihren Konten verknüpft sind.

* [[!UICONTROL Customers per account detail]](#customers-per-account-detail)
* [[!UICONTROL Accounts per opportunity overview]](#accounts-per-opportunity-overview)
* [[!UICONTROL Opportunities per account detail]](#accounts-per-opportunity-detail)

### [!UICONTROL Navigate between dashboard views] {#dashboard-view-navigation}

Um zwischen dem Drill-Through und dem Kontoprofil-Dashboard zu wechseln, wählen Sie das Ordnersymbol (![ein Ordnersymbol) aus.](../images/account-profiles/folder-icon.png)), gefolgt von der richtigen Ansicht aus dem Dropdown-Menü.

![Die Drill-Through-Ansicht im Dashboard „Kontoprofile“ mit hervorgehobenem Dropdown-Menü „Navigation“.](../images/account-profiles/navigation-dropdown.png)

Weitere Informationen zu Drill-Throughs in der Experience Platform-Benutzeroberfläche finden Sie unter [Drill-Through-Handbuch](../sql-insights-query-pro-mode/drill-through.md).

#### [!UICONTROL Customers per account detail] {#customers-per-account-detail}

Das [!UICONTROL Customers per account detail] Diagramm enthält detailliertere Informationen zur Anzahl der Konten, die mit verschiedenen Kundentypen verknüpft sind. Es wird eine dreispaltige Tabelle angezeigt, in der die Anzahl der Konten nach Kundentyp (direkt oder indirekt) und dem damit verbundenen Kundenbereich aufgeführt ist. Dieses Diagramm hilft Ihnen zu verstehen, wie die Kunden auf verschiedene Kundenkategorien verteilt sind und wie viele Konten insgesamt mit den einzelnen Kunden verbunden sind.

![Das Widget „Kunden pro Kontodetails“.](../images/account-profiles/customers-per-account-detail.png)

#### [!UICONTROL Opportunities per account overview] {#opportunities-per-account-overview}

Das [!UICONTROL Opportunities per account overview] stellt eine Zusammenfassung der Accounts dar, die Opportunities haben oder nicht haben. Diese zweizeilige Tabelle hilft Ihnen, schnell die Anzahl der Konten zu ermitteln, die mit Opportunities verbunden sind, und bietet eine Momentaufnahme der Opportunity-Interaktion über alle Konten hinweg.

![Das Widget „Vertriebschancen pro Konto - Übersicht“.](../images/account-profiles/opportunities-per-account-overview.png)

#### [!UICONTROL Opportunities per account detail] {#opportunities-per-account-detail}

Das [!UICONTROL Opportunities per account detail] bietet eine detailliertere Aufschlüsselung der Konten auf der Grundlage der Anzahl der Vertriebschancen, die sie haben. Die Tabelle zeigt die Anzahl der Konten gruppiert nach Opportunity-Zählbereichen an, wie z. B. 1-10 Opportunitys oder 100+ Opportunitys. Dieses Diagramm hilft Ihnen dabei, zu erkennen, wie Konten nach der Anzahl der von ihnen verwalteten Opportunitys verteilt sind.

![Das Widget „Opportunities pro Kontodetails“.](../images/account-profiles/opportunities-per-account-detail.png)

### Neue Konten nach Branche {#accounts-by-industry}

Das Widget [!UICONTROL New accounts by industry] zeigt die Gesamtzahl der Konten in einer einzelnen Metrik in einem Ringdiagramm an. Das Ringdiagramm veranschaulicht die relative Zusammensetzung der verschiedenen Branchen, aus denen diese Summe besteht. Ein farbcodierter Schlüssel bietet eine Aufschlüsselung aller eingeschlossenen Branchen. Die einzelnen Zählungen für jede Branche werden in einem Dialogfeld angezeigt, wenn der Cursor über den entsprechenden Abschnitt des Ringdiagramms bewegt wird.

![Das Widget „Neue Konten nach Branche“.](../images/account-profiles/new-accounts-by-industry.png)

### Neue Konten nach Typ {#accounts-by-type}

Das Widget [!UICONTROL New accounts by type] zeigt die Gesamtzahl der Konten in einer einzelnen Metrik in einem Ringdiagramm an. Das Ringdiagramm veranschaulicht die relative Zusammensetzung verschiedener Kontotypen, aus denen diese Summe besteht. Ein farbcodierter Schlüssel bietet eine Aufschlüsselung aller enthaltenen Kontotypen. Die einzelnen Zählungen für jeden Kontotyp werden in einem Dialogfeld angezeigt, wenn der Cursor über den entsprechenden Abschnitt des Ringdiagramms bewegt wird.

![Das Widget „Neue Konten nach Typ“.](../images/account-profiles/new-accounts-by-type.png)

### Neue Opportunitys nach Personenrolle {#opportunities-by-person-role}

Das Widget [!UICONTROL New opportunities by person role] zeigt die Gesamtzahl Ihrer Opportunitys in einer einzelnen Metrik in einem Ringdiagramm an. Das Ringdiagramm veranschaulicht die relative Zusammensetzung der Rollen, aus denen diese Gesamtzahl von Opportunitys besteht. Ein farbcodierter Schlüssel bietet eine Aufschlüsselung aller enthaltenen Rollen. Die einzelnen Zählungen für jede Rolle werden in einem Dialogfeld angezeigt, wenn der Cursor über den entsprechenden Abschnitt des Ringdiagramms bewegt wird.

>[!NOTE]
>
>Der [!UICONTROL No data found]- oder [!UICONTROL Unable to load] wird verursacht, wenn die Brückentabelle „Opportunity-Person“ nicht in Ihrem Schema verwendet wird. Wenn Ihre insight einen dieser Fehler anzeigt, überprüfen Sie Ihr Vereinigungsschema und stellen Sie sicher, dass die Feldergruppe „Opportunity-Person“ Daten aufnimmt.

![Das Widget „Neue Chancen nach Rolle der Person“.](../images/account-profiles/new-opportunities-by-person-role.png)

### Neue Chancen nach Umsatz {#opportunities-by-revenue}

Das [!UICONTROL New opportunities by revenue] Widget verwendet ein Balkendiagramm, um die geschätzte Gesamteinnahmemenge zu veranschaulichen, die durch Ihre Opportunitys generiert wird. Das Widget unterstützt bis zu sechs Opportunities.

Um ein Dialogfeld anzuzeigen, das den spezifischen Umsatz für eine Opportunity enthält, bewegen Sie den Mauszeiger über die einzelnen Balken.

![Das Widget „Neue Chancen nach Umsatz“.](../images/account-profiles/new-opportunities-by-revenue.png)

### Neue Opportunities nach Status und Phase {#opportunities-by-status-&-stage}

Dieses Widget verwendet ein Balkendiagramm, um die Anzahl der Vertriebschancen zu veranschaulichen, die in allen Phasen der Marketing-/Vertriebs-funnel entweder offen oder geschlossen sind. Das Widget verwendet Farben, um die Phase der Opportunities zu unterscheiden. Ein farbcodierter Schlüssel zeigt die verfügbaren Phasen für Opportunitys an.

![Das Widget „Neue Chancen nach Status und Phase“.](../images/account-profiles/new-opportunities-by-status-&-stage.png)

### Neue gewonnene Gelegenheiten {#opportunities-won}

Das Widget [!UICONTROL New opportunities won] zeigt die Gesamtzahl Ihrer Opportunitys an, die in einem Ringdiagramm in einer einzigen Metrik erfolgreich abgeschlossen wurden. Das Ringdiagramm veranschaulicht die relative Zusammensetzung von Opportunitys, die entweder gewonnen oder nicht gewonnen werden. Ein farbcodierter Schlüssel unterscheidet zwischen gewonnenen und nicht gewonnenen Opportunities. Die einzelnen Zählungen für jede Rolle werden in einem Dialogfeld angezeigt, wenn der Cursor über den entsprechenden Abschnitt des Ringdiagramms bewegt wird.

![Das Widget „Neue gewonnene Gelegenheiten“.](../images/account-profiles/new-opportunities-won.png)

### Hinzugefügte Opportunities {#opportunities-added}

Das [!UICONTROL Opportunities added]-Widget verwendet ein Liniendiagramm, um die Anzahl der Opportunitys anzuzeigen, die jeden Tag über einen bestimmten Zeitraum hinzugefügt werden. Verwenden Sie den globalen Datumsfilter oben in Ihrem Dashboard, um den Analysezeitraum zu bestimmen. Wenn kein Datumsfilter angegeben ist, listet das Standardverhalten die Opportunitys auf, die für das Jahr vor dem heutigen Tag hinzugefügt wurden. Die Ergebnisse können verwendet werden, um einen Trend in der Anzahl der hinzugefügten Opportunitys abzuleiten.

<!-- Link to date filter documentation from Annamalai -->

![Das Widget „Hinzugefügte Opportunitys“.](../images/account-profiles/opportunities-added.png)

### Verteilung der prädiktiven Bewertung {#predictive-scoring-distribution}

Das Widget [!UICONTROL Predictive scoring distribution] zeigt die Score-Verteilung aller Kontoprofile an, damit Sie den Zustand Ihrer Vertriebs-Pipeline auf einen Blick verstehen können. Die Bewertungsdaten werden durch ein Ringdiagramm und ein Säulendiagramm übertragen.

Das Ringdiagramm zeigt den Anteil Ihrer gesamten Account-Profile in jedem der Buckets mit hoher, mittlerer und geringer Kauftendenz. Der Schlüssel bietet weitere Details zu den farbcodierten Abschnitten, einschließlich der Scoring-Bucket-Bereiche und der Anzahl der Account-Profile in diesem Bereich.

Das Säulendiagramm bietet eine detailliertere Aufschlüsselung der Bewertung. Jede Spalte zeigt die Anzahl der Account-Profile in jedem der 20 Buckets mit fünf Punkten.

Das Dropdown-Menü innerhalb des Widgets ermöglicht die Auswahl des Kontobewertungsmodells.

>[!NOTE]
>
>Filter für globale Datumsbereiche gelten nicht für Insights bei der prädiktiven Bewertung. Die Widgets für die prädiktive Bewertung analysieren Daten basierend auf dem im Dropdown-Menü ausgewählten Konto-Scoring-Modell.

![Das Widget „Verteilung der prädiktiven Bewertung“](../images/account-profiles/predictive-scoring-distribution.png)

### Prädiktive Bewertung - wichtigste Einflussfaktoren {#predictive-scoring-top-influential-factors}

Das Widget [!UICONTROL Predictive scoring top influential factors] hilft Ihnen, die wichtigsten Faktoren zu verstehen, die die Bewertungen für jeden Neigungs-Bucket antreiben.

Dieses Widget zeigt die wichtigsten Einflussfaktoren für die Buckets mit hoher, mittlerer und niedriger Neigung an. Ein Balken für jeden Einflussfaktor gibt den Prozentsatz der Kontoprofile in dem Neigungs-Bucket an, der den spezifischen Einflussfaktor enthält.

Das Dropdown-Menü innerhalb des Widgets ermöglicht die Auswahl des Kontobewertungsmodells.

>[!NOTE]
>
>Filter für globale Datumsbereiche gelten nicht für Insights bei der prädiktiven Bewertung. Die Widgets für die prädiktive Bewertung analysieren Daten basierend auf dem im Dropdown-Menü ausgewählten Konto-Scoring-Modell.

![Das Widget „Prädiktive Bewertung - wichtigste Einflussfaktoren“.](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## Fehler beim Laden der Daten {#errors}

Wenn ein Widget angezeigt wird, *[!UICONTROL Unable to load. Try again.]* liegt dies daran, dass keine Daten für die B2B-Entität verfügbar sind. Beispielsweise zeigt das unten angezeigte Widget [!UICONTROL New opportunities by person role] die Nachricht &quot;[!UICONTROL Unable to load. Try again.]&quot;, da diese Sandbox keine Opportunity-Daten hat.

![Fehler &quot;insight kann nicht geladen werden“](../images/account-profiles/unable-to-load.png)

Um das Problem zu beheben, müssen Sie B2B-Entitätsdaten, z. B *Opportunity-*, in die Sandbox aufnehmen. Nach 48 Stunden werden die Daten in den Widgets angezeigt.

## Nächste Schritte

Durch Befolgen dieses Dokuments sollten Sie jetzt wissen, wie Sie das [!UICONTROL Account Profiles]-Dashboard finden und auch die in den verfügbaren Widgets angezeigten Metriken verstehen. Weitere Informationen zum Arbeiten mit Account-Profilen als Teil Ihrer B2B-Daten in der Experience Platform-Benutzeroberfläche finden Sie in der Übersicht [ Account-Profile ](../../rtcdp/accounts/account-profile-overview.md) Adobe Real-Time CDP, B2B edition.
