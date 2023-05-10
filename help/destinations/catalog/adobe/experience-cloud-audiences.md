---
title: (Beta) Experience Cloud Audiences
description: Erfahren Sie, wie Sie Segmente von Experience Platform für verschiedene Experience Platform-Lösungen freigeben können.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1509'
ht-degree: 24%

---

# (Beta) [!UICONTROL Experience Cloud Audiences] connection

Mit diesem Ziel können Sie Segmente von Experience Platform für verschiedene Experience Cloud-Lösungen wie Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target oder Marketo freigeben.

![Das Ziel &quot;Experience Cloud-Zielgruppen&quot;, im Zielkatalog hervorgehoben.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* Dieses Ziel ersetzt die [Integration älterer Segmentfreigabe](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) von der Experience Platform bis zu verschiedenen Experience Cloud-Lösungen.
>* Dieses Ziel befindet sich derzeit in der Betaphase. Dokumentation und Funktionalitäten können sich ändern.


## Anwendungsfälle und Vorteile {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie die [!UICONTROL Experience Cloud Audiences] Ziel, hier finden Sie Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfälle für Data Management Platform aktivieren {#dmp-use-cases}

In Audience Manager können Sie Experience Platform-Segmente für Anwendungsfälle der Data Management Platform verwenden, z. B.:

* Hinzufügen [Drittanbieterdaten](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) zu Ihren Segmenten hinzufügen;
* [Algorithmische Modellierung](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* Aktivieren Sie Ihre Segmente für Cookie-basierte Ziele, die im Zielkatalog der Experience Platform noch nicht unterstützt werden.

### Granulare Steuerung exportierter Segmente {#segments-control}

Verwenden Sie die neue Self-Service-Segmentfreigabe-Integration über das Experience Cloud-Zielgruppen-Ziel, um auszuwählen, welche Segmente in den Audience Manager und darüber hinaus exportiert werden sollen. Auf diese Weise können Sie bestimmen, welche Experience Cloud-Lösungen Sie für andere freigeben möchten und welche Segmente Sie ausschließlich in Experience Platform halten möchten.

Die veraltete Segmentfreigabe-Integration ermöglichte keine präzise Steuerung, welche Segmente in Audience Manager und darüber hinaus exportiert werden sollten.

### Freigeben von Experience Platform-Segmenten für weitere Experience Cloud-Lösungen {#share-segments-with-other-solutions}

Neben der Segmentfreigabe für Audience Manager können Sie mit der Zielkarte Experience Platform-Zielgruppen Segmente für beliebige andere Experience Cloud-Lösungen freigeben, für die Sie bereitgestellt sind, darunter:

* Adobe Campaign
* Adobe Target
* Advertising Cloud
* Analysen
* Marketo

<!--

Note: briefly talk about when to share segments to these destinations using the existing destination cards and when to share using the new Experience Cloud Audiences destination. 

-->

## Voraussetzungen {#prerequisites}

>[!IMPORTANT]
>
> * Dieses Ziel steht für [Adobe Real-time Customer Data Platform Prime und Ultimate](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) -Kunden.
> * Sie benötigen eine Audience Manager-Lizenz, um die [Anwendungsfälle für Data Management Platform](#dmp-use-cases) weiter oben erwähnt.
> * You *nicht benötigen* eine Audience Manager-Lizenz zum Freigeben von Experience Platform-Segmenten für Adobe Advertising Cloud, Adobe Target, Marketo und andere Experience Cloud-Lösungen, die in der [Abschnitt oben](#share-segments-with-other-solutions).


### Für Kunden, die die alte Segmentfreigabe-Lösung verwenden

Wenn Sie bereits Segmente von Experience Platform für Audience Manager und andere Experience Cloud-Lösungen über die [Integration älterer Segmentfreigabe](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam)müssen Sie sich entweder an die Kundenunterstützung oder das Kundenbetreuungsteam Ihrer Adobe wenden, um die veraltete Integration zu deaktivieren. Die Kundenbetreuungs- und Adobe-Kontoteams müssen ein Jira-Ticket (siehe Vorlagenticket AAM-52354) einreichen, um die Integration zu deaktivieren.

Die Bearbeitungszeit zur Lösung des Deprovisioning-Tickets für Beta-Kunden beträgt sechs Geschäftstage oder weniger. Nachdem die vorhandene Legacy-Integration deaktiviert wurde, können Sie mit dem [Erstellen einer Verbindung](#connect) über die Zielkarte des Self-Service.

>[!IMPORTANT]
>
>Der Segmentexport von Experience Platform in Ihre anderen Lösungen wird in der Zeit zwischen der Jira-Ticketauflösung und dem Zeitpunkt, zu dem über die Zielkarte eine neue Verbindung hergestellt wird, gestoppt. Sie können diese Ausfallzeit minimieren, indem Sie die Verbindung über die Zielkarte erstellen, sobald das Jira-Ticket geschlossen wird.

## Bekannte Einschränkungen und Hinweisen {#known-limitations}

Beachten Sie die folgenden bekannten Einschränkungen und wichtigen Hinweisen in der Beta-Version der Experience Cloud Audiences -Karte:

* [Überwachung von Datenflüssen](/help/dataflows/ui/monitor-destinations.md) wird nicht unterstützt.
* Beim Herstellen einer Verbindung zum Ziel sehen Sie eine Option zum [Datenflusswarnungen aktivieren](#enable-alerts). Die Benutzeroberfläche ist zwar sichtbar, die **Option für Warnhinweise wird nicht unterstützt** in der Beta-Version.
* **Aufstockungen werden nicht unterstützt**. Der erste Export in Audience Manager oder andere Segmentlösungen umfasst keine historische Segmentpopulation.
* In der Beta-Version können Sie **eine einzige Zielverbindung zum Ziel &quot;Experience Cloud-Zielgruppen&quot;**, in allen Sandboxes Ihrer Experience Platform-Organisation.
* Es gibt eine **vierstündige Latenz** zwischen dem Zeitpunkt, zu dem die Daten in der Experience Platform aktiviert werden, und dem Zeitpunkt, zu dem die Daten zur Verwendung in Audience Manager- und anderen Experience Cloud-Lösungen bereit sind.

## Unterstützte Identitäten {#supported-identities}

Die Profile, die in die [!UICONTROL Experience Cloud Audiences] Ziel werden den in der folgenden Tabelle beschriebenen Identitäten zugeordnet. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| ECID | Experience Cloud ID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Siehe folgendes Dokument unter [ECID](/help/identity-service/ecid.md) für weitere Informationen. |
| GAID | Google Advertising ID | Profile, die in Experience Platform mit der primären Kennung Google Advertising ID (GAID) erfasst werden, können an dieses Ziel exportiert werden. |
| IDFA | Apple ID für Advertiser | Profile, die in Experience Platform mit der primären ID Apple ID for Advertisers (IDFA) erfasst werden, können an dieses Ziel exportiert werden. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Profile, die in Experience Platform mit einer primären Identität von Hash-E-Mail-Adressen erfasst werden, können an dieses Ziel exportiert werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe), das die im obigen Abschnitt aufgelisteten Identitäten enthält. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

>[!IMPORTANT]
> 
>In der Beta-Version können Sie eine einzige Zielverbindung zum Ziel &quot;Experience Cloud-Zielgruppen&quot;für alle Sandboxes erstellen, die zu Ihrer Experience Platform-Organisation gehören.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Einrichten]** in der Zielkartenansicht des Katalogs und wählen Sie **[!UICONTROL Mit Ziel verbinden]**.

![Ansicht der Option Mit Ziel verbinden für das Experience Cloud Audiences-Ziel.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Konfigurieren Sie den neuen Zielbildschirm mit den erforderlichen und optionalen Einstellungen für die Verbindung mit dem Experience Cloud-Zielgruppen-Ziel.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.


## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele. ](/help/destinations/ui/activate-segment-streaming-destinations.md) Beachten Sie Folgendes: [Zuordnungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) ist erforderlich und nein [Planungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) für dieses Ziel verfügbar ist.

## Überprüfen des Datenexports {#exported-data}

Um einen erfolgreichen Datenexport zu validieren, können Sie überprüfen, ob Ihre Experience Cloud erfolgreich zu Ihrer gewünschten Segmentlösung gelangt sind.

### Daten in Audience Manager überprüfen

Ihre Experience Platform-Segmente werden in Audience Manager als [Signale](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [Eigenschaften](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits)und [Segmente](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). Sie können in Audience Manager überprüfen, ob die Daten wie in den Dokumentationslinks oben beschrieben angezeigt wurden.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

Data Governance in Experience Platform wird von beiden durchgesetzt [Datennutzungsbezeichnungen](/help/data-governance/labels/reference.md) und Marketing-Aktionen.
Datennutzungsbezeichnungen werden an Anwendungen übertragen, Marketing-Aktionen jedoch nicht. Das bedeutet, dass Segmente aus der Experience Platform nach dem Anlanden in Audience Manager an alle verfügbaren Ziele exportiert werden können. In Audience Manager können Sie [Datenexportkontrollen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) , um zu verhindern, dass Segmente an bestimmte Ziele exportiert werden.

### Berechtigungsverwaltung in Audience Manager

Segmente und Eigenschaften in Audience Manager unterliegen [Rollenbasierte Zugriffssteuerung](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=de) (RBAC).

Aus Experience Platform exportierte Segmente werden einer bestimmten Datenquelle in Audience Manager mit dem Namen **[!UICONTROL Experience Platform-Segmente]**.

Um nur bestimmten Benutzern Zugriff auf die Segmente zu gewähren, können Sie Zugriffssteuerungen auf die Segmente anwenden, die zur Datenquelle gehören. Sie müssen in Audience Manager neue Zugriffssteuerungsberechtigungen für diese Experience Platformen und Eigenschaften festlegen, die aus Segmenten erstellt wurden.
