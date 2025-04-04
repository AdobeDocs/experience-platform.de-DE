---
title: Adobe Commerce-Ziel-Connector
description: Erfahren Sie, wie Händler mit Adobe Commerce und Real-Time CDP das Einkaufserlebnis personalisieren können, indem sie hochrelevante Site-Inhalte und Sonderangebote bereitstellen, die auf in Real-Time CDP erstellte und verwaltete Zielgruppen zugeschnitten sind.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 52%

---

# Adobe Commerce-Verbindung {#adobe-commerce}

## Überblick {#overview}

Mit dem [!DNL Adobe Commerce]-Ziel-Connector können Sie eine oder mehrere Real-Time CDP-Zielgruppen auswählen, die Sie in Ihrem [!DNL Adobe Commerce] aktivieren, um Ihren Kunden ein dynamisches, personalisiertes Erlebnis zu bieten. Innerhalb von [!DNL Adobe Commerce] können Sie dann diese Real-Time CDP-Zielgruppen auswählen, um einzigartige Angebote im Warenkorb zu personalisieren, wie beispielsweise „Kaufen Sie zwei, erhalten Sie eins gratis“. Sie können auch Hero-Banner anzeigen und die Produktpreise durch Werbeangebote ändern, die alle an Adobe Real-Time CDP-Zielgruppen angepasst sind.

## Voraussetzungen {#prerequisites}

Dieser Connector ist im Zielkatalog für Kundinnen und Kunden verfügbar, die Real-Time CDP Prime oder Ultimate und Adobe Commerce erworben haben.

Um diese Zielverbindung zu verwenden, stellen Sie sicher, dass Sie Zugriff haben auf:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/). Mit Zugriff auf die Entwicklerkonsole können Sie Informationen zu Service-Konten und Anmeldedaten anzeigen, die zum [ (Abschließen der Konfiguration](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html#configure-the-extension) der Erweiterung in Adobe Commerce erforderlich sind.
- [Adobe Commerce Cloud-Version 2.4.4 oder höher](https://business.adobe.com/de/products/magento/magento-commerce.html)

Erstellen Sie in Experience Platform Folgendes:

- [Schema](../../../xdm/schema/composition.md). Das Schema, das Sie erstellen, repräsentiert die Daten, die Sie aus Adobe Commerce aufnehmen möchten. [Erfahren Sie mehr](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html) darüber, wie man ein Schema erstellt, das Commerce-spezifische Feldergruppen enthält.
- [Datensatz](../../../catalog/datasets/user-guide.md#create). Ein Datensatz ist ein Speicher- und Verwaltungskonstrukt für eine Sammlung von Daten. Sie erstellen diesen Datensatz aus dem Schema, das Sie oben erstellt haben.
- [Datenstrom](../../../datastreams/overview.md#create). ID, die den Datenfluss von Adobe Experience Platform zu anderen Adobe-DX-Produkten ermöglicht. Diese ID muss mit einer bestimmten Website in Ihrer jeweiligen Adobe Commerce-Instanz verknüpft sein. Wenn Sie diesen Datenstrom erstellen, geben Sie das von Ihnen oben erstellte XDM-Schema an.

Nachdem Sie die Voraussetzungen erfüllt haben, stellen Sie eine Verbindung mit dem Ziel [!DNL Commerce] her.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

So stellen Sie eine Verbindung mit dem Ziel [!DNL Adobe Commerce] her:

1. Experience Platform Wechseln Sie in der ](https://experience.adobe.com/platform/) von [zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**.
1. Wählen Sie **[!UICONTROL Personalisierung]** aus.
1. Wählen Sie das Adobe Commerce-Ziel aus, um es zu markieren, und wählen Sie dann **[!UICONTROL Einrichten]** aus.
1. Führen Sie die im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschriebenen Schritte aus.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

- **[!UICONTROL Name]**: Geben Sie den gewünschten Namen für das Ziel ein.
- **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für das Ziel ein. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden. Dieses Feld ist optional.
- **[!UICONTROL Integrationsalias]**: Dieser Wert wird als JSON-Objektname an das Experience Platform Web SDK gesendet.
- **[!UICONTROL Datenstrom-ID]**: Dadurch wird bestimmt, welcher Datenerfassungsdatenstrom die Zielgruppen enthält, die in der Antwort auf die Seite enthalten sind. Das Dropdown-Menü enthält nur Datenströme, für die die Zielkonfiguration aktiviert ist. Weitere Details finden Sie unter [Konfigurieren eines Datenstroms](../../../datastreams/overview.md).

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für das [!DNL Commerce] {#activate}

>[!IMPORTANT]
> 
>Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen [ Aktivieren von Zielgruppen für das [!DNL Commerce]-Ziel finden Sie ](../../ui/activate-edge-personalization-destinations.md)Aktivieren von Profilen und Zielgruppen für Profilanfrageziele“.

## Nächste Schritte in [!DNL Adobe Commerce]

Nachdem Sie das [!DNL Commerce] Ziel in Experience Platform konfiguriert haben, müssen Sie die [!DNL Audience Activation] in [!DNL Commerce] installieren und den [!DNL Commerce Admin] konfigurieren, um die von Ihnen erstellten Real-Time CDP-Zielgruppen zu importieren. Weitere Informationen finden Sie in der [[!DNL Commerce] Dokumentation](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html).

## Validieren von Zielgruppen-Aktivierung in Commerce {#exported-data}

Nachdem Sie Real-Time CDP-Zielgruppen für Ihr [!DNL Adobe Commerce]-Konto aktiviert haben, sehen Sie diese Zielgruppen, wenn Sie zur Seitenleiste _Admin_ gehen und dann zu **[!UICONTROL Kunden]** > **[!UICONTROL Real-Time CDP-Zielgruppe]**.

![Real-Time CDP-Zielgruppen-Dashboard](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
