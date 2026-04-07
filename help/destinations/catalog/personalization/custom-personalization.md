---
keywords: benutzerdefinierte Personalisierung; Ziel; benutzerdefiniertes Ziel von Experience Platform;
title: Benutzerdefinierte Personalization-Verbindung
description: Erfahren Sie, wie Sie das benutzerdefinierte Personalization-Ziel einrichten, um Zielgruppendaten aus Adobe Experience Platform zur Echtzeit-Personalisierung vor Ort abzurufen.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 3779531814cbf7e5718db0ac88aca266f14a1b21
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 28%

---


# Benutzerdefinierte Personalization-Verbindung {#custom-personalization-connection}

## Ziel-Änderungsprotokoll {#changelog}

Verwenden Sie dieses Änderungsprotokoll, um Aktualisierungen am benutzerdefinierten Personalization-Ziel zu verfolgen.

| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
| --- | --- | --- |
| Mai 2023 | Funktions- und Dokumentationsaktualisierung | Seit Mai 2023 unterstützt die **[!UICONTROL Custom personalization]**-Verbindung [attributbasierte Personalisierung](/help/destinations/ui/activate-edge-personalization-destinations.md#map-attributes) und steht allen Kundinnen und Kunden allgemein zur Verfügung. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Profilattribute können vertrauliche Daten enthalten. Um diese Daten zu schützen, verwenden Sie die [Edge Network-](https://developer.adobe.com/data-collection-apis/docs/) beim Konfigurieren des **[!UICONTROL Custom Personalization]** Ziels für die attributbasierte Personalisierung. Alle Edge Network-API-Aufrufe müssen in einem [authentifizierten Kontext](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication) erfolgen.
>
>Rufen Sie Profilattribute über die [Edge Network-API ab](https://developer.adobe.com/data-collection-apis/docs/) indem Sie eine serverseitige Integration hinzufügen, die denselben Datenstrom verwendet, den Sie bereits für Ihre Web- oder Mobile-SDK-Implementierung verwenden.
>
>Wenn Sie die oben genannten Anforderungen nicht erfüllen, basiert die Personalisierung nur auf der Zugehörigkeit zur Zielgruppe.

## Überblick {#overview}

Richten Sie dieses Ziel ein, damit externe Personalisierungsplattformen, Content-Management-Systeme, Anzeigen-Server und andere Anwendungen, die auf Kunden-Websites ausgeführt werden, Zielgruppeninformationen von [!DNL Adobe Experience Platform] abrufen können.

## Voraussetzungen {#prerequisites}

Dieses Ziel erfordert je nach Implementierung eine der folgenden Datenerfassungsmethoden:

* Verwenden Sie die [Adobe Experience Platform Web SDK](/help/collection/js/js-overview.md), um Daten von Ihrer Website zu erfassen.
* Verwenden Sie die [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/), um Daten von Ihrer Mobile App zu erfassen.
* Verwenden Sie die [Edge Network](https://developer.adobe.com/data-collection-apis/docs/)API, wenn Sie weder Web SDK noch Mobile SDK verwenden oder das Benutzererlebnis anhand von Profilattributen personalisieren möchten.

>[!IMPORTANT]
>
>**Attributbasierte Personalisierungsanforderungen:** Um auf der Grundlage von Profilattributen (nicht nur der Zielgruppenzugehörigkeit) zu personalisieren, **** Sie die [Edge Network-API](https://developer.adobe.com/data-collection-apis/docs/) mit authentifizierter Server-seitiger Integration verwenden, unabhängig davon, ob Sie auch Web SDK oder Mobile SDK für die Datenerfassung verwenden.
>
>Web SDK und Mobile SDK unterstützen nur die Personalisierung auf der Grundlage der Zielgruppenzugehörigkeit. Die Edge Network-API ist **erforderlich** um Profilattribute für die Personalisierung sicher abzurufen.

>[!IMPORTANT]
>
>Bevor Sie eine benutzerdefinierte Personalization-Verbindung erstellen, lesen Sie das Handbuch zum Aktivieren [ Zielgruppendaten für Edge-Personalisierungsziele ](/help/destinations/ui/activate-edge-personalization-destinations.md). In dieser Anleitung werden die erforderlichen Konfigurationsschritte für die Anwendungsfälle der Personalisierung derselben Seite und der nächsten Seite für mehrere Experience Platform-Komponenten erläutert.

## Unterstützte Zielgruppen {#supported-audiences}

In der folgenden Tabelle sind die Zielgruppentypen aufgeführt, die Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](/help/segmentation/home.md). |
| Alle anderen Ursprünge der Zielgruppe | Ja | Diese Kategorie enthält alle Ursprünge der Zielgruppe außerhalb der Zielgruppen, die durch die [!DNL Segmentation Service] generiert wurden. Lesen Sie mehr über [verschiedene Ursprünge von Audiences](/help/segmentation/ui/audience-portal.md#customize). Einige Beispiele: <ul><li>benutzerdefinierte Upload-Zielgruppen [importiert](/help/segmentation/ui/audience-portal.md#import-audience) aus CSV-Dateien in Experience Platform,</li><li>Lookalike-Zielgruppen,</li><li>Federated Audiences,</li><li>Zielgruppen, die in anderen Experience Platform-Apps generiert werden, z. B. [!DNL Adobe Journey Optimizer],</li><li>und mehr.</li></ul> |

{style="table-layout:auto"}

Unterstützte Zielgruppen nach Zielgruppen-Datentyp:

| Datentyp der Zielgruppe | Unterstützt | Beschreibung | Anwendungsfälle |
|--------------------|-----------|-------------|-----------|
| [Personen-Zielgruppen](/help/segmentation/types/people-audiences.md) | Ja | Targeting bestimmter Personengruppen basierend auf Kundenprofilen. | Häufige Käufer, Warenkorbabbrüche |
| [Konto-Zielgruppen](/help/segmentation/types/account-audiences.md) | Nein | Targeting von Personen in bestimmten Organisationen für Account-basierte Marketing-Strategien. | B2B-Marketing |
| [Interessenten-Zielgruppen](/help/segmentation/types/prospect-audiences.md) | Nein | Targeting von Personen, die noch keine Kunden sind, aber Merkmale mit Ihrer Zielgruppe teilen. | Akquise mit Drittanbieterdaten |
| [Datensatzexporte](/help/catalog/datasets/overview.md) | Nein | Sammlungen strukturierter Daten, die im Data Lake von [!DNL Adobe Experience Platform] gespeichert sind. | Reporting, Datenwissenschaft-Workflows |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Die folgende Tabelle beschreibt den Exporttyp und die Häufigkeit für dieses Ziel.

| Element | Typ | Anmerkungen |
| --- | --- | --- |
| Exporttyp | **[!UICONTROL Profile request]** | Fordert alle im benutzerdefinierten Personalization-Ziel zugeordneten Zielgruppen für ein einzelnes Profil an. Für verschiedene [Datenerfassungsdatenströme von Adobe können verschiedene benutzerdefinierte Personalization-Ziele eingerichtet ](/help/datastreams/overview.md). |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind immer aktive API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Informationen zu Datenströmen"
>abstract="Diese Option bestimmt, in welchen Datenerfassungsdatenstrom die Zielgruppen in der Antwort auf die Seite aufgenommen werden. Das Dropdown-Menü enthält nur Datenströme, für die die Zielkonfiguration aktiviert ist. Sie müssen einen Datenstrom konfigurieren, bevor Sie Ihr Ziel konfigurieren können."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=de" text="Erfahren Sie, wie Sie einen Datenstrom konfigurieren"

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](/help/destinations/ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](/help/destinations/ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Description]**: Geben Sie eine Beschreibung für Ihr Ziel ein. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden. Dieses Feld ist optional.
* **[!UICONTROL Integration alias]**: Eine erforderliche Zeichenfolge, die dieses Ziel in der Personalisierungsantwort identifiziert. Der Alias-Wert wird zusammen mit den mit diesem Ziel verknüpften Zielgruppen (und, falls konfiguriert, Attributen) an Ihre Website oder Ihr Programm zurückgegeben. Verwenden Sie den Alias in Ihrem Client- oder Server-seitigen Code, um das richtige Personalisierungsobjekt zu finden und zu verarbeiten, wenn mehrere Personalisierungsziele in demselben Datenstrom aktiv sind. Der Alias muss in einer Sandbox für alle benutzerdefinierten Personalization-Ziele eindeutig sein.
* **[!UICONTROL Datastream]**: Dadurch wird bestimmt, in welchen Datenerfassungs-Datenstrom die Zielgruppen in der Antwort auf die Seite aufgenommen werden. Das Dropdown-Menü enthält nur Datenströme, für die die Zielkonfiguration aktiviert ist. Weitere Details finden Sie unter [Konfigurieren eines Datenstroms](/help/datastreams/overview.md).

### Aktivieren von Warnhinweisen {#enable-alerts}

Aktivieren Sie Warnhinweise, um Benachrichtigungen zum Status Ihres Datenflusses zu diesem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](/help/destinations/ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
>
>Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen [ Aktivieren von Zielgruppen für dieses Ziel finden Sie unter „Aktivieren von Profilen ](/help/destinations/ui/activate-edge-personalization-destinations.md) Zielgruppen für Edge-Personalisierungsziele“.

## Exportierte Daten {#exported-data}

Wenn Sie „Tags [ Adobe Experience Platform&quot; zum Bereitstellen ](/help/tags/home.md) Experience Platform Web SDK verwenden, verwenden Sie die Funktion [send event complete](/help/tags/extensions/client/web-sdk/event-types.md). Ihre Aktion mit benutzerdefiniertem Code verfügt über eine `event.destinations` Variable, mit der Sie die exportierten Daten anzeigen können.

Hier finden Sie einen Beispielwert für die `event.destinations`-Variable:

```json
[
   {
      "type":"profileLookup",
      "destinationId":"7bb4cb8d-8c2e-4450-871d-b7824f547111",
      "alias":"personalizationAlias",
      "segments":[
         {
            "id":"399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         },
         {
            "id":"499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         }
      ]
   }
]
```

Wenn Sie „Tags[ nicht zum Bereitstellen ](/help/tags/home.md) Experience Platform Web SDK verwenden, verwenden Sie [Befehlsantworten](/help/collection/js/commands/command-responses.md) um die exportierten Daten anzuzeigen.

Analysieren Sie die JSON-Antwort von [!DNL Adobe Experience Platform], um den Integrationsalias des Programms zu finden, das Sie mit [!DNL Adobe Experience Platform] integrieren. Übergeben Sie die Zielgruppen-IDs als Targeting-Parameter in den Code des Programms. Nachfolgend finden Sie ein Beispiel dafür, wie dies spezifisch für die Zielantwort aussieht.

```js
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    if(result.destinations) { // Looking to see if the destination results are there

        // Get the destination with a particular alias
        var personalizationDestinations = result.destinations.filter(x => x.alias == "personalizationAlias")
        if(personalizationDestinations.length > 0) {
             // Code to pass the audience IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the audience IDs into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

### Beispielantwort für benutzerdefinierte Personalization mit Attributen {#example-response-attributes}

Bei Verwendung von **[!UICONTROL Custom Personalization With Attributes]** sieht die API-Antwort ähnlich wie im folgenden Beispiel aus.

Der Unterschied zwischen **[!UICONTROL Custom Personalization With Attributes]** und **[!UICONTROL Custom Personalization]** besteht in der Aufnahme des `attributes` Abschnitts in die API-Antwort.

```json
[
    {
        "type": "profileLookup",
        "destinationId": "7bb4cb8d-8c2e-4450-871d-b7824f547130",
        "alias": "personalizationAlias",
        "attributes": {
             "countryCode": {
                   "value" : "DE"
              },
             "membershipStatus": {
                   "value" : "PREMIUM"
              }
         },
        "segments": [
            {
                "id": "399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            },
            {
                "id": "499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            }
        ]
    }
]
```

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
