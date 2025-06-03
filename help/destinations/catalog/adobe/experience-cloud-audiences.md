---
title: Experience Cloud-Zielgruppen
description: Erfahren Sie, wie Sie Audiences aus Real-Time Customer Data Platform für verschiedene Experience Cloud-Programme freigeben.
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 00da5d8c0eaaecb5b1f5ad5bff7482f3bf4023e2
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 16%

---


# [!UICONTROL Experience Cloud Audiences]-Verbindung

>[!AVAILABILITY]
>
> Dieses Ziel ist für Kunden von [Adobe Real-Time Customer Data Platform Prime und Ultimate](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) verfügbar.

Verwenden Sie dieses Ziel, um Zielgruppen von Real-Time CDP für Audience Manager und Adobe Analytics zu aktivieren.

Zum Senden von Zielgruppen an Adobe Analytics benötigen Sie eine Audience Manager-Lizenz. Weitere Informationen finden Sie in der Übersicht zu [Audience Analytics](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html?lang=de).

Um Zielgruppen an andere Adobe-Lösungen zu senden, verwenden Sie die Direktverbindungen von Real-Time CDP zu [Adobe Target](../personalization/adobe-target-connection.md), [Adobe Advertising](../advertising/adobe-advertising-cloud-connection.md), [Adobe Campaign](../email-marketing/adobe-campaign.md) und [Marketo Engage](../adobe/marketo-engage.md).

