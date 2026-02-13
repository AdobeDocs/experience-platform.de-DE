---
title: Übersicht über Personalization-Anwendungsfälle
description: Erfahren Sie, wie Sie mit der Adobe Experience Platform Web SDK Anwendungsfälle für die Personalisierung implementieren, einschließlich Rendering-Mustern für Inhalte und Tracking-Anzeige.
keywords: Personalisierung;sendEvent;renderDecisions;applyPropositions;decisionScopes;Ereignisse anzeigen;Flackern;
exl-id: 6beccbfd-fddb-4e19-8a56-caba276e1643
source-git-commit: caaf5cad7276d6429fbbf35585fd4845de6ff60c
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 1%

---

# Übersicht über Personalization-Anwendungsfälle

Adobe Experience Platform Web SDK ermöglicht eine Vielzahl von Anwendungsfällen für die Personalisierung von Web-Eigenschaften. Es unterstützt flexible Architekturen (Client-seitig, Server-seitig und Hybrid), sodass Sie Entscheidungen anfordern und Inhalte auf eine Weise rendern können, die den Anforderungen Ihrer Site entspricht.

## Rendern von personalisierten Inhalten

Der Web-SDK kann Personalisierungsentscheidungen (auch &quot;_&quot; genannt_ abrufen und Ihnen beim Rendern auf der Seite helfen. Das Rendern erfolgt asynchron, sodass kein bestimmter Zeitpunkt für die Anwendung von Inhalten angenommen werden sollte.

Wählen Sie das Muster aus, das den Vorschlagselementen entspricht, die Sie erhalten:

1. **DOM-Aktionsvorschläge automatisch rendern**: Verwenden Sie diese Option, wenn Vorschläge `dom-action` Elemente mit Selektoren und Aktionstypen enthalten, die Web SDK automatisch anwenden kann. Siehe [DOM-Aktionsvorschläge automatisch rendern](render-auto-pers-content.md).
1. **HTML-Angebote ohne Selektoren mit applyPropositions rendern**: Verwenden Sie diese Option, wenn Sie HTML-Inhalte erhalten. Sie müssen jedoch angeben, wo und wie Sie sie über Metadaten anwenden möchten (Selektor + Aktionstyp). Siehe [Rendern von HTML-Angeboten ohne Selektoren](render-html-offers.md).
1. **Vorschläge manuell rendern**: Verwenden Sie diese Option, wenn Sie die volle Kontrolle über die Rendering-Logik benötigen (z. B. beim Erstellen einer Benutzeroberfläche aus JSON oder beim Anwenden benutzerdefinierter Geschäftsregeln). Siehe [Vorschläge manuell rendern](render-manual-propositions.md).

>[!TIP]
>
>Diese Muster können kombiniert werden. Sie können beispielsweise das automatische Rendering von DOM-Aktionen aktivieren und gleichzeitig Inhalte aus bestimmten Entscheidungsumfängen manuell rendern.

## Häufige Begleitthemen

Die meisten Personalisierungsimplementierungen umfassen die folgenden gängigen Themen:

* **Flackern verhindern** (optional): Container während der Personalisierung aus- und einblenden. Siehe [Verwalten von Flackern](manage-flicker.md).
* **Verfolgen Sie, was angezeigt wurde**: Zeichnen Sie Anzeigeereignisse für gerenderte Inhalte auf. Siehe [Verwalten von Anzeigeereignissen](display-events.md).
* **Seitenanfang/Seitenende-Metriken**: Entscheidungen frühzeitig anfordern, Messung später einbeziehen. Siehe [Konfigurieren der Ereignisse auf der Seite oben und ](top-bottom-page-events.md).

## Beispiele für Web SDK

Zusätzlich zu den Dokumentseiten in diesem Ordner verwaltet Adobe ein Repository mit Beispielanwendungen, auf die Sie verweisen können. Unter [Beispiele für Web-SDK](https://github.com/adobe/alloy-samples/) auf GitHub finden Sie weitere Personalisierungsszenarien, darunter:

* Client-seitige Personalisierung
* Server-seitige Personalisierung
* Hybride Personalisierung
* Personalization in Single-Page Applications
