---
title: Ziele – Übersicht
description: Ziele sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Sie können Ziele in Adobe Experience Platform nutzen, um bekannte und unbekannte Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle zu aktivieren.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 6dd6190f1b006ffb3346eea6dc917ce52e0aa1c6
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 63%

---

# [!DNL Destinations] – Übersicht {#overview}

![Übersichtsbanner Ziele .](./assets/overview/destinations-overview-banner.png)

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
* Verwenden Sie Ziele, um Zielgruppen oder Datensätze an Marketing-Automatisierungsplattformen, digitale Werbeplattformen und mehr zu senden.
* Planen Sie Datenexporte an Ihre bevorzugten Ziele zu regelmäßigen Zeiten.

## Steuerelemente {#controls}

Mit den Steuerelementen im [Arbeitsbereich „Ziele“](./ui/destinations-workspace.md) können Sie folgende Aufgaben erledigen:

* Katalog der Zielplattformen durchsuchen, wo Sie Ihre Daten aktivieren können;
* Datenflüsse zu den Zielen im Katalog erstellen, bearbeiten, aktivieren und deaktivieren;
* ein Konto an einem Speicherort erstellen oder Platform mit dem Konto auf der Zielplattform verknüpfen;
* Wählen Sie aus, welche Zielgruppen oder Datensätze für Ziele aktiviert werden sollen.
* Auswählen [Experience-Datenmodell (XDM)-Felder](../xdm/home.md) , um beim Aktivieren von Zielgruppen zu bestimmten Zielen wie E-Mail-Marketing-Zielen, CRM-Plattformen, Cloud-Speicherorten und mehr zu exportieren.
* Aktivieren verschiedener Typen von Profilen und Zielgruppen für Ziele - Personen, Konten und Interessenten.

## Zieltypen und Kategorien {#types-and-categories}

Mit Experience Platform können Sie Daten für verschiedene Zieltypen aktivieren, um Ihren Aktivierungs-Anwendungsfällen gerecht zu werden. Die Ziele reichen von API-basierten Integrationen über Integrationen mit Dateiempfangssystemen bis hin zu Profilsuchzielen und mehr. Detaillierte Informationen zu allen verfügbaren Zielen finden Sie im Abschnitt [Zieltypen und Kategorien - Übersicht](./destination-types.md).

## Von Adobe und von Partnern erstellte Ziele {#adobe-and-partner-built-destinations}

Einige der Connectoren im Zielkatalog von Experience Platform werden von Adobe erstellt und gepflegt, während andere von Partnerunternehmen erstellt und gepflegt werden, die das [Destination SDK](/help/destinations/destination-sdk/overview.md) verwenden. Ein Hinweis oben auf der Dokumentationsseite für jeden von Partnern erstellten Connector gibt ab, ob ein Ziel vom Partner erstellt und gepflegt wird. Beispiel: Der [Amazon S3-Connector](/help/destinations/catalog/cloud-storage/amazon-s3.md) wird von Adobe erstellt, während der [TikTok-Connector](/help/destinations/catalog/social/tiktok.md) vom TikTok-Team erstellt und gepflegt wird.

Bei von Partnern erstellten und gepflegten Connectoren bedeutet dies, dass Probleme mit dem Connector möglicherweise vom Partner-Team behoben werden müssen (die Kontaktmethode ist jeweils im Hinweis auf der Dokumentationsseite angegeben). Wenden Sie sich bei Problemen mit von Adobe erstellten und gepflegten Connectoren an den Support oder den Kundendienst von Adobe.

## Ziele und Zugriffssteuerungen {#access-controls}

Die Funktion „Ziele“ in Platform arbeitet mit Zugriffssteuerungsberechtigungen von Adobe Experience Platform. Je nach Berechtigungsstufe Ihres Anwenders können Sie Ziele anzeigen, verwalten und aktivieren. Informationen zu den individuellen Berechtigungen finden Sie unter [Zugriffskontrolle in Adobe Experience Platform](../access-control/home.md) und scrollen Sie nach unten zur Tabelle unten auf der Seite.

In der folgenden Tabelle sind die Berechtigungen und Berechtigungskombinationen aufgeführt, die zum Ausführen bestimmter Aktionen für Ziele erforderlich sind.

