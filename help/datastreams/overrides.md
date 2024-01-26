---
title: Konfigurieren von Datenstromüberschreibungen
description: Erfahren Sie, wie Sie Datenstromüberschreibungen in der Datenstrom-Benutzeroberfläche konfigurieren und sie über das Web SDK aktivieren.
exl-id: 3f17a83a-dbea-467b-ac67-5462c07c884c
source-git-commit: 11feeae0409822f0b1ccba2df263f0be466d54e3
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 67%

---

# Konfigurieren von Datenstromüberschreibungen

Mit Datenstromüberschreibungen können Sie zusätzliche Konfigurationen für Ihre Datenströme definieren, die über das Web SDK an das Edge-Netzwerk übergeben werden.

Auf diese Weise können Sie andere Verhaltensweisen von Datastreams als die Standardeinstellungen Trigger haben, ohne einen Datastream zu erstellen oder Ihre vorhandenen Einstellungen zu ändern.

Die Außerkraftsetzung der Datastream-Konfiguration erfolgt in zwei Schritten:

1. Zunächst müssen Sie Ihre Datastream-Konfigurationsüberschreibungen im [Datastream-Konfigurationsseite](configure.md).
2. Anschließend müssen Sie die Überschreibungen auf eine der folgenden Arten an das Edge-Netzwerk senden:
   * Durch die `sendEvent` oder `configure` [Web SDK](#send-overrides-web-sdk) Befehle.
   * Über das Web SDK [Tag-Erweiterung](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).
   * Über das Mobile SDK [sendEvent](#send-overrides-mobile-sdk) Befehl.

In diesem Artikel wird der Prozess zur Überschreibung der End-to-End-Datenstromkonfiguration für jeden unterstützten Überschreibungstyp erläutert.

>[!IMPORTANT]
>
>Datenspeicherüberschreibungen werden nur für [Web SDK](../edge/home.md) und [Mobile SDK](https://developer.adobe.com/client-sdks/home/) Integrationen. [Server-API](../server-api/overview.md) -Integrationen unterstützen derzeit keine Überschreibungen von Datastream.
><br>
>Datenstromüberschreibungen sollten verwendet werden, wenn Sie verschiedene Daten an verschiedene Datenströme senden müssen. Verwenden Sie keine Datastream-Überschreibungen für Anwendungsfälle zur Personalisierung oder Einverständnisdaten.

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie Datenstromüberschreibungen verwenden sollten, finden Sie hier einige Beispiele für Anwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit dieser Funktion bewältigen können.

**Datenerfassung für mehrere Regionen**

Ein Unternehmen hat verschiedene Websites oder Subdomains für verschiedene Länder, in denen es tätig ist. Es hat separate Datenströme mit entsprechenden analysespezifischen Report Suites, länderspezifischen Adobe Target-Eigenschafts-Token, länderspezifischen Schemata, Datensätzen, Journey Optimizer-Konfigurationen usw. [konfiguriert](configure.md). Das Unternehmen verfügt außerdem über einen globalen Satz an Konfigurationen, in denen alle landesspezifischen Daten aggregiert werden.

Durch die Verwendung von Datenstromüberschreibungen kann das Unternehmen den Datenfluss dynamisch in verschiedene Datenströme umstellen, anstatt das Standardverhalten zu ändern, Daten an einen Datenstrom zu senden.

Ein gängiger Anwendungsfall könnte das Senden von Daten an einen länderspezifischen Datastream und auch an einen globalen Datastream sein, wo Kunden wichtige Aktionen ausführen, wie z. B. eine Bestellung aufgeben oder ihr Benutzerprofil aktualisieren.

**Unterscheiden von Profilen und Identitäten für verschiedene Geschäftseinheiten**

Ein Unternehmen mit mehreren Geschäftseinheiten möchte mehrere Experience Platform-Sandboxes verwenden, um für jede Geschäftseinheit spezifische Daten zu speichern.

Anstatt Daten an einen standardmäßigen Datenstrom zu senden, kann das Unternehmen Datenstromüberschreibungen verwenden, um sicherzustellen, dass jede Geschäftseinheit über einen eigenen Datenstrom verfügt, über den Daten empfangen werden können.

## Konfigurieren von Datenstromüberschreibungen in der Datenstrom-Benutzeroberfläche {#configure-overrides}

Überschreibungen der Datenstromkonfiguration ermöglichen es Ihnen, die folgenden Datenstromkonfigurationen zu ändern:

* Experience Platform-Ereignisdatensätze
* Adobe Target-Eigenschafts-Token
* Audience Manager-ID-Synchronisierungs-Container
* Report Suites in Adobe Analytics

### Datenstromüberschreibungen für Adobe Target {#target-overrides}

Um Datenstromüberschreibungen für einen Adobe Target-Datenstrom zu konfigurieren, müssen Sie zunächst einen Adobe Target-Datenstrom erstellen lassen. Befolgen Sie die Anweisungen, mit dem [Adobe Target](configure.md#target)-Dienst einen [Datenstrom zu konfigurieren](configure.md).

Nachdem Sie den Datastream erstellt haben, bearbeiten Sie die [Adobe Target](configure.md#target) -Dienst, den Sie hinzugefügt haben, und verwenden Sie **[!UICONTROL Eigenschafts-Token - Überschreibungen]** -Abschnitt, um die gewünschten Datastream-Umgehungen hinzuzufügen, wie in der Abbildung unten dargestellt. Fügen Sie pro Zeile ein Eigenschafts-Token hinzu.

![Screenshot der Datenstrom-Benutzeroberfläche mit den Einstellungen des Adobe Target-Dienstes, wobei die Eigenschafts-Token-Überschreibungen hervorgehoben sind.](assets/overrides/override-target.png)

Nachdem Sie die gewünschten Überschreibungen hinzugefügt haben, speichern Sie Ihre Datenstromeinstellungen.

Ihre Adobe Target-Datenstromüberschreibungen sollten jetzt konfiguriert sein. Jetzt können Sie [die Überschreibungen über das Web SDK an das Edge-Netzwerk senden](#send-overrides).

### Datenstromüberschreibungen für Adobe Analytics {#analytics-overrides}

Um Datenstromüberschreibungen für einen Adobe Analytics-Datenstrom zu konfigurieren, müssen Sie zunächst einen [Adobe Analytics](configure.md#analytics)-Datenstrom erstellen lassen. Befolgen Sie die Anweisungen, mit dem [Adobe Analytics](configure.md#analytics)-Dienst einen [Datenstrom zu konfigurieren](configure.md).

Nachdem Sie den Datastream erstellt haben, bearbeiten Sie die [Adobe Analytics](configure.md#target) -Dienst, den Sie hinzugefügt haben, und verwenden Sie **[!UICONTROL Report Suite - Überschreibungen]** -Abschnitt, um die gewünschten Datastream-Umgehungen hinzuzufügen, wie in der Abbildung unten dargestellt.

Wählen Sie **[!UICONTROL Batch-Modus anzeigen]** aus, um die Stapelbearbeitung der Report Suite-Überschreibungen zu aktivieren. Sie können eine Liste mit Report Suite-Überschreibungen kopieren und einfügen und dabei pro Zeile eine Report Suite eingeben.

![Screenshot der Datenstrom-Benutzeroberfläche mit den Einstellungen des Adobe Analytics-Dienstes, wobei die Report Suite-Überschreibungen hervorgehoben sind.](assets/overrides/override-analytics.png)

Nachdem Sie die gewünschten Überschreibungen hinzugefügt haben, speichern Sie Ihre Datenstromeinstellungen.

Ihre Adobe Analytics-Datenstromüberschreibungen sollten jetzt konfiguriert sein. Jetzt können Sie [die Überschreibungen über das Web SDK an das Edge-Netzwerk senden](#send-overrides).

### Datenstromüberschreibungen für Experience Platform-Ereignisdatensätze {#event-dataset-overrides}

Um Datenstromüberschreibungen für Experience Platform-Ereignisdatensätze zu konfigurieren, müssen Sie zunächst einen [Adobe Experience Platform](configure.md#aep)-Datenstrom erstellt haben. Befolgen Sie die Anweisungen, mit dem [Adobe Experience Platform](configure.md#aep)-Dienst einen [Datenstrom zu konfigurieren](configure.md).

Nachdem Sie den Datastream erstellt haben, bearbeiten Sie die [Adobe Experience Platform](configure.md#aep) den Sie hinzugefügt haben, und wählen Sie **[!UICONTROL Ereignis-Datensatz hinzufügen]** -Option zum Hinzufügen eines oder mehrerer Ereignis-Datensätze überschreiben, wie in der Abbildung unten dargestellt.

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

Die Überschreibungen der Datenstromkonfiguration werden über den Web SDK-Befehl `edgeConfigOverrides` gesendet. Mit diesem Befehl werden Datastream-Überschreibungen erstellt, die an die [!DNL Edge Network] auf dem nächsten Befehl. Wenn Sie die `configure` -Befehl, werden die Überschreibungen für jede Anfrage übergeben.

Die `edgeConfigOverrides` -Befehl erstellt Datastream-Überschreibungen, die an die [!DNL Edge Network] auf dem nächsten Befehl.

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

Informationen zum Senden der Außerkraftsetzungen an das Edge-Netzwerk finden Sie im Abschnitt [Handbuch zum Senden von Überschreibungen mit sendEvent](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-sendevent/) oder [Handbuch zum Senden von Überschreibungen mithilfe von Regeln](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-rules/).

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
