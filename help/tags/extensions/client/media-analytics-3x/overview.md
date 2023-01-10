---
title: Adobe Media Analytics (3.x SDK) for Audio and Video-Erweiterung  Übersicht
description: Machen Sie sich mit der Tag-Erweiterung „Adobe Media Analytics (3.x SDK) for Audio and Video“ in Adobe Experience Platform vertraut.
exl-id: 7289d57d-7e7f-4832-9469-3b5a62183a32
source-git-commit: e21ed1e9fd0c2678551cfc664b611076c198a157
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 98%

---

# Adobe Media Analytics (3.x SDK) for Audio and Video-Erweiterung – Übersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

In dieser Dokumentation finden Sie Informationen zum Installieren, Konfigurieren und Implementieren der „Adobe Media Analytics (3.x SDK) for Audio and Video“-Erweiterung (Media Analytics-Erweiterung). Darin enthalten sind neben Beispielen und Links zu Mustern die verfügbaren Optionen bei Verwendung dieser Erweiterung zum Erstellen einer Regel.

Durch die Media Analytics (MA)-Erweiterung wird das JavaScript-Media-SDK (Media 3.x-SDK) hinzugefügt. Diese Erweiterung bietet die Funktionalität zum Hinzufügen der `Media`-Tracker-Instanz zu einer Site oder einem Projekt mit Tag-Aktivierung. Für die MA-Erweiterung sind zwei weitere Erweiterungen erforderlich:

* [Analytics-Erweiterung](../analytics/overview.md)
* [Experience Cloud ID-Erweiterung](../id-service/overview.md)

>[!IMPORTANT]
>
>Diese Erweiterung wird mit dem Media 3.x SDK bereitgestellt, das nicht abwärtskompatibel mit dem Media 2.x SDK ist. Da 2.x veraltet ist, aktualisieren Sie bitte auf 3.x.

Nachdem Sie alle drei der zuvor erwähnten Erweiterungen in Ihr Projekt mit Tag-Aktivierung eingefügt haben, haben Sie zwei Möglichkeiten, den Vorgang fortzusetzen:

* Verwenden Sie `Media`-APIs aus Ihrer Web-Anwendungserweiterung
* Integrieren oder erstellen Sie eine Player-spezifische Erweiterung, die bestimmte Medienplayer-Ereignisse den APIs der `Media`-Tracker-Instanz zuordnet. Diese Instanz wird über die MA-Erweiterung offengelegt.

## Installieren und Konfigurieren der MA-Erweiterung

* **Installieren:** Um die MA-Erweiterung zu installieren, öffnen Sie die Erweiterungseigenschaft, wählen Sie **[!UICONTROL Erweiterungen > Katalog]** aus, bewegen Sie den Mauszeiger über die Erweiterung **[!UICONTROL Adobe Medien Analytics (3.x SDK) für Audio und Video]** und wählen Sie **[!UICONTROL Installieren]** aus.

* **Konfigurieren:** Um die MA-Erweiterung zu konfigurieren, öffnen Sie die Registerkarte [!UICONTROL Erweiterungen], bewegen Sie den Mauszeiger über die Erweiterung und klicken Sie dann auf **[!UICONTROL Konfigurieren]**:

![Konfigurieren der MA-Erweiterung](../../../images/ext-ma-config.png)

### Konfigurationsoptionen:

| Option | Beschreibung |
| :--- | :--- |
| Collection API Server | Definiert den Media Collection-API-Server (wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um diesen Server zu erhalten) |
| Application Version | Medienplayer-App-/Medienplayer-SDK-Version |
| Player Name | Name des verwendeten Medienplayers, z. B. „AVPlayer“, „HTML5-Player“, „Mein anwenderspezifischer Player“. |
| Kanal | Kanalnamen-Eigenschaft |
| Debug Logging | Aktivieren oder Deaktivieren der Protokollierung |
| Enable SSL | Aktivieren oder Deaktivieren des Sendens von Pings über HTTPS |
| Export APIs to Window Object | Aktivieren oder Deaktivieren des Exports von Media Analytics-APIs für einen globalen Umfang |
| Variable Name | Eine Variable, die Sie zum Exportieren von Media Analytics-APIs unter dem `window`-Objekt verwenden |

