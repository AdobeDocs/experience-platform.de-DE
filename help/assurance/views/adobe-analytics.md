---
title: Adobe Analytics-Ansicht in Assurance
description: In diesem Handbuch wird die Verwendung von Adobe Analytics mit Adobe Experience Platform Assurance erläutert.
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 515f58175a8ccba03581ce4d7faf23fdfed3571e
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# Adobe Analytics-Ansicht in Assurance

>[!IMPORTANT]
>
>Die Analytics-Ereignisansicht ist im Plug-in **Analytics Events 2.0 (Beta)** konsolidiert.  Sie wird in der kommenden Zukunft aus der Zuverlässigkeitserklärung entfernt. Es wird empfohlen, das Plug-in **Analytics Events 2.0 (Beta)** für Ihr Analytics-Debugging für die Assurance-Sitzungen zu verwenden.

Die Adobe Experience Platform Assurance-Integration mit Adobe Analytics bietet Benutzern, die ihre Adobe Analytics-Implementierung debuggen und validieren, eine umfassendere Ansicht der SDK-Ereignisse. In der Ansicht werden nun vom [Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/) an Adobe Analytics gesendete Lebenszyklus- und Aktions-/Statusereignisse angezeigt. Die Ansicht enthält auch &quot;Antwort&quot;-Details, die Informationen darüber enthalten, wie die Ereignisse nach der Anwendung der Verarbeitungsregeln der jeweiligen Report Suite verarbeitet wurden.

![](./images/adobe-analytics/overview.png)

## Erste Schritte

Bevor Sie fortfahren, stellen Sie bitte sicher, dass Sie über die folgenden Dienste verfügen:

- Die [Adobe Experience Platform-Datenerfassungs-Benutzeroberfläche](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Weiterführende Informationen zur Installation von Assurance in Ihrer Anwendung finden Sie im [Implementierungshandbuch für Assurance](../tutorials/implement-assurance.md).

## Status &quot;Nachbearbeitet&quot;

Nachdem das SDK eine Netzwerkanforderung mit Adobe Analytics gestellt hat, wird Ihnen der Status angezeigt, ob Assurance die Nachbearbeitungsinformationen für die Adobe Analytics-Anfrage abrufen konnte.

Beachten Sie, dass der angemeldete Benutzer zum Abrufen von Nachbearbeitungs-Informationen Zugriff auf die entsprechende Report Suite haben muss.

| Status | Beschreibung |
| :----- | :---------- |
| `Queued` | Die Netzwerkanforderung ruft die Nachbearbeitungsinformationen ab. |
| `Processed` | Die Netzwerkanforderung war erfolgreich, und die Nachbearbeitungsinformationen werden empfangen. |
| `Delayed` | Die maximale Anzahl von Anfragen, die erneut versucht haben, die Nachbearbeitungs-Informationen abzurufen, wurde überschritten. |
| `Error` | Ein Fehler führte dazu, dass die Netzwerkanforderung fehlschlug. Weitere Informationen zum Fehler werden in der Ansicht &quot;Ereignisdetails&quot;angezeigt. |
| `Unauthorized` | Der Benutzer hat keinen Zugriff auf die Adobe Analytics Report Suite. |
| `Unavailable` | Die Adobe Analytics-Anfrage weist kein entsprechendes `AnalyticsResponse` -Ereignis auf. |
| `No Debug Flag` | Die aktuelle Adobe Analytics- oder Assurance-SDK-Version unterstützt die Analytics-Debugging-Funktion möglicherweise nicht. Weitere Informationen finden Sie im [Handbuch zur Fehlerbehebung](../troubleshooting.md). |
| `Expired` | Das Ereignis `AnalyticsTrack` oder `LifecycleStart` ist älter als 24 Stunden. |

## Ansicht mit Ereignisdetails

Für ein Analytics-Tracking-Ereignis enthält die Detailansicht die folgenden wertvollen Teile:

- Ein Analytics-Anfrageereignis vom Typ &quot;SDK&quot;.
- OOTB-Meta und Kontextdaten aus der Anfrage, wie z. B. Report Suite-ID, SDK-Erweiterungsversionen, OOTB-Kontextdaten usw.
- Nachbearbeitete Informationen zum Analytics-Ereignis, das die Zuordnung von Vars, eVars, Props usw. enthält.
