---
title: Ziele – Übersicht
description: Ziele sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Sie können Ziele in Adobe Experience Platform nutzen, um bekannte und unbekannte Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle zu aktivieren.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 6d97f132788a249e0bf5c293e34d9d529325f099
workflow-type: tm+mt
source-wordcount: '1231'
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
* Wählen Sie aus, welche [Experience-Datenmodell (XDM)-Felder](../xdm/home.md) exportiert werden sollen, wenn Zielgruppen für bestimmte Ziele wie E-Mail-Marketing-Ziele, CRM-Plattformen, Cloud-Speicher-Standorte und mehr aktiviert werden.
* Aktivieren verschiedener Typen von Profilen und Zielgruppen für Ziele - Personen, Konten und Interessenten.

## Zieltypen und Kategorien {#types-and-categories}

Mit Experience Platform können Sie Daten für verschiedene Zieltypen aktivieren, um Ihren Aktivierungs-Anwendungsfällen gerecht zu werden. Die Ziele reichen von API-basierten Integrationen über Integrationen mit Dateiempfangssystemen bis hin zu Profilsuchzielen und mehr. Detaillierte Informationen zu allen verfügbaren Zielen finden Sie in der [Übersicht über Zieltypen und Kategorien](./destination-types.md).

## Von Adobe und von Partnern erstellte Ziele {#adobe-and-partner-built-destinations}

Einige der Connectoren im Zielkatalog von Experience Platform werden von Adobe erstellt und gepflegt, während andere von Partnerunternehmen erstellt und gepflegt werden, die das [Destination SDK](/help/destinations/destination-sdk/overview.md) verwenden. Ein Hinweis oben auf der Dokumentationsseite für jeden von Partnern erstellten Connector gibt ab, ob ein Ziel vom Partner erstellt und gepflegt wird. Beispiel: Der [Amazon S3-Connector](/help/destinations/catalog/cloud-storage/amazon-s3.md) wird von Adobe erstellt, während der [TikTok-Connector](/help/destinations/catalog/social/tiktok.md) vom TikTok-Team erstellt und gepflegt wird.

Bei von Partnern erstellten und gepflegten Connectoren bedeutet dies, dass Probleme mit dem Connector möglicherweise vom Partner-Team behoben werden müssen (die Kontaktmethode ist jeweils im Hinweis auf der Dokumentationsseite angegeben). Wenden Sie sich bei Problemen mit von Adobe erstellten und gepflegten Connectoren an den Support oder den Kundendienst von Adobe.

## Ziele und Zugriffssteuerungen {#access-controls}

Die Funktion „Ziele“ in Platform arbeitet mit Zugriffssteuerungsberechtigungen von Adobe Experience Platform. Je nach Berechtigungsstufe Ihres Anwenders können Sie Ziele anzeigen, verwalten und aktivieren. Informationen zu den individuellen Berechtigungen finden Sie unter [Zugriffssteuerung in Adobe Experience Platform](../access-control/home.md) und scrollen Sie nach unten zur Tabelle am unteren Seitenrand.

In der folgenden Tabelle sind die Berechtigungen und Berechtigungskombinationen aufgeführt, die zum Ausführen bestimmter Aktionen für Ziele erforderlich sind.

