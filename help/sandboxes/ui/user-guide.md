---
keywords: Experience Platform;Home;beliebte Themen;Sandbox-Benutzerhandbuch;Sandbox-Handbuch
solution: Experience Platform
title: Handbuch zur Sandbox-Benutzeroberfläche
topic-legacy: user guide
description: In diesem Dokument erfahren Sie, wie Sie in der Benutzeroberfläche von Adobe Experience Platform verschiedene Vorgänge im Zusammenhang mit Sandboxes ausführen können.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 48%

---

# Handbuch zur Sandbox-Benutzeroberfläche

In diesem Dokument erfahren Sie, wie Sie in der Benutzeroberfläche von Adobe Experience Platform verschiedene Vorgänge im Zusammenhang mit Sandboxes ausführen können.

## Anzeigen von Sandboxes

Wählen Sie in der Benutzeroberfläche &quot;Experience Platform&quot;in der linken Navigation **[!UICONTROL Sandboxes]** aus, um das Dashboard **[!UICONTROL Sandboxes]** zu öffnen. Im Dashboard werden alle für Ihre Organisation verfügbaren Sandboxes aufgeführt, einschließlich Sandbox-Typ (Produktion oder Entwicklung) und Status (aktiv, wird erstellt, gelöscht oder fehlgeschlagen).

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

Um eine neue Sandbox in der Benutzeroberfläche zu erstellen, klicken Sie auf die Schaltfläche **[!UICONTROL Sandbox erstellen]** oben rechts im Bildschirm.

![](../images/ui/create-sandbox.png)

Der Dialog **[!UICONTROL Sandbox erstellen]** wird angezeigt, in dem Sie aufgefordert werden, einen Anzeigetitel und einen Namen für die Sandbox anzugeben. Der **Anzeigetitel** sollte für Menschen lesbar und deskriptiv genug sein, damit er leicht zu erkennen ist. Die Sandbox **[!UICONTROL Name]** ist ein in Kleinbuchstaben geschriebener Bezeichner für die Verwendung in API-Aufrufen und sollte daher eindeutig und knapp sein. Die Sandbox **[!UICONTROL Name]** darf nur aus alphanumerischen Zeichen und Bindestrichen **(-)** bestehen. Sie muss mit einem Buchstaben beginnen und darf nicht länger als 256 Zeichen sein.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Erstellen]**.

![](../images/ui/create-dialog.png)

>[!NOTE]
>
>Da Sie nur Nicht-Produktions-Sandboxes erstellen können, ist die Option **[!UICONTROL Typ]** bei „Nicht-Produktion“ gesperrt und kann nicht bearbeitet werden.

Nachdem Sie die Sandbox erstellt haben, aktualisieren Sie die Seite und die neue Sandbox wird im Dashboard **[!UICONTROL Sandboxes]** mit dem Status &quot;[!UICONTROL Erstellen]&quot;angezeigt. Die Bereitstellung neuer Sandboxen durch das System dauert etwa 15 Minuten, danach ändert sich ihr Status in &quot;[!UICONTROL Aktiv]&quot;.

![](../images/ui/creating.png)

## Zurücksetzen einer Sandbox

>[!NOTE]
>
> Diese Funktion ist nur bei Nicht-Produktions-Sandboxes verfügbar. Produktions-Sandboxes können nicht zurückgesetzt werden.

Beim Zurücksetzen einer Nicht-Produktions-Sandbox werden alle mit dieser Sandbox verbundenen Ressourcen (Schemas, Datensätze usw.) gelöscht, wobei der Name der Sandbox und die zugehörigen Berechtigungen beibehalten werden. Diese „saubere“ Sandbox ist für Benutzer, die Zugriff darauf haben, unter demselben Namen weiter verfügbar.

Um eine Sandbox in der Benutzeroberfläche zurückzusetzen, wählen Sie in der linken Navigationsleiste **[!UICONTROL Sandboxes]** und dann die Sandbox aus, die Sie zurücksetzen möchten. Wählen Sie im Dialogfeld, das auf der rechten Seite des Bildschirms angezeigt wird, **[!UICONTROL Sandbox zurücksetzen]**.

![](../images/ui/reset-sandbox.png)

Es wird ein Dialog angezeigt, in dem Sie aufgefordert werden, Ihre Auswahl zu bestätigen. Wählen Sie **[!UICONTROL Zurücksetzen]**, um fortzufahren.

![](../images/ui/reset-confirm.png)

Eine Bestätigungsmeldung wird angezeigt und der Status der Sandbox ändert sich in &quot;**[!UICONTROL Zurücksetzen]&quot;**. Sobald das System es bereitgestellt hat, wird sein Status auf **&quot;[!UICONTROL Aktiv]&quot;** oder **&quot;[!UICONTROL Fehlgeschlagen]&quot;** aktualisiert.

![](../images/ui/resetting.png)

## Sandbox löschen

>[!NOTE]
>
> Diese Funktion ist nur bei Nicht-Produktions-Sandboxes verfügbar. Produktions-Sandboxes können nicht gelöscht werden.

Wenn Sie eine Nicht-Produktions-Sandbox löschen, werden alle mit dieser Sandbox verbundenen Ressourcen (einschließlich Berechtigungen) endgültig gelöscht.

Um eine Sandbox in der Benutzeroberfläche zu löschen, wählen Sie **[!UICONTROL Sandboxes]** in der linken Navigationsleiste aus und wählen Sie dann die zu löschende Sandbox aus. Wählen Sie im Dialogfeld, das auf der rechten Seite des Bildschirms angezeigt wird, **[!UICONTROL Sandbox]** löschen.

![](../images/ui/delete-sandbox.png)

Es wird ein Dialog angezeigt, in dem Sie aufgefordert werden, Ihre Auswahl zu bestätigen. Wählen Sie **[!UICONTROL Löschen]**, um fortzufahren.

![](../images/ui/delete-confirm.png)

Eine Bestätigungsmeldung wird angezeigt und die Sandbox wird aus dem Arbeitsbereich **[!UICONTROL Sandboxes]** entfernt.

## Nächste Schritte

In diesem Dokument haben Sie erfahren, wie Sie Sandboxes in der Benutzeroberfläche von Experience Platform verwalten können. Informationen zum Verwalten von Sandboxes mithilfe der Sandbox-API finden Sie im [Sandbox-Entwicklerhandbuch](../api/getting-started.md).
