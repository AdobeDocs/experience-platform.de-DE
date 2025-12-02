---
title: Konfigurationseinstellungen der Datenerfassung
description: Konfigurieren Sie Datenerfassungseinstellungen in der Tag-Erweiterung „Web SDK".
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# Konfigurationseinstellungen der Datenerfassung

In diesem Konfigurationsabschnitt können Sie festlegen, wie Daten in der gesamten Erweiterung erfasst werden.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Extensions]** und wählen Sie **[!UICONTROL Configure]** auf der [!UICONTROL Adobe Experience Platform Web SDK] aus.
1. Scrollen Sie nach unten zum Abschnitt **[!UICONTROL Data collection]** .

![Bild mit den Datenerfassungseinstellungen der Web-SDK-Tag-Erweiterung in der Tags-Benutzeroberfläche.](../assets/web-sdk-ext-collection.png)

Die folgenden Optionen sind verfügbar:

## [!UICONTROL On before event send callback]

Eine Rückruffunktion zur Auswertung und Änderung der an Adobe gesendeten Payload. Innerhalb des Code-Editors haben Sie Zugriff auf die folgenden Variablen:

* **`content.xdm`**: Die XDM-Payload für das Ereignis.
* **`content.data`**: Die Payload des Datenobjekts für das Ereignis.
* **`return true`**: Sofort den Callback beenden und Daten mit den aktuellen Werten im `content` Objekt an Adobe senden.
* **`return false`**: Sofort den Callback beenden und das Senden von Daten an Adobe abbrechen.

Alle Variablen, die außerhalb von `content` definiert wurden, können verwendet werden, sind jedoch nicht in der Payload enthalten, die an Adobe gesendet wird.

>[!WARNING]
>
>Dieser Callback ermöglicht die Verwendung von benutzerdefiniertem Code. Wenn ein Code, den Sie in den Callback einbeziehen, eine nicht abgefangene Ausnahme auslöst, wird die Verarbeitung für das Ereignis angehalten. **Daten werden nicht an Adobe gesendet.**

```js
// Use nullish coalescing assignments to add objects if they don't yet exist
content.xdm.commerce ??= {};
content.xdm.commerce.order ??= {};

// Then add the purchase ID
content.xdm.commerce.order.purchaseID = "12345";

// Use optional chaining to prevent undefined errors when setting tracking code to lower case
if(content.xdm.marketing?.trackingCode) content.xdm.marketing.trackingCode = content.xdm.marketing.trackingCode.toLowerCase();

// Delete operating system version
if(content.xdm.environment) delete content.xdm.environment.operatingSystemVersion;

// Immediately end onBeforeEventSend logic and send the data to Adobe for this event type
if (content.xdm.eventType === "web.webInteraction.linkClicks") {
  return true;
}

// Cancel sending data if it is a known bot
if (myBotDetector.isABot()) {
  return false;
}
```

>[!TIP]
>Vermeiden Sie die Rückgabe von `false` beim ersten Ereignis auf einer Seite. Eine Rückkehr der `false` beim ersten Ereignis kann sich negativ auf die Personalisierung auswirken.

Dieser Callback ist das Tag, das der [`onBeforeEventSend`](/help/collection/js/commands/configure/onbeforeeventsend.md) in der JavaScript-Bibliothek entspricht.

## [!UICONTROL Collect internal link clicks]

Ein Kontrollkästchen, das die Erfassung von Linktracking-Daten innerhalb Ihrer Site oder Eigenschaft ermöglicht. Dieses Kontrollkästchen entspricht dem Tag-[`clickCollection.internalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) in der JavaScript-Bibliothek. Wenn Sie dieses Kontrollkästchen aktivieren, werden Optionen für die Ereignisgruppierung angezeigt:

* **[!UICONTROL No event grouping]**: Linktracking-Daten werden in separaten Ereignissen an Adobe gesendet. Link-Klicks, die in separaten Ereignissen gesendet werden, können die vertragliche Nutzung der an Adobe Experience Platform gesendeten Daten erhöhen.
* **[!UICONTROL Event grouping using session storage]**: Speichern von Linktracking-Daten im Sitzungsspeicher bis zum nächsten Ereignis „Seitenansicht“. Beim nächsten Ereignis, das als „Seitenansicht“ gilt, werden die gespeicherten Linktracking-Daten mit der Ereignis-Payload „Seitenansicht“ zusammengeführt. Adobe empfiehlt, diese Einstellung beim Tracking interner Links zu aktivieren.
* **[!UICONTROL Event grouping using local object]**: Speichern von Linktracking-Daten in einem lokalen Objekt bis zum nächsten „Seitenansicht“-Ereignis. Wenn ein Besucher zu einer neuen Browser-Seite navigiert, gehen Linktracking-Daten verloren. Diese Einstellung ist besonders im Kontext von Einzelseitenanwendungen von Vorteil.

Die Tag-Bibliothek betrachtet ein bestimmtes Ereignis als „Seitenansicht“, wenn die folgenden Elemente in der Payload enthalten sind:

* `xdm.web.webPageDetails.name` enthält einen Zeichenfolgenwert
* `xdm.web.webPageDetails.pageViews.value` ist größer als `0`

## [!UICONTROL Collect external link clicks]

Ein Kontrollkästchen, das die Sammlung externer Links aktiviert. Dieses Kontrollkästchen entspricht dem Tag-[`clickCollection.externalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) in der JavaScript-Bibliothek.

