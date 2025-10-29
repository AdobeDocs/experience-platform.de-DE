---
description: Adobe Experience Platform Destination SDK ist ein Satz von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster für Experience Platform konfigurieren können, um Zielgruppen- und Profildaten basierend auf den von Ihnen ausgewählten Daten- und Authentifizierungsformaten an Ihren Endpunkt oder Speicherort zu senden. Die Konfigurationen werden in Experience Platform gespeichert und können über eine API für zusätzliche Aktualisierungen abgerufen werden.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 22%

---

# Adobe Experience Platform Destination SDK

Adobe Experience Platform Destination SDK ist eine Suite von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster für Experience Platform konfigurieren können, um Zielgruppen- und Profildaten basierend auf den von Ihnen ausgewählten Daten- und Authentifizierungsformaten an Ihren Endpunkt oder Speicherort zu senden. Die Konfigurationen werden in Experience Platform gespeichert und können über eine API für zusätzliche Aktualisierungen abgerufen werden.

Die Destination SDK-Dokumentation enthält Anweisungen dazu, wie Sie mit der Adobe Experience Platform Destination SDK eine produktive Zielintegration mit Adobe Experience Platform konfigurieren, testen und veröffentlichen und Ihr Ziel in den ständig wachsenden Zielkatalog integrieren können. Durch die Verwendung von Destination SDK können Sie auch Ihr eigenes benutzerdefiniertes privates Ziel erstellen, um Daten zu exportieren, die auf Ihre Anforderungen zugeschnitten sind.

![Screenshot der Experience Platform-Benutzeroberfläche mit dem Zielkatalog.](assets/destinations-catalog-overview.png)

## Schnellstart: Wichtige Informationen {#quick-start}

Lesen Sie die Dokumentation in den unten stehenden Links, um schnell mit der Konfiguration und Übermittlung Ihres Ziels über Destination SDK zu beginnen.

>[!BEGINSHADEBOX]

<table style="border: 0;">
  <tbody>
    <tr>
        <td>
            <p><b>Konfigurationsseiten</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/functionality/configuration-options.md">Erklärung aller Konfigurationsoptionen</a></li>
                <li> Ziel-Server-Konfiguration <a href="/help/destinations/destination-sdk/functionality/destination-server/server-specs.md">Server-Spezifikationen</a> und <a href="/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md">Vorlagenspezifikationen</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md">Kundendatenfelder und andere Zielkonfigurationskomponenten</a></li>
                <li><a href="https://experienceleague.adobe.com/de/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">Vorlagen und Makros</a></li>
            </ul>
        </td>
        <td>
            <p><b>Handbücher</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/overview.md#process">Allgemeine Integration</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">Konfigurieren eines Streaming-Ziels</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">Konfigurieren eines dateibasierten Ziels</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-prospect-audience-destination.md">Konfigurieren eines Ziels zum Exportieren von Interessentenprofilen</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/submit-destination.md">Ziel zur Veröffentlichung übermitteln</a></li>
            </ul>
        </td>
                <td>
            <p><b>API-Referenzen</b></p>
            <ul>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-servers-and-templates">API-Referenz für Ziel-Server-Endpunkt</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-configurations">API-Referenz für Zielendpunkt</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Audience-metadata-templates">API-Referenz für Zielgruppen-Metadaten</a></li>
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
            <p><b>Konfigurieren eines Streaming-Ziels - Spickzettel</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">Konfigurieren eines End-to-End-Handbuchs für Streaming-Ziele</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-server/message-format.md">Verstehen der Datenumwandlung mithilfe von Pebble</a>Vorlagen und <a href="/help/destinations/destination-sdk/functionality/destination-server/supported-functions.md">unterstützte Vorlagenfunktionen anzeigen</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md">Datenzusammenführungsrichtlinien verstehen</a></li>
                <li><a href="https://experienceleague.adobe.com/de/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">Live-Konfigurationsbeispiel</a></li>
                <li><a href="/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md">Testen des Streaming-Ziels</a></li>
            </ul>
        </td>
        <td>
            <p><b>Konfigurieren eines dateibasierten Ziels - Spickzettel</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">Konfigurieren eines dateibasierten Ziels - End-to-End-Handbuch</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md">Konfigurieren von Dateiformaten für die exportierten Dateien</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-amazon-s3-destination-with-predefined-file-formatting.md">Live-Konfigurationsbeispiel für ein Amazon S3-Ziel</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/batch-configuration.md">Batch-Konfiguration</a> für den Zeitplan für den Dateiexport und die Dateibenennung</li>
                <li><a href="/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md">Testen des dateibasierten Ziels</a></li>
            </ul>
        </td>
        <td>
            <p><b>Sonstige wesentliche Informationen</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/getting-started.md#obtain-authentication-credentials">Abrufen der erforderlichen Authentifizierungsdaten für die Verwendung der API</a></li>
                <li><a href="/help/destinations/destination-sdk/integration-prerequisites.md">Voraussetzungen für die Integration</a></li>
                <li><a href="/help/destinations/destination-sdk/glossary.md">Glossar der Begriffe in Destination SDK</a></li>                
                <li><a href="/help/destinations/destination-sdk/functionality/rate-limiting-retry-policy.md">Ratenbeschränkungen und Wiederholungsrichtlinie</a></li>
                <li><a href="/help/destinations/destination-sdk/docs-framework/self-service-template.md">Self-Service-Vorlage zur Dokumentation Ihres Ziels</a></li>
            </ul>
        </td>
    </tr>
  </tbody>
