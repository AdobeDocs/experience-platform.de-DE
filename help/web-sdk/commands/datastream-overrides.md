---
title: Überschreibungen der Datastream-Konfiguration
description: Erfahren Sie, wie Sie über das Web SDK Datastream-Überschreibungen konfigurieren.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 2b8ca4bc1d5cf896820a5de95dcdfcd15edc2392
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 10%

---

# Konfigurieren von Datenstromüberschreibungen

Mit dem Objekt `edgeConfigOverrides` können Sie Konfigurationseinstellungen für Befehle überschreiben, die auf der aktuellen Seite ausgeführt werden. Dieses Override-Objekt ist kein Befehl, sondern ein Objekt, das Sie in die meisten Web SDK-Befehle einbeziehen können.

Dieses Objekt ist nützlich, wenn Sie verschiedene Websites oder Subdomänen für verschiedene Länder haben oder wenn Sie mehrere Experience Platform-Sandboxes zum Speichern von Daten haben, die für verschiedene Geschäftseinheiten spezifisch sind.

>[!IMPORTANT]
>
>Detaillierte, End-to-End-Konfigurationsanweisungen für Datastream-Überschreibungen finden Sie in der Dokumentation [Überschreibungen der Datastream-Konfiguration](../../datastreams/overrides.md#configure-overrides) .

Die Außerkraftsetzung der Datastream-Konfiguration erfolgt in zwei Schritten:

1. Zunächst müssen Sie Ihre Außerkraftsetzung der Datastraam-Konfiguration auf der [Datastream-Konfigurationsseite](../../datastreams/configure.md) in der Benutzeroberfläche von Datastreams definieren. Anweisungen zum Konfigurieren von Überschreibungen finden Sie in der Dokumentation [Überschreibungen der Datastream-Konfiguration](../../datastreams/overrides.md#configure-overrides) .
2. Nachdem Sie das Überschreiben des Datastreams in der Benutzeroberfläche konfiguriert haben, müssen Sie die Überschreibungen auf eine der folgenden Arten an das Edge Network senden:
   * Über die Web SDK [Tag-Erweiterung](#tag-extension).
   * Über die Befehle [`sendEvent`](../commands/sendevent/overview.md) oder [`configure`](../commands/configure/overview.md) Web SDK.
   * Über den Mobile SDK-Befehl [`sendEvent`](https://developer.adobe.com/client-sdks/home/getting-started/track-events/#send-events-to-edge-network).

Wenn Sie Überschreibungen sowohl in der Web SDK-Konfiguration als auch in einem bestimmten Befehl (z. B. [`sendEvent`](sendevent/overview.md)) festlegen, haben die Überschreibungen im spezifischen Befehl Priorität.

>[!NOTE]
>
>Wenn Sie möchten, dass ein Experience Cloud-Dienst durch eine Konfigurationsüberschreibungen *deaktiviert* wird, müssen Sie sicherstellen, dass der Dienst in der Datastream-Konfiguration zuerst *aktiviert* ist. Weitere Informationen zum Hinzufügen von Diensten zu einem Datastream finden Sie in der Dokumentation zum [Konfigurieren von Datastreams](../../datastreams/configure.md#add-services) .

## Senden von Datastream-Überschreibungen an das Edge Network über die Web SDK-Tag-Erweiterung {#tag-extension}

Detaillierte Konfigurationsanweisungen finden Sie in der Dokumentation zu [Konfigurieren von Datastream Overrides](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides) der Web SDK-Tag-Erweiterung.

Wenn Sie Datastream-Überschreibungen aus der Web SDK-Tag-Erweiterung konfigurieren möchten, legen Sie jedes gewünschte Feld unter **[!UICONTROL Datastream-Konfiguration überschreibt]** fest, wenn [die Tag-Erweiterung konfigurieren](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf der Karte [!UICONTROL Adobe Experience Platform Web SDK] auf **[!UICONTROL Konfigurieren]** .
1. Scrollen Sie nach unten zum Abschnitt **[!UICONTROL Datastream configuration overrides]** . Legen Sie jeden gewünschten Überschreibungswert fest.
1. Klicken Sie auf **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

Wenn Sie Überschreibungen nur für einen bestimmten Befehl festlegen möchten, legen Sie jedes gewünschte Feld innerhalb der Aktionen einer Tag-Regel fest.

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Aktionen] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Setzen Sie das Dropdown-Feld [!UICONTROL Erweiterung] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie den Aktionstyp ] auf **[!UICONTROL Ereignis senden]** fest.[!UICONTROL 
1. Scrollen Sie nach unten zum Abschnitt mit der Bezeichnung **[!UICONTROL Außerkraftsetzungen der Datastream-Konfiguration]**.
1. Legen Sie für jedes Feld in diesem Abschnitt den gewünschten Wert zum Außerkraftsetzen fest.
1. Klicken Sie auf **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

Separate Felder werden für die Umgebungen [!UICONTROL Entwicklung], [!UICONTROL Staging] und [!UICONTROL Produktion] bereitgestellt. Vergewissern Sie sich, dass Sie jedes gewünschte Feld für jede Umgebung ausfüllen.

## Senden der Überschreibungen an das Edge Network über die Web SDK JavaScript-Bibliothek {#library}

Nachdem [ das Konfigurieren des Datastreams ](../../datastreams/overrides.md) in der Datenerfassungs-Benutzeroberfläche konfiguriert hat, können Sie die Überschreibungen jetzt über die Web SDK JavaScript-Bibliothek an das Edge Network senden.

Wenn Sie das Web SDK verwenden, ist das Senden der Überschreibungen an das Edge Network über den Befehl `edgeConfigOverrides` der zweite und letzte Schritt bei der Aktivierung von Überschreibungen der Datastream-Konfiguration.

Die Überschreibungen der Datenstromkonfiguration werden über den Web SDK-Befehl `edgeConfigOverrides` gesendet. Mit diesem Befehl werden Datastream-Überschreibungen erstellt, die beim nächsten Befehl an [!DNL Edge Network] übergeben werden. Wenn Sie den Befehl `configure` verwenden, werden die Überschreibungen für jede Anfrage übergeben.

Mit dem Befehl `edgeConfigOverrides` werden Datastream-Überschreibungen erstellt, die beim nächsten Befehl an die [!DNL Edge Network] übergeben werden.

Wenn eine Konfigurationsüberschreibung mit dem Befehl `configure` gesendet wird, ist sie in den folgenden Web SDK-Befehlen enthalten.

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [configure](../commands/configure/overview.md)

Global angegebene Optionen können durch die Konfigurationsoption bei einzelnen Befehlen überschrieben werden.

### Senden von Konfigurationsüberschreibungen über den Web SDK `sendEvent`-Befehl {#send-event}

Das folgende Beispiel zeigt alle Konfigurationsoptionen für dynamische Datastreams, die bei einem `sendEvent` -Aufruf unterstützt werden.

Wenn für Ihre Datastream-Konfiguration alle unterstützten Dienste aktiviert sind, überschreibt das Beispiel unten diese Einstellung und deaktiviert alle Dienste (siehe die Einstellung `enabled: false` für jeden Dienst).

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
      reportSuites: ["ujslconfigoverrides3"],
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

| Parameter | Beschreibung |
|---|---|
| `renderDecisions` |  |
| `edgeConfigOverrides.datastreamId` | Verwenden Sie diesen Parameter, um zuzulassen, dass eine einzelne Anfrage an einen anderen Datenstrom als den vom Befehl `configure` definierten gehen kann. |
| `edgeConfigOverrides.com_adobe_experience_platform` | Definiert die dynamische Datastream-Konfiguration für den Experience Platform-Dienst. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | Definiert, ob das Ereignis an den Experience Platform-Dienst gesendet wird oder nicht. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | Definiert die für das Ereignis verwendeten Datensätze. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | Definiert, ob das Ereignis an den Offer decisioning-Dienst gesendet wird oder nicht. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | Definiert, ob das Ereignis an den Edge Segmentation Service gesendet wird oder nicht. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | Definiert, ob die Ereignisdaten an die Edge-Ziele gesendet werden. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | Definiert, ob die Ereignisdaten an den Adobe Journey Optimizer-Dienst gesendet werden. |
| `com_adobe_analytics.enabled` | Definiert, ob die Ereignisdaten an Adobe Analytics gesendet werden. |
| `com_adobe_analytics.reportSuites[]` | Ein Array von Zeichenfolgen, die bestimmen, an welche Report Suites Sie Analytics-Daten senden möchten. |
| `com_adobe_identity.idSyncContainerId` | Der ID-Synchronisierungs-Container von Drittanbietern, den Sie in Audience Manager verwenden möchten. Damit dieser ID-Synchronisierungscontainer funktioniert, müssen Sie `com_adobe_audience_manager.enabled` auf `true` setzen. Andernfalls ist der Audience Manager-Dienst deaktiviert. |
| `com_adobe_target.enabled` | Definiert, ob die Ereignisdaten an Adobe Target gesendet werden. |
| `com_adobe_target.propertyToken` | Das Token für die Adobe Target-Ziel-Eigenschaft. |
| `com_adobe_audience_manager.enabled` | Definiert, ob die Ereignisdaten an den Audience Manager-Dienst gesendet werden. |
| `com_adobe_launch_ssf` | Definiert, ob die Ereignisdaten an die serverseitige Weiterleitung gesendet werden. |

### Senden von Konfigurationsüberschreibungen über den Web SDK `configure`-Befehl {#send-configure}

Das folgende Beispiel zeigt, wie eine Konfigurationsüberschreibung beim Befehl `configure` aussehen könnte.

Wenn für Ihre Datastream-Konfiguration alle unterstützten Dienste aktiviert sind, überschreibt das Beispiel unten diese Einstellung und deaktiviert alle Dienste (siehe die Einstellung `enabled: false` für jeden Dienst).

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77",
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
      reportSuites: ["ujslconfigoverrides2"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34373,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94",
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

| Parameter | Beschreibung |
|---|---|
| `orgId` | Die IMS-Organisations-ID Ihres Adobe-Kontos. |
| `edgeConfigOverrides.datastreamId` | Verwenden Sie diesen Parameter, um zuzulassen, dass eine einzelne Anfrage an einen anderen Datenstrom als den vom Befehl `configure` definierten gehen kann. |
| `edgeConfigOverrides.com_adobe_experience_platform` | Definiert die dynamische Datastream-Konfiguration für den Experience Platform-Dienst. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | Definiert, ob das Ereignis an den Experience Platform-Dienst gesendet wird oder nicht. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | Definiert die für das Ereignis verwendeten Datensätze. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | Definiert, ob das Ereignis an den Offer decisioning-Dienst gesendet wird oder nicht. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | Definiert, ob das Ereignis an den Edge Segmentation Service gesendet wird oder nicht. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | Definiert, ob die Ereignisdaten an die Edge-Ziele gesendet werden. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | Definiert, ob die Ereignisdaten an den Adobe Journey Optimizer-Dienst gesendet werden. |
| `com_adobe_analytics.enabled` | Definiert, ob die Ereignisdaten an Adobe Analytics gesendet werden. |
| `com_adobe_analytics.reportSuites[]` | Ein Array von Zeichenfolgen, die bestimmen, an welche Report Suites Sie Analytics-Daten senden möchten. |
| `com_adobe_identity.idSyncContainerId` | Der ID-Synchronisierungs-Container von Drittanbietern, den Sie in Audience Manager verwenden möchten. Damit dieser ID-Synchronisierungscontainer funktioniert, müssen Sie `com_adobe_audience_manager.enabled` auf `true` setzen. Andernfalls ist der Audience Manager-Dienst deaktiviert. |
| `com_adobe_target.enabled` | Definiert, ob die Ereignisdaten an Adobe Target gesendet werden. |
| `com_adobe_target.propertyToken` | Das Token für die Adobe Target-Ziel-Eigenschaft. |
| `com_adobe_audience_manager.enabled` | Definiert, ob die Ereignisdaten an den Audience Manager-Dienst gesendet werden. |
| `com_adobe_launch_ssf` | Definiert, ob die Ereignisdaten an die serverseitige Weiterleitung gesendet werden. |

