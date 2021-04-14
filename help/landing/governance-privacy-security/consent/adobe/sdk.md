---
title: Verarbeiten von Kundenbestätigungsdaten mit dem Adobe Experience Platform Web SDK
topic: Erste Schritte
description: Erfahren Sie, wie Sie das Adobe Experience Platform Web SDK zur Verarbeitung von Daten zur Kundengenehmigung in Adobe Experience Platform mit dem Adobe 2.0-Standard integrieren.
translation-type: tm+mt
source-git-commit: fee3f005ca3679f8639cea45c16150090b2a1e0f
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 0%

---


# Integrieren Sie das Platform Web SDK, um Daten zur Kundeneinwilligung unter Verwendung des Adobe 2.0-Standards zu verarbeiten.

Mit dem Adobe Experience Platform Web SDK können Sie von CMPs (Consent Management Platforms) generierte Zustimmungssignale abrufen und sie an Adobe Experience Platform senden, sobald ein Ereignis zur Änderung der Einwilligung eintritt.

**Das SDK kann nicht standardmäßig mit CMPs verknüpft werden**. Es liegt an Ihnen, zu bestimmen, wie das SDK in Ihre Website integriert werden soll, auf Änderungen der Zustimmung im CMP zu hören und den entsprechenden Befehl aufzurufen. Dieses Dokument enthält allgemeine Anleitungen zur Integration des CMP in das Platform Web SDK.

## Voraussetzungen

In diesem Lernprogramm wird davon ausgegangen, dass Sie bereits ermittelt haben, wie in Ihrem CMP Genehmigungsdaten generiert werden, und dass Sie einen Datensatz mit Einwilligungsfeldern erstellt haben, die für das Echtzeit-Profil von Kunden aktiviert wurden. Weitere Informationen zu diesen Schritten finden Sie in der Übersicht über die [Verarbeitung der Einwilligung in Experience Platform](./overview.md), bevor Sie zu diesem Handbuch zurückkehren.

Darüber hinaus erfordert dieses Handbuch ein Verständnis der Adobe Experience Platform Launch-Erweiterungen und ihrer Installation in Webanwendungen. Weitere Informationen finden Sie in der folgenden Dokumentation:

