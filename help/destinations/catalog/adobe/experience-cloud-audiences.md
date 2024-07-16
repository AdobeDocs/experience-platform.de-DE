---
title: Experience Cloud-Zielgruppen
description: Erfahren Sie, wie Sie Audiences von Real-time Customer Data Platform für verschiedene Experience Cloud-Apps freigeben können.
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1703'
ht-degree: 16%

---


# Verbindung mit [!UICONTROL Experience Cloud Audiences]

>[!AVAILABILITY]
>
> Dieses Ziel ist für Kunden von [Adobe Real-time Customer Data Platform Prime und Ultimate](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) verfügbar.

Verwenden Sie dieses Ziel, um Zielgruppen von Real-Time CDP zu Audience Manager und Adobe Analytics zu aktivieren.

Zum Senden von Zielgruppen an Adobe Analytics benötigen Sie eine Audience Manager-Lizenz. Weitere Informationen finden Sie in der [Audience Analytics - Übersicht](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html?lang=en) .

Um Zielgruppen an andere Adobe-Lösungen zu senden, verwenden Sie die Direktverbindungen von Real-Time CDP zu [Adobe Target](../personalization/adobe-target-connection.md), [Adobe Advertising](../advertising/adobe-advertising-cloud-connection.md), [Adobe Campaign](../email-marketing/adobe-campaign.md) und [Marketo Engage](../adobe/marketo-engage.md).

>[!IMPORTANT]
>
>Dieses Ziel ersetzt die [alte Audience-Sharing-Integration](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam) von Real-time Customer Data Platform in verschiedene Experience Cloud-Lösungen.
> 
>Wenn Sie bereits Audiences von Real-Time CDP für Audience Manager und andere Experience Cloud-Lösungen über die [alte Audience-Sharing-Integration](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam) freigegeben haben, müssen Sie sich an die Kundenunterstützung wenden, um die veraltete Integration zu deaktivieren, bevor Sie dieses Ziel verwenden.

