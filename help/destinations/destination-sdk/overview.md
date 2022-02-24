---
description: Adobe Experience Platform Destination SDK ist ein Satz von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster konfigurieren können, damit Experience Platform Zielgruppen- und Profildaten basierend auf Daten- und Authentifizierungsformaten Ihrer Wahl an Ihren Endpunkt senden kann. Die Konfigurationen werden in Experience Platform gespeichert und können über eine API für zusätzliche Aktualisierungen abgerufen werden.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 85b308b3f92a734fed0c885a574b71fa05684bb4
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 14%

---

# Adobe Experience Platform Destination SDK

## Übersicht {#destinations-sdk}

Das Adobe Experience Platform Destination SDK ist eine Suite von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster für Experience Platform konfigurieren können, um Zielgruppen- und Profildaten basierend auf den von Ihnen ausgewählten Daten- und Authentifizierungsformaten an Ihren Endpunkt zu senden. Die Konfigurationen werden in Experience Platform gespeichert und können über eine API für zusätzliche Aktualisierungen abgerufen werden.

Die Dokumentation zur Destination SDK enthält Anweisungen dazu, wie Sie mit dem Adobe Experience Platform Destination SDK eine produktive Zielintegration mit Adobe Experience Platform konfigurieren, testen und veröffentlichen und Ihr Ziel in den ständig wachsenden Zielkatalog integrieren können.

![Zielkatalog – Übersicht](./assets/destinations-catalog-overview.png)

## Produktdefinierte und benutzerdefinierte Integrationen {#productized-custom-integrations}

Als Partner der Destination SDK können Sie von der Hinzufügung Ihres produktisierten Ziels zum [Experience Platform Katalog](/help/destinations/catalog/overview.md):
1. Standardisieren Sie die Integrationskonfigurationen für alle Kunden mit vorkonfigurierten Parametern und vereinfachen Sie das Setup-Erlebnis für Kunden.
2. Stellen Sie im Zielkatalog der Experience Platform eine Zielkarte mit Branding vor, um die Kundeneinrichtung und das Kundenbewusstsein zu vereinfachen.
3. Werden Sie als produktive Zielintegration mit Adobe Experience Platform und Real-time Customer Data Platform vorgestellt.

Als Experience Platform-Kunde können Sie ein eigenes benutzerdefiniertes Ziel erstellen, das Ihren Aktivierungsanforderungen am besten entspricht.

![Visuelles Diagramm zur Destination SDK](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## Unterstützte Integrationstypen {#supported-integration-types}

Durch Destination SDK unterstützt Adobe Experience Platform Echtzeit-Integrationen mit Zielen mit einem REST-API-Endpunkt. Die Echtzeit-Integration mit Experience Platform unterstützt Funktionen wie:
* Nachrichtenumwandlung und -aggregation
* Profilaufstockung
* Konfigurierbare Metadatenintegration zum Initialisieren der Zielgruppen-Einrichtung und der Datenübertragung
* Konfigurierbare Authentifizierung
* Eine Suite von Test- und Validierungs-APIs zum Testen und Iterieren Ihrer Zielkonfigurationen

Informationen zu den technischen Anforderungen auf der Zielseite finden Sie im Abschnitt [Integrationsvoraussetzungen](./integration-prerequisites.md) Artikel.


## Zugriff auf Destination SDK erhalten {#get-access}

Der Zugriff auf die Destination SDK hängt von Ihrem Status als Partner oder Experience Platform ab. Weitere Informationen finden Sie in der unten stehenden Tabelle.


| Art des Partners oder Kunden | Zugriff auf die Destination SDK |
---------|----------|
| Unabhängiger Software-Anbieter (ISV) | Mitglied werden [Adobe Exchange-Programm](https://partners.adobe.com/exchangeprogram/experiencecloud.html) und fordern Sie die Bereitstellung einer Experience Platform-Sandbox für den Zugriff auf die Destination SDK an. |
| Systemintegrator (SI) | Sie müssen entweder auf Gold- oder auf Platinebene im [Adobe Solution Partner Program](https://solutionpartners.adobe.com/home.html)und Sie erhalten eine Experience Platformen-Sandbox und Zugriff auf die Destination SDK. |
| Experience Platform-Kunde auf der [Aktivierungspaket](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) | Standardmäßig erhalten Sie Zugriff auf Experience Platform-Sandboxes und Destination SDK. |
| Experience Platform-Kunde auf der [Echtzeit-CDP-Paket](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | Sie haben keinen Zugriff auf Destination SDK, aber Sie haben Zugriff auf alle erstellten Ziele, die von anderen Unternehmen mithilfe von Destination SDK konfiguriert und in Experience Platform-Organisationen veröffentlicht wurden. |

{style=&quot;table-layout:auto&quot;}

## Verfahren auf hoher Ebene {#process}

Der Prozess zum Konfigurieren Ihres Ziels in Experience Platform ist unten beschrieben:

1. Wenn Sie ISV oder SI sind, lesen Sie die Informationen zum Abrufen von Zugriffsinformationen im Abschnitt oben. [Adobe Experience Platform Activation](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) -Kunden können diesen Schritt überspringen.
2. [Anforderung der Bereitstellung einer Experience Platform-Sandbox](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) und aktivieren Sie die Authoring-Berechtigung für das Ziel.
3. [Integration erstellen](./configure-destination-instructions.md) der Produktdokumentation folgen.
4. [Integration testen](./test-destination.md) der Produktdokumentation folgen.
5. [Einreichen der Integration](./submit-destination.md) für die Überprüfung durch die Adobe (die standardmäßige Antwortzeit beträgt 5 Werktage).
6. Wenn Sie eine ISV oder SI sind, erstellen Sie eine [produktive Integration](./overview.md#productized-custom-integrations), verwenden Sie die [Self-Service-Dokumentationsprozess](./docs-framework/documentation-instructions.md) , um eine Produktdokumentationsseite auf der Experience League für Ihr Ziel zu erstellen.
7. Sobald die Integration von Adobe genehmigt wurde, wird sie im [Experience Platform Katalog](/help/destinations/catalog/overview.md).
8. Wenn Sie Ihre Integration aktualisieren möchten, gehen Sie genauso vor.

## Referenz {#reference}

Adobe empfiehlt, die folgende Dokumentation zur Experience Platform zu lesen und zu verstehen:

* [Adobe Experience Platform-Ziele - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [Grundlage der XDM-Schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=de)
* [Übersicht zu Identitäts-Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de)
