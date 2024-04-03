---
title: Sammlungsdatentyp für Sitzungsdetails
description: Erfahren Sie mehr über den Datentyp "Session Details Collection Experience Data Model"(XDM).
source-git-commit: fb000d45d828c01fdb08d7555512f07ab52e1f7b
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 15%

---

# [!UICONTROL Sitzungsdetails] Sammlungsdatentyp

[!UICONTROL Sitzungsdetails] Die Sammlung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Daten im Zusammenhang mit Medienwiedergabesitzungen verfolgt. Mit Medienerfassungsfeldern werden Daten erfasst, die zur weiteren Verarbeitung an andere Adobe-Dienste gesendet werden. Dieses Schema umfasst eine breite Palette von Eigenschaften, die verwendet werden können, um Einblicke in das Benutzerverhalten und die Inhaltskonsummuster zu bieten. Verwenden Sie die [!UICONTROL Sitzungsdetails] Sammlungsdatentyp zur Erfassung der Benutzerinteraktion durch Protokollierung von Wiedergabeereignissen, Anzeigeninteraktionen, Fortschrittsmarken, Pausen und anderen Metriken.

+ + + + Wählen Sie diese Option aus, um ein Diagramm des Datentyps &quot;Session Details Collection&quot;anzuzeigen.
![Ein Diagramm des Datentyps der Sitzungsdetails-Sammlung.](../images/data-types/session-details-collection.png)
+++

