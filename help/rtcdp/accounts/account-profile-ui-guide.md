---
keywords: RTCDP-Profil;Profile RTCDP;RTCDP-Identitäten;RTCDP-Zusammenführungsrichtlinie;Echtzeit-Kundenprofil
title: Handbuch zur Benutzeroberfläche von Account-Profilen
description: Durch die Verwendung von Account-Profilen ermöglicht Ihnen Real-time Customer Data Platform B2B Edition die Vereinheitlichung von Account-Informationen aus verschiedenen Quellen. Dieses Handbuch enthält Details zur Interaktion mit Account-Profilen in der Benutzeroberfläche von Adobe Experience Platform.
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: 9bd7434f2b224d76decac1e04d8491a6b3149a3a
workflow-type: ht
source-wordcount: '1193'
ht-degree: 100%

---

# Handbuch zur Benutzeroberfläche von Account-Profilen

>[!NOTE]
>
>Account-Profile sind nur für Kunden von Real-time Customer Data Platform B2B Edition verfügbar. Um mehr über Real-Time Customer Data Platform zu erfahren, auch zu den für jeden Lizenztyp verfügbaren Funktionen, lesen Sie bitte zunächst den [Überblick über Real-Time Customer Data Platform](../overview.md).

Mit Account-Profilen können Sie Account-Informationen aus mehreren Quellen vereinheitlichen. Diese einheitliche Ansicht eines Accounts führt Daten aus all Ihren Marketing-Kanälen und den diversen Systemen zusammen, die Ihr Unternehmen derzeit zum Speichern von Kunden-Account-Informationen verwendet. Dieses Dokument enthält ein Handbuch zur Interaktion mit Account-Profilen unter Verwendung der in der Benutzeroberfläche von Adobe Experience Platform verfügbaren Funktionen von Real-Time Customer Data Platform (B2B Edition).

Weitere Informationen zur Erstellung von Account-Profilen im Rahmen des B2B-Workflows finden Sie im Abschnitt [End-to-End-Tutorial](../b2b-tutorial.md).

## Durchsuchen von Account-Profilen

Um Account-Profile zu durchsuchen, wählen Sie zunächst **[!UICONTROL Profile]** unter [!UICONTROL Accounts] im linken Navigationsbereich aus.

![](images/b2b-account-browse.png)

Auf der Registerkarte **[!UICONTROL Durchsuchen]** können Sie Account-Profile mithilfe einer Account-ID aus einer verbundenen Unternehmensquelle analysieren oder Quelldetails direkt eingeben.

![](images/b2b-account-browse-by.png)

### Durchsuchen nach [!UICONTROL Verbundener Unternehmensquelle]

Um Account-Profile nach einer verbundenen Unternehmensquelle zu durchsuchen, wählen Sie **[!UICONTROL Verbundene Unternehmensquelle]** aus dem Dropdown-Menü **[!UICONTROL Durchsuchen nach]** und wählen Sie dann mithilfe der Auswahl-Schaltfläche neben dem Feld **[!UICONTROL Quelle]** eine verbundene Quelle aus.

![](images/b2b-account-browse.png)

Dadurch wird der Dialog **[!UICONTROL Quelle auswählen]** geöffnet, in dem Sie eine Quelle auswählen können, die auf den Verbindungen basiert, die Ihr Unternehmen hergestellt hat.

>[!NOTE]
>
>In Ihrem Unternehmen können für denselben Dienstleister mehrere Quellen konfiguriert sein (z. B. Marketo). Daher ist es wichtig, den Verbindungsnamen, das Quellsystem und die Quellsysteminstanz zu überprüfen, um sicherzustellen, dass Sie nach der richtigen Quellinstanz suchen.

Weiterführende Informationen zum Verbinden von Unternehmensquellen finden Sie in der [Quellenübersicht](../sources/sources-overview.md).

![](images/b2b-account-select-source.png)

