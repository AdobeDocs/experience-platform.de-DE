---
keywords: Experience Platform; Startseite; beliebte Themen; Sandbox-Benutzerhandbuch; Sandbox-Handbuch
solution: Experience Platform
title: Handbuch zur Sandbox-UI
topic-legacy: user guide
description: In diesem Dokument erfahren Sie, wie Sie in der Benutzeroberfläche von Adobe Experience Platform verschiedene Vorgänge im Zusammenhang mit Sandboxes ausführen können.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: df0f543b18f008b656c5e411305c5243efa744ad
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 15%

---

# Handbuch zur Sandbox-UI

In diesem Dokument erfahren Sie, wie Sie in der Benutzeroberfläche von Adobe Experience Platform verschiedene Vorgänge im Zusammenhang mit Sandboxes ausführen können.

## Anzeigen von Sandboxes

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Sandboxes]** in der linken Navigation und wählen Sie dann **[!UICONTROL Durchsuchen]** , um [!UICONTROL Sandboxes] Dashboard. Das Dashboard listet alle verfügbaren Sandboxes für Ihre Organisation auf, einschließlich der jeweiligen Typen (Produktion oder Entwicklung).

![Ansicht-Sandboxes](../images/ui/view-sandboxes.png)

## Zwischen Sandboxes wechseln

Die Sandbox-Anzeige befindet sich in der oberen Kopfzeile der Platform-Benutzeroberfläche und zeigt den Titel der Sandbox an, in der Sie sich derzeit befinden, deren Region und deren Typ.

![Sandbox-Indikator](../images/ui/sandbox-indicator.png)

Um zwischen Sandboxes zu wechseln, wählen Sie die Sandbox-Anzeige aus und wählen Sie die gewünschte Sandbox aus der Dropdown-Liste aus.

![switch-interface](../images/ui/switcher-interface.png)

Sobald eine Sandbox ausgewählt ist, wird der Bildschirm aktualisiert und auf die ausgewählte Sandbox aktualisiert.

![Sandbox-vermittelt](../images/ui/sandbox-switched.png)

## Neue Sandbox erstellen {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="Sandbox-Name"
>abstract="Der Sandbox-Name ist der Text, der im Backend zum Erstellen einer eindeutigen ID für diese Sandbox verwendet wird."

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="Sandbox-Titel"
>abstract="Der Sandbox-Titel ist der Anzeigename, der die Sandbox in Menüs und Dropdown-Menüs in der Experience Platform-Benutzeroberfläche darstellt."

