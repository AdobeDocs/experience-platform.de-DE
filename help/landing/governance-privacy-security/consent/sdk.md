---
title: Verarbeiten von Kundeneinwilligungsdaten mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie das Adobe Experience Platform Web SDK integrieren, um Kundeneinwilligungsdaten in Adobe Experience Platform zu verarbeiten.
role: Developer
feature: Consent, Web SDK
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: bf651967714745a0b501dcb27373379fe014c9e1
workflow-type: tm+mt
source-wordcount: '1311'
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

* [Konfigurieren eines Datenstroms](/help/datastreams/overview.md)
* [Installieren des SDK](/help/web-sdk/install/overview.md)
* [SDK für Zustimmungsbefehle konfigurieren](/help/web-sdk/commands/configure/defaultconsent.md)

Die Installationsschritte in diesem Handbuch erfordern ein grundlegendes Verständnis der Tag-Erweiterungen und deren Installation in Webanwendungen. Weiterführende Informationen finden Sie in der folgenden Dokumentation:

* [Übersicht über Tags](/help/tags/home.md)
* [Schnellstartanleitung](/help/tags/quick-start/quick-start.md)
* [Veröffentlichungsübersicht](/help/tags/ui/publishing/overview.md)

## Einrichten eines Datastreams

Damit das SDK Daten an Experience Platform senden kann, müssen Sie zunächst einen Datastream konfigurieren. Wählen Sie in der Datenerfassungs-Benutzeroberfläche oder Experience Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Datastreams]** aus.

