---
title: Adobe Commerce-Ziel-Connector
description: Erfahren Sie, wie Händler mit Adobe Commerce und Real-Time CDP das Einkaufserlebnis personalisieren können, indem sie hochrelevante Site-Inhalte und Sonderangebote bereitstellen, die auf in Real-Time CDP erstellte und verwaltete Zielgruppen zugeschnitten sind.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 36%

---

# Adobe Commerce-Verbindung {#adobe-commerce}

## Überblick {#overview}

Verwenden Sie den [!DNL Adobe Commerce]-Ziel-Connector , um eine oder mehrere [!DNL Real-Time CDP] Audiences auszuwählen, die Sie in Ihrem [!DNL Adobe Commerce]-Konto aktivieren, um Ihren Kundinnen und Kunden ein dynamisches, personalisiertes Erlebnis zu bieten. Innerhalb von [!DNL Adobe Commerce] können Sie dann diese [!DNL Real-Time CDP] Audiences auswählen, um einzigartige Angebote im Warenkorb zu personalisieren, wie beispielsweise „Kaufen Sie zwei, erhalten Sie eins gratis“. Sie können auch Hero-Banner anzeigen und die Produktpreise durch Werbeangebote ändern, die alle an Adobe [!DNL Real-Time CDP] Zielgruppen angepasst sind.

## Voraussetzungen {#prerequisites}

Dieser Connector ist im Zielkatalog für Kundinnen und Kunden verfügbar, die [!DNL Real-Time CDP] Prime oder Ultimate und Adobe Commerce erworben haben.

