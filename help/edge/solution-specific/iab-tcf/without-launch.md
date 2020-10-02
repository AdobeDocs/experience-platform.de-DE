---
title: Verwenden von IAB TCF 2.0 ohne Start
seo-title: Einrichten der IAB TCF 2.0-Zustimmung mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie die IAB TCF 2.0-Zustimmung mit dem Adobe Experience Platform Web SDK einrichten.
seo-description: Erfahren Sie, wie Sie die IAB TCF 2.0-Zustimmung mit dem Adobe Experience Platform Web SDK einrichten.
translation-type: tm+mt
source-git-commit: 48cebe994b450b0dac5e6f256ab81827a7e8a0d5
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---


# Verwenden von IAB TCF 2.0 mit der Adobe Experience Platform Web SDK-Erweiterung

In diesem Handbuch wird gezeigt, wie das Interactive Advertising Bureau Transparency &amp; Consent Framework, Version 2.0 (IAB TCF 2.0), ohne Experience Platform Launch in das Adobe Experience Platform Web SDK integriert werden kann. Einen Überblick über die Integration mit IAB TCF 2.0 finden Sie in der [Übersicht](./overview.md). Eine Anleitung zur Integration in Experience Platform Launch finden Sie im Handbuch [IAB TCF 2.0 für Experience Platform Launch](./with-launch.md).

## Erste Schritte

In diesem Handbuch wird die `__tcfapi` Oberfläche für den Zugriff auf die Informationen zur Einwilligung verwendet. Die direkte Integration mit Ihrem Cloud-Management-Provider (CMP) ist möglicherweise einfacher. Die Informationen in diesem Handbuch können jedoch weiterhin nützlich sein, da die CMP im Allgemeinen eine ähnliche Funktionalität wie die TCF-API bieten.

>[!NOTE]
>
>Bei diesen Beispielen wird davon ausgegangen, dass der Code zum Zeitpunkt der Ausführung auf der Seite definiert `window.__tcfapi` ist. CMPs können einen Haken bereitstellen, in dem Sie diese Funktionen ausführen können, wenn das `__tcfapi` Objekt fertig ist.

Um IAB TCF 2.0 mit Experience Platform Launch und der AEP Web SDK Extension zu verwenden, benötigen Sie ein XDM-Schema. Wenn Sie keines dieser beiden Optionen eingestellt haben, lesen Sie den Beginn in der Anleitung zum JavaScript-Schnellzugriff auf das [Adobe Experience Platform Web SDK-JavaScript, bevor Sie fortfahren](../../getting-started/quick-start-without-launch.md) .

Darüber hinaus erfordert dieses Handbuch ein Verständnis des Adobe Experience Platform Web SDK. Für einen schnellen Auffrischungskommentar lesen Sie bitte die [Adobe Experience Platform Web SDK-Übersicht](../../home.md) und die Dokumentation [Häufig gestellte Fragen](../../getting-started/web-sdk-faq.md) .

## Standardgenehmigung aktivieren

Wenn Sie alle Unbekannte Nutzer gleich behandeln möchten, können Sie die Standardgenehmigung auf `pending`. Dadurch werden Experience Ereignisses in die Warteschlange gestellt, bis die Voreinstellungen für die Zustimmung erhalten wurden.

