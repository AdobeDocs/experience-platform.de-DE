---
title: Integrieren der IAB TCF 2.0-Unterstützung mithilfe des Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie die IAB TCF 2.0-Unterstützung für Ihre Website einrichten, ohne Tags zu verwenden.
seo-description: Erfahren Sie, wie Sie die IAB TCF 2.0-Zustimmung mit dem Adobe Experience Platform Web SDK einrichten.
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 0%

---

# Integrieren der IAB TCF 2.0-Unterstützung in das Platform Web SDK

In diesem Handbuch wird gezeigt, wie das Interactive Advertising Bureau Transparency &amp; Consent Framework, Version 2.0 (IAB TCF 2.0), ohne Tags mit dem Adobe Experience Platform Web SDK integriert werden kann. Eine Übersicht über die Integration mit IAB TCF 2.0 finden Sie in [overview](./overview.md). Eine Anleitung zur Integration mit Tags finden Sie im [IAB TCF 2.0-Handbuch für Tags](./with-launch.md).

## Erste Schritte

In diesem Handbuch wird die `__tcfapi`-Schnittstelle für den Zugriff auf die Zustimmungsinformationen verwendet. Die direkte Integration mit Ihrem Cloud Management-Provider (CMP) kann für Sie einfacher sein. Die Informationen in diesem Handbuch können jedoch weiterhin nützlich sein, da die CMPs im Allgemeinen ähnliche Funktionen wie die TCF-API bieten.

>[!NOTE]
>
>In diesen Beispielen wird davon ausgegangen, dass `window.__tcfapi` zum Zeitpunkt der Ausführung des Codes auf der Seite definiert ist. CMPs können einen Hook bereitstellen, mit dem Sie diese Funktionen ausführen können, wenn das `__tcfapi` -Objekt bereit ist.

Um das IAB TCF 2.0 mit Tags und die Adobe Experience Platform Web SDK-Erweiterung zu verwenden, benötigen Sie ein XDM-Schema. Wenn Sie keines dieser beiden Optionen eingerichtet haben, sehen Sie sich diese Seite an, bevor Sie fortfahren.

Darüber hinaus setzt dieses Handbuch ein Verständnis des Adobe Experience Platform Web SDK voraus. Einen schnellen Auffrischungskurs finden Sie in der [Adobe Experience Platform Web SDK - Übersicht](../../home.md) und der [Dokumentation zu häufig gestellten Fragen](../../web-sdk-faq.md) .

## Standardzustimmung aktivieren

Wenn Sie alle unbekannten Benutzer gleich behandeln möchten, können Sie die Standardzustimmung auf `pending` oder `out` setzen. Dadurch werden Erlebnisereignisse in die Warteschlange gestellt oder verworfen, bis Zustimmungseinstellungen empfangen wurden.

Weitere Informationen zur Standardzustimmung finden Sie im Abschnitt [Standardzustimmung](../../fundamentals/configuring-the-sdk.md#default-consent) in der Konfigurationsdokumentation für das Platform Web SDK.

### Festlegen der Standardzustimmung basierend auf `gdprApplies`

Einige CMPs bieten die Möglichkeit festzustellen, ob die Datenschutz-Grundverordnung (DSGVO) für den Kunden gilt. Wenn Sie die Zustimmung für Kunden annehmen möchten, für die die DSGVO nicht gilt, können Sie die Markierung `gdprApplies` im TCF-API-Aufruf verwenden.

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

In diesem Beispiel wird der Befehl `configure` aufgerufen, nachdem `tcData` von der TCF-API abgerufen wurde. Wenn `gdprApplies` &quot;true&quot;ist, wird die Standardzustimmung auf `pending` gesetzt. Wenn `gdprApplies` false ist, wird die Standardzustimmung auf `in` gesetzt. Stellen Sie sicher, dass Sie die Variable `alloyConfiguration` mit Ihrer Konfiguration ausfüllen.

>[!NOTE]
>
>Wenn die Standardzustimmung auf `in` festgelegt ist, kann der Befehl `setConsent` weiterhin verwendet werden, um die Zustimmungseinstellungen Ihrer Kunden aufzuzeichnen.

## Verwenden des Ereignisses setConsent

Die IAB TCF 2.0-API stellt ein Ereignis für den Zeitpunkt bereit, zu dem die Zustimmung vom Kunden aktualisiert wird. Dies geschieht, wenn der Kunde seine Voreinstellungen anfänglich festlegt und wenn der Kunde seine Voreinstellungen aktualisiert.

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

Dieser Codeblock überwacht das `useractioncomplete` -Ereignis und legt dann die Zustimmung fest, wobei die Zustimmungszeichenfolge und die `gdprApplies` -Markierung übergeben werden. Wenn Sie benutzerdefinierte Identitäten für Ihre Kunden haben, stellen Sie sicher, dass Sie die Variable `identityMap` ausfüllen. Weitere Informationen zum Aufrufen von `setConsent` finden Sie im Handbuch [Unterstützende Zustimmung](../../consent/supporting-consent.md) .

## Einschließen von Einwilligungsinformationen in sendEvent

In XDM-Schemas können Sie Informationen zu Zustimmungsvoreinstellungen aus Experience Events speichern. Es gibt zwei Möglichkeiten, diese Informationen zu jedem Ereignis hinzuzufügen.

Zunächst können Sie bei jedem `sendEvent`-Aufruf das relevante XDM-Schema angeben. Das folgende Beispiel zeigt eine Möglichkeit, dies zu tun:

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

Dieses Beispiel ruft die Zustimmungsinformationen für die TCF-API ab und sendet dann ein Ereignis mit den Zustimmungsinformationen, die zum XDM-Schema hinzugefügt wurden. Informationen zu den Befehlsoptionen `sendEvent` finden Sie im Handbuch [Tracking-Ereignisse](../../fundamentals/tracking-events.md) .

Die andere Möglichkeit, die Zustimmungsinformationen zu jeder Anfrage hinzuzufügen, ist der Rückruf `onBeforeEventSend` . Weiterführende Informationen dazu finden Sie im Abschnitt [Globale Änderungen von Ereignissen](../../fundamentals/tracking-events.md#modifying-events-globally) in der Dokumentation zu Tracking-Ereignissen .

## Nächste Schritte

Nachdem Sie nun gelernt haben, wie Sie IAB TCF 2.0 mit der Platform Web SDK-Erweiterung verwenden, können Sie auch mit anderen Adobe-Lösungen wie Adobe Analytics oder Echtzeit-Kundendatenplattform integrieren. Weitere Informationen finden Sie unter [Übersicht über das IAB Transparency &amp; Consent Framework 2.0](./overview.md) .
