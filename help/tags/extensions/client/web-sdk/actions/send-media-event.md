---
title: Medienereignis senden
description: Senden von Mediendaten an die Adobe Experience Platform Edge Network.
source-git-commit: 639d3d3d8bfb51e6c97066aee61271d0b00ec455
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Medienereignis senden

Die **[!UICONTROL Send media event]**-Aktion sendet Medienereignisse an einen Datenstrom, der dann von Apps und Services wie Adobe Experience Platform oder Adobe Analytics verwendet werden kann. Diese Aktion ist nützlich, wenn Sie Streaming-Medieninhalte in Ihrer Eigenschaft verfolgen.

![Bild der Experience Platform-Benutzeroberfläche mit dem Bildschirm „Medienereignis senden“.](../assets/send-media-event.png)

Die verfügbaren Optionen hängen von der ausgewählten **[!UICONTROL Media event type]** ab. Für alle Medienereignistypen ist ein **[!UICONTROL Player ID]** erforderlich, bei dem es sich um den Inhalts-Player-Namen handelt.

Einige Ereignistypen bieten die Möglichkeit, andere Felder zu konfigurieren. Wenn hier kein Medienereignistyp aufgeführt ist, ist nur das Feld [!UICONTROL Player ID] verfügbar. Die folgenden Medienereignistypen umfassen andere Felder:

## [!UICONTROL Ad break start]

Ermöglicht die Konfiguration von Details zu Werbeblöcken.

* **[!UICONTROL Ad break name]**: Der Anzeigename der Werbeunterbrechung.
* **[!UICONTROL Ad break offset (seconds)]**: Der Versatz der Anzeigenunterbrechung innerhalb des Inhalts in Sekunden.
* **[!UICONTROL Ad break index]**: Der Index der Anzeigenunterbrechung innerhalb des Inhalts, beginnend bei 1.

## [!UICONTROL Ad start]

Ermöglicht die Konfiguration von Werbedetails.

* **[!UICONTROL Ad name]**: Der Anzeigename der Anzeige.
* **[!UICONTROL Ad ID]**: Die ID der Anzeige. Jeder alphanumerische Wert wird unterstützt.
* **[!UICONTROL Ad length (seconds)]**: Die Länge der Videoanzeige in Sekunden.
* **[!UICONTROL Advertiser]**: Das Unternehmen oder die Marke, deren Produkt in der Anzeige zu sehen ist.
* **[!UICONTROL Campaign ID]**: Die ID der Anzeigenkampagne.
* **[!UICONTROL Creative ID]**: Die ID des Kreativinhalts der Anzeige.
* **[!UICONTROL Creative URL]**: Die URL der kreativen Anzeige.
* **[!UICONTROL Placement ID]**: Die Platzierungs-ID der Anzeige.
* **[!UICONTROL Site ID]**: Die ID der Anzeigen-Site.
* **[!UICONTROL Pod position]**: Der Index der Anzeige innerhalb der übergeordneten Anzeigenunterbrechung, beginnend bei 0.

Dieser Ereignistyp unterstützt auch die Möglichkeit, benutzerdefinierte Metadaten als Teil der Medienereignis-Payload bereitzustellen.

## [!UICONTROL Bitrate change]

* **[!UICONTROL Quality of experience data]**: Ein [Quality of Experience](/help/xdm/data-types/qoe-data-details-collection.md)-Objekt, das die Bitrate, die ausgelassenen Frames, die Frames pro Sekunde und die Startzeit angibt.

## [!UICONTROL Chapter start]

Ermöglicht die Konfiguration von Kapiteldetails.

* **[!UICONTROL Chapter name]**: Der Name des Kapitels oder Segments.
* **[!UICONTROL Chapter length]**: Die Länge des Kapitels in Sekunden.
* **[!UICONTROL Chapter index]**: Die Position des Kapitels im Inhalt.
* **[!UICONTROL Chapter offset]**: Der Versatz des Kapitels vom Beginn des Inhalts in Sekunden.

Dieser Ereignistyp unterstützt auch die Möglichkeit, benutzerdefinierte Metadaten als Teil der Medienereignis-Payload bereitzustellen.

## [!UICONTROL Error]

Ermöglicht die Konfiguration von Fehlerdetails.

* **[!UICONTROL Error name]**: Der Fehlername.
* **[!UICONTROL Source]**: Die Fehlerquelle.

## [!UICONTROL Session start]

Ermöglicht die Konfiguration von Details zur Mediensitzung.

* **[!UICONTROL Handle media session automatically]**: Ein Kontrollkästchen, mit dem Web SDK erforderliche Pings automatisch senden kann. Sie können dieses Kontrollkästchen deaktivieren, wenn Sie Pings manuell selbst senden möchten.
* **[!UICONTROL Playhead]**: Der Wiedergabekopf in Sekunden.
* **[!UICONTROL Content type]**: Der Content-Typ. Jeder Zeichenfolgenwert wird unterstützt. Adobe bietet außerdem die folgenden Voreinstellungen:
   * [!UICONTROL Audiobook]
   * [!UICONTROL Downloaded video-on-demand]
   * [!UICONTROL Linear playback of the media asset]
   * [!UICONTROL Live streaming]
   * [!UICONTROL Podcast]
   * [!UICONTROL Radio show]
   * [!UICONTROL Song]
   * [!UICONTROL User-generated content]
   * [!UICONTROL Video-on-demand]
