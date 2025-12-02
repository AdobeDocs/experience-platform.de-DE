---
title: edgeConfigOverrides
description: Konfigurieren von Datenstrom-Überschreibungen für Ihre Implementierung.
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# `edgeConfigOverrides` (`configure` Befehl)

Mit dem `edgeConfigOverrides`-Objekt können Sie Konfigurationseinstellungen für Befehle überschreiben, die auf der aktuellen Seite ausgeführt werden. Dieses Objekt ist nützlich, wenn Sie unterschiedliche Websites oder Subdomains für verschiedene Länder haben oder wenn Sie mehrere Experience Platform-Sandboxes haben, um Daten zu speichern, die für verschiedene Geschäftseinheiten spezifisch sind. Wenn Sie die Konfigurationseinstellungen nur für einen einzelnen Befehl auf der Seite überschreiben möchten, sollten Sie das [`edgeConfigOverrides`-Objekt im `sendEvent` verwenden](../sendevent/edgeconfigoverrides.md).

Der Überschreibungsprozess der Datenstromkonfiguration besteht aus zwei Hauptschritten:

1. Zunächst müssen Sie in der Datenstrom-Benutzeroberfläche [ Überschreiben der Datenstromkonfiguration definieren](/help/datastreams/configure.md) wenn Sie einen Datenstrom konfigurieren. Anweisungen [ Konfigurieren von Überschreibungen finden Sie ](/help/datastreams/overrides.md)Überschreibungen der Datenstromkonfiguration“ in der Dokumentation zu Datenströmen.
1. Nachdem Sie die Datenstrom-Überschreibung in der Datenstrom-Benutzeroberfläche konfiguriert haben, können Sie das `edgeConfigOverrides`-Objekt konfigurieren.

Wenn Sie das `edgeConfigOverrides` -Objekt im `configure` festlegen, gilt dies für alle Daten, die an Adobe gesendet werden. Die folgenden Befehle _auch_ unterstützen das `edgeConfigOverrides`:

* [`sendEvent`](../sendevent/edgeconfigoverrides.md)
* [`setConsent`](../setconsent.md)
* [`getIdentity`](../getidentity.md)
* [`appendIdentityToUrl`](../appendidentitytourl.md)

Wenn beide Werte festgelegt sind, hat das Festlegen von `edgeConfigOverrides` in einem der oben genannten Befehle Vorrang vor dem `edgeConfigOverrides`-Objekt im `configure`. Wenn einer dieser Befehle kein `edgeConfigOverrides`-Objekt enthält, wird das `edgeConfigOverrides`-Objekt im `configure`-Befehl verwendet.

## Beispiel

Wenn in Ihrer Datenstromkonfiguration alle unterstützten Services aktiviert sind, überschreibt das folgende Beispiel diese Einstellung und deaktiviert alle Services.

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77"
        }
      },
      com_adobe_edge_ode: {
        enabled: false
      },
      com_adobe_edge_segmentation: {
        enabled: false
      },
      com_adobe_edge_destinations: {
        enabled: false
      },
      com_adobe_edge_ajo: {
        enabled: false
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["exampleoverridersid","exampleoverridersid2"]
    },
    com_adobe_identity: {
      idSyncContainerId: 34373
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94"
    },
    com_adobe_audience_manager: {
      enabled: false
    },
    com_adobe_launch_ssf: {
      enabled: false
    }
  }
});
```

| Parameter | Typ | Beschreibung |
| --- | --- | --- |
| **`orgId`** | `string` | Die IMS-Organisations-ID Ihres Unternehmens. |
| **`datastreamId`** | `string` | Die Datenstrom-ID, an die Daten gesendet werden sollen. |
| **`com_adobe_experience_platform`** | `object` | Definiert die Konfiguration des dynamischen Datenstroms für Adobe Experience Platform-Services. |
| **`com_adobe_experience_platform.enabled`** | `boolean` | Bestimmt, ob das Ereignis an Adobe Experience Platform gesendet wird. |
| **`com_adobe_experience_platform.datasets`** | `object` | Definiert die für das Ereignis verwendeten Datensätze. |
| **`com_adobe_experience_platform.com_adobe_edge_ode.enabled`** | `boolean` | Bestimmt, ob das Ereignis an Offer Decisioning gesendet wird. |
| **`com_adobe_experience_platform.com_adobe_edge_segmentation.enabled`** | `boolean` | Bestimmt, ob das Ereignis an die Edge-Segmentierung gesendet wird. |
| **`com_adobe_experience_platform.com_adobe_edge_destinations.enabled`** | `boolean` | Bestimmt, ob das Ereignis an Edge-Ziele gesendet wird. |
| **`com_adobe_experience_platform.com_adobe_edge_ajo.enabled`** | `boolean` | Bestimmt, ob das Ereignis an Adobe Journey Optimizer gesendet wird. |
| **`com_adobe_analytics.enabled`** | `boolean` | Bestimmt, ob das Ereignis an Adobe Analytics gesendet wird. |
| **`com_adobe_analytics.reportSuites[]`** | `string[]` | Ein Array von Zeichenfolgen, das bestimmt, an welche Report Suites Analytics-Daten gesendet werden sollen. |
| **`com_adobe_audience_manager.enabled`** | `boolean` | Bestimmt, ob das Ereignis an Adobe Audience Manager gesendet wird. |
| **`com_adobe_identity.idSyncContainerId`** | `integer` | Der Synchronisierungs-Container für Drittanbieter-IDs, den Sie in Audience Manager verwenden möchten. Erfordert, dass `com_adobe_audience_manager.enabled` auf `true` gesetzt ist. Andernfalls ist der Audience Manager-Service deaktiviert. |
| **`com_adobe_target.enabled`** | `boolean` | Bestimmt, ob das Ereignis an Adobe Target gesendet wird. |
| **`com_adobe_target.propertyToken`** | `string` | Das Token für die Adobe Target-Zieleigenschaft. |
| **`com_adobe_launch_ssf`** | `boolean` | Bestimmt, ob das Ereignis an die Server-seitige Weiterleitung gesendet wird. |

## Konfigurationsüberschreibungen mithilfe der Tag-Erweiterung „Web SDK&quot;

Die Web SDK-Tag-Erweiterung, die diesem Feld entspricht, befindet sich unter [Konfigurationsüberschreibungen](/help/tags/extensions/client/web-sdk/configure/configuration-overrides.md) beim Konfigurieren der Tag-Erweiterung.
