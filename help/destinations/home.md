---
keywords: Ziele; Adobe Experience Platform; Plattform; Ziele - Übersicht; aktivieren von Daten; Aktivieren;
title: Ziele – Übersicht
description: Ziele sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Sie können Ziele in der Adobe Experience Platform verwenden, um Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle zu aktivieren.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 44%

---

# [!DNL Destinations] – Übersicht {#overview}

![Übersichtsbanner Ziele](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

## Ziele und Quellen {#destinations-and-sources}

Eine der Kernfunktionen von Platform besteht darin, Ihre Erstanbieterdaten zu erfassen und sie für Ihre geschäftlichen Anforderungen zu aktivieren. Verwendung [sources](../sources/home.md) , um Daten in Platform und Ziele zu erfassen und sie aus Platform zu exportieren.

## Ziele – Schritte {#steps}

* Wählen Sie aus einer [Self-Service-Katalog](./catalog/overview.md) aller in Platform verfügbaren Ziele.
* Verwenden Sie Ziele, um Profile oder Segmente an Plattformen zur Marketing-Automatisierung, digitale Werbeplattformen und mehr zu senden.
* Planen Sie Datenexporte an Ihre bevorzugten Ziele zu regelmäßigen Zeiten.

## Steuerelemente {#controls}

Mit den Steuerelementen im [Arbeitsbereich „Ziele“](./ui/destinations-workspace.md) können Sie folgende Aufgaben erledigen:

* Katalog der Zielplattformen durchsuchen, wo Sie Ihre Daten aktivieren können;
* Datenflüsse zu den Zielen im Katalog erstellen, bearbeiten, aktivieren und deaktivieren;
* Erstellen Sie ein Konto an einem Speicherort oder verknüpfen Sie Platform mit dem Konto in der Zielplattform.
* auswählen, welche Segmente für Ziele aktiviert werden sollen;
* auswählen, welche [Experience Data Model (XDM)-Felder](../xdm/home.md) exportiert werden sollen, wenn Segmente für E-Mail-Marketing-Ziele aktiviert werden.

## Zieltypen und Kategorien {#types-and-categories}

Detaillierte Informationen finden Sie im Abschnitt [Zieltypen und Kategorien - Übersicht](./destination-types.md).

## Ziele und Zugriffskontrollen {#access-controls}

Die Zielfunktion in Platform funktioniert mit Zugriffssteuerungsberechtigungen von Adobe Experience Platform. Je nach Berechtigungsstufe Ihres Anwenders können Sie Ziele anzeigen, verwalten und aktivieren. Informationen zu den individuellen Berechtigungen finden Sie unter [Zugangssteuerung in Adobe Experience Platform](../access-control/home.md); scrollen Sie nach unten bis zum Ende der Seite.

Weiterführende Informationen zu Zugangssteuerungen finden Sie im [Benutzerhandbuch zur Zugangssteuerung](../access-control/ui/overview.md).

## Einschränkungen von Data Governance beim Aktivieren von Daten für Ziele {#data-governance}

Data Governance wird für Platform-Ziele durchgesetzt durch:

* *Marketing-Aktionen* die Sie im Workflow Ziele erstellen auswählen können;
* *Datennutzungsrichtlinien* die die Aktivierung von Daten, die bestimmte Nutzungsbezeichnungen enthalten, auf Ziele mit bestimmten Marketing-Aktionen beschränkt.

Weitere Informationen finden Sie in der Dokumentation zu Data Governance in Platform . [Marketing-Aktionen](../data-governance/policies/overview.md) und [Beheben von Verstößen gegen Datenrichtlinien](../data-governance/enforcement/auto-enforcement.md).

Weitere Informationen zur Auswahl von Marketing-Aktionen im Workflow &quot;Ziel erstellen&quot;finden Sie auf den folgenden Seiten für die verschiedenen Zieltypen in Platform:

* [Werbeziele - Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [Werbeziele - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Werbeziele - Google Display &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [Cloud-Speicher-Ziele](./catalog/cloud-storage/overview.md)
* [E-Mail-Marketing-Ziele ](./catalog/email-marketing/overview.md)
* [Social-Media-Ziele ](./catalog/social/overview.md)

Weitere Informationen zu Verstößen gegen Datenrichtlinien im Workflow für die Segmentaktivierung finden Sie im Schritt Überprüfen in den folgenden Handbüchern:

* [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](./ui/activate-segment-streaming-destinations.md#review)
* [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Profilen](./ui/activate-streaming-profile-destinations.md#review)
* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](./ui/activate-batch-profile-destinations.md#review)
