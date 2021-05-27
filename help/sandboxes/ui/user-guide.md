---
keywords: Experience Platform; Startseite; beliebte Themen; Sandbox-Benutzerhandbuch; Sandbox-Handbuch
solution: Experience Platform
title: Handbuch zur Sandbox-UI
topic-legacy: user guide
description: In diesem Dokument erfahren Sie, wie Sie in der Benutzeroberfläche von Adobe Experience Platform verschiedene Vorgänge im Zusammenhang mit Sandboxes ausführen können.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: ba03ec805d29a95ee7d0d1a23a756feaadcea407
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 20%

---

# Handbuch zur Sandbox-UI

In diesem Dokument erfahren Sie, wie Sie in der Benutzeroberfläche von Adobe Experience Platform verschiedene Vorgänge im Zusammenhang mit Sandboxes ausführen können.

## Anzeigen von Sandboxes

Wählen Sie in der Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Sandboxes]** aus, um das Dashboard [!UICONTROL Sandboxes] zu öffnen. Im Dashboard werden alle für Ihre Organisation verfügbaren Sandboxes aufgeführt, einschließlich Sandbox-Typ (Produktion oder Entwicklung) und Status (aktiv, wird erstellt, gelöscht oder fehlgeschlagen).

![](../images/ui/view-sandboxes.png)

## Zwischen Sandboxes wechseln

Das Steuerelement **Sandbox-Umschalter** oben links im Bildschirm zeigt die derzeit aktive Sandbox an.

![](../images/ui/sandbox-switcher.png)

Um zwischen Sandboxes zu wechseln, wählen Sie den Sandbox-Umschalter aus und wählen Sie die gewünschte Sandbox aus der Dropdown-Liste aus.

![](../images/ui/switcher-menu.png)

Sobald eine Sandbox ausgewählt ist, wird der Bildschirm aktualisiert; die ausgewählte Sandbox wird jetzt im Sandbox-Umschalter angezeigt.

![](../images/ui/switched.png)

## Sandbox suchen

Sie können über die Suchfunktion im Menü Sandbox-Umschalter durch die Liste der verfügbaren Sandboxes navigieren. Geben Sie den Namen der Sandbox ein, auf die Sie zugreifen möchten, um alle für Ihr Unternehmen verfügbaren Sandboxes zu filtern.

![](../images/ui/sandbox-search.png)

## Neue Sandbox erstellen

Im folgenden Video erhalten Sie einen schnellen Überblick über die Verwendung von Sandboxes in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Um eine neue Sandbox zu erstellen, wählen Sie **[!UICONTROL Sandbox erstellen]** in der oberen rechten Ecke des Bildschirms aus.

![create](../images/ui/create.png)

Das Dialogfeld **[!UICONTROL Sandbox erstellen]** wird angezeigt. Wenn Sie eine Entwicklungs-Sandbox erstellen, wählen Sie im Dropdown-Bedienfeld **[!UICONTROL Entwicklung]** aus. Um eine neue Produktions-Sandbox zu erstellen, wählen Sie **[!UICONTROL Produktion]** aus.

![type](../images/ui/type.png)

Geben Sie nach Auswahl des Typs Ihrer Sandbox einen Namen und einen Titel ein. Der Titel ist für Menschen lesbar und sollte beschreibend genug sein, um leicht identifizierbar zu sein. Der Sandbox-Name ist eine in Kleinbuchstaben verfasste Kennung zur Verwendung in API-Aufrufen und sollte daher eindeutig und kurz sein. Der Sandbox-Name muss mit einem Buchstaben beginnen, maximal 256 Zeichen lang sein und nur aus alphanumerischen Zeichen und Bindestrichen (-) bestehen.

Klicken Sie abschließend auf **[!UICONTROL Erstellen]**.

![Info](../images/ui/info.png)

Nachdem Sie die Sandbox fertig erstellt haben, aktualisieren Sie die Seite und die neue Sandbox wird im Dashboard **[!UICONTROL Sandboxes]** mit dem Status &quot;[!UICONTROL Erstellen]&quot;angezeigt. Die Bereitstellung neuer Sandboxes durch das System dauert etwa 30 Sekunden. Danach ändert sich ihr Status in &quot;[!UICONTROL Active]&quot;.

## Zurücksetzen einer Sandbox

