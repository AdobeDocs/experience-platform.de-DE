---
keywords: benutzerdefinierte Personalisierung; Ziel; benutzerdefiniertes Ziel von Experience Platform;
title: Benutzerdefinierte Personalisierungsverbindung
description: Dieses Ziel bietet externen Personalisierungs-, Content-Management-Systemen, Anzeigen-Servern und anderen Anwendungen, die auf Ihrer Site ausgeführt werden, eine Möglichkeit, Zielgruppeninformationen von Adobe Experience Platform abzurufen. Dieses Ziel bietet Echtzeit-Personalisierung basierend auf der Zugehörigkeit zu einer Zielgruppe im Benutzerprofil.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 44a4d5c592e13cdd1d4d75787dee5e1763fae9a4
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 45%

---


# Benutzerdefinierte Personalisierungsverbindung {#custom-personalization-connection}

## Ziel-Änderungsprotokoll {#changelog}

| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| Mai 2023 | Funktions- und Dokumentationsaktualisierung | Seit Mai 2023 unterstützt die **[!UICONTROL Custom personalization]**-Verbindung [attributbasierte Personalisierung](../../ui/activate-edge-personalization-destinations.md#map-attributes) und steht allen Kundinnen und Kunden allgemein zur Verfügung. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Profilattribute können vertrauliche Daten enthalten. Um diese Daten zu schützen, müssen Sie beim Konfigurieren des [-Ziels für ](https://developer.adobe.com/data-collection-apis/docs/) Attribut-basierte Personalisierung die **[!UICONTROL Custom Personalization]** Edge Network-API verwenden. Alle Edge Network-API-Aufrufe müssen in einem [authentifizierten Kontext](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication) erfolgen.
>
><br>Sie können Profilattribute über die [Edge Network-API abrufen](https://developer.adobe.com/data-collection-apis/docs/) indem Sie eine serverseitige Integration hinzufügen, die denselben Datenstrom verwendet, den Sie bereits für Ihre Web- oder Mobile-SDK-Implementierung verwenden.
>
><br>Wenn Sie die oben genannten Anforderungen nicht erfüllen, basiert die Personalisierung nur auf der Zugehörigkeit zur Zielgruppe.

## Überblick {#overview}

Richten Sie dieses Ziel ein, damit externe Personalisierungsplattformen, Content-Management-Systeme, Anzeigen-Server und andere Anwendungen, die auf Kunden-Websites ausgeführt werden, Zielgruppeninformationen von Adobe Experience Platform abrufen können.

## Voraussetzungen {#prerequisites}

Dieses Ziel erfordert je nach Implementierung eine der folgenden Datenerfassungsmethoden:

* Verwenden Sie die [Adobe Experience Platform Web SDK](/help/web-sdk/home.md), wenn Sie Daten von Ihrer Website erfassen möchten.
* Verwenden Sie die [Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/documentation/)SDK, wenn Sie Daten von Ihrer Mobile App erfassen möchten.
* Verwenden Sie die [Edge Network](https://developer.adobe.com/data-collection-apis/docs/)API, wenn Sie [Web SDK](/help/web-sdk/home.md) oder [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) nicht verwenden oder das Benutzererlebnis anhand von Profilattributen personalisieren möchten.

>[!IMPORTANT]
>
>**Attributbasierte Personalisierungsanforderungen:** Wenn Sie eine Personalisierung anhand von Profilattributen (nicht nur der Zielgruppenzugehörigkeit) vornehmen möchten, **** Sie die [Edge Network-API](https://developer.adobe.com/data-collection-apis/docs/) mit authentifizierter serverseitiger Integration verwenden, unabhängig davon, ob Sie auch Web SDK oder Mobile SDK für die Datenerfassung verwenden.
>
>Web SDK und Mobile SDK allein unterstützen nur Personalisierung basierend auf der Zielgruppenzugehörigkeit. Die Edge Network-API ist **erforderlich** um Profilattribute für die Personalisierung sicher abzurufen.

>[!IMPORTANT]
>
>Bevor Sie eine benutzerdefinierte Personalisierungsverbindung erstellen, lesen Sie das Handbuch zum Aktivieren [ Zielgruppendaten für Edge-Personalisierungsziele ](../../ui/activate-edge-personalization-destinations.md). In dieser Anleitung werden die erforderlichen Konfigurationsschritte für die Anwendungsfälle der Personalisierung derselben Seite und der nächsten Seite für mehrere Experience Platform-Komponenten erläutert.

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!DNL Profile request]** | Sie fordern alle Zielgruppen an, die im benutzerdefinierten Personalisierungsziel für ein einzelnes Profil zugeordnet sind. Für verschiedene [Adobe-Datenerfassungsdatenströme](../../../datastreams/overview.md) können verschiedene benutzerdefinierte Personalisierungsziele eingerichtet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Informationen zu Datenströmen"
>abstract="Diese Option bestimmt, in welchen Datenerfassungsdatenstrom die Zielgruppen in der Antwort auf die Seite aufgenommen werden. Das Dropdown-Menü enthält nur Datenströme, für die die Zielkonfiguration aktiviert ist. Sie müssen einen Datenstrom konfigurieren, bevor Sie Ihr Ziel konfigurieren können."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=de" text="Erfahren Sie, wie Sie einen Datenstrom konfigurieren"

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Description]**: Geben Sie eine Beschreibung für Ihr Ziel ein. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden. Dieses Feld ist optional.
* **[!UICONTROL Integration alias]**: Dieser Wert wird als JSON-Objektname an den Experience Platform Web SDK gesendet.
* **[!UICONTROL Datastream]**: Dadurch wird bestimmt, in welchen Datenerfassungs-Datenstrom die Zielgruppen in der Antwort auf die Seite aufgenommen werden. Das Dropdown-Menü enthält nur Datenströme, für die die Zielkonfiguration aktiviert ist. Weitere Details finden Sie unter [Konfigurieren eines Datenstroms](../../../datastreams/overview.md).

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen [ Aktivieren von Zielgruppen für dieses Ziel finden Sie unter ](../../ui/activate-edge-personalization-destinations.md)Aktivieren von Profilen und Zielgruppen für Edge-Personalisierungsziele“.

## Exportierte Daten {#exported-data}

Wenn Sie [Tags in Adobe Experience Platform](../../../tags/home.md) zum Bereitstellen des Experience Platform Web SDK verwenden, nutzen Sie die Funktion [send event complete](../../../tags/extensions/client/web-sdk/event-types.md), damit Ihre Aktion mit benutzerdefiniertem Code über eine `event.destinations`-Variable verfügt, mit der Sie die exportierten Daten anzeigen können.

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

Wenn Sie „Tags[ nicht zum Bereitstellen ](/help/tags/home.md) Experience Platform Web SDK verwenden, verwenden Sie [Befehlsantworten](/help/web-sdk/commands/command-responses.md) um die exportierten Daten anzuzeigen.

Die JSON-Antwort von Adobe Experience Platform kann analysiert werden, um den entsprechenden Integrationsalias des Programms zu finden, das Sie mit Adobe Experience Platform integrieren. Die Zielgruppen-IDs können als Zielgruppenbestimmungsparameter in den Code des Programms übergeben werden. Nachfolgend finden Sie ein Beispiel dafür, wie dies spezifisch für die Zielantwort aussehen würde.

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

### Beispielantwort für [!UICONTROL Custom Personalization With Attributes]

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

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](../../../data-governance/home.md).