>[!NOTE]
>
>Wenn eine neue Sandbox erstellt wird, müssen Sie diese neue Sandbox zunächst Ihrem Produktprofil in [Adobe Admin Console](https://adminconsole.adobe.com/) bevor Sie mit der Verwendung der neuen Sandbox beginnen können. Weitere Informationen finden Sie in der Dokumentation unter [Berechtigungen für ein Produktprofil verwalten](../../access-control/ui/permissions.md) für Informationen zur Bereitstellung einer Sandbox für ein Produktprofil.

Im folgenden Video erhalten Sie einen schnellen Überblick über die Verwendung von Sandboxes in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Um eine neue Sandbox zu erstellen, wählen Sie **[!UICONTROL Sandbox erstellen]** oben rechts im Bildschirm.

![create-sandbox](../images/ui/create-sandbox.png)

Die **[!UICONTROL Sandbox erstellen]** angezeigt. Wenn Sie eine Entwicklungs-Sandbox erstellen, wählen Sie **[!UICONTROL Entwicklung]** im Dropdown-Bedienfeld. Um eine neue Produktions-Sandbox zu erstellen, wählen Sie **[!UICONTROL Produktion]**.

![Sandbox-Typ](../images/ui/sandbox-type.png)

Geben Sie nach Auswahl des Typs Ihrer Sandbox einen Namen und einen Titel ein. Der Titel ist für Menschen lesbar und sollte beschreibend genug sein, um leicht identifizierbar zu sein. Der Sandbox-Name ist eine in Kleinbuchstaben verfasste Kennung zur Verwendung in API-Aufrufen und sollte daher eindeutig und kurz sein. Der Sandbox-Name muss mit einem Buchstaben beginnen, maximal 256 Zeichen lang sein und nur aus alphanumerischen Zeichen und Bindestrichen (-) bestehen.

Klicken Sie abschließend auf **[!UICONTROL Erstellen]**.

![sandbox-info](../images/ui/sandbox-info.png)

Nachdem Sie die Sandbox fertig erstellt haben, aktualisieren Sie die Seite und die neue Sandbox wird im **[!UICONTROL Sandboxes]** Dashboard mit dem Status &quot;[!UICONTROL Erstellen]&quot;. Die Bereitstellung neuer Sandboxes durch das System dauert etwa 30 Sekunden, danach ändert sich ihr Status in &quot;[!UICONTROL Aktiv]&quot;.

![new-sandbox](../images/ui/new-sandbox.png)

## Zurücksetzen einer Sandbox

>[!WARNING]
>
>Im Folgenden finden Sie eine Liste von Ausnahmen, mit denen Sie verhindern können, dass Sie die standardmäßige Produktions-Sandbox oder eine benutzerdefinierte Produktions-Sandbox zurücksetzen: <ul><li>Die standardmäßige Produktions-Sandbox kann nicht zurückgesetzt werden, wenn das in der Sandbox gehostete Identitätsdiagramm auch von Adobe Analytics für die [Geräteübergreifende Analyse (Cross Device Analytics, CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=de) Funktion.</li><li>Die standardmäßige Produktions-Sandbox kann nicht zurückgesetzt werden, wenn das in der Sandbox gehostete Identitätsdiagramm auch von Adobe Audience Manager für die [Benutzerbasierte Ziele (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=de).</li><li>Die standardmäßige Produktions-Sandbox kann nicht zurückgesetzt werden, wenn sie Daten für CDA- und PBD-Funktionen enthält.</li><li>Eine benutzerdefinierte Produktions-Sandbox, die für die bidirektionale Segmentfreigabe mit Adobe Audience Manager oder Audience Core Service verwendet wird, kann nach einer Warnmeldung zurückgesetzt werden.</li></ul>

Durch das Zurücksetzen einer Produktions- oder Entwicklungs-Sandbox werden alle mit dieser Sandbox verknüpften Ressourcen (Schemas, Datensätze usw.) gelöscht, wobei der Name der Sandbox und die zugehörigen Berechtigungen beibehalten werden. Diese „saubere“ Sandbox ist für Benutzer, die Zugriff darauf haben, unter demselben Namen weiter verfügbar.

Wählen Sie in der Sandbox-Liste die Sandbox aus, die Sie zurücksetzen möchten. Wählen Sie im sich öffnenden Navigationsfenster die Option **[!UICONTROL Sandbox zurücksetzen]**.

![Zurücksetzen](../images/ui/reset.png)

Es wird ein Dialogfeld angezeigt, in dem Sie aufgefordert werden, Ihre Auswahl zu bestätigen. Auswählen **[!UICONTROL Weiter]** um fortzufahren.

![reset-warning](../images/ui/reset-warning.png)

Geben Sie im letzten Bestätigungsfenster den Namen der Sandbox in das Dialogfeld ein und wählen Sie **[!UICONTROL Zurücksetzen]**.

![reset-confirm](../images/ui/reset-confirm.png)

## Sandbox löschen

>[!WARNING]
>
>Die standardmäßige Produktions-Sandbox kann nicht gelöscht werden. Jede vom Benutzer erstellte Produktions-Sandbox, die für die bidirektionale Segmentfreigabe mit verwendet wird [!DNL Audience Manager] oder [!DNL Audience Core Service] kann nach einer Warnmeldung gelöscht werden.

Durch das Löschen einer Produktions- oder Entwicklungs-Sandbox werden alle mit dieser Sandbox verknüpften Ressourcen, einschließlich Berechtigungen, endgültig entfernt.

Wählen Sie die Sandbox aus, die Sie aus der Sandbox-Liste löschen möchten. Wählen Sie im sich öffnenden Navigationsfenster die Option **[!UICONTROL Löschen]**.

![löschen](../images/ui/delete.png)

Es wird ein Dialogfeld angezeigt, in dem Sie aufgefordert werden, Ihre Auswahl zu bestätigen. Auswählen **[!UICONTROL Weiter]** um fortzufahren.

![delete-warning](../images/ui/delete-warning.png)

Geben Sie im letzten Bestätigungsfenster den Namen der Sandbox in das Dialogfeld ein und wählen Sie  **[!UICONTROL Weiter]**.

![delete-validation](../images/ui/delete-confirm.png)

## Nächste Schritte

In diesem Dokument haben Sie erfahren, wie Sie Sandboxes in der Benutzeroberfläche von Experience Platform verwalten können. Informationen zum Verwalten von Sandboxes mithilfe der Sandbox-API finden Sie im [Sandbox-Entwicklerhandbuch](../api/getting-started.md).