Nachdem Sie einen neuen Datenspeicher erstellt oder einen vorhandenen zum Bearbeiten ausgewählt haben, wählen Sie die Umschalter-Schaltfläche neben **[!UICONTROL Adobe Experience Platform]** aus. Verwenden Sie anschließend die unten aufgeführten Werte, um das Formular auszufüllen.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Datenspeicherfeld | Wert |
| --- | --- |
| [!UICONTROL Sandbox] | Der Name der Platform [Sandbox](../../../sandboxes/home.md), die die erforderliche Streaming-Verbindung und Datensätze zum Einrichten des Datastreams enthält. |
| [!UICONTROL Ereignis-Datensatz] | Ein [!DNL XDM ExperienceEvent] -Datensatz, an den Sie Ereignisdaten mit dem SDK senden möchten. Sie müssen zwar einen Ereignis-Datensatz bereitstellen, um einen Platform-Datenspeicher zu erstellen, beachten Sie jedoch, dass über Ereignisse gesendete Zustimmungsdaten in nachgelagerten Durchsetzungs-Workflows nicht berücksichtigt werden. |
| [!UICONTROL Profildatensatz] | Der [!DNL Profile]-aktivierte Datensatz mit Feldern zur Kundenzustimmung, den Sie [früher](#prerequisites) erstellt haben. |

Wenn Sie fertig sind, wählen Sie am unteren Bildschirmrand **[!UICONTROL Speichern]** und fahren Sie mit den weiteren Anweisungen fort, um die Konfiguration abzuschließen.

## Installieren und Konfigurieren des Platform Web SDK

Nachdem Sie einen Datenspeicher erstellt haben, wie im vorherigen Abschnitt beschrieben, müssen Sie die Platform Web SDK-Erweiterung konfigurieren, die Sie letztendlich auf Ihrer Site bereitstellen werden. Wenn die SDK-Erweiterung nicht in Ihrer Tag-Eigenschaft installiert ist, wählen Sie im linken Navigationsbereich **[!UICONTROL Erweiterungen]** und dann die Registerkarte **[!UICONTROL Katalog]** aus. Wählen Sie dann **[!UICONTROL Installieren]** unter der Platform SDK-Erweiterung in der Liste der verfügbaren Erweiterungen aus.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Wählen Sie beim Konfigurieren des SDK unter **[!UICONTROL Edge-Konfigurationen]** den im vorherigen Schritt erstellten Datastream aus.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Wählen Sie **[!UICONTROL Speichern]** aus, um die Erweiterung zu installieren.

### Erstellen eines Datenelements zum Festlegen der Standardzustimmung

Wenn die SDK-Erweiterung installiert ist, können Sie ein Datenelement erstellen, das den standardmäßigen Datenerfassungs-Zustimmungswert (`collect.val`) für Ihre Benutzer darstellt. Dies kann nützlich sein, wenn Sie je nach Benutzer unterschiedliche Standardwerte haben möchten, z. B. `pending` für Benutzer der Europäischen Union und `in` für Benutzer in Nordamerika.

In diesem Anwendungsfall können Sie Folgendes implementieren, um die Standardzustimmung auf Grundlage der Region des Benutzers festzulegen:

1. Bestimmen Sie die Region des Benutzers auf dem Webserver.
1. Rendern Sie vor dem Tag `script` (Einbettungscode) auf der Web-Seite ein separates Tag `script` , das eine `adobeDefaultConsent` -Variable basierend auf der Region des Benutzers festlegt.
1. Richten Sie ein Datenelement ein, das die Variable &quot;`adobeDefaultConsent` JavaScript&quot;verwendet, und verwenden Sie dieses Datenelement als standardmäßigen Zustimmungswert für den Benutzer.

Wenn die Region des Benutzers durch eine CMP bestimmt wird, können Sie stattdessen die folgenden Schritte verwenden:

1. Behandeln Sie das Ereignis &quot;CMP geladen&quot;auf der Seite.
1. Legen Sie im Ereignishandler eine `adobeDefaultConsent` -Variable auf Grundlage der Region des Benutzers fest und laden Sie dann das Tag-Bibliotheksskript mithilfe von JavaScript.
1. Richten Sie ein Datenelement ein, das die Variable &quot;`adobeDefaultConsent` JavaScript&quot;verwendet, und verwenden Sie dieses Datenelement als standardmäßigen Zustimmungswert für den Benutzer.

Um ein Datenelement in der Benutzeroberfläche zu erstellen, wählen Sie im linken Navigationsbereich **[!UICONTROL Datenelemente]** aus und klicken Sie dann auf **[!UICONTROL Datenelement hinzufügen]** , um zum Dialogfeld zur Datenelementerstellung zu navigieren.

Von hier aus müssen Sie ein auf `adobeDefaultConsent` basierendes Datenelement der JavaScript-Variablen [!UICONTROL 1} erstellen. ] Wählen Sie **[!UICONTROL Speichern]**, wenn Sie fertig sind.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Nachdem das Datenelement erstellt wurde, navigieren Sie zurück zur Konfigurationsseite der Web SDK-Erweiterung . Wählen Sie im Abschnitt [!UICONTROL Datenschutz] die Option **[!UICONTROL Wird durch Datenelement bereitgestellt]** und wählen Sie im bereitgestellten Dialogfeld das zuvor erstellte standardmäßige Datenelement für die Einwilligung aus.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Bereitstellen der Erweiterung auf Ihrer Website

Nachdem Sie die Konfiguration der Erweiterung abgeschlossen haben, kann sie in Ihre Website integriert werden. Detaillierte Informationen zum Bereitstellen des aktualisierten Bibliotheks-Builds finden Sie im [Publishing-Handbuch](../../../tags/ui/publishing/overview.md) in der Tag-Dokumentation.

## Festlegen von Befehlen zur Änderung der Zustimmung {#commands}

Nachdem Sie die SDK-Erweiterung in Ihre Website integriert haben, können Sie mit der Verwendung des Befehls Platform Web SDK `setConsent` beginnen, um Zustimmungsdaten an Platform zu senden.

Der Befehl `setConsent` führt zwei Aktionen durch:

