---
keywords: benutzerdefinierte Personalisierung; Ziel; benutzerdefiniertes Ziel von Experience Platform;
title: Benutzerdefinierte Personalisierungsverbindung
description: Dieses Ziel bietet externen Personalisierungs-, Content-Management-Systemen, Anzeigen-Servern und anderen Programmen, die auf Ihrer Site ausgeführt werden, die Möglichkeit, Segmentinformationen von Adobe Experience Platform abzurufen. Dieses Ziel bietet Echtzeit-Personalisierung auf der Grundlage auf der Zugehörigkeit zu einem Benutzerprofilsegment.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: c83c7e2a74a6bf4a7a4c9c04ccebfd0296c89bce
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 61%

---

# Benutzerdefinierte Personalisierungsverbindung {#custom-personalization-connection}

## Übersicht {#overview}

Dieses Ziel bietet eine Möglichkeit, Segmentinformationen von Adobe Experience Platform auf externe Personalisierungsplattformen, Content-Management-Systeme, Anzeigen-Server und andere Programme zu übertragen, die auf Kunden-Websites ausgeführt werden.

## Voraussetzungen {#prerequisites}

Diese Integration basiert auf dem [Adobe Experience Platform Web SDK](../../../edge/home.md) oder [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/). Sie müssen eines dieser SDKs verwenden, um dieses Ziel verwenden zu können.

>[!IMPORTANT]
>
>Lesen Sie vor der Erstellung einer benutzerdefinierten Personalisierungsverbindung die Anleitung zum [Konfigurieren von Personalisierungszielen für die Personalisierung derselben Seite und der nächsten Seite](../../ui/configure-personalization-destinations.md). In dieser Anleitung werden die erforderlichen Konfigurationsschritte für die Anwendungsfälle der Personalisierung derselben Seite und der nächsten Seite für mehrere Experience Platform-Komponenten erläutert.

## Exporttyp und Häufigkeit {#export-type-frequency}

**Profilanfrage**: Sie fordern alle Segmente an, die im benutzerdefinierten Personalisierungsziel für ein einzelnes Profil zugeordnet sind. Für verschiedene [Adobe-Datenerfassungsdatenströme](../../../edge/fundamentals/datastreams.md) können verschiedene benutzerdefinierte Personalisierungsziele eingerichtet werden.

## Anwendungsfälle {#use-cases}

Die [!DNL Custom personalization connection] ermöglicht Ihnen die Verwendung eigener Plattformen für Personalisierungspartner (z. B. [!DNL Optimizely], [!DNL Pega]), wobei auch die Datenerfassungs- und Segmentierungsfunktionen des Edge-Netzwerks genutzt werden, um eine tiefere Kundenpersonalisierung zu ermöglichen.

Die unten beschriebenen Anwendungsfälle umfassen sowohl die Personalisierung der Site als auch zielgruppengerechte On-site-Werbung.

Um diese Anwendungsfälle zu aktivieren, benötigen Kunden eine schnelle, optimierte Methode zum Abrufen von Segmentinformationen aus der Experience Platform und zum Senden dieser Informationen an ihre vorgesehenen Systeme, die sie in der Experience Platform-Benutzeroberfläche als benutzerdefinierte Personalisierungsverbindungen konfiguriert haben.

Bei diesen Systemen kann es sich um externe Personalisierungsplattformen, Content Management-Systeme, Adserver und andere Anwendungen handeln, die über die Web- und mobilen Eigenschaften von Kunden hinweg ausgeführt werden.

### Personalisierung auf derselben Seite {#same-page}

Ein Benutzer besucht eine Seite Ihrer Website. Der Kunde kann die aktuelle Seitenbesuchsinformationen (z. B. verweisende URL, Browsersprache, eingebettete Produktinformationen) verwenden, um die nächste Aktion/Entscheidung (z. B. Personalisierung) auszuwählen, indem er die benutzerdefinierte Personalisierungsverbindung für Plattformen ohne Adobe verwendet (z. B. [!DNL Pega], [!DNL Optimizely]usw.).

### Personalisierung der nächsten Seite {#next-page}

Ein Benutzer besucht Seite A auf Ihrer Website. Auf der Grundlage dieser Interaktion hat sich der Benutzer für eine Reihe von Segmenten qualifiziert. Der Benutzer klickt dann auf einen Link, der ihn von Seite A zu Seite B bringt. Die Segmente, für die sich der Benutzer während der vorherigen Interaktion auf Seite A qualifiziert hat, werden zusammen mit den durch den aktuellen Website-Besuch festgelegten Profilaktualisierungen verwendet, um die nächste Aktion/Entscheidung zu ermöglichen (z. B. welches Werbebanner dem Besucher angezeigt werden soll oder, im Fall von A/B-Tests, welche Version der Seite angezeigt werden soll).

### Personalisierung der nächsten Sitzung {#next-session}

Ein Benutzer besucht mehrere Seiten auf Ihrer Website. Auf der Grundlage dieser Interaktionen hat sich der Benutzer für eine Reihe von Segmenten qualifiziert. Der Benutzer beendet dann die aktuelle Browser-Sitzung.

Am folgenden Tag kehrt der Benutzer zur gleichen Kundenwebsite zurück. Die Segmente, für die sie sich während der vorherigen Interaktion mit allen besuchten Webseiten qualifiziert hatten, sowie die durch den aktuellen Website-Besuch bestimmten Profilattribute werden zur Auswahl der nächsten Aktion/Entscheidung verwendet (z. B. welches Werbebanner dem Besucher angezeigt werden soll oder, im Fall von A/B-Tests, welche Version der Seite angezeigt werden soll).

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Informationen zu Datenstrom-IDs"
>abstract="Diese Option bestimmt, in welchen Datenerfassungsdatenstrom die Segmente in der Antwort auf die Seite aufgenommen werden. Das Dropdown-Menü enthält nur Datenströme, für die die Zielkonfiguration aktiviert ist. Sie müssen einen Datenstrom konfigurieren, bevor Sie Ihr Ziel konfigurieren können."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=de" text="Erfahren Sie, wie Sie einen Datenstrom konfigurieren"

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie den gewünschten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für das Ziel ein. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden. Dieses Feld ist optional.
* **[!UICONTROL Integrationsalias]**: Dieser Wert wird als JSON-Objektname an das Experience Platform Web SDK gesendet.
* **[!UICONTROL Datenstrom-ID]**: Diese Angabe legt fest, in welchen Datenerfassungsdatenstrom die Segmente in der Antwort auf die Seite aufgenommen werden. Das Dropdown-Menü enthält nur Datenströme, für die die Zielkonfiguration aktiviert ist. Weitere Details finden Sie unter [Konfigurieren eines Datenstroms](../../../edge/fundamentals/datastreams.md).

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Profilen und Segmenten für Profilanfrageziele](../../ui/activate-profile-request-destinations.md).

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
        var personalizationDestinations = result.destinations.filter(x => x.alias == “personalizationAlias”)
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == “adServerAlias”)
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](../../../data-governance/home.md).