**Erinnerung:** Für die MA-Erweiterung sind die [Analytics](../analytics/overview.md)- und [Experience Cloud ID](../id-service/overview.md)-Erweiterungen erforderlich. Sie müssen diese Erweiterungen auch Ihrer Erweiterungseigenschaft hinzufügen und konfigurieren.

## Verwenden der MA-Erweiterung

### Verwendung auf einer Webseite/JS-App

Die MA-Erweiterung exportiert die Media-APIs im globalen Fensterobjekt, indem sie die Einstellung „Export APIs to Window Object“ auf der Seite [!UICONTROL Konfiguration] aktiviert. Die APIs werden unter dem konfigurierten Variablennamen exportiert. Wenn der Variablenname beispielsweise als `ADB` konfiguriert ist, ist der Media-API-Zugriff über `window.ADB.Media` möglich.

>[!IMPORTANT]
>
>Die MA-Erweiterung exportiert die APIs nur, wenn `window["CONFIGURED_VARIABLE_NAME"]` nicht definiert ist, und vorhandene Variablen werden nicht überschrieben.

1. **Media-APIs:** `window["CONFIGURED_VARIABLE_NAME"].Media`

   Dadurch werden alle APIs und Konstanten aus dem Media-SDK verfügbar gemacht: [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. **Media-Tracker-Instanz erstellen:** `window["CONFIGURED_VARIABLE_NAME"].Media.getInstance`

   **Rückgabewert:** Eine `Media`-Tracker-Instanz zur Verfolgung einer Mediensitzung.

   ```javascript
   var Media = window["CONFIGURED_VARIABLE_NAME"].Media;
   
   var tracker = Media.getInstance();
   ```

1. Verwenden Sie die Media-Tracker-Instanz und befolgen Sie die [JS-API-Dokumentation](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html), um die Medienverfolgung zu implementieren.

Sie können den Beispielplayer hier abrufen: [MA Sample Player](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x). Der Beispiel-Player dient als Referenz zur Verwendung der MA-Erweiterung zur Unterstützung von Media Analytics direkt über eine Webapp.


### Verwendung in anderen Erweiterungen

Die MA-Erweiterung stellt `media` als freigegebenes Modul anderen Erweiterungen zur Verfügung. (Weitere Informationen zu freigegebenen Modulen finden Sie in der [Dokumentation zu freigegebenen Modulen](../../../extension-dev/web/shared.md).)

>[!IMPORTANT]
>
>Der Zugriff auf freigegebene Module ist nur über andere Erweiterungen möglich. Das heißt, eine Website/JavaScript-App kann nicht außerhalb einer Erweiterung auf die freigegebenen Module zugreifen oder `turbine` verwenden (siehe Code-Beispiel unten).

1. **Media-APIs:** `media` Freigegebenes Modul

   Dadurch werden alle APIs und Konstanten aus dem Media SDK verfügbar gemacht: [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. Erstellen Sie die Media-Tracker-Instanz wie folgt:

   **Rückgabewert:** Eine `Media`-Tracker-Instanz zur Verfolgung einer Mediensitzung.

   ```javascript
   var Media =
     turbine.getSharedModule('adobe-media-analytics', 'media');
   
   var tracker = Media.getInstance();
   ```

1. Verwenden Sie die Media-Tracker-Instanz und befolgen Sie die [JS-API-Dokumentation](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html), um die Medienverfolgung zu implementieren.

>[!NOTE]
>
>**Testen:** Um Ihre Erweiterung zu testen, müssen Sie sie in [Platform](../../../extension-dev/submit/upload-and-test.md) hochladen, wo Sie Zugriff auf alle abhängigen Erweiterungen haben.