</table>


>[!ENDSHADEBOX]

## Produktdefinierte und benutzerdefinierte Integrationen {#productized-custom-integrations}

>[!IMPORTANT]
>
> Diese Funktion zum Erstellen privater benutzerdefinierter Ziele ist nur für [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html)-Kunden verfügbar.

Als Destination SDK-Partner können Sie von der Hinzufügung Ihres produktspezifischen Ziels zum [Experience Platform-Katalog](../catalog/overview.md) profitieren:

1. Standardisieren Sie die Integrationskonfigurationen für alle Kunden mit vorkonfigurierten Parametern und vereinfachen Sie die Einrichtung für Kunden.
2. Stellen Sie im Zielkatalog von Experience Platform eine Zielkarte mit Branding vor, um die Einrichtung und den Bekanntheitsgrad für Kunden zu vereinfachen.
3. Wird als produktbezogene Zielintegration mit Adobe Experience Platform und Adobe Real-Time Customer Data Platform vorgestellt.

Als Experience Platform-Kunde können Sie auch Ihr eigenes benutzerdefiniertes Ziel erstellen, das Ihren Aktivierungsanforderungen am besten entspricht.

![Übersichtsdiagramm, das zeigt, wie Zielentwickler mit Destination SDK interagieren und wie Real-Time CDP-Kunden von produktbezogenen und privaten Zielen profitieren.](assets/destination-sdk-visual.png)

## Unterstützte Integrationstypen {#supported-integration-types}

### Echtzeit-Integrationen (Streaming) {#real-time-integrations}

Über Destination SDK unterstützt Adobe Experience Platform Echtzeit-Integrationen (auch als Streaming bezeichnet) mit Zielen mit einem REST-API-Endpunkt. Die Echtzeit-Integration mit Experience Platform unterstützt Funktionen wie:

* Nachrichtenumwandlung und -aggregation
* Profilaufstockung
* Konfigurierbare Metadatenintegration zum Initialisieren der Zielgruppen-Einrichtung und der Datenübertragung
* Konfigurierbare Authentifizierung
* Eine Suite von Test- und Validierungs-APIs zum Testen und Iterieren Ihrer Zielkonfigurationen

### Dateibasierte Integrationen {#file-based-integrations}

Über Destination SDK können Sie auch Integrationen einrichten, um Dateien regelmäßig an den gewünschten Speicherort zu exportieren. Die dateibasierte Integration mit Experience Platform unterstützt Funktionen wie:

* Dateiexport in verschiedenen unterstützten Formaten (CSV, Parquet, JSON)
* Konfigurierbare Dateiformatierungsoptionen, mit denen Sie das Format der exportierten Dateien strukturieren können, um Ihre nachgelagerten Anforderungen zu erfüllen.

