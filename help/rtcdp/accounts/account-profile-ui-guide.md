---
keywords: RTCDP-Profil;Profile RTCDP;RTCDP-Identitäten;RTCDP-Zusammenführungsrichtlinie;Echtzeit-Kundenprofil
title: Handbuch zur Benutzeroberfläche von Account-Profilen
description: Durch die Verwendung von Kontoprofilen ermöglicht Ihnen Adobe Real-time Customer Data Platform B2B Edition die Vereinheitlichung von Kontoinformationen aus verschiedenen Quellen. Dieses Handbuch enthält Details zur Interaktion mit Account-Profilen in der Benutzeroberfläche von Adobe Experience Platform.
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
feature: Profiles, B2B
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: 96f29d5c64bb29125d8a63dd3ddb3bdedb5ebd52
workflow-type: tm+mt
source-wordcount: '1680'
ht-degree: 55%

---

# Handbuch zur Benutzeroberfläche von Account-Profilen

>[!NOTE]
>
>Kontoprofile sind nur für Kunden von Real-time Customer Data Platform B2B Edition verfügbar. Um mehr über Real-Time CDP zu erfahren, einschließlich der für jeden Lizenztyp verfügbaren Funktionen und Funktionen, lesen Sie zunächst die [Real-Time CDP - Übersicht](../overview.md) .

Mit Account-Profilen können Sie Account-Informationen aus mehreren Quellen vereinheitlichen. Diese einheitliche Ansicht eines Accounts führt Daten aus all Ihren Marketing-Kanälen und den diversen Systemen zusammen, die Ihr Unternehmen derzeit zum Speichern von Kunden-Account-Informationen verwendet. Dieses Dokument enthält eine Anleitung zur Interaktion mit Kontoprofilen mithilfe der in der Benutzeroberfläche von Adobe Experience Platform verfügbaren Real-Time CDP-Funktionen, B2B Edition.

Weitere Informationen zur Erstellung von Account-Profilen im Rahmen des B2B-Workflows finden Sie im Abschnitt [End-to-End-Tutorial](../b2b-tutorial.md).

## Übersicht über Account-Profile {#account-profiles-overview}

Wählen Sie **[!UICONTROL Profile]** unter [!UICONTROL Konten] im linken Navigationsbereich aus, um die Übersicht über Kontoprofile anzuzeigen. Unter der Registerkarte [!UICONTROL Übersicht] zeigt das Dashboard eine Grafik oder ein Diagramm mit Widgets als Einstiegspunkt an.

![Die Registerkarte Übersicht über Kontoprofile mit Profilen im linken Navigationsbereich und hervorgehobener Übersicht.](images/b2b-account-profile-overview.png)

Weitere Informationen finden Sie in der Dokumentation zum Dashboard [[!UICONTROL Kontoprofile]](../../dashboards/guides/account-profiles.md) . Weitere Informationen dazu, wie Sie mit Ihren Insights-Datenmodellen benutzerdefinierte Diagramme für Ihre Dashboards erstellen können, finden Sie in der Dokumentation zu [Real-time Customer Data Platform Insights-Datenmodell B2B Edition](../../dashboards/data-models/cdp-insights-data-model-b2b.md) .

## Konfigurieren des Leads zur Kontozuordnung {#configure-lead-to-account-matching}

>[!IMPORTANT]
>
> Nur B2B AI-Administratoren können den Lead aktivieren, deaktivieren und konfigurieren, um den Dienst für die Kontoabstimmung zu aktivieren. Nach der Deaktivierung des Dienstes werden die entsprechenden Ergebnisse innerhalb von 24 Stunden gelöscht.

Wählen Sie zum Konfigurieren der Kontoübereinstimmung die Option **[!UICONTROL Profile]** unter [!UICONTROL Konten] im linken Navigationsbereich aus. Wählen Sie auf der Registerkarte **[!UICONTROL Übersicht]** oben rechts die Option **[!UICONTROL Einstellungen]** aus.

![Die Registerkarte Übersicht über die Kontoprofile mit hervorgehobener Einstellung.](images/b2b-configuring-accounts-profile.png)

