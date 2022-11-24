---
title: Adobe Media Analytics for Audio and Video-Erweiterung – Übersicht
description: Machen Sie sich mit der Tag-Erweiterung „Adobe Media Analytics for Audio and Video“ in Adobe Experience Platform vertraut.
exl-id: 426cfd08-aead-4b35-824c-45494bca2fc8
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 100%

---

# Adobe Media Analytics for Audio and Video-Erweiterung – Übersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

In dieser Dokumentation finden Sie Informationen zum Installieren, Konfigurieren und Implementieren der „Adobe Media Analytics für Audio und Video“-Erweiterung (Media Analytics-Erweiterung). Darin enthalten sind neben Beispielen und Links zu Mustern die verfügbaren Optionen bei Verwendung dieser Erweiterung zum Erstellen einer Regel.

Durch die Media Analytics (MA)-Erweiterung wird das JavaScript-Media-SDK (Media 2.x-SDK) hinzugefügt. Diese Erweiterung bietet die Funktionalität zum Hinzufügen der `MediaHeartbeat`-Tracker-Instanz zu einer Tag-Site oder einem Projekt. Für die MA-Erweiterung sind zwei weitere Erweiterungen erforderlich:

* [Analytics-Erweiterung](../analytics/overview.md)
* [Experience Cloud ID-Erweiterung](../id-service/overview.md)

>[!IMPORTANT]
>
>Für das Audio-Tracking ist die Analytics-Erweiterung Version 1.6 oder höher erforderlich.

Nachdem Sie alle drei der zuvor erwähnten Erweiterungen in Ihr Tag-Projekt eingefügt haben, haben Sie zwei Möglichkeiten, den Vorgang fortzusetzen:

* Verwenden Sie `MediaHeartbeat`-APIs aus Ihrer Web-Anwendungserweiterung
* Integrieren oder erstellen Sie eine Player-spezifische Erweiterung, die bestimmte Medienplayer-Ereignisse den APIs der `MediaHeartbeat`-Tracker-Instanz zuordnet. Diese Instanz wird über die MA-Erweiterung offengelegt.

## Installieren und Konfigurieren der MA-Erweiterung

* **Installieren:** Um die MA-Erweiterung zu installieren, öffnen Sie die Erweiterungseigenschaft, wählen Sie **[!UICONTROL Erweiterungen > Katalog]** aus, bewegen Sie den Mauszeiger über die Erweiterung **[!UICONTROL Adobe Media Analytics für Audio und Video]** und wählen Sie **[!UICONTROL Installieren]** aus.

* **Konfigurieren:** Um die MA-Erweiterung zu konfigurieren, öffnen Sie die Registerkarte [!UICONTROL Erweiterungen], bewegen Sie den Mauszeiger über die Erweiterung und klicken Sie dann auf **[!UICONTROL Konfigurieren]**:

![Konfigurieren der MA-Erweiterung](../../../images/ext-va-config.jpg)

### Konfigurationsoptionen:

| Option | Beschreibung |
| :--- | :--- |
| Tracking Server | Definiert den Server für das Tracking von Medientakten (dies ist nicht derselbe Server wie Ihr Analyse-Tracking-Server) |
| Application Version | Medienplayer-App-/Medienplayer-SDK-Version |
| Player Name | Name des verwendeten Medienplayers, z. B. „AVPlayer“, „HTML5-Player“, „Mein anwenderspezifischer Player“. |
| Kanal | Kanalnamen-Eigenschaft |
| Online Video Provider | Name der Online-Videoplattform, über die der Inhalt verteilt wird |
| Debug Logging | Aktivieren oder Deaktivieren der Protokollierung |
| Enable SSL | Aktivieren oder Deaktivieren des Sendens von Pings über HTTPS |
| Export APIs to Window Object | Aktivieren oder Deaktivieren des Exports von Media Analytics-APIs für einen globalen Umfang |
| Variable Name | Eine Variable, die Sie zum Exportieren von Media Analytics-APIs unter dem `window`-Objekt verwenden |

**Erinnerung:** Für die MA-Erweiterung sind die [Analytics](../analytics/overview.md)- und [Experience Cloud ID](../id-service/overview.md)-Erweiterungen erforderlich. Sie müssen diese Erweiterungen auch Ihrer Erweiterungseigenschaft hinzufügen und konfigurieren.

## Verwenden der MA-Erweiterung

### Verwendung auf einer Webseite/JS-App

Die MA-Erweiterung exportiert die MediaHeartbeat-APIs im globalen Fensterobjekt, indem sie die Einstellung „Exportieren von APIs in das Fensterobjekt“ auf der Seite [!UICONTROL Konfiguration] aktiviert. Die APIs werden unter dem konfigurierten Variablennamen exportiert. Wenn der Variablenname beispielsweise als `ADB` konfiguriert ist, ist der MediaHeartbeat-Zugriff über `window.ADB.MediaHeartbeat` möglich.

