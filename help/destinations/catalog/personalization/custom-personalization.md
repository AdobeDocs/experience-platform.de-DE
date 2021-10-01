---
keywords: benutzerdefinierte Personalisierung; Bestimmungsort; Benutzerdefiniertes Ziel der Erlebnisplattform;
title: Benutzerdefinierte Personalisierungsverbindung (Beta)
description: Dieses Ziel bietet eine externe Personalisierung, Content Management-Systeme, Anzeigen-Server und andere Anwendungen, die auf Ihrer Site ausgeführt werden, um Segmentinformationen aus Adobe Experience Platform abzurufen. Dieses Ziel bietet 1:1-Echtzeit-Personalisierung und basiert auf der Segmentmitgliedschaft eines Benutzerprofils.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: ba27484655438df654a1e062309ddd30638f62a5
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 8%

---

# Benutzerdefinierte Personalisierungsverbindung (Beta) {#custom-personalization-connection}

## Übersicht {#overview}

>[!IMPORTANT]
>
>Die Verbindung zur benutzerdefinierten Personalisierung in Adobe Experience Platform befindet sich derzeit in der Betaversion. Dokumentation und Funktionalität können sich ändern.

Dieses Ziel bietet eine Möglichkeit, Segmentinformationen von Adobe Experience Platform zu externen Personalisierungsplattformen, Content-Management-Systemen, Anzeigen-Servern und anderen Anwendungen abzurufen, die auf Kunden-Websites ausgeführt werden.

## Voraussetzungen {#prerequisites}

Diese Integration basiert auf dem [Adobe Experience Platform Web SDK](../../../edge/home.md). Sie müssen dieses SDK verwenden, um dieses Ziel zu verwenden.

## Exporttyp {#export-type}

**Profilanfrage** : Sie fordern alle Segmente an, die im benutzerdefinierten Personalisierungsziel für ein einzelnes Profil zugeordnet sind. Für verschiedene [Datenerfassungs-Datenspeicher der Adobe](../../../edge/fundamentals/datastreams.md) können verschiedene benutzerdefinierte Personalisierungsziele eingerichtet werden.

## Anwendungsfälle {#use-cases}

Dieses Ziel teilt Zielgruppen mit Adservern und Nicht-Adobe-Personalisierungsanwendungen, die in Echtzeit verwendet werden, um zu entscheiden, welche Advertising-Benutzer auf einer Website sehen sollen.

### Anwendungsfall 1

**Personalisieren einer Startseite**

Eine Website zum Vermieten und Verkaufen möchte ihre Startseite anhand von Segmentqualifikationen in Adobe Experience Platform personalisieren. Das Unternehmen kann auswählen, welche Zielgruppen ein personalisiertes Erlebnis erhalten sollen, und diese Zielgruppen dem benutzerdefinierten Personalisierungsziel zuordnen, das für seine Nicht-Adobe-Personalisierungsanwendung als Targeting-Kriterien eingerichtet wurde.

**Targeting-Onsite-Werbung**

Mithilfe eines separaten benutzerdefinierten Personalisierungsziels für den Anzeigenserver kann dieselbe Website für die Werbung auf der Site einen anderen Satz von Segmenten aus Adobe Experience Platform als Targeting-Kriterien verwenden.

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden. Dieses Feld ist optional.
* **[!UICONTROL Integrationsalias]**: Dieser Wert wird als JSON-Objektname an das Experience Platform Web SDK gesendet.
* **[!UICONTROL Datastream-ID]**: Dadurch wird bestimmt, in welchem Datenerfassungsdatenstrom die Segmente in die Antwort auf die Seite aufgenommen werden. Das Dropdown-Menü zeigt nur Datensätze an, für die die Zielkonfiguration aktiviert ist. Weitere Informationen finden Sie unter [Konfigurieren eines Datastreams](../../../edge/fundamentals/datastreams.md) .

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Profile und Segmente für Profilanfrageziele aktivieren](../../ui/activate-profile-request-destinations.md) .

## Exportierte Daten {#exported-data}

Wenn Sie [Adobe-Tags](../../../tags/home.md) zum Bereitstellen des Experience Platform Web SDK verwenden, verwenden Sie die Funktion [Ereignis-Abschluss senden](../../../edge/extension/event-types.md) und Ihre benutzerdefinierte Codeaktion verfügt über eine `event.destinations`-Variable, mit der Sie die exportierten Daten anzeigen können.

Wenn Sie [Adobe-Tags](../../../tags/home.md) nicht zum Bereitstellen des Experience Platform Web SDK verwenden, verwenden Sie die Funktion [Verarbeiten von Antworten aus Ereignissen](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events), um die exportierten Daten anzuzeigen.

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
}).then(function(results) {
    if(results.destinations) { // Looking to see if the destination results are there
 
        // Get the destination with a particular alias
        var personalizationDestinations = results.destinations.filter(x => x.alias == “personalizationAlias”)
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = results.destinations.filter(x => x.alias == “adServerAlias”)
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

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen dazu, wie [!DNL Adobe Experience Platform] Data Governance durchsetzt, finden Sie unter [Übersicht über Data Governance](../../../data-governance/home.md).
