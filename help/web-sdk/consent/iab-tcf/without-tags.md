---
title: Integrieren der IAB TCF 2.0-Unterstützung mithilfe der Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie IAB TCF 2.0-Unterstützung für Ihre Website einrichten, ohne Tags zu verwenden.
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# Integrieren der IAB TCF 2.0-Unterstützung mit Platform Web SDK

In diesem Handbuch wird gezeigt, wie Sie das Interactive Advertising Bureau Transparency &amp; Consent Framework, Version 2.0 (IAB TCF 2.0), ohne Verwendung von Tags in Adobe Experience Platform Web SDK integrieren. Eine Übersicht über die Integration mit IAB TCF 2.0 finden Sie in [Übersicht](./overview.md). Eine Anleitung zur Integration mit Tags finden Sie im [IAB TCF 2.0-Handbuch für Tags](./with-tags.md).

## Erste Schritte

Dieses Handbuch verwendet die `__tcfapi`-Schnittstelle für den Zugriff auf die Einverständnisinformationen. Es könnte einfacher für Sie sein, direkt mit Ihrem Cloud Management Provider (CMP) zu integrieren. Die Informationen in diesem Handbuch können jedoch weiterhin nützlich sein, da die CMPs im Allgemeinen ähnliche Funktionen wie die TCF-API bieten.

>[!NOTE]
>
>Bei diesen Beispielen wird davon ausgegangen, dass zum Zeitpunkt der Ausführung des Codes `window.__tcfapi` auf der Seite definiert ist. CMPs können einen Hook bereitstellen, in dem Sie diese Funktionen ausführen können, wenn das `__tcfapi`-Objekt bereit ist.

Um IAB TCF 2.0 mit Tags und der Adobe Experience Platform Web SDK-Erweiterung verwenden zu können, benötigen Sie ein verfügbares XDM-Schema. Wenn Sie keines dieser Elemente eingerichtet haben, rufen Sie zunächst diese Seite auf, bevor Sie fortfahren.

Darüber hinaus setzt dieses Handbuch ein Grundverständnis für Adobe Experience Platform Web SDK voraus. Zur schnellen Auffrischung lesen Sie bitte die [Übersicht über Adobe Experience Platform Web SDK](../../home.md) und die Dokumentation [Häufig gestellte Fragen](../../faq.md) .

## Aktivieren des Standardeinverständnisses

Wenn Sie alle unbekannten Benutzer gleich behandeln möchten, können Sie [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) auf `pending` oder `out` setzen. Diese stellt Erlebnisereignisse in die Warteschlange oder verwirft sie, bis die Einverständnisvoreinstellungen empfangen werden.

### Festlegen des Standardeinverständnisses basierend auf `gdprApplies`

Einige CMPs bieten die Möglichkeit festzustellen, ob die Datenschutz-Grundverordnung (DSGVO) auf den Kunden anwendbar ist. Wenn Sie von einem Einverständnis für Kunden ausgehen möchten, für die die DSGVO nicht gilt, können Sie das `gdprApplies`-Flag im TCF-API-Aufruf verwenden.

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

In diesem Beispiel wird der Befehl `configure` aufgerufen, nachdem die `tcData` von der TCF-API abgerufen wurde. Wenn `gdprApplies` „true“ ist, wird das Standardeinverständnis auf `pending` festgelegt. Wenn `gdprApplies` den Wert „false“ hat, wird das Standardeinverständnis auf &quot;`in`&quot; festgelegt. Stellen Sie sicher, dass Sie die Variable `alloyConfiguration` mit Ihrer Konfiguration ausfüllen.

>[!NOTE]
>
>Wenn das Standardeinverständnis auf `in` festgelegt ist, kann der Befehl `setConsent` weiterhin verwendet werden, um die Einverständnisvoreinstellungen Ihrer Kunden aufzuzeichnen.

## Verwenden des setConsent-Ereignisses

Die IAB TCF 2.0-API stellt ein Ereignis bereit, für das das Einverständnis vom Kunden aktualisiert wird. Dies tritt auf, wenn der Kunde anfänglich seine Voreinstellungen festlegt und wenn der Kunde seine Voreinstellungen aktualisiert.

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

Dieser Code-Block überwacht das `useractioncomplete`-Ereignis und legt dann das Einverständnis fest, wobei die Einverständniszeichenfolge und das `gdprApplies`-Flag übergeben werden. Wenn Sie benutzerdefinierte Identitäten für Ihre Kunden haben, stellen Sie sicher, dass Sie die `identityMap` Variable ausfüllen. Weitere Informationen finden Sie im Handbuch [setConsent](../../../web-sdk/commands/setconsent.md).

## Einverständnisinformationen in sendEvent einschließen

Innerhalb von XDM-Schemata können Sie Informationen zu Einverständnisvoreinstellungen aus Erlebnisereignissen speichern. Es gibt zwei Möglichkeiten, diese Informationen zu jedem Ereignis hinzuzufügen.

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

Dieses Beispiel ruft die Einverständnisinformationen für die TCF-API ab und sendet dann ein Ereignis mit den Einverständnisinformationen, die dem XDM-Schema hinzugefügt wurden.

Die andere Möglichkeit, die Einverständnisinformationen zu jeder Anfrage hinzuzufügen, besteht in dem [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) Callback.

## Nächste Schritte

Nachdem Sie nun gelernt haben, wie Sie IAB TCF 2.0 mit der Platform Web SDK-Erweiterung verwenden, können Sie sich auch für die Integration mit anderen Adobe-Lösungen wie Adobe Analytics oder Adobe Real-time Customer Data Platform entscheiden. Weitere Informationen finden [ in der Übersicht zum IAB Transparency &amp; Consent Framework ](./overview.md).0 .
