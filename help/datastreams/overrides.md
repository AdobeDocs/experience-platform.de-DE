---
title: Konfigurieren von Datenstromüberschreibungen
description: Erfahren Sie, wie Sie Datenstromüberschreibungen in der Datenstrom-Benutzeroberfläche konfigurieren und sie über das Web SDK aktivieren.
exl-id: 3f17a83a-dbea-467b-ac67-5462c07c884c
source-git-commit: 252bda1395a2a31cd7e2e2789e5c2508fbd3fd5e
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 77%

---

# Konfigurieren von Datenstromüberschreibungen

Mit Datenstromüberschreibungen können Sie zusätzliche Konfigurationen für Ihre Datenströme definieren, die über das Web SDK an das Edge-Netzwerk übergeben werden.

Dies hilft Ihnen beim Auslösen anderer Datenstromverhaltensweisen als der standardmäßigen, ohne einen neuen Datenstrom zu erstellen oder Ihre vorhandenen Einstellungen zu ändern.

Das Überschreiben der Datenstromkonfiguration besteht aus zwei Schritten:

1. Zunächst müssen Sie Ihre Überschreibungen der Datenstromkonfiguration auf der Seite [Datenstromkonfiguration](configure.md) definieren.
2. Anschließend müssen Sie die Überschreibungen auf eine der folgenden Arten an das Edge-Netzwerk senden:
   * Durch die `sendEvent` oder `configure` [Web SDK](#send-overrides-web-sdk) Befehle.
   * Über das Web SDK [Tag-Erweiterung](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).
   * Über das Mobile SDK [sendEvent-API](#send-overrides-mobile-sdk) aufrufen.

In diesem Artikel wird der Prozess zur Überschreibung der End-to-End-Datenstromkonfiguration für jeden unterstützten Überschreibungstyp erläutert.

>[!IMPORTANT]
>
>Datenspeicherüberschreibungen werden nur für [Web SDK](../edge/home.md) und [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) Integrationen. [Server-API](../server-api/overview.md) -Integrationen unterstützen derzeit keine Überschreibungen von Datastream.
><br>
>Datenstromüberschreibungen sollten verwendet werden, wenn Sie verschiedene Daten an verschiedene Datenströme senden müssen. Sie sollten keine Datenstromüberschreibungen für Personalisierungsanwendungsfälle oder Einverständnisdaten verwenden.

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie Datenstromüberschreibungen verwenden sollten, finden Sie hier einige Beispiele für Anwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit dieser Funktion bewältigen können.

**Datenerfassung für mehrere Regionen**

Ein Unternehmen hat verschiedene Websites oder Subdomains für verschiedene Länder, in denen es tätig ist. Es hat separate Datenströme mit entsprechenden analysespezifischen Report Suites, länderspezifischen Adobe Target-Eigenschafts-Token, länderspezifischen Schemata, Datensätzen, Journey Optimizer-Konfigurationen usw. [konfiguriert](configure.md). Das Unternehmen verfügt außerdem über einen globalen Satz an Konfigurationen, in denen alle landesspezifischen Daten aggregiert werden.

Durch die Verwendung von Datenstromüberschreibungen kann das Unternehmen den Datenfluss dynamisch in verschiedene Datenströme umstellen, anstatt das Standardverhalten zu ändern, Daten an einen Datenstrom zu senden.

Ein gängiger Anwendungsfall könnte darin bestehen, Daten an einen länderspezifischen Datenstrom zu senden und Daten auch an einen globalen Datenstrom zu senden, wo Kundinnen und Kunden wichtige Aktionen ausführen, wie z. B. eine Bestellung aufgeben oder ihr Benutzerprofil aktualisieren.

**Unterscheiden von Profilen und Identitäten für verschiedene Geschäftseinheiten**

Ein Unternehmen mit mehreren Geschäftseinheiten möchte mehrere Experience Platform-Sandboxes verwenden, um Daten zu speichern, die für jede Geschäftseinheit spezifisch sind.

Anstatt Daten an einen standardmäßigen Datenstrom zu senden, kann das Unternehmen Datenstromüberschreibungen verwenden, um sicherzustellen, dass jede Geschäftseinheit über einen eigenen Datenstrom verfügt, über den Daten empfangen werden können.

## Konfigurieren von Datenstromüberschreibungen in der Datenstrom-Benutzeroberfläche {#configure-overrides}

Überschreibungen der Datenstromkonfiguration ermöglichen es Ihnen, die folgenden Datenstromkonfigurationen zu ändern:

* Experience Platform-Ereignisdatensätze
* Adobe Target-Eigenschafts-Token
* Audience Manager-ID-Synchronisierungs-Container
* Report Suites in Adobe Analytics

### Datenstromüberschreibungen für Adobe Target {#target-overrides}

Um Datenstromüberschreibungen für einen Adobe Target-Datenstrom zu konfigurieren, müssen Sie zunächst einen Adobe Target-Datenstrom erstellen lassen. Befolgen Sie die Anweisungen, mit dem [Adobe Target](configure.md#target)-Dienst einen [Datenstrom zu konfigurieren](configure.md).

Nachdem Sie den Datenstrom erstellt haben, bearbeiten Sie den [Adobe Target](configure.md#target)-Dienst, den Sie hinzugefügt haben, und verwenden Sie den Abschnitt **[!UICONTROL Eigenschafts-Token-Überschreibungen]**, um die gewünschten Datenstromüberschreibungen hinzuzufügen, wie in der Abbildung unten dargestellt. Fügen Sie pro Zeile ein Eigenschafts-Token hinzu.

![Screenshot der Datenstrom-Benutzeroberfläche mit den Einstellungen des Adobe Target-Dienstes, wobei die Eigenschafts-Token-Überschreibungen hervorgehoben sind.](assets/overrides/override-target.png)

Nachdem Sie die gewünschten Überschreibungen hinzugefügt haben, speichern Sie Ihre Datenstromeinstellungen.

Ihre Adobe Target-Datenstromüberschreibungen sollten jetzt konfiguriert sein. Jetzt können Sie [die Überschreibungen über das Web SDK an das Edge-Netzwerk senden](#send-overrides).

### Datenstromüberschreibungen für Adobe Analytics {#analytics-overrides}

Um Datenstromüberschreibungen für einen Adobe Analytics-Datenstrom zu konfigurieren, müssen Sie zunächst einen [Adobe Analytics](configure.md#analytics)-Datenstrom erstellen lassen. Befolgen Sie die Anweisungen, mit dem [Adobe Analytics](configure.md#analytics)-Dienst einen [Datenstrom zu konfigurieren](configure.md).

Nachdem Sie den Datenstrom erstellt haben, bearbeiten Sie den [Adobe Analytics](configure.md#target)-Dienst, den Sie hinzugefügt haben, und verwenden Sie den Abschnitt **[!UICONTROL Report Suite-Überschreibungen]**, um die gewünschten Datenstromüberschreibungen hinzuzufügen, wie in der Abbildung unten dargestellt.

Wählen Sie **[!UICONTROL Batch-Modus anzeigen]** aus, um die Stapelbearbeitung der Report Suite-Überschreibungen zu aktivieren. Sie können eine Liste mit Report Suite-Überschreibungen kopieren und einfügen und dabei pro Zeile eine Report Suite eingeben.

![Screenshot der Datenstrom-Benutzeroberfläche mit den Einstellungen des Adobe Analytics-Dienstes, wobei die Report Suite-Überschreibungen hervorgehoben sind.](assets/overrides/override-analytics.png)

Nachdem Sie die gewünschten Überschreibungen hinzugefügt haben, speichern Sie Ihre Datenstromeinstellungen.

Ihre Adobe Analytics-Datenstromüberschreibungen sollten jetzt konfiguriert sein. Jetzt können Sie [die Überschreibungen über das Web SDK an das Edge-Netzwerk senden](#send-overrides).

### Datenstromüberschreibungen für Experience Platform-Ereignisdatensätze {#event-dataset-overrides}

Um Datenstromüberschreibungen für Experience Platform-Ereignisdatensätze zu konfigurieren, müssen Sie zunächst einen [Adobe Experience Platform](configure.md#aep)-Datenstrom erstellt haben. Befolgen Sie die Anweisungen, mit dem [Adobe Experience Platform](configure.md#aep)-Dienst einen [Datenstrom zu konfigurieren](configure.md).

Nachdem Sie den Datenstrom erstellt haben, bearbeiten Sie den [Adobe Experience Platform](configure.md#aep)-Dienst, den Sie hinzugefügt haben, und wählen Sie die Option **[!UICONTROL Ereignisdatensatz hinzufügen]** aus, um einen oder mehrere Ereignisdatensätze zur Überschreibung hinzuzufügen, wie in der Abbildung unten dargestellt.

![Screenshot der Datenstrom-Benutzeroberfläche mit den Einstellungen des Adobe Experience Platform-Dienstes, wobei die Überschreibungen des Ereignisdatensatzes hervorgehoben sind.](assets/overrides/override-aep.png)

Nachdem Sie die gewünschten Überschreibungen hinzugefügt haben, speichern Sie Ihre Datenstromeinstellungen.

Sie sollten jetzt die Adobe Experience Platform-Datenstromüberschreibungen konfiguriert haben. Jetzt können Sie [die Überschreibungen über das Web SDK an das Edge-Netzwerk senden](#send-overrides).

### Datenstromüberschreibungen für ID-Synchronisierungs-Container von Drittanbietern {#container-overrides}

Um Datenstromüberschreibungen für ID-Synchronisierungs-Container von Drittanbietern zu konfigurieren, müssen Sie zunächst einen Datenstrom erstellen lassen. Befolgen Sie die Anweisungen zum [Konfigurieren eines Datenstroms](configure.md), um einen Datenstrom zu erstellen.

Nachdem Sie den Datenstrom erstellt haben, navigieren Sie zu **[!UICONTROL Erweiterte Optionen]** und aktivieren Sie die Option **[!UICONTROL Synchronisierung der Drittanbieter-ID]**.

Verwenden Sie dann den Abschnitt **[!UICONTROL Container-ID-Überschreibungen]**, um die Container-IDs hinzuzufügen, für die Sie die Standardeinstellung überschreiben möchten, wie in der Abbildung unten dargestellt.

>[!IMPORTANT]
>
>Container-IDs müssen numerische Werte sein, z. B. `1234567`, nicht aber Zeichenfolgen wie `"1234567"`. Wenn Sie einen Zeichenfolgenwert über das Web SDK als Container-ID-Überschreibung senden, erhalten Sie einen Fehler.

![Screenshot der Datenstrom-Benutzeroberfläche mit den Einstellungen des Datenstroms, wobei der Container für die ID-Synchronisierung von Drittanbietern hervorgehoben ist.](assets/overrides/override-container.png)

Nachdem Sie die gewünschten Überschreibungen hinzugefügt haben, speichern Sie Ihre Datenstromeinstellungen.

Sie sollten jetzt die Überschreibungen des ID-Synchronisierungs-Containers konfiguriert haben. Jetzt können Sie [die Überschreibungen über das Web SDK an das Edge-Netzwerk senden](#send-overrides).

## Senden der Überschreibungen an das Edge-Netzwerk über das Web SDK {#send-overrides-web-sdk}

>[!NOTE]
>
>Alternativ zum Senden der Konfigurationsüberschreibungen über Web SDK-Befehle können Sie auch die Konfigurationsüberschreibungen zur [Tag-Erweiterung](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) des Web SDK hinzufügen.

Nach dem [Konfigurieren der Datenstromüberschreibungen](#configure-overrides) in der Datenerfassungs-Benutzeroberfläche können Sie die Überschreibungen jetzt über das Web SDK an das Edge-Netzwerk senden.

Wenn Sie das Web SDK verwenden, senden Sie die Überschreibungen über das `edgeConfigOverrides` -Befehl ist der zweite und letzte Schritt zum Aktivieren von Überschreibungen der Datastream-Konfiguration.

Die Überschreibungen der Datenstromkonfiguration werden über den Web SDK-Befehl `edgeConfigOverrides` gesendet. Mit diesem Befehl werden Datenstromüberschreibungen erstellt, die mit dem nächsten Befehl (bzw. im Fall des Befehls `configure` mit jeder Anfrage) an das [!DNL Edge Network] weitergegeben werden.

Der Befehl `edgeConfigOverrides` erstellt Datenstromüberschreibungen, die mit dem nächsten Befehl (bzw. im Fall des Befehls `configure` mit jeder Anfrage) an das [!DNL Edge Network] weitergegeben werden.

Wenn eine Konfigurationsüberschreibung mit dem Befehl `configure` gesendet wird, ist sie in den folgenden Web SDK-Befehlen enthalten.

* [sendEvent](../edge/fundamentals/tracking-events.md)
* [setConsent](../edge/consent/iab-tcf/overview.md)
* [getIdentity](../edge/identity/overview.md)
* [appendIdentityToUrl](../edge/identity/id-sharing.md#cross-domain-sharing)
* [configure](../edge/fundamentals/configuring-the-sdk.md)

Global angegebene Optionen können durch die Konfigurationsoption bei einzelnen Befehlen überschrieben werden.

### Überschreibungen der Konfiguration über das Web SDK senden `sendEvent` command {#send-event}

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

### Überschreibungen der Konfiguration über das Web SDK senden `configure` command {#send-configure}

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

## Senden der Überschreibungen an das Edge-Netzwerk über das Mobile SDK {#send-overrides-mobile-sdk}

Nachher [Konfigurieren der Überschreibungen des Datastreams](#configure-overrides) In der Datenerfassungs-Benutzeroberfläche können Sie die Überschreibungen jetzt über das Mobile SDK an das Edge-Netzwerk senden.

Wenn Sie das Mobile SDK verwenden, senden Sie die Überschreibungen über das `sendEvent` API ist der zweite und letzte Schritt zum Aktivieren von Außerkraftsetzen der Datastream-Konfiguration.

Weitere Informationen zum Experience Platform Mobile SDK finden Sie unter [Dokumentation zum Mobile SDK](https://developer.adobe.com/client-sdks/edge/edge-network/).

### Überschreiben der Datastream-ID über das Mobile SDK {#id-override-mobile}

Die folgenden Beispiele zeigen, wie eine Datastream-ID-Überschreibung bei einer Mobile SDK-Integration aussehen könnte. Wählen Sie die folgenden Registerkarten aus, um die [!DNL iOS] und [!DNL Android] Beispiele.

>[!BEGINTABS]

>[!TAB iOS (Swift)]

Dieses Beispiel zeigt, wie eine Datastream-ID-Überschreibung in einem Mobile SDK aussieht. [!DNL iOS] Integration.

```swift
// Create Experience event from dictionary
var xdmData: [String: Any] = [
  "eventType": "SampleXDMEvent",
  "sample": "data",
]
let experienceEvent = ExperienceEvent(xdm: xdmData, datastreamIdOverride: "SampleDatastreamId")

Edge.sendEvent(experienceEvent: experienceEvent) { (handles: [EdgeEventHandle]) in
  // Handle the Edge Network response
}
```

>[!TAB Android (Kotlin)]

Dieses Beispiel zeigt, wie eine Datastream-ID-Überschreibung in einem Mobile SDK aussieht. [!DNL Android] Integration.

```kotlin
// Create experience event from Map
val xdmData = mutableMapOf < String, Any > ()
xdmData["eventType"] = "SampleXDMEvent"
xdmData["sample"] = "data"

val experienceEvent = ExperienceEvent.Builder()
    .setXdmSchema(xdmData)
    .setDatastreamIdOverride("SampleDatastreamId")
    .build()

Edge.sendEvent(experienceEvent) {
    // Handle the Edge Network response
}
```

>[!ENDTABS]

### Überschreiben der Datastream-Konfiguration über das Mobile SDK {#config-override-mobile}

Die folgenden Beispiele zeigen, wie eine Außerkraftsetzung der Datastream-Konfiguration bei einer Mobile SDK-Integration aussehen könnte. Wählen Sie die folgenden Registerkarten aus, um die [!DNL iOS] und [!DNL Android] Beispiele.

>[!BEGINTABS]

>[!TAB iOS (Swift)]

Dieses Beispiel zeigt, wie eine Außerkraftsetzung einer Datastream-Konfiguration in einem Mobile SDK aussieht [!DNL iOS] Integration.

```swift
// Create Experience event from dictionary
var xdmData: [String: Any] = [
  "eventType": "SampleXDMEvent",
  "sample": "data",
]

let configOverrides: [String: Any] = [
  "com_adobe_experience_platform": [
    "datasets": [
      "event": [
        "datasetId": "SampleEventDatasetIdOverride"
      ]
    ]
  ],
  "com_adobe_analytics": [
  "reportSuites": [
        "MyFirstOverrideReportSuite",
          "MySecondOverrideReportSuite",
          "MyThirdOverrideReportSuite"
      ]
  ],
  "com_adobe_identity": [
    "idSyncContainerId": "1234567"
  ],
  "com_adobe_target": [
    "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
 ],
]

let experienceEvent = ExperienceEvent(xdm: xdmData, datastreamConfigOverride: configOverrides)

Edge.sendEvent(experienceEvent: experienceEvent) { (handles: [EdgeEventHandle]) in
  // Handle the Edge Network response
}
```

>[!TAB Android (Kotlin)]

Dieses Beispiel zeigt, wie eine Außerkraftsetzung einer Datastream-Konfiguration in einem Mobile SDK aussieht [!DNL Android] Integration.

```kotlin
// Create experience event from Map
val xdmData = mutableMapOf < String, Any > ()
xdmData["eventType"] = "SampleXDMEvent"
xdmData["sample"] = "data"

val configOverrides = mapOf(
    "com_adobe_experience_platform"
    to mapOf(
        "datasets"
        to mapOf(
            "event"
            to mapOf("datasetId"
                to "SampleEventDatasetIdOverride")
        )
    ),
    "com_adobe_analytics"
    to mapOf(
        "reportSuites"
        to listOf(
            "MyFirstOverrideReportSuite",
            "MySecondOverrideReportSuite",
            "MyThirdOverrideReportSuite"
        )
    ),
    "com_adobe_identity"
    to mapOf(
        "idSyncContainerId"
        to "1234567"
    ),
    "com_adobe_target"
    to mapOf(
        "propertyToken"
        to "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    )
)

val experienceEvent = ExperienceEvent.Builder()
    .setXdmSchema(xdmData)
    .setDatastreamConfigOverride(configOverrides)
    .build()

Edge.sendEvent(experienceEvent) {
    // Handle the Edge Network response
}
```

>[!ENDTABS]

## Payload-Beispiel {#payload-example}

Die obigen Beispiele generieren eine [!DNL Edge Network] Nutzlast ähnlich der unten stehenden.

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "SampleProfileDatasetIdOverride"
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
    "state": {  }
  },
  "events": [  ]
}
```
