---
description: Adobe Experience Platform Destination SDK ist ein Satz von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster konfigurieren können, damit Experience Platform Zielgruppen- und Profildaten basierend auf den von Ihnen ausgewählten Daten- und Authentifizierungsformaten an Ihren Endpunkt oder Speicherort übermitteln kann. Die Konfigurationen werden in Experience Platform gespeichert und können über eine API für zusätzliche Aktualisierungen abgerufen werden.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 42%

---

# Adobe Experience Platform Destination SDK

Adobe Experience Platform Destination SDK ist eine Suite von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster für die Experience Platform konfigurieren können, um Zielgruppen- und Profildaten basierend auf den von Ihnen ausgewählten Daten- und Authentifizierungsformaten an Ihren Endpunkt oder Speicherort bereitzustellen. Die Konfigurationen werden in Experience Platform gespeichert und können über eine API für zusätzliche Aktualisierungen abgerufen werden.

Die Dokumentation zum Destination SDK enthält Anweisungen dazu, wie Sie mit dem Adobe Experience Platform Destination SDK eine produktive Zielintegration mit Adobe Experience Platform konfigurieren, testen und veröffentlichen und Ihr Ziel in den ständig wachsenden Zielkatalog integrieren können. Durch die Verwendung von Destination SDK können Sie auch Ihr eigenes benutzerdefiniertes privates Ziel erstellen, um Daten zu exportieren, die auf Ihre Anforderungen zugeschnitten sind.

![Screenshot der Experience Platform-Benutzeroberfläche mit dem Zielkatalog](assets/destinations-catalog-overview.png)

## Produktdefinierte und benutzerdefinierte Integrationen {#productized-custom-integrations}

>[!IMPORTANT]
>
> Diese Funktion zum Erstellen privater benutzerdefinierter Ziele ist nur für verfügbar. [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) -Kunden.

Als Destination SDK-Partner können Sie von der Hinzufügung Ihres produktspezifischen Ziels zum [Experience Platform-Katalog](../catalog/overview.md) profitieren:

1. Standardisieren Sie die Integrationskonfigurationen für alle Kunden mit vorkonfigurierten Parametern und vereinfachen Sie die Einrichtung für Kunden.
2. Stellen Sie im Zielkatalog von Experience Platform eine Zielkarte mit Branding vor, um die Einrichtung und den Bekanntheitsgrad für Kunden zu vereinfachen.
3. Werden Sie als produktive Zielintegration mit Adobe Experience Platform und Adobe Real-time Customer Data Platform vorgestellt.

Als Experience Platform-Kunde können Sie auch Ihr eigenes benutzerdefiniertes Ziel erstellen, das Ihren Aktivierungsanforderungen am besten entspricht.

![Übersichtsdiagramm, das zeigt, wie Zielentwickler mit Destination SDK interagieren und wie Real-Time CDP-Kunden von produktiven und privaten Zielen profitieren.](assets/destination-sdk-visual.png)

## Unterstützte Integrationstypen {#supported-integration-types}

### Echtzeit-Integrationen (Streaming) {#real-time-integrations}

Durch Destination SDK unterstützt Adobe Experience Platform Echtzeit-Integrationen (auch als Streaming bezeichnet) mit Zielen, die über einen REST-API-Endpunkt verfügen. Die Echtzeit-Integration mit Experience Platform unterstützt Funktionen wie:

* Nachrichtenumwandlung und -aggregation
* Profilaufstockung
* Konfigurierbare Metadatenintegration zum Initialisieren der Zielgruppen-Einrichtung und der Datenübertragung
* Konfigurierbare Authentifizierung
* Eine Suite von Test- und Validierungs-APIs zum Testen und Iterieren Ihrer Zielkonfigurationen

### Dateibasierte Integrationen {#file-based-integrations}

Über Destination SDK können Sie auch Integrationen einrichten, um Dateien regelmäßig an den Speicherort Ihrer Wahl zu exportieren. Die dateibasierte Integration mit Experience Platform unterstützt Funktionen wie:

