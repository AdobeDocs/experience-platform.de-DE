---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Benutzerhandbuch zu Datennutzungsrichtlinien
topic: policies
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 39%

---


# Benutzerhandbuch zu Datennutzungsrichtlinien

Adobe Experience Platform [!DNL Data Governance] provides a user interface that allows you to create and manage data usage policies. This document provides an overview of the actions you can perform in the _Policies_ workspace in the [!DNL Experience Platform] user interface.

>[!IMPORTANT]
>
>Alle Datenverwendungsrichtlinien (einschließlich der von Adobe bereitgestellten Core-Richtlinien) sind standardmäßig deaktiviert. Damit eine einzelne Richtlinie zur Durchsetzung in Betracht gezogen werden kann, müssen Sie diese Richtlinie manuell aktivieren. Anweisungen dazu finden Sie im Abschnitt zum [Aktivieren von Richtlinien](#enable) in der Benutzeroberfläche.

## Voraussetzungen

This guide requires a working understanding of the following [!DNL Experience Platform] concepts:

- [!DNL Data Governance](../home.md)
- [Datennutzungsrichtlinien](./overview.md)

## Datennutzungsrichtlinien anzeigen {#view-policies}

In the [!DNL Experience Platform] UI, click **[!UICONTROL Policies]** to open the *[!UICONTROL Policies]* workspace. Auf der Registerkarte **[!UICONTROL Durchsuchen]** wird eine Liste der verfügbaren Richtlinien angezeigt, einschließlich der zugehörigen Bezeichnungen, Marketing-Aktionen und Status.

![](../images/policies/browse-policies.png)

Klicken Sie auf eine aufgelistete Richtlinie, um deren Beschreibung und Typ anzuzeigen. Wenn eine benutzerdefinierte Richtlinie ausgewählt ist, werden zusätzliche Steuerelemente zum Bearbeiten, Löschen oder [Aktivieren/Deaktivieren der Richtlinie](#enable) angezeigt.

![](../images/policies/policy-details.png)

## Benutzerdefinierte Datennutzungsrichtlinie erstellen {#create-policy}

To create a new custom data usage policy, click **[!UICONTROL Create policy]** in the top-right corner of the **[!UICONTROL Browse]** tab in the *[!UICONTROL Policies]* workspace.

![](../images/policies/create-policy-button.png)

Der Workflow *[!UICONTROL Richtlinie erstellen]* wird angezeigt. Geben Sie zunächst einen Namen und eine Beschreibung für die neue Richtlinie an.

![](../images/policies/create-policy-description.png)

Wählen Sie anschließend die Datennutzungsbezeichnungen aus, auf denen die Richtlinie basieren soll. Wenn Sie mehrere Bezeichnungen auswählen, können Sie entscheiden, ob die Daten alle Bezeichnungen oder nur eine der Bezeichnungen enthalten müssen, damit die Richtlinie angewendet wird. Klicken Sie auf **[!UICONTROL Weiter]**, wenn Sie fertig sind.

![](../images/policies/add-labels.png)

Der Schritt *[!UICONTROL Marketing-Aktionen auswählen]* wird angezeigt. Wählen Sie die entsprechenden Marketing-Aktionen aus der bereitgestellten Liste und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

>[!NOTE]
>
>Bei Auswahl mehrerer Marketing-Aktionen interpretiert die Richtlinie diese als „OR“-Regel. Mit anderen Worten: Die Richtlinie findet Anwendung, wenn _beliebige_ der ausgewählten Marketing-Aktionen ausgeführt werden.

![](../images/policies/add-marketing-actions.png)

Der Schritt *[!UICONTROL Überprüfung]* wird angezeigt, in dem Sie die Details der neuen Richtlinie vor der Erstellung überprüfen können. Wenn Sie zufrieden sind, klicken Sie auf **[!UICONTROL Fertig stellen]**, um die Richtlinie zu erstellen.

![](../images/policies/policy-review.png)

Die Registerkarte *[!UICONTROL Durchsuchen]* wird erneut angezeigt, wo die neu erstellte Richtlinie jetzt mit dem Status „Entwurf“ aufgelistet wird. Informationen zum Aktivieren der Richtlinie finden Sie im nächsten Abschnitt.

![](../images/policies/created-policy.png)

## Datennutzungsrichtlinie aktivieren oder deaktivieren {#enable}

Alle Datenverwendungsrichtlinien (einschließlich der von Adobe bereitgestellten Core-Richtlinien) sind standardmäßig deaktiviert. Damit eine einzelne Richtlinie zur Durchsetzung in Betracht gezogen werden kann, müssen Sie diese Richtlinie manuell über die API oder Benutzeroberfläche aktivieren.

You can enable or disable policies from the *[!UICONTROL Browse]* tab in the *[!UICONTROL Policies]* workspace. Wählen Sie eine benutzerdefinierte Richtlinie aus der Liste, um auf der rechten Seite die entsprechenden Details anzuzeigen. Klicken Sie unter *[!UICONTROL Status]* auf die Schaltfläche zum Umschalten, um die Richtlinie zu aktivieren oder zu deaktivieren.

![](../images/policies/enable-policy.png)

## Marketingaktionen für Ansichten {#view-marketing-actions}

Wählen Sie im Arbeitsbereich &quot; **[!UICONTROL Richtlinien]** &quot;die Registerkarte &quot; **[!UICONTROL Marketingaktionen]** &quot;aus, um eine Liste der verfügbaren Marketingaktionen Ansicht, die von Adobe und Ihrem eigenen Unternehmen definiert wurden.

![](../images/policies/marketing-actions.png)

## Create a marketing action {#create-marketing-action}

Um eine neue benutzerdefinierte Marketingaktion zu erstellen, klicken Sie auf Marketingaktion **** erstellen in der oberen rechten Ecke der Registerkarte &quot; **[!UICONTROL Marketingaktionen]** &quot;im Arbeitsbereich &quot; *[!UICONTROL Richtlinien]* &quot;.

![](../images/policies/create-marketing-action.png)

Das Dialogfeld *[!UICONTROL Marketingaktion]* erstellen wird angezeigt. Geben Sie einen Namen und eine Beschreibung für die Marketingaktion ein und klicken Sie dann auf **[!UICONTROL Erstellen]**.

![](../images/policies/create-marketing-action-details.png)

Die neu erstellte Aktion wird auf der Registerkarte &quot; *[!UICONTROL Marketingaktionen]* &quot;angezeigt. Sie können die Marketingaktion jetzt beim [Erstellen neuer Datenverwendungsrichtlinien](#create-policy)verwenden.

![](../images/policies/created-marketing-action.png)

## Bearbeiten oder Löschen einer Marketingaktion {#edit-delete-marketing-action}

>[!NOTE]
>
>Es können nur benutzerdefinierte Marketingaktionen bearbeitet werden, die von Ihrer Organisation definiert wurden. Von Adobe definierte Marketingaktionen können nicht geändert oder gelöscht werden.

Wählen Sie im Arbeitsbereich &quot; **[!UICONTROL Richtlinien]** &quot;die Registerkarte &quot; **[!UICONTROL Marketingaktionen]** &quot;aus, um eine Liste der verfügbaren Marketingaktionen Ansicht, die von Adobe und Ihrem eigenen Unternehmen definiert wurden. Wählen Sie eine benutzerdefinierte Marketingaktion aus der Liste und bearbeiten Sie dann die Details der Marketingaktion mit den entsprechenden Feldern im rechten Bereich.

![](../images/policies/edit-marketing-action.png)

Wenn die Marketingaktion nicht von vorhandenen Nutzungsrichtlinien verwendet wird, können Sie sie löschen, indem Sie auf Marketingaktion **[!UICONTROL löschen klicken]**.

>[!NOTE]
>
>Beim Versuch, eine Marketingaktion zu löschen, die von einer vorhandenen Richtlinie verwendet wird, wird eine Fehlermeldung angezeigt, die darauf hinweist, dass der Löschversuch fehlgeschlagen ist.

![](../images/policies/delete-marketing-action.png)

## Nächste Schritte

This document provided an overview of how to manage data usage policies in [!DNL Experience Platform] UI. For steps on how to manage policies using the DULE Policy API, see the [developer guide](../api/getting-started.md). Informationen zum Erzwingen von Datennutzungsrichtlinien finden Sie in der [Übersicht zur Durchsetzung von Richtlinien](../enforcement/overview.md).

Das folgende Video zeigt, wie mit Nutzungsrichtlinien in der [!DNL Experience Platform] Benutzeroberfläche gearbeitet wird:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)