Sie können eine Quelle auswählen, indem Sie die Optionsschaltfläche neben dem Verbindungsnamen auswählen und dann **[!UICONTROL Auswählen]** verwenden, um zur Registerkarte [!UICONTROL Durchsuchen] zurückzukehren.

Bei ausgewählter Quelle müssen Sie jetzt eine **[!UICONTROL Account-ID]** eingeben, die mit der Quelle verknüpft ist. Wenn Sie beispielsweise eine Salesforce-Quelle auswählen, müssen Sie eine Account-ID aus der Salesforce-Instanz eingeben, um das mit dieser ID verknüpfte Account-Profil anzuzeigen.

>[!NOTE]
>
>Für Marketo-Account-IDs können zwei Account-Tabellen referenziert werden. Daher müssen Sie eine bestimmte Syntax verwenden, um sicherzustellen, dass Sie den richtigen Account anzeigen.
>
>Die häufigste Standardsyntax ist die Marketo-Account-ID, an die `.mkto_org` angehängt wird (z. B. `1234567.mkto_org`). Marketo-Kunden mit Account-basiertem Marketing verfügen möglicherweise über zusätzliche Werte, die mithilfe der Marketo-Account-ID mit dem Anhang `.mkto_account` gefunden werden können. Wenn Sie sich nicht sicher sind, welche Syntax Sie verwenden sollten, wenden Sie sich an Ihren Marketo-Administrator.

![](images/b2b-account-browse-id.png)

### Durchsuchen nach [!UICONTROL Sonstige]

Real-Time Customer Data Platform B2B Edition unterstützt die Möglichkeit, eine direkte Suche durchzuführen, indem Sie **[!UICONTROL Quellnamen]**, **[!UICONTROL Quellinstanz]** und **[!UICONTROL Account-ID]** für den Account eingeben, den Sie anzeigen möchten. Indem Sie den Quellnamen und die Instanz direkt eingeben, geben Sie den Kontext an, den Experience Platform benötigt, um nach den richtigen Account-Profildaten zu suchen und diese anzuzeigen.

Die Möglichkeit, eine direkte Suche durchzuführen, ist unter Umständen nützlich, wenn eine direkte Quellverbindung zu den Daten nicht möglich ist. Wenn Ihr Unternehmen beispielsweise über Data Governance-Richtlinien verfügt, die eine direkte Verbindung zu einem CRM verhindern, können Sie diese Daten in ein Cloud-Speichersystem exportieren und dann in Experience Platform aufnehmen.

Ein weiteres Beispiel könnte sein, dass Sie eine Umwandlung der Daten durchführen, nachdem diese ein System verlassen haben und bevor sie in Platform aufgenommen werden. Sie können die Funktion für die direkte Suche verwenden, um einen Kontext für die Daten bereitzustellen (z. B. um anzugeben, dass es sich um Marketo-Daten handelt, obwohl sie beispielsweise von einem Amazon S3-Bucket stammen), sodass das System weiß, wo die Daten gesucht werden sollen und wie sie korrekt wiedergegeben werden.

Um eine direkte Suche zu starten, wählen Sie **[!UICONTROL Sonstige]** aus dem Dropdown-Menü **[!UICONTROL Durchsuchen nach]** aus, und geben Sie dann **[!UICONTROL Quellnamen]**, **[!UICONTROL Quellinstanz]** und **[!UICONTROL Account-ID]** für den Account ein, den Sie anzeigen möchten.

![](images/b2b-account-browse-adhoc.png)

## Anzeigen von Details zum Account-Profil

Nachdem Sie die Registerkarte **[!UICONTROL Durchsuchen]** zum Suchen eines Account-Profils verwendet haben, wird durch Auswahl von **[!UICONTROL Profilkennung]** die Registerkarte **[!UICONTROL Detail]** für das Account-Profil geöffnet. Die auf der Registerkarte **[!UICONTROL Detail]** angezeigten Profildaten wurden aus mehreren Profilfragmenten zusammengeführt, um eine zentrale Ansicht des jeweiligen Accounts zu erstellen. Dazu gehören Account-Details wie grundlegende Attribute und Social-Media-Daten.

