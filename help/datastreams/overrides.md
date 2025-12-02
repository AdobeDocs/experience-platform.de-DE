---
title: Konfigurieren von Datenstromüberschreibungen
description: Erfahren Sie, wie Sie Datenstrom-Überschreibungen in der Datenstrom-Benutzeroberfläche konfigurieren und über die Web-SDK oder mobile SDK aktivieren.
exl-id: 3f17a83a-dbea-467b-ac67-5462c07c884c
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 53%

---

# Konfigurieren von Datenstromüberschreibungen

Mit Datenstrom-Überschreibungen können Sie zusätzliche Konfigurationen für Ihre Datenströme definieren, die über die Web-SDK oder mobile SDK an die Edge Network übergeben werden.

Auf diese Weise können Sie andere Datenstromverhaltensweisen als die standardmäßigen Trigger vornehmen, ohne einen Datenstrom zu erstellen oder Ihre vorhandenen Einstellungen zu ändern.

Die Überschreibung der Datenstromkonfiguration ist ein zweistufiger Prozess:

1. Zunächst müssen Sie Ihre Überschreibung der Datenstromkonfiguration auf der Seite [Datenstromkonfiguration“ ](configure.md).
2. Anschließend müssen Sie die Überschreibungen auf eine der folgenden Arten an Edge Network senden:
   * Durch die `sendEvent` oder `configure` [Web SDK](#send-overrides)-Befehle.
   * Über die Web-SDK [Tag-Erweiterung](../tags/extensions/client/web-sdk/configure/configuration-overrides.md).
   * Über die Mobile SDK [sendEvent](#send-overrides)-API oder mithilfe von [Rules](#send-overrides).

In diesem Artikel wird der Prozess zur Überschreibung der End-to-End-Datenstromkonfiguration für jeden unterstützten Überschreibungstyp erläutert.

>[!IMPORTANT]
>
>[Edge Network-API](https://developer.adobe.com/data-collection-apis/docs/api/)-Integrationen unterstützen derzeit keine Datenstrom-Überschreibungen.
><br>
>Datenstromüberschreibungen sollten verwendet werden, wenn Sie verschiedene Daten an verschiedene Datenströme senden müssen. Verwenden Sie keine Datenstrom-Überschreibungen für Personalisierungs-Anwendungsfälle oder Einverständnisdaten.

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie Datenstromüberschreibungen verwenden sollten, finden Sie hier einige Beispiele für Anwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit dieser Funktion bewältigen können.

**Datenerfassung für mehrere Regionen**

Ein Unternehmen hat verschiedene Websites oder Subdomains für verschiedene Länder, in denen es tätig ist. Es hat separate Datenströme mit entsprechenden analysespezifischen Report Suites, länderspezifischen Adobe Target-Eigenschafts-Token, länderspezifischen Schemata, Datensätzen, Journey Optimizer-Konfigurationen usw. [konfiguriert](configure.md). Das Unternehmen verfügt außerdem über einen globalen Satz an Konfigurationen, in denen alle landesspezifischen Daten aggregiert werden.

Durch die Verwendung von Datenstromüberschreibungen kann das Unternehmen den Datenfluss dynamisch in verschiedene Datenströme umstellen, anstatt das Standardverhalten zu ändern, Daten an einen Datenstrom zu senden.

Ein gängiges Anwendungsbeispiel könnte das Senden von Daten an einen länderspezifischen Datenstrom und auch an einen globalen Datenstrom sein, bei dem Kundinnen und Kunden eine wichtige Aktion ausführen, z. B. eine Bestellung aufgeben oder ihr Benutzerprofil aktualisieren.

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

Nachdem Sie den Datenstrom erstellt haben, bearbeiten Sie den [Adobe Target](configure.md#target)-Service, den Sie hinzugefügt haben, und verwenden Sie den Abschnitt **[!UICONTROL Property Token Overrides]** , um die gewünschten Datenstromüberschreibungen hinzuzufügen, wie in der Abbildung unten dargestellt. Fügen Sie pro Zeile ein Eigenschafts-Token hinzu.

![Screenshot der Datenstrom-Benutzeroberfläche mit den Einstellungen des Adobe Target-Dienstes, wobei die Eigenschafts-Token-Überschreibungen hervorgehoben sind.](assets/overrides/override-target.png)

Nachdem Sie die gewünschten Überschreibungen hinzugefügt haben, speichern Sie Ihre Datenstromeinstellungen.

Ihre Adobe Target-Datenstromüberschreibungen sollten jetzt konfiguriert sein. Jetzt können Sie [die Überschreibungen über die Web-SDK oder mobile SDK an die Edge Network senden](#send-overrides).

### Datenstromüberschreibungen für Adobe Analytics {#analytics-overrides}

Um Datenstromüberschreibungen für einen Adobe Analytics-Datenstrom zu konfigurieren, müssen Sie zunächst einen [Adobe Analytics](configure.md#analytics)-Datenstrom erstellen lassen. Befolgen Sie die Anweisungen, mit dem [Adobe Analytics](configure.md#analytics)-Dienst einen [Datenstrom zu konfigurieren](configure.md).

Nachdem Sie den Datenstrom erstellt haben, bearbeiten Sie den [Adobe Analytics](configure.md#target)-Service, den Sie hinzugefügt haben, und verwenden Sie den Abschnitt **[!UICONTROL Report Suite Overrides]** , um die gewünschten Datenstromüberschreibungen hinzuzufügen, wie in der Abbildung unten dargestellt.

Wählen Sie **[!UICONTROL Show Batch Mode]** aus, um die Batch-Bearbeitung der Report Suite-Überschreibungen zu aktivieren. Sie können eine Liste mit Report Suite-Überschreibungen kopieren und einfügen und dabei pro Zeile eine Report Suite eingeben.

![Screenshot der Datenstrom-Benutzeroberfläche mit den Einstellungen des Adobe Analytics-Dienstes, wobei die Report Suite-Überschreibungen hervorgehoben sind.](assets/overrides/override-analytics.png)

Nachdem Sie die gewünschten Überschreibungen hinzugefügt haben, speichern Sie Ihre Datenstromeinstellungen.

Ihre Adobe Analytics-Datenstromüberschreibungen sollten jetzt konfiguriert sein. Jetzt können Sie [die Überschreibungen über die Web-SDK oder mobile SDK an die Edge Network senden](#send-overrides).

### Datenstromüberschreibungen für Experience Platform-Ereignisdatensätze {#event-dataset-overrides}

Um Datenstromüberschreibungen für Experience Platform-Ereignisdatensätze zu konfigurieren, müssen Sie zunächst einen [Adobe Experience Platform](configure.md#aep)-Datenstrom erstellt haben. Befolgen Sie die Anweisungen, mit dem [Adobe Experience Platform](configure.md#aep)-Dienst einen [Datenstrom zu konfigurieren](configure.md).

Nachdem Sie den Datenstrom erstellt haben, bearbeiten Sie den [Adobe Experience Platform](configure.md#aep)-Service, den Sie hinzugefügt haben, und wählen Sie die Option **[!UICONTROL Add Event Dataset]** aus, um einen oder mehrere Ereignis-Datensätze zu überschreiben, wie in der Abbildung unten dargestellt.

![Screenshot der Datenstrom-Benutzeroberfläche mit den Einstellungen des Adobe Experience Platform-Dienstes, wobei die Überschreibungen des Ereignisdatensatzes hervorgehoben sind.](assets/overrides/override-aep.png)

Nachdem Sie die gewünschten Überschreibungen hinzugefügt haben, speichern Sie Ihre Datenstromeinstellungen.

Sie sollten jetzt die Adobe Experience Platform-Datenstromüberschreibungen konfiguriert haben. Jetzt können Sie [die Überschreibungen über die Web-SDK oder mobile SDK an die Edge Network senden](#send-overrides).

### Datenstromüberschreibungen für ID-Synchronisierungs-Container von Drittanbietern {#container-overrides}

Um Datenstromüberschreibungen für ID-Synchronisierungs-Container von Drittanbietern zu konfigurieren, müssen Sie zunächst einen Datenstrom erstellen lassen. Befolgen Sie die Anweisungen zum [Konfigurieren eines Datenstroms](configure.md), um einen Datenstrom zu erstellen.

Nachdem Sie den Datenstrom erstellt haben, navigieren Sie zu **[!UICONTROL Advanced Options]** und aktivieren Sie die Option **[!UICONTROL Third Party ID Sync]** .

Verwenden Sie dann den Abschnitt **[!UICONTROL Container ID Overrides]** , um die Container-IDs hinzuzufügen, die Sie die Standardeinstellung überschreiben möchten, wie in der Abbildung unten dargestellt.

>[!IMPORTANT]
>
>Container-IDs müssen numerische Werte sein, z. B. `1234567`, nicht aber Zeichenfolgen wie `"1234567"`. Wenn Sie einen Zeichenfolgenwert über das Web SDK als Container-ID-Überschreibung senden, erhalten Sie einen Fehler.

![Screenshot der Datenstrom-Benutzeroberfläche mit den Einstellungen des Datenstroms, wobei der Container für die ID-Synchronisierung von Drittanbietern hervorgehoben ist.](assets/overrides/override-container.png)

Nachdem Sie die gewünschten Überschreibungen hinzugefügt haben, speichern Sie Ihre Datenstromeinstellungen.

Sie sollten jetzt die Überschreibungen des ID-Synchronisierungs-Containers konfiguriert haben. Jetzt können Sie [die Überschreibungen über die Web-SDK oder mobile SDK an die Edge Network senden](#send-overrides).

## Überschreibungen an Edge Network senden {#send-overrides}

Nach dem Konfigurieren von Datenstrom-Überschreibungen in der Datenerfassungs-Benutzeroberfläche können Sie die Überschreibungen über die Web-SDK oder die mobile SDK an die Edge Network senden.

* **Web SDK**: Siehe [Überschreibungen der Datenstromkonfiguration](/help/collection/js/commands/configure/edgeconfigoverrides.md) für Code-Beispiele für die JavaScript-Bibliothek.
* **Mobile SDK**: Überschreibungen der Datenstrom-ID können entweder über die [sendEvent-API](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-sendevent/) oder mithilfe von [Rules](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-rules/) gesendet werden.

## Payload-Beispiel {#payload-example}

Die obigen Beispiele generieren eine [!DNL Edge Network] Payload, die der folgenden ähnelt.

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
