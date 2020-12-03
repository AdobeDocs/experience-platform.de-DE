---
keywords: RTCDP;CDP;Real-time Customer Data Platform;real time customer data platform;real time cdp;cdp;destinations;destination;rtcdp
title: Ziele – Übersicht
seo-title: Ziele – Übersicht
description: Stellen Sie Platform-Daten für kanalübergreifende Marketing-Kampagnen, E-Mails, zielgruppengerechte Werbung und vieles mehr bereit.
seo-description: Ziele sind vordefinierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus der Echtzeit-Kundendatenplattform ermöglichen. Sie können Ziele in der Echtzeit-Kundendatenplattform von nutzen, um Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle zu aktivieren.
translation-type: tm+mt
source-git-commit: 5f120a716cc3396ef7749463bb6052a8ced2fbb4
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 56%

---


# [!DNL Destinations] Übersicht {#overview}

![Übersichtsbanner Ziele](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** sind vordefinierte Integrationen mit Zielplattformen, die die nahtlose Aktivierung von Daten aus der Echtzeit-Kundendatenplattform ermöglichen. Sie können Ziele verwenden, um bekannte und unbekannte Daten für Cross-Kanal-Marketing-Kampagnen, E-Mail-Kampagnen, gezielte Werbung und viele andere Anwendungsfälle zu aktivieren.

## Ziele und Quellen {#destinations-and-sources}

Eine der Kernfunktionen der Echtzeit-Kundendatenplattform besteht darin, Ihre Daten von Erstparteien zu erfassen und für Ihre geschäftlichen Anforderungen zu aktivieren. Verwenden Sie Quellen, um Daten in Echtzeit-CDP und Ziele zu erfassen und Daten aus Echtzeit-CDP zu exportieren.

## Ziele – Schritte {#steps}

* Wählen Sie in einem [Self-Service-Katalog](./catalog/overview.md) unter allen in der Echtzeit-Kundendatenplattform verfügbaren Zielen.
* Verwenden Sie **[!UICONTROL Ziele]**, um Profile oder Segmente zu [aktivieren](./ui/activate-destinations.md) und an Plattformen für Marketing-Automatisierung, digitale Werbung und andere zu senden.
* Planen Sie Datenexporte an Ihre bevorzugten Ziele zu regelmäßigen Zeiten.

## Steuerelemente {#controls}

Mit den Steuerelementen im [Arbeitsbereich „Ziele“](./ui/destinations-workspace.md) können Sie folgende Aufgaben erledigen:

* Katalog der Zielplattformen durchsuchen, wo Sie Ihre Daten aktivieren können;
* Datenflüsse zu den Zielen im Katalog erstellen, bearbeiten, aktivieren und deaktivieren;
* ein Konto an einem Speicherort erstellen oder die Echtzeit-Kundendatenplattform mit dem Konto in der Zielplattform verknüpfen;
* auswählen, welche Segmente für Ziele aktiviert werden sollen;
* auswählen, welche [Experience Data Model (XDM)-Felder](../xdm/home.md) exportiert werden sollen, wenn Segmente für E-Mail-Marketing-Ziele aktiviert werden.

## Zieltypen und Kategorien {#types-and-categories}

Detaillierte Informationen finden Sie unter [Zieltypen und Kategorien - Übersicht](./destination-types.md).

## Ziele und Zugangssteuerungen {#access-controls}

Die Funktion &quot;Ziele&quot;in Echtzeit-CDP funktioniert mit Adobe Experience Platform-Zugriffskontrolle-Berechtigungen. Je nach Berechtigungsstufe Ihres Anwenders können Sie Ziele anzeigen, verwalten und aktivieren. Informationen zu den individuellen Berechtigungen finden Sie unter [Zugangssteuerung in Adobe Experience Platform](../access-control/home.md); scrollen Sie nach unten bis zum Ende der Seite.

Weiterführende Informationen zu Zugangssteuerungen finden Sie im [Benutzerhandbuch zur Zugangssteuerung](../access-control/ui/overview.md).

## [!DNL Data Governance] Einschränkungen bei der Datenaktivierung zu Zielen {#data-governance}

Die Datenverwaltung wird für CDP-Ziele in Echtzeit durchgesetzt durch:

* *Anwendungsfälle* für Marketing, die Sie im Arbeitsablauf zum Erstellen von Zielen auswählen können;
* *Datenverwendungsrichtlinien* , die die Aktivierung von Daten mit bestimmten Verwendungsbeschriftungen auf Ziele mit bestimmten Anwendungsfällen beschränken.

Weitere Informationen zu Anwendungsfällen [!DNL Data Governance] im [Marketing und zur](../rtcdp/privacy/data-governance-overview.md#destinations) Behebung von Verstößen [](../rtcdp/privacy/data-governance-overview.md#enforcement)gegen die Datenrichtlinie finden Sie in der CDP-Dokumentation in Echtzeit.

Weitere Informationen zur Auswahl von Anwendungsfällen für Marketingzwecke im Arbeitsablauf zum Erstellen des Ziels finden Sie auf den folgenden Seiten für die verschiedenen Zieltypen in CDP in Echtzeit:

* [Werbeziele - Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [Werbeziele - Google-Anzeigen](./catalog/advertising/google-ads-destination.md)
* [Werbeziele - Google Display &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [ Cloud-Speicher-Ziele](./catalog/cloud-storage/workflow.md)
* [E-Mail-Marketing-Ziele](./catalog/email-marketing/overview.md)
* [Ziele in sozialen Netzwerken ](./catalog/social/workflow.md)

Weitere Informationen zu Verstößen gegen die Datenrichtlinie im Arbeitsablauf für die Segmentanalyse finden Sie im Schritt &quot;Aktivierung überprüfen&quot;unter [Profil und Segmente an ein Ziel](./ui/activate-destinations.md#review)aktivieren.