* Dateiexport in verschiedenen unterstützten Formaten (CSV, Parquet, JSON)
* Konfigurierbare Dateiformatierungsoptionen, mit denen Sie das Format der exportierten Dateien entsprechend Ihren nachgelagerten Anforderungen strukturieren können.

Informationen zu den technischen Anforderungen auf der Zielseite finden Sie im Abschnitt [Integrationsvoraussetzungen](integration-prerequisites.md) Artikel und lesen Sie mehr über alle unterstützten Konfigurationen in [Konfigurationsoptionen](functionality/configuration-options.md) Artikel

## Zugriff auf das Destination SDK {#get-access}

Der Zugriff auf die Destination SDK variiert je nach Ihrem Status als Partner oder Experience Platform, Real-Time CDP-Kunde. Weiterführende Informationen finden Sie in der folgenden Tabelle.

| Art des Partners oder Kunden | Zugriff auf das Destination SDK |
---------|----------|
| Unabhängiger Software-Anbieter (ISV) | Mitglied werden [Partnerprogramm für Adobe und Technologie](https://partners.adobe.com/technologyprogram/experiencecloud.html) und fordern Sie die Bereitstellung einer Experience Platform-Sandbox für den Zugriff auf die Destination SDK an. |
| Systemintegrator (SI) | Sie müssen entweder den Gold- oder Platin-Status im [Adobe-Lösungspartner-Programm](https://solutionpartners.adobe.com/home.html) erreicht haben, um eine Experience Platform-Sandbox und Zugriff auf das Destination SDK zu erhalten. |
| Experience Platform-Kunde auf der [Real-Time CDP Ultimate-Package](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) | Standardmäßig erhalten Sie Zugriff auf Experience Platform-Sandboxes und Destination SDK, sodass Sie private Ziele für Ihr Unternehmen erstellen können. |

{style="table-layout:auto"}

## Allgemeine Vorgehensweise {#process}

Der Prozess zum Konfigurieren Ihres Ziels in Experience Platform ist unten beschrieben:

1. Wenn Sie ISV oder SI sind, lesen Sie den Abschnitt [Zugriff erhalten](#get-access) Informationen im obigen Abschnitt. [Real-Time CDP Ultimate-Package](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) -Kunden können diesen Schritt überspringen.
2. [Fordern Sie die Bereitstellung einer Experience Platform-Sandbox an](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) und aktivieren Sie die Authoring-Berechtigung für das Ziel.
3. Erstellen Sie Ihre Integration. Befolgen Sie die Anweisungen in der Produktdokumentation, um [Streaming-Ziele](guides/configure-destination-instructions.md) oder [dateibasierte Ziele](guides/configure-file-based-destination-instructions.md).
4. Testen Sie Ihre Integration. Befolgen Sie zum Testen die Anweisungen in der Produktdokumentation [Streaming-Ziele](testing-api/streaming-destinations/streaming-destination-testing-overview.md) oder [dateibasierte Ziele](testing-api/batch-destinations/file-based-destination-testing-overview.md).
5. Wenn Sie eine ISV oder SI sind, erstellen Sie eine [produktive Integration](./overview.md#productized-custom-integrations), [Integration übermitteln](guides/submit-destination.md) für die Überprüfung durch die Adobe (die standardmäßige Antwortzeit beträgt fünf Werktage).
6. Wenn Sie ein ISV oder SI sind und eine angepasste Integration erstellen, verwenden Sie den [Self-Service-Dokumentationsprozess](docs-framework/documentation-instructions.md), um eine Produktdokumentationsseite auf Experience League für Ihr Ziel zu erstellen.
7. Bei produktiven Integrationen wird Ihre Integration nach Genehmigung durch Adobe im [Experience Platform Katalog](../catalog/overview.md).
8. Wenn Sie Ihre Integration aktualisieren möchten, gehen Sie genauso vor.

## Referenz {#reference}

Adobe empfiehlt, die folgende Dokumentation zu Experience Platform zu lesen und zu verstehen:

* [Adobe Experience Platform-Ziele – Übersicht](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=de)
* [Grundlagen der XDM-Schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=de)
* [Übersicht zu Identitäts-Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de)
