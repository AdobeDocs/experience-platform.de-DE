---
title: Verarbeiten von Kundeneinverständnisdaten mit der Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie Adobe Experience Platform Web SDK integrieren können, um Kundeneinverständnisdaten in Adobe Experience Platform zu verarbeiten.
role: Developer
feature: Consent, Web SDK
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1293'
ht-degree: 2%

---

# Integrieren von Experience Platform Web SDK zur Verarbeitung von Kundeneinverständnisdaten

Mit der Adobe Experience Platform Web SDK können Sie Einverständnissignale von Kundinnen und Kunden abrufen, die von Einverständnisverwaltungsplattformen (CMPs) generiert wurden, und sie an Adobe Experience Platform senden, wenn ein Einverständnisänderungsereignis auftritt.

**Der SDK stellt standardmäßig keine Schnittstelle zu CMPs bereit**. Es liegt an Ihnen zu bestimmen, wie Sie die SDK in Ihre Website integrieren, auf Einverständnisänderungen in der CMP zu warten und den entsprechenden Befehl aufzurufen. Dieses Dokument enthält allgemeine Anleitungen zum Integrieren Ihres CMP mit Experience Platform Web SDK.

## Voraussetzungen {#prerequisites}

In diesem Tutorial wird davon ausgegangen, dass Sie bereits bestimmt haben, wie Einverständnisdaten in Ihrer CMP generiert werden, und einen Datensatz mit Einverständnisfeldern erstellt haben, die dem Adobe-Standard oder dem IAB Transparency and Consent Framework (TCF) 2.0-Standard entsprechen. Wenn Sie diesen Datensatz noch nicht erstellt haben, lesen Sie die folgenden Tutorials, bevor Sie zu diesem Handbuch zurückkehren:

* [Erstellen eines Datensatzes mit dem Adobe-Standard](./adobe/dataset.md)
* [Erstellen eines Datensatzes mit dem TCF 2.0-Standard](./iab/dataset.md)

Dieses Handbuch folgt dem Workflow zum Einrichten der SDK mithilfe der Tag-Erweiterung in der Benutzeroberfläche. Wenn Sie die -Erweiterung nicht verwenden möchten und es vorziehen würden, die eigenständige Version der SDK direkt auf Ihrer Site einzubetten, lesen Sie bitte die folgenden Dokumente anstelle dieses Handbuchs:

* [Konfigurieren eines Datenstroms](/help/datastreams/overview.md)
* [Installieren des SDK](/help/collection/js/install/overview.md)
* [Konfigurieren von SDK für Einverständnisbefehle](/help/collection/js/commands/configure/defaultconsent.md)

Die Installationsschritte in diesem Handbuch erfordern ein grundlegendes Verständnis von Tag-Erweiterungen und ihrer Installation in Web-Anwendungen. Weiterführende Informationen finden Sie in der folgenden Dokumentation:

* [Übersicht über Tags](/help/tags/home.md)
* [Schnellstartanleitung](/help/tags/quick-start/quick-start.md)
* [Veröffentlichungsübersicht](/help/tags/ui/publishing/overview.md)

## Einrichten eines Datenstroms

Damit SDK Daten an Experience Platform senden kann, müssen Sie zunächst einen Datenstrom konfigurieren. Wählen Sie in der Datenerfassungs-Benutzeroberfläche oder der Experience Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Datastreams]** aus.

