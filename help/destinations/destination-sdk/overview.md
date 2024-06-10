---
description: Adobe Experience Platform Destinationen SDK sind eine Reihe von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster konfigurieren können, damit Experience Platform Zielgruppen- und Profildaten basierend auf Daten- und Authentifizierungsformaten Ihrer Wahl an Ihren Endpunkt oder Speicherort übermitteln kann. Die Konfigurationen werden in Experience Platform gespeichert und können über eine API für zusätzliche Aktualisierungen abgerufen werden.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 9c59f6edd51c61c1fe2ff69e0adea49e6efb8745
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 22%

---

# Adobe Experience Platform Destination SDK

Adobe Experience Platform Destinationen SDK sind eine Suite von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster konfigurieren können, damit Experience Platform Zielgruppen- und Profildaten basierend auf Daten- und Authentifizierungsformaten Ihrer Wahl an Ihren Endpunkt oder Speicherort übermitteln kann. Die Konfigurationen werden in Experience Platform gespeichert und können über eine API für zusätzliche Aktualisierungen abgerufen werden.

Die Dokumentation zur Destination SDK enthält Anleitungen zum Verwenden der Adobe Experience Platform Destinationen SDK zum Konfigurieren, Testen und Veröffentlichen einer produktiven Zielintegration mit Adobe Experience Platform und dazu, dass Ihr Ziel Teil des ständig wachsenden Zielkatalogs wird. Durch die Verwendung von Destination SDK können Sie auch Ihr eigenes benutzerdefiniertes privates Ziel erstellen, um Daten zu exportieren, die auf Ihre Anforderungen zugeschnitten sind.

![Screenshot der Experience Platform-Benutzeroberfläche mit dem Zielkatalog.](assets/destinations-catalog-overview.png)

## Schnellstart - wichtige Informationen erkunden {#quick-start}

Lesen Sie die Dokumentation unter den unten stehenden Links, um schnell mit der Konfiguration und dem Versand Ihres Ziels über Destination SDK zu beginnen.

>[!BEGINSHADEBOX]

<table style="border: 0;">
  <tbody>
    <tr>
        <td>
            <p><b>Konfigurationsseiten</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/functionality/configuration-options.md">Alle Konfigurationsoptionen erklärt</a></li>
                <li> Konfiguration des Zielservers - <a href="/help/destinations/destination-sdk/functionality/destination-server/server-specs.md">Serverspezifikationen</a> und <a href="/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md">Vorlagentypen</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md">Kundendatenfelder und andere Zielkonfigurationskomponenten</a></li>
                <li><a href="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">Vorlagen und Makros</a></li>
            </ul>
        </td>
        <td>
            <p><b>Handbücher</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/overview.md#process">Integrationsprozess auf hoher Ebene</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">Streaming-Ziel konfigurieren</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">Dateibasiertes Ziel konfigurieren</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-prospect-audience-destination.md">Konfigurieren eines Ziels für den Export von Profilen</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/submit-destination.md">Ziel zur Veröffentlichung übermitteln</a></li>
            </ul>
        </td>
                <td>
            <p><b>API-Referenzen</b></p>
            <ul>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-servers-and-templates">API-Referenz für Ziel-Server-Endpunkt</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-configurations">API-Referenz für Ziel-Endpunkt</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Audience-metadata-templates">Referenz zur Audience Metadata-API</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-testing">API-Referenz testen</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-publishing">API-Referenz zur Zielveröffentlichung</a></li>
            </ul>
        </td>
    </tr>
  </tbody>
</table>

<table style="border: 0;">
  <tbody>
    <tr>
        <td>
            <p><b>Streaming-Ziel konfigurieren - Spickzettel</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">End-to-End-Handbuch für Streaming-Ziele konfigurieren</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-server/message-format.md">Grundlegendes zur Datenumwandlung mithilfe von Kieselstein-Vorlagen</a> und <a href="/help/destinations/destination-sdk/functionality/destination-server/supported-functions.md">Anzeigen unterstützter Vorlagenfunktionen</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md">Grundlagen zu Datenerfassungsrichtlinien</a></li>
                <li><a href="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">Beispiel für eine Live-Konfiguration</a></li>
                <li><a href="/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md">Streaming-Ziel testen</a></li>
            </ul>
        </td>
        <td>
            <p><b>Konfigurieren eines dateibasierten Ziels - Cheatsheet</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">Konfigurieren eines dateibasierten Ziel-End-to-End-Handbuchs</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md">Dateiformate für die exportierten Dateien konfigurieren</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-amazon-s3-destination-with-predefined-file-formatting.md">Beispiel für eine Live-Konfiguration für ein Amazon S3-Ziel</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/batch-configuration.md">Batch-Konfiguration</a> für den Dateiexportplan und die Dateibenennung</li>
                <li><a href="/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md">Testen des dateibasierten Ziels</a></li>
            </ul>
        </td>
        <td>
            <p><b>Weitere wichtige Informationen</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/getting-started.md#obtain-authentication-credentials">Abrufen der erforderlichen Authentifizierungsberechtigungen für die Verwendung der API</a></li>
                <li><a href="/help/destinations/destination-sdk/integration-prerequisites.md">Voraussetzungen für die Integration</a></li>
                <li><a href="/help/destinations/destination-sdk/glossary.md">Glossar der Destination SDK</a></li>                
                <li><a href="/help/destinations/destination-sdk/functionality/rate-limiting-retry-policy.md">Ratenbeschränkungen und Wiederholungspolitik</a></li>
                <li><a href="/help/destinations/destination-sdk/docs-framework/self-service-template.md">Self-Service-Vorlage zum Dokument Ihres Ziels</a></li>
            </ul>
        </td>
    </tr>
  </tbody>
