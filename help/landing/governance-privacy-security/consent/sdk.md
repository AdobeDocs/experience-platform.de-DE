---
title: Verarbeiten von Kundeneinwilligungsdaten mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie das Adobe Experience Platform Web SDK integrieren, um Kundeneinwilligungsdaten in Adobe Experience Platform zu verarbeiten.
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 2%

---

# Integrieren des Platform Web SDK zur Verarbeitung von Daten zur Kundenzustimmung

Mit dem Adobe Experience Platform Web SDK können Sie von Consent Management Platforms (CMP) generierte Zustimmungssignale von Kunden abrufen und an Adobe Experience Platform senden, sobald ein Zustimmungsänderungsereignis eintritt.

**Das SDK verfügt nicht standardmäßig über eine Schnittstelle mit CMPs**. Sie müssen bestimmen, wie das SDK in Ihre Website integriert werden kann, auf Zustimmungsänderungen in der CMP warten und den entsprechenden Befehl aufrufen. Dieses Dokument enthält allgemeine Anleitungen zur Integration Ihres CMP mit dem Platform Web SDK.

## Voraussetzungen {#prerequisites}

In diesem Tutorial wird davon ausgegangen, dass Sie bereits ermittelt haben, wie Einwilligungsdaten in Ihrer CMP generiert werden, und einen Datensatz mit Einwilligungsfeldern erstellt haben, die dem Adobe-Standard oder dem IAB Transparency and Consent Framework (TCF) 2.0-Standard entsprechen. Wenn Sie diesen Datensatz noch nicht erstellt haben, lesen Sie die folgenden Tutorials, bevor Sie zu diesem Handbuch zurückkehren:

* [Datensatz mit dem Adobe-Standard erstellen](./adobe/dataset.md)
* [Datensatz mit dem TCF 2.0-Standard erstellen](./iab/dataset.md)

Dieses Handbuch folgt dem Workflow zum Einrichten des SDK mithilfe der Tag-Erweiterung in der Benutzeroberfläche. Wenn Sie die -Erweiterung nicht verwenden möchten und die eigenständige Version des SDK lieber direkt auf Ihrer Site einbetten möchten, lesen Sie die folgenden Dokumente anstelle dieses Handbuchs:

* [Konfigurieren eines Datenstroms](../../../edge/datastreams/overview.md)
* [Installieren des SDK](../../../edge/fundamentals/installing-the-sdk.md)
* [Konfigurieren des SDK für Zustimmungsbefehle](../../../edge/consent/supporting-consent.md)

Die Installationsschritte in diesem Handbuch erfordern ein Verständnis der Tag-Erweiterungen und deren Installation in Webanwendungen. Weitere Informationen finden Sie in der folgenden Dokumentation:

* [Übersicht über Tags](../../../tags/home.md)
* [Schnellstartanleitung](../../../tags/quick-start/quick-start.md)
* [Veröffentlichungsübersicht](../../../tags/ui/publishing/overview.md)

## Einrichten eines Datastreams

Damit das SDK Daten an Experience Platform senden kann, müssen Sie zunächst einen Datenspeicher konfigurieren. Wählen Sie in der Datenerfassungs-Benutzeroberfläche oder der Benutzeroberfläche &quot;Experience Platform&quot;die Option **[!UICONTROL Datenspeicher]** in der linken Navigation.

Nachdem Sie einen neuen Datensatz erstellt oder einen vorhandenen ausgewählt haben, den Sie bearbeiten möchten, wählen Sie die Umschalter-Schaltfläche neben **[!UICONTROL Adobe Experience Platform]**. Verwenden Sie anschließend die unten aufgeführten Werte, um das Formular auszufüllen.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Datenspeicherfeld | Wert |
| --- | --- |
| [!UICONTROL Sandbox] | Der Name der Plattform [Sandbox](../../../sandboxes/home.md) , die die erforderliche Streaming-Verbindung und Datensätze zum Einrichten des Datastreams enthält. |
| [!UICONTROL Streaming-Inlet] | Eine gültige Streaming-Verbindung für die Experience Platform. Siehe Tutorial zu [Erstellen einer Streaming-Verbindung](../../../ingestion/tutorials/create-streaming-connection-ui.md) , wenn Sie keinen Streaming-Inlet haben. |
| [!UICONTROL Ereignis-Datensatz] | Ein [!DNL XDM ExperienceEvent] Datensatz, an den Sie Ereignisdaten mit dem SDK senden möchten. Sie müssen zwar einen Ereignis-Datensatz bereitstellen, um einen Platform-Datenspeicher zu erstellen, beachten Sie jedoch, dass über Ereignisse gesendete Zustimmungsdaten in nachgelagerten Durchsetzungs-Workflows nicht berücksichtigt werden. |
| [!UICONTROL Profildatensatz] | Die [!DNL Profile]-aktivierter Datensatz mit von Ihnen erstellten Feldern zur Kundenzustimmung [früher](#prerequisites). |

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Speichern]** unten auf dem Bildschirm und folgen Sie weiteren Anweisungen, um die Konfiguration abzuschließen.