* **[!UICONTROL Clip length/runtime (seconds)]**: Die maximale Dauer des konsumierten Inhalts in Sekunden. Bei Live-Medien mit einer unbekannten Dauer ist der Wert von `86400` der Standardwert.
* **[!UICONTROL Content ID]**: Die Inhalts-ID des Inhalts.
* **[!UICONTROL Ad load type]**: Der Typ der geladenen Anzeige. Die folgenden beiden Werte werden unterstützt:
   * [!UICONTROL Ads same as TV]
   * [!UICONTROL Other (custom/dynamic ads)]
* **[!UICONTROL Album]**: Das Album, zu dem das Lied gehört.
* **[!UICONTROL Artist]**: Der Künstler des Liedes.
* **[!UICONTROL Asset ID]**: Die eindeutige Kennung für den Inhalt des Medien-Assets. Diese IDs werden normalerweise von Metadatenbehörden wie EIDR, TMS/Gracenote oder Rovi abgeleitet. Diese Kennungen können auch von anderen proprietären oder internen Systemen stammen.
* **[!UICONTROL Author]**: Der Name des Autors des Hörbuchs.
* **[!UICONTROL Authorized]**: Ein Flag, das bestimmt, ob die Benutzerin bzw. der Benutzer über die Adobe-Authentifizierung angemeldet ist.
* **[!UICONTROL Day part]**: Die Tageszeit, zu der der Inhalt gesendet oder wiedergegeben wurde. Jeder Zeichenfolgenwert wird unterstützt.
* **[!UICONTROL Episode]**: Die Nummer der Folge.
* **[!UICONTROL Feed type]**: Die Art des Feeds.
* **[!UICONTROL First air date]**: Das Datum, an dem der Inhalt erstmals im Fernsehen ausgestrahlt wurde. Jeder Zeichenfolgenwert wird unterstützt. Adobe empfiehlt jedoch die Verwendung des `YYYY-MM-DD`.
* **[!UICONTROL First digital date]**: Das Datum, an dem der Inhalt auf einem digitalen Kanal oder einer digitalen Plattform erstmals ausgestrahlt wurde. Jeder Zeichenfolgenwert wird unterstützt. Adobe empfiehlt jedoch die Verwendung des `YYYY-MM-DD`.
* **[!UICONTROL Content name]**: Der Anzeigename des Inhalts.
* **[!UICONTROL Genre]**: Der Typ oder die Gruppierung des Inhalts, der bzw. die vom Inhaltsersteller definiert wird. Dieses Feld unterstützt mehrere Werte, die durch ein Komma getrennt sind.
* **[!UICONTROL Label]**: Der Name der Datensatzkennzeichnung.
* **[!UICONTROL Rating]**: Die Bewertung gemäß der Definition in den Richtlinien für TV Parental.
* **[!UICONTROL MVPD]**: Die MVPD, wie sie von der Adobe-Authentifizierung bereitgestellt wird.
* **[!UICONTROL Network]**: Der Netzwerk- oder Kanalname.
* **[!UICONTROL Originator]**: Der Ersteller des Inhalts.
* **[!UICONTROL Publisher]**: Der Herausgeber des Audioinhalts.
* **[!UICONTROL Season]**: Wenn die Sendung Teil einer Serie ist, die Staffelnummer der Sendung.
* **[!UICONTROL Show]**: Wenn die Sendung Teil einer Serie ist, der Serienname.
* **[!UICONTROL Show type]**: Der Sendungstyp. Jeder Zeichenfolgenwert wird unterstützt. Adobe bietet außerdem die folgenden Voreinstellungen:
   * [!UICONTROL Clip]
   * [!UICONTROL Full episode]
   * [!UICONTROL Other]
   * [!UICONTROL Preview/trailer]
* **[!UICONTROL Stream type]**: Der Stream-Typ.
* **[!UICONTROL Stream format]**: Das Format des Streams, z. B. HD oder SD.
* **[!UICONTROL Station]**: Name oder ID des Radiosenders.

Dieser Ereignistyp unterstützt auch die Möglichkeit, benutzerdefinierte Metadaten als Teil der Medienereignis-Payload bereitzustellen. Es ermöglicht auch Überschreibungen der Datenstromkonfiguration, sodass Sie steuern können, welche Apps und Services diese Daten erhalten. Wenn Sie eine Überschreibung der Datenstromkonfiguration sowohl in einem einzelnen Befehl als auch in den Konfigurationseinstellungen der Tag-Erweiterung festlegen, hat der einzelne Befehl Vorrang. Weitere [&#x200B; finden Sie unter &#x200B;](../configure/configuration-overrides.md) der Datenstromkonfiguration .

## [!UICONTROL States update]

Ermöglicht die Konfiguration von Statusaktualisierungsdetails. Sie können die folgenden Status starten oder beenden:

* [!UICONTROL Closed captioning]
* [!UICONTROL Full screen]
* [!UICONTROL In focus]
* [!UICONTROL Mute]
* [!UICONTROL Picture in picture]

Die folgenden Felder sind verfügbar:

* **[!UICONTROL States started]**: Ein Dropdown-Menü, mit dem Sie angeben können, dass ein Status gestartet wurde. Durch Auswahl der Schaltfläche **[!UICONTROL Add another state that started]** können Sie mehrere Status in derselben Aktion starten.
* **[!UICONTROL States ended]**: Ein Dropdown-Menü, mit dem Sie angeben können, dass ein Status beendet wurde. Durch Auswahl der Schaltfläche **[!UICONTROL Add another state that ended]** können Sie mehrere Status in derselben Aktion beenden.
