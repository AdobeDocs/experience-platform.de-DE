---
title: edgeConfigOverrides
description: Konfigurieren Sie Datenstromüberschreibungen nur für den Befehl sendEvent .
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# `edgeConfigOverrides` (`sendEvent` Befehl)

Mit dem `edgeConfigOverrides`-Objekt können Sie Konfigurationseinstellungen nur für den aktuellen `sendEvent`-Befehl überschreiben. Dieses Objekt ist nützlich, wenn sich auf derselben Seite spezifische Befehle befinden, die mit anderen Konfigurationseinstellungen als die restliche Web SDK-Implementierung ausgeführt werden sollen. Wenn Sie die Konfigurationseinstellungen für alle Befehle auf einer bestimmten Seite überschreiben möchten, sollten Sie das [`edgeConfigOverrides`-Objekt im `configure` verwenden](../configure/edgeconfigoverrides.md).

Der übergeordnete Prozess zur Außerkraftsetzung der Datenstromkonfiguration besteht aus zwei Hauptschritten:

1. Zunächst müssen Sie in der Datenstrom-Benutzeroberfläche [&#x200B; Überschreiben der Datenstromkonfiguration definieren](/help/datastreams/configure.md) wenn Sie einen Datenstrom konfigurieren. Anweisungen [&#x200B; Konfigurieren von Überschreibungen finden Sie &#x200B;](/help/datastreams/overrides.md)Überschreibungen der Datenstromkonfiguration“ in der Dokumentation zu Datenströmen.
1. Nachdem Sie die Datenstrom-Überschreibung in der Datenstrom-Benutzeroberfläche konfiguriert haben, können Sie das `edgeConfigOverrides`-Objekt konfigurieren.

Beachten Sie, dass der `configure`-Befehl auch ein `edgeConfigOverrides`-Objekt unterstützt; siehe [`edgeConfigOverrides`](../configure/edgeconfigoverrides.md) unter dem `configure`-Befehl. Das `edgeConfigOverrides` Objekt im `sendEvent`-Befehl hat Vorrang vor dem `edgeConfigOverrides` Objekt im `configure`-Befehl, wenn beide festgelegt sind.

## Beispiel

Wenn in Ihrer Datenstromkonfiguration alle unterstützten Services aktiviert sind, überschreibt das folgende Beispiel diese Einstellung und deaktiviert alle Services (siehe die `enabled: false` für jeden Service). Dieses Objekt unterstützt dieselben Eigenschaften wie das [`edgeConfigOverrides`](../configure/edgeconfigoverrides.md) im `configure`.

```js
alloy("sendEvent", {
  renderDecisions: true,
  edgeConfigOverrides: {
    datastreamId: "bfa8fe21-6157-42d3-b47a-78310920b39d",
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f949a8a6891ca8a28911",
        },
      },
      com_adobe_edge_ode: {
        enabled: false,
      },
      com_adobe_edge_segmentation: {
        enabled: false,
      },
      com_adobe_edge_destinations: {
        enabled: false,
      },
      com_adobe_edge_ajo: {
        enabled: false,
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["examplersid3"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34374,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "f3fd55e1-a06d-8650-9aa5-c8356c6e2223",
    },
    com_adobe_audience_manager: {
      enabled: false,
    },
    com_adobe_launch_ssf: {
      enabled: false,
    },
  },
});
```

## Überschreibungen der Datenstromkonfiguration mithilfe der Tag-Erweiterung Web SDK

Die Web SDK-Tag-Erweiterung, die diesem Objekt entspricht, ist der Abschnitt [Überschreibungen der Datenstromkonfiguration](/help/tags/extensions/client/web-sdk/actions/send-event.md#datastream-configuration-overrides) beim Konfigurieren der Aktion &quot;[!UICONTROL Send event]&quot;.
