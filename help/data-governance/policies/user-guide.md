---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Benutzerhandbuch zu Datenverwendungsrichtlinien
topic: policies
translation-type: tm+mt
source-git-commit: 235a43ad72dee45db1b3d35ae84ce9a1c4d729b8

---


# Benutzerhandbuch zu Datenverwendungsrichtlinien

Adobe Experience Platform Data Governance bietet eine Benutzeroberfläche, über die Sie Datennutzungsrichtlinien erstellen und verwalten können. Dieses Dokument bietet einen Überblick über die Aktionen, die Sie im Arbeitsbereich &quot; _Richtlinien_ &quot;der Experience Platform-Benutzeroberfläche durchführen können.

## Voraussetzungen

Dieses Handbuch erfordert ein Verständnis der folgenden Konzepte der Erlebnisplattform:

- [Data Governance](../home.md)
- [Datenverwendungsrichtlinien](./overview.md)

## Ansicht-Datenverwendungsrichtlinien

Klicken Sie in der Benutzeroberfläche von Experience Platform auf **[!UICONTROL Policies]** , um den *[!UICONTROL Policies]* Arbeitsbereich zu öffnen. Auf der **[!UICONTROL Browse]** Registerkarte können Sie eine Liste der verfügbaren Richtlinien einschließlich der zugehörigen Beschriftungen, Marketingaktionen und Status anzeigen.

![](../images/policies/browse-policies.png)

Klicken Sie auf eine aufgelistete Richtlinie, um deren Beschreibung und Typ Ansicht. Wenn eine benutzerdefinierte Richtlinie ausgewählt ist, werden zusätzliche Steuerelemente angezeigt, um die Richtlinie zu bearbeiten, zu löschen oder zu [aktivieren/deaktivieren](#enable).

![](../images/policies/policy-details.png)

## Benutzerdefinierte Datenverwendungsrichtlinie erstellen

Um eine neue Richtlinie zur Verwendung benutzerdefinierter Daten zu erstellen, klicken Sie in der oberen rechten Ecke des Arbeitsbereichs &quot; **[!UICONTROL Create policy]** Richtlinien ** &quot;auf .

![](../images/policies/create-policy-button.png)

Der *[!UICONTROL Create policy]* Workflow wird angezeigt. Beginn durch Angabe eines Namens und einer Beschreibung der neuen Richtlinie.

![](../images/policies/create-policy-description.png)

Wählen Sie anschließend die Datenverwendungsbeschriftungen aus, auf denen die Richtlinie basieren soll. Wenn Sie mehrere Bezeichnungen auswählen, können Sie festlegen, ob die Daten alle oder nur eine der Bezeichnungen enthalten sollen, damit die Richtlinie angewendet werden kann. Klicken Sie zum Fertigstellen auf **[!UICONTROL Next]**.

![](../images/policies/add-labels.png)

Der *[!UICONTROL Select marketing actions]* Schritt wird angezeigt. Wählen Sie die entsprechenden Marketingaktionen aus der bereitgestellten Liste und klicken Sie dann auf **[!UICONTROL Next]** , um fortzufahren.

>[!NOTE] Bei der Auswahl mehrerer Marketingaktionen interpretiert die Richtlinie diese als &quot;OR&quot;-Regel. Mit anderen Worten, die Richtlinie gilt, wenn _eine_ der ausgewählten Marketingaktionen durchgeführt wird.

![](../images/policies/add-marketing-actions.png)

Der *[!UICONTROL Review]* Schritt wird angezeigt, damit Sie die Details der neuen Richtlinie überprüfen können, bevor Sie sie erstellen. Nachdem Sie zufrieden sind, klicken Sie auf **[!UICONTROL Finish]** , um die Richtlinie zu erstellen.

![](../images/policies/policy-review.png)

Die *[!UICONTROL Browse]* Registerkarte wird wieder angezeigt, wodurch die neu erstellte Richtlinie nun im Status &quot;Entwurf&quot;Liste wird. Informationen zum Aktivieren der Richtlinie finden Sie im nächsten Abschnitt.

![](../images/policies/created-policy.png)

## Datenschutzrichtlinien aktivieren oder deaktivieren {#enable}

Sie können benutzerdefinierte Datenverwendungsrichtlinien auf der *[!UICONTROL Browse]* Registerkarte im *[!UICONTROL Policies]* Arbeitsbereich aktivieren oder deaktivieren. Wählen Sie eine benutzerdefinierte Richtlinie aus der Liste, um die Details auf der rechten Seite anzuzeigen. Klicken Sie unter *[!UICONTROL Status]* die Schaltfläche zum Umschalten, um die Richtlinie zu aktivieren oder zu deaktivieren.

![](../images/policies/enable-policy.png)

## Nächste Schritte

Dieses Dokument gab einen Überblick darüber, wie Datenverwendungsrichtlinien in der Benutzeroberfläche von Experience Platform verwaltet werden. Anweisungen zum Verwalten von Richtlinien mit der DUL-Richtlinie-API finden Sie im [Entwicklerhandbuch](../api/getting-started.md). Informationen zum Erzwingen von Datenverwendungsrichtlinien finden Sie in der Übersicht über die [Richtliniendurchsetzung](../enforcement/overview.md).