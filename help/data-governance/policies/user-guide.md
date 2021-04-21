---
keywords: Experience Platform;Startseite;beliebte Themen;Datenverwaltung;Benutzerhandbuch zur Datenverwendungsrichtlinie
solution: Experience Platform
title: Verwalten von Datennutzungsrichtlinien in der Benutzeroberfläche
topic-legacy: policies
description: Adobe Experience Platform Data Governance bietet eine Benutzeroberfläche, über die Sie Datennutzungsrichtlinien erstellen und verwalten können. Dieses Dokument bietet einen Überblick über die Aktionen, die Sie in der Benutzeroberfläche "Experience Platform"im Arbeitsbereich "Richtlinien"ausführen können.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 31%

---

# Datennutzungsrichtlinien in der Benutzeroberfläche verwalten

Adobe Experience Platform [!DNL Data Governance] bietet eine Benutzeroberfläche, über die Sie Datenverwendungsrichtlinien erstellen und verwalten können. Dieses Dokument bietet einen Überblick über die Aktionen, die Sie in der **Richtlinien**-Arbeitsfläche der [!DNL Experience Platform]-Benutzeroberfläche ausführen können.

>[!IMPORTANT]
>
>Alle Datenverwendungsrichtlinien (einschließlich der von der Adobe bereitgestellten Kernrichtlinien) sind standardmäßig deaktiviert. Damit eine einzelne Richtlinie zur Durchsetzung in Betracht gezogen werden kann, müssen Sie diese Richtlinie manuell aktivieren. Anweisungen dazu finden Sie im Abschnitt [Aktivieren von Richtlinien](#enable) in der Benutzeroberfläche.

## Voraussetzungen

Dieses Handbuch erfordert ein funktionierendes Verständnis der folgenden [!DNL Experience Platform]-Konzepte:

- [[!DNL Data Governance]](../home.md)
- [Datennutzungsrichtlinien](./overview.md)

## Ansicht bestehender Richtlinien {#view-policies}

Wählen Sie in der Benutzeroberfläche [!DNL Experience Platform] **[!UICONTROL Richtlinien]** aus, um den Arbeitsbereich **[!UICONTROL Richtlinien]** zu öffnen. Auf der Registerkarte **[!UICONTROL Durchsuchen]** wird eine Liste der verfügbaren Richtlinien angezeigt, einschließlich der zugehörigen Bezeichnungen, Marketing-Aktionen und Status.

![](../images/policies/browse-policies.png)

Wählen Sie eine aufgelistete Richtlinie aus, um deren Beschreibung und Typ Ansicht. Wenn eine benutzerdefinierte Richtlinie ausgewählt ist, werden zusätzliche Steuerelemente zum Bearbeiten, Löschen oder [Aktivieren/Deaktivieren der Richtlinie](#enable) angezeigt.

![](../images/policies/policy-details.png)

## Erstellen einer benutzerdefinierten Richtlinie {#create-policy}

Um eine neue benutzerdefinierte Datenverwendungsrichtlinie zu erstellen, wählen Sie **[!UICONTROL Richtlinie erstellen]** in der oberen rechten Ecke der Registerkarte **[!UICONTROL Durchsuchen]** im Arbeitsbereich **[!UICONTROL Richtlinien]**.

![](../images/policies/create-policy-button.png)

Der Workflow **[!UICONTROL Richtlinie erstellen]** wird angezeigt. Geben Sie zunächst einen Namen und eine Beschreibung für die neue Richtlinie an.

![](../images/policies/create-policy-description.png)

Wählen Sie anschließend die Datennutzungsbezeichnungen aus, auf denen die Richtlinie basieren soll. Wenn Sie mehrere Bezeichnungen auswählen, können Sie entscheiden, ob die Daten alle Bezeichnungen oder nur eine der Bezeichnungen enthalten müssen, damit die Richtlinie angewendet wird. Wählen Sie **[!UICONTROL Weiter]**, wenn Sie fertig sind.

![](../images/policies/add-labels.png)

Der Schritt **[!UICONTROL Marketing-Aktionen auswählen]** wird angezeigt. Wählen Sie in der bereitgestellten Liste die entsprechenden Marketingaktionen und dann **[!UICONTROL Weiter]** aus, um fortzufahren.

>[!NOTE]
>
> Bei Auswahl mehrerer Marketing-Aktionen interpretiert die Richtlinie diese als „OR“-Regel. Mit anderen Worten: Die Richtlinie findet Anwendung, wenn **beliebige** der ausgewählten Marketing-Aktionen ausgeführt werden.

![](../images/policies/add-marketing-actions.png)

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, in dem Sie die Details der neuen Richtlinie vor der Erstellung überprüfen können. Wenn Sie zufrieden sind, wählen Sie **[!UICONTROL Fertig stellen]**, um die Richtlinie zu erstellen.

![](../images/policies/policy-review.png)

Die Registerkarte **[!UICONTROL Durchsuchen]** wird erneut angezeigt, wo die neu erstellte Richtlinie jetzt mit dem Status „Entwurf“ aufgelistet wird. Informationen zum Aktivieren der Richtlinie finden Sie im nächsten Abschnitt.

![](../images/policies/created-policy.png)

## Aktivieren oder Deaktivieren einer Richtlinie {#enable}

Alle Datenverwendungsrichtlinien (einschließlich der von der Adobe bereitgestellten Kernrichtlinien) sind standardmäßig deaktiviert. Damit eine einzelne Richtlinie zur Durchsetzung in Betracht gezogen werden kann, müssen Sie diese Richtlinie manuell über die API oder Benutzeroberfläche aktivieren.

Sie können Richtlinien auf der Registerkarte **[!UICONTROL Durchsuchen]** im Arbeitsbereich **[!UICONTROL Richtlinien]** aktivieren oder deaktivieren. Wählen Sie eine benutzerdefinierte Richtlinie aus der Liste, um auf der rechten Seite die entsprechenden Details anzuzeigen. Klicken Sie unter **[!UICONTROL Status]** auf die Schaltfläche zum Umschalten, um die Richtlinie zu aktivieren oder zu deaktivieren.

![](../images/policies/enable-policy.png)

## Ansicht-Marketingaktionen {#view-marketing-actions}

Wählen Sie im Arbeitsbereich **[!UICONTROL Richtlinien]** die Registerkarte **[!UICONTROL Marketingaktionen]**, um eine Liste der verfügbaren Marketingaktionen Ansicht, die von der Adobe und Ihrem eigenen Unternehmen definiert werden.

![](../images/policies/marketing-actions.png)

## Erstellen einer Marketingaktion {#create-marketing-action}

Um eine neue benutzerdefinierte Marketingaktion zu erstellen, wählen Sie **[!UICONTROL Marketingaktion erstellen]** in der oberen rechten Ecke der Registerkarte **[!UICONTROL Marketingaktionen]** im Arbeitsbereich **[!UICONTROL Richtlinien]**.

![](../images/policies/create-marketing-action.png)

Das Dialogfeld **[!UICONTROL Marketingaktion erstellen]** wird angezeigt. Geben Sie einen Namen und eine Beschreibung für die Marketingaktion ein und wählen Sie **[!UICONTROL Erstellen]**.

![](../images/policies/create-marketing-action-details.png)

Die neu erstellte Aktion wird auf der Registerkarte **[!UICONTROL Marketingaktionen]** angezeigt. Sie können die Marketingaktion jetzt verwenden, wenn [Sie neue Datenverwendungsrichtlinien](#create-policy) erstellen.

![](../images/policies/created-marketing-action.png)

## Bearbeiten oder Löschen einer Marketingaktion {#edit-delete-marketing-action}

>[!NOTE]
>
>Es können nur benutzerdefinierte Marketingaktionen bearbeitet werden, die von Ihrer Organisation definiert wurden. Durch Adobe definierte Marketingaktionen können nicht geändert oder gelöscht werden.

Wählen Sie im Arbeitsbereich **[!UICONTROL Richtlinien]** die Registerkarte **[!UICONTROL Marketingaktionen]**, um eine Liste der verfügbaren Marketingaktionen Ansicht, die von der Adobe und Ihrem eigenen Unternehmen definiert werden. Wählen Sie eine benutzerdefinierte Marketingaktion aus der Liste und bearbeiten Sie dann die Details der Marketingaktion mit den entsprechenden Feldern im rechten Bereich.

![](../images/policies/edit-marketing-action.png)

Wenn die Marketingaktion von keiner der vorhandenen Nutzungsrichtlinien verwendet wird, können Sie sie löschen, indem Sie **[!UICONTROL Marketingaktion]** löschen auswählen.

>[!NOTE]
>
>Beim Versuch, eine Marketingaktion zu löschen, die von einer vorhandenen Richtlinie verwendet wird, wird eine Fehlermeldung angezeigt, die darauf hinweist, dass der Löschversuch fehlgeschlagen ist.

![](../images/policies/delete-marketing-action.png)

## Nächste Schritte

Dieses Dokument gab einen Überblick darüber, wie Datenverwendungsrichtlinien in der [!DNL Experience Platform]-Benutzeroberfläche verwaltet werden. Anweisungen zum Verwalten von Richtlinien mit [!DNL Policy Service API] finden Sie im [Entwicklerhandbuch](../api/getting-started.md). Informationen zum Erzwingen von Datennutzungsrichtlinien finden Sie in der [Übersicht zur Durchsetzung von Richtlinien](../enforcement/overview.md).

Das folgende Video zeigt, wie mit Nutzungsrichtlinien in der [!DNL Experience Platform]-Benutzeroberfläche gearbeitet wird:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
