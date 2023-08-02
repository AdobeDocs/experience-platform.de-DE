---
title: Konfigurieren von Überschreibungen für Datenströme
description: Erfahren Sie, wie Sie in der Benutzeroberfläche von Datastreams Außerkraftsetzungen von Datastreams konfigurieren und über das Web SDK aktivieren.
exl-id: 7829f411-acdc-49a1-a8fe-69834bcdb014
source-git-commit: b0b53d9fcf410812eee3abdbbb6960d328fee99f
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 4%

---

# Konfigurieren von Überschreibungen für Datenströme

Mit Datastream-Überschreibungen können Sie zusätzliche Konfigurationen für Ihre Datenspeicher definieren, die über das Web SDK an das Edge-Netzwerk übergeben werden.

Dies hilft Ihnen beim Trigger verschiedener Datenspeicherverhaltensweisen als der Standardeinstellungen, ohne einen neuen Datenspeicher zu erstellen oder Ihre vorhandenen Einstellungen zu ändern.

Die Außerkraftsetzung der Datastream-Konfiguration besteht aus zwei Schritten:

1. Zunächst müssen Sie Ihre Überschreibungen der Datenstromkonfiguration auf der Seite [Datenstromkonfiguration](configure.md) definieren.
2. Anschließend müssen Sie die Überschreibungen entweder über einen Web SDK-Befehl oder mithilfe der [Tag-Erweiterung](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) des Web SDK an das Edge-Netzwerk senden.

In diesem Artikel wird der Prozess zur Außerkraftsetzung der End-to-End-Datenspeicherung für jede unterstützte Überschreibungstyp erläutert.

>[!IMPORTANT]
>
>Datenspeicherüberschreibungen werden nur für [Web SDK](../edge/home.md) Integrationen. [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) und [Server-API](../server-api/overview.md) -Integrationen unterstützen derzeit keine Überschreibungen von Datastream.
><br><br>
>Datastream-Überschreibungen sollten verwendet werden, wenn Sie verschiedene Daten an verschiedene Datastreams senden müssen. Sie sollten keine Datastream-Überschreibungen für Personalisierungsanwendungsfälle oder Zustimmungsdaten verwenden.

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Datastream-Umgehungen verwendet werden, finden Sie hier einige Anwendungsfälle, die Adobe Experience Platform-Kunden mit dieser Funktion lösen können.

**Multiregion-Datenerfassung**

Ein Unternehmen hat verschiedene Websites oder Subdomänen für verschiedene Länder, in denen es tätig ist. Sie haben [konfiguriert](configure.md) separate Datenspeicher mit entsprechenden analysespezifischen Report Suites, länderspezifischen Adobe Target-Eigenschafts-Token, länderspezifischen Schemata, Datensätzen, Journey Optimizer-Konfigurationen usw. Das Unternehmen verfügt außerdem über einen globalen Satz an Konfigurationen, in denen alle landesspezifischen Daten aggregiert werden.

Durch die Verwendung von Datastream-Überschreibungen kann das Unternehmen den Datenfluss dynamisch in verschiedene Datastraams umstellen, anstatt das Standardverhalten, Daten an einen Datastream zu senden.

Ein gängiger Anwendungsfall könnte darin bestehen, Daten an einen länderspezifischen Datastream zu senden und Daten an einen globalen Datastream zu senden, wo Kunden wichtige Aktionen ausführen, wie z. B. eine Bestellung aufgeben oder ihr Benutzerprofil aktualisieren.

**Unterscheiden von Profilen und Identitäten für verschiedene Geschäftsbereiche**

Ein Unternehmen mit mehreren Geschäftseinheiten möchte mehrere Experience Platformen-Sandboxes verwenden, um Daten zu speichern, die für jede Geschäftseinheit spezifisch sind.

Anstatt Daten an einen standardmäßigen Datastream zu senden, kann das Unternehmen Datenspeicherüberschreibungen verwenden, um sicherzustellen, dass jede Geschäftseinheit über einen eigenen Datenspeicher verfügt, über den Daten empfangen werden können.

## Konfigurieren von Datastream-Überschreibungen in der Benutzeroberfläche von Datastreams {#configure-overrides}

Überschreibungen der Datastream-Konfiguration ermöglichen es Ihnen, die folgenden Datastream-Konfigurationen zu ändern:

* Experience Platform von Ereignis-Datensätzen
* Adobe Target-Eigenschafts-Token
* Audience Manager-ID-Synchronisierungs-Container
*  Report Suites in Adobe Analytics

### Datenspeicherüberschreibungen für Adobe Target {#target-overrides}

