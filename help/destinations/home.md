---
keywords: Ziele;adobe-Erlebnisplattform;Plattform;Ziele-Übersicht;Daten aktivieren;Aktivieren;
title: Ziele – Übersicht
seo-title: Ziele – Übersicht
description: Erfahren Sie, wie Sie Adobe Experience Platform-Daten für Cross-Kanal-Marketing-Kampagnen, E-Mails, gezielte Werbung und mehr aktivieren können.
seo-description: Ziele sind vordefinierte Integrationen mit Zielplattformen, die die nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Sie können Destinations in Adobe Experience Platform verwenden, um bekannte und unbekannte Daten für Cross-Kanal-Marketing-Kampagnen, E-Mail-Kampagnen, gezielte Werbung und viele andere Anwendungsfälle zu aktivieren.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
translation-type: tm+mt
source-git-commit: 805cb72e91e6446f74cc3461d39841740eb576c7
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 27%

---

# [!DNL Destinations] Übersicht {#overview}

![Übersichtsbanner Ziele](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** sind vordefinierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Sie können Ziele verwenden, um bekannte und unbekannte Daten für Cross-Kanal-Marketing-Kampagnen, E-Mail-Kampagnen, gezielte Werbung und viele andere Anwendungsfälle zu aktivieren.

## Ziele und Quellen {#destinations-and-sources}

Eine der Kernfunktionen von Platform besteht darin, Ihre Erstanbieter-Daten zu integrieren und sie für Ihre geschäftlichen Anforderungen zu aktivieren. Verwenden Sie [sources](../sources/home.md), um Daten in Plattform und Ziele zu erfassen und Daten von der Plattform zu exportieren.

## Ziele – Schritte {#steps}

* Wählen Sie aus einem [Selbstbedienungskatalog](./catalog/overview.md) aller in der Plattform verfügbaren Ziele.
* Verwenden Sie Ziele, um [zu aktivieren](./ui/activate-destinations.md) und senden Sie Profil oder Segmente an Marketingautomationsplattformen, digitale Werbungsplattformen und mehr.
* Planen Sie Datenexporte an Ihre bevorzugten Ziele zu regelmäßigen Zeiten.

## Steuerelemente {#controls}

Mit den Steuerelementen im [Arbeitsbereich „Ziele“](./ui/destinations-workspace.md) können Sie folgende Aufgaben erledigen:

* Katalog der Zielplattformen durchsuchen, wo Sie Ihre Daten aktivieren können;
* Datenflüsse zu den Zielen im Katalog erstellen, bearbeiten, aktivieren und deaktivieren;
* Erstellen Sie ein Konto an einem Speicherort der Datenspeicherung oder verknüpfen Sie Plattform mit dem Konto in der Zielplattform.
* auswählen, welche Segmente für Ziele aktiviert werden sollen;
* auswählen, welche [Experience Data Model (XDM)-Felder](../xdm/home.md) exportiert werden sollen, wenn Segmente für E-Mail-Marketing-Ziele aktiviert werden.

## Zieltypen und Kategorien {#types-and-categories}

Detaillierte Informationen finden Sie unter [Übersicht über Zieltypen und Kategorien](./destination-types.md).

## Ziele und Zugriffskontrollen {#access-controls}

Die Funktion &quot;Ziele&quot;in &quot;Plattform&quot;funktioniert mit Adobe Experience Platform-Zugriffskontrolle-Berechtigungen. Je nach Berechtigungsstufe Ihres Anwenders können Sie Ziele anzeigen, verwalten und aktivieren. Informationen zu den individuellen Berechtigungen finden Sie unter [Zugangssteuerung in Adobe Experience Platform](../access-control/home.md); scrollen Sie nach unten bis zum Ende der Seite.

Weiterführende Informationen zu Zugangssteuerungen finden Sie im [Benutzerhandbuch zur Zugangssteuerung](../access-control/ui/overview.md).

## [!DNL Data Governance] Einschränkungen bei der Datenaktivierung zu Zielen  {#data-governance}

Datenverwaltung wird für Plattformziele durch folgende Maßnahmen erzwungen:

* *Marketingaktionen,* die Sie im Arbeitsablauf zum Erstellen von Zielen auswählen können;
* *Datenverwendungsrichtlinien,* die die Aktivierung von Daten mit bestimmten Gebrauchsbeschriftungen auf Ziele mit bestimmten Marketingaktionen beschränken.

Weitere Informationen zu [Marketingaktionen](../data-governance/policies/overview.md) und [Auflösen von Verstößen gegen die Datenrichtlinie](../data-governance/enforcement/auto-enforcement.md) finden Sie in der Plattformdokumentation unter [!DNL Data Governance].

Weitere Informationen zur Auswahl von Marketingaktionen im Arbeitsablauf zum Erstellen von Zielen finden Sie auf den folgenden Seiten für die verschiedenen Zieltypen in Plattform:

* [Werbeziele - Google Ad Manager  ](./catalog/advertising/google-ad-manager.md)
* [Werbeziele - Google-Anzeigen](./catalog/advertising/google-ads-destination.md)
* [Werbeziele - Google Display &amp; Video 360  ](./catalog/advertising/google-dv360.md)
* [ Cloud-Speicher-Ziele](./catalog/cloud-storage/workflow.md)
* [E-Mail-Marketing-Ziele](./catalog/email-marketing/overview.md)
* [Social-Ziele](./catalog/social/workflow.md)

Weitere Informationen zu Verstößen gegen die Datenrichtlinie im Arbeitsablauf zur Segmentüberprüfung finden Sie im Schritt Überprüfen unter [Profil und Aktivierungen für ein Ziel](./ui/activate-destinations.md#review) aktivieren.
