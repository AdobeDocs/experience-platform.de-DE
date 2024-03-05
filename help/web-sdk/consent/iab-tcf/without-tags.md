---
title: Integrieren der IAB TCF 2.0-Unterstützung mithilfe des Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie die IAB TCF 2.0-Unterstützung für Ihre Website einrichten, ohne Tags zu verwenden.
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# Integrieren der IAB TCF 2.0-Unterstützung in das Platform Web SDK

In diesem Handbuch wird gezeigt, wie das Interactive Advertising Bureau Transparency &amp; Consent Framework, Version 2.0 (IAB TCF 2.0), ohne Tags mit dem Adobe Experience Platform Web SDK integriert werden kann. Eine Übersicht über die Integration mit IAB TCF 2.0 finden Sie im Abschnitt [Übersicht](./overview.md). Eine Anleitung zur Integration mit Tags finden Sie im Abschnitt [IAB TCF 2.0-Handbuch für Tags](./with-tags.md).

## Erste Schritte

In diesem Handbuch werden die `__tcfapi` -Schnittstelle für den Zugriff auf die Zustimmungsinformationen. Die direkte Integration mit Ihrem Cloud Management-Provider (CMP) kann für Sie einfacher sein. Die Informationen in diesem Handbuch können jedoch weiterhin nützlich sein, da die CMPs im Allgemeinen ähnliche Funktionen wie die TCF-API bieten.

>[!NOTE]
>
>Bei diesen Beispielen wird davon ausgegangen, dass zum Zeitpunkt der Ausführung des Codes `window.__tcfapi` wird auf der Seite definiert. CMPs können einen Hook bereitstellen, mit dem Sie diese Funktionen ausführen können, wenn die `__tcfapi` -Objekt bereit ist.

Um das IAB TCF 2.0 mit Tags und die Adobe Experience Platform Web SDK-Erweiterung zu verwenden, benötigen Sie ein XDM-Schema. Wenn Sie keines dieser beiden Optionen eingerichtet haben, sehen Sie sich diese Seite an, bevor Sie fortfahren.

Darüber hinaus setzt dieses Handbuch ein Verständnis des Adobe Experience Platform Web SDK voraus. Für einen schnellen Auffrischungskurs lesen Sie bitte die [Übersicht über das Adobe Experience Platform Web SDK](../../home.md) und [Häufig gestellte Fragen](../../faq.md) Dokumentation.

## Standardzustimmung aktivieren

Wenn Sie alle unbekannten Benutzer gleich behandeln möchten, können Sie [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) nach `pending` oder `out`. Dadurch werden Erlebnisereignisse in die Warteschlange gestellt oder verworfen, bis Zustimmungseinstellungen empfangen wurden.

### Festlegen der Standardzustimmung basierend auf `gdprApplies`

Einige CMPs bieten die Möglichkeit festzustellen, ob die Datenschutz-Grundverordnung (DSGVO) für den Kunden gilt. Wenn Sie die Zustimmung für Kunden übernehmen möchten, für die die DSGVO nicht gilt, können Sie die `gdprApplies` -Markierung im TCF-API-Aufruf.

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

In diesem Beispiel wird die `configure` aufgerufen wird, nachdem die `tcData` wird von der TCF-API abgerufen. Wenn `gdprApplies` auf &quot;true&quot;gesetzt ist, wird die Standardzustimmung auf `pending`. Wenn `gdprApplies` ist &quot;false&quot;, ist die standardmäßige Zustimmung auf `in`. Vergewissern Sie sich, dass Sie die `alloyConfiguration` mit Ihrer Konfiguration.

>[!NOTE]
>
>Wenn die standardmäßige Zustimmung auf `in`, die `setConsent` kann weiterhin verwendet werden, um die Zustimmungsvoreinstellungen Ihrer Kunden aufzuzeichnen.

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

Dieser Codeblock überwacht die `useractioncomplete` -Ereignis und legt dann die Zustimmung fest, wobei die Zustimmungszeichenfolge und die `gdprApplies` Markierung. Wenn Sie benutzerdefinierte Identitäten für Ihre Kunden haben, füllen Sie `identityMap` -Variable. Weitere Informationen finden Sie im Handbuch unter [Zustimmung](../../consent/supporting-consent.md) für weitere Informationen zum Aufruf von `setConsent`.

## Einschließen von Einwilligungsinformationen in sendEvent

In XDM-Schemas können Sie Informationen zu Zustimmungsvoreinstellungen aus Experience Events speichern. Es gibt zwei Möglichkeiten, diese Informationen zu jedem Ereignis hinzuzufügen.

Zuerst können Sie das relevante XDM-Schema für jede `sendEvent` aufrufen. Das folgende Beispiel zeigt eine Möglichkeit, dies zu tun:

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

Dieses Beispiel ruft die Zustimmungsinformationen für die TCF-API ab und sendet dann ein Ereignis mit den Zustimmungsinformationen, die zum XDM-Schema hinzugefügt wurden.

Die andere Möglichkeit, die Zustimmungsinformationen zu jeder Anfrage hinzuzufügen, ist mit der [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) Callback.

## Nächste Schritte

Nachdem Sie jetzt gelernt haben, wie Sie IAB TCF 2.0 mit der Platform Web SDK-Erweiterung verwenden, können Sie auch mit anderen Adobe-Lösungen wie Adobe Analytics oder Adobe Real-time Customer Data Platform integrieren. Siehe [Übersicht über das IAB Transparency &amp; Consent Framework 2.0](./overview.md) für weitere Informationen.
