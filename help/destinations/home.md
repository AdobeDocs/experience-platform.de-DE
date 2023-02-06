---
keywords: Ziele; Adobe Experience Platform; Plattform; Ziele - Übersicht; aktivieren von Daten; Aktivieren;
title: Ziele – Übersicht
description: Ziele sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Sie können Ziele in der Adobe Experience Platform verwenden, um Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle zu aktivieren.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 25f1b2197e5b10b04668d16bff3a6ce48cfad5fc
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 33%

---

# [!DNL Destinations] – Übersicht {#overview}

![Übersichtsbanner Ziele](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Ziele und Quellen {#destinations-and-sources}

Eine der Kernfunktionen von Platform besteht darin, Ihre Erstanbieterdaten zu erfassen und sie für Ihre geschäftlichen Anforderungen zu aktivieren. Verwendung [sources](../sources/home.md) , um Daten in Platform und Ziele zu erfassen und sie aus Platform zu exportieren.

## Ziele – Schritte {#steps}

* Wählen Sie aus einer [Self-Service-Katalog](./catalog/overview.md) aller in Platform verfügbaren Ziele.
* Verwenden Sie Ziele, um Profile oder Segmente an Plattformen zur Marketing-Automatisierung, digitale Werbeplattformen und mehr zu senden.
* Planen Sie Datenexporte an Ihre bevorzugten Ziele zu regelmäßigen Zeiten.

## Steuerelemente {#controls}

Die Steuerelemente in der [Zielarbeitsbereich](./ui/destinations-workspace.md) ermöglichen Ihnen Folgendes:

* Katalog der Zielplattformen durchsuchen, wo Sie Ihre Daten aktivieren können;
* Datenflüsse zu den Zielen im Katalog erstellen, bearbeiten, aktivieren und deaktivieren;
* Erstellen Sie ein Konto an einem Speicherort oder verknüpfen Sie Platform mit dem Konto in der Zielplattform.
* auswählen, welche Segmente für Ziele aktiviert werden sollen;
* auswählen, welche [Experience Data Model (XDM)-Felder](../xdm/home.md) exportiert werden sollen, wenn Segmente für E-Mail-Marketing-Ziele aktiviert werden.

## Zieltypen und Kategorien {#types-and-categories}

Mit Experience Platform können Sie Daten für verschiedene Zieltypen aktivieren, um Ihre Aktivierungs-Anwendungsfälle zu erfüllen. Die Ziele reichen von API-basierten Integrationen über Integrationen mit Dateiempfangssystemen bis hin zu Profilsuche-Zielen und mehr. Detaillierte Informationen zu allen verfügbaren Zielen finden Sie im Abschnitt [Zieltypen und Kategorien - Übersicht](./destination-types.md).

## Ziele und Zugriffskontrollen {#access-controls}

Die Zielfunktion in Platform funktioniert mit Zugriffssteuerungsberechtigungen von Adobe Experience Platform. Je nach Berechtigungsstufe Ihres Anwenders können Sie Ziele anzeigen, verwalten und aktivieren. Informationen zu den individuellen Berechtigungen finden Sie unter [Zugangssteuerung in Adobe Experience Platform](../access-control/home.md); scrollen Sie nach unten bis zum Ende der Seite.

In der folgenden Tabelle sind die Berechtigungen und Berechtigungskombinationen aufgeführt, die zum Ausführen bestimmter Aktionen für Ziele erforderlich sind:

| Berechtigungsebene | Beschreibung |
| ---- | ----|
| **[!UICONTROL Verwalten von Zielen]** | Um eine Verbindung zu Zielen herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). |
| **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** | Um Segmente für Ziele zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). |

{style=&quot;table-layout:auto&quot;}

Weiterführende Informationen zu Zugangssteuerungen finden Sie im [Benutzerhandbuch zur Zugangssteuerung](../access-control/ui/overview.md).

### Attributbasierte Zugriffskontrolle für Ziele {#attribute-based-access}

Die attributbasierte Zugriffssteuerung in Adobe Experience Platform ermöglicht Admins, den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen zu steuern.

Mit der attributbasierten Zugriffssteuerung können Sie Zuordnungskonfigurationen auf Felder anwenden, für die Sie über Berechtigungen verfügen. Außerdem können Sie keine Daten an ein Ziel exportieren, wenn Sie nicht Zugriff auf alle Felder im Datensatz haben.

Weitere Informationen dazu, wie Ziele mit attributbasierten Zugriffssteuerelementen funktionieren, finden Sie in der [Attributbasierte Zugriffskontrolle - Übersicht](../access-control/abac/overview.md#destinations).

## Zielüberwachung {#destinations-monitoring}

Nachdem Sie eine Verbindung zu einem Ziel hergestellt und den Aktivierungs-Workflow abgeschlossen haben, können Sie die Datenexporte an Ihr Empfangssystem überwachen. Lesen Sie die [Handbuch zur Überwachung von Datenflüssen zu Zielen in der Benutzeroberfläche](/help/dataflows/ui/monitor-destinations.md) für weitere Informationen.

Sie können auch überprüfen, ob die Daten erfolgreich zu Ihrem Ziel gelangen. Die meisten Zieldokumentationsseiten im Katalog verfügen über eine *Abschnitt &quot;Datenexport überprüfen&quot;*, der anzeigt, wie Sie in der Zielplattform überprüfen können, ob Daten erfolgreich aus Experience Platform importiert wurden.

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

Weitere Informationen zu Verstößen gegen Datenrichtlinien im Workflow für die Segmentaktivierung finden Sie unter **[!UICONTROL Überprüfen]** in die folgenden Handbücher zu übernehmen:

* [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](./ui/activate-segment-streaming-destinations.md#review)
* [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Profilen](./ui/activate-streaming-profile-destinations.md#review)
* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](./ui/activate-batch-profile-destinations.md#review)
