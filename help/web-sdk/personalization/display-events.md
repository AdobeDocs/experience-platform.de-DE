---
title: Verwalten von Anzeigeereignissen im Web SDK
description: In diesem Artikel wird erläutert, was Anzeigeereignisse sind und wie Sie sie im Web SDK verwenden können.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: 4c7313afdce6645ab638b2998573e5a4f7c5de8f
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Verwalten von Anzeigeereignissen im Web SDK

Anzeigeereignisse werden vom Web SDK verwendet, um Ihren Personalisierungs- oder Analytics-Dienst zu informieren, wenn ein bestimmter Personalisierungsinhalt auf einer Seite angezeigt wird.

Das Senden von Anzeigeereignissen verbessert die Genauigkeit von Personalisierungsmetriken und bietet Ihnen einen genauen Überblick darüber, was die Benutzer auf Ihrer Seite sehen.

Mit dem Web SDK können Sie Anzeigeereignisse auf zwei Arten senden:

* [Automatisch](#send-automatically), unmittelbar nachdem der personalisierte Inhalt auf der Seite wiedergegeben wurde. Weitere Informationen finden Sie in der Dokumentation zum Rendern personalisierter Inhalte durch [1}.](rendering-personalization-content.md)
* [Manuell](#send-sendEvent-calls) durch nachfolgende `sendEvent` -Aufrufe.

>[!NOTE]
>
>Anzeigeereignisse werden beim Aufruf der Funktion `applyPropositions` nicht automatisch gesendet.

## Automatische Übermittlung von Anzeigeereignissen {#send-automatically}

Das Senden von Anzeigeereignissen liefert automatisch genauere Analytics-Metriken, da das Ereignis unmittelbar nach dem Laden der Personalisierung gesendet wird. Diese Implementierung verfügt auch über eine rationellere Implementierungsmethode.

Um Anzeigeereignisse automatisch nach der Wiedergabe des personalisierten Inhalts auf der Seite zu senden, müssen Sie die folgenden Parameter konfigurieren:

* `renderDecisions: true`
* `personalization.sendDisplayEvent: true` oder nicht angegeben

Das Web SDK sendet die Anzeigeereignisse unmittelbar nach der Wiedergabe einer Personalisierung als Ergebnis eines `sendEvent` -Aufrufs.

## Senden von Anzeigeereignissen in nachfolgenden sendEvent-Aufrufen {#send-sendEvent-calls}

Im Vergleich zum Versand von [automatischen](#send-automatically) Anzeigeereignissen haben Sie beim Einbeziehen dieser Ereignisse in nachfolgende `sendEvent` -Aufrufe auch die Möglichkeit, weitere Informationen über das Laden der Seite in den Aufruf aufzunehmen. Hierbei kann es sich um zusätzliche Informationen handeln, die bei der Anforderung des personalisierten Inhalts nicht verfügbar waren.

Darüber hinaus werden durch das Senden von Anzeigeereignissen in `sendEvent` -Aufrufen Fehler bei der Absprungrate bei der Verwendung von Adobe Analytics minimiert.

>[!IMPORTANT]
>
>Bei der Verwendung manuell gerenderter Vorschläge werden Anzeigeereignisse nur über `sendEvent` -Aufrufe unterstützt. In diesem Fall können keine Anzeigeereignisse automatisch gesendet werden.

### Senden von Anzeigeereignissen für automatisch gerenderte Vorschläge {#auto-rendered-propositions}

Um Anzeigeereignisse für automatisch gerenderte Vorschläge zu senden, müssen Sie die folgenden Parameter im `sendEvent` -Aufruf konfigurieren:

* `renderDecisions: true`
* `personalization.sendDisplayEvent: false` für den oberen Seitenaufruf

Um die Anzeigeereignisse zu senden, rufen Sie `sendEvent` mit `personalization.includeRenderedPropositions: true` auf

### Senden von Anzeigeereignissen für manuell gerenderte Vorschläge {#manually-rendered-propositions}

Um Anzeigeereignisse für manuell gerenderte Vorschläge zu senden, müssen Sie diese in das XDM-Feld `_experience.decisioning.propositions` einschließen, einschließlich der Felder `id`, `scope` und `scopeDetails` aus den Vorschlägen.

Setzen Sie außerdem das Feld `include _experience.decisioning.propositionEventType.display` auf `1`.