>[!IMPORTANT]
>
>Die MA-Erweiterung exportiert die APIs nur, wenn `window["CONFIGURED_VARIABLE_NAME"]` nicht definiert ist, und vorhandene Variablen werden nicht überschrieben.

1. **MediaHeartbeat-Instanz erstellen:** `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance`

   **Parameter:** Ein gültiges Delegationsobjekt, das diese Funktionen offenlegt.

   | Methode |  Beschreibung   |
   | :--- | :--- |
   | `getQoSObject()` | Gibt die `theMediaObject`-Instanz zurück, die aktuelle Informationen zur Servicequalität enthält. Diese Methode wird mehrmals während einer Wiedergabesitzung aufgerufen. Die Player-Implementierung muss stets die aktuellsten verfügbaren Servicequalitätsdaten zurückgeben. |
   | `getCurrentPlaybackTime()` | Gibt die aktuelle Position der Abspielleiste zurück. Bei VOD-Tracking wird der Wert in Sekunden ab Beginn des Medienelements angegeben. Beim Tracking von LIVE-Assets wird der Wert in Sekunden ab Beginn des Programms angegeben. |

   **Wert zurückgeben:** Eine Zusage, die entweder mit einer `MediaHeartbeat`-Instanz aufgelöst oder mit einer Fehlermeldung zurückgewiesen wird.

1. **Auf MediaHeartbeat-Konstanten zugreifen:** `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat`

   Dadurch werden alle Konstanten und statischen Methoden aus der [`MediaHeartbeat`](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)-Klasse bereitgestellt.

   Sie können den Beispielplayer hier abrufen: [MA Sample Player](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/2.x). Der Beispiel-Player dient als Referenz zur Verwendung der MA-Erweiterung zur Unterstützung von Media Analytics direkt über eine Webapp.

1. Erstellen Sie die MediaHeartbeat-Tracker-Instanz wie folgt:

   ```javascript
   var MediaHeartbeat = window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat;
   
   var delegate = {
       getCurrentPlaybackTime: this._getCurrentPlaybackTime.bind(this),
       getQoSObject: this._getQoSObject.bind(this),
   };
   
   var config = {
       playerName: "Custom Player",
       ovp: "Custom OVP",
       channel: "Custom Channel"
   };
   
   var self = this;
   MediaHeartbeat.getInstance(delegate, config).then(function(instance) {
       self._mediaHeartbeat = instance;
       // Do Tracking using the MediaHeartbeat instance.
   }).catch(function(err){
       // Getting MediaHeartbeat instance failed.
   });
   ```

### Verwendung in anderen Erweiterungen

Die MA-Erweiterung legt die `get-instance` und die freigegebenen `media-heartbeat`-Module für andere Erweiterungen offen. (Weitere Informationen zu freigegebenen Modulen finden Sie in der [Dokumentation zu freigegebenen Modulen](../../../extension-dev/web/shared.md).)

>[!IMPORTANT]
>
>Der Zugriff auf freigegebene Module ist nur über andere Erweiterungen möglich. Das heißt, eine Webseite/JS-App kann nicht außerhalb einer Erweiterung auf die freigegebenen Module zugreifen oder `turbine` verwenden (siehe Code-Beispiel unten).

1. **MediaHeartbeat-Instanz erstellen:** Freigegebenes `get-instance`-Modul

   **Parameter:**

   * Ein gültiges Delegatobjekt, das die folgenden Funktionen zur Verfügung stellt:

      | Methode |  Beschreibung   |
      | :--- | :--- |
      | `getQoSObject()` | Gibt die `MediaObject`-Instanz zurück, die die aktuellen Informationen zur Servicequalität enthält. Diese Methode wird mehrmals während einer Wiedergabesitzung aufgerufen. Die Player-Implementierung muss stets die aktuellsten verfügbaren Servicequalitätsdaten zurückgeben. |
      | `getCurrentPlaybackTime()` | Gibt die aktuelle Position der Abspielleiste zurück. Bei VOD-Tracking wird der Wert in Sekunden ab Beginn des Medienelements angegeben. Beim Tracking von LIVE-Assets wird der Wert in Sekunden ab Beginn des Programms angegeben. |

   * Ein optionales Konfigurationsobjekt, das die folgenden Eigenschaften zur Verfügung stellt:

      | Eigenschaft | Beschreibung | Erforderlich |
      | :--- | :--- | :--- |
      | Online-Videoanbieter | Name der Online-Videoplattform, über die der Inhalt verteilt wird. | Nein. Überschreibt den während der Erweiterungskonfiguration definierten Wert, sofern vorhanden. |
      | Player-Name | Name des verwendeten Medienplayers, z. B. „AVPlayer“, „HTML5-Player“, „Mein anwenderspezifischer Player“. | Nein. Überschreibt den während der Erweiterungskonfiguration definierten Wert, sofern vorhanden. |
      | Kanal | Kanalnamen-Eigenschaft | Nein. Überschreibt den während der Erweiterungskonfiguration definierten Wert, sofern vorhanden. |
   **Wert zurückgeben:** Eine Zusage, die entweder mit einer `MediaHeartbeat`-Instanz aufgelöst oder mit einer Fehlermeldung zurückgewiesen wird.

