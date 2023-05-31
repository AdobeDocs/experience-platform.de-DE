---
keywords: benutzerdefinierte Personalisierung; Ziel; benutzerdefiniertes Ziel von Experience Platform;
title: Benutzerdefinierte Personalisierungsverbindung
description: Dieses Ziel bietet externen Personalisierungs-, Content-Management-Systemen, Anzeigen-Servern und anderen Programmen, die auf Ihrer Site ausgeführt werden, die Möglichkeit, Segmentinformationen von Adobe Experience Platform abzurufen. Dieses Ziel bietet Echtzeit-Personalisierung auf der Grundlage auf der Zugehörigkeit zu einem Benutzerprofilsegment.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 1ffcbabe29994fb881ff622394d669c4340c94f1
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 77%

---


# Benutzerdefinierte Personalisierungsverbindung {#custom-personalization-connection}

## Ziel-Änderungsprotokoll {#changelog}

| Veröffentlichungsmonat | Aktualisierungstyp | Beschreibung |
|---|---|---|
| Mai 2023 | Aktualisierung der Funktionen und Dokumentation | Ab Mai 2023 wird die **[!UICONTROL Benutzerdefinierte Personalisierung]** Verbindungsunterstützung [attributbasierte Personalisierung](../../ui/activate-edge-personalization-destinations.md#map-attributes) und ist allgemein für alle Kunden verfügbar. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Profilattribute können vertrauliche Daten enthalten. Um diese Daten zu schützen, muss die Variable **[!UICONTROL Benutzerdefinierte Personalisierung]** Für das Ziel müssen Sie die [Edge Network Server-API](/help/server-api/overview.md) beim Konfigurieren des Ziels für eine attributbasierte Personalisierung. Alle Server-API-Aufrufe müssen in einem [authentifizierter Kontext](../../../server-api/authentication.md).
>
><br>Wenn Sie bereits Web SDK oder Mobile SDK für Ihre Integration verwenden, können Sie Attribute über die Server-API abrufen, indem Sie eine serverseitige Integration hinzufügen.
>
><br>Wenn Sie die oben genannten Anforderungen nicht erfüllen, basiert die Personalisierung nur auf der Segmentzugehörigkeit.

## Übersicht {#overview}

Dieses Ziel bietet eine Möglichkeit, Segmentinformationen von Adobe Experience Platform auf externe Personalisierungsplattformen, Content-Management-Systeme, Anzeigen-Server und andere Programme zu übertragen, die auf Kunden-Websites ausgeführt werden.

## Voraussetzungen {#prerequisites}

Diese Integration basiert auf dem [Adobe Experience Platform Web SDK](../../../edge/home.md) oder [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/). Sie müssen eines dieser SDKs verwenden, um dieses Ziel verwenden zu können.

>[!IMPORTANT]
>
>Lesen Sie vor der Erstellung einer benutzerdefinierten Personalisierungsverbindung das Handbuch zum [Aktivieren von Zielgruppendaten für Edge-Personalisierungsziele](../../ui/activate-edge-personalization-destinations.md). In dieser Anleitung werden die erforderlichen Konfigurationsschritte für die Anwendungsfälle der Personalisierung derselben Seite und der nächsten Seite für mehrere Experience Platform-Komponenten erläutert.

## Exporttyp und Häufigkeit {#export-type-frequency}

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!DNL Profile request]** | Sie fordern alle Segmente an, die im benutzerdefinierten Personalisierungsziel für ein einzelnes Profil zugeordnet sind. Für verschiedene [Adobe-Datenerfassungsdatenströme](../../../edge/datastreams/overview.md) können verschiedene benutzerdefinierte Personalisierungsziele eingerichtet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Informationen zu Datenstrom-IDs"
>abstract="Diese Option bestimmt, in welchen Datenerfassungsdatenstrom die Segmente in der Antwort auf die Seite aufgenommen werden. Das Dropdown-Menü enthält nur Datenströme, für die die Zielkonfiguration aktiviert ist. Sie müssen einen Datenstrom konfigurieren, bevor Sie Ihr Ziel konfigurieren können."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=de" text="Erfahren Sie, wie Sie einen Datenstrom konfigurieren"

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie den gewünschten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für das Ziel ein. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden. Dieses Feld ist optional.
* **[!UICONTROL Integrationsalias]**: Dieser Wert wird als JSON-Objektname an das Experience Platform Web SDK gesendet.
* **[!UICONTROL Datenstrom-ID]**: Diese Angabe legt fest, in welchen Datenerfassungsdatenstrom die Segmente in der Antwort auf die Seite aufgenommen werden. Das Dropdown-Menü enthält nur Datenströme, für die die Zielkonfiguration aktiviert ist. Weitere Details finden Sie unter [Konfigurieren eines Datenstroms](../../../edge/datastreams/overview.md).

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Profile und Segmente aktivieren Edge-Personalisierungsziele](../../ui/activate-edge-personalization-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Exportierte Daten {#exported-data}

Wenn Sie [Tags in Adobe Experience Platform](../../../tags/home.md) zum Bereitstellen des Experience Platform Web SDK verwenden, nutzen Sie die Funktion [send event complete](../../../edge/extension/event-types.md), damit Ihre Aktion mit benutzerdefiniertem Code über eine `event.destinations`-Variable verfügt, mit der Sie die exportierten Daten anzeigen können.

Hier finden Sie einen Beispielwert für die `event.destinations`-Variable:

```
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

Wenn Sie [Tags](../../../tags/home.md) nicht zum Bereitstellen des Experience Platform Web SDK verwenden, nutzten Sie die Funktion [handling responses from events](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events), um die exportierten Daten anzuzeigen.

Die JSON-Antwort von Adobe Experience Platform kann analysiert werden, um den entsprechenden Integrationsalias des Programms zu finden, das Sie mit Adobe Experience Platform integrieren. Die Segment-IDs können als Targeting-Parameter dem Code des Programms übergeben werden. Nachfolgend finden Sie ein Beispiel dafür, wie dies spezifisch für die Zielantwort aussehen würde.

```
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
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

### Beispielantwort für [!UICONTROL Benutzerdefinierte Personalisierung mit Attributen]

Bei Verwendung von **[!UICONTROL Benutzerdefinierte Personalisierung mit Attributen]**, sieht die API-Antwort ähnlich wie im folgenden Beispiel aus.

Der Unterschied zwischen **[!UICONTROL Benutzerdefinierte Personalisierung mit Attributen]** und **[!UICONTROL Benutzerdefinierte Personalisierung]** ist die Aufnahme der `attributes` in der API-Antwort.

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

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](../../../data-governance/home.md).