>[!NOTE]
>
>Jeder Anzeigename enthält einen Link zu weiteren Informationen zu den Audio- und Videoparametern. Die verknüpften Seiten enthalten Details zu den von Adobe erfassten Videoanzeigendaten, Implementierungswerten, Netzwerkparametern, Berichten und wichtigen Aspekten.

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|----------|---------------------------------------------------------------------------------------|
| [!UICONTROL Anzeigenladetyp] | `adLoad` | Zeichenfolge | Nein | Die Art der geladenen Anzeige, wie durch die interne Darstellung jedes Kunden definiert. |
| [[!UICONTROL Album]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#album) | `album` | Zeichenfolge | Nein | Der Name des Albums, zu dem die Musikaufnahme oder das Video gehört. |
| [[!UICONTROL Künstler]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#artist) | `artist` | Zeichenfolge | Nein | Der Name des Album-Künstlers oder der Gruppe, der/die die Musikaufnahme oder das Video abspielt. |
| [[!UICONTROL Asset-ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#asset-id) | `assetID` | Zeichenfolge | Nein | Die [!UICONTROL Asset-ID] ist die eindeutige Kennung für den Inhalt des Medien-Assets, z. B. die Kennung einer Serienfolge, eines Film-Assets oder eines Live-Events. Normalerweise stammen diese IDs von Metadatensystemen wie EIDR, TMS/Gracenote oder Rovi. Diese Kennungen können auch von anderen proprietären oder internen Systemen stammen. |
| [[!UICONTROL Autor]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#author) | `author` | Zeichenfolge | Nein | Der Name des Medienautors. |
| [[!UICONTROL Broadcast Content Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-type) | `contentType` | Zeichenfolge | Ja | Die [!UICONTROL Broadcast Content Type] der Stream-Bereitstellung. Verfügbare Werte pro [!UICONTROL Streamtyp] include:<br>Audio: &quot;Song&quot;, &quot;Podcast&quot;, &quot;audiobook&quot; und &quot;Radio&quot;;<br>Video: &quot;VoD&quot;, &quot;Live&quot;, &quot;Linear&quot;, &quot;UGC&quot;und &quot;DVoD&quot;.<br>Kunden können für diesen Parameter benutzerdefinierte Werte bereitstellen. |
| [[!UICONTROL Übertragungsnetz]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#network) | `network` | Zeichenfolge | Nein | Der Netzwerk-/Kanalname. |
| [[!UICONTROL Inhaltskanal]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-channel) | `channel` | Zeichenfolge | Ja | Die [!UICONTROL Inhaltskanal] ist der Verteilungskanal, von dem aus der Inhalt wiedergegeben wurde. |
| [[!UICONTROL Inhaltsbeendigungen]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-complete) | `isCompleted` | Boolesch | Nein | [!UICONTROL Inhaltsbeendigungen] gibt an, ob ein zeitgesteuertes Medien-Asset bis zum Ende angesehen wurde. Dieses Ereignis bedeutet nicht unbedingt, dass der Betrachter das gesamte Video angesehen hat. Der Betrachter hätte vorausspringen können. |
| [!UICONTROL Netzwerk zur Inhaltsbereitstellung] | `cdn` | Zeichenfolge | Nein | Die [!UICONTROL Netzwerk zur Inhaltsbereitstellung] des wiedergegebenen Inhalts. |
| [[!UICONTROL Inhalts-ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-id) | `name` | Zeichenfolge | Ja | Die [!UICONTROL Inhalts-ID] ist eine eindeutige Kennung des Inhalts. Sie kann verwendet werden, um eine Verknüpfung mit anderen Branchen- oder CMS-IDs herzustellen. |
| [[!UICONTROL Inhaltsname]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-name-(variable)) | `friendlyName` | Zeichenfolge | Nein | Die [!UICONTROL Inhaltsname] ist der (für Menschen lesbare) Anzeigename des Inhalts. |
| [[!UICONTROL Inhalts-Player-Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-player-name) | `playerName` | Zeichenfolge | Ja | Der Name des Inhaltsplayers. |
| [[!UICONTROL Name des Erstellers]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#originator) | `originator` | Zeichenfolge | Nein | Der Name des Inhaltserstellers. |
| [[!UICONTROL Tagesteil]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#day-part) | `dayPart` | Zeichenfolge | Nein | Eine Eigenschaft, die die Tageszeit definiert, zu der der Inhalt gesendet oder wiedergegeben wurde. Dies kann dazu führen, dass Kunden jeden erforderlichen Wert festlegen |
| [[!UICONTROL Episode Number]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#episode) | `episode` | Zeichenfolge | Nein | Die Nummer der Folge. |
| [[!UICONTROL Feed-Typ]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-feed-type) | `feed` | Zeichenfolge | Nein | Der Feed-Typ, der entweder tatsächliche Feed-bezogene Daten wie EAST HD oder SD oder die Quelle des Feeds wie eine URL darstellen kann. |
| [[!UICONTROL Erstes Sendedatum]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-air-date) | `firstAirDate` | Zeichenfolge | Nein | Das Datum der Erstausstrahlung des Inhalts im Fernsehen. Jedes Datumsformat ist akzeptabel, Adobe empfiehlt jedoch: JJJJ-MM-TT. |
| [[!UICONTROL Erstes digitales Datum]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-digital-date) | `firstDigitalDate` | Zeichenfolge | Nein | Das Datum der Erstausstrahlung des Inhalts auf einem digitalen Kanal oder einer digitalen Plattform. Jedes Datumsformat ist akzeptabel, Adobe empfiehlt jedoch: JJJJ-MM-TT. |
| [[!UICONTROL Genre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#genre) | `genre` | Zeichenfolge | Nein | Der Typ oder die Gruppierung des Inhalts entsprechend der Definition des Inhaltserstellers. Werte sollten bei der Variablenimplementierung durch Kommas getrennt sein. |
| [[!UICONTROL Medien autorisiert]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#authorized) | `authorized` | Zeichenfolge | Nein | Bestätigt, ob der Benutzer über Adobe-Authentifizierung autorisiert wurde. |
| [[!UICONTROL Länge des Medieninhalts]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-length-(variable)) | `length` | Ganzzahl | Ja | Die [!UICONTROL Länge des Medieninhalts] enthält die Cliplänge/-laufzeit - Dies ist die maximale Länge (oder Dauer) des konsumierten Inhalts (in Sekunden). |
| [[!UICONTROL Medienstarts]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-starts) | `isViewed` | Boolesch | Nein | Das Ladeereignis für das Medium. Dies tritt auf, wenn der Viewer die Wiedergabeschaltfläche auswählt. Dies zählt auch, wenn Pre-Roll-Anzeigen, Pufferung, Fehler usw. vorhanden sind. |
| [[!UICONTROL MVPD-Kennung]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#mvpd) | `mvpd` | Zeichenfolge | Nein | Die MVPD-Kennung (Multi-Channel Video Programming Distributor), die über Adobe-Authentifizierung bereitgestellt wurde. |
| [[!UICONTROL Herausgeber]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#publisher) | `publisher` | Zeichenfolge | Nein | Der Name des Herausgebers des Audioinhalts. |
| [[!UICONTROL Funkstation]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#station) | `station` | Zeichenfolge | Nein | Der Name des Radiosenders, auf dem das Audio abgespielt wird. |
| [[!UICONTROL Bewertungswert]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-rating) | `rating` | Zeichenfolge | Nein | Die von TV Parental Guidelines definierte Bewertung. |
| [[!UICONTROL Record Label]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#label) | `label` | Zeichenfolge | Nein | Der Name der Datensatzbeschriftung. |
| [[!UICONTROL Fortsetzen]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-resumes) | `hasResume` | Boolesch | Nein | Markiert jede Wiedergabe, die nach mehr als 30 Minuten Puffer-, Pause- oder Anhaltezeit wieder aufgenommen wurde. |
| [[!UICONTROL Staffelnummer]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#season) | `season` | Zeichenfolge | Nein | Die [!UICONTROL Staffelnummer] , zu dem die Sendung gehört. Die Staffelserie ist nur erforderlich, wenn die Sendung Teil einer Serie ist. |
| [[!UICONTROL Serienname]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show) | `show` | Zeichenfolge | Nein | Der Name des Programms/der Serie. Der Programmname ist nur erforderlich, wenn die Sendung Teil einer Serie ist. |
| [[!UICONTROL Sendungstyp]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show-type) | `showType` | Zeichenfolge | Nein | Der Inhaltstyp. Beispiel: ein Trailer oder eine vollständige Folge. Der Inhaltstyp wird als Ganzzahl zwischen 0 und 3 angegeben. Beispiel: &quot;0&quot;= vollständige Folge; &quot;1&quot;= Vorschau/Trailer; &quot;2&quot;= Clip; &quot;3&quot;= Sonstige. |
| [[!UICONTROL Stream-Format]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-format) | `streamFormat` | Zeichenfolge | Nein | Das Format des Streams (HD, SD). |
| [[!UICONTROL Streamtyp]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-type) | `streamType` | Zeichenfolge | Nein | Der Typ des Medien-Streams. |
| [[!UICONTROL Version]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#sdk-version) | `appVersion` | Zeichenfolge | Nein | Die vom Player verwendete SDK-Version. Dies kann einen beliebigen benutzerdefinierten Wert haben, der für Ihren Player sinnvoll ist. |

{style="table-layout:auto"}

<!-- This is required for sessionStart. 
Q) How do I indicate that?
Q) Do you know where to link for:
Ad Load Type
Content Delivery Network
 -->