| Berechtigungsebene | Beschreibung |
| ---- | ---- |
| **[!UICONTROL Anzeigen von Zielen]** | Um auf die Registerkarte &quot;Ziele&quot;in der Experience Platform-Benutzeroberfläche zuzugreifen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). |
| **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele verwalten]** | Um eine Verbindung zu Zielen herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). |
| **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** | So aktivieren Sie Zielgruppen für Ziele und aktivieren die [Zuordnungsschritt](ui/activate-batch-profile-destinations.md#mapping) des Workflows benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). |
| **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Aktivieren von Segmenten ohne Zuordnung]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** | So fügen Sie Zielgruppen zu vorhandenen Datenflüssen hinzu oder entfernen diese, ohne Zugriff auf die [Zuordnungsschritt](ui/activate-batch-profile-destinations.md#mapping) des Workflows benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Aktivieren von Segmenten ohne Zuordnung]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). |
| **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Verwalten und Aktivieren von Datensatzzielen]** | Um Datensätze an Ziele zu exportieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Verwalten und Aktivieren von Datensatzzielen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). |
| **[!UICONTROL Anzeigen von Identitätsdiagrammen]** | Export *identities* zu Zielen hinzufügen, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

Das folgende Diagramm zeigt visuell, welche Berechtigungen Sie benötigen, abhängig von den Vorgängen, die Sie für Ziele ausführen möchten.

![Diagramm mit den erforderlichen Berechtigungen zum Ausführen bestimmter Aktionen für Ziele.](/help/destinations/assets/overview/permissions-diagram.png)

Weiterführende Informationen zu Zugriffssteuerungen finden Sie im [Benutzerhandbuch zur Zugriffssteuerung](../access-control/ui/overview.md).

### Attributbasierte Zugriffssteuerung für Ziele {#attribute-based-access}

Die attributbasierte Zugriffssteuerung in Adobe Experience Platform ermöglicht Admins, den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen zu steuern.

Mit der attributbasierten Zugriffssteuerung können Sie Zuordnungskonfigurationen auf Felder anwenden, für die Sie über Berechtigungen verfügen. Im Übrigen können Sie keine Daten an ein Ziel exportieren, wenn Sie nicht auf alle Felder im Datensatz Zugriff haben.

Weitere Informationen dazu, wie Ziele mit attributbasierten Zugriffssteuerelementen funktionieren, finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](../access-control/abac/overview.md#destinations).

## Zielüberwachung {#destinations-monitoring}

Nachdem Sie eine Verbindung zu einem Ziel hergestellt und den Aktivierungs-Workflow abgeschlossen haben, können Sie die Datenexporte an Ihr Empfangssystem überwachen. Weitere Informationen finden Sie im [Handbuch zur Überwachung von Datenflüssen zu Zielen in der Benutzeroberfläche](/help/dataflows/ui/monitor-destinations.md).

![Beispiel für die Zielüberwachungsseite.](./assets/overview/monitoring-page-example.png)

Sie können auch überprüfen, ob die Daten erfolgreich zum Ziel gelangen. Die meisten Zieldokumentationsseiten im Katalog verfügen über eine *Abschnitt &quot;Datenexport überprüfen&quot;*, der anzeigt, wie Sie in der Zielplattform überprüfen können, ob Daten erfolgreich von Experience Platform bereitgestellt wurden. Ein Beispiel für diesen Abschnitt anzeigen für [Amazon Ads-Ziel](/help/destinations/catalog/advertising/amazon-ads.md#exported-data).

## Data Governance-Einschränkungen bei der Aktivierung von Daten für Ziele {#data-governance}

Data Governance wird für Platform-Ziele durchgesetzt durch:

* *Marketing-Aktionen*, die Sie im Workflow zum Erstellen von Zielen auswählen können;
* *Datenrichtlinien*, die verhindern, dass Daten mit bestimmten Nutzungskennzeichnungen für Ziele mit bestimmten Marketing-Aktionen aktiviert werden.

Weitere Informationen zu [Marketing-Aktionen](../data-governance/policies/overview.md) und zum [Beheben von Verstößen gegen Datenrichtlinien](../data-governance/enforcement/auto-enforcement.md) finden Sie in der Dokumentation zu Data Governance in Platform.

Weitere Informationen zur Auswahl von Marketing-Aktionen im Workflow zum Erstellen von Zielen finden Sie auf den folgenden Seiten für die verschiedenen Zieltypen in Platform:

* [Werbeziele – Google Ad Manager](./catalog/advertising/google-ad-manager.md)
* [Werbeziele – Google Ads](./catalog/advertising/google-ads-destination.md)
* [Werbeziele – Google Display &amp; Video 360](./catalog/advertising/google-dv360.md)
* [Cloud-Speicher-Ziele](./catalog/cloud-storage/overview.md)
* [E-Mail-Marketing-Ziele ](./catalog/email-marketing/overview.md)
* [Social-Media-Ziele](./catalog/social/overview.md)

Weitere Informationen zu Verstößen gegen Datenrichtlinien im Workflow für die Zielgruppenaktivierung finden Sie im Schritt **[!UICONTROL Überprüfen]** der folgenden Handbücher:

* [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Zielgruppen](./ui/activate-segment-streaming-destinations.md#review)
* [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Profilen](./ui/activate-streaming-profile-destinations.md#review)
* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](./ui/activate-batch-profile-destinations.md#review)
