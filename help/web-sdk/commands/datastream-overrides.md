---
title: Überschreibungen der Datenstromkonfiguration
description: Erfahren Sie, wie Sie Datenstrom-Überschreibungen über die Web-SDK konfigurieren.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 2b8ca4bc1d5cf896820a5de95dcdfcd15edc2392
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 10%

---

# Konfigurieren von Datenstromüberschreibungen

Mit dem `edgeConfigOverrides`-Objekt können Sie Konfigurationseinstellungen für Befehle überschreiben, die auf der aktuellen Seite ausgeführt werden. Dieses Überschreibungsobjekt ist kein Befehl, sondern ein Objekt, das Sie in die meisten Web SDK-Befehle einbeziehen können.

Dieses Objekt ist nützlich, wenn Sie unterschiedliche Websites oder Subdomains für verschiedene Länder haben oder wenn Sie mehrere Experience Platform-Sandboxes haben, um Daten zu speichern, die für verschiedene Geschäftseinheiten spezifisch sind.

>[!IMPORTANT]
>
>Detaillierte End-to-End-Konfigurationsanweisungen für Datenstromüberschreibungen finden Sie in der Dokumentation [Datenstromkonfigurationsüberschreibungen](../../datastreams/overrides.md#configure-overrides).

Die Überschreibung der Datenstromkonfiguration ist ein zweistufiger Prozess:

1. Zunächst müssen Sie in der Datenstrom-Benutzeroberfläche auf der Seite [Datenstromkonfiguration“ ](../../datastreams/configure.md) Überschreiben der Datenstromkonfiguration definieren. Anweisungen [ Konfigurieren von Überschreibungen finden Sie ](../../datastreams/overrides.md#configure-overrides) der Dokumentation zu Datenstromkonfigurationsüberschreibungen .
2. Nachdem Sie die Datenstrom-Überschreibung in der Benutzeroberfläche konfiguriert haben, müssen Sie die Überschreibungen auf eine der folgenden Arten an das Edge Network senden:
   * Über die Web-SDK [Tag-Erweiterung](#tag-extension).
   * Über die [`sendEvent`](../commands/sendevent/overview.md) oder [`configure`](../commands/configure/overview.md) Web SDK-Befehle.
   * Über den [`sendEvent`](https://developer.adobe.com/client-sdks/home/getting-started/track-events/#send-events-to-edge-network)-Befehl Mobile SDK .

Wenn Sie Überschreibungen sowohl in der Web-SDK-Konfiguration als auch in einem bestimmten Befehl (z. B. [`sendEvent`](sendevent/overview.md)) festlegen, haben die Überschreibungen im jeweiligen Befehl Vorrang.

>[!NOTE]
>
>Wenn Sie möchten, dass ein Experience Cloud-Service durch *Konfiguration* (deaktiviert) wird, müssen Sie sicherstellen, dass der Service in *Datenstromkonfiguration* (aktiviert) ist. Weitere Informationen zum Hinzufügen von [ zu einem Datenstrom finden Sie in ](../../datastreams/configure.md#add-services) Dokumentation zum Konfigurieren von Datenströmen .

## Senden von Datenstrom-Überschreibungen an das Edge Network über die Tag-Erweiterung „Web SDK&quot; {#tag-extension}

Detaillierte Konfigurationsanweisungen finden Sie in der Dokumentation [Konfigurieren von Datenstrom](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides)Überschreibungen über die Tag-Erweiterung von Web SDK .

Wenn Sie Datenstrom-Überschreibungen aus der Web SDK-Tag-Erweiterung konfigurieren möchten, legen Sie jedes gewünschte Feld unter &quot;**[!UICONTROL von Datenstrom-Konfigurationen]** beim [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) fest.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]** auf der Karte [!UICONTROL Adobe Experience Platform Web SDK].
1. Scrollen Sie nach unten zum Abschnitt **[!UICONTROL Überschreibungen der Datenstromkonfiguration]**. Legen Sie jeden gewünschten Überschreibungswert fest.
1. Klicken Sie **[!UICONTROL Speichern]** und veröffentlichen Sie Ihre Änderungen.

Wenn Sie Überschreibungen nur für einen bestimmten Befehl festlegen möchten, legen Sie jedes gewünschte Feld in den Aktionen einer Tag-Regel fest.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen [!UICONTROL  unter &quot;]&quot; eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie das [!UICONTROL Erweiterung] Dropdown-Feld auf **[!UICONTROL Adobe Experience Platform Web SDK]** fest und legen Sie den [!UICONTROL Aktionstyp] auf **[!UICONTROL Ereignis senden]**.
1. Scrollen Sie nach unten zum Abschnitt mit **[!UICONTROL Überschreibungen der Datenstromkonfiguration]**.
1. Legen Sie für jedes Feld in diesem Abschnitt den gewünschten Überschreibungswert fest.
1. Klicken Sie **[!UICONTROL Änderungen beibehalten]** und führen Sie dann den Veröffentlichungs-Workflow aus.

Für die Umgebungen [!UICONTROL Entwicklung], [!UICONTROL Staging] und [!UICONTROL Produktion] werden separate Felder bereitgestellt. Stellen Sie sicher, dass Sie jedes gewünschte Feld für jede Umgebung ausfüllen.

## Senden Sie die Überschreibungen über die Web-SDK-JavaScript-Bibliothek an das Edge Network {#library}

Nach [Konfigurieren der Datenstrom-Überschreibungen](../../datastreams/overrides.md) in der Datenerfassungs-Benutzeroberfläche können Sie die Überschreibungen jetzt über die Web-SDK-JavaScript-Bibliothek an das -Edge Network senden.

Wenn Sie Web SDK verwenden, ist das Senden der Überschreibungen an das Edge Network über den `edgeConfigOverrides` der zweite und letzte Schritt zum Aktivieren von Überschreibungen der Datenstromkonfiguration.

Die Überschreibungen der Datenstromkonfiguration werden über den Web SDK-Befehl `edgeConfigOverrides` gesendet. Dieser Befehl erstellt Datenstrom-Überschreibungen, die beim nächsten Befehl an den [!DNL Edge Network] übergeben werden. Wenn Sie den `configure`-Befehl verwenden, werden die Überschreibungen für jede Anfrage übergeben.

Der Befehl `edgeConfigOverrides` erstellt Datenstromüberschreibungen, die beim nächsten Befehl an den [!DNL Edge Network] übergeben werden.

Wenn eine Konfigurationsüberschreibung mit dem Befehl `configure` gesendet wird, ist sie in den folgenden Web SDK-Befehlen enthalten.

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [configure](../commands/configure/overview.md)

Global angegebene Optionen können durch die Konfigurationsoption bei einzelnen Befehlen überschrieben werden.

### Senden von Konfigurationsüberschreibungen über den `sendEvent`-Befehl von Web SDK {#send-event}

Das folgende Beispiel zeigt alle dynamischen Datenstromkonfigurationsoptionen, die bei einem `sendEvent`-Aufruf unterstützt werden.

Wenn in Ihrer Datenstromkonfiguration alle unterstützten Services aktiviert sind, überschreibt das folgende Beispiel diese Einstellung und deaktiviert alle Services (siehe die `enabled: false` für jeden Service).

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
| `edgeConfigOverrides.com_adobe_experience_platform` | Definiert die Konfiguration des dynamischen Datenstroms für den Experience Platform-Service. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | Definiert, ob das Ereignis an den Experience Platform-Service gesendet wird oder nicht. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | Definiert die für das Ereignis verwendeten Datensätze. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | Definiert, ob das Ereignis an den Offer decisioning-Service gesendet wird oder nicht. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | Definiert, ob das Ereignis an den Edge-Segmentierungs-Service gesendet wird oder nicht. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | Definiert, ob die Ereignisdaten an die Edge-Ziele gesendet werden oder nicht. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | Definiert, ob die Ereignisdaten an den Adobe Journey Optimizer-Service gesendet werden oder nicht. |
| `com_adobe_analytics.enabled` | Definiert, ob die Ereignisdaten an Adobe Analytics gesendet werden oder nicht. |
| `com_adobe_analytics.reportSuites[]` | Ein Array von Zeichenfolgen, das bestimmt, an welche Report Suites Sie Analytics-Daten senden möchten. |
| `com_adobe_identity.idSyncContainerId` | Der Synchronisierungs-Container für Drittanbieter-IDs, den Sie im Audience Manager verwenden möchten. Damit dieser ID-Synchronisierungs-Container funktioniert, müssen Sie `com_adobe_audience_manager.enabled` auf `true` setzen. Andernfalls ist der Audience Manager-Service deaktiviert. |
| `com_adobe_target.enabled` | Definiert, ob die Ereignisdaten an Adobe Target gesendet werden. |
| `com_adobe_target.propertyToken` | Das Token für die Adobe Target-Zieleigenschaft. |
| `com_adobe_audience_manager.enabled` | Definiert, ob die Ereignisdaten an den Audience Manager-Service gesendet werden. |
| `com_adobe_launch_ssf` | Definiert, ob die Ereignisdaten an die Server-seitige Weiterleitung gesendet werden. |

### Senden von Konfigurationsüberschreibungen über den `configure`-Befehl von Web SDK {#send-configure}

Das folgende Beispiel zeigt, wie eine Konfigurationsüberschreibung beim Befehl `configure` aussehen könnte.

Wenn in Ihrer Datenstromkonfiguration alle unterstützten Services aktiviert sind, überschreibt das folgende Beispiel diese Einstellung und deaktiviert alle Services (siehe die `enabled: false` für jeden Service).

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
| `orgId` | Die IMS-Organisations-ID, die Ihrem Adobe-Konto entspricht. |
| `edgeConfigOverrides.datastreamId` | Verwenden Sie diesen Parameter, um zuzulassen, dass eine einzelne Anfrage an einen anderen Datenstrom als den vom Befehl `configure` definierten gehen kann. |
| `edgeConfigOverrides.com_adobe_experience_platform` | Definiert die Konfiguration des dynamischen Datenstroms für den Experience Platform-Service. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | Definiert, ob das Ereignis an den Experience Platform-Service gesendet wird oder nicht. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | Definiert die für das Ereignis verwendeten Datensätze. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | Definiert, ob das Ereignis an den Offer decisioning-Service gesendet wird oder nicht. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | Definiert, ob das Ereignis an den Edge-Segmentierungs-Service gesendet wird oder nicht. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | Definiert, ob die Ereignisdaten an die Edge-Ziele gesendet werden oder nicht. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | Definiert, ob die Ereignisdaten an den Adobe Journey Optimizer-Service gesendet werden oder nicht. |
| `com_adobe_analytics.enabled` | Definiert, ob die Ereignisdaten an Adobe Analytics gesendet werden oder nicht. |
| `com_adobe_analytics.reportSuites[]` | Ein Array von Zeichenfolgen, das bestimmt, an welche Report Suites Sie Analytics-Daten senden möchten. |
| `com_adobe_identity.idSyncContainerId` | Der Synchronisierungs-Container für Drittanbieter-IDs, den Sie im Audience Manager verwenden möchten. Damit dieser ID-Synchronisierungs-Container funktioniert, müssen Sie `com_adobe_audience_manager.enabled` auf `true` setzen. Andernfalls ist der Audience Manager-Service deaktiviert. |
| `com_adobe_target.enabled` | Definiert, ob die Ereignisdaten an Adobe Target gesendet werden. |
| `com_adobe_target.propertyToken` | Das Token für die Adobe Target-Zieleigenschaft. |
| `com_adobe_audience_manager.enabled` | Definiert, ob die Ereignisdaten an den Audience Manager-Service gesendet werden. |
| `com_adobe_launch_ssf` | Definiert, ob die Ereignisdaten an die Server-seitige Weiterleitung gesendet werden. |