Nachdem Sie einen neuen Datenstrom erstellt oder einen vorhandenen ausgewählt haben, um ihn zu bearbeiten, klicken Sie auf die Umschaltfläche neben **[!UICONTROL Adobe Experience Platform]**. Verwenden Sie als Nächstes die unten aufgeführten Werte, um das Formular auszufüllen.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Datenstromfeld | Wert |
| --- | --- |
| [!UICONTROL Sandbox] | Der Name der Experience Platform [Sandbox](/help/sandboxes/home.md) die die erforderliche Streaming-Verbindung und Datensätze zum Einrichten des Datenstroms enthält. |
| [!UICONTROL Event Dataset] | Ein [!DNL XDM ExperienceEvent] Datensatz, an den Sie Ereignisdaten mithilfe der SDK senden möchten. Sie müssen zwar einen Ereignisdatensatz bereitstellen, um einen Experience Platform-Datenstrom zu erstellen, aber beachten Sie, dass Einverständnisdaten, die über Ereignisse gesendet werden, in nachgelagerten Erzwingungs-Workflows nicht berücksichtigt werden. |
| [!UICONTROL Profile Dataset] | Der [!DNL Profile] Datensatz mit Feldern für das Kundeneinverständnis, die Sie [früher“ ](#prerequisites). |

Wenn Sie fertig sind, wählen Sie unten im Bildschirm **[!UICONTROL Save]** aus und befolgen Sie weitere Anweisungen, um die Konfiguration abzuschließen.

## Installieren und Konfigurieren der Experience Platform Web SDK

Nachdem Sie einen Datenstrom wie im vorherigen Abschnitt beschrieben erstellt haben, müssen Sie dann die Experience Platform Web SDK-Erweiterung konfigurieren, die Sie schließlich auf Ihrer Site bereitstellen. Wenn Sie die SDK-Erweiterung nicht in Ihrer Tag-Eigenschaft installiert haben, wählen Sie im linken Navigationsbereich **[!UICONTROL Extensions]** und dann die Registerkarte **[!UICONTROL Catalog]** aus. Wählen Sie dann in der Liste der verfügbaren Erweiterungen **[!UICONTROL Install]** unter der Experience Platform SDK-Erweiterung aus.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Wählen Sie beim Konfigurieren von SDK unter **[!UICONTROL Edge Configurations]** den Datenstrom aus, den Sie im vorherigen Schritt erstellt haben.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Wählen Sie **[!UICONTROL Save]** aus, um die Erweiterung zu installieren.

### Erstellen eines Datenelements zum Festlegen des Standardeinverständnisses

Wenn die SDK-Erweiterung installiert ist, haben Sie die Möglichkeit, ein Datenelement zu erstellen, das den standardmäßigen Einverständniswert für die Datenerfassung (`collect.val`) für Ihre Benutzerinnen und Benutzer darstellt. Dies kann nützlich sein, wenn Sie je nach Benutzer unterschiedliche Standardwerte verwenden möchten, z. B. `pending` für Benutzer der Europäischen Union und `in` für nordamerikanische Benutzer.

In diesem Anwendungsfall können Sie Folgendes implementieren, um das Standardeinverständnis basierend auf der Region des Benutzers festzulegen:

1. Bestimmen der Region des Benutzers auf dem Webserver
1. Rendern Sie vor dem `script`-Tag (Einbettungs-Code) auf der Web-Seite ein separates `script`-Tag, das eine `adobeDefaultConsent`-Variable basierend auf der Region des Benutzers festlegt.
1. Richten Sie ein Datenelement ein, das die `adobeDefaultConsent` JavaScript-Variable verwendet, und verwenden Sie dieses Datenelement als standardmäßigen Einverständniswert für den Benutzer.

Wenn die Region des Benutzers durch eine CMP bestimmt wird, können Sie stattdessen die folgenden Schritte verwenden:

1. Behandeln Sie das Ereignis „CMP Loaded“ auf der Seite.
1. Legen Sie im Ereignishandler eine `adobeDefaultConsent` Variable basierend auf der Region des Benutzers fest und laden Sie dann das Tag-Bibliotheksskript mit JavaScript.
1. Richten Sie ein Datenelement ein, das die `adobeDefaultConsent` JavaScript-Variable verwendet, und verwenden Sie dieses Datenelement als standardmäßigen Einverständniswert für den Benutzer.

Um ein Datenelement in der Benutzeroberfläche zu erstellen, klicken Sie im linken Navigationsbereich auf **[!UICONTROL Data Elements]** und wählen Sie dann **[!UICONTROL Add Data Element]** aus, um zum Dialogfeld für die Erstellung von Datenelementen zu navigieren.

Von hier aus müssen Sie ein [!UICONTROL JavaScript Variable] Datenelement basierend auf `adobeDefaultConsent` erstellen. Wählen Sie **[!UICONTROL Save]** aus, wenn Sie fertig sind.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Nachdem das Datenelement erstellt wurde, navigieren Sie zurück zur Konfigurationsseite der Web-SDK-Erweiterung. Wählen Sie im Abschnitt [!UICONTROL Privacy] die Option **[!UICONTROL Provided by data element]** aus und verwenden Sie das bereitgestellte Dialogfeld, um das zuvor erstellte Datenelement für das Standardeinverständnis auszuwählen.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Bereitstellen der Erweiterung auf Ihrer Website

Nachdem Sie die Konfiguration der Erweiterung abgeschlossen haben, kann sie in Ihre Website integriert werden. Ausführliche Informationen zur Bereitstellung [ aktualisierten Bibliotheks-Builds finden Sie ](/help/tags/ui/publishing/overview.md) „Veröffentlichungshandbuch“ in der Tags-Dokumentation.

## Erstellen von Befehlen zur Einverständnisänderung {#commands}

Nachdem Sie die SDK-Erweiterung in Ihre Website integriert haben, können Sie mit dem Befehl Experience Platform Web SDK `setConsent` Einverständnisdaten an Experience Platform senden.

Der Befehl `setConsent` führt zwei Aktionen aus:

1. Aktualisiert die Profilattribute des Benutzers direkt im Profilspeicher. Dadurch werden keine Daten an den Data Lake gesendet.
1. Erstellt ein [Erlebnisereignis](/help/xdm/classes/experienceevent.md) das ein mit einem Zeitstempel versehenes Konto des Einverständnisänderungsereignisses aufzeichnet. Diese Daten werden direkt an den Data Lake gesendet und können verwendet werden, um Änderungen der Einverständnispräferenzen im Laufe der Zeit zu verfolgen.

### Wann `setConsent` aufgerufen werden soll

Es gibt zwei Szenarien, in denen `setConsent` auf Ihrer Site aufgerufen werden sollten:

1. Wenn das Einverständnis auf der Seite geladen wird (d. h. bei jedem Laden der Seite)
1. Als Teil eines CMP-Hooks oder Ereignis-Listeners, der Änderungen an den Einverständniseinstellungen erkennt

### `setConsent`

Der [`setConsent`](/help/collection/js/commands/setconsent.md)-Befehl erwartet ein Payload-Objekt, das eine einzige Eigenschaft vom Typ Array enthält: `consent`. Das `consent`-Array muss mindestens ein Objekt enthalten, das die erforderlichen Einverständnisfelder für den Adobe-Standard bereitstellt.

Die erforderlichen Einverständnisfelder für den Adobe-Standard werden im folgenden Beispiel `setConsent` -Aufruf gezeigt:

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
        time: "YYYY-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| Payload-Eigenschaft | Beschreibung |
| --- | --- |
| `standard` | Der verwendete Einverständnisstandard. Für den Adobe-Standard muss dieser Wert auf `Adobe` festgelegt werden. |
| `version` | Die Versionsnummer des Einverständnisstandards, die unter `standard` angegeben ist. Dieser Wert muss für die Einverständnisverarbeitung nach Adobe-Standard auf `2.0` gesetzt werden. |
| `value` | Die aktualisierten Einverständnisinformationen des Kunden, bereitgestellt als XDM-Objekt, das der Struktur der Einverständnisfelder des profilaktivierten Datensatzes entspricht. |

>[!NOTE]
>
>Wenn Sie andere Einverständnisstandards in Verbindung mit `Adobe` verwenden (z. B. `IAB TCF`), können Sie dem `consent`-Array für jeden Standard zusätzliche Objekte hinzufügen. Jedes Objekt muss geeignete Werte für `standard`, `version` und `value` für den Einverständnisstandard enthalten, den sie repräsentieren.

Der folgende JavaScript zeigt ein Beispiel für eine Funktion, die Änderungen der Einverständnisvoreinstellungen auf einer Website verarbeitet, die als Callback in einem Ereignis-Listener oder CMP-Hook verwendet werden können:

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

  // Pass the XDM object to the Experience Platform Web SDK
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

Alle [!DNL Experience Platform SDK]-Befehle geben Zusagen zurück, die angeben, ob der Aufruf erfolgreich war oder fehlgeschlagen ist. Sie können diese Antworten dann für zusätzliche Logik verwenden, z. B. um Bestätigungsnachrichten an den Kunden anzuzeigen. Weitere Informationen finden [ unter ](/help/collection/js/commands/command-responses.md).

Nachdem Sie `setConsent` Aufrufe mit der SDK erfolgreich durchgeführt haben, können Sie mit dem Profil-Viewer in der Experience Platform-Benutzeroberfläche überprüfen, ob Daten im Profilspeicher landen. Weitere Informationen finden Sie im Abschnitt [Durchsuchen von Profilen nach ](/help/profile/ui/user-guide.md#browse-identity)).

## Nächste Schritte

In diesem Handbuch haben Sie die Experience Platform Web SDK-Erweiterung konfiguriert, um Einverständnisdaten an Experience Platform zu senden. Anleitungen zum Testen Ihrer Implementierung finden Sie in der Dokumentation zum Einverständnisstandard, den Sie implementieren:

* [Adobe Standard](./adobe/overview.md#test)
* [TCF 2.0-Standard](./iab/overview.md#test)