Um diese Zielverbindung zu verwenden, stellen Sie sicher, dass Sie Zugriff haben auf:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/). Mit Zugriff auf die Entwicklerkonsole können Sie Informationen zu Service-Konten und Anmeldedaten anzeigen, die zum [&#x200B; (Abschließen der Konfiguration](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html?lang=de#configure-the-extension) der Erweiterung in Adobe Commerce erforderlich sind.
- [Adobe Commerce-Version 2.4.4 oder höher](https://business.adobe.com/de/products/commerce.html)

Erstellen Sie in Experience Platform Folgendes:

- [Schema](../../../xdm/schema/composition.md). Das Schema, das Sie erstellen, repräsentiert die Daten, die Sie aus Adobe Commerce aufnehmen möchten. [Erfahren Sie mehr](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html?lang=de) darüber, wie man ein Schema erstellt, das Commerce-spezifische Feldergruppen enthält.
- [Datensatz](../../../catalog/datasets/user-guide.md#create). Ein Datensatz ist ein Speicher- und Verwaltungskonstrukt für eine Sammlung von Daten. Sie erstellen diesen Datensatz aus dem Schema, das Sie oben erstellt haben.
- [Datenstrom](../../../datastreams/configure.md#create). ID, die den Datenfluss von [!DNL Adobe Experience Platform] zu anderen Adobe DX-Produkten ermöglicht. Diese ID muss mit einer bestimmten Website in Ihrer jeweiligen Adobe Commerce-Instanz verknüpft sein. Wenn Sie diesen Datenstrom erstellen, geben Sie das von Ihnen oben erstellte XDM-Schema an.

Nachdem Sie die Voraussetzungen erfüllt haben, stellen Sie eine Verbindung mit dem Ziel [!DNL Commerce] her.

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Alle anderen Ursprünge der Zielgruppe | Ja | Diese Kategorie enthält alle Ursprünge der Zielgruppe außerhalb der Zielgruppen, die durch die [!DNL Segmentation Service] generiert wurden. Lesen Sie mehr über [verschiedene Ursprünge von Audiences](/help/segmentation/ui/audience-portal.md#customize). Einige Beispiele: <ul><li> benutzerdefinierte Upload-Zielgruppen [importiert](../../../segmentation/ui/audience-portal.md#import-audience) aus CSV-Dateien in Experience Platform,</li><li> Lookalike-Zielgruppen, </li><li> Federated Audiences, </li><li> Zielgruppen, die in anderen Experience Platform-Apps generiert werden, z. B. [!DNL Adobe Journey Optimizer], </li><li> und mehr. </li></ul> |

{style="table-layout:auto"}



Unterstützte Zielgruppen nach Zielgruppen-Datentyp:

| Datentyp der Zielgruppe | Unterstützt | Beschreibung | Anwendungsfälle |
|--------------------|-----------|-------------|-----------|
| [Personen-Zielgruppen](/help/segmentation/types/people-audiences.md) | Ja | Basierend auf Kundenprofilen können Sie bestimmte Personengruppen für Marketing-Kampagnen ansprechen. | Häufige Käufer, Warenkorbabbrüche |
| [Konto-Zielgruppen](/help/segmentation/types/account-audiences.md) | Nein | Targeting von Personen in bestimmten Organisationen für Account-basierte Marketing-Strategien. | B2B-Marketing |
| [Interessenten-Zielgruppen](/help/segmentation/types/prospect-audiences.md) | Nein | Targeting von Personen, die noch keine Kunden sind, aber Merkmale mit Ihrer Zielgruppe teilen. | Akquise mit Drittanbieterdaten |
| [Datensatzexporte](/help/catalog/datasets/overview.md) | Nein | Sammlungen strukturierter Daten, die im Data Lake von [!DNL Adobe Experience Platform] gespeichert sind. | Reporting, Datenwissenschaft-Workflows |

{style="table-layout:auto"}


## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. &#x200B;](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

So stellen Sie eine Verbindung mit dem Ziel [!DNL Adobe Commerce] her:

1. Wechseln Sie in der [Experience Platform](https://experience.adobe.com/platform/)Benutzeroberfläche zu **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
1. Wählen Sie **[!UICONTROL Personalization]** aus.
1. Wählen Sie das Adobe Commerce-Ziel aus, um es zu markieren, und wählen Sie dann **[!UICONTROL Set up]** aus.
1. Führen Sie die im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschriebenen Schritte aus.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

- **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
- **[!UICONTROL Description]**: Geben Sie eine Beschreibung für Ihr Ziel ein. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden. Dieses Feld ist optional.
- **[!UICONTROL Integration alias]**: Dieser Wert wird als JSON-Objektname an den Experience Platform Web SDK gesendet.
- **[!UICONTROL Datastream ID]**: Dadurch wird bestimmt, welcher Datenerfassungs-Datenstrom die Zielgruppen enthält, die in der Antwort auf die Seite enthalten sind. Das Dropdown-Menü enthält nur Datenströme, für die die Zielkonfiguration aktiviert ist. Weitere Details finden Sie unter [Konfigurieren eines Datenstroms](../../../datastreams/overview.md).

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für das [!DNL Commerce] {#activate}

>[!IMPORTANT]
>
>Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen [&#x200B; Aktivieren von Zielgruppen für das &#x200B;](../../ui/activate-edge-personalization-destinations.md)-Ziel finden Sie [!DNL Commerce]Aktivieren von Profilen und Zielgruppen für Profilanfrageziele“.

## Nächste Schritte in [!DNL Adobe Commerce] {#next-steps-adobe-commerce}

Nachdem Sie das [!DNL Commerce] Ziel in Experience Platform konfiguriert haben, müssen Sie die [!DNL Audience Activation] in [!DNL Commerce] installieren und den [!DNL Commerce Admin] konfigurieren, um die von Ihnen erstellten [!DNL Real-Time CDP]-Zielgruppen zu importieren. Weitere Informationen finden Sie in der [[!DNL Commerce] Dokumentation](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html?lang=de).

## Validieren von Zielgruppen-Aktivierung in Commerce {#exported-data}

Nachdem Sie [!DNL Real-Time CDP] Zielgruppen für Ihr [!DNL Adobe Commerce]-Konto aktiviert haben, sehen Sie diese Zielgruppen, wenn Sie zur Seitenleiste _Admin_ navigieren und dann zu **[!UICONTROL Customers]** > **[!UICONTROL Real-Time CDP Audience]** gehen.

![Real-Time CDP-Zielgruppen-Dashboard](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
