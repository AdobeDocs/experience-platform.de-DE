---
description: Das Adobe Experience Platform Destination SDK umfasst eine Reihe von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster für Experience Platform konfigurieren können, um Zielgruppen- und Profildaten basierend auf den von Ihnen ausgewählten Daten- und Authentifizierungsformaten an Ihren Endpunkt zu senden. Die Konfigurationen werden in Experience Platform gespeichert und können über eine API für zusätzliche Aktualisierungen abgerufen werden.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: c207b6700a31c59b00af6d55264c7a345219d999
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Experience Platform Destination SDK

## Übersicht {#destinations-sdk}

Das Adobe Experience Platform Destination SDK ist eine Suite von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster für Experience Platform konfigurieren können, um Zielgruppen- und Profildaten basierend auf den von Ihnen ausgewählten Daten- und Authentifizierungsformaten an Ihren Endpunkt zu senden. Die Konfigurationen werden in Experience Platform gespeichert und können über eine API für zusätzliche Aktualisierungen abgerufen werden.

Die Dokumentation zum Destination SDK enthält Anweisungen dazu, wie Sie mit dem Adobe Experience Platform Destination SDK eine produktive Zielintegration mit Adobe Experience Platform konfigurieren, testen und veröffentlichen und Ihr Ziel in den ständig wachsenden Zielkatalog integrieren können.

![Zielkatalog – Übersicht](./assets/destinations-catalog-overview.png)

## Produktdefinierte und benutzerdefinierte Integrationen {#productized-custom-integrations}

Als Destination SDK-Partner können Sie von der Hinzufügung Ihres produktspezifischen Ziels zum [Experience Platform-Katalog](/help/destinations/catalog/overview.md) profitieren:
1. Standardisieren Sie die Integrationskonfigurationen für alle Kunden mit vorkonfigurierten Parametern und vereinfachen Sie die Einrichtung für Kunden.
2. Stellen Sie im Zielkatalog von Experience Platform eine Zielkarte mit Branding vor, um die Einrichtung und den Bekanntheitsgrad für Kunden zu vereinfachen.
3. Lassen Sie sich als produktbezogene Zielintegration mit Adobe Experience Platform und Real-time Customer Data Platform vorstellen.

Als Experience Platform-Kunde können Sie ein eigenes benutzerdefiniertes Ziel erstellen, das Ihren Aktivierungsanforderungen am besten entspricht.

![Visuelles Diagramm zum Destination SDK](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## Unterstützte Integrationstypen {#supported-integration-types}

Durch das Destination SDK unterstützt Adobe Experience Platform Echtzeit-Integrationen mit Zielen mit einem REST-API-Endpunkt. Die Echtzeit-Integration mit Experience Platform unterstützt Funktionen wie:
* Nachrichtenumwandlung und -aggregation
* Profilaufstockung
* Konfigurierbare Metadatenintegration zum Initialisieren der Zielgruppen-Einrichtung und der Datenübertragung
* Konfigurierbare Authentifizierung
* Eine Suite von Test- und Validierungs-APIs zum Testen und Iterieren Ihrer Zielkonfigurationen

Informationen zu den technischen Anforderungen auf der Zielseite finden Sie im Artikel [Integrationsvoraussetzungen](./integration-prerequisites.md).

## Zugriff auf das Destination SDK {#get-access}

Der Zugriff auf die Destination SDK variiert je nach Ihrem Status als Partner oder Experience Platform, Real-Time CDP-Kunde. Weiterführende Informationen finden Sie in der folgenden Tabelle.


| Art des Partners oder Kunden | Zugriff auf das Destination SDK |
---------|----------|
| Unabhängiger Software-Anbieter (ISV) | Werden Sie Mitglied im [Adobe Exchange-Programm](https://partners.adobe.com/exchangeprogram/experiencecloud.html) und beantragen Sie die Bereitstellung einer Experience Platform-Sandbox für den Zugriff auf das Destination SDK. |
| Systemintegrator (SI) | Sie müssen entweder den Gold- oder Platin-Status im [Adobe-Lösungspartner-Programm](https://solutionpartners.adobe.com/home.html) erreicht haben, um eine Experience Platform-Sandbox und Zugriff auf das Destination SDK zu erhalten. |
| Experience Platform-Kunde mit dem [Aktivierungspaket](https://helpx.adobe.com/de/legal/product-descriptions/adobe-experience-platform0.html) | Sie erhalten standardmäßig Zugriff auf Experience Platform-Sandboxes und das Destination SDK. <br> Sie erhalten außerdem Zugriff auf alle erstellten Ziele, die von anderen Unternehmen mithilfe von Destination SDK konfiguriert und in Experience Platform-Unternehmen veröffentlicht wurden. |
| Experience Platform-Kunde auf der [Real-Time CDP Ultimate-Package](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) | Sie erhalten standardmäßig Zugriff auf Experience Platform-Sandboxes und das Destination SDK. <br> Sie erhalten außerdem Zugriff auf alle erstellten Ziele, die von anderen Unternehmen mithilfe von Destination SDK konfiguriert und in Experience Platform-Unternehmen veröffentlicht wurden. |

{style=&quot;table-layout:auto&quot;}

## Allgemeine Vorgehensweise {#process}

Der Prozess zum Konfigurieren Ihres Ziels in Experience Platform ist unten beschrieben:

1. Wenn Sie ein ISV oder SI sind, lesen Sie die Informationen zum Abrufen von Zugriffsinformationen im Abschnitt oben. [Adobe Experience Platform Activation](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html)-Kunden können diesen Schritt überspringen.
2. [Fordern Sie die Bereitstellung einer Experience Platform-Sandbox an](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) und aktivieren Sie die Authoring-Berechtigung für das Ziel.
3. Erstellen Sie Ihre Integration. Befolgen Sie die Anweisungen in der Produktdokumentation, um [Streaming-Ziele](./configure-destination-instructions.md) oder [dateibasierte Ziele (Beta)](./configure-file-based-destination-instructions.md).
4. Testen Sie Ihre Integration. Befolgen Sie zum Testen die Anweisungen in der Produktdokumentation [Streaming-Ziele](./test-destination.md) oder [dateibasierte Ziele (Beta)](./file-based-destination-testing-overview.md).
5. Wenn Sie eine ISV oder SI sind, erstellen Sie eine [produktive Integration](./overview.md#productized-custom-integrations), [Integration übermitteln](./submit-destination.md) für die Überprüfung durch die Adobe (die standardmäßige Antwortzeit beträgt fünf Werktage).
6. Wenn Sie ein ISV oder SI sind und eine angepasste Integration erstellen, verwenden Sie den [Self-Service-Dokumentationsprozess](./docs-framework/documentation-instructions.md), um eine Produktdokumentationsseite auf Experience League für Ihr Ziel zu erstellen.
7. Bei produktiven Integrationen wird Ihre Integration nach Genehmigung durch Adobe im [Experience Platform Katalog](/help/destinations/catalog/overview.md).
8. Wenn Sie Ihre Integration aktualisieren möchten, gehen Sie genauso vor.

## Referenz {#reference}

Adobe empfiehlt, die folgende Dokumentation zu Experience Platform zu lesen und zu verstehen:

* [Adobe Experience Platform-Ziele – Übersicht](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=de)
* [Grundlagen der XDM-Schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=de)
* [Übersicht zu Identitäts-Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de)