Informationen zu den technischen Anforderungen auf der Zielseite finden Sie im Artikel [Integrationsvoraussetzungen](integration-prerequisites.md) und Informationen zu allen unterstützten Konfigurationen finden Sie [&#x200B; Artikel &#x200B;](functionality/configuration-options.md) Konfigurationsoptionen

## Zugriff auf das Destination SDK {#get-access}

Der Zugriff auf Destination SDK hängt von Ihrem Partnerstatus bzw. Ihrem Status als Experience Platform- oder Real-Time CDP-Kunde ab. Weitere Informationen finden Sie in der Tabelle unten.

| Art des Partners oder Kunden | Zugriff auf das Destination SDK |
|---------|----------|
| Unabhängiger Software-Anbieter (ISV) | Werden Sie Mitglied im [Adobe-Technologiepartnerprogramm](https://partners.adobe.com/technologyprogram/experiencecloud.html) und beantragen Sie die Bereitstellung einer Experience Platform-Sandbox für den Zugriff auf Destination SDK. |
| Systemintegrator (SI) | Sie müssen entweder den Gold- oder Platin-Status im [Adobe-Lösungspartner-](https://solutionpartners.adobe.com/home.html) erreicht haben, um eine Experience Platform-Sandbox und Zugriff auf Destination SDK zu erhalten. |
| Experience Platform-Kunde mit dem [Real-Time CDP Ultimate-Paket](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) | Standardmäßig erhalten Sie Zugriff auf Experience Platform-Sandboxes und Destination SDK, sodass Sie private Ziele für Ihr Unternehmen erstellen können. |

{style="table-layout:auto"}

## Allgemeine Vorgehensweise {#process}

Der Prozess zum Konfigurieren Ihres Ziels in Experience Platform ist unten beschrieben:

1. Wenn Sie ein ISV oder SI sind, lesen Sie die Informationen [Zugriff erhalten](#get-access) im obigen Abschnitt. [Real-Time CDP Ultimate-Paket](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) Kunden können diesen Schritt überspringen.
2. [Fordern Sie die Bereitstellung einer Experience Platform-Sandbox an](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) und aktivieren Sie die Authoring-Berechtigung für das Ziel.
3. Erstellen Sie Ihre Integration. Befolgen Sie die Anweisungen in der Produktdokumentation zum Konfigurieren [Streaming](guides/configure-destination-instructions.md)Ziele oder [dateibasierte Ziele](guides/configure-file-based-destination-instructions.md).
4. Testen Sie die Integration. Befolgen Sie die Anweisungen in der Produktdokumentation zum Testen [Streaming](testing-api/streaming-destinations/streaming-destination-testing-overview.md)Ziele oder [dateibasierte Ziele](testing-api/batch-destinations/file-based-destination-testing-overview.md).
5. Wenn Sie ein ISV oder SI sind und eine [angepasste Integration](./overview.md#productized-custom-integrations) erstellen, [Ihre Integration übermitteln](guides/submit-destination.md) zur Überprüfung durch Adobe (die standardmäßige Antwortzeit beträgt fünf Werktage).
6. Wenn Sie ein ISV oder SI sind und eine angepasste Integration erstellen, verwenden Sie den [Self-Service-Dokumentationsprozess](docs-framework/documentation-instructions.md) um eine Produktdokumentationsseite auf Experience League für Ihr Ziel zu erstellen.
7. Bei produktbezogenen Integrationen wird Ihre Integration nach der Genehmigung durch Adobe im [Experience Platform-Katalog angezeigt](../catalog/overview.md).
8. Wenn Sie Ihre Integration aktualisieren möchten, gehen Sie genauso vor.

## Referenz {#reference}

Adobe empfiehlt, die folgende Dokumentation zu Experience Platform zu lesen und zu verstehen:

* [Adobe Experience Platform-Ziele – Übersicht](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=de)
* [Grundlagen der XDM-Schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=de)
* [Übersicht zu Identitäts-Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de)