Um Datastream-Überschreibungen für einen Adobe Target-Datastream zu konfigurieren, müssen Sie zunächst einen Adobe Target-Datenspeicher erstellen lassen. Befolgen Sie die Anweisungen unter [Datensatz konfigurieren](configure.md) mit dem [Adobe Target](configure.md#target) -Dienst.

Nachdem Sie den Datastream erstellt haben, bearbeiten Sie die [Adobe Target](configure.md#target) -Dienst, den Sie hinzugefügt haben, und verwenden Sie **[!UICONTROL Eigenschafts-Token - Überschreibungen]** -Abschnitt, um die gewünschten Datastream-Umgehungen hinzuzufügen, wie in der Abbildung unten dargestellt. Fügen Sie pro Zeile ein Property-Token hinzu.

![Screenshot der Benutzeroberfläche von Datastreams mit den Einstellungen des Adobe Target-Dienstes, wobei das Eigenschafts-Token überschrieben wird.](assets/overrides/override-target.png)

Nachdem Sie die gewünschten Überschreibungen hinzugefügt haben, speichern Sie Ihre Datastream-Einstellungen.

Sie sollten jetzt die Adobe Target-Datastream-Überschreibungen konfiguriert haben. Jetzt können Sie [Senden der Überschreibungen an das Edge-Netzwerk über das Web SDK](#send-overrides).

### Datenspeicherüberschreibungen für Adobe Analytics {#analytics-overrides}

Um Datastream-Überschreibungen für einen Adobe Analytics-Datastream zu konfigurieren, müssen Sie zunächst über eine [Adobe Analytics](configure.md#analytics) Datastream erstellt. Befolgen Sie die Anweisungen unter [Datensatz konfigurieren](configure.md) mit dem [Adobe Analytics](configure.md#analytics) -Dienst.

Nachdem Sie den Datastream erstellt haben, bearbeiten Sie die [Adobe Analytics](configure.md#target) -Dienst, den Sie hinzugefügt haben, und verwenden Sie **[!UICONTROL Report Suite - Überschreibungen]** -Abschnitt, um die gewünschten Datastream-Umgehungen hinzuzufügen, wie in der Abbildung unten dargestellt.

Auswählen **[!UICONTROL Batch-Modus anzeigen]** , um die Stapelbearbeitung der Report Suite-Überschreibung zu aktivieren. Sie können eine Liste mit Report Suite-Überschreibungen kopieren und einfügen und dabei pro Zeile eine Report Suite eingeben.

![Screenshot der Benutzeroberfläche von Datastreams mit den Einstellungen des Adobe Analytics-Dienstes, wobei die Report Suite-Überschreibung hervorgehoben wird.](assets/overrides/override-analytics.png)

Nachdem Sie die gewünschten Überschreibungen hinzugefügt haben, speichern Sie Ihre Datastream-Einstellungen.

Sie sollten jetzt die Adobe Analytics-Datastream-Überschreibungen konfiguriert haben. Jetzt können Sie [Senden der Überschreibungen an das Edge-Netzwerk über das Web SDK](#send-overrides).

### Datastream-Überschreibungen für Experience Platform-Ereignis-Datensätze {#event-dataset-overrides}

Um Datastream-Überschreibungen für Experience Platform-Ereignis-Datensätze zu konfigurieren, müssen Sie zunächst über eine [Adobe Experience Platform](configure.md#aep) Datastream erstellt. Befolgen Sie die Anweisungen unter [Datensatz konfigurieren](configure.md) mit dem [Adobe Experience Platform](configure.md#aep) -Dienst.

Nachdem Sie den Datastream erstellt haben, bearbeiten Sie die [Adobe Experience Platform](configure.md#aep) den Sie hinzugefügt haben, und wählen Sie **[!UICONTROL Ereignis-Datensatz hinzufügen]** -Option zum Hinzufügen eines oder mehrerer Ereignis-Datensätze überschreiben, wie in der Abbildung unten dargestellt.

![Screenshot der Benutzeroberfläche von Datastreams mit den Einstellungen des Adobe Experience Platform-Dienstes, wobei die Außerkraftsetzungen des Ereignisdatensatzes hervorgehoben sind.](assets/overrides/override-aep.png)

Nachdem Sie die gewünschten Überschreibungen hinzugefügt haben, speichern Sie Ihre Datastream-Einstellungen.

Sie sollten jetzt die Adobe Experience Platform-Datastream-Überschreibungen konfiguriert haben. Jetzt können Sie [Senden der Überschreibungen an das Edge-Netzwerk über das Web SDK](#send-overrides).

### Datastream-Überschreibungen für ID-Synchronisierungs-Container von Drittanbietern {#container-overrides}

Um Datastream-Überschreibungen für ID-Synchronisierungscontainer von Drittanbietern zu konfigurieren, müssen Sie zunächst einen Datastream erstellen lassen. Befolgen Sie die Anweisungen unter [Datensatz konfigurieren](configure.md) , um eine zu erstellen.

Nachdem Sie den Datastream erstellt haben, navigieren Sie zu **[!UICONTROL Erweiterte Optionen]** und aktivieren Sie die **[!UICONTROL Synchronisierung der Drittanbieter-ID]** -Option.

Verwenden Sie dann die **[!UICONTROL Überschreibungen der Container-ID]** -Abschnitt, um die Container-IDs hinzuzufügen, die Sie die Standardeinstellung überschreiben möchten, wie in der Abbildung unten dargestellt.

>[!IMPORTANT]
>
>Container-IDs müssen numerische Werte sein, z. B. `1234567`, nicht aber Zeichenfolgen wie `"1234567"`. Wenn Sie einen Zeichenfolgenwert über das Web SDK als Container-ID-Überschreibung senden, erhalten Sie einen Fehler.

![Screenshot der Benutzeroberfläche von Datastreams mit den Einstellungen des Datastreams, wobei der Container für die ID-Synchronisierung von Drittanbietern hervorgehoben wird.](assets/overrides/override-container.png)

Nachdem Sie die gewünschten Überschreibungen hinzugefügt haben, speichern Sie Ihre Datastream-Einstellungen.

Sie sollten jetzt die Außerkraftsetzungen des ID-Synchronisierungs-Containers konfiguriert haben. Jetzt können Sie [Senden der Überschreibungen an das Edge-Netzwerk über das Web SDK](#send-overrides).

## Senden der Überschreibungen an das Edge-Netzwerk über das Web SDK {#send-overrides}

>[!NOTE]
>
>Alternativ zum Senden der Konfigurationsüberschreibungen über Web SDK-Befehle können Sie die Konfigurationsüberschreibungen zum Web SDK hinzufügen [Tag-Erweiterung](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

Nachher [Konfigurieren der Überschreibungen des Datastreams](#configure-overrides) In der Datenerfassungs-Benutzeroberfläche können Sie die Überschreibungen jetzt über das Web SDK an das Edge-Netzwerk senden.

Das Senden der Überschreibungen an das Edge-Netzwerk über das Web SDK ist der zweite und letzte Schritt beim Aktivieren von Überschreibungen für die Datastream-Konfiguration.

Die Außerkraftsetzungen der Datastream-Konfiguration werden über das `edgeConfigOverrides` Web SDK-Befehl. Mit diesem Befehl werden Datastream-Überschreibungen erstellt, die an die [!DNL Edge Network] auf dem nächsten Befehl oder, im Falle der `configure` -Befehl für jede Anfrage.

Die `edgeConfigOverrides` -Befehl erstellt Datastream-Überschreibungen, die an die [!DNL Edge Network] beim nächsten Befehl oder, im Fall von `configure`, für jede Anfrage.

Wenn eine Konfigurationsüberschreibungen mit dem `configure` angegeben ist, ist sie in den folgenden Web SDK-Befehlen enthalten.

* [sendEvent](../edge/fundamentals/tracking-events.md)
* [setConsent](../edge/consent/iab-tcf/overview.md)
* [getIdentity](../edge/identity/overview.md)
* [appendIdentityToUrl](../edge/identity/id-sharing.md#cross-domain-sharing)
* [konfigurieren](../edge/fundamentals/configuring-the-sdk.md)

Global angegebene Optionen können durch die Konfigurationsoption bei einzelnen Befehlen überschrieben werden.

### Überschreibungen der Versandkonfiguration über die `sendEvent` command {#send-event}

Das folgende Beispiel zeigt, wie eine Konfigurationsüberschreibung auf einem `sendEvent` Befehl.

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
          datasetId: "MyOverrideDataset"
        },
        profile: {
          datasetId: "www"
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
| `edgeConfigOverrides.datastreamId` | Verwenden Sie diesen Parameter, um zuzulassen, dass eine einzelne Anfrage an einen anderen als den von der `configure` Befehl. |

### Überschreibungen der Versandkonfiguration über die `configure` command {#send-configure}

Das folgende Beispiel zeigt, wie eine Konfigurationsüberschreibung auf einem `configure` Befehl.

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
          datasetId: "MyOverrideDataset"
        },
        "profile": { 
          datasetId: "www"
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

### Beispiel einer Nutzlast {#payload-example}

Die obigen Beispiele generieren eine [!DNL Edge Network] Nutzlast, die wie folgt aussieht:

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "MyOverrideDataset"
          },
          "profile": {
            "datasetId": "www"
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
  "events": [  ],
  "query": {
    "identity": {
      "fetch": [
        "ECID"
      ]
    }
  }
}
```