## Installieren und Konfigurieren des Platform Web SDK

Nachdem Sie einen Datenspeicher erstellt haben, wie im vorherigen Abschnitt beschrieben, müssen Sie die Platform Web SDK-Erweiterung konfigurieren, die Sie letztendlich auf Ihrer Site bereitstellen werden. Wenn die SDK-Erweiterung nicht in Ihrer Tag-Eigenschaft installiert ist, wählen Sie **[!UICONTROL Erweiterungen]** im linken Navigationsbereich, gefolgt von der **[!UICONTROL Katalog]** Registerkarte. Wählen Sie anschließend **[!UICONTROL Installieren]** unter der Platform SDK-Erweiterung in der Liste der verfügbaren Erweiterungen.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Beim Konfigurieren des SDK finden Sie unter **[!UICONTROL Edge-Konfigurationen]**, wählen Sie den Datenspeicher aus, den Sie im vorherigen Schritt erstellt haben.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Auswählen **[!UICONTROL Speichern]** , um die Erweiterung zu installieren.

### Erstellen eines Datenelements zum Festlegen der Standardzustimmung

Wenn die SDK-Erweiterung installiert ist, können Sie ein Datenelement erstellen, das den standardmäßigen Datenerfassungs-Zustimmungswert darstellt (`collect.val`) für Ihre Benutzer. Dies kann nützlich sein, wenn Sie je nach Benutzer unterschiedliche Standardwerte haben möchten, z. B. `pending` für Benutzer der Europäischen Union und `in` für nordamerikanische Benutzer.

In diesem Anwendungsfall können Sie Folgendes implementieren, um die Standardzustimmung auf Grundlage der Region des Benutzers festzulegen:

1. Bestimmen Sie die Region des Benutzers auf dem Webserver.
1. Vor `script` -Tag (Einbettungscode) auf der Web-Seite ein separates `script` -Tag, das `adobeDefaultConsent` auf Grundlage der Region des Benutzers.
1. Richten Sie ein Datenelement ein, das die `adobeDefaultConsent` JavaScript-Variable und verwenden Sie dieses Datenelement als standardmäßigen Zustimmungswert für den Benutzer.

Wenn die Region des Benutzers durch eine CMP bestimmt wird, können Sie stattdessen die folgenden Schritte verwenden:

1. Behandeln Sie das Ereignis &quot;CMP geladen&quot;auf der Seite.
1. Legen Sie im Ereignis-Handler eine `adobeDefaultConsent` auf Grundlage der Region des Benutzers und laden Sie dann das Tag-Bibliotheksskript mithilfe von JavaScript.
1. Richten Sie ein Datenelement ein, das die `adobeDefaultConsent` JavaScript-Variable und verwenden Sie dieses Datenelement als standardmäßigen Zustimmungswert für den Benutzer.

Um ein Datenelement in der Benutzeroberfläche zu erstellen, wählen Sie **[!UICONTROL Datenelemente]** Wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Datenelement hinzufügen]** , um zum Dialogfeld zur Datenelementerstellung zu navigieren.

Von hier aus müssen Sie eine [!UICONTROL JavaScript-Variable] Datenelement basierend auf `adobeDefaultConsent`. Wählen Sie **[!UICONTROL Speichern]**, wenn Sie fertig sind.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Nachdem das Datenelement erstellt wurde, navigieren Sie zurück zur Konfigurationsseite der Web SDK-Erweiterung . Unter dem [!UICONTROL Datenschutz] Bereich, wählen Sie **[!UICONTROL Wird vom Datenelement bereitgestellt]** und verwenden Sie das bereitgestellte Dialogfeld, um das zuvor erstellte standardmäßige Datenelement für die Einwilligung auszuwählen.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Bereitstellen der Erweiterung auf Ihrer Website

Nachdem Sie die Konfiguration der Erweiterung abgeschlossen haben, kann sie in Ihre Website integriert werden. Siehe Abschnitt [Publishing-Handbuch](../../../tags/ui/publishing/overview.md) in der Tag-Dokumentation finden Sie detaillierte Informationen zur Bereitstellung Ihres aktualisierten Bibliotheks-Builds.

## Festlegen von Befehlen zur Änderung der Zustimmung {#commands}

Nachdem Sie die SDK-Erweiterung in Ihre Website integriert haben, können Sie mit der Verwendung des Platform Web SDK beginnen `setConsent` -Befehl zum Senden von Einwilligungsdaten an Platform.

Die `setConsent` -Befehl führt zwei Aktionen aus:

1. Aktualisiert die Profilattribute des Benutzers direkt im Profilspeicher. Dadurch werden keine Daten an den Data Lake gesendet.
1. Erstellt eine [Erlebnisereignis](../../../xdm/classes/experienceevent.md) , das ein mit Zeitstempel versehenes Konto des Zustimmungsänderungsereignisses aufzeichnet. Diese Daten werden direkt an den Data Lake gesendet und können verwendet werden, um Änderungen der Zustimmungsparameter im Laufe der Zeit zu verfolgen.

