---
title: Verwenden von Adobe Experience Platform Assurance
description: In diesem Handbuch wird erläutert, wie Sie Adobe Experience Platform Assurance nach der Installation und Implementierung verwenden.
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Verwenden von Adobe Experience Platform Assurance

In diesem Tutorial wird erläutert, wie Sie Adobe Experience Platform Assurance verwenden. Anweisungen zur Installation und Implementierung der Adobe Experience Platform Assurance-Erweiterung finden Sie im Tutorial [Implementieren der Assurance-Erweiterung](./implement-assurance.md).

## Erstellen von Sitzungen

Nachdem Sie sich bei der Benutzeroberfläche von [Assurance ](https://experience.adobe.com/assurance) haben, können Sie auf **[!UICONTROL Sitzung erstellen]** klicken, um eine Sitzung zu erstellen.

![Die Schaltfläche „Sitzung erstellen“ ist hervorgehoben und zeigt an, wo Sie eine Sitzung erstellen können.](./images/using-assurance/create-session.png)

Das **[!UICONTROL Neue Sitzung erstellen]** wird angezeigt. Bitte die angegebenen Anweisungen überprüfen und mit der Auswahl von **[!UICONTROL Starten]** fortfahren.

![Das Dialogfeld Neue Sitzung erstellen mit Anweisungen zur Verwendung von Assurance wird angezeigt.](./images/using-assurance/create-new-session.png)

Sie können jetzt einen Namen eingeben, um die Sitzung zu identifizieren, und dann eine **[!UICONTROL Basis-URL]** angeben (Deep-Link-URL für Ihre App). Klicken Sie nach Angabe dieser Details auf **[!UICONTROL Weiter]**.

>[!INFO]
>
>Die Basis-URL ist die Stammdefinition, die zum Starten Ihrer App über eine URL verwendet wird. Es wird eine Sitzungs-URL generiert, mit der Sie die Assurance-Sitzung starten können. Ein Beispielwert könnte wie folgt aussehen: `myapp://default` Geben Sie in das Feld **[!UICONTROL Basis]** URL) die Basis-Deep-Link-Definition Ihrer App ein.

![Der vollständige Workflow zum Erstellen einer neuen Sitzung wird angezeigt.](./images/using-assurance/create-session.gif)

## Verbindung zu einer Sitzung herstellen

Nachdem Sie eine Sitzung erstellt haben, stellen Sie sicher, dass das Dialogfeld **[!UICONTROL Neue Sitzung erstellen]** jetzt einen Link, einen QR-Code und eine PIN anzeigt.

![Ein Dialogfeld mit den Optionen zum Herstellen einer Verbindung mit Ihrer Assurance-Sitzung wird angezeigt.](./images/using-assurance/create-new-session-pin.png)

Wenn dieses Dialogfeld angezeigt wird, können Sie entweder die Kamera-App Ihres Geräts verwenden, um den QR-Code zu scannen und Ihre App zu öffnen, oder den Link kopieren und in Ihrer App öffnen. Wenn Ihre App gestartet wird, sollte der PIN-Eingabebildschirm überlagert sein. Geben Sie die PIN aus dem vorherigen Schritt ein und drücken Sie **[!UICONTROL Verbinden]**.

Sie können überprüfen, ob Ihre App mit Assurance verbunden ist, wenn das Adobe Experience Platform-Symbol (rote Adobe „A„) in Ihrer App angezeigt wird.

![Der vollständige Workflow zum Verbinden Ihres Programms mit einer Assurance-Sitzung wird angezeigt.](./images/using-assurance/connect-session.gif)

## Exportieren einer Sitzung

Um eine Assurance-Sitzung zu exportieren, wählen Sie auf der Seite mit den Sitzungsdetails der Mobile App **[!UICONTROL In JSON exportieren]** aus:

![Exportieren einer Sitzung](./images/using-assurance/export-session.png)

Die Exportoption berücksichtigt die Suchfilterergebnisse und exportiert nur die in der Ereignisansicht angezeigten Ereignisse. Wenn Sie beispielsweise nach Ereignissen des Typs „Verfolgen“ suchen und dann **[!UICONTROL In JSON exportieren]** wählen, werden nur die Ergebnisse des Ereignisses „Verfolgen“ exportiert.
