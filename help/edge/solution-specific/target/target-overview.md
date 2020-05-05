---
title: 'Adobe Zielgruppe und das Adobe Experience Platform Web SDK. '
seo-title: Adobe Experience Platform Web SDK und Verwendung von Adobe Zielgruppe
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK mit Adobe Zielgruppe rendern
seo-description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK mit Adobe Zielgruppe rendern
translation-type: tm+mt
source-git-commit: db4bfec04a1116ce2b6a0be7ca0e8cb2f9639ad6

---


# Übersicht über Zielgruppen

Das Adobe Experience Platform Web SDK ist über diese [Personalisierungsfunktion](../../fundamentals/rendering-personalization-content.md) in die Adobe-Zielgruppe integriert und ermöglicht es Ihnen, personalisierte Inhalte und Entscheidungen einfach bereitzustellen.

## Aktivieren von Adobe Zielgruppe

Um die Zielgruppe zu aktivieren, müssen Sie folgende Schritte ausführen:

- Aktivieren Sie die Zielgruppe in Ihrer [Edge-Konfiguration](../../fundamentals/edge-configuration.md) mit dem entsprechenden Clientcode.
- Hinzufügen Sie die `renderDecisions` Option auf Ihre Ereignis.

Optional können Sie auch:

- Hinzufügen Sie `scopes` Ihre Ereignisse an, um bestimmte Aktivitäten abzurufen (nützlich für Aktivitäten, die mit dem formularbasierten Composer erstellt wurden).
- Hinzufügen Sie das [Ausblendungsfragment](../../fundamentals/managing-flicker.md) , um nur bestimmte Teile der Seite auszublenden.

## VEC verwenden

Mit dem SDK können Sie den VEC normal mit einer Ausnahme verwenden, benötigen Sie die [Zielgruppe VEC Helper Extension](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) installiert und aktiv.

## Verwenden des formularbasierten Composers

Der formularbasierte Composer kann auch verwendet werden, um Inhalte zurückzugeben. Die Bereiche werden als Positionen (mBoxes) in der Benutzeroberfläche der Zielgruppe angezeigt. Außerdem sollten Sie sicherstellen, dass Ihr Entwickler nach Antworten sucht, wenn er Scopes verwendet.

## Audiencen in XDM

In Zielgruppe werden XDM-Daten im Audience Builder als benutzerdefinierter Parameter angezeigt. Der XDM wird mit Punktnotation serialisiert (z. `web.webPageDetails.name`)

## Terminologie

__Entscheidungen__ - In Zielgruppe korrelieren diese mit dem Erlebnis, das aus einer Aktivität ausgewählt wurde.

__Anwendungsbereich__ - Der Anwendungsbereich des Beschlusses. In Zielgruppe ist dies die mBox. Die globale mBox ist der `__view__` Anwendungsbereich.

__Schema__ - Das Schema eines Beschlusses ist die Art des Angebots in der Zielgruppe.

__XDM__ - Der XDM wird in Punktnotation serialisiert und dann als mBox-Parameter in Zielgruppe gesetzt.