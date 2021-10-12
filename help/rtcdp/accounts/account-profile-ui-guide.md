---
keywords: rtcdp profile; profile rtcdp; rtcdp identities; rtcdp-Zusammenführungsrichtlinien; Echtzeit-Kundenprofil
title: Handbuch zur Benutzeroberfläche des Kontoprofils
description: Durch die Verwendung von Kontoprofilen ermöglicht Ihnen Real-time Customer Data Platform B2B Edition die Vereinheitlichung von Kontoinformationen aus verschiedenen Quellen. Dieses Handbuch enthält Details zur Interaktion mit Kontoprofilen in der Benutzeroberfläche von Adobe Experience Platform.
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: 5bd2afcc594d96878ee51af2e9e99d74b764009e
workflow-type: tm+mt
source-wordcount: '1191'
ht-degree: 0%

---

# Handbuch zur Benutzeroberfläche des Kontoprofils

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B Edition befindet sich derzeit in der Beta-Phase. Dokumentation und Funktionalität können sich ändern.

>[!NOTE]
>
>Kontoprofile sind nur für Kunden von Real-time Customer Data Platform B2B Edition verfügbar. Um mehr über die Echtzeit-Kundendatenplattform zu erfahren, einschließlich der für jeden Lizenztyp verfügbaren Funktionen, lesen Sie zunächst den [Überblick über die Echtzeit-Kundendatenplattform](../overview.md).

Mit Kontoprofilen können Sie Kontoinformationen aus mehreren Quellen vereinheitlichen. Diese einheitliche Ansicht eines Kontos führt Daten aus all Ihren Marketing-Kanälen und den diversen Systemen zusammen, die Ihr Unternehmen derzeit zum Speichern von Kundenkontoinformationen verwendet. Dieses Dokument enthält eine Anleitung zur Interaktion mit Kontoprofilen unter Verwendung der in der Benutzeroberfläche von Adobe Experience Platform verfügbaren Funktionen der Echtzeit-Kundendatenplattform (B2B Edition).

## Kontoprofile durchsuchen

Um Kontoprofile zu durchsuchen, wählen Sie zunächst **[!UICONTROL Profile]** unter [!UICONTROL Konten] im linken Navigationsbereich aus.

![](images/b2b-account-browse.png)

Auf der Registerkarte **[!UICONTROL Durchsuchen]** können Sie Kontoprofile mithilfe einer Konto-ID aus einer verbundenen Unternehmensquelle analysieren oder Quelldetails direkt eingeben.

![](images/b2b-account-browse-by.png)

### Durchsuchen nach [!UICONTROL Connected enterprise source]

Um Kontoprofile nach einer verbundenen Unternehmensquelle zu durchsuchen, wählen Sie **[!UICONTROL Connected enterprise source]** aus dem Dropdown-Menü **[!UICONTROL Durchsuchen nach]** und wählen Sie dann mithilfe der Selektor-Schaltfläche neben dem Feld **[!UICONTROL Quelle]** eine verbundene Quelle aus.

![](images/b2b-account-browse.png)

Dadurch wird das Dialogfeld **[!UICONTROL Quelle]** auswählen geöffnet, in dem Sie eine Quelle auswählen können, die auf den Verbindungen basiert, die Ihr Unternehmen hergestellt hat.

>[!NOTE]
>
>Ihr Unternehmen kann über mehrere für denselben Dienstleister konfigurierte Quellen verfügen (z. B. Marketo). Daher ist es wichtig, den Verbindungsnamen, das Quellsystem und die Quellsysteminstanz zu überprüfen, um sicherzustellen, dass Sie nach der richtigen Quellinstanz suchen.

Weiterführende Informationen zum Verbinden von Unternehmensquellen finden Sie in der [Quellenübersicht](../sources/sources-overview.md).

![](images/b2b-account-select-source.png)

Sie können eine Quelle auswählen, indem Sie das Optionsfeld neben dem Verbindungsnamen auswählen und dann **[!UICONTROL Select]** verwenden, um zur Registerkarte [!UICONTROL Durchsuchen] zurückzukehren.