### Wann wird aufgerufen `setConsent`

Es gibt zwei Szenarien, in denen `setConsent` sollte auf Ihrer Site aufgerufen werden:

1. Wenn die Einwilligung auf der Seite geladen wird (d. h. bei jedem Laden der Seite)
1. Als Teil eines CMP-Hooks oder Ereignis-Listeners, der Änderungen in den Zustimmungseinstellungen erkennt

### `setConsent` Syntax

>[!NOTE]
>
>Eine Einführung in die allgemeine Syntax für Platform SDK-Befehle finden Sie im Dokument unter [Ausführen von Befehlen](../../../edge/fundamentals/executing-commands.md).

Die `setConsent` -Befehl erwartet zwei Argumente:

1. Eine Zeichenfolge, die den Befehlstyp angibt (in diesem Fall `"setConsent"`)
1. Ein Payload-Objekt, das eine einzelne Eigenschaft vom Typ Array enthält: `consent`. Die `consent` -Array muss mindestens ein Objekt enthalten, das die erforderlichen Einwilligungsfelder für den Adobe-Standard bereitstellt.

Die erforderlichen Einwilligungsfelder für den Adobe-Standard werden im folgenden Beispiel angezeigt `setConsent` Aufruf:

```js
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: {
        val: "y"
      },
      share: {
        val: "y"
      },
      personalize: {
        content: {
          val: "y"
        }
      },
      metadata: {
        time: "2020-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| Payload-Eigenschaft | Beschreibung |
| --- | --- |
| `standard` | Der verwendete Zustimmungsstandard. Für den Adobe-Standard muss dieser Wert auf `Adobe`. |
| `version` | Die unter `standard`. Dieser Wert muss auf `2.0` für die Verarbeitung von Einwilligungen nach Adobe-Standard. |
| `value` | Die aktualisierten Zustimmungsinformationen des Kunden, die als XDM-Objekt bereitgestellt werden, das der Struktur der Einwilligungsfelder des Profilaktivierten Datensatzes entspricht. |

>[!NOTE]
>
>Wenn Sie andere Zustimmungsstandards in Verbindung mit `Adobe` (z. B. `IAB TCF`) können Sie weitere Objekte zur `consent` -Array für jeden Standard. Jedes Objekt muss die entsprechenden Werte für `standard`, `version`und `value` für den Einverständnisstandard, den sie darstellen.

Das folgende JavaScript zeigt ein Beispiel für eine Funktion, die Änderungen der Zustimmungsvoreinstellungen auf einer Website verarbeitet, die als Rückruf in einem Ereignis-Listener oder CMP-Erweiterungspunkt verwendet werden kann:

```js
var setConsent = function () {

  // Retrieve the current consent data.
  var categories = getConsentData();

  // If the script is running on a consent change, generate a new timestamp.
  // If the script is running on page load, set the timestamp to when the consent values last changed.
  var now = new Date();
  var collectedAt = consentChanged ? now.toISOString() : categories.collectedAt;

  //  Map the consent values and timestamp to XDM
  var consentXDM = {
    collect: {
      val: categories.collect !== -1 ? "y" : "n"
    },
    personalize: {
      content: {
        val: categories.personalizeContent !== -1 ? "y" : "n"
      }
    },
    share: {
      val: categories.share !== -1 ? "y" : "n"
    },
    metadata: {
      time: collectedAt
    }
  };

  // Pass the XDM object to the Platform Web SDK
  alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: consentXDM
    }]
  });
});
```

## Umgang mit SDK-Antworten

Alle [!DNL Platform SDK] -Befehle geben Zusagen zurück, die angeben, ob der Aufruf erfolgreich war oder fehlgeschlagen ist. Sie können diese Antworten dann für zusätzliche Logik verwenden, z. B. für die Anzeige von Bestätigungsnachrichten an den Kunden. Siehe Abschnitt zu [Umgang mit Erfolg oder Fehlschlagen](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) im Handbuch zum Ausführen von SDK-Befehlen für spezifische Beispiele.

Nachdem Sie erfolgreich `setConsent` -Aufrufe mit dem SDK verwenden, können Sie mit dem Profil-Viewer in der Platform-Benutzeroberfläche überprüfen, ob Daten im Profilspeicher landen. Siehe Abschnitt zu [Profile nach Identität durchsuchen](../../../profile/ui/user-guide.md#browse-identity) für weitere Informationen.

## Nächste Schritte

In diesem Handbuch haben Sie die Platform Web SDK-Erweiterung so konfiguriert, dass Einwilligungsdaten an Experience Platform gesendet werden. Eine Anleitung zum Testen Ihrer Implementierung finden Sie in der Dokumentation zum Einverständnisstandard, den Sie implementieren:

* [Adobe Standard](./adobe/overview.md#test)
* [TCF 2.0-Standard](./iab/overview.md#test)
