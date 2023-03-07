---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Benutzeroberfläche;Benutzeroberfläche;Anpassung;Profil-Dashboard;Dashboard
title: Handbuch zum Profile-Dashboard
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zu den Echtzeit-Kundenprofildaten Ihres Unternehmens anzeigen können.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: a28c1c00fd0b33af3b797ecf2b4d45154dedc823
workflow-type: tm+mt
source-wordcount: '3385'
ht-degree: 92%

---

# [!UICONTROL Profile]-Dashboard

Die Benutzeroberfläche von Adobe Experience Platform verfügt über ein Dashboard, über das Sie wichtige Informationen über Ihre [!DNL Real-Time Customer Profile]-Daten anzeigen können, die während eines täglichen Schnappschusses erfasst wurden. In diesem Handbuch wird beschrieben, wie Sie auf das Profile-Dashboard in der Benutzeroberfläche zugreifen und mit ihm arbeiten können. Außerdem erhalten Sie Informationen zu den im Dashboard angezeigten Metriken.

Eine Übersicht über alle Profilfunktionen in der Benutzeroberfläche der Experience Platform finden Sie im Abschnitt [Handbuch zur Benutzeroberfläche des Echtzeit-Kundenprofils](../../profile/ui/user-guide.md).

## Daten des Profile-Dashboards

Im Dashboard „Profile“ wird eine Momentaufnahme der Attributdaten (Datensatzdaten) wiedergegeben, die sich für Ihre Organisation im Profilspeicher in Experience Platform befinden. Die Momentaufnahme enthält keine Ereignisdaten (Zeitreihendaten).

Die Attributdaten in der Momentaufnahme zeigen die Daten exakt so an, wie sie zum Zeitpunkt der Momentaufnahme vorgefunden werden. Das heißt, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten und das Profile-Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme der Momentaufnahme an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn die nächste Momentaufnahme erstellt wird.

## Das Profile-Dashboard erkunden

Um in der Platform-Benutzeroberfläche zum Profile-Dashboard zu navigieren, wählen Sie **[!UICONTROL Profile]** in der linken Leiste und dann die Registerkarte **[!UICONTROL Übersicht]** aus, um das Dashboard anzuzeigen.

>[!NOTE]
>
>Wenn Platform neu für Ihr Unternehmen ist und noch keine aktiven Profildatensätze oder Zusammenführungsrichtlinien erstellt hat, ist das Profile-Dashboard nicht zu sehen. Stattdessen wird die [!UICONTROL Übersicht] enthält Links und Dokumentation, die Ihnen bei den ersten Schritten mit dem Echtzeit-Kundenprofil helfen.

![Das Dashboard Experience Platform Profile mit hervorgehobenen Profilen und Übersicht.](../images/profiles/dashboard-overview.png)

### Das Profile-Dashboard modifizieren

Sie können das Erscheinungsbild des Profile-Dashboards ändern, indem Sie **[!UICONTROL Dashboard modifizieren]** auswählen. Dadurch können Sie Widgets im Dashboard verschieben, hinzufügen und entfernen sowie auf die **[!UICONTROL Widget-Bibliothek]** zugreifen, um verfügbare Widgets zu erkunden und benutzerdefinierte Widgets für Ihre Organisation zu erstellen.

Weitere Informationen finden Sie in der Dokumentation [Dashboards modifizieren](../customize/modify.md) und [Widget-Bibliothek – Übersicht](../customize/widget-library.md).

### Hinzufügen von Widgets {#add-widget}

Wählen Sie **[!UICONTROL Widget hinzufügen]** aus, um zur Widget-Bibliothek zu navigieren und eine Liste der verfügbaren Widgets anzuzeigen, die Sie Ihrem Dashboard hinzufügen können.

![Die Übersicht über das Profile-Dashboard mit der hervorgehobenen Option „Widget hinzufügen“.](../images/profiles/profiles-overview-add-widget.png)

