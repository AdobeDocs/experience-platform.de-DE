---
title: Adobe Commerce Source Connector
description: Erfahren Sie, wie Sie Ihre Commerce-Daten mit der Adobe Commerce-Quelle an Experience Platform übertragen.
last-substantial-update: 2023-12-13T00:00:00Z
exl-id: 8313e3d5-5c3d-448c-883c-b9386dbbb2f5
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Adobe Commerce

Adobe Commerce ist eine agile B2B- und B2C-Commerce-Plattform, die es Händlern und Marken ermöglicht, durch kundenorientierte digitale Commerce-Erlebnisse in Online- und physischen Räumen Umsätze zu steigern.

Adobe Experience Platform-Quellen unterstützen die Integration von Adobe Commerce, damit Händler Storefront- und Backoffice-Daten an Experience Platform Edge Network senden können, damit andere Adobe Experience Cloud-Produkte wie Adobe Analytics und Adobe Target [!DNL Commerce] verwenden können.

* **Storefront-Ereignisse**: Erfassen Sie Kundeninteraktionen wie `View Page`, `View Product` und `Add to Cart`. Für B2B-Händler erfassen Storefront-Ereignisse auch [Anforderungslisten](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html?lang=de).
* **Back-Office-Ereignisse**: Erfassen Sie Informationen zum Status einer Bestellung, z. B. ob eine Bestellung aufgegeben, storniert, zurückerstattet, versendet oder abgeschlossen wurde.

>[!NOTE]
>
>Die in Adobe Commerce erfassten Daten enthalten keine personenbezogenen Daten (PII). Alle Benutzerkennungen wie Cookie-IDs und IP-Adressen werden streng anonymisiert.

## Voraussetzungen

Um Adobe Commerce mit Experience Platform zu verbinden, benötigen Sie Folgendes:

* Adobe Commerce 2.4.3 oder neuer.
* Eine gültige Adobe ID und Organisations-ID.
* Zugriff auf die [Adobe Client-Datenschicht-Erweiterung](../../../tags/extensions/client/client-data-layer/overview.md). Diese Erweiterung ist erforderlich, um Storefront-Ereignisdaten zu erfassen.
* Berechtigungen für andere Adobe DX-Produkte.

## Onboarding-Schritte

Um Ihr Adobe Commerce-Quellkonto vollständig zu integrieren, führen Sie die unten beschriebenen Schritte zusammen mit der entsprechenden Dokumentation aus.

* [Installieren der  [!DNL Data Connection] -Erweiterung](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/install.html?lang=de) für Adobe Commerce. Sie können die Connector-Erweiterung vom [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html) herunterladen.
* Nachdem Sie die Connector-Erweiterung erfolgreich installiert haben, melden Sie sich bei Ihrem Adobe-Konto in Experience Cloud an und [bestätigen Sie Ihre Organisations-ID](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=de#concept_EA8AEE5B02CF46ACBDAD6A8508646255). Diese ID ist mit Ihrem bereitgestellten Experience Cloud-Unternehmen verknüpft. Sie ist als 24-stellige alphanumerische Zeichenfolge formatiert und enthält eine obligatorische `@AdobeOrg`.
* Erstellen oder aktualisieren Sie anschließend Ihr Experience-Datenmodell (XDM)-Schema mit Ihren Commerce-spezifischen Feldergruppen. Ausführliche Anweisungen zum Hinzufügen von Commerce-spezifischen Feldergruppen zu Ihrem XDM-Schema finden Sie im Handbuch unter [Hinzufügen von Feldergruppen zu einem XDM-Schema](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html?lang=de).
* Nachdem Ihr Schema konfiguriert wurde, müssen Sie einen Datensatz erstellen, der auf Ihrem neuen Schema basiert. Dieser Datensatz enthält dann die [!DNL Commerce] Daten, die Sie senden. Ausführliche Anweisungen zum Erstellen eines Datensatzes für [!DNL Commerce] Daten finden Sie im Handbuch unter [Senden von Daten an Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=de#create-a-dataset).
* Erstellen Sie als Nächstes einen Datenstrom und wählen Sie das XDM-Schema aus, das Ihre Commerce-spezifischen Feldergruppen enthält. Weitere Informationen zu Datenströmen finden Sie unter [Datenströme - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=de).
* Anschließend müssen Sie Ihre Adobe Commerce-Instanz mit dem [Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html?lang=de) verbinden. Dadurch kann Ihre Commerce-Instanz als SaaS (Software as a Service) bereitgestellt werden.
* Nachdem alle oben genannten Konfigurationen abgeschlossen sind, können Sie jetzt eine Verbindung zu Experience Platform herstellen, indem Sie sowohl den Commerce Services Connector als auch die [!DNL Data Connection] mithilfe der [!DNL Commerce Admin] konfigurieren. Weitere Informationen zu diesem letzten Schritt finden Sie im Handbuch unter [Verbinden von Commerce-Daten mit Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/connect-data.html?lang=de).