## [!UICONTROL Collect download link clicks]

Ein Kontrollkästchen, das die Sammlung von Download-Links aktiviert. Dieses Kontrollkästchen entspricht dem Tag-[`clickCollection.downloadLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) in der JavaScript-Bibliothek.

## [!UICONTROL Download link qualifier]

Ein regulärer Ausdruck, der eine Link-URL als Download-Link kennzeichnet. Diese Zeichenfolge ist das Tag, das der [`downloadLinkQualifier`](/help/collection/js/commands/configure/downloadlinkqualifier.md) in der JavaScript-Bibliothek entspricht.

## [!UICONTROL Filter click properties]

Eine Rückruffunktion, mit der klickbezogene Eigenschaften vor der Sammlung ausgewertet und geändert werden können. Diese Funktion wird vor dem [!UICONTROL On before event send callback] ausgeführt und ist das Tag, das der [`clickCollection.filterClickDetails`](/help/collection/js/commands/configure/clickcollection.md) in der JavaScript-Bibliothek entspricht. Innerhalb des Code-Editors haben Sie Zugriff auf die folgenden Variablen:

* **`content.clickedElement`**: Das angeklickte DOM-Element.
* **`content.pageName`**: Der Seitenname zum Zeitpunkt des Klicks.
* **`content.linkName`**: Der Name des angeklickten Links.
* **`content.linkRegion`**: Die Region des angeklickten Links.
* **`content.linkType`**: Der Link-Typ (Beenden, Herunterladen oder sonstiges).
* **`content.linkURL`**: Die Ziel-URL des angeklickten Links.
* **`return true`**: Sofort den Callback mit den aktuellen Variablenwerten beenden.
* **`return false`**: Sofort den Callback beenden und die Datenerfassung abbrechen.
* Alle Variablen, die außerhalb von `content` definiert wurden, können verwendet werden, sind jedoch nicht in der Payload enthalten, die an Adobe gesendet wird.

>[!TIP]
>
>Das Feld **[!UICONTROL On before link click send]** ist ein veralteter Callback, der nur für Eigenschaften sichtbar ist, für die er bereits konfiguriert wurde. Es handelt sich dabei um das Tag-Äquivalent zu [`onBeforeLinkClickSend`](/help/collection/js/commands/configure/onbeforelinkclicksend.md) in der JavaScript-Bibliothek. Verwenden Sie den **[!UICONTROL Filter click properties]**-Callback, um Klickdaten zu filtern oder anzupassen, oder verwenden Sie die **[!UICONTROL On before event send callback]**, um die gesamte an Adobe gesendete Payload zu filtern oder anzupassen. Wenn sowohl der **[!UICONTROL Filter click properties]** als auch der **[!UICONTROL On before link click send]** Callback festgelegt sind, wird nur der **[!UICONTROL Filter click properties]** Callback ausgeführt.

## Kontexteinstellungen

Sammelt automatisch Besucherinformationen, mit denen bestimmte XDM-Felder für Sie ausgefüllt werden. Sie können zwischen **[!UICONTROL All default context information]** und **[!UICONTROL Specific context information]** wählen. Es handelt sich dabei um das Tag-Äquivalent zu [`context`](/help/collection/js/commands/configure/context.md) in der JavaScript-Bibliothek.

* **[!UICONTROL Web]**: Sammelt Informationen über die aktuelle Seite.
* **[!UICONTROL Device]**: Sammelt Informationen zum Gerät des Benutzers.
* **[!UICONTROL Environment]**: Sammelt Informationen zum Browser des Benutzers.
* **[!UICONTROL Place context]**: Sammelt Informationen zum Standort des Benutzers.
* **[!UICONTROL High entropy user-agent hints]**: Erfasst detailliertere Informationen über das Gerät des Benutzers.
