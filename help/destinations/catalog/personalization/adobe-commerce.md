---
title: (Beta) Adobe Commerce Destination Connector
description: Erfahren Sie, wie Adobe Commerce- und Real-Time CDP-Händler das Einkaufserlebnis personalisieren können, indem sie hochrelevante Site-Inhalte und -Promotions bereitstellen, die auf Kundensegmente zugeschnitten sind, die in Real-Time CDP erstellt und verwaltet werden.
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 24%

---

# (Beta) Adobe Commerce-Verbindung {#adobe-commerce}

## Übersicht {#overview}

>[!IMPORTANT]
> 
>Die **[!UICONTROL Adobe Commerce]** -Connector befindet sich in der Beta-Phase und steht nur einer bestimmten Anzahl von Kunden zur Verfügung.

Die [!DNL Adobe Commerce] Mit dem Ziel-Connector können Sie ein oder mehrere Experience Platform-Segmente auswählen, die für Ihre [!DNL Adobe Commerce] -Konto ein dynamisches personalisiertes Erlebnis für Ihre Kunden bereitstellen. Within [!DNL Adobe Commerce]können Sie dann diese Adobe Experience Platform-Segmente auswählen, um individuelle Angebote im Warenkorb zu personalisieren, z. B. &quot;Kauf 2 erhält 1 kostenlos&quot;. Sie können Hero-Banner auch anzeigen und die Produktpreise über Werbeangebote ändern, die alle auf Adobe Experience Platform-Segmente zugeschnitten sind.

<!--## Use cases {#use-cases}

To help you better understand how and when you should use the *YourDestination* destination, here are sample use cases that Adobe Experience Platform customers can solve by using this destination.

### Use case #1 {#use-case-1}

*For mobile messaging platforms:*

*A home rental and sales platform wants to push mobile notifications to customers' Android and iOS devices to let them know that there are 100 updated listings in the area where they previously searched for a rental.*

### Use case #2 {#use-case-2}

*For social network platforms:*

*An athletic apparel brand wants to reach existing customers through their social media accounts. The apparel brand can ingest email addresses from their own CRM to Adobe Experience Platform, build segments from their own offline data, and send these segments to YourDestination, to display ads in their customers' social media feeds.*-->

## Voraussetzungen {#prerequisites}

Diese Erweiterung ist im Zielkatalog für ausgewählte Beta-Kunden verfügbar, die Real-Time CDP Prime oder Ultimate und Adobe Commerce erworben haben.

Beta-Kunden sollten Zugriff auf Folgendes haben:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/)
- [Adobe Commerce Cloud-Version 2.4.3 oder höher](https://business.adobe.com/products/magento/magento-commerce.html)

Erstellen Sie in Experience Platform Folgendes:

- [Schema](../../../xdm/schema/composition.md). Das von Ihnen erstellte Schema stellt die Daten dar, die Sie aus Adobe Commerce aufnehmen möchten. [Weitere Infos](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html) Informationen zum Erstellen eines Schemas, das Commerce-spezifische Feldergruppen enthält.
- [Datensatz](../../../catalog/datasets/user-guide.md#create). Ein Datensatz ist ein Speicher- und Verwaltungskonstrukt für eine Datenerfassung. Sie müssen diesen Datensatz aus dem oben erstellten Schema erstellen.
- [Datenstrom](../../../edge/datastreams/overview.md#create). ID, die den Datenfluss von Adobe Experience Platform zu anderen Adobe-DX-Produkten ermöglicht. Diese ID muss mit einer bestimmten Website in Ihrer jeweiligen Adobe Commerce-Instanz verknüpft sein. Wenn Sie diesen Datastream erstellen, geben Sie das oben erstellte XDM-Schema an.

Nachdem Sie die Voraussetzungen erfüllt haben, stellen Sie eine Verbindung zum [!DNL Commerce] Ziel.

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

So stellen Sie eine Verbindung zu [!DNL Adobe Commerce] Ziel:

1. Im [Plattform-Benutzeroberfläche](https://experience.adobe.com/platform/), gehen Sie zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**.
1. Auswählen **[!UICONTROL Personalisierung]**.
1. Wählen Sie das Adobe Commerce-Ziel aus, um es zu markieren, und wählen Sie dann **[!UICONTROL Einrichten]**.
1. Führen Sie die im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md).

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

- **[!UICONTROL Name]**: Geben Sie den gewünschten Namen für das Ziel ein.
- **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für das Ziel ein. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden. Dieses Feld ist optional.
- **[!UICONTROL Integrationsalias]**: Dieser Wert wird als JSON-Objektname an das Experience Platform Web SDK gesendet.
- **[!UICONTROL Datenstrom-ID]**: Diese Angabe legt fest, in welchen Datenerfassungsdatenstrom die Segmente in der Antwort auf die Seite aufgenommen werden. Das Dropdown-Menü enthält nur Datenströme, für die die Zielkonfiguration aktiviert ist. Weitere Details finden Sie unter [Konfigurieren eines Datenstroms](../../../edge/datastreams/overview.md).

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen über den Status des Datenflusses an Ihr Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zu [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung angegeben haben, wählen Sie **[!UICONTROL Nächste]**.

## Aktivieren von Segmenten für die [!DNL Commerce] Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Profile und Segmente für Profilanforderungsziele aktivieren](../../ui/activate-profile-request-destinations.md) Anweisungen zum Aktivieren von Zielgruppensegmenten für die [!DNL Commerce] Ziel.

## Nächste Schritte in [!DNL Adobe Commerce]

Nachdem Sie die [!DNL Commerce] Ziel in Experience Platform konfigurieren, müssen Sie die [!DNL Commerce Admin] , um die von Ihnen erstellten Real-Time CDP-Segmente zu importieren. Siehe [[!DNL Commerce] Dokumentation](https://docs.magento.com/user-guide/marketing/customer-segment-rtcdp.html) , um mehr zu erfahren.

## Datenexport überprüfen {#exported-data}

Nachdem Sie Real-Time CDP-Segmente für Ihre [!DNL Adobe Commerce] -Konto verwenden, werden diese Segmente im [!DNL Admin] beim Erstellen einer Warenkorbpreisregel:

![Adobe Commerce Admin](../../assets/catalog/personalization/adobe-commerce/rtcdp-in-admin.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
