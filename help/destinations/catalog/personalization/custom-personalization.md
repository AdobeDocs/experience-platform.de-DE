---
keywords: benutzerdefinierte Personalisierung; Bestimmungsort; Benutzerdefiniertes Ziel der Erlebnisplattform;
title: Benutzerdefinierte Personalisierungsverbindung
description: Dieses Ziel bietet eine externe Personalisierung, Content Management-Systeme, Anzeigen-Server und andere Anwendungen, die auf Ihrer Site ausgeführt werden, um Segmentinformationen aus Adobe Experience Platform abzurufen. Dieses Ziel bietet eine Echtzeit-Personalisierung basierend auf der Mitgliedschaft in einem Benutzerprofilsegment.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: dd9493077706b102467493e90b363ac202550eee
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 7%

---

# Benutzerdefinierte Personalisierungsverbindung {#custom-personalization-connection}

## Übersicht {#overview}

Dieses Ziel bietet eine Möglichkeit, Segmentinformationen von Adobe Experience Platform zu externen Personalisierungsplattformen, Content-Management-Systemen, Anzeigen-Servern und anderen Anwendungen abzurufen, die auf Kunden-Websites ausgeführt werden.

## Voraussetzungen {#prerequisites}

Diese Integration basiert auf der [Adobe Experience Platform Web SDK](../../../edge/home.md) oder [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/). Sie müssen eines dieser SDKs verwenden, um dieses Ziel zu verwenden.

## Exporttyp {#export-type}

**Profilanfrage** - Sie fordern alle Segmente an, die im benutzerdefinierten Personalisierungsziel für ein einzelnes Profil zugeordnet sind. Verschiedene benutzerdefinierte Personalisierungsziele können für verschiedene [Datenerfassungs-Datenspeicher der Adobe](../../../edge/fundamentals/datastreams.md).

## Anwendungsfälle {#use-cases}

Dieses Ziel teilt Zielgruppen mit Adservern und Nicht-Adobe-Personalisierungsanwendungen, die in Echtzeit verwendet werden, um zu entscheiden, welche Advertising-Benutzer auf einer Website sehen sollen.

### Anwendungsfall 1

**Personalisieren einer Startseite**

Eine Website zum Vermieten und Verkaufen möchte ihre Startseite anhand von Segmentqualifikationen in Adobe Experience Platform personalisieren. Das Unternehmen kann auswählen, welche Zielgruppen ein personalisiertes Erlebnis erhalten sollen, und diese Zielgruppen dem benutzerdefinierten Personalisierungsziel zuordnen, das für seine Nicht-Adobe-Personalisierungsanwendung als Targeting-Kriterien eingerichtet wurde.

**Targeting-Onsite-Werbung**

Mithilfe eines separaten benutzerdefinierten Personalisierungsziels für den Anzeigenserver kann dieselbe Website für die Werbung auf der Site einen anderen Satz von Segmenten aus Adobe Experience Platform als Targeting-Kriterien verwenden.

## Mit Ziel verbinden {#connect}

Gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md).

### Verbindungsparameter {#parameters}

while [Einrichten](../../ui/connect-destination.md) An diesem Ziel müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden. Dieses Feld ist optional.
* **[!UICONTROL Integrationsalias]**: Dieser Wert wird als JSON-Objektname an das Experience Platform Web SDK gesendet.
* **[!UICONTROL Datenspeicher-ID]**: Dadurch wird bestimmt, in welchem Datenerfassungsdatenstrom die Segmente in die Antwort auf die Seite aufgenommen werden. Das Dropdown-Menü zeigt nur Datensätze an, für die die Zielkonfiguration aktiviert ist. Siehe [Konfigurieren eines Datastreams](../../../edge/fundamentals/datastreams.md) für weitere Details.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Lesen [Profile und Segmente für Profilanforderungsziele aktivieren](../../ui/activate-profile-request-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Exportierte Daten {#exported-data}

Wenn Sie [Adobe Tags](../../../tags/home.md) Verwenden Sie zum Bereitstellen des Experience Platform Web SDK die [Abschluss des Versandereignisses](../../../edge/extension/event-types.md) -Funktion und Ihre Aktion mit benutzerdefiniertem Code verfügt über eine `event.destinations` -Variable, mit der Sie die exportierten Daten anzeigen können.

Hier finden Sie einen Beispielwert für die `event.destinations` Variable:

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

Wenn Sie [Adobe Tags](../../../tags/home.md) Verwenden Sie zum Bereitstellen des Experience Platform Web SDK die [Umgang mit Antworten von Ereignissen](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) -Funktion, um die exportierten Daten anzuzeigen.

Die JSON-Antwort von Adobe Experience Platform kann analysiert werden, um den entsprechenden Integrationsalias der Anwendung zu finden, die Sie in Adobe Experience Platform integrieren. Die Segment-IDs können als Targeting-Parameter in den Code der Anwendung übergeben werden. Nachfolgend finden Sie ein Beispiel dafür, wie dies spezifisch für die Zielantwort aussehen würde.

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


## Datennutzung und -verwaltung {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, lesen Sie die [Data Governance - Übersicht](../../../data-governance/home.md).
