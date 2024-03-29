---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Benutzeroberfläche;Benutzeroberfläche;Anpassung;Profil-Dashboard;Dashboard
title: Handbuch zum Profile-Dashboard
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zu den Echtzeit-Kundenprofildaten Ihres Unternehmens anzeigen können.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 78cf435f506a21ddd2348642c07380ad810bc693
workflow-type: tm+mt
source-wordcount: '4996'
ht-degree: 48%

---

# [!UICONTROL Profile]-Dashboard

Die Benutzeroberfläche von Adobe Experience Platform verfügt über ein Dashboard, über das Sie wichtige Informationen über Ihre [!DNL Real-Time Customer Profile]-Daten anzeigen können, die während eines täglichen Schnappschusses erfasst wurden. In diesem Handbuch wird beschrieben, wie Sie auf das Profile-Dashboard in der Benutzeroberfläche zugreifen und mit ihm arbeiten können. Außerdem erhalten Sie Informationen zu den im Dashboard angezeigten Metriken.

Siehe Abschnitt [Handbuch zur Benutzeroberfläche des Echtzeit-Kundenprofils](../../profile/ui/user-guide.md) für einen Überblick über die Profilfunktionen in der Experience Platform-Benutzeroberfläche.

## Daten des Profile-Dashboards

Im Dashboard „Profile“ wird eine Momentaufnahme der Attributdaten (Datensatzdaten) wiedergegeben, die sich für Ihre Organisation im Profilspeicher in Experience Platform befinden. Die Momentaufnahme enthält keine Ereignisdaten (Zeitreihendaten).

Die Attributdaten in der Momentaufnahme zeigen die Daten exakt so an, wie sie zum Zeitpunkt der Momentaufnahme vorgefunden werden. Das heißt, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten und das Profile-Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme der Momentaufnahme an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn die nächste Momentaufnahme erstellt wird.

## Dashboard &quot;Profile&quot;durchsuchen {#explore-dashboard}

Um in der Platform-Benutzeroberfläche zum Profile-Dashboard zu navigieren, wählen Sie **[!UICONTROL Profile]** in der linken Leiste und dann die Registerkarte **[!UICONTROL Übersicht]** aus, um das Dashboard anzuzeigen.

>[!NOTE]
>
>Wenn Platform neu für Ihr Unternehmen ist und noch keine aktiven Profildatensätze oder Zusammenführungsrichtlinien erstellt hat, ist das Profile-Dashboard nicht zu sehen. Stattdessen wird die [!UICONTROL Übersicht] enthält Links und Dokumentation, die Ihnen bei den ersten Schritten mit dem Echtzeit-Kundenprofil helfen.

![Das Dashboard Experience Platform-Profile mit hervorgehobenen Profilen und Überblick.](../images/profiles/dashboard-overview.png)

### Ändern des Dashboards &quot;Profile&quot; {#modify-dashboard}

Sie können das Erscheinungsbild des Profile-Dashboards ändern, indem Sie **[!UICONTROL Dashboard modifizieren]** auswählen. Sie können Widgets aus dem Dashboard verschieben, hinzufügen, ändern und entfernen sowie auf die **[!UICONTROL Widget-Bibliothek]** , um verfügbare Widgets zu erkunden und benutzerdefinierte Widgets für Ihre Organisation zu erstellen.

Weitere Informationen finden Sie im Abschnitt [Ändern von Dashboards](../customize/modify.md) und [Übersicht über die Widget-Bibliothek](../customize/widget-library.md) Dokumentation.

### Hinzufügen von Widgets {#add-widget}

Wählen Sie **[!UICONTROL Widget hinzufügen]** aus, um zur Widget-Bibliothek zu navigieren und eine Liste der verfügbaren Widgets anzuzeigen, die Sie Ihrem Dashboard hinzufügen können.

![Die Übersicht über das Profile-Dashboard mit der hervorgehobenen Option „Widget hinzufügen“.](../images/profiles/profiles-overview-add-widget.png)