![Das Ziel &quot;Experience Cloud-Zielgruppen&quot;, im Zielkatalog hervorgehoben.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

## Anwendungsfälle und Vorteile {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie das Ziel [!UICONTROL Experience Cloud-Zielgruppen] verwenden sollten, finden Sie hier Beispielanwendungsfälle, die Real-Time CDP-Kunden mit diesem Ziel lösen können.

### Anwendungsfälle für Data Management Platform aktivieren {#dmp-use-cases}

In Audience Manager können Sie Real-Time CDP-Zielgruppen für Anwendungsfälle der Data Management Platform verwenden, z. B.:

* Hinzufügen von [Drittanbieterdaten](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html#third-party-data) zu Ihren Segmenten;
* [Algorithmische Modellierung](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html);
* Aktivieren Ihrer Zielgruppen für Cookie-basierte Ziele, die im Real-Time CDP-Zielkatalog noch nicht unterstützt werden.

### Granulare Steuerung exportierter Zielgruppen {#segments-control}

Verwenden Sie die neue Self-Service-Zielgruppenfreigabe-Integration über das Experience Cloud-Zielgruppen-Ziel, um festzulegen, welche Zielgruppen in Audience Manager und darüber hinaus exportiert werden sollen.  Auf diese Weise können Sie bestimmen, welche Zielgruppen Sie für andere Experience Cloud-Lösungen freigeben möchten und welche Zielgruppen Sie ausschließlich in Real-Time CDP beibehalten möchten.

Die veraltete Zielgruppenfreigabe-Integration ermöglichte keine präzise Steuerung, welche Zielgruppen in Audience Manager und darüber hinaus exportiert werden sollten.

### Freigeben von Real-Time CDP-Zielgruppen für Adobe Analytics {#share-audiences-with-analytics}

Zielgruppen, die Sie an das Experience Cloud Audiences-Ziel senden, werden nicht automatisch in Adobe Analytics angezeigt.

Bevor Sie Zielgruppen an Adobe Analytics senden können, müssen Sie [den Experience Cloud Identity-Dienst für Analytics und Audience Manager](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-aam-analytics.html?lang=en) implementieren.

>[!IMPORTANT]
>
>Um Zielgruppen von Real-Time CDP an Adobe Analytics über das Experience Cloud Audiences-Ziel zu senden, benötigen Sie eine Audience Manager-Lizenz.

### Real-Time CDP-Zielgruppen mit anderen Experience Cloud-Lösungen teilen {#share-segments-with-other-solutions}

Sie können die Zielkarte Real-Time CDP-Zielgruppen verwenden, um Zielgruppen mit anderen Experience Cloud-Lösungen zu teilen.

Adobe empfiehlt jedoch dringend die Verwendung der folgenden dedizierten Zielkarten, wenn Sie Zielgruppen für diese Lösungen freigeben möchten:

* [Adobe Campaign](../email-marketing/adobe-campaign.md)
* [Adobe Target](../personalization/adobe-target-connection.md)
* [Advertising Cloud](../advertising/adobe-advertising-cloud-connection.md)
* [Marketo](../adobe/marketo-engage.md)

## Voraussetzungen {#prerequisites}

>[!IMPORTANT]
>
> * Sie benötigen eine Audience Manager-Lizenz, um die oben erwähnten [Anwendungsfälle der Data Management Platform](#dmp-use-cases) zu aktivieren.
> * Sie *do* benötigen eine Audience Manager-Lizenz, um Real-Time CDP-Zielgruppen für Adobe Analytics freizugeben.
> * Sie benötigen *keine Audience Manager-Lizenz, um Real-Time CDP-Zielgruppen für Adobe Advertising Cloud, Adobe Target, Marketo und andere Experience Cloud-Lösungen freizugeben, wie im obigen Abschnitt [ erläutert.*](#share-segments-with-other-solutions)

### Für Kunden, die die veraltete Lösung zur Freigabe von Zielgruppen verwenden

Wenn Sie bereits Audiences von Real-Time CDP für Audience Manager- und andere Experience Cloud-Lösungen über die [alte Audience-Sharing-Integration](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam) freigegeben haben, müssen Sie sich an die Kundenunterstützung wenden, um die veraltete Integration zu deaktivieren.

Die Bearbeitungszeit für die Lösung des Deprovisioning-Tickets beträgt sechs Geschäftstage oder weniger. Nachdem die vorhandene alte Integration deaktiviert wurde, können Sie mit [Erstellen einer Verbindung](#connect) über die Self-Service-Zielkarte fortfahren.

>[!IMPORTANT]
>
>Der Zielgruppenexport aus Real-Time CDP in Ihre anderen Lösungen wird in der Zeit zwischen der Ticketauflösung und dem Zeitpunkt gestoppt, zu dem über die Zielkarte eine neue Verbindung hergestellt wird. Sie können diese Ausfallzeit minimieren, indem Sie die Verbindung über die Zielkarte erstellen, nachdem das Ticket geschlossen wurde.

## Bekannte Einschränkungen und Hinweisen {#known-limitations}

Beachten Sie die folgenden bekannten Einschränkungen und wichtigen Hinweisen bei der Verwendung der Experience Cloud Audiences -Karte:

* Derzeit wird ein einzelnes Experience Cloud-Zielgruppen-Ziel unterstützt. Der Versuch, eine zweite Zielverbindung zu konfigurieren, führt zu einem Fehler.
* Beim Herstellen einer Verbindung mit dem Ziel sehen Sie eine Option zum [Aktivieren von Datenfluss-Warnhinweisen](../../ui/alerts.md). Die Option **Warnhinweise aktivieren ist zwar in der Benutzeroberfläche sichtbar, wird jedoch derzeit nicht unterstützt**.
* **Unterstützung der Zielgruppen-Aufstockung**: Der erste Export in Audience Manager- oder andere Experience Cloud-Lösungen umfasst eine historische Population der Zielgruppen. Benutzer der [alten Audience-Sharing-Integration](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam), die dieses Ziel konfigurieren, sollten mit einer Aufstockungsdifferenz von etwa sechs Stunden rechnen.
* Zielgruppen aus [Zielgruppenkomposition](../../../segmentation/ui/audience-composition.md) werden nicht direkt unterstützt. Um gemischte Zielgruppen für dieses Ziel zu aktivieren, müssen Sie eine Zielgruppendefinition mithilfe von [Segment Builder](../../../segmentation/ui/segment-builder.md) erstellen, die auf Ihrer gemischten Zielgruppe basiert, und die neu erstellte Zielgruppe aktivieren.

### Latenz beim Aktivieren von Zielgruppen {#audience-activation-latency}

Es gibt eine vierstündige Latenz zwischen dem Zeitpunkt, zu dem Zielgruppen in Real-Time CDP erstmals aktiviert werden, und dem Zeitpunkt, zu dem sie für die Verwendung in Audience Manager- und anderen Experience Cloud-Lösungen bereit sind.

Es kann bis zu 24 Stunden dauern, bis Zielgruppen im Audience Manager für alle Anwendungsfälle vollständig verfügbar sind. Es kann bis zu 48 Stunden dauern, bis Zielgruppen aus Experience Cloud-Zielgruppen in Audience Manager-Berichten angezeigt werden.

Metadaten wie Zielgruppennamen sind innerhalb von Minuten nach der Einrichtung des Exports für das Experience Cloud-Zielgruppen-Ziel im Audience Manager verfügbar.

## Unterstützte Identitäten {#supported-identities}

Die Profile, die in das Ziel [!UICONTROL Experience Cloud Audiences] exportiert werden, werden den in der folgenden Tabelle beschriebenen Identitäten zugeordnet. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| ECID | Experience Cloud ID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Weitere Informationen finden Sie im folgenden Dokument zu [ECID](/help/identity-service/features/ecid.md) . |
| GAID | GOOGLE ADVERTISING ID | In Real-Time CDP erfasste Profile mit der primären Kennung Google Advertising ID (GAID) können an dieses Ziel exportiert werden. |
| IDFA | Apple ID für Advertiser | In Real-Time CDP erfasste Profile mit der Hauptidentität Apple ID for Advertisers (IDFA) können an dieses Ziel exportiert werden. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | In Real-Time CDP erfasste Profile mit einer primären Identität von Hash-E-Mail-Adressen können an dieses Ziel exportiert werden. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welcher Audience-Typ Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
| ---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die durch den Experience Platform [Segmentierungsdienst](../../../segmentation/home.md) generiert wurden. |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe, die von den im obigen Abschnitt aufgelisteten Identitäten abgeleitet sind. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Wenn ein Profil in Real-Time CDP basierend auf einer Zielgruppenbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Einrichten]** in der Zielkartenansicht im Katalog und dann **[!UICONTROL Mit Ziel verbinden]** aus.

![Ansicht der Option Mit Ziel verbinden für das Experience Cloud Audiences-Ziel.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Konfigurieren Sie den neuen Zielbildschirm mit den erforderlichen und optionalen Einstellungen für die Verbindung mit dem Experience Cloud-Zielgruppen-Ziel.](../..//assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für das Streaming von Zielgruppenexport-Zielen](/help/destinations/ui/activate-segment-streaming-destinations.md) . Für dieses Ziel ist kein [Zuordnungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) erforderlich und es ist kein [Planungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) verfügbar.

## Überprüfen des Datenexports {#exported-data}

Um einen erfolgreichen Datenexport zu validieren, können Sie überprüfen, ob Ihre Zielgruppen diese erfolgreich zu Ihrer gewünschten Experience Cloud-Lösung geführt haben.

### Daten in Audience Manager überprüfen

Ihre Real-Time CDP-Zielgruppen werden in Audience Manager als [Signale](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-signals), [Eigenschaften](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-traits) und [Segmente](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-segments) angezeigt. Sie können in Audience Manager überprüfen, ob die Daten wie in den Dokumentationslinks oben beschrieben angezeigt wurden.

Segmentnamen beginnen in Audience Manager 15 Minuten nach dem Versand der Zielgruppen aus Real-Time CDP mit dem Ausfüllen.

Die Segmentpopulation fließt innerhalb von 6 Stunden nach dem Versand aus Real-Time CDP in den Audience Manager und wird alle 24 Stunden im Audience Manager aktualisiert.

Die gesamte Population wird nach 72 Stunden im Audience Manager sichtbar sein und die Populationen fließen weiter in den Audience Manager, es sei denn, die Zielgruppe wird aus dem Ziel in Real-Time CDP entfernt.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Real-Time CDP]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

Data Governance in Real-Time CDP wird sowohl durch [Datennutzungsbezeichnungen](/help/data-governance/labels/reference.md) als auch durch Marketing-Aktionen durchgesetzt.
Datennutzungsbezeichnungen werden an Anwendungen übertragen, Marketing-Aktionen jedoch nicht. Das bedeutet, dass Zielgruppen aus Real-Time CDP nach dem landen im Audience Manager an alle verfügbaren Ziele exportiert werden können. In Audience Manager können Sie [Datenexport-Steuerelemente](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html) verwenden, um den Export von Zielgruppen an bestimmte Ziele zu verhindern.

Mit der Marketing-Aktion [!DNL HIPAA] markierte Zielgruppen werden nicht von Real-Time CDP an Audience Manager gesendet.

### Berechtigungsverwaltung in Audience Manager

Zielgruppen und Eigenschaften in Audience Manager unterliegen [rollenbasierten Zugriffskontrollen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html) (RBAC).

Aus Real-Time CDP exportierte Zielgruppen werden einer bestimmten Datenquelle im Audience Manager **[!UICONTROL Experience Platform-Segmente]** zugewiesen.

Um nur bestimmten Benutzern Zugriff auf die Zielgruppen zu gewähren, verwenden Sie [rollenbasierte Zugriffskontrollen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html) , um den Benutzerzugriff auf die in Real-Time CDP-Zielgruppen erstellten Zielgruppen und Eigenschaften zu konfigurieren.
