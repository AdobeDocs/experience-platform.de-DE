---
title: Überschreibungen der Datastream-Konfiguration
description: Erfahren Sie, wie Sie über das Web SDK Datastream-Überschreibungen konfigurieren.
source-git-commit: 9cb46957a1c9755dcad6279aae5f5cc04eb6b305
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 14%

---


# Konfigurieren von Datenstromüberschreibungen

Die `edgeConfigOverrides` -Objekt können Sie Konfigurationseinstellungen für Befehle überschreiben, die auf der aktuellen Seite ausgeführt werden. Dieses Override-Objekt ist kein Befehl, sondern ein Objekt, das Sie in die meisten Web SDK-Befehle einbeziehen können.

Dieses Objekt ist nützlich, wenn Sie verschiedene Websites oder Subdomänen für verschiedene Länder haben oder wenn Sie mehrere Experience Platform-Sandboxes zum Speichern von Daten haben, die für verschiedene Geschäftseinheiten spezifisch sind.

>[!IMPORTANT]
>
>Detaillierte End-to-End-Konfigurationsanweisungen für Datastream-Überschreibungen finden Sie in der [Überschreibungen der Datenspeicherkonfiguration](../../datastreams/overrides.md#configure-overrides) Dokumentation.

Die Außerkraftsetzung der Datastream-Konfiguration erfolgt in zwei Schritten:

1. Zunächst müssen Sie Ihre Datastream-Konfigurationsüberschreibungen im [Datastream-Konfigurationsseite](../../datastreams/configure.md), in der Benutzeroberfläche von Datastreams. Siehe [Überschreibungen der Datenspeicherkonfiguration](../../datastreams/overrides.md#configure-overrides) Dokumentation für Anweisungen zum Konfigurieren von Außerkraftsetzungen.
2. Nachdem Sie das Überschreiben des Datastreams in der Benutzeroberfläche konfiguriert haben, müssen Sie die Überschreibungen auf eine der folgenden Arten an das Edge-Netzwerk senden:
   * Über das Web SDK [Tag-Erweiterung](#tag-extension).
   * Durch die `sendEvent` oder `configure` Web SDK-Befehle.
   * Über das Mobile SDK `sendEvent` Befehl.

Wenn Sie Überschreibungen sowohl in der Web SDK-Konfiguration als auch in einem bestimmten Befehl festlegen (z. B. [`sendEvent`](sendevent/overview.md)), haben die Überschreibungen im spezifischen Befehl Priorität.

## Objekteigenschaften

Die folgenden Eigenschaften sind in diesem Objekt verfügbar:

* **Datastream override**: Senden Sie Aufrufe an einen anderen Datenspeicher. Wenn Sie diesen Wert festlegen, müssen andere Überschreibungen, die eine Konfiguration des Datenspeichers erfordern, im hier festgelegten Datastream konfiguriert werden.
* **ID-Synchronisierungs-Container von Drittanbietern**: Die ID für den Ziel-ID-Synchronisierungs-Container von Drittanbietern in Adobe Audience Manager. Bevor Sie dieses Feld verwenden, ist es erforderlich, einen Drittanbieter-ID-Container zu konfigurieren, der in den Einstellungen des Datenspeichers überschrieben wird.
* **Target-Eigenschafts-Token**: Das Token für die Ziel-Property in Adobe Target. Bevor Sie dieses Feld verwenden, ist es erforderlich, eine Target-Eigenschafts-Token-Überschreibung in den Einstellungen des Datastreams zu konfigurieren.
* **Report Suites**: Die Report Suite-IDs, die in Adobe Analytics überschrieben werden sollen. Vor der Verwendung dieses Felds ist es erforderlich, die Report Suite-Überschreibung in den Einstellungen des Datenspeichers zu konfigurieren.

## Senden von Datastream-Überschreibungen an das Edge-Netzwerk über die Web SDK-Tag-Erweiterung {#tag-extension}

Siehe die Dokumentation unter [Konfigurieren von Überschreibungen von Datastreams](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides) von der Web SDK-Tag-Erweiterung , um detaillierte Konfigurationsanweisungen zu erhalten.

Wenn Sie Datastream-Überschreibungen aus der Web SDK-Tag-Erweiterung konfigurieren möchten, legen Sie jedes gewünschte Feld unter **[!UICONTROL Überschreibungen der Datastream-Konfiguration]** when [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Scrollen Sie nach unten zum **[!UICONTROL Überschreibungen der Datastream-Konfiguration]** Abschnitt. Legen Sie jeden gewünschten Überschreibungswert fest.
1. Klicks **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

Wenn Sie Überschreibungen nur für einen bestimmten Befehl festlegen möchten, legen Sie jedes gewünschte Feld innerhalb der Aktionen einer Tag-Regel fest.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. under [!UICONTROL Aktionen], wählen Sie eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie die [!UICONTROL Erweiterung] Dropdown-Feld zu **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie die [!UICONTROL Aktionstyp] nach **[!UICONTROL Ereignis senden]**.
1. Scrollen Sie nach unten zum Abschnitt mit der Bezeichnung **[!UICONTROL Überschreibungen der Datastream-Konfiguration]**.
1. Legen Sie für jedes Feld in diesem Abschnitt den gewünschten Wert zum Außerkraftsetzen fest.
1. Klicks **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

Separate Felder werden bereitgestellt für [!UICONTROL Entwicklung], [!UICONTROL Staging], und [!UICONTROL Produktion] Umgebungen. Vergewissern Sie sich, dass Sie jedes gewünschte Feld für jede Umgebung ausfüllen.

## Senden der Überschreibungen an das Edge-Netzwerk über die Web SDK-JavaScript-Bibliothek {#library}

Nachher [Konfigurieren der Überschreibungen des Datastreams](../../datastreams/overrides.md) In der Datenerfassungs-Benutzeroberfläche können Sie die Überschreibungen jetzt über die Web SDK-JavaScript-Bibliothek an das Edge-Netzwerk senden.

Wenn Sie das Web SDK verwenden, senden Sie die Überschreibungen über das `edgeConfigOverrides` -Befehl ist der zweite und letzte Schritt zum Aktivieren von Überschreibungen der Datastream-Konfiguration.

Die Überschreibungen der Datenstromkonfiguration werden über den Web SDK-Befehl `edgeConfigOverrides` gesendet. Mit diesem Befehl werden Datastream-Überschreibungen erstellt, die an die [!DNL Edge Network] auf dem nächsten Befehl. Wenn Sie die `configure` -Befehl, werden die Überschreibungen für jede Anfrage übergeben.

Die `edgeConfigOverrides` -Befehl erstellt Datastream-Überschreibungen, die an die [!DNL Edge Network] auf dem nächsten Befehl.

Wenn eine Konfigurationsüberschreibung mit dem Befehl `configure` gesendet wird, ist sie in den folgenden Web SDK-Befehlen enthalten.

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [configure](../commands/configure/overview.md)

Global angegebene Optionen können durch die Konfigurationsoption bei einzelnen Befehlen überschrieben werden.

### Senden von Konfigurationsüberschreibungen über das Web SDK `sendEvent` command {#send-event}

Das folgende Beispiel zeigt, wie eine Konfigurationsüberschreibung beim Befehl `sendEvent` aussehen könnte.

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
    datastreamId: "{DATASTREAM_ID}"
    com_adobe_experience_platform: {
      datasets: {
        event: {
          datasetId: "SampleEventDatasetIdOverride"
        }
      }
    },
    com_adobe_analytics: {
      reportSuites: [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
        ]
    },
    com_adobe_identity: {
      idSyncContainerId: "1234567"
    },
    com_adobe_target: {
      propertyToken: "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  }
});
```

| Parameter | Beschreibung |
|---|---|
| `edgeConfigOverrides.datastreamId` | Verwenden Sie diesen Parameter, um zuzulassen, dass eine einzelne Anfrage an einen anderen Datenstrom als den vom Befehl `configure` definierten gehen kann. |
| `com_adobe_analytics.reportSuites[]` | Ein Array von Zeichenfolgen, die bestimmen, an welche Report Suites Analytics-Daten senden möchten. |
| `com_adobe_identity.idSyncContainerId` | Der ID-Synchronisierungs-Container von Drittanbietern, den Sie in Audience Manager verwenden möchten. |
| `com_adobe_target.propertyToken` | Das Token für die Adobe Target-Ziel-Eigenschaft. |

### Senden von Konfigurationsüberschreibungen über das Web SDK `configure` command {#send-configure}

Das folgende Beispiel zeigt, wie eine Konfigurationsüberschreibung beim Befehl `configure` aussehen könnte.

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  datastreamId: "{DATASTREAM_ID}",
  orgId: "org",
  debugEnabled: true,
  edgeConfigOverrides: {
    "com_adobe_experience_platform": {
      "datasets": {
        "event": {
          datasetId: "SampleProfileDatasetIdOverride"
        }
      }
    },
    "com_adobe_analytics": {
      "reportSuites": [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
      ]
    },
    "com_adobe_identity": {
      "idSyncContainerId": "1234567"
    },
    "com_adobe_target": {
      "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  },
  onBeforeEventSend: function() { /* … */ });
};
```

| Parameter | Beschreibung |
|---|---|
| `edgeConfigOverrides.datastreamId` | Verwenden Sie diesen Parameter, um zuzulassen, dass eine einzelne Anfrage an einen anderen Datenstrom als den vom Befehl `configure` definierten gehen kann. |
| `com_adobe_analytics.reportSuites[]` | Ein Array von Zeichenfolgen, die bestimmen, an welche Report Suites Analytics-Daten senden möchten. |
| `com_adobe_identity.idSyncContainerId` | Der ID-Synchronisierungs-Container von Drittanbietern, den Sie in Audience Manager verwenden möchten. |
| `com_adobe_target.propertyToken` | Das Token für die Adobe Target-Ziel-Eigenschaft. |