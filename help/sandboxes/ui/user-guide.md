---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sandbox-Benutzerhandbuch
topic: user guide
translation-type: tm+mt
source-git-commit: 6438c1841889ff345e1ebaedabfed0531c1f97f9
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Sandbox-Benutzerhandbuch

In diesem Dokument wird beschrieben, wie Sie verschiedene Vorgänge im Zusammenhang mit Sandboxen in der Benutzeroberfläche von Adobe Experience Platform durchführen.

## Ansicht-Sandboxen

Klicken Sie in der Benutzeroberfläche der Erlebnisplattform auf **Sandboxes** im linken Navigationsbereich, um das _Sandbox_ -Dashboard zu öffnen. Das Dashboard Liste alle für Ihr Unternehmen verfügbaren Sandboxen, einschließlich Sandbox-Typ (Produktion oder Entwicklung) und Status (aktiv, erstellen, gelöscht oder fehlgeschlagen).

![](../images/ui/sandboxes-tab.png)

## Zwischen Sandboxen wechseln

Das **Sandbox-Umschalter** oben links auf dem Bildschirm zeigt die derzeit aktive Sandbox an.

![](../images/ui/sandbox-selector.png)

Um zwischen Sandboxen zu wechseln, klicken Sie auf den Sandbox-Umschalter und wählen Sie die gewünschte Sandbox aus der Dropdown-Liste aus.

![](../images/ui/switch-sandbox.png)

Sobald eine Sandbox ausgewählt ist, wird der Bildschirm aktualisiert, wobei die ausgewählte Sandbox jetzt im Sandbox-Umschalter angezeigt wird.

![](../images/ui/sandbox-switched.png)

## Neue Sandbox erstellen

Um eine neue Sandbox in der Benutzeroberfläche zu erstellen, klicken Sie auf **Sandboxen** in der linken Navigationsleiste und dann auf Sandbox **erstellen**.

![](../images/ui/create-sandbox-button.png)

Das Dialogfeld &quot;Sandbox _erstellen_ &quot;wird angezeigt, in dem Sie aufgefordert werden, einen Anzeigentitel und einen Namen für die Sandbox anzugeben. Der **Anzeigentitel** soll für Menschen lesbar sein und sollte so beschreibend sein, dass er leicht zu identifizieren ist. Der **Name** der Sandbox ist ein in Kleinbuchstaben geschriebener Bezeichner für die Verwendung in API-Aufrufen und sollte daher eindeutig und knapp sein.

Klicken Sie abschließend auf **Erstellen**.

![](../images/ui/create-sandbox-dialog.png)

>[!NOTE] Da Sie nur auf das Erstellen von Nicht-Produktions-Sandbox-Typen beschränkt sind, ist die **Typoption** bei &quot;Nicht-Produktion&quot;gesperrt und kann nicht bearbeitet werden.

Nachdem Sie die Sandbox erstellt haben, aktualisieren Sie die Seite und die neue Sandbox wird im _Sandbox_ -Dashboard mit dem Status &quot;Erstellen&quot;angezeigt. Neue Sandboxen benötigen ca. 15 Minuten, um vom System bereitgestellt zu werden. Danach ändert sich ihr Status in &quot;Aktiv&quot;.

![](../images/ui/sandbox-created.png)

## Zurücksetzen einer Sandbox

>[!NOTE] Diese Funktion ist nur für Nicht-Produktions-Sandboxen verfügbar. Produktions-Sandboxes können nicht zurückgesetzt werden.

Beim Zurücksetzen einer Nicht-Produktions-Sandbox werden alle mit dieser Sandbox verbundenen Ressourcen (Schema, Datensätze usw.) gelöscht, wobei der Name der Sandbox und die zugehörigen Berechtigungen beibehalten werden. Diese &quot;saubere&quot;Sandbox ist weiterhin unter demselben Namen für Benutzer verfügbar, die Zugriff darauf haben.

Um eine Sandbox in der Benutzeroberfläche zurückzusetzen, klicken Sie im linken Navigationsbereich auf **Sandboxen** und dann auf die Sandbox, die Sie zurücksetzen möchten. Klicken Sie im Dialogfeld auf der rechten Seite des Bildschirms auf **Sandbox zurücksetzen**.

![](../images/ui/reset-sandbox-button.png)

Es wird ein Dialogfeld angezeigt, in dem Sie aufgefordert werden, Ihre Auswahl zu bestätigen. Click **Reset** to continue.

<img src="../images/ui/reset-are-you-sure.png" width="350"><br>

Eine Bestätigungsmeldung wird angezeigt und der Status der Sandbox ändert sich in &quot;Zurücksetzen&quot;. Sobald das System es bereitgestellt hat, wird sein Status auf &quot;Aktiv&quot;oder &quot;Fehlgeschlagen&quot;aktualisiert.

![](../images/ui/sandbox-resetting.png)

## Sandbox löschen

>[!NOTE] Diese Funktion ist nur für Nicht-Produktions-Sandboxen verfügbar. Produktions-Sandboxes können nicht gelöscht werden.

Wenn Sie eine Sandbox ohne Produktionscharakter löschen, werden alle mit dieser Sandbox verbundenen Ressourcen, einschließlich Berechtigungen, endgültig entfernt.

Um eine Sandbox in der Benutzeroberfläche zu löschen, klicken Sie im linken Navigationsbereich auf **Sandboxen** und dann auf die zu löschende Sandbox. Klicken Sie im Dialogfeld auf der rechten Seite des Bildschirms auf Sandbox **löschen**.

![](../images/ui/delete-sandbox-button.png)

Es wird ein Dialogfeld angezeigt, in dem Sie aufgefordert werden, Ihre Auswahl zu bestätigen. Click **Delete** to continue.

<img src="../images/ui/delete-are-you-sure.png" width="350"><br>

Eine Bestätigungsmeldung wird angezeigt und die Sandbox wird aus dem _Sandbox_ -Arbeitsbereich entfernt.

## Nächste Schritte

In diesem Dokument wurde gezeigt, wie Sandboxen in der Experience Platform-Benutzeroberfläche verwaltet werden. Informationen zum Verwalten von Sandboxen mit der Sandbox-API finden Sie im [Sandbox-Entwicklerhandbuch](../api/getting-started.md).