>[!IMPORTANT]
>
>Die standardmäßige Produktions-Sandbox kann nicht zurückgesetzt werden, wenn das darin gehostete Identitätsdiagramm auch von Adobe Analytics für die Funktion [Cross Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) verwendet wird oder wenn das darin gehostete Identitätsdiagramm auch von Adobe Audience Manager für die Funktion [People Based Destinations (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html) verwendet wird. Produktions-Sandboxes, die für die bidirektionale Segmentfreigabe mit Adobe Audience Manager oder Audience Core Service verwendet werden, können ebenfalls nicht zurückgesetzt werden.

Durch das Zurücksetzen einer Produktions- oder Entwicklungs-Sandbox werden alle mit dieser Sandbox verknüpften Ressourcen (Schemas, Datensätze usw.) gelöscht, wobei der Name der Sandbox und die zugehörigen Berechtigungen beibehalten werden. Diese „saubere“ Sandbox ist für Benutzer, die Zugriff darauf haben, unter demselben Namen weiter verfügbar.

Wählen Sie in der Sandbox-Liste die Sandbox aus, die Sie zurücksetzen möchten. Wählen Sie im rechten Navigationsfenster **[!UICONTROL Sandbox reset]** aus.

![Zurücksetzen](../images/ui/reset.png)

Es wird ein Dialogfeld angezeigt, in dem Sie aufgefordert werden, Ihre Auswahl zu bestätigen. Wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![reset-warning](../images/ui/reset-warning.png)

Geben Sie im letzten Bestätigungsfenster den Namen der Sandbox in das Dialogfeld ein und wählen Sie **[!UICONTROL Zurücksetzen]** aus.

![reset-confirm](../images/ui/reset-confirm.png)

Nach einigen Augenblicken wird unten im Bildschirm ein Bestätigungsfeld angezeigt, um eine erfolgreiche Zurücksetzung zu bestätigen.

![Erfolgreich](../images/ui/success.png)

### Fehlermeldungen

Eine standardmäßige Produktions-Sandbox, die CDA-Daten enthält, kann nicht zurückgesetzt werden und gibt den folgenden Fehler zurück.

![cda](../images/ui/cda.png)

Eine standardmäßige Produktions-Sandbox, die PBD-Daten enthält, kann ebenfalls nicht zurückgesetzt werden und gibt den folgenden Fehler zurück.

![pbd](../images/ui/pbd.png)

Eine standardmäßige Produktions-Sandbox, die Daten für CDA und PBD enthält, kann ebenfalls nicht zurückgesetzt werden und gibt den folgenden Fehler zurück.

![both](../images/ui/both.png)

Eine Produktions-Sandbox, die für die bidirektionale Segmentfreigabe mit Adobe Audience Manager oder Audience Core Service verwendet wird, kann ebenfalls nicht zurückgesetzt werden und gibt den folgenden Fehler zurück.

![seg](../images/ui/seg.png)

## Sandbox löschen

>[!IMPORTANT]
>
>Die standardmäßige Produktions-Sandbox kann nicht gelöscht werden und Produktions-Sandboxes, die für die bidirektionale Segmentfreigabe mit Adobe Audience Manager oder Audience Core Service verwendet werden, können ebenfalls nicht gelöscht werden.

Durch das Löschen einer Produktions- oder Entwicklungs-Sandbox werden alle mit dieser Sandbox verknüpften Ressourcen, einschließlich Berechtigungen, endgültig entfernt.

Wählen Sie die Sandbox aus, die Sie aus der Sandbox-Liste löschen möchten. Wählen Sie im sich öffnenden Navigationsfenster **[!UICONTROL Delete]** aus.

![Löschen Sie](../images/ui/delete.png)

Es wird ein Dialogfeld angezeigt, in dem Sie aufgefordert werden, Ihre Auswahl zu bestätigen. Wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![delete-warning](../images/ui/delete-warning.png)

Geben Sie im letzten Bestätigungsfenster den Namen der Sandbox in das Dialogfeld ein und wählen Sie **[!UICONTROL Weiter]**

![delete-validation](../images/ui/delete-confirm.png)

Eine Produktions-Sandbox, die für die bidirektionale Segmentfreigabe mit Adobe Audience Manager oder Audience Core Service verwendet wird, kann nicht gelöscht werden und gibt den folgenden Fehler zurück.

![seg](../images/ui/seg.png)

## Nächste Schritte

In diesem Dokument haben Sie erfahren, wie Sie Sandboxes in der Benutzeroberfläche von Experience Platform verwalten können. Informationen zum Verwalten von Sandboxes mithilfe der Sandbox-API finden Sie im [Sandbox-Entwicklerhandbuch](../api/getting-started.md).