Das Dialogfeld **[!UICONTROL Kontoeinstellungen]** wird geöffnet. Wählen Sie hier den Umschalter **[!UICONTROL Lead-zu-Konto-Abgleich aktivieren]** aus, um die Funktion zu aktivieren. Verwenden Sie das Dropdown-Menü, um **[!UICONTROL Täglich]** für die Einstellung **[!UICONTROL Übereinstimmungscadence]** auszuwählen. Wählen Sie abschließend die relevanten Optionen für **[!UICONTROL Übereinstimmungskriterien]** und danach **[!UICONTROL Speichern]** aus, um Ihre Einstellungen zu bestätigen und zum Bildschirm **[!UICONTROL Kontoprofile]** zurückzukehren.

>[!NOTE]
>
> Die Adresse kann nicht als einziges übereinstimmendes Kriterium verwendet werden. Es müssen mindestens eines der anderen Kriterien ausgewählt werden.

![Kontoeinstellungen konfigurieren](images/b2b-configuring-account-settings.png)

Weiterführende Informationen zum Abgleich von Leads mit Konten finden Sie in der Übersicht über die Kontozuordnung bei Real-Time CDP B2B](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).[

## Durchsuchen von Account-Profilen {#browse-account-profiles}

Um Account-Profile zu durchsuchen, wählen Sie zunächst **[!UICONTROL Profile]** unter [!UICONTROL Accounts] im linken Navigationsbereich aus.

Auf der Registerkarte **[!UICONTROL Durchsuchen]** können Sie Account-Profile mithilfe einer Account-ID aus einer verbundenen Unternehmensquelle analysieren oder Quelldetails direkt eingeben.

![Verwenden Sie die Konto-ID, um Profile zu analysieren](images/b2b-account-browse-by.png)

### Durchsuchen nach [!UICONTROL Verbundener Unternehmensquelle] {#browse-by-connected-enterprise-source}

Um Account-Profile nach einer verbundenen Unternehmensquelle zu durchsuchen, wählen Sie **[!UICONTROL Verbundene Unternehmensquelle]** aus dem Dropdown-Menü **[!UICONTROL Durchsuchen nach]** und wählen Sie dann mithilfe der Auswahl-Schaltfläche neben dem Feld **[!UICONTROL Quelle]** eine verbundene Quelle aus.

![Kontoprofile nach verbundener Unternehmensquelle durchsuchen](images/b2b-account-browse.png)

Dadurch wird der Dialog **[!UICONTROL Quelle auswählen]** geöffnet, in dem Sie eine Quelle auswählen können, die auf den Verbindungen basiert, die Ihr Unternehmen hergestellt hat.

>[!NOTE]
>
>In Ihrem Unternehmen können für denselben Dienstleister mehrere Quellen konfiguriert sein (z. B. Marketo). Daher ist es wichtig, den Verbindungsnamen, das Quellsystem und die Quellsysteminstanz zu überprüfen, um sicherzustellen, dass Sie nach der richtigen Quellinstanz suchen.

Weiterführende Informationen zum Verbinden von Unternehmensquellen finden Sie in der [Quellenübersicht](../sources/sources-overview.md).

Sie können eine Quelle auswählen, indem Sie die Optionsschaltfläche neben dem Verbindungsnamen auswählen und dann **[!UICONTROL Auswählen]** verwenden, um zur Registerkarte [!UICONTROL Durchsuchen] zurückzukehren.

![Quell-Workflow auswählen](images/b2b-account-select-source.png)

Bei ausgewählter Quelle müssen Sie jetzt eine **[!UICONTROL Account-ID]** eingeben, die mit der Quelle verknüpft ist. Wenn Sie beispielsweise eine Salesforce-Quelle auswählen, müssen Sie eine Account-ID aus der Salesforce-Instanz eingeben, um das mit dieser ID verknüpfte Account-Profil anzuzeigen.

>[!NOTE]
>
>Für Marketo-Account-IDs können zwei Account-Tabellen referenziert werden. Daher müssen Sie eine bestimmte Syntax verwenden, um sicherzustellen, dass Sie den richtigen Account anzeigen.
>
>Die häufigste Standardsyntax ist die Marketo-Account-ID, an die `.mkto_org` angehängt wird (z. B. `1234567.mkto_org`). Marketo-Kunden mit Account-basiertem Marketing verfügen möglicherweise über zusätzliche Werte, die mithilfe der Marketo-Account-ID mit dem Anhang `.mkto_account` gefunden werden können. Wenn Sie sich nicht sicher sind, welche Syntax Sie verwenden sollten, wenden Sie sich an Ihren Marketo-Administrator.

![Auswahl der Konto-ID](images/b2b-account-browse-id.png)

### Durchsuchen nach [!UICONTROL Sonstige] {#browse-by-others}

Real-Time CDP, B2B Edition unterstützt die Möglichkeit, eine direkte Suche durchzuführen, indem Sie einen **[!UICONTROL Source name]**, **[!UICONTROL Source instance]** und **[!UICONTROL Account ID]** für ein Konto eingeben können, das Sie anzeigen möchten. Indem Sie den Quellnamen und die Instanz direkt eingeben, geben Sie den Kontext an, den Experience Platform benötigt, um nach den richtigen Account-Profildaten zu suchen und diese anzuzeigen.

Die Möglichkeit, eine direkte Suche durchzuführen, ist unter Umständen nützlich, wenn eine direkte Quellverbindung zu den Daten nicht möglich ist. Wenn Ihr Unternehmen beispielsweise über Data Governance-Richtlinien verfügt, die eine direkte Verbindung zu einem CRM verhindern, können Sie diese Daten in ein Cloud-Speichersystem exportieren und dann in Experience Platform aufnehmen.

Ein weiteres Beispiel könnte sein, dass Sie eine Umwandlung der Daten durchführen, nachdem diese ein System verlassen haben und bevor sie in Platform aufgenommen werden. Sie können die Funktion für die direkte Suche verwenden, um einen Kontext für die Daten bereitzustellen (z. B. um anzugeben, dass es sich um Marketo-Daten handelt, obwohl sie beispielsweise von einem Amazon S3-Bucket stammen), sodass das System weiß, wo die Daten gesucht werden sollen und wie sie korrekt wiedergegeben werden.

Um eine direkte Suche zu starten, wählen Sie **[!UICONTROL Sonstige]** aus dem Dropdown-Menü **[!UICONTROL Durchsuchen nach]** aus, und geben Sie dann **[!UICONTROL Quellnamen]**, **[!UICONTROL Quellinstanz]** und **[!UICONTROL Account-ID]** für den Account ein, den Sie anzeigen möchten.

![Durchsuchen durch andere](images/b2b-account-browse-adhoc.png)

## Anzeigen von Details zum Account-Profil {#view-account-profile-details}

Nachdem Sie die Registerkarte **[!UICONTROL Durchsuchen]** zum Suchen eines Account-Profils verwendet haben, wird durch Auswahl von **[!UICONTROL Profilkennung]** die Registerkarte **[!UICONTROL Detail]** für das Account-Profil geöffnet. Die auf der Registerkarte **[!UICONTROL Detail]** angezeigten Profildaten wurden aus mehreren Profilfragmenten zusammengeführt, um eine zentrale Ansicht des jeweiligen Accounts zu erstellen. Dazu gehören Account-Details wie grundlegende Attribute und Social-Media-Daten.

Die Standardfelder können auch auf Organisationsebene geändert werden, um die bevorzugten Account-Profil-Attribute anzuzeigen.

>[!NOTE]
>
>Ähnliche Funktionen sind für Kundenprofile verfügbar und es gibt eine schrittweise Anleitung zum Hinzufügen und Entfernen von Attributen, zum Ändern der Größe von Panels usw. Weitere Informationen finden Sie im [Handbuch zur Anpassung von Profildetails](../../profile/ui/profile-customization.md).

![Kontoprofildetails anzeigen](images/b2b-account-details.png)

Sie können zusätzliche Details zum Konto anzeigen, indem Sie eine andere der verfügbaren Registerkarten auswählen. Diese Registerkarten umfassen Attribute, Personen und die Registerkarte „Opportunitys“, auf der die offenen und geschlossenen Chancen für das Konto in Ihren Unternehmenssystemen angezeigt werden. Weitere Informationen zu den einzelnen Registerkarten finden Sie in den folgenden Abschnitten.

## Registerkarte „Attribute“ {#attributes-tab}

Auf der Registerkarte **[!UICONTROL Attribute]** werden alle Datensatzinformationen aufgelistet, die sich auf den Account beziehen. Dazu gehören Attributdaten aus mehreren Quellen, die zusammengeführt wurden, um eine einzige Ansicht des Accounts zu bilden.

Sie können die Daten nicht nur in einer Liste anzeigen, sondern auch in der Suchleiste nach bestimmten Attributen suchen oder die Datensatzdaten als JSON anzeigen.

![Registerkarte &quot;Attribute&quot;](images/b2b-account-attributes.png)

## Registerkarte „Personen“ {#people-tab}

Die Registerkarte **[!UICONTROL Personen]** enthält eine Liste der einzelnen Personen, die mit dem Account in Verbindung stehen. Diese Personen können Kontakte und Leads aus verschiedenen Unternehmenssystemen sein, die von verschiedenen Teams in Ihrem Unternehmen verwaltet werden. In Real-Time CDP, B2B Edition werden sie jedoch in einer einzigen Liste vorgestellt, in der Sie eine ganzheitlichere Übersicht über Ihre Kontokontakte erhalten.

>[!NOTE]
>
>Auf der Registerkarte [!UICONTROL Personen] wird eine Liste mit bis zu 25 Personen angezeigt, die mit dem Account in Verbindung stehen. Bei Accounts mit mehr als 25 Personen zeigt das System eine Stichprobe von 25 Datensätzen an.

Neben einer Momentaufnahme der Informationen für den Kontakt enthält jede aufgeführte Person auch eine **[!UICONTROL Profil-ID]**, bei der es sich um einen anklickbaren Link handelt, über den Sie das Echtzeit-Kundenprofil für diese Person ermitteln können. Weitere Informationen zum Anzeigen einzelner Kundenprofile für Ihre Konten finden Sie im Handbuch für das Durchsuchen von Profilen in Real-Time CDP, B2B Edition](../profile/profile-browse.md).[

![Registerkarte &quot;Personen&quot;](images/b2b-account-people.png)

## Registerkarte „Opportunitys“ {#opportunities-tab}

Die Registerkarte **[!UICONTROL Opportunitys]** enthält Informationen zu offenen und geschlossenen Opportunitys im Zusammenhang mit dem Account. Diese Möglichkeiten können aus verschiedenen Quellen in Experience Platform eingebunden werden, aber Real-Time CDP, B2B Edition macht es für Marketingexperten einfach, all diese Möglichkeiten an einem Ort zu sehen.

>[!NOTE]
>
>Auf der Registerkarte [!UICONTROL Opportunitys] wird eine Liste mit bis zu 25 mit dem Account verbundenen Opportunitys angezeigt. Bei Accounts mit mehr als 25 verbundenen Opportunitys zeigt das System eine Stichprobe von 25 Datensätzen an.

Jede Opportunity umfasst Informationen wie den Namen der Opportunity, ihren Umfang, die Phase und ob die Opportunity offen, geschlossen, gewonnen oder verloren ist.

![Registerkarte &quot;Kontogelegenheiten&quot;](images/b2b-account-opportunities.png)

## Registerkarte &quot;Verwandte Konten&quot; {#related-accounts-tab}

Die Registerkarte **[!UICONTROL Zugehörige Konten]** enthält Informationen zu anderen Konten, die mit dem Konto in Verbindung stehen, das Sie durchsuchen. Detaillierte Informationen zur Funktion finden Sie in der [Übersicht über zugehörige Konten](/help/rtcdp/b2b-ai-ml-services/related-accounts.md).

>[!NOTE]
>
>* Eine Gruppe verwandter Konten kann über maximal 30 Kontoprofile verfügen. Wenn mehr als 30 Kontoprofile als verwandt gefunden wurden, werden sie willkürlich in mehrere Gruppen unterteilt, von denen jede maximal 30 Mitglieder hat. Die Gruppe Zugehörige Konten eines Kontoprofils enthält immer sich selbst.
>* Auf der Registerkarte [!UICONTROL Zugehörige Konten] wird derzeit eine Liste mit bis zu 25 Konten angezeigt, die mit dem Konto verknüpft sind, das Sie durchsuchen. Dies ist eine Einschränkung, die in einer zukünftigen Aktualisierung behoben wird. Trotz dieser Benutzeroberflächenbeschränkung werden bei der Verwendung verwandter Konten in Segmentdefinitionen für Gruppen mit 30 verwandten Kontoprofilen alle Profile für das Targeting verwendet.

Jedes zugehörige Konto enthält Informationen wie die Kontoprofil-ID und den Namen, den Kontoquellschlüssel und weitere Informationen zu Homepage, Adresse, übergeordnetem Konto, Telefon, Branche und Jahresumsatz.

![Registerkarte &quot;Verwandte Konten&quot;](images/b2b-account-related-accounts.png)

Sie können die zugehörigen Konten in dieser Liste für Segmentierungszwecke verwenden. In einem [Segmentierungsbeispiel](/help/rtcdp/segmentation/b2b.md#related-account) erfahren Sie, wie Sie verwandte Konten verwenden können, um Ihre Reichweite in Segmentdefinitionen zu erweitern.