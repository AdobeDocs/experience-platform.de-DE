---
keywords: Ziele;Adobe Experience Platform;Plattform;Übersicht Ziele;Aktivieren von Daten;Aktivieren;
title: Ziele – Übersicht
description: Ziele sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Sie können Ziele in Adobe Experience Platform nutzen, um bekannte und unbekannte Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle zu aktivieren.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 546758c419670746cf55de35cbb33131d4457cb9
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 100%

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

Eine der Kernfunktionen von Platform besteht darin, Ihre Daten von Erstparteien zu erfassen und für Ihre geschäftlichen Anforderungen zu aktivieren. Verwenden Sie [Quellen](../sources/home.md), um Daten in Platform aufzunehmen, und Ziele, um Daten aus Platform zu exportieren.

## Ziele – Schritte {#steps}

* Wählen Sie in einem [Selbstbedienungs-Katalog](./catalog/overview.md) unter allen in Platform verfügbaren Zielen.
* Verwenden Sie Ziele, um Profile oder Segmente an Plattformen für Marketing-Automatisierung, digitale Werbung und andere zu senden.
* Planen Sie Datenexporte an Ihre bevorzugten Ziele zu regelmäßigen Zeiten.

## Steuerelemente {#controls}

Mit den Steuerelementen im [Arbeitsbereich „Ziele“](./ui/destinations-workspace.md) können Sie folgende Aufgaben erledigen:

* Katalog der Zielplattformen durchsuchen, wo Sie Ihre Daten aktivieren können;
* Datenflüsse zu den Zielen im Katalog erstellen, bearbeiten, aktivieren und deaktivieren;
* ein Konto an einem Speicherort erstellen oder Platform mit dem Konto auf der Zielplattform verknüpfen;
* auswählen, welche Segmente für Ziele aktiviert werden sollen;
* auswählen, welche [Experience Data Model (XDM)-Felder](../xdm/home.md) exportiert werden sollen, wenn Segmente für E-Mail-Marketing-Ziele aktiviert werden.

## Zieltypen und Kategorien {#types-and-categories}

Mit Experience Platform können Sie Daten für verschiedene Zieltypen aktivieren, um Ihren Aktivierungs-Anwendungsfällen gerecht zu werden. Die Ziele reichen von API-basierten Integrationen über Integrationen mit Dateiempfangssystemen bis hin zu Profilsuchzielen und mehr. Detaillierte Informationen zu allen verfügbaren Zielen finden Sie unter [Zieltypen und Kategorien – Übersicht](./destination-types.md).

## Ziele und Zugriffssteuerungen {#access-controls}

Die Funktion „Ziele“ in Platform arbeitet mit Zugriffssteuerungsberechtigungen von Adobe Experience Platform. Je nach Berechtigungsstufe Ihres Anwenders können Sie Ziele anzeigen, verwalten und aktivieren. Informationen zu den individuellen Berechtigungen finden Sie unter [Zugangssteuerung in Adobe Experience Platform](../access-control/home.md); scrollen Sie nach unten bis zum Ende der Seite.

In der folgenden Tabelle sind die Berechtigungen und Berechtigungskombinationen aufgeführt, die zum Ausführen bestimmter Aktionen für Ziele erforderlich sind:

| Berechtigungsebene | Beschreibung |
| ---- | ----|
| **[!UICONTROL Verwalten von Zielen]** | Um eine Verbindung zu Zielen herzustellen, benötigen Sie die [Zugriffssteuerungsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. |
| **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** | Zum Aktivieren von Segmenten für Ziele und Aktivieren des [Zuordnungsschritts](ui/activate-batch-profile-destinations.md#mapping) des Workflows sind die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** erforderlich. |
| **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Segmente ohne Zuordnung aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** | Zum Aktivieren von Segmenten für Ziele und Ausblenden des [Zuordnungsschritts](ui/activate-batch-profile-destinations.md#mapping) des Workflows sind die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Segmente ohne Zuordnung aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** erforderlich. |

{style="table-layout:auto"}

Weiterführende Informationen zu Zugriffssteuerungen finden Sie im [Benutzerhandbuch zur Zugriffssteuerung](../access-control/ui/overview.md).

### Attributbasierte Zugriffssteuerung für Ziele {#attribute-based-access}

Die attributbasierte Zugriffssteuerung in Adobe Experience Platform ermöglicht Admins, den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen zu steuern.

Mit der attributbasierten Zugriffssteuerung können Sie Zuordnungskonfigurationen auf Felder anwenden, für die Sie über Berechtigungen verfügen. Im Übrigen können Sie keine Daten an ein Ziel exportieren, wenn Sie nicht auf alle Felder im Datensatz Zugriff haben.

Weitere Informationen dazu, wie Ziele mit attributbasierten Zugriffssteuerelementen funktionieren, finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](../access-control/abac/overview.md#destinations).

## Zielüberwachung {#destinations-monitoring}

Nachdem Sie eine Verbindung zu einem Ziel hergestellt und den Aktivierungs-Workflow abgeschlossen haben, können Sie die Datenexporte an Ihr Empfangssystem überwachen. Weitere Informationen finden Sie im [Handbuch zur Überwachung von Datenflüssen zu Zielen in der Benutzeroberfläche](/help/dataflows/ui/monitor-destinations.md).

Sie können auch überprüfen, ob die Daten erfolgreich zum Ziel gelangen. Die meisten Zieldokumentationsseiten im Katalog verfügen über einen *Abschnitt „Datenexport validieren“*, der anzeigt, wie Sie in der Zielplattform feststellen können, ob Daten erfolgreich aus Experience Platform importiert wurden.

## Data-Governance-Beschränkungen beim Aktivieren von Daten für Ziele {#data-governance}

Data Governance wird für Platform-Ziele durchgesetzt durch:

* *Marketing-Aktionen*, die Sie im Workflow zum Erstellen von Zielen auswählen können;
* *Datenrichtlinien*, die verhindern, dass Daten mit bestimmten Nutzungskennzeichnungen für Ziele mit bestimmten Marketing-Aktionen aktiviert werden.

Weitere Informationen zu [Marketing-Aktionen](../data-governance/policies/overview.md) und zum [Beheben von Verstößen gegen Datenrichtlinien](../data-governance/enforcement/auto-enforcement.md) finden Sie in der Dokumentation zu Data Governance in Platform.

Weitere Informationen zur Auswahl von Marketing-Aktionen im Workflow zum Erstellen von Zielen finden Sie auf den folgenden Seiten für die verschiedenen Zieltypen in Platform:

* [Werbeziele – Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [Werbeziele – Google Ads](./catalog/advertising/google-ads-destination.md)
* [Werbeziele – Google Display &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [Cloud-Speicher-Ziele](./catalog/cloud-storage/overview.md)
* [E-Mail-Marketing-Ziele ](./catalog/email-marketing/overview.md)
* [Social-Media-Ziele ](./catalog/social/overview.md)

Weitere Informationen zu Verstößen gegen Datenrichtlinien im Workflow für die Segmentaktivierung finden Sie im Schritt **[!UICONTROL Überprüfen]** der folgenden Handbücher:

* [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](./ui/activate-segment-streaming-destinations.md#review)
* [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Profilen](./ui/activate-streaming-profile-destinations.md#review)
* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](./ui/activate-batch-profile-destinations.md#review)