Weitere Informationen zur Standardgenehmigung finden Sie im Abschnitt zur [Standardgenehmigung](../../fundamentals/configuring-the-sdk.md#default-consent) in der Platform Web SDK-Konfigurationsdokumentation.

### Festlegen der Standardgenehmigung basierend auf `gdprApplies`

Einige CMPs bieten die Möglichkeit zu bestimmen, ob die Allgemeine Datenschutzverordnung (GDPR) für den Kunden gilt. Wenn Sie die Zustimmung für Kunden übernehmen möchten, für die GDPR nicht gilt, können Sie das `gdprApplies` Flag im TCF-API-Aufruf verwenden.

Das folgende Beispiel zeigt eine Möglichkeit, dies zu tun:

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

In diesem Beispiel wird der `configure` Befehl aufgerufen, nachdem der Befehl von der TCF-API abgerufen `tcData` wurde. Wenn `gdprApplies` &quot;true&quot;festgelegt ist, wird die Standardgenehmigung auf `pending`. Wenn `gdprApplies` &quot;false&quot;festgelegt ist, wird die Standardgenehmigung auf `in`. Achten Sie darauf, die `alloyConfiguration` Variable mit Ihrer Konfiguration auszufüllen.

>[!NOTE]
>
>Wenn die standardmäßige Zustimmung auf `in`festgelegt ist, kann der `setConsent` Befehl weiterhin verwendet werden, um die Voreinstellungen für die Zustimmung Ihrer Kunden aufzuzeichnen.

## Verwenden des Ereignisses setConsent

Die IAB TCF 2.0-API bietet ein Ereignis für den Zeitpunkt, zu dem die Zustimmung vom Kunden aktualisiert wird. Dies geschieht, wenn der Kunde seine Voreinstellungen zum ersten Mal festlegt und die Voreinstellungen aktualisiert.

Das folgende Beispiel zeigt eine Möglichkeit, dies zu tun:

```javascript
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

Dieser Codeblock überwacht das `useractioncomplete` Ereignis und legt dann die Zustimmung fest, wobei die Zustimmungszeichenfolge und die `gdprApplies` -Flag übergeben werden. Wenn Sie benutzerdefinierte Identitäten für Ihre Kunden haben, füllen Sie die `identityMap` Variable unbedingt aus. Weitere Informationen zum Anrufen finden Sie im Leitfaden zur [Unterstützung der Zustimmung](../../fundamentals/supporting-consent.md) `setConsent`.

## Einschließlich der Einwilligungsinformationen in sendEvent

In XDM-Schemas können Sie Informationen zu den Voreinstellungen für die Zustimmung von Experience Ereignisses speichern. Es gibt zwei Möglichkeiten, diese Informationen jedem Ereignis hinzuzufügen.

Zunächst können Sie bei jedem `sendEvent` Aufruf das entsprechende XDM-Schema angeben. Das folgende Beispiel zeigt eine Möglichkeit, dies zu tun:

```javascript
var sendEventOptions = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    sendEventOptions.xdm.consentStrings = [{
      consentStandard: "IAB TCF"
      consentStandardVersion: "2.0"
      consentStringValue: tcData.tcString,
      gdprApplies: tcData.gdprApplies
    }];
    window.alloy("sendEvent", sendEventOptions);
  }
});
```

In diesem Beispiel werden die Informationen zur Einwilligung für die TCF-API abgerufen und dann ein Ereignis mit den dem XDM-Schema hinzugefügten Informationen zur Einwilligung gesendet. Informationen zu den [Befehlsoptionen finden Sie im Handbuch zu Tracking-Ereignissen](../../fundamentals/tracking-events.md) `sendEvent` .

Die andere Möglichkeit, die Einwilligungsinformationen jeder Anforderung hinzuzufügen, ist der `onBeforeEventSend` Rückruf. Weitere Informationen dazu finden Sie im Abschnitt zum globalen [](../../fundamentals/tracking-events.md#modifying-events-globally) Ändern von Ereignissen in der Dokumentation zu Tracking-Ereignissen.

## Nächste Schritte

Nachdem Sie nun gelernt haben, wie Sie IAB TCF 2.0 mit der Adobe Experience Platform Web SDK-Erweiterung verwenden können, können Sie sich auch für die Integration mit anderen Adoben wie Adobe Analytics oder Echtzeit-Kundendatenplattform entscheiden. Weitere Informationen finden Sie in der Übersicht [zum](./overview.md) IAB-Transparenz- und Bestätigungsrahmen 2.0.
