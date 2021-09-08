---
description: Das Adobe Experience Platform Destination SDK ist eine Reihe von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster für die Experience Platform konfigurieren können, um Zielgruppen- und Profildaten an Ihren Endpunkt zu senden. Dies basiert auf Daten- und Authentifizierungsformaten Ihrer Wahl. Die Konfigurationen werden in Experience Platform gespeichert und können über API für zusätzliche Aktualisierungen abgerufen werden.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 2841adc0ce212a945c35ba38209d4c00c519ad7b
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 4%

---

# Adobe Experience Platform Destination SDK

## Übersicht {#destinations-sdk}

Das Adobe Experience Platform Destination SDK ist eine Suite von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster für die Experience Platform konfigurieren können, um Zielgruppen- und Profildaten basierend auf den von Ihnen ausgewählten Daten- und Authentifizierungsformaten an Ihren Endpunkt zu senden. Die Konfigurationen werden in Experience Platform gespeichert und können über API für zusätzliche Aktualisierungen abgerufen werden.

Die Dokumentation zum Ziel-SDK enthält Anweisungen zur Verwendung des Adobe Experience Platform Destination SDK zum Konfigurieren, Testen und Veröffentlichen einer produktiven Zielintegration mit Adobe Experience Platform und dazu, dass Ihr Ziel Teil des ständig wachsenden Zielkatalogs wird.

![Zielkatalog – Übersicht](./assets/destinations-catalog-overview.png)

## Produktdefinierte und benutzerdefinierte Integrationen {#productized-custom-integrations}

Als Ziel-SDK-Partner können Sie von der Hinzufügung Ihres produktionalisierten Ziels zum [Experience Platform-Katalog](/help/destinations/catalog/overview.md) profitieren:
1. Standardisieren Sie die Integrationskonfigurationen für alle Kunden mit vorkonfigurierten Parametern und vereinfachen Sie das Setup-Erlebnis für Kunden.
2. Stellen Sie im Zielkatalog der Experience Platform eine Zielkarte mit Branding vor, um die Kundeneinrichtung und das Kundenbewusstsein zu vereinfachen.
3. Werden Sie als produktive Zielintegration in Adobe Experience Platform und die Echtzeit-Kundendatenplattform vorgestellt.

Als Experience Platform-Kunde können Sie ein eigenes benutzerdefiniertes Ziel erstellen, das Ihren Aktivierungsanforderungen am besten entspricht.

![Visuelles Ziel-SDK-Diagramm](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## Unterstützte Integrationstypen {#supported-integration-types}

Über das Ziel-SDK unterstützt Adobe Experience Platform Echtzeit-Integrationen mit Zielen mit einem REST-API-Endpunkt. Die Echtzeit-Integration mit Experience Platform unterstützt Funktionen wie:
* Nachrichtenumwandlung und -aggregation
* Profilaufstockung
* Konfigurierbare Metadatenintegration zum Initialisieren der Zielgruppen-Einrichtung und der Datenübertragung
* Konfigurierbare Authentifizierung
* Eine Suite von Test- und Validierungs-APIs zum Testen und Iterieren Ihrer Zielkonfigurationen

Lesen Sie die technischen Anforderungen auf der Seite Ziele im Artikel [Integrationsanforderungen](./integration-prerequisites.md) .


## Zugriff auf das Ziel-SDK erhalten {#get-access}

Der Ziel-SDK-Zugriff variiert je nach Ihrem Status als Partner oder Experience Platform-Kunde. Weitere Informationen finden Sie in der unten stehenden Tabelle.


| Art des Partners oder Kunden | Zugriff auf das Ziel-SDK |
---------|----------|
| Unabhängiger Software-Anbieter (ISV) | Treten Sie dem [Adobe Exchange-Programm](https://partners.adobe.com/exchangeprogram/experiencecloud.html) bei und fordern Sie auf, eine Experience Platform-Sandbox für den Zugriff auf das Destination SDK bereitzustellen. |
| Systemintegrator (SI) | Sie müssen entweder auf Gold- oder Platinebene im [Adobe Solution Partner Program](https://solutionpartners.adobe.com/home.html) sein, und Sie erhalten eine Experience Platform-Sandbox, die bereitgestellt wird, sowie Zugriff auf das Ziel-SDK. |
| Experience Platform-Kunde im Aktivierungspaket | Standardmäßig erhalten Sie Zugriff auf Experience Platform-Sandboxes und Ziel-SDK. |
| Experience Platform-Kunde im Echtzeit-CDP-Paket | Sie haben keinen Zugriff auf das Ziel-SDK, sondern Zugriff auf alle produktiven Ziele, die von anderen Unternehmen mithilfe des Ziel-SDK konfiguriert und in Experience Platform-Unternehmen veröffentlicht wurden. |

{style=&quot;table-layout:auto&quot;}

## Verfahren auf hoher Ebene {#process}

Der Prozess zum Konfigurieren Ihres Ziels in Experience Platform ist unten beschrieben:

1. Wenn Sie ISV oder SI sind, lesen Sie die Informationen zum Abrufen von Zugriffsinformationen im Abschnitt oben. [Adobe Experience Platform ](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) Activation-Kunden können diesen Schritt überspringen.
2. [Anforderung der Bereitstellung einer Experience Platform-](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) Sandbox und Aktivierung der Authoring-Berechtigung für das Ziel.
3. [Erstellen Sie Ihre ](./configure-destination-instructions.md) Integration gemäß der Produktdokumentation.
4. [Testen Sie Ihre ](./test-destination.md) Integration gemäß der Produktdokumentation.
5. [Übermitteln Sie Ihre ](./destination-publish-api.md) Integration zur Überprüfung durch Adobe (die standardmäßige Reaktionszeit beträgt 5 Werktage).
6. Wenn Sie ISV oder SI sind und eine [produktionierte Integration](./overview.md#productized-custom-integrations) erstellen, verwenden Sie den [Self-Service-Dokumentationsprozess](./docs-framework/documentation-instructions.md), um eine Produktdokumentationsseite auf der Experience League für Ihr Ziel zu erstellen.
7. Nach der Genehmigung durch Adobe wird Ihre Integration im [Experience Platform-Katalog](/help/destinations/catalog/overview.md) angezeigt.
8. Wenn Sie Ihre Integration aktualisieren möchten, gehen Sie genauso vor.

## Referenz {#reference}

Adobe empfiehlt, die folgende Dokumentation zur Experience Platform zu lesen und zu verstehen:

* [Adobe Experience Platform-Ziele - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [Grundlage der XDM-Schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=de)
* [Übersicht zu Identitäts-Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de)
