---
title: (Beta) Experience Cloud Audiences
description: Erfahren Sie, wie Sie Audiences von Experience Platform an verschiedene Experience Platform-Lösungen freigeben können.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 72225ac673ed921b5857a14070660134949e7e3e
workflow-type: tm+mt
source-wordcount: '1611'
ht-degree: 23%

---

# (Beta) [!UICONTROL Experience Cloud Audiences] connection

Mit diesem Ziel können Sie Zielgruppen von Experience Platform für verschiedene Experience Cloud-Lösungen wie Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target oder Marketo freigeben.

![Das Ziel &quot;Experience Cloud-Zielgruppen&quot;, im Zielkatalog hervorgehoben.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* Dieses Ziel ersetzt die [Integration älterer Zielgruppenfreigabe](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) von Experience Platform bis zu verschiedenen Experience Cloud-Lösungen.
>* Dieses Ziel befindet sich derzeit in der Betaphase. Dokumentation und Funktionalitäten können sich ändern.

## Anwendungsfälle und Vorteile {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie die [!UICONTROL Experience Cloud Audiences] Ziel, hier finden Sie Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfälle für Data Management Platform aktivieren {#dmp-use-cases}

In Audience Manager können Sie Experience Platform-Zielgruppen für Anwendungsfälle von Data Management Platform verwenden, z. B.:

* Hinzufügen [Drittanbieterdaten](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) zu Ihren Segmenten hinzufügen;
* [Algorithmische Modellierung](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* Aktivieren Sie Ihre Zielgruppen für Cookie-basierte Ziele, die noch nicht im Experience Platform-Zielkatalog unterstützt werden.

### Granulare Steuerung exportierter Zielgruppen {#segments-control}

Verwenden Sie die neue Self-Service-Zielgruppenfreigabe-Integration über das Experience Cloud Audiences-Ziel, um auszuwählen, welche Zielgruppen in Audience Manager und darüber hinaus exportiert werden sollen. Auf diese Weise können Sie bestimmen, welche Zielgruppen Sie für andere Experience Cloud-Lösungen freigeben möchten und welche Zielgruppen Sie ausschließlich im Experience Platform halten möchten.

Die veraltete Zielgruppenfreigabe-Integration ermöglichte keine präzise Steuerung, welche Zielgruppen in Audience Manager und darüber hinaus exportiert werden sollten.

### Experience Platform-Audiences mit weiteren Experience Cloud-Lösungen freigeben {#share-segments-with-other-solutions}

Neben der Freigabe von Zielgruppen für Audience Manager können Sie mit der Zielkarte &quot;Experience Platform-Zielgruppen&quot;Zielgruppen für jede andere Experience Cloud-Lösung freigeben, für die Sie bereitgestellt sind, darunter:

* Adobe Campaign
* Adobe Target
* Advertising Cloud
* Analysen
* Marketo

<!--

Note: briefly talk about when to share audiences to these destinations using the existing destination cards and when to share using the new Experience Cloud Audiences destination. 

-->

## Voraussetzungen {#prerequisites}

>[!IMPORTANT]
>
> * Dieses Ziel steht für [Adobe Real-time Customer Data Platform Prime und Ultimate](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) -Kunden.
> * Sie benötigen eine Audience Manager-Lizenz, um die [Anwendungsfälle für Data Management Platform](#dmp-use-cases) weiter oben erwähnt.
> * You *nicht benötigen* eine Audience Manager-Lizenz für die gemeinsame Nutzung von Experience Platform-Zielgruppen mit Adobe Advertising Cloud, Adobe Target, Marketo und anderen Experience Cloud-Lösungen, die in der [Abschnitt oben](#share-segments-with-other-solutions).

### Für Kunden, die die alte Zielgruppen-Sharing-Lösung verwenden

Wenn Sie bereits Audiences von Experience Platform an Audience Manager und andere Experience Cloud-Lösungen über die [Integration älterer Zielgruppenfreigabe](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam)müssen Sie sich an die Kundenunterstützung oder Ihr Adobe-Account-Team wenden, um die alte Integration zu deaktivieren. Kundenunterstützung und Adobe-Account-Teams müssen ein Jira-Ticket (siehe Vorlagenticket PLAT-160986) einreichen, um die Integration zu deaktivieren.

Die Bearbeitungszeit zur Lösung des Deprovisioning-Tickets für Beta-Kunden beträgt sechs Geschäftstage oder weniger. Nachdem die vorhandene Legacy-Integration deaktiviert wurde, können Sie mit [Erstellen einer Verbindung](#connect) über die Zielkarte des Self-Service.

>[!IMPORTANT]
>
>Der Zielgruppenexport von Experience Platform in Ihre anderen Lösungen wird in der Zeit zwischen der Jira-Ticketauflösung und dem Zeitpunkt, zu dem über die Zielkarte eine neue Verbindung hergestellt wird, gestoppt. Sie können diese Ausfallzeit minimieren, indem Sie die Verbindung über die Zielkarte erstellen, sobald das Jira-Ticket geschlossen wird.

## Bekannte Einschränkungen und Hinweisen {#known-limitations}

Beachten Sie die folgenden bekannten Einschränkungen und wichtigen Hinweisen in der Beta-Version der Experience Cloud Audiences-Karte:

* [Überwachung von Datenflüssen](/help/dataflows/ui/monitor-destinations.md) wird nicht unterstützt.
* Beim Herstellen einer Verbindung zum Ziel sehen Sie eine Option zum [Datenflusswarnungen aktivieren](#enable-alerts). Die Benutzeroberfläche ist zwar sichtbar, die **Option für Warnhinweise wird nicht unterstützt** in der Beta-Version.
* **Aufstockungen werden nicht unterstützt**. Der erste Export in Audience Manager oder andere Experience Cloud-Lösungen umfasst keine historische Population der Zielgruppen.
* In der Beta-Version können Sie **eine einzige Zielverbindung zum Experience Cloud-Audiences-Ziel**, über alle Sandboxes Ihrer Experience Platform-Organisation hinweg.

### Latenz beim Aktivieren von Zielgruppen {#audience-activation-latency}

Es gibt eine vierstündige Latenz zwischen dem Zeitpunkt, zu dem Zielgruppen zum ersten Mal in Experience Platform aktiviert werden, und dem Zeitpunkt, zu dem sie für die Verwendung in Audience Manager- und anderen Experience Cloud-Lösungen für bestimmte Anwendungsfälle bereit sind.

Es kann bis zu 24 Stunden dauern, bis Zielgruppen im Audience Manager für alle Anwendungsfälle vollständig verfügbar sind, und bis zu 48 Stunden, bis Zielgruppen aus den Experience Cloud-Zielgruppen in Audience Manager-Berichten angezeigt werden.

Metadaten wie Zielgruppennamen sind innerhalb von Minuten nach der Einrichtung des Exports für das Experience Cloud-Zielgruppen-Ziel im Audience Manager verfügbar.

## Unterstützte Identitäten {#supported-identities}

Die Profile, die in die [!UICONTROL Experience Cloud Audiences] Ziel werden den in der folgenden Tabelle beschriebenen Identitäten zugeordnet. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| ECID | Experience Cloud ID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Siehe folgendes Dokument unter [ECID](/help/identity-service/ecid.md) für weitere Informationen. |
| GAID | Google Advertising ID | In Experience Platform erfasste Profile mit einer primären Kennung der Google Advertising ID (GAID) können an dieses Ziel exportiert werden. |
| IDFA | Apple ID für Advertiser | In Experience Platform erfasste Profile mit der primären ID Apple ID for Advertisers (IDFA) können an dieses Ziel exportiert werden. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | In Experience Platform erfasste Profile mit einer primären Identität von Hash-E-Mail-Adressen können an dieses Ziel exportiert werden. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Über die Experience Platform generierte Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe, die von den im obigen Abschnitt aufgelisteten Identitäten abgeleitet sind. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

>[!IMPORTANT]
> 
>In der Beta-Version können Sie eine einzige Zielverbindung zum Experience Cloud-Zielgruppen-Ziel für alle Sandboxes Ihrer Experience Platform-Organisation erstellen.

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

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.


## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele. ](/help/destinations/ui/activate-segment-streaming-destinations.md) Beachten Sie Folgendes: [Zuordnungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) ist erforderlich und nein [Planungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) für dieses Ziel verfügbar ist.

## Überprüfen des Datenexports {#exported-data}

Um einen erfolgreichen Datenexport zu validieren, können Sie überprüfen, ob Ihre Zielgruppen diese erfolgreich zu Ihrer gewünschten Experience Cloud-Lösung geführt haben.

### Daten in Audience Manager überprüfen

Ihre Experience Platform-Zielgruppen werden in Audience Manager als [Signale](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [Eigenschaften](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits), und [Segmente](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). Sie können in Audience Manager überprüfen, ob die Daten wie in den Dokumentationslinks oben beschrieben angezeigt wurden.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

Data Governance in Experience Platform wird von beiden durchgesetzt [Datennutzungsbezeichnungen](/help/data-governance/labels/reference.md) und Marketing-Aktionen.
Datennutzungsbezeichnungen werden an Anwendungen übertragen, Marketing-Aktionen jedoch nicht. Das bedeutet, dass Zielgruppen von Experience Platform nach dem landen im Audience Manager an alle verfügbaren Ziele exportiert werden können. In Audience Manager können Sie [Datenexportkontrollen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) um den Export von Audiences in bestimmte Ziele zu blockieren.

### Berechtigungsverwaltung in Audience Manager

Zielgruppen und Eigenschaften in Audience Manager unterliegen [Rollenbasierte Zugriffssteuerung](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=de) (RBAC).

Aus Experience Platform exportierte Zielgruppen werden einer bestimmten Datenquelle in Audience Manager mit dem Namen **[!UICONTROL Experience Platform von Segmenten]**.

Um nur bestimmten Benutzern Zugriff auf die Zielgruppen zu gewähren, können Sie Zugriffskontrollen auf die Zielgruppen anwenden, die zur Datenquelle gehören. Sie müssen in Audience Manager neue Zugriffssteuerungsberechtigungen für diese Zielgruppen und Eigenschaften festlegen, die aus Experience Platform-Segmenten erstellt wurden.
