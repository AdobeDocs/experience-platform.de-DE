---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Benutzerhandbuch zu Datenverwendungsrichtlinien
topic: policies
translation-type: tm+mt
source-git-commit: c4554e3fbc0dd527606b81e2767cb5777b6e81e7
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 1%

---


# Benutzerhandbuch zu Datenverwendungsrichtlinien

Adobe Experience Platform Data Governance bietet eine Benutzeroberfläche, über die Sie Datennutzungsrichtlinien erstellen und verwalten können. Dieses Dokument bietet einen Überblick über die Aktionen, die Sie in der Benutzeroberfläche &quot;Experience Platform&quot;im Arbeitsbereich &quot; _Richtlinien_ &quot;ausführen können.

>[!IMPORTANT] Alle Datenverwendungsrichtlinien (einschließlich der von Adobe bereitgestellten Core-Richtlinien) sind standardmäßig deaktiviert. Damit eine einzelne Richtlinie zur Durchsetzung in Betracht gezogen werden kann, müssen Sie diese Richtlinie manuell aktivieren. Anweisungen dazu finden Sie im Abschnitt zum [Aktivieren von Richtlinien](#enable) in der Benutzeroberfläche.

## Voraussetzungen

Dieser Leitfaden erfordert ein Verständnis der folgenden Konzepte der Experience Platform:

- [Data Governance](../home.md)
- [Datenverwendungsrichtlinien](./overview.md)

## Ansicht-Datenverwendungsrichtlinien {#view-policies}

Klicken Sie in der Benutzeroberfläche &quot;Experience Platform&quot;auf **[!UICONTROL Richtlinien]** , um den Arbeitsbereich &quot; *[!UICONTROL Richtlinien]* &quot;zu öffnen. Auf der Registerkarte &quot; **[!UICONTROL Durchsuchen]** &quot;wird eine Liste der verfügbaren Richtlinien angezeigt, einschließlich der zugehörigen Beschriftungen, Marketingaktionen und Status.

![](../images/policies/browse-policies.png)

Klicken Sie auf eine aufgelistete Richtlinie, um deren Beschreibung und Typ Ansicht. Wenn eine benutzerdefinierte Richtlinie ausgewählt ist, werden zusätzliche Steuerelemente angezeigt, um die Richtlinie zu bearbeiten, zu löschen oder zu [aktivieren/deaktivieren](#enable).

![](../images/policies/policy-details.png)

## Benutzerdefinierte Datenverwendungsrichtlinie erstellen {#create-policy}

Um eine neue Richtlinie zur Verwendung benutzerdefinierter Daten zu erstellen, klicken Sie auf Richtlinie **** erstellen in der oberen rechten Ecke der Registerkarte &quot; **[!UICONTROL Durchsuchen]** &quot;im Arbeitsbereich &quot; *Richtlinien* &quot;.

![](../images/policies/create-policy-button.png)

Der Arbeitsablauf zum *[!UICONTROL Erstellen von Richtlinien]* wird angezeigt. Beginn durch Angabe eines Namens und einer Beschreibung der neuen Richtlinie.

![](../images/policies/create-policy-description.png)

Wählen Sie anschließend die Datenverwendungsbeschriftungen aus, auf denen die Richtlinie basieren soll. Wenn Sie mehrere Bezeichnungen auswählen, können Sie festlegen, ob die Daten alle oder nur eine der Bezeichnungen enthalten sollen, damit die Richtlinie angewendet werden kann. Klicken Sie auf **[!UICONTROL Weiter]**, wenn Sie fertig sind.

![](../images/policies/add-labels.png)

Der Schritt Marketingaktionen *[!UICONTROL auswählen]* wird angezeigt. Wählen Sie die entsprechenden Marketingaktionen aus der bereitgestellten Liste und klicken Sie dann auf **[!UICONTROL Weiter]** , um fortzufahren.

>[!NOTE] Bei der Auswahl mehrerer Marketingaktionen interpretiert die Richtlinie diese als &quot;OR&quot;-Regel. Mit anderen Worten, die Richtlinie gilt, wenn _eine_ der ausgewählten Marketingaktionen durchgeführt wird.

![](../images/policies/add-marketing-actions.png)

Der Schritt *[!UICONTROL Überprüfung]* wird angezeigt, mit dem Sie die Details der neuen Richtlinie überprüfen können, bevor Sie sie erstellen. Wenn Sie zufrieden sind, klicken Sie auf **[!UICONTROL Fertig stellen]** , um die Richtlinie zu erstellen.

![](../images/policies/policy-review.png)

Die Registerkarte &quot; *[!UICONTROL Durchsuchen]* &quot;wird wieder angezeigt, wodurch die neu erstellte Richtlinie jetzt im Status &quot;Entwurf&quot;Liste wird. Informationen zum Aktivieren der Richtlinie finden Sie im nächsten Abschnitt.

![](../images/policies/created-policy.png)

## Datenschutzrichtlinien aktivieren oder deaktivieren {#enable}

Alle Datenverwendungsrichtlinien (einschließlich der von Adobe bereitgestellten Core-Richtlinien) sind standardmäßig deaktiviert. Damit eine einzelne Richtlinie zur Durchsetzung in Betracht gezogen werden kann, müssen Sie diese Richtlinie manuell über die API oder Benutzeroberfläche aktivieren.

Sie können Richtlinien auf der Registerkarte &quot; *[!UICONTROL Durchsuchen]* &quot;im Arbeitsbereich &quot; *[!UICONTROL Richtlinien]* &quot;aktivieren oder deaktivieren. Wählen Sie eine benutzerdefinierte Richtlinie aus der Liste, um die Details auf der rechten Seite anzuzeigen. Klicken Sie unter *[!UICONTROL Status]* auf die Schaltfläche zum Umschalten, um die Richtlinie zu aktivieren oder zu deaktivieren.

![](../images/policies/enable-policy.png)

## Marketingaktionen für Ansichten {#view-marketing-actions}

Wählen Sie im Arbeitsbereich &quot; **[!UICONTROL Richtlinien]** &quot;die Registerkarte &quot; **[!UICONTROL Marketingaktionen]** &quot;aus, um eine Liste der verfügbaren Marketingaktionen Ansicht, die von Adobe und Ihrem eigenen Unternehmen definiert wurden.

![](../images/policies/marketing-actions.png)

## Erstellen einer Marketingaktion {#create-marketing-action}

Um eine neue benutzerdefinierte Marketingaktion zu erstellen, klicken Sie auf Marketingaktion **** erstellen in der oberen rechten Ecke der Registerkarte &quot; **[!UICONTROL Marketingaktionen]** &quot;im Arbeitsbereich &quot; *[!UICONTROL Richtlinien]* &quot;.

![](../images/policies/create-marketing-action.png)

Das Dialogfeld *[!UICONTROL Marketingaktion]* erstellen wird angezeigt. Geben Sie einen Namen und eine Beschreibung für die Marketingaktion ein und klicken Sie dann auf **[!UICONTROL Erstellen]**.

![](../images/policies/create-marketing-action-details.png)

Die neu erstellte Aktion wird auf der Registerkarte &quot; *[!UICONTROL Marketingaktionen]* &quot;angezeigt. Sie können die Marketingaktion jetzt beim [Erstellen neuer Datenverwendungsrichtlinien](#create-policy)verwenden.

![](../images/policies/created-marketing-action.png)

## Bearbeiten oder Löschen einer Marketingaktion {#edit-delete-marketing-action}

>[!NOTE] Es können nur benutzerdefinierte Marketingaktionen bearbeitet werden, die von Ihrer Organisation definiert wurden. Von Adobe definierte Marketingaktionen können nicht geändert oder gelöscht werden.

Wählen Sie im Arbeitsbereich &quot; **[!UICONTROL Richtlinien]** &quot;die Registerkarte &quot; **[!UICONTROL Marketingaktionen]** &quot;aus, um eine Liste der verfügbaren Marketingaktionen Ansicht, die von Adobe und Ihrem eigenen Unternehmen definiert wurden. Wählen Sie eine benutzerdefinierte Marketingaktion aus der Liste und bearbeiten Sie dann die Details der Marketingaktion mit den entsprechenden Feldern im rechten Bereich.

![](../images/policies/edit-marketing-action.png)

Wenn die Marketingaktion nicht von vorhandenen Nutzungsrichtlinien verwendet wird, können Sie sie löschen, indem Sie auf Marketingaktion **[!UICONTROL löschen klicken]**.

>[!NOTE] Beim Versuch, eine Marketingaktion zu löschen, die von einer vorhandenen Richtlinie verwendet wird, wird eine Fehlermeldung angezeigt, die darauf hinweist, dass der Löschversuch fehlgeschlagen ist.

![](../images/policies/delete-marketing-action.png)

## Nächste Schritte

Dieses Dokument gab einen Überblick darüber, wie Datenverwendungsrichtlinien in der Benutzeroberfläche der Experience Platform verwaltet werden. Anweisungen zum Verwalten von Richtlinien mit der DUL-Richtlinie-API finden Sie im [Entwicklerhandbuch](../api/getting-started.md). Informationen zum Erzwingen von Datenverwendungsrichtlinien finden Sie in der Übersicht über die [Richtliniendurchsetzung](../enforcement/overview.md).

Im folgenden Video wird gezeigt, wie mit Nutzungsrichtlinien in der Benutzeroberfläche der Experience Platform gearbeitet wird:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)