1. Aktualisiert die Profilattribute des Benutzers direkt im Profilspeicher. Dadurch werden keine Daten an den Data Lake gesendet.
1. Erstellt ein [Erlebnisereignis](../../../xdm/classes/experienceevent.md) , das ein mit Zeitstempel versehenes Konto des Zustimmungsänderungsereignisses aufzeichnet. Diese Daten werden direkt an den Data Lake gesendet und können verwendet werden, um Änderungen der Zustimmungsparameter im Laufe der Zeit zu verfolgen.

### Wann wird `setConsent` aufgerufen?

Es gibt zwei Szenarien, in denen `setConsent` auf Ihrer Site aufgerufen werden sollte:

1. Wenn die Zustimmung auf der Seite geladen wird (d. h. bei jedem Laden der Seite)
1. Als Teil eines CMP-Hooks oder Ereignis-Listeners, der Änderungen in den Zustimmungseinstellungen erkennt

### Syntax `setConsent`

Der Befehl [`setConsent`](/help/web-sdk/commands/setconsent.md) erwartet ein Payload-Objekt, das eine einzelne Eigenschaft vom Typ Array enthält: `consent`. Das Array `consent` muss mindestens ein Objekt enthalten, das die erforderlichen Einwilligungsfelder für den Adobe-Standard bereitstellt.

Die erforderlichen Einwilligungsfelder für den Adobe-Standard sind im folgenden Beispiel-Aufruf `setConsent` aufgeführt:

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
| `standard` | Der verwendete Zustimmungsstandard. Für den Adobe-Standard muss dieser Wert auf `Adobe` gesetzt werden. |
| `version` | Die Versionsnummer des Zustimmungsstandards, angegeben unter `standard`. Dieser Wert muss auf `2.0` gesetzt werden, damit die Einwilligungsverarbeitung auf dem Adobe-Standard erfolgt. |
| `value` | Die aktualisierten Zustimmungsinformationen des Kunden, die als XDM-Objekt bereitgestellt werden, das der Struktur der Einwilligungsfelder des Profilaktivierten Datensatzes entspricht. |

>[!NOTE]
>
>Wenn Sie andere Zustimmungsstandards zusammen mit `Adobe` verwenden (z. B. `IAB TCF`), können Sie dem Array `consent` für jeden Standard zusätzliche Objekte hinzufügen. Jedes Objekt muss die entsprechenden Werte für `standard`, `version` und `value` für den Zustimmungsstandard enthalten, den sie darstellen.

Im folgenden JavaScript finden Sie ein Beispiel für eine Funktion, mit der Änderungen der Zustimmungsvoreinstellungen auf einer Website verarbeitet werden, die als Callback in einem Ereignis-Listener oder CMP-Hook verwendet werden kann:

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

Alle [!DNL Platform SDK]-Befehle geben Zusagen zurück, die angeben, ob der Aufruf erfolgreich war oder fehlgeschlagen ist. Sie können diese Antworten dann für zusätzliche Logik verwenden, z. B. für die Anzeige von Bestätigungsnachrichten an den Kunden. Weitere Informationen finden Sie unter [Befehlsantworten](/help/web-sdk/commands/command-responses.md) .

Nachdem Sie mit dem SDK erfolgreich `setConsent` -Aufrufe durchgeführt haben, können Sie mit dem Profil-Viewer in der Platform-Benutzeroberfläche überprüfen, ob Daten im Profilspeicher landen. Weitere Informationen finden Sie im Abschnitt zum [Durchsuchen von Profilen nach Identität](../../../profile/ui/user-guide.md#browse-identity) .

## Nächste Schritte

In diesem Handbuch haben Sie die Platform Web SDK-Erweiterung so konfiguriert, dass Einwilligungsdaten an Experience Platform gesendet werden. Eine Anleitung zum Testen Ihrer Implementierung finden Sie in der Dokumentation zum Einverständnisstandard, den Sie implementieren:

* [Adobe-Standard](./adobe/overview.md#test)
* [TCF 2.0-Standard](./iab/overview.md#test)
