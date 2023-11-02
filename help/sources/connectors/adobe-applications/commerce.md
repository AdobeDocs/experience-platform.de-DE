---
title: Adobe Commerce Source Connector
description: Erfahren Sie, wie Sie mit der Adobe Commerce-Quelle Ihre Commerce-Daten an Experience Platform übermitteln können.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 8313e3d5-5c3d-448c-883c-b9386dbbb2f5
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 5%

---

# Adobe Commerce

Adobe Commerce ist eine agile B2B- und B2C-Commerce-Plattform, mit der Händler und Marken Umsätze durch kundenorientierte digitale Commerce-Erlebnisse über Online- und physische Bereiche hinweg beschleunigen können.

Adobe Experience Platform Sources unterstützt die Integration von Adobe Commerce, damit Händler Storefront- und Backoffice-Daten an das Experience Platform Edge Network senden können, sodass andere Adobe Experience Cloud-Produkte wie Adobe Analytics und Adobe Target verwenden können [!DNL Commerce] Daten.

* **Storefront-Ereignisse**: Erfassen Sie Kundeninteraktionen wie `View Page`, `View Product`, und `Add to Cart`. Für B2B-Händler werden auch Storefront-Ereignisse erfasst [Anforderungslisten](<https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html>).
* **Back-Office-Ereignisse**: Erfassen Sie Informationen zum Status einer Bestellung, z. B. ob eine Bestellung aufgegeben, storniert, rückerstattet, versandt oder abgeschlossen wurde.

>[!NOTE]
>
>Die erfassten Daten in Adobe Commerce enthalten keine personenbezogenen Daten (PII). Alle Benutzer-IDs wie Cookie-IDs und IP-Adressen werden streng anonymisiert.

## Voraussetzungen

Um Adobe Commerce mit Experience Platform zu verbinden, müssen Sie über Folgendes verfügen:

* Adobe Commerce 2.4.3 oder höher.
* Eine gültige Adobe ID- und Organisations-ID.
* Zugriff auf [Adobe Client-Datenschichterweiterung](../../../tags/extensions/client/client-data-layer/overview.md). Diese Erweiterung ist erforderlich, um Storefront-Ereignisdaten zu erfassen.
* Berechtigungen für andere Adobe DX-Produkte.

## Onboarding-Schritte

Um Ihr Adobe Commerce-Quellkonto vollständig zu integrieren, führen Sie die unten beschriebenen Schritte zusammen mit der entsprechenden Dokumentation aus.

* [Installieren der Experience Platform-Connector-Erweiterung](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/install.html) für Adobe Commerce. Sie können die Connector-Erweiterung von [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html).
* Nachdem Sie die Connector-Erweiterung erfolgreich installiert haben, melden Sie sich unter Experience Cloud bei Ihrem Adobe-Konto an und [Ihre Organisations-ID bestätigen](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=de#concept_EA8AEE5B02CF46ACBDAD6A8508646255). Diese ID ist mit Ihrem bereitgestellten Experience Cloud-Unternehmen verknüpft. Sie ist als 24-stellige alphanumerische Zeichenfolge formatiert und enthält eine obligatorische `@AdobeOrg`.
* Als Nächstes erstellen oder aktualisieren Sie Ihr Experience-Datenmodell (XDM)-Schema mit Ihren Commerce-spezifischen Feldergruppen. Ausführliche Anweisungen zum Hinzufügen Commerce-spezifischer Feldergruppen zu Ihrem XDM-Schema finden Sie im Handbuch unter [Hinzufügen von Feldergruppen zu einem XDM-Schema](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html?lang=de).
* Nachdem Ihr Schema konfiguriert wurde, müssen Sie einen Datensatz erstellen, der auf Ihrem neuen Schema basiert. Dieser Datensatz enthält dann die [!DNL Commerce] Daten, die Sie senden. Detaillierte Schritte zum Erstellen eines Datensatzes für [!DNL Commerce] Daten, lesen Sie das Handbuch zu [Senden von Daten an Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset).
* Erstellen Sie anschließend einen Datastream und wählen Sie das XDM-Schema aus, das Ihre Commerce-spezifischen Feldergruppen enthält. Weitere Informationen zu Datastreams finden Sie im Abschnitt [Übersicht über Datastreams](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=de).
* Anschließend müssen Sie Ihre Adobe Commerce-Instanz mit der [Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html). Dadurch kann Ihre Commerce-Instanz als SaaS (Software as a Service) bereitgestellt werden.
* Nachdem alle oben genannten Konfigurationen abgeschlossen sind, können Sie jetzt eine Verbindung zu Experience Platform herstellen, indem Sie sowohl den Commerce Services Connector als auch den Experience Platform Connector mit dem [!DNL Commerce Admin]. Weitere Informationen zu diesem letzten Schritt finden Sie im Handbuch unter [Verbinden von Commerce-Daten mit Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/connect-data.html).