>[!IMPORTANT]
>
>Dieses Ziel ersetzt die [veraltete Audience-Sharing-Integration](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=de#aep-segments-in-aam) von Real-Time Customer Data Platform zu verschiedenen Experience Cloud-Lösungen.
> 
>Wenn Sie Zielgruppen bereits von Real-Time CDP für Audience Manager und andere Experience Cloud-Lösungen über die [veraltete Integration zur Freigabe von Zielgruppen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=de#aep-segments-in-aam) freigeben, müssen Sie sich an die Kundenunterstützung wenden, um die veraltete Integration zu deaktivieren, bevor Sie dieses Ziel verwenden.

![Das Experience Cloud-Zielgruppen-Ziel, das im Zielkatalog hervorgehoben ist.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

## Anwendungsbeispiele und Vorteile {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das Ziel [!UICONTROL Experience Cloud Audiences] verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Kundinnen und Kunden von Real-Time CDP mit diesem Ziel bewältigen können.

### Anwendungsfälle der Data Management-Plattform aktivieren {#dmp-use-cases}

In Audience Manager können Sie Real-Time CDP-Zielgruppen für Anwendungsfälle der Data Management-Plattform verwenden, z. B.:

* Hinzufügen [Drittanbieterdaten](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=de#third-party-data) zu Ihren Segmenten
* [Algorithmische Modellierung](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=de);
* Aktivieren Ihrer Zielgruppen für Cookie-basierte Ziele, die noch nicht im Real-Time CDP-Zielkatalog unterstützt werden.

### Granulare Steuerung exportierter Zielgruppen {#segments-control}

Um auszuwählen, welche Zielgruppen in Audience Manager und darüber hinaus exportiert werden sollen, verwenden Sie die neue Integration der Self-Service-Zielgruppenfreigabe über das Experience Cloud-Zielgruppen-Ziel.  Auf diese Weise können Sie festlegen, welche Zielgruppen Sie für andere Experience Cloud-Lösungen freigeben möchten und welche Zielgruppen Sie ausschließlich in Real-Time CDP behalten möchten.

Die veraltete Integration zur Freigabe von Audiences ermöglichte keine granulare Kontrolle darüber, welche Audiences nach Audience Manager und darüber hinaus exportiert werden sollten.

### Freigeben von Real-Time CDP-Zielgruppen mit Adobe Analytics {#share-audiences-with-analytics}

Zielgruppen, die Sie an das Experience Cloud-Zielgruppen-Ziel senden, werden in Adobe Analytics nicht automatisch angezeigt.

Bevor Sie Zielgruppen an Adobe Analytics senden können, müssen Sie [den Experience Cloud Identity Service für Analytics und Audience Manager implementieren](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-aam-analytics.html?lang=de).

>[!IMPORTANT]
>
>Zum Senden von Zielgruppen von Real-Time CDP über das Experience Cloud Audiences -Ziel an Adobe Analytics benötigen Sie eine Audience Manager-Lizenz.

### Freigeben von Real-Time CDP-Zielgruppen mit anderen Experience Cloud-Lösungen {#share-segments-with-other-solutions}

Sie können die Zielkarte Real-Time CDP-Zielgruppen verwenden, um Zielgruppen für andere Experience Cloud-Lösungen freizugeben.

Adobe empfiehlt jedoch dringend die Verwendung der folgenden dedizierten Zielkarten, wenn Sie Zielgruppen für diese Lösungen freigeben möchten:

* [Adobe Campaign](../email-marketing/adobe-campaign.md)
* [Adobe Target](../personalization/adobe-target-connection.md)
* [Advertising Cloud](../advertising/adobe-advertising-cloud-connection.md)
* [Marketo](../adobe/marketo-engage.md)

## Voraussetzungen {#prerequisites}

>[!IMPORTANT]
>
> * Sie benötigen eine Audience Manager-Lizenz, um die oben genannten Anwendungsfälle [Datenverwaltungsplattform](#dmp-use-cases) zu aktivieren.
> * Sie ** eine Audience Manager-Lizenz, um Real-Time CDP-Zielgruppen für Adobe Analytics freizugeben.
> * Sie *keine Audience Manager* Lizenz benötigen, um Real-Time CDP-Zielgruppen für Adobe Advertising Cloud, Adobe Target, Marketo und andere Experience Cloud-Lösungen freizugeben, die im [ Abschnitt oben ](#share-segments-with-other-solutions).

### Für Kunden, die die alte Lösung zur Freigabe von Zielgruppen verwenden

Wenn Sie Zielgruppen bereits von Real-Time CDP für Audience Manager und andere Experience Cloud-Lösungen über die [veraltete Integration zur Freigabe von Zielgruppen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=de#aep-segments-in-aam) freigeben, müssen Sie sich an die Kundenunterstützung wenden, um die veraltete Integration zu deaktivieren.

Die Durchlaufzeit zur Lösung des Deprovisioning-Tickets beträgt maximal sechs Werktage. Nachdem die vorhandene Legacy-Integration deaktiviert wurde, können Sie über [ Selbstbedienungs-Zielkarte mit dem ](#connect) „Verbindung erstellen“ fortfahren.

>[!IMPORTANT]
>
>Der Zielgruppenexport aus Real-Time CDP in Ihre anderen Lösungen wird in der Zeit zwischen der Ticketauflösung und dem Zeitpunkt angehalten, zu dem über die Zielkarte eine neue Verbindung hergestellt wird. Sie können diese Ausfallzeit minimieren, indem Sie die Verbindung über die Zielkarte erstellen, nachdem das Ticket geschlossen wurde.

## Bekannte Einschränkungen und Hinweise {#known-limitations}

Beachten Sie die folgenden bekannten Einschränkungen und wichtigen Hinweise bei der Verwendung der Karte Experience Cloud-Zielgruppen :

* Derzeit können Sie das Experience Cloud Audiences -Ziel in einer Sandbox pro Organisation konfigurieren. Der Versuch, eine zweite Zielverbindung in einer anderen Sandbox zu konfigurieren, führt zu einem Fehler.
* Beim Herstellen einer Verbindung zum Ziel wird die Option &quot;[ aktivieren“ ](../../ui/alerts.md). Die Option **Warnhinweise aktivieren“ ist zwar in der Benutzeroberfläche sichtbar, wird aber derzeit nicht**.
* **Unterstützung der Zielgruppen-Aufstockung**: Der erste Export in Audience Manager oder andere Experience Cloud-Lösungen umfasst eine historische Population der Zielgruppen. Benutzende der [Legacy-Zielgruppenfreigabeintegration](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=de#aep-segments-in-aam) die dieses Ziel konfigurieren, sollten mit einer Aufstockungsdifferenz von etwa sechs Stunden rechnen.
* Audiences, die aus [Audience-Komposition](../../../segmentation/ui/audience-composition.md) stammen, werden nicht direkt unterstützt. Um zusammengesetzte Zielgruppen für dieses Ziel zu aktivieren, müssen Sie über [Segment Builder](../../../segmentation/ui/segment-builder.md) eine Zielgruppendefinition basierend auf Ihrer zusammengesetzten Zielgruppe erstellen und die neu erstellte Zielgruppe aktivieren.

### Latenz beim Aktivieren von Zielgruppen {#audience-activation-latency}

Zwischen der ersten Aktivierung von Zielgruppen in Real-Time CDP und der Zeit, in der sie für die Verwendung in Audience Manager und anderen Experience Cloud-Lösungen bereit sind, liegt eine Latenz von vier Stunden.

Es kann bis zu 24 Stunden dauern, bis Zielgruppen in Audience Manager für alle Anwendungsfälle vollständig verfügbar sind. Es kann bis zu 48 Stunden dauern, bis Zielgruppen aus Experience Cloud-Zielgruppen in Audience Manager-Berichten angezeigt werden.

Metadaten wie Zielgruppennamen sind in Audience Manager innerhalb von Minuten nach der Einrichtung des Exports für das Experience Cloud Audiences-Ziel verfügbar.

## Unterstützte Identitäten {#supported-identities}

Die Profile, die an das Ziel [!UICONTROL Experience Cloud Audiences] exportiert werden, werden den in der folgenden Tabelle beschriebenen Identitäten zugeordnet. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| ECID | Experience Cloud ID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Weitere Informationen finden Sie im folgenden Dokument [ECID](/help/identity-service/features/ecid.md) . |
| GAID | GOOGLE ADVERTISING ID | Profile, die in Real-Time CDP mit der Hauptidentität Google Advertising ID (GAID) aufgenommen werden, können an dieses Ziel exportiert werden. |
| IDFA | Apple-ID für Werbetreibende | Profile, die in Real-Time CDP mit der Hauptidentität Apple ID for Advertisers (IDFA) aufgenommen werden, können an dieses Ziel exportiert werden. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Profile, die in Real-Time CDP mit der primären Identität einer gehashten E-Mail-Adresse aufgenommen werden, können an dieses Ziel exportiert werden. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Art von Zielgruppe Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
| ---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe, die aus den im obigen Abschnitt aufgelisteten Identitäten abgeleitet wurden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Wenn ein Profil in Real-Time CDP auf der Grundlage einer Zielgruppenbewertung aktualisiert wird, sendet der Connector die Aktualisierung nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Einrichten]** in der Ansicht der Zielkarte im Katalog und wählen Sie **[!UICONTROL Mit Ziel verbinden]**.

![Ansicht der Option Mit Ziel verbinden für das Experience Cloud Audiences -Ziel.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Bildschirm Neues Ziel konfigurieren mit den erforderlichen und optionalen Einstellungen für die Verbindung mit dem Experience Cloud Audiences-Ziel.](../..//assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen [ Aktivieren von Zielgruppen für dieses Ziel finden Sie unter „Aktivieren von Profilen ](/help/destinations/ui/activate-segment-streaming-destinations.md) Zielgruppen für Streaming-Zielgruppenexportziele“. Für [ Ziel ist ](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)Zuordnungsschritt) erforderlich und kein [Planungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) verfügbar.

## Überprüfen des Datenexports {#exported-data}

Um einen erfolgreichen Datenexport zu validieren, können Sie überprüfen, ob Ihre Zielgruppen erfolgreich zu Ihrer gewünschten Experience Cloud-Lösung gelangt sind.

### Validieren von Daten in Audience Manager

Ihre Real-Time CDP-Zielgruppen werden in Audience Manager [Signale](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=de#aep-segments-as-aam-signals), [Eigenschaften](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=de#aep-segments-as-aam-traits) und [Segmente](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=de#aep-segments-as-aam-segments). Sie können in Audience Manager überprüfen, ob die Daten wie unter den obigen Dokumentations-Links beschrieben angezeigt wurden.

Segmentnamen werden 15 Minuten, nachdem die Zielgruppen von Real-Time CDP gesendet wurden, in Audience Manager angezeigt.

Die Segmentpopulation beginnt innerhalb von 6 Stunden nach dem Versand aus Real-Time CDP in Audience Manager zu fließen und wird in Audience Manager alle 24 Stunden aktualisiert.

Die gesamte Population ist nach 72 Stunden in Audience Manager sichtbar und die Populationen fließen weiterhin nach Audience Manager, es sei denn, die Zielgruppe wurde aus dem Ziel in Real-Time CDP entfernt.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Real-Time CDP]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

Data Governance in Real-Time CDP wird sowohl durch [Datennutzungskennzeichnungen“ als auch durch ](/help/data-governance/labels/reference.md) erzwungen.
Datennutzungskennzeichnungen werden an Programme übertragen, Marketing-Aktionen jedoch nicht. Dies bedeutet, dass Zielgruppen aus Real-Time CDP nach der Landung in Audience Manager an alle verfügbaren Ziele exportiert werden können. In Audience Manager können Sie [Datenexportsteuerelemente) verwenden](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=de) um zu verhindern, dass Zielgruppen in bestimmte Ziele exportiert werden.

Zielgruppen, die mit der Marketing-Aktion [!DNL HIPAA] gekennzeichnet sind, werden nicht von Real-Time CDP an Audience Manager gesendet.

### Berechtigungsverwaltung in Audience Manager

Zielgruppen und Eigenschaften in Audience Manager unterliegen [rollenbasierten Zugriffssteuerung](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=de) (RBAC).

Aus Real-Time CDP exportierte Zielgruppen werden einer bestimmten Datenquelle in Audience Manager zugewiesen, die als **[!UICONTROL Experience Platform-Segmente bezeichnet]**.

Um nur bestimmten Benutzenden den Zugriff auf die Zielgruppen zu gewähren, konfigurieren Sie mit [Rollenbasierten Zugriffssteuerungen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=de) den Benutzerzugriff auf die Zielgruppen und Eigenschaften, die aus Real-Time CDP-Zielgruppen erstellt wurden.
