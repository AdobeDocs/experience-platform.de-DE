---
title: Verarbeiten von Kundeneinwilligungsdaten mit dem Adobe Experience Platform Web SDK
topic-legacy: getting started
description: Erfahren Sie, wie Sie das Adobe Experience Platform Web SDK integrieren, um Kundeneinwilligungsdaten in Adobe Experience Platform mit dem Adobe 2.0-Standard zu verarbeiten.
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1254'
ht-degree: 2%

---

# Integrieren des Platform Web SDK zur Verarbeitung von Kundeneinwilligungsdaten mithilfe des Adobe 2.0-Standards

Mit dem Adobe Experience Platform Web SDK können Sie von Consent Management Platforms (CMP) generierte Zustimmungssignale von Kunden abrufen und an Adobe Experience Platform senden, sobald ein Zustimmungsänderungsereignis eintritt.

**Das SDK verfügt nicht standardmäßig** über eine Schnittstelle mit CMPs. Sie müssen bestimmen, wie das SDK in Ihre Website integriert werden kann, auf Zustimmungsänderungen in der CMP warten und den entsprechenden Befehl aufrufen. Dieses Dokument enthält allgemeine Anleitungen zur Integration Ihres CMP mit dem Platform Web SDK.

>[!NOTE]
>
>Dieses Handbuch führt Sie durch die Schritte zur Integration des SDK über eine Tag-Erweiterung in der Datenerfassungs-Benutzeroberfläche. Wenn Sie stattdessen die eigenständige Version des SDK verwenden möchten, lesen Sie die folgenden Dokumente:
>
>* [Konfigurieren eines Datenspeichers](../../../../edge/fundamentals/datastreams.md)
* [Installieren des SDK](../../../../edge/fundamentals/installing-the-sdk.md)
* [Konfigurieren des SDK für Zustimmungsbefehle](../../../../edge/consent/supporting-consent.md)


## Voraussetzungen

In diesem Tutorial wird davon ausgegangen, dass Sie bereits ermittelt haben, wie Einwilligungsdaten in Ihrer CMP generiert werden, und einen Datensatz mit Einwilligungsfeldern erstellt haben, der für das Echtzeit-Kundenprofil aktiviert wurde. Weitere Informationen zu diesen Schritten finden Sie in der Übersicht über die [Verarbeitung der Einwilligung in Experience Platform](./overview.md) , bevor Sie zu diesem Handbuch zurückkehren.

Darüber hinaus setzt dieses Handbuch ein Verständnis der Tag-Erweiterungen und deren Installation in Webanwendungen voraus. Weitere Informationen finden Sie in der folgenden Dokumentation:

* [Übersicht über Tags](../../../../tags/home.md)
* [Schnellstartanleitung](../../../../tags/quick-start/quick-start.md)
* [Veröffentlichungsübersicht](../../../../tags/ui/publishing/overview.md)

## Einrichten eines Datastreams

Damit das SDK Daten an Experience Platform senden kann, muss in der Datenerfassungs-Benutzeroberfläche ein vorhandener Datastream für Platform eingerichtet sein. Darüber hinaus muss der [!UICONTROL Profildatensatz], den Sie für die Konfiguration auswählen, standardisierte Einwilligungsfelder enthalten.

Nachdem Sie eine neue Konfiguration erstellt oder eine vorhandene zur Bearbeitung ausgewählt haben, wählen Sie die Umschalter-Schaltfläche neben **[!UICONTROL Adobe Experience Platform]** aus. Verwenden Sie anschließend die unten aufgeführten Werte, um das Formular auszufüllen.