Bei ausgewählter Quelle müssen Sie jetzt eine **[!UICONTROL Konto-ID]** eingeben, die mit der Quelle verknüpft ist. Wenn Sie beispielsweise eine Salesforce-Quelle auswählen, müssen Sie eine Konto-ID aus der Salesforce-Instanz eingeben, um das mit dieser ID verknüpfte Kontoprofil anzuzeigen.

>[!NOTE]
>
>Für Marketo-Konto-IDs können zwei Kontotabellen referenziert werden. Daher müssen Sie eine bestimmte Syntax verwenden, um sicherzustellen, dass Sie das richtige Konto anzeigen.
>
>Die häufigste Standardsyntax ist die Marketo-Konto-ID, die von `.mkto_org` angehängt wird (z. B. `1234567.mkto_org`). Kunden von Marketo Account-basiertem Marketing verfügen möglicherweise über zusätzliche Werte, die mithilfe der von `.mkto_account` angehängten Marketo-Konto-ID gefunden werden können. Wenn Sie sich nicht sicher sind, welche Syntax Sie verwenden sollten, wenden Sie sich an Ihren Marketo-Administrator.

![](images/b2b-account-browse-id.png)

### Nach [!UICONTROL Andere] durchsuchen

Die Echtzeit-Kundendatenplattform B2B Edition unterstützt die Möglichkeit, eine direkte Suche durchzuführen, indem Sie einen **[!UICONTROL Quellnamen]**, **[!UICONTROL Quellinstanz]** und **[!UICONTROL Konto-ID]** für ein Konto eingeben können, das Sie anzeigen möchten. Indem Sie den Quellnamen und die Instanz direkt eingeben, geben Sie den Kontext an, der für die Experience Platform erforderlich ist, um nach den richtigen Kontoprofildaten zu suchen und diese anzuzeigen.

Die Möglichkeit, eine direkte Suche durchzuführen, ist unter Umständen nützlich, wenn eine direkte Quellverbindung zu den Daten nicht möglich ist. Wenn Ihr Unternehmen beispielsweise über Data Governance-Richtlinien verfügt, die eine direkte Verbindung zu einem CRM verhindern, können Sie diese Daten in ein Cloud-Speichersystem exportieren und dann in Experience Platform aufnehmen.

Ein weiteres Beispiel könnte sein, dass Sie eine Transformation der Daten zwischen dem Verlassen eines Systems und dem Eintritt in Platform durchführen. Sie können die Funktion für die direkte Suche verwenden, um einen Kontext für die Daten bereitzustellen (z. B. um anzugeben, dass es sich um Marketo-Daten handelt, obwohl es beispielsweise von einem Amazon S3-Bucket stammt), sodass das System weiß, wo die Daten gesucht werden sollen und wie sie korrekt wiedergegeben werden.

Um eine direkte Suche zu starten, wählen Sie **[!UICONTROL Sonstige]** aus dem Dropdown-Menü **[!UICONTROL Durchsuchen nach]** aus, geben Sie dann einen **[!UICONTROL Quellnamen]**, **[!UICONTROL Quellinstanz]** und **[!UICONTROL Konto-ID]** für das Konto ein, das Sie anzeigen möchten.

![](images/b2b-account-browse-adhoc.png)

## Kontoprofildetails anzeigen

Nachdem Sie die Registerkarte **[!UICONTROL Durchsuchen]** zum Suchen eines Kontoprofils verwendet haben, wird durch Auswahl von **[!UICONTROL Profil-ID]** die Registerkarte **[!UICONTROL Detail]** für das Kontoprofil geöffnet. Die auf der Registerkarte **[!UICONTROL Detail]** angezeigten Profilinformationen wurden aus mehreren Profilfragmenten zusammengeführt, um eine einzige Ansicht des einzelnen Kontos zu bilden. Dazu gehören Kontodetails wie grundlegende Attribute und Social-Media-Daten.

Die angezeigten Standardfelder können auch auf Organisationsebene geändert werden, um die bevorzugten Kontoprofilattribute anzuzeigen.