In der Widget-Bibliothek können Sie die standardmäßigen und benutzerdefinierten Segment-Widgets durchsuchen. Informationen zum Hinzufügen von Widgets finden Sie in der Widget-Bibliothek-Dokumentation zum [Hinzufügen eines Widgets](../customize/widget-library.md#add-widgets).

<!-- ## (Beta) Profile efficacy insights {#profile-efficacy-insights}

>[!IMPORTANT]
>
>The profile efficacy insight functionality is currently in beta and are not available to all users. The documentation and the functionality are subject to change.

The [!UICONTROL Efficacy] tab provides metrics on the quality and completeness of your profile data through the use of profile efficacy widgets. These widgets illustrate at a glance the composition of your profiles, trends in completeness over time, and assessments on the quality of your profile data.

![The profile efficacy dashboard.](../images/profiles/attributes-quality-assessment.png)

See the [profile efficacy widgets section](#profile-efficacy-widgets) for more information on the widgets currently available.

The layout of this dashboard is also customizable by selecting [**[!UICONTROL Modify dashboard]**](../customize/modify.md) from the [!UICONTROL Overview] tab. -->

## Profile durchsuchen {#browse-profiles}

Mit der Registerkarte [!UICONTROL Durchsuchen] können Sie die schreibgeschützten Profile Ihrer Organisation durchsuchen und anzeigen. Hier finden Sie wichtige Informationen über das Profil bezüglich Voreinstellungen, vergangener Ereignisse, Interaktionen und Segmente.

Weitere Informationen zu den in der Platform-Benutzeroberfläche bereitgestellten Funktionen zur Profilanzeige finden Sie in der Dokumentation unter [Durchsuchen von Profilen in Adobe Real-time Customer Data Platform](../../rtcdp/profile/profile-browse.md).

## Zusammenführungsrichtlinien {#merge-policies}

Die im Dashboard &quot;Profile&quot;angezeigten Metriken basieren auf Zusammenführungsrichtlinien, die auf Ihre Echtzeit-Kundenprofildaten angewendet werden. Wenn Daten aus mehreren Quellen zusammengeführt werden, um das Kundenprofil zu erstellen, können die Daten widersprüchliche Werte enthalten. Beispielsweise kann ein Datensatz einen Kunden als „unverheiratet“ auflisten, während ein anderer Datensatz den Kunden als „verheiratet“ führt. Mithilfe der Zusammenführungsrichtlinie wird bestimmt, welche Daten als Teil des Profils priorisiert und angezeigt werden sollen.

Weitere Informationen zu Zusammenführungsrichtlinien, einschließlich der Erstellung, Bearbeitung und Deklaration einer standardmäßigen Zusammenführungsrichtlinie für Ihre Organisation, finden Sie im Abschnitt [Zusammenführungsrichtlinien – Übersicht](../../profile/merge-policies/overview.md).

Im Dashboard wird automatisch eine zu verwendende Zusammenführungsrichtlinie ausgewählt. Die angewendete Zusammenführungsrichtlinie kann über das Dropdown-Menü neben dem Namen der Zusammenführungsrichtlinie geändert werden.

>[!NOTE]
>
>Im Dropdown-Menü werden nur Zusammenführungsrichtlinien angezeigt, die das `_xdm.context.profile`-Schema verwenden. Wenn Ihr Unternehmen jedoch mehrere Zusammenführungsrichtlinien erstellt hat, müssen Sie möglicherweise scrollen, um die vollständige Liste der verfügbaren Zusammenführungsrichtlinien zu sehen.

![Die Registerkarte „Profile – Übersicht“ mit hervorgehobenem Dropdown-Menü „Zusammenführungsrichtlinie“.](../images/profiles/select-merge-policy.png)

## Vereinigungsschemata

Das Dashboard [!UICONTROL Vereinigungsschema] zeigt das Vereinigungsschema für eine bestimmte XDM-Klasse an. Durch Auswahl des Dropdown-Menüs **[!UICONTROL Klasse]** können Sie die Vereinigungsschemata für verschiedene XDM-Klassen anzeigen.

Vereinigungsschemata bestehen aus mehreren Schemata, die dieselbe Klasse haben und für Profil aktiviert wurden. Damit haben Sie die Möglichkeit, in einer einzigen Ansicht alle Felder zu sehen, die in allen Schemata derselben Klasse enthalten sind.

Weitere Informationen über das [Anzeigen von Vereinigungsschemata in der Platform-Benutzeroberfläche](../../profile/ui/union-schema.md#view-union-schemas) finden Sie im Handbuch zur Benutzeroberfläche des Vereinigungsschemas.

## Widgets und Metriken

Das Dashboard besteht aus Widgets, die schreibgeschützte Metriken sind und wichtige Informationen zu Ihren Profildaten enthalten.

Datum und Uhrzeit des letzten Schnappschusses werden oben in der Registerkarte [!UICONTROL Übersicht] neben dem Dropdown-Menü „Zusammenführungsrichtlinie“ angezeigt. Alle Widget-Daten sind zum Stand dieses Datums und dieser Uhrzeit korrekt. Der Zeitstempel der Momentaufnahme wird im UTC-Format angegeben, nicht in der Zeitzone der jeweiligen Person oder Organisation.

![Die Registerkarte „Profile-Dashboard – Übersicht“ mit hervorgehobenem Zeitstempel des letzten Schnappschusses.](../images/profiles/snapshot-timestamp.png)

## Standard-Widgets {#standard-widgets}

Adobe bietet mehrere Standard-Widgets, mit denen Sie verschiedene Metriken im Zusammenhang mit Ihren Profildaten visualisieren können. Über die [!UICONTROL Widget-Bibliothek] können Sie auch benutzerdefinierte Widgets erstellen und für Ihre Organisation freigeben. Um mehr über das Erstellen benutzerdefinierter Widgets zu erfahren, lesen Sie zunächst den Abschnitt [Widget-Bibliothek – Übersicht](../customize/widget-library.md).

Um mehr über die einzelnen verfügbaren Standard-Widgets zu erfahren, wählen Sie den Namen eines Widgets aus der folgenden Liste aus:

* [[!UICONTROL Anzahl der Profile]](#profile-count)
* [[!UICONTROL Trend der Profilanzahl]](#profile-count-trend)
* [[!UICONTROL Änderung der Profilanzahl]](#profile-count-change)
* [[!UICONTROL Trend der Änderung der Profilanzahl]](#profiles-count-change-trend)
* [[!UICONTROL Trend der Änderung der Profilanzahl nach Identität]](#profiles-count-change-trend-by-identity)
* [[!UICONTROL Profile nach Identität]](#profiles-by-identity)
* [[!UICONTROL Identitätsüberschneidung]](#identity-overlap)
* [[!UICONTROL Einzelidentitätsprofile]](#single-identity-profiles)
* [[!UICONTROL Einzelne Identitätsprofile nach Identität]](#single-identity-profiles-by-identity)
* [[!UICONTROL Nicht segmentierte Profile]](#unsegmented-profiles)
* [[!UICONTROL Trendänderung von nicht segmentierten Profilen]](#unsegmented-profiles-change-trend)
* [[!UICONTROL Nicht segmentierte Profile nach Identität]](#unsegmented-profiles-by-identity)
* [[!UICONTROL Audiences]](#audiences)
* [[!UICONTROL Audiences, die einem Zielstatus zugeordnet sind]](#audiences-mapped-to-destination-status)
* [[!UICONTROL Audience-Größe]](#audiences-size)
* [[!UICONTROL Zielgruppenüberschneidung nach Zusammenführungsrichtlinie]](#audience-overlap-by-merge-policy)
* [[!UICONTROL Bericht zur Zielgruppenüberschneidung]](#audience-overlap-report)

### [!UICONTROL Anzahl der Profile] {#profile-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilecount"
>title="Anzahl der Profile"
>abstract="Dieses Widget zeigt die Gesamtzahl der zusammengeführten Profile im Profilspeicher zum Zeitpunkt des Schnappschusses an. Die Zahl hängt von der ausgewählten Zusammenführungsrichtlinie ab, die auf Ihre Profildaten angewendet wird."

Das Widget **[!UICONTROL Profilanzahl]** zeigt die Gesamtzahl der zusammengeführten Profile im Profilspeicher zum Zeitpunkt des Schnappschusses an. Diese Zahl ist das Ergebnis der Anwendung der ausgewählten Zusammenführungsrichtlinie auf Ihre Profildaten, um für jede Person Profilfragmente zu einem einzigen Profil zusammenzuführen.

Weitere Informationen finden Sie im [Abschnitt über Zusammenführungsrichtlinien weiter oben in diesem Dokument](#merge-policies).

>[!NOTE]
>
>Das Widget [!UICONTROL Profilanzahl] kann aus mehreren Gründen eine andere Zahl anzeigen als die Registerkarte [!UICONTROL Durchsuchen] im Abschnitt [!UICONTROL Profile] der Benutzeroberfläche. Der häufigste Grund ist, dass die Registerkarte [!UICONTROL Durchsuchen] die Gesamtzahl der zusammengeführten Profile basierend auf der standardmäßigen Zusammenführungsrichtlinie Ihrer Organisation angibt, während das Widget [!UICONTROL Profilanzahl] die Gesamtzahl der zusammengeführten Profile basierend auf der Zusammenführungsrichtlinie referenziert, die Sie für die Anzeige im Dashboard ausgewählt haben.
>
>Ein weiterer häufiger Grund besteht darin, dass der Dashboard-Schnappschuss und der Beispielvorgang für die Registerkarte [!UICONTROL Durchsuchen] zu unterschiedlichen Zeiten ausgeführt wird. Sie können sehen, wann das Widget [!UICONTROL Profilanzahl] zuletzt aktualisiert wurde, indem Sie den Zeitstempel im Widget überprüfen. Weitere Informationen dazu, wie der Beispielauftrag im [!UICONTROL Durchsuchen] Registerkarte, siehe [Abschnitt zur Profilanzahl im Handbuch zur Benutzeroberfläche des Echtzeit-Kundenprofils](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=de#profile-count).

![Das Dashboard Experience Platform Profile mit hervorgehobenem Widget Profilanzahl.](../images/profiles/profile-count.png)

### [!UICONTROL Trend der Profilanzahl] {#profile-count-trend}

Das Widget [!UICONTROL Trend der Profilanzahl] verwendet ein Liniendiagramm, um den Trend der Gesamtzahl der im System enthaltenen Profile im Zeitverlauf zu veranschaulichen. Diese Gesamtzahl enthält alle Profile, die seit dem letzten täglichen Schnappschuss in das System importiert wurden. Die Daten können über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt.

![Das Widget „Trend der Profilanzahl“.](../images/profiles/profile-count-trend.png)

### [!UICONTROL Änderung der Profilanzahl] {#profile-count-change}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescountchange"
>title="Änderung der Profilanzahl"
>abstract="Dieses Widget zeigt die Gesamtzahl der zusammengeführten Profile an, die zum Profilspeicher zum Zeitpunkt des letzten Schnappschusses **hinzugefügt** wurden. Die Zahl hängt von der ausgewählten Zusammenführungsrichtlinie ab, die auf Ihre Profildaten angewendet wird."

Das Widget **[!UICONTROL Änderung der Profilanzahl]** zeigt die Anzahl der zusammengeführten Profile an, die seit dem vorherigen Schnappschuss zum Profilspeicher hinzugefügt wurden. Diese Zahl ist das Ergebnis der Anwendung der ausgewählten Zusammenführungsrichtlinie auf Ihre Profildaten, um für jede Person Profilfragmente zu einem einzigen Profil zusammenzuführen. Mit der Dropdown-Auswahl können Sie die Anzahl der Profile anzeigen, die in den letzten 30 Tagen, 90 Tagen oder 12 Monaten hinzugefügt wurden.

>[!NOTE]
>
>Das Widget [!UICONTROL Änderung der Profilanzahl] enthält die Anzahl der hinzugefügten Profile, die **nach** der ersten Profilaufnahme und der Einrichtung des Profilspeichers hinzugefügt wurden. Mit anderen Worten: Wenn Ihre Organisation den Profilspeicher einrichtet und am ersten Tag 4.000.000 aufnimmt, ist das Dashboard innerhalb von 24 Stunden verfügbar, jedoch wird im Widget [!UICONTROL Änderung der Profilanzahl] 0 angezeigt. Dies geschieht, um eine Spitze zu vermeiden, die mit der anfänglichen Aufnahme von Profilen in das System verbunden ist. In den nächsten 30 Tagen nimmt Ihre Organisation weitere 1.000.000 Profile in den Profilspeicher auf. Wenn der nächste Schnappschuss erstellt wird, zeigt das Widget [!UICONTROL Änderung der Profilanzahl] insgesamt 1.000.000 hinzugefügte Profile an, während das Widget [!UICONTROL Profilanzahl] insgesamt 5.000.000 Profile anzeigt.

![Das Profile-Dashboard der Platform-Benutzeroberfläche mit dem hervorgehobenen Widget „Änderung der Profilanzahl“.](../images/profiles/profile-count-change.png)

### [!UICONTROL Trend der Änderung der Profilanzahl] {#profiles-count-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesaddedtrend"
>title="Trend der Änderung der Profilanzahl"
>abstract="Dieses Widget zeigt die Zahl der zusammengeführten Profile an, die in den letzten 30 Tagen, 90 Tagen oder 12 Monaten täglich zum Profilspeicher hinzugefügt wurden. Die Zahl hängt auch von der ausgewählten Zusammenführungsrichtlinie ab, die auf Ihre Profildaten angewendet wird."

Das Widget **[!UICONTROL Trend der Änderung der Profilanzahl]** zeigt die Gesamtzahl der zusammengeführten Profile an, die in den letzten 30 Tagen, 90 Tagen oder 12 Monaten täglich zum Profilspeicher hinzugefügt wurden. Diese Zahl wird jeden Tag aktualisiert, wenn der Schnappschuss erstellt wird. Wenn Sie also Profile in Platform aufnehmen, wird die Anzahl der Profile erst beim nächsten Schnappschuss angezeigt. Die Anzahl der hinzugefügten Profile ist das Ergebnis der ausgewählten Zusammenführungsrichtlinie, die auf Ihre Profildaten angewendet wird, um Profilfragmente zusammenzuführen und so für jede Person ein Profil zu erstellen.

Weitere Informationen finden Sie im [Abschnitt über Zusammenführungsrichtlinien weiter oben in diesem Dokument](#merge-policies).

Das Widget **[!UICONTROL Trend der Änderung der Profilanzahl]** verfügt oben rechts im Widget über eine Schaltfläche für Beschriftungen. Wählen Sie **[!UICONTROL Beschriftungen]** aus, um das Dialogfeld „Automatische Beschriftungen“ zu öffnen.

![Die Registerkarte „Profilübersicht“ mit dem Widget „Trend der Änderung der Profilanzahl“ und der hervorgehobenen Schaltfläche „Beschriftungen“.](../images/profiles/profiles-count-change-trend-captions.png)

Ein Modell für maschinelles Lernen generiert automatisch Beschriftungen zur Beschreibung der wichtigsten Trends und Ereignisse, indem es das Diagramm und die Daten analysiert. Anmerkungen werden dem Diagramm basierend auf den Beschriftungen hinzugefügt. Wählen Sie eine Beschriftung aus, um sich auf die zugehörige Anmerkung zu konzentrieren.

![Das Dialogfeld für automatische Beschriftungen für das Widget „Trend der Änderung der Profilanzahl“.](../images/profiles/profiles-added-trends-automatic-captions-dialog-with-annotation.png)

### [!UICONTROL Trend der Änderung der Profilanzahl nach Identität] {#profiles-count-change-trend-by-identity}

<!-- This widget uses a line graph to illustrate the change in number of profiles filtered by a chosen source identity and merge policy. -->

Dieses Widget filtert die Profilanzahl anhand einer ausgewählten Quellidentität und Zusammenführungsrichtlinie und veranschaulicht dann mithilfe eines Liniendiagramms die Änderung der Anzahl für verschiedene Zeiträume. Die Zusammenführungsrichtlinie wird oben auf der Seite im Dropdown-Menü „Übersicht“ ausgewählt. Die Quellidentität und der Zeitraum werden aus den Widget-Dropdown-Menüs ausgewählt. Der Trend kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden.

Dieses Widget hilft Ihnen bei der Verwaltung Ihrer Zielaktivierung, indem es das Wachstumsmuster der Profile darstellt, die nach der entsprechenden Identität gefiltert wurden.

![Der Trend der Veränderung der Profilanzahl nach Identitäts-Widget.](../images/profiles/profiles-count-change-trend-by-identity.png)

### [!UICONTROL Profile nach Identität] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbyidentity"
>title="Profile nach Identität"
>abstract="Dieses Widget zeigt die Aufschlüsselung aller zusammengeführten Profile im Profil Store nach Identitäten an."

Das Widget **[!UICONTROL Profile nach Identität]** zeigt die Aufschlüsselung der Identitäten in allen zusammengeführten Profile in Ihrem Profile Store an. Die Gesamtzahl der Profile nach Identität (d. h. das Addieren der für jeden Namespace angezeigten Werte) kann höher sein als die Gesamtzahl der zusammengeführten Profile, da einem Profil mehrere Namespaces zugeordnet sein können. Wenn beispielsweise ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Namespaces zugeordnet.

Weitere Informationen finden Sie im [Abschnitt zu Zusammenführungsrichtlinien weiter oben in diesem Dokument](#merge-policies).

![Das Dashboard „Profile – Übersicht“ mit hervorgehobenem Widget „Profile nach Identität“.](../images/profiles/profiles-by-identity.png)

Wählen Sie **[!UICONTROL Beschriftungen]** aus, um das Dialogfeld für automatische Beschriftungen zu öffnen.

![Das Dialogfeld für Beschriftung von Profilen nach Identität.](../images/profiles/profiles-by-identity-captions.png)

Ein maschinelles Lernmodell generiert automatisch Dateneinblicke, indem es die Gesamtverteilung und die Schlüsselaspekte der Daten analysiert.

Weitere Informationen zu Identitäten finden Sie in der [Dokumentation zu Adobe Experience Platform Identity Service](../../identity-service/home.md).

### [!UICONTROL Identitätsüberschneidung] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_identityoverlap"
>title="Identitätsüberschneidung"
>abstract="Dieses Widget verwendet ein Venn-Diagramm, um die Überschneidung von Profilen in Ihrem Profile Store anzuzeigen, die die beiden ausgewählten Identitäten enthalten."

Das Widget **[!UICONTROL Identitätsüberschneidung]** verwendet ein Venn-Diagramm, oder Mengendiagramm, um die Überschneidung von Profilen in Ihrem Profile Store anzuzeigen, die die beiden ausgewählten Identitäten enthalten.

Verwenden Sie die Widget-Dropdown-Menüs, um die Identitäten auszuwählen, die Sie vergleichen möchten. Kreise zeigen die relative Gesamtzahl der Profile an, in denen jede Identität enthalten ist. Die Anzahl der Profile, in denen beide Identitäten enthalten sind, wird durch die Größe der Überschneidung zwischen den Kreisen dargestellt. Wenn ein Kunde mit Ihrer Marke über mehr als einen Kanal interagiert, werden diesem einzelnen Kunden mehrere Identitäten zugeordnet. Daher ist es wahrscheinlich, dass Ihre Organisation über mehrere Profile verfügt, die Fragmente aus mehr als einer Identität enthalten.

Weiterführende Informationen zu Profilfragmenten finden Sie im Abschnitt zu [Profilfragmente im Vergleich zu zusammengeführten Profilen](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=de#profile-fragments-vs-merged-profiles) in der Übersicht über das Echtzeit-Kundenprofil .

Weitere Informationen zu Identitäten finden Sie in der [Dokumentation zu Adobe Experience Platform Identity Service](../../identity-service/home.md).

![Die Übersicht über das Profil-Dashboard mit dem Widget zur Identitätsüberschneidung wurde hervorgehoben.](../images/profiles/identity-overlap.png)

### [!UICONTROL Einzelne Identitätsprofile] {#single-identity-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_singleidentityprofiles"
>title="Einzelne Identitätsprofile"
>abstract="Dieses Widget gibt die Anzahl der Profile in Ihrer Organisation an, die zur Erstellung ihrer Identität nur über einen einzigen ID-Typ verfügen. Dieser ID-Typ kann entweder eine E-Mail oder eine ECID sein."

Das Widget [!UICONTROL Einzelne Identitätsprofile] gibt die Anzahl der Profile Ihres Unternehmens an, die nur über einen einzigen ID-Typ verfügen, mit dem ihre Identität erstellt wird. Dieser ID-Typ kann entweder eine E-Mail oder eine ECID sein. Die Anzahl der Profile wird aus den Daten des letzten Schnappschusses generiert.

![Das Widget „Einzelne Identitätsprofile“.](../images/profiles/single-identity-profiles.png)

### [!UICONTROL Einzelne Identitätsprofile nach Identität] {#single-identity-profiles-by-identity}

Dieses Widget verwendet ein Balkendiagramm, um die Gesamtanzahl der Profile zu veranschaulichen, die mit nur einer eindeutigen Kennung gekennzeichnet sind. Das Widget unterstützt bis zu fünf der am häufigsten vorkommenden Identitäten.

Bewegen Sie den Mauszeiger über die einzelnen Balken, um ein Dialogfeld mit der Gesamtanzahl der Profile für eine Identität aufzurufen.

![Die einzelnen Identitätsprofile nach Identitäts-Widget.](../images/profiles/single-identity-profiles-by-identity.png)

### [!UICONTROL Nicht segmentierte Profile] {#unsegmented-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofiles"
>title="Nicht segmentierte Profile"
>abstract="Dieses Widget stellt die Gesamtanzahl aller Profile bereit, die keinem Segment zugeordnet sind, und bietet die Möglichkeit zur Profilaktivierung in Ihrer gesamten Organisation."

Das Widget [!UICONTROL Nicht segmentierte Profile] gibt die Gesamtanzahl aller Profile an, die mit keinem Segment verbunden sind. Der generierte Wert gibt die zum Zeitpunkt der letzten Momentaufnahme korrekte Anzahl an und zeigt, wie viele Profile in Ihrer gesamten Organisation aktiviert werden können. Es zeigt auch die Möglichkeit an, Profile auszuschließen, die keinen angemessenen ROI liefern.

![Das Widget „Nicht segmentierte Profile“.](../images/profiles/unsegmented-profiles.png)

### [!UICONTROL Trendänderung von nicht segmentierten Profilen] {#unsegmented-profiles-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilestrend"
>title="Trend von nicht segmentierten Profilen"
>abstract="Dieses Widget bietet eine grafische Darstellung der Anzahl der Profile, die in einem bestimmten Zeitraum nicht mit einem Segment verbunden sind. Der Trend der Profile, die keinem Segment zugeordnet sind, kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden."

Die [!UICONTROL Trendänderung von nicht segmentierten Profilen] -Widget verwendet ein Liniendiagramm, um die Anzahl der Profile zu veranschaulichen, die seit der letzten täglichen Momentaufnahme hinzugefügt wurden und an kein Segment angehängt sind. Der Änderungstrend von Profilen, die keinem Segment zugeordnet sind, kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt. Die Anzahl der Profile wird auf der Y-Achse und die Zeit auf der X-Achse dargestellt.

![Das Trend-Widget für nicht segmentierte Profile ändert sich.](../images/profiles/unsegmented-profiles-change-trend.png)

### [!UICONTROL Nicht segmentierte Profile nach Identität] {#unsegmented-profiles-by-identity}

>[!NOTE]
>
>Das Widget Nicht segmentierte Profile nach Identität wird seit Oktober 2022 nicht mehr unterstützt und ist nicht mehr verfügbar.

<!-- 

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilesbyidentity"
>title="Unsegmented profiles by identity"
>abstract="This widget categorizes the total number of unsegmented profiles by their unique identifier."

The [!UICONTROL Unsegmented Profiles by Identity] widget categorizes the total number of unsegmented profiles by their unique identifier. The data is visualized in a bar chart for ease of comparison. 

![The Unsegmented Profiles by Identity widget.](../images/profiles/unsegmented-profiles-by-identity.png) -->

### [!UICONTROL Audiences] {#audiences}

Dieses Widget ermittelt die Gesamtzahl der Segmente, die entsprechend der ausgewählten Zusammenführungsrichtlinie, die auf Ihre Profildaten angewendet wird, aktiviert werden können.

Wählen Sie **[!UICONTROL Zielgruppen]** aus, um zum [!UICONTROL Segmente]-Dashboard und zur Registerkarte [!UICONTROL Durchsuchen] zu navigieren. Dort finden Sie eine Liste aller Segmentdefinitionen für Ihre Organisation.

![Das Zielgruppen-Widget.](../images/profiles/audiences.png)

<!-- https://jira.corp.adobe.com/browse/PLAT-115291 -->

<!-- * [[!UICONTROL Audiences change trend]](#audiences-change-trend) -->
<!-- ### [!UICONTROL Audiences change trend] {#audiences-change-trend}

This line graph widget visualizes the change in the total number of audiences each day, trending over time. The change in the number of audiences is dependent on the selected merge policy being applied to your profile data. The period of analysis is selected from the widget dropdown menu. The bar chart can be visualized over 30 days, 90 days, and 12-month periods.  

The visualization allows you to monitor the overall health of audiences within Adobe Experience Platform by understanding trends in the growth or decline of the total number of audiences. -->

<!-- ![The Audiences change trend widget.]() -->

### [!UICONTROL Der Bericht „Zielgruppenüberschneidung“] {#audience-overlap-report}

Dieses Widget enthält eine tabellarische Darstellung der Zielgruppenüberschneidungsdaten aus allen verfügbaren Segmenten, die nach Zusammenführungsrichtlinien gefiltert wurden. Für die Zusammenführungsrichtlinie, die oben im Bildschirm im Dropdown-Menü ausgewählt wird, wird eine Liste mit fünf Zielgruppen, sortiert von den höchsten bis zu den niedrigsten Überschneidungsprozentsätzen, bereitgestellt. Die beiden analysierten Segmente werden in den Spalten [!UICONTROL NAME SEGMENT A] und [!UICONTROL NAME SEGMENT B] aufgeführt. Die prozentuale Überschneidung wird in der dritten Spalte auf zwölf Dezimalstellen genau angegeben.

Der Bericht zur Zielgruppenüberschneidung hilft Ihnen beim Erstellen neuer, hochqualitativer Segmente. Durch die Beachtung hoher prozentualer Überschneidungen können Sie Zielgruppen unterdrücken und das Senden derselben Zielgruppe an verschiedene Ziele verhindern. Diese Daten helfen Ihnen auch dabei, verborgene Insights zu entdecken, die bei einer besseren Segmentierung hilfreich sein können. Eine geringe prozentuale Überschneidung hilft, eindeutige Profile zu finden, deren Kontaktierung Sie fortsetzen sollten.

Wählen Sie **[!UICONTROL Mehr anzeigen]** aus, um ein Vollbilddialogfeld zu öffnen, das mehr Daten zu Zielgruppenüberschneidungen enthält.

![Das Widget „Bericht Zielgruppenüberscheidung“ mit hervorgehobener Option „Mehr anzeigen“.](../images/profiles/profiles-audience-overlap-report.png)

Das Dialogfeld [!UICONTROL Bericht zur Zielgruppenüberschneidung] wird angezeigt. Dieses Dialogfeld kann bis zu 50 Zeilen mit Analysen zur Zielgruppenüberschneidung enthalten, die in sechs Spalten unterteilt sind. Wählen Sie das Einstellungssymbol (![Das Einstellungssymbol.](../images/profiles/settings-icon.png)) aus, um Spalten aus der Tabelle zu entfernen oder zur Tabelle hinzuzufügen.

![Das Dialogfeld mit dem Bericht zur Zielgruppenüberschneidung.](../images/profiles/profiles-audience-overlap-report-dialog.png)

>[!NOTE]
>
>Wählen Sie die Spaltenüberschrift **[!UICONTROL Überschneidung]** aus, um die Rangfolge der Ergebnisse vom höchsten zum niedrigsten bzw. vom niedrigsten zum höchsten zu ändern.

Um den gesamten Bericht im PDF-Format herunterzuladen, wählen Sie das Optionsmenü (**`...`**) und dann **[!UICONTROL Download]** aus.

![Das Dialogfeld mit dem Bericht zur Zielgruppenüberschneidung mit den Auslassungszeichen und der hervorgehobenen Download-Option.](../images/profiles/profiles-audience-overlap-report-dialog-download.png)

Wählen Sie eine Zeile aus dem Bericht aus, um ein Venn-Diagramm der Überschneidungsanalyse zu öffnen. Bewegen Sie den Mauszeiger über einen Abschnitt des Venn-Diagramms, um die Profilanzahl in einem Dialogfeld anzuzeigen.

![Das Dialogfeld „Bericht Zielgruppenüberschneidung“ mit Hervorhebung eines Venn-Diagramms und einer Zeile.](../images/profiles/profiles-audience-overlap-report-dialog-venn.png)

Wählen Sie **[!UICONTROL Schließen]** aus, um zum [!UICONTROL Profile]-Dashboard zurückzukehren.

### [!UICONTROL Audiences, die einem Zielstatus zugeordnet sind] {#audiences-mapped-to-destination-status}

Das Widget [!UICONTROL Zielgruppen, die dem Zielstatus zugeordnet sind] stellt in einer gemeinsamen Metrik die Gesamtzahl der zugeordneten und nicht zugeordneten Zielgruppen dar und veranschaulicht in einem Ringdiagramm den proportionalen Unterschied zwischen den beiden Zahlen. Die berechneten Zahlen hängen von der gewählten Zusammenführungsrichtlinie ab.

Wenn der Mauszeiger über den entsprechenden Abschnitt des Ringdiagramms bewegt wird, werden die separaten Zählungen für zugeordnete oder nicht zugeordnete Zielgruppen in einem Dialogfeld angezeigt.

![Das Widget „Zielgruppen, die dem Zielstatus zugeordnet sind“.](../images/profiles/audiences-mapped-to-destination-status.png)

### [!UICONTROL Audience-Größe] {#audiences-size}

Das Widget [!UICONTROL Zielgruppengröße] bietet eine zweispaltige Tabelle, in der bis zu 20 Segmente und die Gesamtzahl der in den einzelnen Segmenten enthaltenen Zielgruppen aufgelistet sind. Die Liste ist gemäß der Gesamtzahl der Zielgruppen von der höchsten zur niedrigsten sortiert. Die Gesamtgröße der Zielgruppen hängt von der angewendeten Zusammenführungsrichtlinie ab.

![Das Widget „Zielgruppengröße“.](../images/profiles/audiences-size.png)

Um umfassende Informationen zu einem Segment anzuzeigen, wählen Sie den entsprechenden Segmentnamen aus der bereitgestellten Liste aus, um zur [!UICONTROL Detailseite] des [!UICONTROL Segments] zu navigieren. Außerdem können Sie durch die Auswahl von **[!UICONTROL Alle Segmente anzeigen]** am Ende des Widgets zur Registerkarte [!UICONTROL Durchsuchen] von [!UICONTROL Segmenten] navigieren, um ein vorhandenes Segment zu finden.

![Das Widget „Zielgruppengröße“ mit Hervorhebung eines Segmentnamens und des Texts „Alle Segmente anzeigen“.](../images/profiles/audiences-size-view-all-segments.png)

Weitere Informationen zur Registerkarte [!UICONTROL Durchsuchen] von [[!UICONTROL Segmenten] finden Sie in der Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=de#browse).

### [!UICONTROL Zielgruppenüberschneidung nach Zusammenführungsrichtlinie] {#audience-overlap-by-merge-policy}

Dieses Widget verwendet ein Venn-Diagramm, um die Überschneidung zweier ausgewählter Segmente anzuzeigen. Die Zusammenführungsrichtlinie wird oben auf der Seite aus dem Dropdown-Menü „Übersicht“ ausgewählt und die zu analysierenden Segmente werden aus zwei Dropdown-Menüs im Widget ausgewählt. Die Gesamtzahl der in der entsprechenden Segmentdefinition enthaltenen Profile kann durch Bewegen des Mauszeigers über einen Kreis oder die Schnittmenge angezeigt werden.

Dieses Widget stellt die visuelle Überschneidung von Segmentdefinitionen dar und ermöglicht es Ihnen, die Segmentierungsstrategie zu optimieren, indem Sie die Ähnlichkeiten zwischen Ihren Segmentdefinitionen untersuchen.

![Das Profile-Dashboard der Platform-Benutzeroberfläche mit Hervorhebung des Dropdown-Menüs „Zusammenführungsrichtlinie“ und der Dropdown-Menüs der Widget-Segmente.](../images/profiles/audience-overlap-by-merge-policy.png)


<!-- ## (Beta) Profile efficacy widgets {#profile-efficacy-widgets}

>[!IMPORTANT]
>
>The profile efficacy widgets are currently in Beta and are not available to all users. The documentation and the functionality are subject to change.

Adobe provides multiple widgets to assess the completeness of the ingested profiles available for your data analysis. Each of the profile efficacy widgets can be filtered by the merge policy. To change the merge policy filter, select the[!UICONTROL Profiles using merge policy] dropdown and choose the appropriate policy from the available list.

To learn more about each of the profile efficacy widgets, select the name of a widget from the following list:

* [[!UICONTROL Attribute quality assessment]](#attributes-quality-assessment)
* [[!UICONTROL Profiles by completeness]](#profiles-by-completeness)
* [[!UICONTROL Profiles completeness trend]](#profiles-completeness-trend)

### (Beta) [!UICONTROL Attributes quality assessment] {#attributes-quality-assessment}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_attributesqualityassessment"
>title="Attributes quality assessment"
>abstract="This widget shows the completeness and cardinality of all profiles according to their attributes. Each row describes one attribute. The **Profiles** column provides the number of profiles that have this attribute and are filled with non-null values. The **Completeness** percentage is determined by the total number of profiles that have this attribute and are filled with non-null values divided by the total number of non-empty values in the profiles for that attribute. **Cardinality** provides the total number of unique non-null values of this attribute across all attributes."

The [!UICONTROL Attribute quality assessment] widget shows the completeness and cardinality of all profiles according to their attributes. The data is accurate to the last processing date. This information is presented as a table with four columns where each row in the table represents a single attribute.

| Column  | Description  |
|---|---|
| Attribute  | The name of the attribute.  |
| Profiles  | The number of profiles that have this attribute and are filled with non-null values.  |
| Completeness  | This percentage is determined by the total number of profiles that have this attribute and are filled with non-null values. The number is calculated by dividing the total number of profiles by the total number of non-empty values in the profiles for that attribute.  |
| Cardinality  | The total number of **unique** non-null values of this attribute. It is measured across all profiles. |

![The attributes quality assessment widget](../images/profiles/attributes-quality-assessment.png)

### (Beta) [!UICONTROL Profiles by completeness] {#profiles-by-completeness}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbycompleteness"
>title="Profiles by completeness"
>abstract="The donut chart displays the percentage of profile attributes that are filled with non-null values among all observed attributes. It illustrates the proportion of profiles that are of high, medium, or low completeness. High completeness profiles have more than 70% of their attributes filled. Medium completeness profiles have between 30% and 70% of their attributes filled. Low completeness profiles have less than 30% of their attributes filled."

The [!UICONTROL Profiles by completeness] widget creates a donut chart of profile completeness since the last processing date. The completeness of a profile is measured by the percentage of attributes that are filled with non-null values among all observed attributes.

This widget shows the proportion of profiles that are of high, medium, or low completeness. By default, there are three levels of completeness configured: 

* High completeness: Profiles have more than 70% of their attributes filled. 
* Medium completeness: Profiles have between 30% and 70% of their attributes filled. 
* Low completeness: Profiles have less than 30% of their attributes filled. 

![The profiles by completeness widget](../images/profiles/profiles-by-completeness.png)

### (Beta) [!UICONTROL Profiles completeness trend] {#profiles-completeness-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescompletenesstrend"
>title="Profiles completeness trend"
>abstract="This widget creates a stacked area chart to depict the trend of profile completeness over time. Completeness is measured by the percentage of attributes that are filled with non-null values among all observed attributes."

This widget creates a stacked area chart to depict the trend of profile completeness over time. Completeness is measured by the percentage of attributes filled with non-null values among all observed attributes. It categorizes the profile completeness as high, medium, or low completeness since the last processing date.

The x-axis represents time, the y-axis represents the number of profiles, and the colors represent the three levels of profile completeness. 

The three levels of completeness are:

* High completeness: Profiles have more than 70% of attributes filled. 
* Medium completeness: Profiles have less than 70% and more than 30% of attributes filled. 
* Low completeness: Profiles have less than 30% of attributes filled.

![The profiles completeness trend widget](../images/profiles/profiles-completeness-trend.png) -->

## Nächste Schritte

Wenn Sie mit diesem Dokument fertig sind, sollten Sie in der Lage sein, das Profile-Dashboard zu finden und die in den verfügbaren Widgets angezeigten Metriken zu verstehen. Weitere Informationen zum Arbeiten mit [!DNL Profile] Daten in der Experience Platform-Benutzeroberfläche, siehe [Handbuch zur Benutzeroberfläche des Echtzeit-Kundenprofils](../../profile/ui/user-guide.md).