</table>


>[!ENDSHADEBOX]

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

Der Zugriff auf die Destination SDK variiert je nach Ihrem Status als Partner oder Experience Platform, Real-Time CDP-Kunde. Weitere Informationen finden Sie in der unten stehenden Tabelle.

| Art des Partners oder Kunden | Zugriff auf das Destination SDK |
---------|----------|
| Unabhängiger Software-Anbieter (ISV) | Mitglied werden [Adobe Technology Partner Program](https://partners.adobe.com/technologyprogram/experiencecloud.html) und fordern Sie die Bereitstellung einer Experience Platform-Sandbox für den Zugriff auf die Destination SDK an. |
| Systemintegrator (SI) | Sie müssen entweder auf Gold- oder auf Platinebene im [Adobe Solution Partner Program](https://solutionpartners.adobe.com/home.html) , um eine Experience Platform-Sandbox bereitzustellen und Zugriff auf die Destination SDK zu erhalten. |
| Experience Platform-Kunde auf dem [Real-Time CDP Ultimate-Package](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) | Standardmäßig erhalten Sie Zugriff auf Experience Platform-Sandboxes und Destination SDK, sodass Sie private Ziele für Ihr Unternehmen erstellen können. |

{style="table-layout:auto"}

## Allgemeine Vorgehensweise {#process}

Der Prozess zum Konfigurieren Ihres Ziels in Experience Platform ist unten beschrieben:

1. Wenn Sie ISV oder SI sind, lesen Sie den Abschnitt [Zugriff erhalten](#get-access) Informationen im obigen Abschnitt. [Real-Time CDP Ultimate-Package](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) -Kunden können diesen Schritt überspringen.
2. [Fordern Sie die Bereitstellung einer Experience Platform-Sandbox an](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) und aktivieren Sie die Authoring-Berechtigung für das Ziel.
3. Erstellen Sie Ihre Integration. Befolgen Sie die Anweisungen in der Produktdokumentation, um [Streaming-Ziele](guides/configure-destination-instructions.md) oder [dateibasierte Ziele](guides/configure-file-based-destination-instructions.md).
4. Testen Sie Ihre Integration. Befolgen Sie zum Testen die Anweisungen in der Produktdokumentation [Streaming-Ziele](testing-api/streaming-destinations/streaming-destination-testing-overview.md) oder [dateibasierte Ziele](testing-api/batch-destinations/file-based-destination-testing-overview.md).
5. Wenn Sie eine ISV oder SI sind, erstellen Sie eine [produktive Integration](./overview.md#productized-custom-integrations), [Integration übermitteln](guides/submit-destination.md) Für Adobe-Überprüfung (die standardmäßige Antwortzeit beträgt fünf Werktage).
6. Wenn Sie ein ISV oder SI sind und eine produktionserwartete Integration erstellen, verwenden Sie die [Self-Service-Dokumentationsprozess](docs-framework/documentation-instructions.md) , um eine Produktdokumentationsseite auf dem Experience League für Ihr Ziel zu erstellen.
7. Bei produktionierten Integrationen wird nach der Genehmigung durch Adobe Ihre Integration im [Experience Platform-Katalog](../catalog/overview.md).
8. Wenn Sie Ihre Integration aktualisieren möchten, gehen Sie genauso vor.

## Referenz {#reference}

Adobe empfiehlt, die folgende Dokumentation zu Experience Platform zu lesen und zu verstehen:

* [Adobe Experience Platform-Ziele – Übersicht](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=de)
* [Grundlagen der XDM-Schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=de)
* [Übersicht zu Identitäts-Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de)