>[!NOTE]
>
>Ähnliche Funktionen sind für Kundenprofile verfügbar. Eine schrittweise Anleitung zum Hinzufügen und Entfernen von Attributen, zum Ändern der Größe von Bedienfeldern usw. wurde erstellt. Weitere Informationen finden Sie im [Handbuch zur Anpassung von Profildetails](../../profile/ui/profile-customization.md) .

![](images/b2b-account-details.png)

Sie können zusätzliche Details zum Konto anzeigen, indem Sie eine andere der verfügbaren Registerkarten auswählen. Diese Registerkarten umfassen Attribute, Personen und die Registerkarte &quot;Chancen&quot;, auf der die offenen und geschlossenen Möglichkeiten für das Konto in Ihren Unternehmenssystemen angezeigt werden. Weitere Informationen zu den einzelnen Registerkarten finden Sie in den folgenden Abschnitten.

## Registerkarte &quot;Attribute&quot;

Auf der Registerkarte **[!UICONTROL Attribute]** werden alle Datensatzinformationen aufgelistet, die sich auf das Konto beziehen. Dazu gehören Attributdaten aus mehreren Quellen, die zusammengeführt wurden, um eine einzige Ansicht des Kontos zu bilden.

Sie können die Daten nicht nur in einer Liste anzeigen, sondern auch in der Suchleiste nach bestimmten Attributen suchen oder die Datensatzdaten als JSON anzeigen.

![](images/b2b-account-attributes.png)

## Personenregisterkarte

Die Registerkarte **[!UICONTROL Personen]** enthält eine Liste der einzelnen Personen, die mit dem Konto verknüpft sind. Diese Personen können Kontakte und Leads aus verschiedenen Unternehmenssystemen sein, die von verschiedenen Teams in Ihrem Unternehmen verwaltet werden. In der Echtzeit-Kundendatenplattform B2B Edition werden sie jedoch in einer Liste zusammengefasst, sodass Sie eine ganzheitlichere Ansicht Ihrer Kontokontakte erhalten.

>[!NOTE]
>
>Auf der Registerkarte [!UICONTROL Personen] wird eine Liste mit bis zu 25 Personen angezeigt, die mit dem Konto verknüpft sind. Bei Konten mit mehr als 25 Personen zeigt das System eine Zufallsauswahl von 25 Datensätzen an.

Neben der Anzeige einer Momentaufnahme der Informationen für den Kontakt enthält jede aufgeführte Person auch eine **[!UICONTROL Profil-ID]**, bei der es sich um einen anklickbaren Link handelt, über den Sie das Echtzeit-Kundenprofil für diese Person ermitteln können. Weitere Informationen zum Anzeigen einzelner Kundenprofile in Bezug auf Ihre Konten finden Sie im Handbuch für [Browsing-Profile in der Echtzeit-Kundendatenplattform, B2B Edition](../profile/profile-browse.md).

![](images/b2b-account-people.png)

## Registerkarte &quot;Chancen&quot;

Der Tab **[!UICONTROL Chancen]** enthält Informationen zu offenen und geschlossenen Gelegenheiten im Zusammenhang mit dem Konto. Diese Möglichkeiten können aus verschiedenen Quellen in die Experience Platform aufgenommen werden. Die Echtzeit-Kundendatenplattform B2B Edition erleichtert es jedoch Marketern, all diese Möglichkeiten an einem Ort zu sehen.

>[!NOTE]
>
>Auf dem Tab [!UICONTROL Chancen] wird eine Liste mit bis zu 25 mit dem Konto verbundenen Möglichkeiten angezeigt. Bei Konten mit mehr als 25 verbundenen Möglichkeiten zeigt das System eine Stichprobe von 25 Datensätzen an.

Jede Gelegenheit umfasst Informationen wie den Namen der Gelegenheit, ihren Umfang, die Phase und ob die Gelegenheit offen, geschlossen, gewonnen oder verloren ist.

![](images/b2b-account-opportunities.png)
