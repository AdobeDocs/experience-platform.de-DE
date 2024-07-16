---
title: In-App-Nachrichtenansicht
description: In diesem Handbuch werden Informationen zur In-App-Messaging-Ansicht in Adobe Experience Platform Assurance beschrieben.
exl-id: 6131289a-aebb-4b3a-9045-4b2cf23415f8
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 0%

---

# Ansicht &quot;In-App Messaging&quot;in &quot;Assurance&quot;

Die In-App-Messaging-Ansicht in Adobe Experience Platform Assurance bietet die Möglichkeit, Ihre App zu validieren, In-App-Nachrichten, die an Ihr Gerät gesendet werden, zu überwachen und Nachrichten an Ihr Gerät zu simulieren.

## Nachrichten auf Gerät

Oben auf der Registerkarte **[!UICONTROL Nachrichten auf Gerät]** befindet sich ein Dropdown-Menü **[!UICONTROL Nachricht]** . Dies umfasst alle Nachrichten, die in der Zuverlässigkeitssitzung empfangen wurden. Wenn eine Nachricht nicht in dieser Liste enthalten ist, bedeutet dies, dass sie von der App nie empfangen wurde.

![Message](./images/in-app-messaging/message.png)

Wenn Sie eine Nachricht auswählen, werden wie in den folgenden Abschnitten beschrieben viele Informationen zu dieser Nachricht angezeigt.

### Nachrichtenvorschau

Im rechten Bereich befindet sich ein Bereich mit der **[!UICONTROL Nachrichtenvorschau]**, der eine Vorschau der Nachricht anzeigt. Wenn Sie **[!UICONTROL Auf Gerät simulieren]** auswählen, wird diese Nachricht an alle Geräte gesendet, die derzeit mit der Sitzung verbunden sind.

![Vorschau](./images/in-app-messaging/preview.png)

### Nachrichtenverhalten

Unter dem Bereich **[!UICONTROL Nachrichtenvorschau]** befindet sich die Registerkarte **[!UICONTROL Nachrichtenverhalten]**. Hier finden Sie alle Details zur Anzeige der Nachricht. Zu diesen Informationen gehören Positionierungsinformationen, Animationen, Wischgesten und Darstellungseinstellungen.

![Verhalten](./images/in-app-messaging/gestures.png)

### Registerkarte &quot;Info&quot;

Im linken Bereich befinden sich vier Registerkarten, auf denen Details zur Nachricht angezeigt werden. Auf der Registerkarte **[!UICONTROL Info]** werden Informationen angezeigt, die aus Adobe Journey Optimizer (AJO) zur Nachrichtenkampagne geladen wurden.

Sie können auch **[!UICONTROL Kampagne anzeigen]** auswählen, um die Nachricht in AJO zur Überprüfung oder Bearbeitung zu öffnen.

![Info](./images/in-app-messaging/info.png)

### Registerkarte &quot;Regeln&quot;

Die Registerkarte **[!UICONTROL Regeln]** zeigt an, was passieren muss, damit diese Nachricht angezeigt wird. So erhalten Sie Einblicke in den Trigger einer Nachricht, die angezeigt werden soll. Sehen Sie sich dieses Beispiel an:

![Regeln](./images/in-app-messaging/rules.png)

Das Beispiel zeigt drei verschiedene Bedingungen für die Regel. Wenn Sie ein Ereignis auswählen (aus einer Ereignisliste, dem Tab Analyse oder in der Timeline), wird dieses Ereignis anhand dieser Regeln ausgewertet. Wenn das Ereignis mit einer Bedingung übereinstimmt, wird ein grünes Häkchen angezeigt:

![Regelübereinstimmung](./images/in-app-messaging/rule-match.png)

Wenn das Ereignis nicht übereinstimmt, wird ein rotes Symbol angezeigt:

![Regelabweichung](./images/in-app-messaging/rule-mismatch.png)

Wenn alle drei Bedingungen mit dem aktuellen Ereignis übereinstimmen, wird die Nachricht angezeigt.

### Registerkarte &quot;Analyse&quot;

Die Registerkarte **[!UICONTROL Analysieren]** bietet zusätzliche Einblicke in die Regeln. In unserem Beispiel filtern wir jedes Ereignis in der Sitzung danach, wie nah unsere Nachrichtenregel mit dem Ereignis übereinstimmt.

![Analyze](./images/in-app-messaging/analyze.png)

Im Beispiel im Abschnitt **[!UICONTROL Regeln-Tab]** gibt es drei Bedingungen in der Regel. Auf dieser Registerkarte wird angezeigt, welcher Prozentsatz der Regel bei jedem Ereignis übereinstimmt. Die Mehrzahl der Ereignisse entspricht 33 % (eine von drei Bedingungen) und die übrigen 100 %.

Daher können Sie Ereignisse finden, die der Regel nahe kommen, aber nicht vollständig entsprechen.

![Schwellenwert](./images/in-app-messaging/threshold.png)

Mit dem Schieberegler **[!UICONTROL Übereinstimmungsschwellenwert]** können Sie filtern, welche Ereignisse angezeigt werden sollen. Dies kann beispielsweise auf 50 % bis 90 % festgelegt werden, um eine Liste der Ereignisse zu erhalten, die genau zwei der drei Bedingungen erfüllen.

### Registerkarte &quot;Interaktionen&quot;

Der Tab **[!UICONTROL Interaktionen]** enthält eine Liste der Interaktionsereignisse, die zu Tracking-Zwecken an die Edge gesendet wurden.

![Interaktionen](./images/in-app-messaging/interactions.png)

In der Regel gibt es vier Interaktionsereignisse, wenn eine Nachricht angezeigt wird:

```
trigger > display > interact > dismiss
```

Der Interaktion &quot;Interaktion&quot;ist ein zusätzlicher Aktionswert zugeordnet. Mögliche Werte sind &quot;angeklickt&quot;oder &quot;abbrechen&quot;.

In der Validierungsspalte wird angezeigt, ob das Interaktionsereignis von der Edge ordnungsgemäß empfangen und verarbeitet wurde.

## Validierung

Auf der Registerkarte **[!UICONTROL Validierung]** werden Validierungen für Ihre aktuelle Sitzung ausgeführt, um zu überprüfen, ob die App ordnungsgemäß für In-App-Nachrichten konfiguriert wurde:

![Validierung](./images/in-app-messaging/validation.png)

Wenn Fehler gefunden wurden, werden Details zur Behebung dieser Fehler bereitgestellt.

## Ereignisliste

![Validierung](./images/in-app-messaging/event-list.png)

Die Registerkarte **[!UICONTROL Ereignisliste]** bietet einen schnellen Überblick über alle Ereignisse in der Zuverlässigkeitssitzung, die sich auf In-App-Nachrichten beziehen. Einige der Ereignisse, die hier möglicherweise auftreten, sind:

* Anforderungen und Antworten zum Abrufen von Nachrichten
* Meldungsereignisse anzeigen
* Interaction-Tracking-Ereignisse

In dieser Ansicht können Sie viele der standardmäßigen Ereignislistenfunktionen verwenden, darunter Suchen, Anwenden von Filtern, Hinzufügen oder Entfernen von Spalten und Exportieren von Daten.

Wählen Sie ein Ereignis aus, um die Rohdetails des Ereignisses im rechten Bereich anzuzeigen.

Im rechten Detailbereich kann das ausgewählte Ereignis markiert werden. Dies ist hilfreich, um etwas zu markieren, das von einer anderen Person geprüft werden soll.
