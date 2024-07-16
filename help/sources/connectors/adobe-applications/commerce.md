---
title: Adobe Commerce Source Connector
description: Erfahren Sie, wie Sie mit der Adobe Commerce-Quelle Ihre Commerce-Daten an Experience Platform übermitteln können.
last-substantial-update: 2023-12-13T00:00:00Z
exl-id: 8313e3d5-5c3d-448c-883c-b9386dbbb2f5
source-git-commit: 506f33e03dea5d5879808bccb82948209714926a
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Adobe Commerce

Adobe Commerce ist eine agile B2B- und B2C-Commerce-Plattform, mit der Händler und Marken Umsätze durch kundenorientierte digitale Commerce-Erlebnisse über Online- und physische Bereiche hinweg beschleunigen können.

Adobe Experience Platform Sources unterstützt die Integration von Adobe Commerce, damit Händler Storefront- und Backoffice-Daten an das Experience Platform-Edge Network senden können, sodass andere Adobe Experience Cloud-Produkte wie Adobe Analytics und Adobe Target [!DNL Commerce] -Daten verwenden können.

* **Storefront-Ereignisse**: Erfassen Sie Kaufinteraktionen wie `View Page`, `View Product` und `Add to Cart`. Bei B2B-Händlern werden bei Storefront-Ereignissen auch [Anforderungslisten](<https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html>) erfasst.
* **Backoffice-Ereignisse**: Erfassen Sie Informationen zum Status einer Bestellung, z. B. ob eine Bestellung aufgegeben, storniert, rückerstattet, versandt oder abgeschlossen wurde.

>[!NOTE]
>
>Die erfassten Daten in Adobe Commerce enthalten keine personenbezogenen Daten (PII). Alle Benutzer-IDs wie Cookie-IDs und IP-Adressen werden streng anonymisiert.

## Voraussetzungen

Um Adobe Commerce mit Experience Platform zu verbinden, müssen Sie über Folgendes verfügen:

* Adobe Commerce 2.4.3 oder höher.
* Eine gültige Adobe ID- und Organisations-ID.
* Zugriff auf die [Adobe Client-Datenschichterweiterung](../../../tags/extensions/client/client-data-layer/overview.md). Diese Erweiterung ist erforderlich, um Storefront-Ereignisdaten zu erfassen.
* Berechtigungen für andere Adobe DX-Produkte.

## Onboarding-Schritte

Um Ihr Adobe Commerce-Quellkonto vollständig zu integrieren, führen Sie die unten beschriebenen Schritte zusammen mit der entsprechenden Dokumentation aus.

* [Installieren Sie die  [!DNL Data Connection] Erweiterung](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/install.html) für Adobe Commerce. Sie können die Connector-Erweiterung von [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html) herunterladen.
* Nachdem Sie die Connector-Erweiterung erfolgreich installiert haben, melden Sie sich bei Ihrem Adobe-Konto unter Experience Cloud an und [bestätigen Sie Ihre Organisations-ID](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255). Diese ID ist mit Ihrem bereitgestellten Experience Cloud-Unternehmen verknüpft. Sie ist als 24-stellige alphanumerische Zeichenfolge formatiert und enthält den obligatorischen Wert `@AdobeOrg`.
* Als Nächstes erstellen oder aktualisieren Sie Ihr Experience-Datenmodell (XDM)-Schema mit Ihren Commerce-spezifischen Feldergruppen. Ausführliche Anweisungen zum Hinzufügen Commerce-spezifischer Feldergruppen zu Ihrem XDM-Schema finden Sie im Handbuch zum Hinzufügen von Feldergruppen zu einem XDM-Schema [.](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html)
* Nachdem Ihr Schema konfiguriert wurde, müssen Sie einen Datensatz erstellen, der auf Ihrem neuen Schema basiert. Dieser Datensatz enthält dann die von Ihnen gesendeten [!DNL Commerce] -Daten. Detaillierte Anweisungen zum Erstellen eines Datensatzes für [!DNL Commerce] -Daten finden Sie im Handbuch zum [Senden von Daten an Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset).
* Erstellen Sie anschließend einen Datastream und wählen Sie das XDM-Schema aus, das Ihre Commerce-spezifischen Feldgruppen enthält. Weiterführende Informationen zu Datastreams finden Sie in der [Übersicht über Datastreams](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=de) .
* Anschließend müssen Sie Ihre Adobe Commerce-Instanz mit dem [Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html) verbinden. Dadurch kann Ihre Commerce-Instanz als SaaS (Software as a Service) bereitgestellt werden.
* Nachdem alle oben genannten Konfigurationen abgeschlossen sind, können Sie jetzt eine Verbindung zu Experience Platform herstellen, indem Sie sowohl den Commerce Services Connector als auch die Erweiterung [!DNL Data Connection] mit dem [!DNL Commerce Admin] konfigurieren. Weitere Informationen zu diesem letzten Schritt finden Sie im Handbuch zum [Verbinden von Commerce-Daten mit Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/connect-data.html).
