---
title: IAB TCF 2.0-Unterstützung mithilfe des Adobe Experience Platform Web SDK integrieren
description: Erfahren Sie, wie Sie die IAB TCF 2.0-Unterstützung für Ihre Website ohne Verwendung von Adobe Experience Platform Launch einrichten.
seo-description: Erfahren Sie, wie Sie die IAB TCF 2.0-Zustimmung mit dem Adobe Experience Platform Web SDK einrichten.
translation-type: tm+mt
source-git-commit: b9fb71ac7eca95c65165d6780b681ada3f16325b
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# Integrieren der IAB TCF 2.0-Unterstützung in das Platform Web SDK

In diesem Handbuch wird gezeigt, wie das Interactive Advertising Bureau Transparency &amp; Consent Framework, Version 2.0 (IAB TCF 2.0), ohne Verwendung von Experience Platform Launch in das Adobe Experience Platform Web SDK integriert werden kann. Eine Übersicht zur Integration in IAB TCF 2.0 finden Sie im Abschnitt [overview](./overview.md). Eine Anleitung zur Integration in Experience Platform Launch finden Sie im Handbuch [IAB TCF 2.0 für Experience Platform Launch](./with-launch.md).

## Erste Schritte

Dieses Handbuch verwendet die `__tcfapi`-Schnittstelle für den Zugriff auf die Informationen zur Einwilligung. Die direkte Integration mit Ihrem Cloud-Management-Provider (CMP) ist möglicherweise einfacher. Die Informationen in diesem Handbuch können jedoch weiterhin nützlich sein, da die CMP im Allgemeinen eine ähnliche Funktionalität wie die TCF-API bieten.

>[!NOTE]
>
>Bei diesen Beispielen wird davon ausgegangen, dass `window.__tcfapi` bei Ausführung des Codes auf der Seite definiert ist. CMPs können einen Haken bereitstellen, in dem Sie diese Funktionen ausführen können, wenn das `__tcfapi`-Objekt fertig ist.

Um IAB TCF 2.0 mit Experience Platform Launch und der Adobe Experience Platform Web SDK Extension zu verwenden, benötigen Sie ein XDM-Schema. Wenn Sie keines dieser beiden Optionen eingestellt haben, zeigen Sie Beginn auf dieser Seite an, bevor Sie fortfahren.

Darüber hinaus erfordert dieses Handbuch ein Verständnis des Adobe Experience Platform Web SDK. Eine kurze Auffrischung erhalten Sie in der Dokumentation [Adobe Experience Platform Web SDK overview](../../home.md) und [Häufig gestellte Fragen](../../web-sdk-faq.md).

## Standardgenehmigung aktivieren

Wenn Sie alle Unbekannte Nutzer gleich behandeln möchten, können Sie die Standardgenehmigung auf `pending` oder `out` festlegen. Diese Warteschlangen verwerfen oder verwerfen Experience Ereignisses, bis die Voreinstellungen für die Zustimmung erhalten sind.

Weitere Informationen zur Standardgenehmigung finden Sie im Abschnitt [Standardgenehmigung](../../fundamentals/configuring-the-sdk.md#default-consent) in der Platform Web SDK-Konfigurationsdokumentation.

### Standardgenehmigung basierend auf `gdprApplies` festlegen

Einige CMPs bieten die Möglichkeit zu bestimmen, ob die Allgemeine Datenschutzverordnung (GDPR) für den Kunden gilt. Wenn Sie die Zustimmung für Kunden übernehmen möchten, für die GDPR nicht gilt, können Sie das `gdprApplies`-Flag im TCF-API-Aufruf verwenden.

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

In diesem Beispiel wird der Befehl `configure` aufgerufen, nachdem `tcData` von der TCF-API abgerufen wurde. Wenn `gdprApplies` &quot;true&quot;ist, wird die Standardgenehmigung auf `pending` eingestellt. Wenn `gdprApplies` den Wert false hat, wird die Standardgenehmigung auf `in` eingestellt. Achten Sie darauf, die Variable `alloyConfiguration` mit Ihrer Konfiguration auszufüllen.

>[!NOTE]
>
>Wenn die Standardgenehmigung auf `in` eingestellt ist, kann der Befehl `setConsent` weiterhin verwendet werden, um die Voreinstellungen für die Zustimmung Ihrer Kunden aufzuzeichnen.

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

Dieser Codeblock überwacht das `useractioncomplete`-Ereignis und stellt dann die Zustimmung ein, wobei die Zustimmungszeichenfolge und die `gdprApplies`-Flag übergeben werden. Wenn Sie benutzerdefinierte Identitäten für Ihre Kunden haben, füllen Sie die Variable `identityMap` aus. Weitere Informationen zum Aufrufen von `setConsent` finden Sie im Handbuch [Unterstützungszustimmung](../../consent/supporting-consent.md).

## Einschließlich der Einwilligungsinformationen in sendEvent

Innerhalb von XDM-Schemas können Sie Informationen zu den Voreinstellungen für die Zustimmung von Experience Ereignisses speichern. Es gibt zwei Möglichkeiten, diese Informationen jedem Ereignis hinzuzufügen.

Zunächst können Sie bei jedem `sendEvent`-Aufruf das entsprechende XDM-Schema bereitstellen. Das folgende Beispiel zeigt eine Möglichkeit, dies zu tun:

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

In diesem Beispiel werden die Informationen zur Einwilligung für die TCF-API abgerufen und dann ein Ereignis mit den dem XDM-Schema hinzugefügten Informationen zur Einwilligung gesendet. Informationen zu den [Tracking-Ereignissen](../../fundamentals/tracking-events.md) finden Sie im Handbuch `sendEvent`-Befehlsoptionen.

Die andere Möglichkeit, die Einwilligungsinformationen jeder Anforderung hinzuzufügen, ist der `onBeforeEventSend`-Rückruf. Weitere Informationen dazu finden Sie im Abschnitt [Globale Änderungen an Ereignissen](../../fundamentals/tracking-events.md#modifying-events-globally) in der Dokumentation zu Tracking-Ereignissen.

## Nächste Schritte

Nachdem Sie nun gelernt haben, wie Sie IAB TCF 2.0 mit der Platform Web SDK Extension einsetzen, können Sie sich auch für die Integration mit anderen Adoben wie Adobe Analytics oder Echtzeit-Kundendatenplattform entscheiden. Weitere Informationen finden Sie unter [Übersicht über IAB-Transparenz und -Zustimmung-Framework 2.0](./overview.md).