* [platform launch - Übersicht](https://experienceleague.adobe.com/docs/launch/using/home.html)
* [Schnellstartanleitung](https://experienceleague.adobe.com/docs/launch/using/get-started/quick-start.html)
* [Veröffentlichungsübersicht](https://experienceleague.adobe.com/docs/launch/using/publish/overview.html)

## Einrichten einer Edge-Konfiguration

Damit das SDK Daten an die Experience Platform senden kann, müssen Sie über eine in Adobe Experience Platform Launch eingerichtete Edge-Konfiguration für die Plattform verfügen. Darüber hinaus müssen die für die Konfiguration ausgewählten [!UICONTROL Profil-Dataset] standardisierte Kennwortfelder enthalten.

Nachdem Sie eine neue Konfiguration erstellt oder eine vorhandene zur Bearbeitung ausgewählt haben, klicken Sie auf die Umschalter neben **[!UICONTROL Adobe Experience Platform]**. Verwenden Sie anschließend die unten aufgeführten Werte, um das Formular auszufüllen.

![](../../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Edge-Konfigurationsfeld | Wert |
| --- | --- |
| [!UICONTROL Sandbox] | Der Name der Plattform [Sandbox](../../../../sandboxes/home.md), die die erforderliche Streaming-Verbindung und die zum Einrichten der Edge-Konfiguration erforderlichen Datensätze enthält. |
| [!UICONTROL Streaming-Inlet] | Eine gültige Streaming-Verbindung zur Experience Platform. Sehen Sie sich das Lernprogramm unter [Erstellen einer Streaming-Verbindung](../../../../ingestion/tutorials/create-streaming-connection-ui.md) an, wenn Sie keinen vorhandenen Streaming-Einlass haben. |
| [!UICONTROL Ereignis DataSet] | Ein [!DNL XDM ExperienceEvent]-Datensatz, den Sie planen, Ereignis-Daten an die Verwendung des SDK zu senden. Sie müssen zwar einen Ereignis-Datensatz bereitstellen, um eine Plattformedge-Konfiguration zu erstellen, beachten Sie jedoch, dass das Senden von Genehmigungsdaten direkt über Ereignis derzeit nicht unterstützt wird. |
| [!UICONTROL Profil DataSet] | Der [!DNL Profile]-aktivierte Datensatz mit den zuvor erstellten Feldern zur Kundengenehmigung. |

Wenn Sie fertig sind, wählen Sie unten im Bildschirm **[!UICONTROL Speichern]** und folgen Sie den weiteren Eingabeaufforderungen, um die Konfiguration abzuschließen.


## Installieren und Konfigurieren der Platform Web SDK-Erweiterung

Nachdem Sie eine Edge-Konfiguration wie im vorherigen Abschnitt beschrieben erstellt haben, müssen Sie die Platform Web SDK-Erweiterung konfigurieren, die Sie letztendlich auf Ihrer Site bereitstellen werden. Wenn die SDK-Erweiterung nicht auf Ihrer Platform launch-Eigenschaft installiert ist, wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation und anschließend die Registerkarte **[!UICONTROL Katalog]**. Wählen Sie dann **[!UICONTROL Install]** unter der Platform SDK-Erweiterung in der Liste der verfügbaren Erweiterungen.

![](../../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Wählen Sie beim Konfigurieren des SDK unter **[!UICONTROL Edge Configurations]** die Konfiguration aus, die Sie im vorherigen Schritt erstellt haben.

![](../../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Wählen Sie **[!UICONTROL Speichern]**, um die Erweiterung zu installieren.

### Datenelement zum Festlegen der Standardgenehmigung erstellen

Wenn die SDK-Erweiterung installiert ist, können Sie ein Datenelement erstellen, das den standardmäßigen Datenerfassungs-Zustimmungswert (`collect.val`) für Ihre Benutzer darstellt. Dies kann nützlich sein, wenn Sie je nach Benutzer unterschiedliche Standardwerte haben möchten, z. B. `pending` für Benutzer europäischer Vereinigungen und `in` für Benutzer in Nordamerika.

In diesem Anwendungsfall können Sie Folgendes implementieren, um die Standardgenehmigung basierend auf der Region des Benutzers festzulegen:

1. Legen Sie die Region des Benutzers auf dem Webserver fest.
1. Richten Sie vor dem Platform launch-Skript-Tag (Einbettungscode) auf der Webseite ein separates Skript-Tag aus, das die Variable `adobeDefaultConsent` auf Grundlage der Benutzerregion festlegt.
1. Richten Sie ein Datenelement ein, das die JavaScript-Variable `adobeDefaultConsent` verwendet, und verwenden Sie dieses Datenelement als Standardwert für die Zustimmung des Benutzers.

Wenn die Region des Benutzers durch einen CMP bestimmt wird, können Sie stattdessen die folgenden Schritte durchführen:

1. Behandeln Sie das Ereignis &quot;CMP geladen&quot;auf der Seite.
1. Legen Sie im Ereignis-Handler die Variable `adobeDefaultConsent` auf Grundlage des Benutzerbereichs fest und laden Sie dann das Platform launch-Bibliotheksskript mit JavaScript.
1. Richten Sie ein Datenelement ein, das die JavaScript-Variable `adobeDefaultConsent` verwendet, und verwenden Sie dieses Datenelement als Standardwert für die Zustimmung des Benutzers.

Um ein Datenelement in der Platform launch-Benutzeroberfläche zu erstellen, wählen Sie **[!UICONTROL Datenelemente]** in der linken Navigation und dann **[!UICONTROL Hinzufügen Datenelement]**, um zum Dialogfeld zur Datenelementerstellung zu navigieren.

Von hier aus müssen Sie ein [!UICONTROL JavaScript-Variable]-Datenelement erstellen, das auf `adobeDefaultConsent` basiert. Wählen Sie **[!UICONTROL Speichern]**, wenn Sie fertig sind.

![](../../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Nachdem das Datenelement erstellt wurde, navigieren Sie zurück zur Konfigurationsseite der Web SDK-Erweiterung. Wählen Sie im Abschnitt [!UICONTROL Datenschutz] **[!UICONTROL Von Datenelement]** bereitgestellt und wählen Sie im bereitgestellten Dialogfeld das zuvor erstellte Datenelement für die Standardgenehmigung aus.

![](../../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Bereitstellen der Erweiterung auf Ihrer Website

Nachdem Sie die Erweiterung konfiguriert haben, kann sie in Ihre Website integriert werden. Detaillierte Informationen zum Bereitstellen des aktualisierten Bibliotheksaufbaus finden Sie im Handbuch [Veröffentlichung](https://experienceleague.adobe.com/docs/launch/using/publish/overview.html) in der Platform launch.

## Befehle zum Ändern der Zustimmung

Nachdem Sie die SDK-Erweiterung in Ihre Website integriert haben, können Sie Beginn mit dem Platform Web SDK `setConsent`-Befehl ausführen, um Genehmigungsdaten an die Plattform zu senden.

Es gibt zwei Szenarien, in denen `setConsent` auf Ihrer Site aufgerufen werden sollte:

1. Wenn die Einwilligung auf der Seite geladen wird (d. h. bei jedem Laden der Seite)
1. Als Teil eines CMP-Haken- oder Ereignis-Listeners, der Änderungen in den Einstellungen für die Zustimmung erkennt

>[!NOTE]
>
>Eine Einführung in die gebräuchliche Syntax für Platform SDK-Befehle finden Sie im Dokument zu [Ausführen von Befehlen](../../../../edge/fundamentals/executing-commands.md).

Der Befehl `setConsent` erwartet zwei Argumente:

1. Eine Zeichenfolge, die den Befehlstyp angibt (in diesem Fall `"setConsent"`)
1. Ein Payload-Objekt, das eine einzelne Array-Eigenschaft enthält: `consent`. Das `consent`-Array muss mindestens ein Objekt enthalten, das die erforderlichen Felder für die Zustimmung für den Adobe-Standard bereitstellt.

Die erforderlichen Felder für die Zustimmung zum Standardaufruf der Adobe sind im folgenden Beispiel dargestellt:`setConsent`

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
| `version` | Die Versionsnummer des Zustimmungsstandards, die unter `standard` angegeben ist. Dieser Wert muss auf `2.0` gesetzt werden, damit die Adobe-Standard-Verarbeitung der Zustimmung ausgeführt werden kann. |
| `value` | Die aktualisierten Informationen zum Einverständnis des Kunden, die als XDM-Objekt bereitgestellt werden, das der Struktur der Einwilligungsfelder des Profil-aktivierten Datensatzes entspricht. |

>[!NOTE]
>
>Wenn Sie andere Zustimmungsstandards in Verbindung mit `Adobe` (z. B. `IAB TCF`) verwenden, können Sie dem `consent`-Array für jeden Standard weitere Objekte hinzufügen. Jedes Objekt muss geeignete Werte für `standard`, `version` und `value` für den von ihnen repräsentierten Zustimmungsstandard enthalten.

Das folgende JavaScript zeigt eine Funktion, die Änderungen der Voreinstellungen für die Einwilligung auf einer Website verarbeitet, die als Rückruf in einem Ereignis-Listener oder CMP-Haken verwendet werden kann:

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

Alle [!DNL Platform SDK]-Befehle geben Versprechungen zurück, die angeben, ob der Aufruf erfolgreich war oder fehlgeschlagen ist. Sie können diese Antworten dann für zusätzliche Logik verwenden, z. B. für die Anzeige von Bestätigungsmeldungen an den Kunden. Genaue Beispiele finden Sie im Abschnitt [Handhabung von Erfolg oder Fehler](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) im Handbuch zum Ausführen von SDK-Befehlen.

## Nächste Schritte

Durch Befolgen dieses Handbuchs haben Sie die Plattform Web SDK-Erweiterung so konfiguriert, dass die Genehmigungsdaten an die Experience Platform gesendet werden. Sie können nun zur Übersicht über die Verarbeitung der Einwilligung zurückkehren, um Anweisungen zum [Testen Ihrer Implementierung](./overview.md#test-implementation) zu erhalten.