Die Standardfelder können auch auf Organisationsebene geändert werden, um die bevorzugten Account-Profil-Attribute anzuzeigen.

>[!NOTE]
>
>Ähnliche Funktionen sind für Kundenprofile verfügbar und es gibt eine schrittweise Anleitung zum Hinzufügen und Entfernen von Attributen, zum Ändern der Größe von Panels usw. Weitere Informationen finden Sie im [Handbuch zur Anpassung von Profildetails](../../profile/ui/profile-customization.md).

![](images/b2b-account-details.png)

Sie können zusätzliche Details zum Konto anzeigen, indem Sie eine andere der verfügbaren Registerkarten auswählen. Diese Registerkarten umfassen Attribute, Personen und die Registerkarte „Opportunitys“, auf der die offenen und geschlossenen Chancen für das Konto in Ihren Unternehmenssystemen angezeigt werden. Weitere Informationen zu den einzelnen Registerkarten finden Sie in den folgenden Abschnitten.

## Registerkarte „Attribute“

Auf der Registerkarte **[!UICONTROL Attribute]** werden alle Datensatzinformationen aufgelistet, die sich auf den Account beziehen. Dazu gehören Attributdaten aus mehreren Quellen, die zusammengeführt wurden, um eine einzige Ansicht des Accounts zu bilden.

Sie können die Daten nicht nur in einer Liste anzeigen, sondern auch in der Suchleiste nach bestimmten Attributen suchen oder die Datensatzdaten als JSON anzeigen.

![](images/b2b-account-attributes.png)

## Registerkarte „Personen“

Die Registerkarte **[!UICONTROL Personen]** enthält eine Liste der einzelnen Personen, die mit dem Account in Verbindung stehen. Diese Personen können Kontakte und Leads aus verschiedenen Unternehmenssystemen sein, die von verschiedenen Teams in Ihrem Unternehmen verwaltet werden. In Real-Time Customer Data Platform B2B Edition werden sie jedoch in einer Liste zusammengefasst, sodass Sie eine ganzheitlichere Ansicht Ihrer Account-Kontakte erhalten.

>[!NOTE]
>
>Auf der Registerkarte [!UICONTROL Personen] wird eine Liste mit bis zu 25 Personen angezeigt, die mit dem Account in Verbindung stehen. Bei Accounts mit mehr als 25 Personen zeigt das System eine Stichprobe von 25 Datensätzen an.

Neben der Anzeige einer Momentaufnahme der Informationen für den Kontakt enthält jede aufgeführte Person auch eine **[!UICONTROL Profilkennung]**, bei der es sich um einen anklickbaren Link handelt, über den Sie das Echtzeit-Kundenprofil für diese Person ermitteln können. Weitere Informationen zum Anzeigen einzelner Account-Profile in Bezug auf Ihre Accounts finden Sie im Handbuch zum [Durchsuchen von Profilen in Real-Time Customer Data Platform B2B Edition](../profile/profile-browse.md).

![](images/b2b-account-people.png)

## Registerkarte „Opportunitys“

Die Registerkarte **[!UICONTROL Opportunitys]** enthält Informationen zu offenen und geschlossenen Opportunitys im Zusammenhang mit dem Account. Diese Opportunitys können aus verschiedenen Quellen in Experience Platform aufgenommen werden. Real-Time Customer Data Platform B2B Edition erleichtert es Marketing-Experten jedoch, all diese Opportunitys an einem Ort zu sehen.

>[!NOTE]
>
>Auf der Registerkarte [!UICONTROL Opportunitys] wird eine Liste mit bis zu 25 mit dem Account verbundenen Opportunitys angezeigt. Bei Accounts mit mehr als 25 verbundenen Opportunitys zeigt das System eine Stichprobe von 25 Datensätzen an.

Jede Opportunity umfasst Informationen wie den Namen der Opportunity, ihren Umfang, die Phase und ob die Opportunity offen, geschlossen, gewonnen oder verloren ist.

![](images/b2b-account-opportunities.png)
