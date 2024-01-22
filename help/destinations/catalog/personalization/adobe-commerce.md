---
title: Adobe Commerce Destination Connector
description: Erfahren Sie, wie Adobe Commerce- und Real-Time CDP-Händler das Einkaufserlebnis personalisieren können, indem sie hochrelevante Site-Inhalte und -Promotions bereitstellen, die auf in Real-Time CDP erstellte und verwaltete Kundenzielgruppen zugeschnitten sind.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 53%

---

# Adobe Commerce-Verbindung {#adobe-commerce}

## Übersicht {#overview}

Die [!DNL Adobe Commerce] Mit dem Ziel-Connector können Sie eine oder mehrere Real-Time CDP-Zielgruppen auswählen, die für Ihre [!DNL Adobe Commerce] -Konto ein dynamisches personalisiertes Erlebnis für Ihre Kunden bereitstellen. Within [!DNL Adobe Commerce]können Sie dann diese Real-Time CDP-Zielgruppen auswählen, um individuelle Angebote im Warenkorb zu personalisieren, z. B. &quot;Kauf 2 erhalten 1 gratis&quot;. Sie können Hero-Banner auch anzeigen und die Produktpreise über Werbeangebote ändern, die alle auf Adobe Real-Time CDP-Zielgruppen abgestimmt sind.

## Voraussetzungen {#prerequisites}

Dieser Connector ist im Zielkatalog für Kunden verfügbar, die Real-Time CDP Prime oder Ultimate und Adobe Commerce erworben haben.

Um diese Zielverbindung zu verwenden, müssen Sie Zugriff auf Folgendes haben:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer-Konsole](https://developer.adobe.com/developer-console/docs/guides/getting-started/). Mit Zugriff auf die Entwicklerkonsole können Sie Informationen zu Dienstkonten und Anmeldedaten anzeigen, die für [Konfiguration abschließen](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html#configure-the-extension) der Erweiterung in Adobe Commerce.
- [Adobe Commerce Cloud-Version 2.4.4 oder höher](https://business.adobe.com/de/products/magento/magento-commerce.html)

Erstellen Sie in Experience Platform Folgendes:

- [Schema](../../../xdm/schema/composition.md). Das Schema, das Sie erstellen, repräsentiert die Daten, die Sie aus Adobe Commerce aufnehmen möchten. [Erfahren Sie mehr](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html) darüber, wie man ein Schema erstellt, das Commerce-spezifische Feldergruppen enthält.
- [Datensatz](../../../catalog/datasets/user-guide.md#create). Ein Datensatz ist ein Speicher- und Verwaltungskonstrukt für eine Sammlung von Daten. Sie erstellen diesen Datensatz aus dem Schema, das Sie oben erstellt haben.
- [Datenstrom](../../../datastreams/overview.md#create). ID, die den Datenfluss von Adobe Experience Platform zu anderen Adobe-DX-Produkten ermöglicht. Diese ID muss mit einer bestimmten Website in Ihrer jeweiligen Adobe Commerce-Instanz verknüpft sein. Wenn Sie diesen Datenstrom erstellen, geben Sie das von Ihnen oben erstellte XDM-Schema an.

Nachdem Sie die Voraussetzungen erfüllt haben, stellen Sie eine Verbindung mit dem Ziel [!DNL Commerce] her.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

So stellen Sie eine Verbindung mit dem Ziel [!DNL Adobe Commerce] her:

1. Gehen Sie in der [Platform-Oberfläche](https://experience.adobe.com/platform/) zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**.
1. Wählen Sie **[!UICONTROL Personalisierung]** aus.
1. Wählen Sie das Adobe Commerce-Ziel aus, um es zu markieren, und wählen Sie dann **[!UICONTROL Einrichten]** aus.
1. Führen Sie die im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschriebenen Schritte aus.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

- **[!UICONTROL Name]**: Geben Sie den gewünschten Namen für das Ziel ein.
- **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für das Ziel ein. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden. Dieses Feld ist optional.
- **[!UICONTROL Integrationsalias]**: Dieser Wert wird als JSON-Objektname an das Experience Platform Web SDK gesendet.
- **[!UICONTROL Datenspeicher-ID]**: Dadurch wird bestimmt, welcher Datenerfassungs-Datastream die Zielgruppen enthält, die in der Antwort auf die Seite enthalten sind. Das Dropdown-Menü enthält nur Datenströme, für die die Zielkonfiguration aktiviert ist. Weitere Details finden Sie unter [Konfigurieren eines Datenstroms](../../../datastreams/overview.md).

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für die [!DNL Commerce] Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Profile und Zielgruppen für Profilanfrageziele aktivieren](../../ui/activate-edge-personalization-destinations.md) Anweisungen zum Aktivieren von Zielgruppen für die [!DNL Commerce] Ziel.

## Nächste Schritte in [!DNL Adobe Commerce]

Nachdem Sie die [!DNL Commerce] Ziel innerhalb von Experience Platform, müssen Sie die [!DNL Audience Activation] Erweiterung in [!DNL Commerce] und konfigurieren Sie die [!DNL Commerce Admin] , um die von Ihnen erstellten Real-Time CDP-Zielgruppen zu importieren. Weitere Informationen finden Sie in der [[!DNL Commerce] Dokumentation](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html).

## Validieren von Zielgruppen-Aktivierung in Commerce {#exported-data}

Nachdem Sie Real-Time CDP-Zielgruppen für Ihre [!DNL Adobe Commerce] -Konto verwenden, werden diese Zielgruppen angezeigt, wenn Sie zum _Admin_ Seitenleiste, dann zu **[!UICONTROL Kunden]** > **[!UICONTROL Real-Time CDP Audience]**.

![Dashboard für Real-Time CDP-Zielgruppen](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
