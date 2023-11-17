---
title: Verwalten von Anzeigeereignissen im Web SDK
description: In diesem Artikel wird beschrieben, was Anzeigeereignisse sind und wie sie im Web SDK funktionieren.
source-git-commit: 221a9348803e111a1842b3abf2e74f7408da5994
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Verwalten von Anzeigeereignissen im Web SDK

Anzeigeereignisse werden vom Web SDK verwendet, um Ihren Personalisierungs- oder Analytics-Dienst zu informieren, wenn ein bestimmter Personalisierungsinhalt auf einer Seite angezeigt wird.

Das Senden von Anzeigeereignissen verbessert die Genauigkeit von Personalisierungsmetriken und bietet Ihnen einen genauen Überblick darüber, was die Benutzer auf Ihrer Seite sehen.

Mit dem Web SDK können Sie Anzeigeereignisse auf zwei Arten senden:

* [Automatisch](#send-automatically), unmittelbar nachdem der personalisierte Inhalt auf der Seite wiedergegeben wurde. Weitere Informationen finden Sie in der Dokumentation [Rendern von personalisiertem Inhalt](rendering-personalization-content.md) für weitere Informationen.
* [Manuell](#send-sendEvent-calls)durch nachfolgende `sendEvent` -Aufrufe.

>[!NOTE]
>
>Anzeigeereignisse werden beim Aufruf der `applyPropositions` -Funktion.

## Automatische Übermittlung von Anzeigeereignissen {#send-automatically}

Das Senden von Anzeigeereignissen liefert automatisch genauere Analytics-Metriken, da das Ereignis unmittelbar nach dem Laden der Personalisierung gesendet wird. Diese Implementierung verfügt auch über eine rationellere Implementierungsmethode.

Um Anzeigeereignisse automatisch nach der Wiedergabe des personalisierten Inhalts auf der Seite zu senden, müssen Sie die folgenden Parameter konfigurieren:

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: true` oder nicht spezifiziert

Das Web SDK sendet die Anzeigeereignisse unmittelbar nach der Wiedergabe einer Personalisierung als Ergebnis einer `sendEvent` aufrufen.

## Senden von Anzeigeereignissen in nachfolgenden sendEvent-Aufrufen {#send-sendEvent-calls}

Im Vergleich zu [automatisch](#send-automatically) Senden von Anzeigeereignissen, wenn Sie sie in nachfolgende `sendEvent` -Aufrufe haben Sie auch die Möglichkeit, weitere Informationen über das Laden der Seite in den -Aufruf aufzunehmen. Hierbei kann es sich um zusätzliche Informationen handeln, die bei der Anforderung des personalisierten Inhalts nicht verfügbar waren.

Senden von Anzeigeereignissen in `sendEvent` -Aufrufe minimieren Fehler bei der Absprungrate bei der Verwendung von Adobe Analytics.

>[!IMPORTANT]
>
>Bei der Verwendung manuell gerenderter Vorschläge werden Anzeigeereignisse nur über `sendEvent` -Aufrufe. In diesem Fall können keine Anzeigeereignisse automatisch gesendet werden.

### Senden von Anzeigeereignissen für automatisch gerenderte Vorschläge {#auto-rendered-propositions}

Um Anzeigeereignisse für automatisch gerenderte Vorschläge zu senden, müssen Sie die folgenden Parameter im `sendEvent` Aufruf:

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: false` für den oberen Seitenaufruf

Um die Anzeigeereignisse zu senden, rufen Sie `sendEvent` mit `personalization.includePendingDisplayNotifications: true`

### Senden von Anzeigeereignissen für manuell gerenderte Vorschläge {#manually-rendered-propositions}

Um Anzeigeereignisse für manuell gerenderte Vorschläge zu senden, müssen Sie sie in die `_experience.decisioning.propositions` XDM-Feld, einschließlich `id`, `scope`, und `scopeDetails` aus den Vorschlägen.

Legen Sie außerdem die `include _experience.decisioning.propositionEventType.display` -Feld zu `1`.