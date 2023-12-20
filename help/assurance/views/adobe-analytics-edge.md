---
title: Analytics Events 2.0 in Assurance
description: In diesem Handbuch wird die Verwendung der Adobe Analytics- und Analytics Edge-Ansicht mit Adobe Experience Platform Assurance erläutert.
badgeBeta: label="Beta" type="Informative"
source-git-commit: f707554ea89731fbd3f013d6065fde27ba7fa811
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---

# Analytics Events 2.0 in Assurance

Analytics Events 2.0 bietet Benutzern, die ihre Adobe Analytics-Implementierung debuggen und validieren, eine umfassendere Ansicht der SDK-Ereignisse. In der Ansicht werden Ereignisse angezeigt, die von der [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/solution/adobe-analytics/) sowie [Adobe Experience Platform Edge Network SDK](https://developer.adobe.com/client-sdks/edge/edge-network/). Die Ansicht enthält außerdem ein Detailbedienfeld, das Kontext zur Verarbeitung des Ereignisses durch das Client-SDK sowie durch die Upstream-Dienste bietet, nachdem es das Gerät verlassen hat.

## Erste Schritte

Führen Sie die folgenden Schritte aus, um diese Ansicht zu verwenden:

1. [Einrichten von Adobe Experience Platform Assurance](../tutorials/implement-assurance.md).
2. [Erstellen und Herstellen einer Verbindung zu einer Assetsitzung](../tutorials/using-assurance.md).
3. In der Assurance-Benutzeroberfläche der linken Navigation **Startseite** Ansichtsmenü auswählen **Analytics Events 2.0 (Beta)**. Wenn diese Option nicht angezeigt wird, wählen Sie **Konfigurieren** Fügen Sie links unten im Fenster den **Analytics Events 2.0 (Beta)** und wählen Sie **Speichern**.

## Analytics-Ereignisansicht

Verwenden Sie die Analytics-Ereignisansicht , wenn Sie die **Adobe Analytics** mobile Erweiterung. In dieser Ansicht können Sie mühelos Analytics-Ereignisse anzeigen, die von Ihrem verbundenen Client gesendet wurden, einschließlich Verfolgungsaktion, Status verfolgen und Lebenszyklusereignissen. Durch Auswahl eines der Analytics-Ereignisse in der Tabelle können Details zur Verarbeitung des Ereignisses im rechten Bereich angezeigt werden.

![Ein Bild, das verschiedene Komponenten in der Analytics-Ereignisansicht zeigt.](./images/adobe-analytics-edge/analytics-events.png)

### Status &quot;Nachbearbeitet&quot;

Nachdem das SDK eine Netzwerkanforderung mit Adobe Analytics gestellt hat, wird Ihnen der Status angezeigt, ob Assurance die Nachbearbeitungsinformationen für die Adobe Analytics-Anfrage abrufen konnte. Die Ansicht &quot;Analytics-Ereignisse&quot;muss aktiv bleiben, während der Status der Nachbearbeitung aktiv ist, nachdem die Anfrage ausgelöst wurde.

Beachten Sie, dass der angemeldete Benutzer zum Abrufen von Nachbearbeitungs-Informationen Zugriff auf die entsprechende Report Suite haben muss.

| Status | Beschreibung |
| :----- | :---------- |
| `Queued` | Die Netzwerkanforderung ruft die Nachbearbeitungsinformationen ab. |
| `Processed` | Die Netzwerkanforderung war erfolgreich, und die Nachbearbeitungsinformationen werden empfangen. |
| `Delayed` | Die maximale Anzahl von Anfragen, die erneut versucht haben, die Nachbearbeitungs-Informationen abzurufen, wurde überschritten. |
| `Error` | Ein Fehler führte dazu, dass die Netzwerkanforderung fehlschlug. Weitere Informationen zum Fehler werden in der Ansicht &quot;Ereignisdetails&quot;angezeigt. |
| `Unauthorized` | Der Benutzer hat keinen Zugriff auf die Adobe Analytics Report Suite. |
| `Unavailable` | Die Adobe Analytics-Anfrage weist keine entsprechende `AnalyticsResponse` -Ereignis. |
| `No Debug Flag` | Die aktuelle Adobe Analytics- oder Assurance-SDK-Version unterstützt die Analytics-Debugging-Funktion möglicherweise nicht. Weitere Informationen finden Sie im [Handbuch zur Fehlerbehebung](../troubleshooting.md). |
| `Expired` | Die `AnalyticsTrack` oder `LifecycleStart` -Ereignis ist älter als 24 Stunden. |

### Ansicht mit Ereignisdetails

Für ein Analytics-Verfolgungsereignis enthält die Detailansicht die folgenden Teile:

- Ein Analytics-Anfrageereignis vom Typ &quot;SDK&quot;.
- Meta- und Kontextdaten aus der Anfrage, z. B. Report Suite-ID, SDK-Erweiterungsversionen und Kontextdaten.
- Nachbearbeitete Informationen zum Analytics-Ereignis, das die Zuordnung von Vars, eVars und Props enthält.

### Validierung der Analytics-Ansicht

Die Überprüfungsansicht ermöglicht es Ihnen, die Ergebnisse von Überprüfungsskripten für Analytics einfach anzuzeigen. Fehler, die von Validatoren angezeigt werden, können Links zu den Stellen enthalten, an denen sie korrigiert werden sollen, oder Ereignisse anzeigen, die einen Fehlerstatus aufweisen.

![Ein Bild, das die Registerkarte &quot;Validatoren&quot;in der Analytics-Ansicht anzeigt.](./images/adobe-analytics-edge/analytics-validation-view.png)

## Analytics Edge-Ansicht

Verwenden Sie die Analytics Edge-Ansicht, wenn Sie **Edge Network** oder **Edge Bridge** mobile Erweiterungen. Um diese Ansicht zu aktivieren, wählen Sie oben rechts den Umschalter &quot;Analytics Edge (Beta)&quot;aus, um die über das Edge-Netzwerk gesendeten Analytics-Ereignisse in Ihrer aktuellen Sitzung anzuzeigen. Dies umfasst alle Ereignisse, die von der Lifecycle-Erweiterung, Edge-Anforderungen und/oder Edge Bridge-Ereignissen basierend auf &quot;Track Action&quot;und &quot;Track State&quot;ausgelöst wurden.

![Ein Bild, das einen Umschalter anzeigt, der zum Umschalten zwischen der Analytics-Ansicht und der Analytics-Edge-Ansicht verwendet wurde.](./images/adobe-analytics-edge/analytics-view-toggle.png)

Die Analytics Edge-Ansicht enthält Informationen zu Analytics-bezogenen Edge-Anforderungen und -Lebenszyklusmethoden, die vom Client gesendet werden. Durch Auswahl eines Ereignisses in der Liste werden im rechten Bereich die Ereignisse angezeigt, die vom Client-SDK sowie vom Upstream-Dienst verarbeitet wurden, nachdem diese das Gerät verlassen haben. So können Sie die Ereigniskette, die sich aus einem Aufruf ergab, einfach anzeigen.

![Ein Bild, das verschiedene Komponenten in der Analytics Edge-Ansicht zeigt.](./images/adobe-analytics-edge/edge-analytics-events.png)

### Analytics Edge-Validierung

Mit der Überprüfungsansicht von Analytics Edge können Sie die Ergebnisse zu Überprüfungsskripten im Zusammenhang mit Analytics Edge einfach anzeigen. Fehler, die von Validatoren angezeigt werden, können Links zu den Stellen enthalten, an denen sie korrigiert werden sollen, oder Ereignisse anzeigen, die einen Fehlerstatus aufweisen.

![Ein Bild, das die Registerkarte &quot;Validatoren&quot;in der Analytics Edge-Ansicht anzeigt.](./images/adobe-analytics-edge/edge-analytics-validation-view.png)
