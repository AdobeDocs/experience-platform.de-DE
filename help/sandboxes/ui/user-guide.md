---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sandbox-Benutzerhandbuch
topic: user guide
translation-type: tm+mt
source-git-commit: c52d8cdbc5a4ee6fab8c2b1b284efea5f735d424
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 80%

---


# Sandbox-Benutzerhandbuch

In diesem Dokument erfahren Sie, wie Sie in der Benutzeroberfläche von Adobe Experience Platform verschiedene Vorgänge im Zusammenhang mit Sandboxes ausführen können.

## Anzeigen von Sandboxes

Klicken Sie in der Benutzeroberfläche von Experience Platform im linken Navigationsbereich auf **[!UICONTROL Sandboxes]**, um das Dashboard _[!UICONTROL Sandboxes]_zu öffnen. Im Dashboard werden alle für Ihre Organisation verfügbaren Sandboxes aufgeführt, einschließlich Sandbox-Typ (Produktion oder Entwicklung) und Status (aktiv, wird erstellt, gelöscht oder fehlgeschlagen).

![](../images/ui/sandboxes-tab.png)

## Zwischen Sandboxes wechseln

Das Steuerelement **Sandbox-Umschalter** oben links im Bildschirm zeigt die derzeit aktive Sandbox an.

![](../images/ui/sandbox-selector.png)

Um zwischen Sandboxes zu wechseln, klicken Sie auf den Sandbox-Umschalter und wählen Sie die gewünschte Sandbox aus der Dropdown-Liste aus.

![](../images/ui/switch-sandbox.png)

Sobald eine Sandbox ausgewählt ist, wird der Bildschirm aktualisiert; die ausgewählte Sandbox wird jetzt im Sandbox-Umschalter angezeigt.

![](../images/ui/sandbox-switched.png)

## Neue Sandbox erstellen

Im folgenden Video erhalten Sie einen schnellen Überblick über die Verwendung von Sandboxen in der Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Um in der Benutzeroberfläche eine neue Sandbox zu erstellen, klicken Sie im linken Navigationsbereich auf **[!UICONTROL Sandboxes]** und dann auf **[!UICONTROL Sandbox erstellen]**.

![](../images/ui/create-sandbox-button.png)

Der Dialog _[!UICONTROL Sandbox erstellen]_wird angezeigt, in dem Sie aufgefordert werden, einen Anzeigetitel und einen Namen für die Sandbox anzugeben. Der **Anzeigetitel**sollte für Menschen lesbar und deskriptiv genug sein, damit er leicht zu erkennen ist. The sandbox**[!UICONTROL  Name ]**is an all-lowercase identifier for use in API calls, and should therefore be unique and concise.

Klicken Sie abschließend auf **[!UICONTROL Erstellen]**.

![](../images/ui/create-sandbox-dialog.png)

>[!NOTE]
>
>Da Sie nur Nicht-Produktions-Sandboxes erstellen können, ist die Option **[!UICONTROL Typ]** bei „Nicht-Produktion“ gesperrt und kann nicht bearbeitet werden.

Once you have finished creating the sandbox, refresh the page and the new sandbox appears in the _[!UICONTROL Sandboxes]_dashboard with a status of &quot;[!UICONTROL Creating]&quot;. New sandboxes take approximately 15 minutes to be provisioned by the system, after which their status changes to &quot;[!UICONTROL Active]&quot;.

![](../images/ui/sandbox-created.png)

## Zurücksetzen einer Sandbox

>[!NOTE]
>
> Diese Funktion ist nur bei Nicht-Produktions-Sandboxes verfügbar. Produktions-Sandboxes können nicht zurückgesetzt werden.

Beim Zurücksetzen einer Nicht-Produktions-Sandbox werden alle mit dieser Sandbox verbundenen Ressourcen (Schemas, Datensätze usw.) gelöscht, wobei der Name der Sandbox und die zugehörigen Berechtigungen beibehalten werden. Diese „saubere“ Sandbox ist für Benutzer, die Zugriff darauf haben, unter demselben Namen weiter verfügbar.

Um eine Sandbox in der Benutzeroberfläche zurückzusetzen, klicken Sie im linken Navigationsbereich auf **[!UICONTROL Sandboxes]** und dann auf die Sandbox, die Sie zurücksetzen möchten. Klicken Sie im Dialog auf der rechten Seite des Bildschirms auf **[!UICONTROL Sandbox zurücksetzen]**.

![](../images/ui/reset-sandbox-button.png)

Es wird ein Dialog angezeigt, in dem Sie aufgefordert werden, Ihre Auswahl zu bestätigen. Klicken Sie auf **[!UICONTROL Zurücksetzen]**, um fortzufahren.

<img src="../images/ui/reset-are-you-sure.png" width="350"><br>

A confirmation message appears and the sandbox&#39;s state changes to &quot;[!UICONTROL Resetting]&quot;. Once it has been provisioned by the system, its state will update to &quot;[!UICONTROL Active]&quot; or &quot;[!UICONTROL Failed]&quot;.

![](../images/ui/sandbox-resetting.png)

## Sandbox löschen

>[!NOTE]
>
> Diese Funktion ist nur bei Nicht-Produktions-Sandboxes verfügbar. Produktions-Sandboxes können nicht gelöscht werden.

Wenn Sie eine Nicht-Produktions-Sandbox löschen, werden alle mit dieser Sandbox verbundenen Ressourcen (einschließlich Berechtigungen) endgültig gelöscht.

Um eine Sandbox in der Benutzeroberfläche zu löschen, klicken Sie im linken Navigationsbereich auf **[!UICONTROL Sandboxes]** und dann auf die Sandbox, die Sie löschen möchten. Klicken Sie im Dialog auf der rechten Seite des Bildschirms auf **[!UICONTROL Sandbox löschen]**.

![](../images/ui/delete-sandbox-button.png)

Es wird ein Dialog angezeigt, in dem Sie aufgefordert werden, Ihre Auswahl zu bestätigen. Klicken Sie auf **[!UICONTROL Löschen]**, um fortzufahren.

<img src="../images/ui/delete-are-you-sure.png" width="350"><br>

Eine Bestätigungsmeldung wird angezeigt und die Sandbox wird aus dem Arbeitsbereich _[!UICONTROL Sandboxes]_entfernt.

## Nächste Schritte

In diesem Dokument haben Sie erfahren, wie Sie Sandboxes in der Benutzeroberfläche von Experience Platform verwalten können. Informationen zum Verwalten von Sandboxes mithilfe der Sandbox-API finden Sie im [Sandbox-Entwicklerhandbuch](../api/getting-started.md).