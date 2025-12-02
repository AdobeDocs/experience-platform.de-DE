---
title: Verwalten von Anzeigeereignissen in der Web-SDK
description: Erläutert Anzeigeereignisse und deren Verwendung in der Web-SDK.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Verwalten von Anzeigeereignissen in der Web-SDK

Anzeigeereignisse werden von Web SDK verwendet, um Ihren Personalisierungs- oder Analytics-Service zu informieren, wenn ein bestimmter Personalisierungsinhalt auf einer Seite angezeigt wird. Das Senden von Anzeigeereignissen verbessert die Genauigkeit von Personalisierungsmetriken und bietet Ihnen einen genauen Überblick darüber, was die Benutzer auf Ihrer Seite sehen.

>[!NOTE]
>
>Anzeigeereignisse werden beim Aufrufen der `applyPropositions` nicht automatisch gesendet.

## Anzeigeereignisse automatisch senden

Das Senden von Anzeigeereignissen liefert automatisch genauere Analysemetriken, da das Ereignis unmittelbar nach dem Laden der Personalisierung gesendet wird. Diese Implementierung verfügt außerdem über eine optimierte Implementierungsmethode.

Um Anzeigeereignisse automatisch zu senden, nachdem der personalisierte Inhalt auf der Seite gerendert wurde, müssen Sie die folgenden Parameter konfigurieren:

* `renderDecisions: true`
* `personalization.sendDisplayEvent: true` oder nicht angegeben

Web SDK sendet die Anzeigeereignisse sofort, nachdem eine Personalisierung als Ergebnis eines `sendEvent`-Aufrufs gerendert wurde.

## Senden von Anzeigeereignissen in nachfolgenden sendEvent-Aufrufen

Anders als beim automatischen Senden von Anzeigeereignissen haben Sie bei der Einbeziehung in nachfolgende `sendEvent`-Aufrufe auch die Möglichkeit, weitere Informationen zum Laden der Seite in den Aufruf aufzunehmen. Hierbei kann es sich um zusätzliche Informationen handeln, die beim Anfordern der personalisierten Inhalte nicht verfügbar waren.

Darüber hinaus werden durch das Senden von Anzeigeereignissen in `sendEvent`-Aufrufen Bounce-Ratenfehler bei der Verwendung von Adobe Analytics minimiert.

>[!IMPORTANT]
>
>Bei Verwendung manuell gerenderter Vorschläge werden Anzeigeereignisse nur über `sendEvent` unterstützt. Anzeigeereignisse können in diesem Fall nicht automatisch gesendet werden.

### Senden von Anzeigeereignissen für automatisch gerenderte Vorschläge

Um Anzeigeereignisse für automatisch gerenderte Vorschläge zu senden, müssen Sie die folgenden Parameter im `sendEvent`-Aufruf konfigurieren:

* `renderDecisions: true`
* `personalization.sendDisplayEvent: false` für den Seitenanfang

Um die Anzeigeereignisse zu senden, rufen Sie `sendEvent` mit `personalization.includeRenderedPropositions: true` auf

### Senden von Anzeigeereignissen für manuell gerenderte Vorschläge

Um Anzeigeereignisse für manuell gerenderte Vorschläge zu senden, müssen Sie sie in das XDM-Feld `_experience.decisioning.propositions` einbeziehen, einschließlich der Felder `id`, `scope` und `scopeDetails` aus den Vorschlägen.

Legen Sie außerdem das Feld `include _experience.decisioning.propositionEventType.display` auf `1` fest.
