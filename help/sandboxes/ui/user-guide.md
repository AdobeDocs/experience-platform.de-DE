---
keywords: Experience Platform;home;popular topics;sandbox user guide;sandbox guide
solution: Experience Platform
title: Sandbox-Benutzerhandbuch
topic: user guide
description: In diesem Dokument erfahren Sie, wie Sie in der Benutzeroberfläche von Adobe Experience Platform verschiedene Vorgänge im Zusammenhang mit Sandboxes ausführen können.
translation-type: tm+mt
source-git-commit: 2d1a9699866bd39de7251731e9f0cd2f753a5083
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 50%

---


# Sandbox-Benutzerhandbuch

In diesem Dokument erfahren Sie, wie Sie in der Benutzeroberfläche von Adobe Experience Platform verschiedene Vorgänge im Zusammenhang mit Sandboxes ausführen können.

## Anzeigen von Sandboxes

In the Experience Platform UI, select **[!UICONTROL Sandboxes]** in the left-navigation to open the **[!UICONTROL Sandboxes]** dashboard. Im Dashboard werden alle für Ihre Organisation verfügbaren Sandboxes aufgeführt, einschließlich Sandbox-Typ (Produktion oder Entwicklung) und Status (aktiv, wird erstellt, gelöscht oder fehlgeschlagen).

![](../images/ui/view-sandboxes.png)

## Zwischen Sandboxes wechseln

Das Steuerelement **Sandbox-Umschalter** oben links im Bildschirm zeigt die derzeit aktive Sandbox an.

![](../images/ui/sandbox-switcher.png)

Um zwischen Sandboxen zu wechseln, wählen Sie den Sandbox-Umschalter aus und wählen Sie die gewünschte Sandbox aus der Dropdown-Liste aus.

![](../images/ui/switcher-menu.png)

Sobald eine Sandbox ausgewählt ist, wird der Bildschirm aktualisiert; die ausgewählte Sandbox wird jetzt im Sandbox-Umschalter angezeigt.

![](../images/ui/switched.png)

## Suchen nach einer Sandbox

Sie können über die Suchfunktion im Menü &quot;Sandbox-Umschalter&quot;durch die Liste der Ihnen zur Verfügung stehenden Sandboxen navigieren. Geben Sie den Namen der Sandbox ein, auf die Sie zugreifen möchten, um durch alle für Ihr Unternehmen verfügbaren Sandboxen zu filtern.

![](../images/ui/sandbox-search.png)

## Neue Sandbox erstellen

Im folgenden Video erhalten Sie einen schnellen Überblick über die Verwendung von Sandboxen in der Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Um eine neue Sandbox in der Benutzeroberfläche zu erstellen, klicken Sie oben rechts im Bildschirm auf die Schaltfläche &quot;Sandbox **[!UICONTROL erstellen]** &quot;.

![](../images/ui/create-sandbox.png)

Der Dialog **[!UICONTROL Sandbox erstellen]** wird angezeigt, in dem Sie aufgefordert werden, einen Anzeigetitel und einen Namen für die Sandbox anzugeben. Der **Anzeigetitel** sollte für Menschen lesbar und deskriptiv genug sein, damit er leicht zu erkennen ist. The sandbox **[!UICONTROL Name]** is an all-lowercase identifier for use in API calls, and should therefore be unique and concise. Der **[!UICONTROL Name]** der Sandbox darf nur aus alphanumerischen Zeichen und Bindestrichen **(-)** bestehen, muss mit einem Buchstaben beginnen und darf nicht länger als 256 Zeichen sein.

When finished, select **[!UICONTROL Create]**.

![](../images/ui/create-dialog.png)

>[!NOTE]
>
>Da Sie nur Nicht-Produktions-Sandboxes erstellen können, ist die Option **[!UICONTROL Typ]** bei „Nicht-Produktion“ gesperrt und kann nicht bearbeitet werden.

Once you have finished creating the sandbox, refresh the page and the new sandbox appears in the **[!UICONTROL Sandboxes]** dashboard with a status of &quot;[!UICONTROL Creating]&quot;. New sandboxes take approximately 15 minutes to be provisioned by the system, after which their status changes to &quot;[!UICONTROL Active]&quot;.

![](../images/ui/creating.png)

## Zurücksetzen einer Sandbox

>[!NOTE]
>
> Diese Funktion ist nur bei Nicht-Produktions-Sandboxes verfügbar. Produktions-Sandboxes können nicht zurückgesetzt werden.

Beim Zurücksetzen einer Nicht-Produktions-Sandbox werden alle mit dieser Sandbox verbundenen Ressourcen (Schemas, Datensätze usw.) gelöscht, wobei der Name der Sandbox und die zugehörigen Berechtigungen beibehalten werden. Diese „saubere“ Sandbox ist für Benutzer, die Zugriff darauf haben, unter demselben Namen weiter verfügbar.

To reset a sandbox in the UI, select **[!UICONTROL Sandboxes]** in the left-nav, then select the sandbox you want to reset. In the dialog that appears on the right-hand side of the screen, select **[!UICONTROL Reset Sandbox]**.

![](../images/ui/reset-sandbox.png)

Es wird ein Dialog angezeigt, in dem Sie aufgefordert werden, Ihre Auswahl zu bestätigen. Select **[!UICONTROL Reset]** to continue.

![](../images/ui/reset-confirm.png)

A confirmation message appears and the sandbox&#39;s state changes to &quot;**[!UICONTROL Resetting]&quot;**. Once it has been provisioned by the system, its state will update to **&quot;[!UICONTROL Active]&quot;** or **&quot;[!UICONTROL Failed]&quot;**.

![](../images/ui/resetting.png)

## Sandbox löschen

>[!NOTE]
>
> Diese Funktion ist nur bei Nicht-Produktions-Sandboxes verfügbar. Produktions-Sandboxes können nicht gelöscht werden.

Wenn Sie eine Nicht-Produktions-Sandbox löschen, werden alle mit dieser Sandbox verbundenen Ressourcen (einschließlich Berechtigungen) endgültig gelöscht.

To delete a sandbox in the UI, select **[!UICONTROL Sandboxes]** in the left-nav, then select the sandbox you want to delete. In the dialog that appears on the right-hand side of the screen, select **[!UICONTROL Delete Sandbox]**.

![](../images/ui/delete-sandbox.png)

Es wird ein Dialog angezeigt, in dem Sie aufgefordert werden, Ihre Auswahl zu bestätigen. Select **[!UICONTROL Delete]** to continue.

![](../images/ui/delete-confirm.png)

Eine Bestätigungsmeldung wird angezeigt und die Sandbox wird aus dem Arbeitsbereich **[!UICONTROL Sandboxes]** entfernt.

## Nächste Schritte

In diesem Dokument haben Sie erfahren, wie Sie Sandboxes in der Benutzeroberfläche von Experience Platform verwalten können. Informationen zum Verwalten von Sandboxes mithilfe der Sandbox-API finden Sie im [Sandbox-Entwicklerhandbuch](../api/getting-started.md).