| Berechtigungsebene | Beschreibung |
| ---- | ---- |
| **[!UICONTROL Anzeigen von Zielen]** | Um auf die Registerkarte &quot;Ziele&quot;in der Experience Platform-Benutzeroberfläche zuzugreifen, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Ziele anzeigen]** [3}.](/help/access-control/home.md#permissions) |
| **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele verwalten]** | Um eine Verbindung zu Zielen herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [.](/help/access-control/home.md#permissions) |
| **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** | Um Zielgruppen für Ziele zu aktivieren und den Schritt [Zuordnen](ui/activate-batch-profile-destinations.md#mapping) des Workflows zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [.](/help/access-control/home.md#permissions) |
| **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Segmente ohne Zuordnung aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** | Um Zielgruppen aus vorhandenen Datenflüssen hinzuzufügen oder aus ihnen zu entfernen, ohne Zugriff auf den Schritt [Zuordnen](ui/activate-batch-profile-destinations.md#mapping) des Workflows zu haben, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Segmente ohne Zuordnung aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [.](/help/access-control/home.md#permissions) |
| **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Datensatzziele verwalten und aktivieren]** | Zum Exportieren von Datensätzen in Ziele benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Datenziele verwalten und aktivieren]** [.](/help/access-control/home.md#permissions) |
| **[!UICONTROL Anzeigen von Identitätsdiagrammen]** | Um *Identitäten* in Ziele zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions) <br>. ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

Das folgende Diagramm zeigt visuell, welche Berechtigungen Sie benötigen, abhängig von den Vorgängen, die Sie für Ziele ausführen möchten.

![Diagramm, das die erforderlichen Berechtigungen zum Ausführen bestimmter Aktionen für Ziele anzeigt.](/help/destinations/assets/overview/permissions-diagram.png)

Weiterführende Informationen zu Zugriffssteuerungen finden Sie im [Benutzerhandbuch zur Zugriffssteuerung](../access-control/ui/overview.md).

### Attributbasierte Zugriffssteuerung für Ziele {#attribute-based-access}

Die attributbasierte Zugriffssteuerung in Adobe Experience Platform ermöglicht Admins, den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen zu steuern.

Mit der attributbasierten Zugriffssteuerung können Sie Zuordnungskonfigurationen auf Felder anwenden, für die Sie über Berechtigungen verfügen. Im Übrigen können Sie keine Daten an ein Ziel exportieren, wenn Sie nicht auf alle Felder im Datensatz Zugriff haben.

Weitere Informationen dazu, wie Ziele mit attributbasierten Zugriffssteuerelementen funktionieren, finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](../access-control/abac/overview.md#destinations).

## Zielüberwachung {#destinations-monitoring}

Nachdem Sie eine Verbindung zu einem Ziel hergestellt und den Aktivierungs-Workflow abgeschlossen haben, können Sie die Datenexporte an Ihr Empfangssystem überwachen. Weitere Informationen finden Sie im [Handbuch zur Überwachung von Datenflüssen zu Zielen in der Benutzeroberfläche](/help/dataflows/ui/monitor-destinations.md).

![Beispiel der Überwachungsseite für Ziele.](./assets/overview/monitoring-page-example.png)

Sie können auch überprüfen, ob die Daten erfolgreich zum Ziel gelangen. Die meisten Zieldokumentationsseiten im Katalog verfügen über einen Abschnitt *Datenexport überprüfen* , der anzeigt, wie Sie in der Zielplattform überprüfen können, ob Daten erfolgreich von Experience Platform bereitgestellt wurden. Sehen Sie sich ein Beispiel für diesen Abschnitt für das [Amazon Ads-Ziel](/help/destinations/catalog/advertising/amazon-ads.md#exported-data) an.

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

## Allgemeine Geschäftsbedingungen {#terms-and-conditions}

Mit der Verwendung eines der Ziele, die als Beta (&quot;Beta&quot;) gekennzeichnet sind, erkennen Sie hiermit an, dass der Beta ohne jegliche Garantie ******&quot;as is&quot; bereitgestellt wird.

Adobe ist nicht verpflichtet, die Beta-Version zu pflegen, zu korrigieren, zu aktualisieren, zu ändern oder anderweitig zu unterstützen. Es wird empfohlen, Informativ zu verwenden und sich nicht auf die ordnungsgemäße Funktionsweise oder Leistung der Beta und/oder der Begleitmaterialien zu verlassen. Die Beta-Version wird als vertrauliche Information von Adobe betrachtet.

Jedes „Feedback“ (Informationen zur Beta-Version, einschließlich, aber nicht beschränkt auf Probleme oder Mängel, auf die Sie bei der Verwendung der Beta-Version stoßen, Vorschläge, Verbesserungen und Empfehlungen), das Sie Adobe übermitteln, wird hiermit an Adobe übertragen, einschließlich aller Rechte, Titel und Interessen an diesem Feedback.

Senden Sie offenes Feedback oder erstellen Sie ein Support-Ticket, um Ihre Vorschläge mitzuteilen, einen Fehler zu melden oder um eine Funktionsverbesserung zu bitten.