1. **Auf MediaHeartbeat-Konstanten zugreifen:** Freigegebenes `media-heartbeat`-Modul

   Dieses Modul legt alle Konstanten und statischen Methoden dieser Klasse offen: [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html).

1. Erstellen Sie die MediaHeartbeat-Tracker-Instanz wie folgt:

   ```javascript
   var getMediaHeartbeatInstance =
     turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   
   var MediaHeartbeat =
     turbine.getSharedModule('adobe-video-analytics', 'media-heartbeat');
     ...
   
   var delegate = {
       getCurrentPlaybackTime: this._getCurrentPlaybackTime.bind(this),
       getQoSObject: this._getQoSObject.bind(this),
   }
   
   var config = {
       playerName: "Custom Player",
       ovp: "Custom OVP",
       channel: "Custom Channel"
   }
   ...
   
   var self = this;
   getMediaHeartbeatInstance(delegate, config).then(function(instance) {
       self._mediaHeartbeat = instance;
       ...
       // Do Tracking using the MediaHeartbeat instance.
   }).catch(function(err){
       // Getting MediaHeartbeat instance failed.
   });
   
   ...
   ```

1. Verwenden Sie die Media Heartbeat-Instanz und befolgen Sie die [Medien-SDK-JS-](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/setup/setup-javascript/set-up-js-2.html?lang=de) und die [JS-API-Dokumentation](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html), um das Medien-Tracking zu implementieren.

>[!NOTE]
>
>**Testen:** Um Ihre Erweiterung zu testen, müssen Sie sie in [Platform](../../../extension-dev/submit/upload-and-test.md) hochladen, wo Sie Zugriff auf alle abhängigen Erweiterungen haben.


<!--
## Leveraging the sample HTML5 player

You can obtain the MA extension sample HTML5 player here: [HTML5 Sample Player](https://github.com/adobe/reactor-adobe-va-sample-player). The sample player acts as a reference to create video player extensions and to showcase using the MA extension to support media tracking.

### Sample player extension action types

This section describes the action types available in the Sample Player extension.

#### Open Video

The _Open Video_ action provides various configurations for creating and customizing an HTML5 player, providing a video to play and enabling/disabling Adobe Video Analytics tracking.

**Action Configuration / Player Settings:** Note the CSS Selector setting which specifics the `<div>` in the web page where the player is added. Note also that the _Enable Adobe Analytics_ checkbox is checked in the Analytics Settings pane.

![Player Extension Action Configuration](../../../images/ext-va-sp-action.png)

![Player Extension Action Configuration](../../../images/ext-va-sp-action1.png)

* [\[...\]/openVideo/openVideo.jsx](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/view/actions/openVideo/openVideo.jsx) -

  UI Code to configure the Action is defined here.

* [\[...\]/actions/openVideo.js](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/lib/actions/openVideo.js) - This file exports a function that gets executed when the Action is triggered as part of the tag rule.

  This is a code snippet from `openVideo.js` where the `openVideo` Action is executed:

  ```javascript
    function openVideo(settings) {
        let player;
        try {
            Logger.info(LOG_TAG, `Executing action with ${JSON.stringify(settings)}`);

            player = new PlayerFacade(settings);
            PlayerStore.registerPlayer(player);
            player.load(settings.media);
        } catch (ex) {
            Logger.error(LOG_TAG, `Creating player for action openVideo failed with error ${ex.message}`);

            // Cleanup from DOM.
            if (player) {
                player.destroy();
            }
        }
    }
    ...
  ```

* [\[...\]/analytics/adobeAnalyticsProvider.js](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/lib/helpers/analytics/adobeAnalyticsProvider.js) - This file implements Video Analytics tracking by using Shared Modules exposed by the VA extension.

### Sample player extension basic deployment

Once the Sample Player extension is installed, you'll need to create at least one rule to properly deploy it. The Image below shows a sample rule that opens the specified video when the core extension fires the `DOMLoaded` event.

![Player Extension Sample Rule](../../../images/ext-va-sp-rule.png)

After you have saved this rule, you will need to add it to a Library, and then build and deploy so that you can test the behavior.

-->