In der Widget-Bibliothek können Sie die Auswahl von Standard- und benutzerdefinierten Zielgruppen-Widgets durchsuchen. Informationen zum Hinzufügen von Widgets finden Sie in der Widget-Bibliothek-Dokumentation zum [Hinzufügen eines Widget](../customize/widget-library.md#add-widgets).

### SQL anzeigen {#view-sql}

Sie können die SQL, die die in Ihrem Dashboard visualisierten Einblicke generiert, mit einem Umschalter im [!UICONTROL Übersicht] Arbeitsbereich. Sie können sich die SQL Ihrer vorhandenen Einblicke inspirieren lassen, um neue Abfragen zu erstellen, die anhand Ihrer geschäftlichen Anforderungen eindeutige Einblicke aus Platform-Daten gewinnen. Weitere Informationen zu dieser Funktion finden Sie unter [Handbuch zur SQL-Benutzeroberfläche](../view-sql.md).

<!-- ## (Beta) Profile efficacy insights {#profile-efficacy-insights}

>[!IMPORTANT]
>
>The profile efficacy insight functionality is currently in beta and are not available to all users. The documentation and the functionality are subject to change.

The [!UICONTROL Efficacy] tab provides metrics on the quality and completeness of your profile data through the use of profile efficacy widgets. These widgets illustrate at a glance the composition of your profiles, trends in completeness over time, and assessments on the quality of your profile data.

![The profile efficacy dashboard.](../images/profiles/attributes-quality-assessment.png)

See the [profile efficacy widgets section](#profile-efficacy-widgets) for more information on the widgets currently available.

The layout of this dashboard is also customizable by selecting [**[!UICONTROL Modify dashboard]**](../customize/modify.md) from the [!UICONTROL Overview] tab. -->

## Profile durchsuchen {#browse-profiles}

Mit der Registerkarte [!UICONTROL Durchsuchen] können Sie die schreibgeschützten Profile Ihrer Organisation durchsuchen und anzeigen. Von hier aus können Sie wichtige Informationen aus dem Profil zu ihren Voreinstellungen, vergangenen Ereignissen, Interaktionen und Zielgruppen sehen.

## Profildetails {#profile-details}

So öffnen Sie die [!UICONTROL Profile] [!UICONTROL Detail] Arbeitsbereich auswählen [!UICONTROL Profil-ID] aus der Liste.

![Die Registerkarte &quot;Profile Browse&quot;, auf der die Profil-ID hervorgehoben ist.](../images/profiles/profile-id.png)

Die [!UICONTROL Profile] [!UICONTROL Detail] Workspace zeigt mehrere vorkonfigurierte Widgets an, die Informationen zu diesem Profil enthalten. Anhand dieser Informationen können Sie die wichtigsten Attribute des Profils auf einen Blick nachvollziehen. Sie können auch Ihre [!UICONTROL Profile] [!UICONTROL Detail] Arbeitsbereich durch Erstellen eigener Widgets. Siehe Abschnitt zu [Hinzufügen von Widgets](#add-widgets) für weitere Details.

![Die [!UICONTROL Profile] [!UICONTROL Detail] Arbeitsbereich mit [!UICONTROL Detail] hervorgehoben.](../images/profiles/profile-details-workspace.png)

### Profildetails-Widgets {#widgets}

Die vorkonfigurierten Profildetails-Widgets lauten wie folgt:

#### Kundenprofil {#customer-profile}

Die [!UICONTROL Kundenprofil] Widget zeigt den Vor- und Nachnamen des mit dem Profil verknüpften Benutzers sowie dessen [!UICONTROL Profil-ID]. Eine Profil-ID ist eine automatisch generierte Kennung, die mit einem Identitätstyp verknüpft ist und ein Profil darstellt. Weiterführende Informationen zu Identitäten und Identitäts-Namespaces finden Sie unter [Identitäten – Übersicht](../../rtcdp/profile/identities-overview.md).

![Das Widget Kundenprofil .](../images/profiles/customer-profile.png)

#### Grundlegende Attribute {#basic-attributes}

Die [!UICONTROL Grundlegende Attribute] Widget zeigt die am häufigsten verwendeten Attribute an, die zum Definieren eines einzelnen Profils verwendet werden.

![Das Widget Grundlegende Attribute .](../images/profiles/basic-attributes.png)

#### Verknüpfte Identitäten {#linked-identities}

Die [!UICONTROL Verknüpfte Identitäten] -Widget zeigt alle anderen Identitäten an, die mit dem Profil verknüpft sind.

So zeigen Sie die Identitätsdetails des Profils tiefer an und navigieren zur [!UICONTROL Identitäten] Arbeitsbereich auswählen **[!UICONTROL Identitätsdiagramm anzeigen]**.

![Das Widget Verknüpfte Identitäten .](../images/profiles/linked-identities.png)

#### Kanaleinstellungen {#channel-preferences}

Die [!UICONTROL Kanaleinstellungen] Widget zeigt die Kommunikationskanäle an, von denen der Benutzer dem Empfang von Nachrichten zugestimmt hat. Ein Häkchen kennzeichnet jeden Kanal, von dem der Benutzer dem Empfang von Nachrichten zugestimmt hat.

<!-- image needs a blue tick added below -->

![Das Widget Kanalvoreinstellungen .](../images/profiles/channel-preferences.png)

Die Zustimmung des Kunden und die Kontakteinstellungen sind komplexe Themen. Um zu erfahren, wie Zustimmungs- und Kontextvoreinstellungen unter Experience Platform erfasst, verarbeitet und gefiltert werden können, sollten Sie die folgenden Dokumente lesen:

* Informationen zu den für das Schema erforderlichen Feldergruppen [Einverständnisdaten gemäß dem Adobe-Standard erfassen](../../landing/governance-privacy-security/consent/adobe/overview.md), lesen Sie die Dokumentation zu diesen Profilaktivierten Schemafeldgruppen.
   * [[!UICONTROL Einverständnis und Präferenzdetails]](../../xdm/field-groups/profile/consents.md)
   * [[!UICONTROL IdentityMap]](../../xdm/field-groups/profile/identitymap.md) (erforderlich, wenn das Platform Web oder Mobile SDK zum Senden von Zustimmungssignalen verwendet wird)
* Informationen zur Verarbeitung von Einwilligungs- und Präferenzdaten von Kunden mithilfe des Adobe-Standards finden Sie in der Übersicht unter [Zustimmungsverarbeitung in Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md).
* Eine kombinierte Data Governance- und Einverständnisrichtlinie kann verwendet werden, um Profile nach Segmentierung basierend auf ihren Zustimmungseinstellungen und Ihren festgelegten Organisationsregeln zu filtern. Informationen zum Erstellen und Verwenden dieser kombinierten Richtlinien finden Sie im Benutzerhandbuch zu [Richtlinien zur Datennutzung verwalten](../../data-governance/policies/user-guide.md#combine-policies).

### Hinzufügen von Widgets {#add-widgets}

So fügen Sie Ihren [!UICONTROL Profile] [!UICONTROL Detail] Arbeitsbereich auswählen **[!UICONTROL Profildetails anpassen]**.

![Der Arbeitsbereich &quot;Profildetails&quot;mit [!UICONTROL Profildetails anpassen] hervorgehoben.](../images/profiles/customize-profile-details.png)

Sie können den Arbeitsbereich jetzt bearbeiten, indem Sie die Größe der Widgets ändern oder sie neu anordnen. Auswählen **[!UICONTROL Widget hinzufügen]** , um ein Widget mit benutzerdefinierten Attributen zu erstellen.

![Die Profile [!UICONTROL Detail] Arbeitsbereich mit [!UICONTROL Widget hinzufügen] hervorgehoben.](../images/profiles/add-widget.png)

Der Ersteller des Widgets wird angezeigt. Geben Sie einen beschreibenden Namen für Ihr Widget im [!UICONTROL Kartentitel] Textfeld und wählen Sie **[!UICONTROL Hinzufügen von Attributen]**.

![Die Arbeitsfläche des Widget-Erstellers mit der [!UICONTROL Kartentitel] und [!UICONTROL Hinzufügen von Attributen] hervorgehoben.](../images/profiles/widget-creator.png)

Es wird ein Dialogfeld mit einer Visualisierung des Vereinigungsschemas des Profils angezeigt. Verwenden Sie das Suchfeld oder scrollen Sie nach den Attributen, über die Sie mit Ihrem Widget Berichte erstellen möchten. Aktivieren Sie das Kontrollkästchen für alle Attribute, die Sie einbeziehen möchten. Auswählen **[!UICONTROL Auswählen]** , um den Erstellungs-Workflow fortzusetzen.

>[!TIP]
>
>Eine Auswahl des Kontrollkästchens der obersten Ebene umfasst alle untergeordneten Elemente.

![Das Vereinigungsschema-Diagramm mit dem Kontrollkästchen &quot;Treueattribut&quot;und [!UICONTROL Auswählen] hervorgehoben.](../images/profiles/union-schema-attributes.png)

Auf der Arbeitsfläche wird eine Vorschau des abgeschlossenen Widgets angezeigt. Sobald Sie mit den von Ihnen ausgewählten Attributen zufrieden sind, wählen Sie **[!UICONTROL Speichern]** um Ihre Auswahl zu bestätigen und zur [!UICONTROL Profile] [!UICONTROL Detail] Arbeitsbereich. Das neu erstellte Widget ist jetzt im Arbeitsbereich sichtbar.

![Die Arbeitsfläche des Widget-Erstellers mit hervorgehobenem Speichern und Anzeige der Widget-Vorschau.](../images/profiles/widget-preview.png)

## Zusammenführungsrichtlinien {#merge-policies}

Die im Dashboard &quot;Profile&quot;angezeigten Metriken basieren auf Zusammenführungsrichtlinien, die auf Ihre Echtzeit-Kundenprofildaten angewendet werden. Wenn Daten aus mehreren Quellen zusammengeführt werden, um das Kundenprofil zu erstellen, können die Daten widersprüchliche Werte enthalten. Beispielsweise kann ein Datensatz einen Kunden als „unverheiratet“ auflisten, während ein anderer Datensatz den Kunden als „verheiratet“ führt. Mithilfe der Zusammenführungsrichtlinie wird bestimmt, welche Daten als Teil des Profils priorisiert und angezeigt werden sollen.

Weitere Informationen zu Zusammenführungsrichtlinien, einschließlich der Erstellung, Bearbeitung und Deklaration einer standardmäßigen Zusammenführungsrichtlinie für Ihre Organisation, finden Sie im Abschnitt [Zusammenführungsrichtlinien – Übersicht](../../profile/merge-policies/overview.md).

Das Dashboard wählt automatisch eine zu verwendende Zusammenführungsrichtlinie aus. Die angewendete Zusammenführungsrichtlinie kann über das Dropdown-Menü neben dem Namen der Zusammenführungsrichtlinie geändert werden.

>[!NOTE]
>
>Im Dropdown-Menü werden nur Zusammenführungsrichtlinien angezeigt, die das `_xdm.context.profile`-Schema verwenden. Wenn Ihr Unternehmen jedoch mehrere Zusammenführungsrichtlinien erstellt hat, müssen Sie möglicherweise scrollen, um die vollständige Liste der verfügbaren Zusammenführungsrichtlinien zu sehen.

![Die Registerkarte „Profile – Übersicht“ mit hervorgehobenem Dropdown-Menü „Zusammenführungsrichtlinie“.](../images/profiles/select-merge-policy.png)

## Vereinigungsschemata

Das Dashboard [!UICONTROL Vereinigungsschema] zeigt das Vereinigungsschema für eine bestimmte XDM-Klasse an. Durch Auswahl des Dropdown-Menüs **[!UICONTROL Klasse]** können Sie die Vereinigungsschemata für verschiedene XDM-Klassen anzeigen.

Vereinigungsschemata bestehen aus mehreren Schemata, die dieselbe Klasse haben und für Profil aktiviert wurden. Damit haben Sie die Möglichkeit, in einer einzigen Ansicht alle Felder zu sehen, die in allen Schemata derselben Klasse enthalten sind.

Weitere Informationen zu [Anzeigen von Vereinigungsschemas in der Platform-Benutzeroberfläche](../../profile/ui/union-schema.md#view-union-schemas), siehe Handbuch zur Benutzeroberfläche des Vereinigungsschemas .

## Widgets und Metriken

Das Dashboard besteht aus Widgets, die schreibgeschützte Metriken sind und wichtige Informationen zu Ihren Profildaten enthalten.

Datum und Uhrzeit des letzten Schnappschusses werden oben in der Registerkarte [!UICONTROL Übersicht] neben dem Dropdown-Menü „Zusammenführungsrichtlinie“ angezeigt. Alle Widget-Daten sind zum Stand dieses Datums und dieser Uhrzeit korrekt. Der Zeitstempel der Momentaufnahme wird im UTC-Format angegeben, nicht in der Zeitzone der jeweiligen Person oder Organisation.

![Die Registerkarte „Profile-Dashboard – Übersicht“ mit hervorgehobenem Zeitstempel des letzten Schnappschusses.](../images/profiles/snapshot-timestamp.png)

## Standard-Widgets {#default-widgets}

Für alle neuen Instanzen von Adobe Experience Platform wird ein standardmäßiges Widget-Load-out bereitgestellt, in dem die neuesten verfügbaren Einblicke aus Ihren Daten hervorgehoben werden. Die folgenden Widgets werden von Anfang an in Ihrer Segmentansicht vorkonfiguriert. Ausführliche Informationen zum Zweck und zur Funktion der Widgets finden Sie unten.

* [[!UICONTROL Anzahl der Profile]](#profile-count)
* [[!UICONTROL Änderung der Profilanzahl]](#profile-count-change)
* [[!UICONTROL Trend der Änderung der Profilanzahl]](#profiles-count-change-trend)
* [[!UICONTROL Profile nach Identität]](#profiles-by-identity)
* [[!UICONTROL Identitätsüberschneidung]](#identity-overlap)

>[!NOTE]
>
>Ab dem 26. Juli 2023 wird die [!UICONTROL Profile], [!UICONTROL Zielgruppen], und [!UICONTROL Ziele] Die Übersichts-Dashboards wurden für alle Benutzer, die ihre Ansichten in den letzten sechs Monaten nicht geändert haben, auf ein neues standardmäßiges Widget-Load-out zurückgesetzt. Weitere Informationen finden Sie in der Dokumentation unter [Ziele](./destinations.md#default-widgets) und [Zielgruppen](./audiences.md#default-widgets) Standard-Widget-Abschnitte für Details darüber, welche Widgets als Teil der standardmäßigen Widget-Ladevorgänge einbezogen werden. Sie können Ihre Dashboard-Widgets weiterhin wie bisher anpassen.

## Kunden-KI-Widgets {#customer-ai-profiles-widgets}

Customer AI wird verwendet, um für einzelne Profile skaliert benutzerdefinierte Tendenzwerte wie Abwanderung und Konversion zu berechnen. Customer AI analysiert dazu vorhandene Erlebnisereignisdaten von Verbrauchern, um sie vorherzusagen **Tendenzwerte für Abwanderung oder Konversion**. Diese hochpräzisen kundenspezifischen Tendenzmodelle ermöglichen eine präzisere Segmentierung und Targeting. Die [Verteilung der Punktzahl](#customer-ai-distribution-of-scores) und [Bewertungszusammenfassung](#customer-ai-scoring-summary) Einblicke zeigen die Aufteilung in Ihrer Zielgruppe. Sie heben hervor, welche Profile die hohe/niedrige/mittlere Tendenz aufweisen und wie sie über Ihre Profilzahlen verteilt sind.

* [[!UICONTROL Kunden-KI – Bewertungszusammenfassung]](#customer-ai-scoring-summary)
* [[!UICONTROL Kunden-KI – Verteilung von Bewertungen]](#customer-ai-distribution-of-scores)

### [!UICONTROL Kunden-KI – Verteilung von Bewertungen] {#customer-ai-distribution-of-scores}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_distributionOfScores"
>title="Verteilung der Scores"
>abstract="Dieses Widget visualisiert die Verteilung der Gesamtanzahl der Profile anhand ihrer Tendenzwerte in Schritten von fünf Prozent. Die Verteilung der Profilanzahl wird durch das KI-Modell und die ausgewählte Zusammenführungsrichtlinie bestimmt. Sie können das KI-Modell im Dropdown-Menü unter dem Widget-Titel ändern."

Die [!UICONTROL Customer AI-Verteilung von Bewertungen] Widget kategorisiert die Gesamtanzahl der Profile nach ihren Tendenzwerten. Die Verteilung der Profilanzahl wird durch das AI-Modell und die ausgewählte Zusammenführungsrichtlinie bestimmt und dann in fünfprozentigen Schritten visualisiert, die ihre Neigung angeben. Die Anzahl der Profile wird entlang der Y-Achse angegeben und die Tendenzwerte werden entlang der X-Achse angegeben.

>[!NOTE]
>
>Wenn es sich bei der Visualisierung um eine Konversion-Tendenzbewertung handelt, werden die hohen Werte grün und die niedrigen Punkte rot angezeigt. Wenn Sie die Abwanderungsneigung vorhersagen, wird diese gespiegelt, die hohen Werte sind rot und die niedrigen Werte grün. Der mittlere Eimer bleibt gelb, unabhängig vom gewählten Tendenztyp.

Das AI-Modell, das die Tendenzwerte bestimmt, wird aus der Dropdown-Auswahl unter dem Widget-Titel ausgewählt. Das Dropdown-Menü enthält eine Liste aller konfigurierten Customer AI-Modelle. Wählen Sie aus der Liste der verfügbaren Modelle das passende KI-Modell für Ihre Analyse aus. Wenn kein Customer AI-Modell verfügbar ist, werden Sie durch eine Meldung im Widget angewiesen, mindestens ein Customer AI-Modell zu konfigurieren. Außerdem wird ein Hyperlink zur Konfigurationsseite des Customer AI-Modells bereitgestellt. Anweisungen finden Sie in der Dokumentation zu [Konfigurieren einer Customer AI-Instanz](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>Wählen Sie das Dropdown-Menü direkt unter dem Tab Übersicht aus, um die Zusammenführungsrichtlinie zu ändern, die bestimmt, welche Profile in die Analyse aufgenommen werden. Siehe Abschnitt zu [Zusammenführungsrichtlinien](#merge-policies) für eine kurze Beschreibung oder [Zusammenführungsrichtlinienübersicht](../../profile/merge-policies/overview.md) für weitere Details.

Um zur detaillierten Insight-Seite für das ausgewählte Customer AI-Modell zu navigieren, wählen Sie **[!UICONTROL Modelldetails anzeigen]**.

![Das Dashboard &quot;Experience Platform-Zielgruppen&quot;mit dem [!UICONTROL Customer AI-Verteilung von Bewertungen] Widget und [!UICONTROL Modelldetails anzeigen] hervorgehoben.](../images/segments/customer-ai-distribution-of-scores.png)

Die Seite mit detaillierten Modelleinblicken wird angezeigt.

![Die Einblicke-Seite für die Customer AI.](../images/profiles/customer-ai-insights-page.png)

Weitere Informationen zu Customer AI finden Sie im [Leitfaden zur Benutzeroberfläche für Einblicke](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

### [!UICONTROL Kunden-KI – Bewertungszusammenfassung] {#customer-ai-scoring-summary}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_scoringSummary"
>title="Bewertungszusammenfassung"
>abstract="Dieses Widget zeigt die Gesamtzahl der bewerteten Profile und kategorisiert sie in hohe, mittlere und niedrige Tendenz. Das Ringdiagramm zeigt die proportionale Zusammensetzung der Gesamtprofile über eine hohe, mittlere und niedrige Tendenz hinweg."

Dieses Widget zeigt die Gesamtzahl der bewerteten Profile und kategorisiert sie in Behälter mit hoher, mittlerer und niedriger Neigung als grün, gelb und rot. Ein Ringdiagramm veranschaulicht die proportionale Zusammensetzung von Profilen zwischen hohen, mittleren und niedrigen Tendenzen. Ein Profil ist qualifiziert für eine hohe Tendenz bei über 75, eine mittlere Neigung zwischen 25 und 74 und eine niedrige Tendenz unter 24. Eine Legende zeigt den Farbcode und die Schwellen der Eigenschaften an. Profilzahlen für die Eigenschaften &quot;Hoch&quot;, &quot;Mittel&quot;und &quot;Niedrig&quot;werden in einem Dialogfeld angezeigt, wenn der Cursor den Mauszeiger über den entsprechenden Abschnitt des Ringdiagramms bewegt.

>[!NOTE]
>
>Wenn es sich bei der Visualisierung um eine Konversion-Tendenzbewertung handelt, werden die hohen Werte grün und die niedrigen Punkte rot angezeigt. Wenn Sie die Abwanderungsneigung vorhersagen, wird diese gespiegelt, die hohen Werte sind rot und die niedrigen Werte grün. Der mittlere Eimer bleibt gelb, unabhängig vom gewählten Tendenztyp.

Das Dropdown-Menü unter dem Widget-Titel enthält eine Liste aller konfigurierten Customer AI-Modelle. Wählen Sie aus der Liste der verfügbaren Modelle das passende KI-Modell für Ihre Analyse aus. Wenn kein Customer AI-Modell verfügbar ist, werden Sie durch eine Meldung im Widget angewiesen, mindestens ein Customer AI-Modell zu konfigurieren. Außerdem wird ein Hyperlink zur Konfigurationsseite des Customer AI-Modells bereitgestellt. Siehe die Dokumentation unter [Konfigurieren einer Customer AI-Instanz](../../intelligent-services/customer-ai/user-guide/configure.md) für detaillierte Anweisungen.

>[!NOTE]
>
>Die Gesamtzahl der berechneten Profile hängt von der gewählten Zusammenführungsrichtlinie ab. Um die verwendete Zusammenführungsrichtlinie zu ändern, wählen Sie das Dropdown-Menü direkt unter der Registerkarte Übersicht aus. Siehe Abschnitt zu [Zusammenführungsrichtlinien](#merge-policies) für eine kurze Beschreibung oder [Zusammenführungsrichtlinienübersicht](../../profile/merge-policies/overview.md) für weitere Details.

![Das Dashboard Experience Platform-Zielgruppen mit dem Widget Customer AI-Bewertungszusammenfassung wurde hervorgehoben.](../images/segments/customer-ai-scoring-summary.png)

Um zur detaillierten Insight-Seite für das ausgewählte Customer AI-Modell zu navigieren, wählen Sie **[!UICONTROL Modelldetails anzeigen]**. Weitere Informationen zu Customer AI finden Sie im [Leitfaden zur Benutzeroberfläche für Einblicke](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

## Standard-Widgets {#standard-widgets}

Adobe bietet mehrere Standard-Widgets, mit denen Sie verschiedene Metriken im Zusammenhang mit Ihren Profildaten visualisieren können. Über die [!UICONTROL Widget-Bibliothek] können Sie auch benutzerdefinierte Widgets erstellen und für Ihre Organisation freigeben. Um mehr über das Erstellen benutzerdefinierter Widgets zu erfahren, lesen Sie zunächst den Abschnitt [Übersicht über die Widget-Bibliothek](../customize/widget-library.md).

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
* [[!UICONTROL Änderungs-Trend bei nicht segmentierten Profilen]](#unsegmented-profiles-change-trend)
* [[!UICONTROL Nicht segmentierte Profile nach Identität]](#unsegmented-profiles-by-identity)
* [[!UICONTROL Zielgruppen]](#audiences)
* [[!UICONTROL Zielgruppen, die einem Zielstatus zugeordnet sind]](#audiences-mapped-to-destination-status)
* [[!UICONTROL Zielgruppen-Größe]](#audiences-size)
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
>Das Widget [!UICONTROL Profilanzahl] kann aus mehreren Gründen eine andere Zahl anzeigen als die Registerkarte [!UICONTROL Durchsuchen] im Abschnitt [!UICONTROL Profile] der Benutzeroberfläche. Der häufigste Grund für diesen Unterschied besteht darin, dass die [!UICONTROL Durchsuchen] -Registerkarte gibt die Gesamtzahl der zusammengeführten Profile basierend auf der standardmäßigen Zusammenführungsrichtlinie Ihres Unternehmens an, während die Variable [!UICONTROL Profilanzahl] -Widget verweist auf die Gesamtzahl der zusammengeführten Profile basierend auf der Zusammenführungsrichtlinie, die Sie im Dashboard angezeigt haben.
>
>Ein weiterer häufiger Grund besteht darin, dass der Dashboard-Schnappschuss und der Beispielvorgang für die Registerkarte [!UICONTROL Durchsuchen] zu unterschiedlichen Zeiten ausgeführt wird. Sie können sehen, wann das Widget [!UICONTROL Profilanzahl] zuletzt aktualisiert wurde, indem Sie den Zeitstempel im Widget überprüfen. Weitere Informationen dazu, wie der Beispielauftrag im [!UICONTROL Durchsuchen] Registerkarte, siehe [Abschnitt zur Profilanzahl im Handbuch zur Benutzeroberfläche des Echtzeit-Kundenprofils](../../profile/ui/user-guide.md#profile-count).

![Das Dashboard Experience Platform-Profile mit dem Widget Profilanzahl wird hervorgehoben.](../images/profiles/profile-count.png)

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
>Das Widget [!UICONTROL Änderung der Profilanzahl] enthält die Anzahl der hinzugefügten Profile, die **nach** der ersten Profilaufnahme und der Einrichtung des Profilspeichers hinzugefügt wurden. Mit anderen Worten: Wenn Ihre Organisation den Profilspeicher einrichtet und am ersten Tag 4.000.000 aufnimmt, ist das Dashboard innerhalb von 24 Stunden verfügbar, jedoch wird im Widget [!UICONTROL Änderung der Profilanzahl] 0 angezeigt. Diese Zählmethode wird durchgeführt, um eine Spitze zu vermeiden, die mit der anfänglichen Aufnahme von Profilen in das System verbunden ist. In den nächsten 30 Tagen nimmt Ihre Organisation weitere 1.000.000 Profile in den Profilspeicher auf. Wenn der nächste Schnappschuss erstellt wird, zeigt das Widget [!UICONTROL Änderung der Profilanzahl] insgesamt 1.000.000 hinzugefügte Profile an, während das Widget [!UICONTROL Profilanzahl] insgesamt 5.000.000 Profile anzeigt.

![Das Profile-Dashboard der Platform-Benutzeroberfläche mit dem hervorgehobenen Widget „Änderung der Profilanzahl“.](../images/profiles/profile-count-change.png)

### [!UICONTROL Trend der Änderung der Profilanzahl] {#profiles-count-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesaddedtrend"
>title="Trend der Änderung der Profilanzahl"
>abstract="Dieses Widget zeigt die Zahl der zusammengeführten Profile an, die in den letzten 30 Tagen, 90 Tagen oder 12 Monaten täglich zum Profilspeicher hinzugefügt wurden. Die Zahl hängt auch von der ausgewählten Zusammenführungsrichtlinie ab, die auf Ihre Profildaten angewendet wird."

Das Widget **[!UICONTROL Trend der Änderung der Profilanzahl]** zeigt die Gesamtzahl der zusammengeführten Profile an, die in den letzten 30 Tagen, 90 Tagen oder 12 Monaten täglich zum Profilspeicher hinzugefügt wurden. Diese Zahl wird jeden Tag aktualisiert, wenn der Schnappschuss erstellt wird. Wenn Sie also Profile in Platform aufnehmen, wird die Anzahl der Profile erst beim nächsten Schnappschuss angezeigt. Die Anzahl der hinzugefügten Profile ist das Ergebnis der ausgewählten Zusammenführungsrichtlinie, die auf Ihre Profildaten angewendet wird, um Profilfragmente zusammenzuführen und so für jede Person ein Profil zu erstellen.

Weitere Informationen finden Sie im Abschnitt [Abschnitt zu Zusammenführungsrichtlinien weiter oben in diesem Dokument](#merge-policies).

Das Widget **[!UICONTROL Trend der Änderung der Profilanzahl]** verfügt oben rechts im Widget über eine Schaltfläche für Beschriftungen. Um das Dialogfeld für automatische Beschriftungen zu öffnen, wählen Sie **[!UICONTROL Untertitel]**.

![Die Registerkarte „Profilübersicht“ mit dem Widget „Trend der Änderung der Profilanzahl“ und der hervorgehobenen Schaltfläche „Beschriftungen“.](../images/profiles/profiles-count-change-trend-captions.png)

Ein Modell für maschinelles Lernen generiert automatisch Beschriftungen zur Beschreibung der wichtigsten Trends und Ereignisse, indem es das Diagramm und die Daten analysiert. Anmerkungen werden dem Diagramm basierend auf den Beschriftungen hinzugefügt. Wählen Sie eine Beschriftung aus, um sich auf die zugehörige Anmerkung zu konzentrieren.

![Das Dialogfeld für automatische Beschriftungen für das Widget „Trend der Änderung der Profilanzahl“.](../images/profiles/profiles-added-trends-automatic-captions-dialog-with-annotation.png)

### [!UICONTROL Trend der Änderung der Profilanzahl nach Identität] {#profiles-count-change-trend-by-identity}

<!-- This widget uses a line graph to illustrate the change in number of profiles filtered by a chosen source identity and merge policy. -->

Dieses Widget filtert die Profilanzahl auf der Grundlage einer ausgewählten Quellidentität und führt die Richtlinie zusammen und veranschaulicht dann die Änderung der Anzahl für verschiedene Zeiträume mithilfe eines Liniendiagramms. Die Zusammenführungsrichtlinie wird oben auf der Seite aus dem Dropdown-Menü &quot;Übersicht&quot;ausgewählt, die Quellidentität und der Zeitraum werden aus den Widget-Dropdown-Menüs ausgewählt. Der Trend kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden.

Dieses Widget hilft Ihnen bei der Verwaltung Ihrer Zielaktivierung, indem es das Wachstumsmuster der Profile darstellt, die nach der entsprechenden Identität gefiltert wurden.

![Der Trend der Veränderung der Profilanzahl nach Identitäts-Widget.](../images/profiles/profiles-count-change-trend-by-identity.png)

### [!UICONTROL Profile nach Identität] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbyidentity"
>title="Profile nach Identität"
>abstract="Dieses Widget zeigt die Aufschlüsselung aller zusammengeführten Profile im Profil Store nach Identitäten an."

Das Widget **[!UICONTROL Profile nach Identität]** zeigt die Aufschlüsselung der Identitäten in allen zusammengeführten Profile in Ihrem Profile Store an. Die Gesamtzahl der Profile nach Identität (d. h. das Addieren der für jeden Namespace angezeigten Werte) kann höher sein als die Gesamtzahl der zusammengeführten Profile, da einem Profil mehrere Namespaces zugeordnet sein können. Wenn beispielsweise ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, würden diesem einzelnen Kunden mehrere Namespaces zugeordnet.

Weitere Informationen finden Sie im Abschnitt [Abschnitt zu Zusammenführungsrichtlinien weiter oben in diesem Dokument](#merge-policies).

![Das Dashboard „Profile – Übersicht“ mit hervorgehobenem Widget „Profile nach Identität“.](../images/profiles/profiles-by-identity.png)

Um das Dialogfeld für automatische Beschriftungen zu öffnen, wählen Sie **[!UICONTROL Untertitel]**.

![Das Dialogfeld für Beschriftung von Profilen nach Identität.](../images/profiles/profiles-by-identity-captions.png)

Ein maschinelles Lernmodell generiert automatisch Dateneinblicke, indem es die Gesamtverteilung und die Schlüsselaspekte der Daten analysiert.

Weitere Informationen zu Identitäten finden Sie im Abschnitt [Dokumentation zu Adobe Experience Platform Identity Service](../../identity-service/home.md).

### [!UICONTROL Identitätsüberschneidung] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_identityoverlap"
>title="Identitätsüberschneidung"
>abstract="Dieses Widget verwendet ein Venn-Diagramm, um die Überschneidung von Profilen in Ihrem Profile Store anzuzeigen, die die beiden ausgewählten Identitäten enthalten."

Das Widget **[!UICONTROL Identitätsüberschneidung]** verwendet ein Venn-Diagramm, oder Mengendiagramm, um die Überschneidung von Profilen in Ihrem Profile Store anzuzeigen, die die beiden ausgewählten Identitäten enthalten.

Verwenden Sie die Widget-Dropdown-Menüs, um die Identitäten auszuwählen, die Sie vergleichen möchten. Kreise zeigen die relative Gesamtzahl der Profile an, in denen jede Identität enthalten ist. Die Anzahl der Profile, in denen beide Identitäten enthalten sind, wird durch die Größe der Überschneidung zwischen den Kreisen dargestellt. Wenn ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, würden diesem einzelnen Kunden mehrere Identitäten zugeordnet. In diesem Fall ist es wahrscheinlich, dass Ihr Unternehmen über mehrere Profile verfügt, die Fragmente aus mehreren Identitäten enthalten.

Weiterführende Informationen zu Profilfragmenten finden Sie im Abschnitt zu [Profilfragmente und zusammengeführte Profile](../../profile/home.md#profile-fragments-vs-merged-profiles) in der Übersicht über das Echtzeit-Kundenprofil .

Weitere Informationen zu Identitäten finden Sie im Abschnitt [Dokumentation zu Adobe Experience Platform Identity Service](../../identity-service/home.md).

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

Um ein Dialogfeld mit der Gesamtanzahl der Profile für eine Identität anzuzeigen, verwenden Sie den Cursor, um den Mauszeiger über einzelne Balken zu bewegen.

![Die einzelnen Identitätsprofile nach Identitäts-Widget.](../images/profiles/single-identity-profiles-by-identity.png)

### [!UICONTROL Nicht segmentierte Profile] {#unsegmented-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofiles"
>title="Nicht segmentierte Profile"
>abstract="Dieses Widget stellt die Gesamtanzahl aller Profile bereit, die keiner Zielgruppe zugeordnet sind, und bietet die Möglichkeit zur Profilaktivierung in Ihrer gesamten Organisation."

Die [!UICONTROL Nicht segmentierte Profile] -Widget stellt die Gesamtanzahl aller Profile bereit, die keiner Zielgruppe zugeordnet sind. Der generierte Wert gibt die zum Zeitpunkt der letzten Momentaufnahme korrekte Anzahl an und zeigt, wie viele Profile in Ihrer gesamten Organisation aktiviert werden können. Es zeigt auch die Möglichkeit an, Profile auszuschließen, die keinen angemessenen ROI liefern.

![Das Widget „Nicht segmentierte Profile“.](../images/profiles/unsegmented-profiles.png)

### [!UICONTROL Änderungs-Trend bei nicht segmentierten Profilen] {#unsegmented-profiles-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilestrend"
>title="Trend von nicht segmentierten Profilen"
>abstract="Dieses Widget bietet eine grafische Darstellung der Anzahl der Profile, die in einem bestimmten Zeitraum nicht mit einer Zielgruppe verbunden sind. Der Trend der Profile, die keiner Zielgruppe zugeordnet sind, kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden."

Die [!UICONTROL Trendänderung von nicht segmentierten Profilen] Widget verwendet ein Liniendiagramm, um die Anzahl der Profile zu veranschaulichen, die seit dem letzten täglichen Schnappschuss hinzugefügt wurden und an keine Zielgruppe angehängt sind. Der Änderungstrend von Profilen, die keiner Zielgruppe zugeordnet sind, kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt. Die Anzahl der Profile wird auf der Y-Achse und die Zeit auf der X-Achse dargestellt.

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

### [!UICONTROL Zielgruppen] {#audiences}

Dieses Widget stellt die Gesamtzahl der Zielgruppen bereit, die entsprechend der ausgewählten Zusammenführungsrichtlinie, die auf Ihre Profildaten angewendet wird, aktiviert werden können.

Auswählen **[!UICONTROL Zielgruppen]** , um zur [!UICONTROL Zielgruppen] Dashboard [!UICONTROL Durchsuchen] Registerkarte. Von dort aus können Sie eine Liste aller Segmentdefinitionen für Ihre Organisation sehen.

![Das Zielgruppen-Widget.](../images/profiles/audiences.png)

<!-- https://jira.corp.adobe.com/browse/PLAT-115291 -->

<!-- * [[!UICONTROL Audiences change trend]](#audiences-change-trend) -->
<!-- ### [!UICONTROL Audiences change trend] {#audiences-change-trend}

This line graph widget visualizes the change in the total number of audiences each day, trending over time. The change in the number of audiences is dependent on the selected merge policy being applied to your profile data. The period of analysis is selected from the widget dropdown menu. The bar chart can be visualized over 30 days, 90 days, and 12-month periods.

The visualization allows you to monitor the overall health of audiences within Adobe Experience Platform by understanding trends in the growth or decline of the total number of audiences. -->

<!-- ![The Audiences change trend widget.]() -->

### [!UICONTROL Der Bericht „Zielgruppenüberschneidung“] {#audience-overlap-report}

Dieses Widget tabellarisiert die Datenüberschneidung von allen verfügbaren Zielgruppen, gefiltert nach Zusammenführungsrichtlinien. Für die Zusammenführungsrichtlinie, die oben im Bildschirm im Dropdown-Menü ausgewählt wird, wird eine Liste mit fünf Zielgruppen, sortiert von den höchsten bis zu den niedrigsten Überschneidungsprozentsätzen, bereitgestellt. Die beiden analysierten Zielgruppen werden im [!UICONTROL ZIELGRUPPE A NAME] und [!UICONTROL AUDIENCE B NAME] Spalten. Die prozentuale Überschneidung wird in der dritten Spalte auf zwölf Dezimalstellen genau angegeben.

Der Bericht zur Zielgruppenüberschneidung hilft Ihnen beim Erstellen neuer, leistungsstarker Zielgruppen. Durch die Beachtung hoher prozentualer Überschneidungen können Sie Zielgruppen unterdrücken und das Senden derselben Zielgruppe an verschiedene Ziele verhindern. Diese Daten helfen Ihnen auch dabei, verborgene Insights zu entdecken, die bei einer besseren Segmentierung hilfreich sein können. Eine geringe prozentuale Überschneidung hilft, eindeutige Profile zu finden, deren Kontaktierung Sie fortsetzen sollten.

Wählen Sie **[!UICONTROL Mehr anzeigen]** aus, um ein Vollbilddialogfeld zu öffnen, das mehr Daten zu Zielgruppenüberschneidungen enthält.

![Das Widget „Bericht Zielgruppenüberscheidung“ mit hervorgehobener Option „Mehr anzeigen“.](../images/profiles/profiles-audience-overlap-report.png)

Das Dialogfeld [!UICONTROL Bericht zur Zielgruppenüberschneidung] wird angezeigt. Dieses Dialogfeld kann bis zu 50 Zeilen mit Analysen zur Zielgruppenüberschneidung enthalten, die in sechs Spalten unterteilt sind. Um Spalten aus der Tabelle zu entfernen oder hinzuzufügen, wählen Sie das Einstellungssymbol (![Das Einstellungssymbol.](../images/profiles/settings-icon.png)).

![Das Dialogfeld mit dem Bericht zur Zielgruppenüberschneidung.](../images/profiles/profiles-audience-overlap-report-dialog.png)

>[!NOTE]
>
>Wenn Sie die Rangfolge der Ergebnisse zwischen dem höchsten und dem niedrigsten bzw. dem höchsten ändern möchten, wählen Sie die **[!UICONTROL Überlappung]** Spaltenüberschrift.

Um den gesamten Bericht im PDF-Format herunterzuladen, wählen Sie das Optionsmenü (**`...`**) und dann **[!UICONTROL Download]** aus.

![Das Dialogfeld mit dem Bericht zur Zielgruppenüberschneidung mit den Auslassungszeichen und der hervorgehobenen Download-Option.](../images/profiles/profiles-audience-overlap-report-dialog-download.png)

Um ein Venn-Diagramm der Überschneidungsanalyse zu öffnen, wählen Sie eine Zeile aus dem Bericht aus. Um die Profilanzahl in einem Dialogfeld anzuzeigen, bewegen Sie den Mauszeiger über einen Abschnitt des Venn-Diagramms.

![Das Dialogfeld „Bericht Zielgruppenüberschneidung“ mit Hervorhebung eines Venn-Diagramms und einer Zeile.](../images/profiles/profiles-audience-overlap-report-dialog-venn.png)

Wählen Sie **[!UICONTROL Schließen]** aus, um zum [!UICONTROL Profile]-Dashboard zurückzukehren.

### [!UICONTROL Zielgruppen, die einem Zielstatus zugeordnet sind] {#audiences-mapped-to-destination-status}

Die [!UICONTROL Zielgruppen, die dem Zielstatus zugeordnet sind] -Widget zeigt die Gesamtanzahl der zugeordneten und nicht zugeordneten Zielgruppen in einer einzelnen Metrik an und verwendet ein Ringdiagramm, um den proportionalen Unterschied zwischen den Summen zu veranschaulichen. Die berechneten Zahlen hängen von der gewählten Zusammenführungsrichtlinie ab.

Wenn der Mauszeiger über den entsprechenden Abschnitt des Ringdiagramms bewegt wird, werden die separaten Zählungen für zugeordnete oder nicht zugeordnete Zielgruppen in einem Dialogfeld angezeigt.

![Das Widget „Zielgruppen, die dem Zielstatus zugeordnet sind“.](../images/profiles/audiences-mapped-to-destination-status.png)

### [!UICONTROL Zielgruppen-Größe] {#audiences-size}

Die [!UICONTROL Zielgruppengröße] -Widget bietet eine zweispaltige Tabelle, in der die Namen von bis zu 20 Zielgruppen und die Gesamtzahl der in den einzelnen Zielgruppen enthaltenen Profile aufgelistet werden. Die Liste wird in Abhängigkeit von der Gesamtzahl der in der Audience enthaltenen Profile von hoch bis niedrig geordnet. Die Gesamtzahl der Zielgruppengrößen hängt von der angewendeten Zusammenführungsrichtlinie ab.

![Das Widget „Zielgruppengröße“.](../images/profiles/audiences-size.png)

Um umfassende Informationen zu einer Zielgruppe anzuzeigen, wählen Sie einen Zielgruppennamen aus der bereitgestellten Liste aus, um zur [!UICONTROL Zielgruppen] [!UICONTROL Detail] Seite. Außerdem durch Auswahl von **[!UICONTROL Alle Zielgruppen anzeigen]** Sie können am Ende des Widgets zur [!UICONTROL Zielgruppen] [!UICONTROL Durchsuchen] um eine beliebige existierende Zielgruppe zu finden.

![Das Widget Größe von Zielgruppen mit einem Zielgruppennamen und dem Text Alle Zielgruppen anzeigen hervorgehoben.](../images/profiles/audiences-size-view-all-audiences.png)

Weitere Informationen zu finden Sie in der Dokumentation . [[!UICONTROL Zielgruppen] [!UICONTROL  Durchsuchen] tab](../../segmentation/ui/overview.md#browse).

### [!UICONTROL Zielgruppenüberschneidung nach Zusammenführungsrichtlinie] {#audience-overlap-by-merge-policy}

Dieses Widget verwendet ein Venn-Diagramm, um die Überschneidung zweier ausgewählter Zielgruppen anzuzeigen. Die Zusammenführungsrichtlinie wird oben auf der Seite aus dem Dropdown-Menü Übersicht ausgewählt und die Zielgruppen für die Analyse werden aus zwei Dropdown-Menüs im Widget ausgewählt. Die Gesamtzahl der in der relevanten Segmentdefinition enthaltenen Profile kann durch Bewegen des Mauszeigers über einen Kreis oder die Schnittmenge angezeigt werden.

Dieses Widget stellt die visuelle Überschneidung von Segmentdefinitionen dar und ermöglicht es Ihnen, die Segmentierungsstrategie zu optimieren, indem Sie die Ähnlichkeiten zwischen Ihren Segmentdefinitionen untersuchen.

![Das Dashboard Platform UI Profile mit der Dropdown-Liste Zusammenführungsrichtlinie und den Dropdown-Listen Widget-Zielgruppe werden hervorgehoben.](../images/profiles/audience-overlap-by-merge-policy.png)


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

Durch Befolgen dieses Dokuments sollten Sie jetzt in der Lage sein, das Profil-Dashboard zu finden und die in den verfügbaren Widgets angezeigten Metriken zu verstehen. Weitere Informationen zum Arbeiten mit [!DNL Profile] Daten in der Experience Platform-Benutzeroberfläche, siehe [Handbuch zur Benutzeroberfläche des Echtzeit-Kundenprofils](../../profile/ui/user-guide.md).
