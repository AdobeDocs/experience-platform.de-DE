---
title: Adobe Analytics-Ansicht in Assurance
description: In diesem Handbuch wird die Verwendung von Adobe Analytics mit Adobe Experience Platform Assurance erläutert.
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 66c9b8c1489b86b0b928fc37380f2187a7d237cf
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# Adobe Analytics-Ereignisansicht in Assurance

Analytics Events bietet eine umfassendere Ansicht von SDK Events für Anwender, die ihre Adobe Analytics-Implementierung debuggen und validieren. In der Ansicht werden Ereignisse angezeigt, die von der [Adobe Experience Platform Edge Network SDK ](https://developer.adobe.com/client-sdks/edge/edge-network/) der [Adobe Experience Platform Mobile SDK an Adobe Analytics gesendet ](https://developer.adobe.com/client-sdks/solution/adobe-analytics/). Die Ansicht enthält auch ein Bedienfeld Details , das Kontext dazu bietet, wie das Ereignis von der Client-SDK und den Upstream-Services verarbeitet wurde, nachdem es das Gerät verlassen hat.

## Erste Schritte

Um diese Ansicht zu verwenden, führen Sie die folgenden Schritte aus:

1. [Einrichten von Adobe Experience Platform Assurance](../tutorials/implement-assurance.md).
2. [Erstellen einer Assurance-Sitzung und Herstellen einer Verbindung zu ihr](../tutorials/using-assurance.md).
3. Wählen Sie in der Assurance-Benutzeroberfläche im linken **(**) die Option **Analytics-Ereignisse**. Wenn diese Option nicht angezeigt wird, wählen Sie **Konfigurieren** unten links im Fenster aus, fügen Sie die **Analytics-Ereignisse** hinzu und klicken Sie auf **Speichern**.

## Analytics Edge-Ansicht

Verwenden Sie die Ansicht „Analytics Edge&quot;, wenn Sie die Erweiterungen **Edge Network** oder **Edge Bridge** Mobile verwenden. Diese Ansicht wird aktiviert, wenn oben rechts der Umschalter „Analytics Edge View“ aktiviert wird, der die über das Edge-Netzwerk gesendeten Analytics-Ereignisse in Ihrer aktuellen Sitzung anzeigt. Dazu gehören alle Ereignisse, die von der Lebenszykluserweiterung, der Edge-Erweiterung und/oder der Edge Bridge-Erweiterung ausgelöst wurden.

![Ein Bild, das einen Umschalter anzeigt, der zur Edge-Ansicht von Analytics gewechselt ist.](./images/adobe-analytics/edge-analytics-view-toggle.png)

Die Ansicht Analytics-Edge enthält Informationen zu Analytics-bezogenen Edge-Ereignissen und Lebenszyklus-Ereignissen, die vom Client gesendet werden. Wenn Sie ein Ereignis in der Liste auswählen, werden im Bereich für die Ereignisdetailansicht auf der rechten Seite die Ereignisse angezeigt, die von der Client-SDK und vom Upstream-Service verarbeitet wurden, nachdem sie das Gerät verlassen haben. Auf diese Weise können Sie die Kette von Ereignissen, die aus einem Aufruf resultierten, einfach anzeigen.

![Abbildung mit verschiedenen Komponenten in der Analytics-Edge-Ansicht für das Edge Bridge-Szenario.](./images/adobe-analytics/edgebridge-analytics-events.png)

Das **Nachbearbeitungs-Daten**-Ereignis in der Liste bestätigt, dass die Daten erfolgreich verarbeitet und an Adobe Analytics gesendet wurden. Wenn dieses Ereignis oder verarbeitete Daten fehlen, können Benutzer jedes Ereignis in der Liste erweitern, um detaillierte Debugging-Informationen anzuzeigen.

### Analytics Edge-Ereignisdetailansicht

Für ein Edge-Anfrageereignis oder ein Analytics-Tracking-Ereignis enthält die Detailansicht die folgenden Informationen:

* Ereignisdetails: Ein SDK-Edge-Anforderungsereignis, das ausgelöst wird.
* Edge Bridge-Anfrage: Ein Ereignis, das ausschließlich für den Workflow der Edge Bridge-Erweiterung bestimmt ist.
* Datenstrom: Ein Ereignis, das für den Datenstrom für diese Sitzung dargestellt wird.
* Edge-Treffer erhalten: Stellt den von Edge empfangenen Treffer dar.
* Edge-Treffer verarbeitet: Stellt den in Edge verarbeiteten Treffer dar.
* Analytics-Treffer: Stellt den von Analytics empfangenen Treffer dar.
* Analytics-Zuordnung: Stellt den Datenzuordnungsstatus in Analytics dar.
* Analytics Responsed: Der Antwortstatus von Analytics.
* Nachverarbeitungsdaten: Informationen zum Ereignis, das die Zuordnung von eVars, eVars und Props enthält.

### Validierung von Analytics Edge

Mit der Validierungsansicht von Analytics Edge können Sie die Ergebnisse von Validierungsskripten im Zusammenhang mit einer Analytics Edge-Sitzung einfach anzeigen. Fehler, die von Validatoren angezeigt werden, können Links zu enthalten, in denen sie behoben werden sollten, oder Ereignisse mit Fehlerstatus anzeigen.

![Ein Bild, das die Registerkarte „Validatoren“ in der Ansicht „Analytics Edge&quot; anzeigt.](./images/adobe-analytics/edge-analytics-validation-view.png)

## Analytics-Ereignisansicht

Verwenden Sie die Analytics-Ereignisansicht, wenn Sie die Erweiterung **Adobe Analytics** Mobile verwenden. In dieser Ansicht können Sie ganz einfach Analytics-Ereignisse anzeigen, die von Ihrem verbundenen Client gesendet wurden, einschließlich „Aktion verfolgen“, „Status verfolgen“ und „Lebenszyklus-Ereignisse“. Diese Ansicht ist aktiv, wenn der Umschalter „Analytics Edge-Ansicht“ oben rechts deaktiviert ist.

![Ein Bild, das einen Umschalter anzeigt, der zur Analytics-Ansicht gewechselt ist.](./images/adobe-analytics/direct-analytics-view-toggle-button.png)

Durch Auswahl eines der Analytics-Ereignisse in der Ereignistabelle können Details zur Verarbeitung des Ereignisses im rechten Bedienfeld angezeigt werden.

![Ein Bild, das verschiedene Komponenten in der Ansicht „Analytics-Ereignisse“ zeigt.](./images/adobe-analytics/analytics-events.png)

### Status „Nachbearbeitet“

Nachdem der SDK eine Netzwerkanfrage mit Adobe Analytics gestellt hat, werden Sie über den Status informiert, ob Assurance die Nachbearbeitungsinformationen für die Adobe Analytics-Anfrage abrufen konnte. Die Ansicht „Analytics-Ereignisse“ muss aktiv bleiben, während der Nachbearbeitungsstatus nach dem Auslösen der Anfrage aktiv ist.

Beachten Sie, dass der angemeldete Benutzer Zugriff auf die entsprechende Report Suite haben muss, um Nachbearbeitungs-Informationen abzurufen.

| Status | Beschreibung |
| :----- | :---------- |
| `Queued` | Die Netzwerkanfrage ruft die Nachverarbeitungsinformationen ab. |
| `Processed` | Die Netzwerkanfrage war erfolgreich, und die Nachverarbeitungsinformationen werden empfangen. |
| `Delayed` | Die maximale Anzahl der erneuten Anfragen zum Abrufen der Nachbearbeitungs-Informationen wurde überschritten. |
| `Error` | Ein Fehler führte dazu, dass die Netzwerkanfrage fehlschlug. Weitere Informationen zum Fehler finden Sie in der Ansicht Ereignisdetails . |
| `Unauthorized` | Die Benutzenden haben keinen Zugriff auf die Adobe Analytics Report Suite. |
| `Unavailable` | Die Adobe Analytics-Anfrage hat kein entsprechendes `AnalyticsResponse`. |
| `No Debug Flag` | Die aktuelle Adobe Analytics- oder Assurance SDK-Version unterstützt die Analytics-Debugging-Funktion möglicherweise nicht. Weitere Informationen finden Sie im [Handbuch zur Fehlerbehebung](../troubleshooting.md). |
| `Expired` | Das `AnalyticsTrack` oder `LifecycleStart` Ereignis ist älter als 24 Stunden. |

### Ansicht „Ereignisdetails“

Für ein Analytics-Tracking-Ereignis enthält die Detailansicht die folgenden Teile:

* Ein von SDK Analytics stammendes Anfrageereignis.
* Meta- und Kontextdaten aus der Anfrage, z. B. Report Suite-ID, SDK-Erweiterungsversionen und Kontextdaten.
* Nachverarbeitete Informationen zum Analytics-Ereignis, das die Zuordnung von eVars, eVars und Props enthält.

### Validierung der Analytics-Ansicht

Die Validierungsansicht ermöglicht es Ihnen, die Ergebnisse der Validierungsskripte im Zusammenhang mit Analytics einfach anzuzeigen. Fehler, die von Validatoren angezeigt werden, können Links zu enthalten, in denen sie behoben werden sollten, oder Ereignisse mit Fehlerstatus anzeigen.

![Ein Bild, das die Registerkarte „Validatoren“ in der Analytics-Ansicht anzeigt.](./images/adobe-analytics/analytics-validation-view.png)