![](../../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Datenspeicherfeld | Wert |
| --- | --- |
| [!UICONTROL Sandbox] | Der Name der Plattform [Sandbox](../../../../sandboxes/home.md), die die erforderliche Streaming-Verbindung und Datensätze zum Einrichten des Datastreams enthält. |
| [!UICONTROL Streaming-Inlet] | Eine gültige Streaming-Verbindung für die Experience Platform. Lesen Sie das Tutorial zu [Erstellen einer Streaming-Verbindung](../../../../ingestion/tutorials/create-streaming-connection-ui.md) , wenn Sie keinen vorhandenen Streaming-Inlet haben. |
| [!UICONTROL Ereignis-Datensatz] | Ein [!DNL XDM ExperienceEvent] -Datensatz, an den Sie Ereignisdaten mit dem SDK senden möchten. Sie müssen zwar einen Ereignis-Datensatz bereitstellen, um einen Platform-Datenspeicher zu erstellen, beachten Sie jedoch, dass das direkte Senden von Zustimmungsdaten über Ereignisse derzeit nicht unterstützt wird. |
| [!UICONTROL Profildatensatz] | Der [!DNL Profile]-aktivierte Datensatz mit Feldern zur Kundenzustimmung, den Sie zuvor erstellt haben. |

Wählen Sie nach Abschluss des Vorgangs **[!UICONTROL Speichern]** am unteren Bildschirmrand aus und folgen Sie den weiteren Anweisungen, um die Konfiguration abzuschließen.


## Installieren und Konfigurieren des Platform Web SDK

Nachdem Sie einen Datenspeicher erstellt haben, wie im vorherigen Abschnitt beschrieben, müssen Sie die Platform Web SDK-Erweiterung konfigurieren, die Sie letztendlich auf Ihrer Site bereitstellen werden. Wenn die SDK-Erweiterung nicht in Ihrer Tag-Eigenschaft installiert ist, wählen Sie im linken Navigationsbereich **[!UICONTROL Erweiterungen]** und danach die Registerkarte **[!UICONTROL Katalog]** aus. Wählen Sie dann **[!UICONTROL Install]** unter der Platform SDK-Erweiterung in der Liste der verfügbaren Erweiterungen aus.

![](../../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Wählen Sie beim Konfigurieren des SDK unter **[!UICONTROL Edge-Konfigurationen]** den Datastream aus, den Sie im vorherigen Schritt erstellt haben.

![](../../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Wählen Sie **[!UICONTROL Save]** aus, um die Erweiterung zu installieren.

### Erstellen eines Datenelements zum Festlegen der Standardzustimmung

Wenn die SDK-Erweiterung installiert ist, können Sie ein Datenelement erstellen, das den standardmäßigen Datenerfassungs-Zustimmungswert (`collect.val`) für Ihre Benutzer darstellt. Dies kann nützlich sein, wenn Sie je nach Benutzer unterschiedliche Standardwerte haben möchten, z. B. `pending` für Benutzer der Europäischen Union und `in` für Benutzer in Nordamerika.

In diesem Anwendungsfall können Sie Folgendes implementieren, um die Standardzustimmung auf Grundlage der Region des Benutzers festzulegen:

1. Bestimmen Sie die Region des Benutzers auf dem Webserver.
1. Rendern Sie vor dem Tag `script` (Einbettungscode) auf der Web-Seite ein separates Tag `script` , das eine `adobeDefaultConsent` -Variable basierend auf der Region des Benutzers festlegt.
1. Richten Sie ein Datenelement ein, das die JavaScript-Variable `adobeDefaultConsent` verwendet, und verwenden Sie dieses Datenelement als standardmäßigen Zustimmungswert für den Benutzer.

Wenn die Region des Benutzers durch eine CMP bestimmt wird, können Sie stattdessen die folgenden Schritte verwenden:

1. Behandeln Sie das Ereignis &quot;CMP geladen&quot;auf der Seite.
1. Legen Sie im Ereignishandler eine `adobeDefaultConsent` -Variable auf Grundlage der Region des Benutzers fest und laden Sie dann das Tag-Bibliotheksskript mit JavaScript.
1. Richten Sie ein Datenelement ein, das die JavaScript-Variable `adobeDefaultConsent` verwendet, und verwenden Sie dieses Datenelement als standardmäßigen Zustimmungswert für den Benutzer.

Um ein Datenelement in der Datenerfassungs-Benutzeroberfläche zu erstellen, wählen Sie **[!UICONTROL Datenelemente]** im linken Navigationsbereich und dann **[!UICONTROL Datenelement hinzufügen]** aus, um zum Dialogfeld für die Datenelementerstellung zu navigieren.

Von hier aus müssen Sie ein [!UICONTROL JavaScript-Variable]-Datenelement erstellen, das auf `adobeDefaultConsent` basiert. Wählen Sie **[!UICONTROL Speichern]**, wenn Sie fertig sind.

![](../../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Nachdem das Datenelement erstellt wurde, navigieren Sie zurück zur Konfigurationsseite der Web SDK-Erweiterung . Wählen Sie im Abschnitt [!UICONTROL Datenschutz] die Option **[!UICONTROL Wird durch Datenelement]** bereitgestellt und wählen Sie im bereitgestellten Dialogfeld das zuvor erstellte standardmäßige Datenelement für die Einwilligung aus.

![](../../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Bereitstellen der Erweiterung auf Ihrer Website

Nachdem Sie die Konfiguration der Erweiterung abgeschlossen haben, kann sie in Ihre Website integriert werden. Ausführliche Informationen zum Bereitstellen des aktualisierten Bibliotheks-Builds finden Sie im [Publishing-Handbuch](https://experienceleague.adobe.com/docs/launch/using/publish/overview.html?lang=de) in der Tag-Dokumentation.

## Festlegen von Befehlen zur Änderung der Zustimmung {#commands}

Nachdem Sie die SDK-Erweiterung in Ihre Website integriert haben, können Sie mit der Verwendung des Befehls `setConsent` des Platform Web SDK beginnen, um Zustimmungsdaten an Platform zu senden.

Es gibt zwei Szenarien, in denen `setConsent` auf Ihrer Site aufgerufen werden sollte:

1. Wenn die Einwilligung auf der Seite geladen wird (d. h. bei jedem Laden der Seite)
1. Als Teil eines CMP-Hooks oder Ereignis-Listeners, der Änderungen in den Zustimmungseinstellungen erkennt

>[!NOTE]
Eine Einführung in die allgemeine Syntax für Platform SDK-Befehle finden Sie im Dokument zu [Ausführen von Befehlen](../../../../edge/fundamentals/executing-commands.md).

Der Befehl `setConsent` erwartet zwei Argumente:

1. Eine Zeichenfolge, die den Befehlstyp angibt (in diesem Fall `"setConsent"`).
1. Ein Payload-Objekt, das eine einzelne Eigenschaft vom Typ Array enthält: `consent`. Das Array `consent` muss mindestens ein Objekt enthalten, das die erforderlichen Einwilligungsfelder für den Adobe-Standard bereitstellt.

Die erforderlichen Einwilligungsfelder für den Adobe-Standard sind im folgenden Beispiel für den Aufruf `setConsent` dargestellt:

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
| `standard` | Der verwendete Zustimmungsstandard. Für den Adobe-Standard muss dieser Wert auf `Adobe` gesetzt werden. |
| `version` | Die Versionsnummer des Zustimmungsstandards, angegeben unter `standard`. Dieser Wert muss auf `2.0` gesetzt werden, damit die Zustimmungsverarbeitung nach Adobe-Standard erfolgt. |
| `value` | Die aktualisierten Zustimmungsinformationen des Kunden, die als XDM-Objekt bereitgestellt werden, das der Struktur der Einwilligungsfelder des Profilaktivierten Datensatzes entspricht. |

>[!NOTE]
Wenn Sie andere Zustimmungsstandards zusammen mit `Adobe` verwenden (z. B. `IAB TCF`), können Sie dem `consent`-Array für jeden Standard zusätzliche Objekte hinzufügen. Jedes Objekt muss die entsprechenden Werte für `standard`, `version` und `value` für den Zustimmungsstandard enthalten, den sie darstellen.

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

Alle [!DNL Platform SDK]-Befehle geben Zusagen zurück, die angeben, ob der Aufruf erfolgreich war oder fehlgeschlagen ist. Sie können diese Antworten dann für zusätzliche Logik verwenden, z. B. für die Anzeige von Bestätigungsnachrichten an den Kunden. Spezifische Beispiele finden Sie im Abschnitt [Umgang mit Erfolg oder Fehler](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) im Handbuch zum Ausführen von SDK-Befehlen .

## Nächste Schritte

In diesem Handbuch haben Sie die Platform Web SDK-Erweiterung so konfiguriert, dass Einwilligungsdaten an Experience Platform gesendet werden. Sie können jetzt zur Übersicht über die Zustimmungsverarbeitung zurückkehren, um zu erfahren, wie Sie Ihre Implementierung testen können.](./overview.md#test-implementation)[
