---
title: Überschreibungen der Datastream-Konfiguration
description: Erfahren Sie, wie Sie über das Web SDK Datastream-Überschreibungen konfigurieren.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 14%

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
   * Über die Befehle `sendEvent` oder `configure` Web SDK.
   * Über den Mobile SDK-Befehl `sendEvent`.

Wenn Sie Überschreibungen sowohl in der Web SDK-Konfiguration als auch in einem bestimmten Befehl (z. B. [`sendEvent`](sendevent/overview.md)) festlegen, haben die Überschreibungen im spezifischen Befehl Priorität.

## Objekteigenschaften

Die folgenden Eigenschaften sind in diesem Objekt verfügbar:

* **Datastream override**: Senden Sie Aufrufe an einen anderen Datastream. Wenn Sie diesen Wert festlegen, müssen andere Überschreibungen, die eine Konfiguration des Datenspeichers erfordern, im hier festgelegten Datastream konfiguriert werden.
* **ID-Synchronisierungscontainer von Drittanbietern**: Die ID für den ID-Synchronisierungscontainer von Drittanbietern in Adobe Audience Manager. Bevor Sie dieses Feld verwenden, ist es erforderlich, einen Drittanbieter-ID-Container zu konfigurieren, der in den Einstellungen des Datenspeichers überschrieben wird.
* **Target-Eigenschafts-Token**: Das Token für die Ziel-Eigenschaft in Adobe Target. Bevor Sie dieses Feld verwenden, ist es erforderlich, eine Target-Eigenschafts-Token-Überschreibung in den Einstellungen des Datastreams zu konfigurieren.
* **Report Suites**: Die Report Suite-IDs, die in Adobe Analytics überschrieben werden sollen. Vor der Verwendung dieses Felds ist es erforderlich, die Report Suite-Überschreibung in den Einstellungen des Datenspeichers zu konfigurieren.

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

### Senden von Konfigurationsüberschreibungen über den Web SDK `configure`-Befehl {#send-configure}

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
