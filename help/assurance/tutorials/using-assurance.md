---
title: Verwenden von Adobe Experience Platform Assurance
description: In diesem Handbuch wird die Verwendung von Adobe Experience Platform Assurance nach der Installation und Implementierung erläutert.
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Verwenden von Adobe Experience Platform Assurance

In diesem Tutorial wird die Verwendung von Adobe Experience Platform Assurance erläutert. Anweisungen zum Installieren und Implementieren der Adobe Experience Platform Assurance-Erweiterung finden Sie im Tutorial zum Implementieren von [Assurance-Erweiterung](./implement-assurance.md).

## Erstellen von Sitzungen

Nachdem Sie sich bei der [Assurance-Benutzeroberfläche](https://experience.adobe.com/assurance) angemeldet haben, können Sie **[!UICONTROL Sitzung erstellen]** auswählen, um mit der Erstellung einer Sitzung zu beginnen.

![Die Schaltfläche Sitzung erstellen ist hervorgehoben und zeigt an, wo Sie eine Sitzung erstellen können.](./images/using-assurance/create-session.png)

Das Dialogfeld **[!UICONTROL Neue Sitzung erstellen]** wird angezeigt. Überprüfen Sie die Anweisungen und wählen Sie **[!UICONTROL Start]** aus.

![Das Dialogfeld &quot;Neue Sitzung erstellen&quot;wird mit Anweisungen zur Verwendung von &quot;Assurance&quot;angezeigt.](./images/using-assurance/create-new-session.png)

Sie können jetzt einen Namen eingeben, um die Sitzung zu identifizieren, und dann eine **[!UICONTROL Basis-URL]** (Deep-Link-URL für Ihre App) angeben. Nachdem Sie diese Details angegeben haben, wählen Sie **[!UICONTROL Weiter]** aus.

>[!INFO]
>
>Die Basis-URL ist die Stammdefinition, mit der Ihre App über eine URL gestartet wird. Es wird eine Sitzungs-URL generiert, mit der Sie die Zuverlässigkeitssitzung starten können. Ein Beispielwert könnte wie folgt aussehen: `myapp://default` Geben Sie im Feld **[!UICONTROL Basis-URL]** die Deep-Link-Definition Ihrer App ein.

![Der vollständige Workflow zum Erstellen einer neuen Sitzung wird angezeigt.](./images/using-assurance/create-session.gif)

## Herstellen einer Verbindung zu einer Sitzung

Nachdem Sie eine Sitzung erstellt haben, stellen Sie sicher, dass das Dialogfeld &quot;**[!UICONTROL Neue Sitzung erstellen]**&quot;jetzt einen Link, einen QR-Code und eine PIN anzeigt.

![Ein Dialogfeld mit den Optionen zum Herstellen einer Verbindung zu Ihrer Zuverlässigkeitssitzung wird angezeigt.](./images/using-assurance/create-new-session-pin.png)

Wenn dieses Dialogfeld angezeigt wird, können Sie entweder die Kamera-App Ihres Geräts verwenden, um den QR-Code zu scannen und Ihre App zu öffnen oder den Link zu kopieren und in Ihrer App zu öffnen. Wenn Ihre App gestartet wird, sollte der Bildschirm PIN-Eintrag überlagert werden. Geben Sie die PIN aus dem vorherigen Schritt ein und drücken Sie **[!UICONTROL Verbinden]**.

Sie können überprüfen, ob Ihre App mit Assurance verbunden ist, wenn in Ihrer App das Adobe Experience Platform-Symbol (rote Adobe &quot;A&quot;) angezeigt wird.

![Der vollständige Workflow zum Verbinden Ihrer Anwendung mit einer Zuverlässigkeitssitzung wird angezeigt.](./images/using-assurance/connect-session.gif)

## Eine Sitzung exportieren

Um eine Zuverlässigkeitssitzung zu exportieren, wählen Sie auf der Seite mit den Sitzungsdetails Ihrer App **[!UICONTROL In JSON exportieren]** in einer Sitzung aus:

![Exportieren einer Sitzung](./images/using-assurance/export-session.png)

Die Exportoption berücksichtigt Suchfilterergebnisse und exportiert nur Ereignisse, die in der Ereignisansicht angezeigt werden. Wenn Sie beispielsweise nach &quot;track&quot;-Ereignissen gesucht und dann **[!UICONTROL Nach JSON exportieren]** auswählen, werden nur die &quot;track&quot;-Ereignisergebnisse exportiert.
