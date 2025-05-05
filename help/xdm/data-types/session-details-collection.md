---
title: Datentyp der Datenerfassung für Sitzungsdetails
description: Erfahren Sie mehr über den Datentyp „Session Details Collection Experience Data Model (XDM)“.
exl-id: ffe6bcf7-61e1-4f7a-ba95-7fcb78683cc9
source-git-commit: 9350cfc299c20bd63a2a559c177b3af02739e5b9
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 16%

---

# [!UICONTROL Sitzungsdetails] Datentyp „Sammlung“

[!UICONTROL Sitzungsdetails]-Sammlung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Daten verfolgt, die sich auf Medienwiedergabesitzungen beziehen. Mediensammlungsfelder werden verwendet, um Daten zu erfassen, die zur weiteren Verarbeitung an andere Adobe-Services gesendet werden. Dieses Schema umfasst eine breite Palette von Eigenschaften, die verwendet werden können, um Einblicke in das Benutzerverhalten und die Verbrauchsmuster von Inhalten zu bieten. Verwenden Sie den [!UICONTROL Sitzungsdetails] Datentyp „Sammlung“, um Benutzerinteraktionen zu erfassen, indem Wiedergabeereignisse, Anzeigeninteraktionen, Fortschrittsmarken, Pausen und andere Metriken protokolliert werden.

+++Wählen Sie diese Option aus, um ein Diagramm des Datentyps „Session Details Collection“ anzuzeigen.
![Ein Diagramm zum Datentyp „Session Details Collection“.](../images/data-types/session-details-collection.png)
+++

>[!NOTE]
>
>Jeder Anzeigename enthält einen Link zu weiteren Informationen zu den Audio- und Videoparametern. Die verknüpften Seiten enthalten Details zu den von Adobe erfassten Video-Anzeigendaten, Implementierungswerten, Netzwerkparametern, Berichten und wichtigen Überlegungen.

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|----------|---------------------------------------------------------------------------------------|
| [!UICONTROL Anzeigenladetyp] | `adLoad` | Zeichenfolge | Nein | Die Art der geladenen Anzeige, wie durch die interne Darstellung jedes Kunden definiert. |
| [[!UICONTROL Album]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#album) | `album` | Zeichenfolge | Nein | Der Name des Albums, zu dem die Musikaufnahme oder das Video gehört. |
| [[!UICONTROL Künstler]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#artist) | `artist` | Zeichenfolge | Nein | Der Name des Interpreten oder der Gruppe, die die Musikaufnahme oder das Video aufführt. |
| [[!UICONTROL Asset-ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#asset-id) | `assetID` | Zeichenfolge | Nein | Die [!UICONTROL Asset-ID] ist die eindeutige Kennung für den Inhalt des Medien-Assets, z. B. die Kennung der TV-Serienepisode, die Kennung des Film-Assets oder die Kennung des Live-Ereignisses. Diese IDs werden in der Regel von Metadatenbehörden wie EIDR, TMS/Gracenote oder Rovi abgeleitet. Diese Kennungen können auch von anderen proprietären oder internen Systemen stammen. |
| [[!UICONTROL author]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#author) | `author` | Zeichenfolge | Nein | Der Name des Medienautors. |
| [[!UICONTROL Typ des ausgestrahlten &#x200B;]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-type) | `contentType` | Zeichenfolge | Ja | Der [!UICONTROL Typ des gesendeten &#x200B;]) der Stream-Bereitstellung. Verfügbare Werte pro [!UICONTROL Stream-]: <br>Audio: „Song“, „Podcast“, „Hörbuch“ und „Radio“; <br>Video: „VoD“, „Live“, „Linear“, „UGC“ und „DVoD“.<br>Kunden können benutzerdefinierte Werte für diesen Parameter angeben. |
| [[!UICONTROL Broadcast-Netzwerk]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#network) | `network` | Zeichenfolge | Nein | Der Netzwerk-/Kanalname. |
| [[!UICONTROL Inhaltskanal]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-channel) | `channel` | Zeichenfolge | Ja | Der [!UICONTROL Inhaltskanal] ist der Verteilungskanal, von dem aus der Inhalt wiedergegeben wurde. |
| [!UICONTROL Content Delivery Network] | `cdn` | Zeichenfolge | Nein | Das [!UICONTROL Content Delivery Network] des wiedergegebenen Inhalts. |
| [[!UICONTROL Inhalts-ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-id) | `name` | Zeichenfolge | Ja | Die [!UICONTROL Inhalts-ID] ist eine eindeutige Kennung des Inhalts. Sie kann verwendet werden, um eine Verknüpfung zu anderen Branchen- oder CMS-IDs herzustellen. |
| [[!UICONTROL Inhaltsname]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-name-(variable)) | `friendlyName` | Zeichenfolge | Nein | Der [!UICONTROL Inhaltsname] ist der „benutzerfreundliche“ (menschenlesbare) Name des Inhalts. |
| [[!UICONTROL Name des Inhalts-Players]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-player-name) | `playerName` | Zeichenfolge | Ja | Der Name des Content-Players. |
| [[!UICONTROL Name des Erstellers]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#originator) | `originator` | Zeichenfolge | Nein | Der Name des Inhaltserstellers. |
| [[!UICONTROL Day Part]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#day-part) | `dayPart` | Zeichenfolge | Nein | Eine Eigenschaft, die die Tageszeit definiert, zu der der Inhalt gesendet oder wiedergegeben wurde. Für diesen Wert können Kunden bei Bedarf einen Wert festlegen |
| [[!UICONTROL Folge-Nummer]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#episode) | `episode` | Zeichenfolge | Nein | Die Nummer der Folge. |
| [[!UICONTROL Feed-Typ]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-feed-type) | `feed` | Zeichenfolge | Nein | Die Art des Feeds, die entweder tatsächliche Feed-bezogene Daten wie EAST HD oder SD oder die Quelle des Feeds wie eine URL darstellen kann. |
| [[!UICONTROL Datum der Erstausstrahlung]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-air-date) | `firstAirDate` | Zeichenfolge | Nein | Das Datum, an dem der Inhalt erstmals im Fernsehen ausgestrahlt wurde. Jedes Datumsformat ist akzeptabel, aber Adobe empfiehlt: JJJJ-MM-TT. |
| [[!UICONTROL Erstes digitales Datum]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-digital-date) | `firstDigitalDate` | Zeichenfolge | Nein | Das Datum, an dem der Inhalt auf einem digitalen Kanal oder einer digitalen Plattform erstmals ausgestrahlt wurde. Jedes Datumsformat ist akzeptabel, aber Adobe empfiehlt: JJJJ-MM-TT. |
| [[!UICONTROL Genre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#genre) | `genre` | Zeichenfolge | Nein | Der Typ oder die Gruppierung des Inhalts, wie vom Inhaltsersteller definiert. Werte sollten in der Variablenimplementierung durch Kommas getrennt sein. |
| [[!UICONTROL Medien autorisiert]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#authorized) | `authorized` | Zeichenfolge | Nein | Bestätigt, ob der Benutzer über die Adobe-Authentifizierung autorisiert wurde. |
| [[!UICONTROL Länge des Medieninhalts]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-length-(variable)) | `length` | Ganzzahl | Ja | Die [!UICONTROL Medieninhaltslänge] enthält die Clip-Länge/Laufzeit - Dies ist die maximale Länge (oder Dauer) des konsumierten Inhalts (in Sekunden). |
| [[!UICONTROL MVPD-Kennung]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#mvpd) | `mvpd` | Zeichenfolge | Nein | Die Kennung des Multi-Channel Video Programming Distributor (MVPD), die über die Adobe-Authentifizierung bereitgestellt wurde. |
| [[!UICONTROL publisher]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#publisher) | `publisher` | Zeichenfolge | Nein | Der Name des Herausgebers des Audioinhalts. |
| [[!UICONTROL Radiosender]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#station) | `station` | Zeichenfolge | Nein | Der Name des Radiosenders, auf dem das Audio wiedergegeben wird. |
| [[!UICONTROL Wert der Bewertung]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-rating) | `rating` | Zeichenfolge | Nein | Die Bewertung gemäß der Definition in den Richtlinien für TV Parental. |
| [[!UICONTROL Plattenlabel]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#label) | `label` | Zeichenfolge | Nein | Der Name der Datensatzkennzeichnung. |
| [[!UICONTROL Fortsetzen]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-resumes) | `hasResume` | Boolesch | Nein | Markiert jede Wiedergabe, die nach mehr als 30 Minuten Puffer-, Pause- oder Anhaltezeit wieder aufgenommen wurde. |
| [[!UICONTROL Staffelnummer]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#season) | `season` | Zeichenfolge | Nein | Die [!UICONTROL Staffelnummer] zu der die Sendung gehört. Staffel Serie ist nur erforderlich, wenn die Sendung Teil einer Serie ist. |
| [[!UICONTROL Serienname]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show) | `show` | Zeichenfolge | Nein | Der Name des Programms/der Serie. Der Programmname ist nur erforderlich, wenn die Sendung Teil einer Serie ist. |
| [[!UICONTROL Sendungstyp]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show-type) | `showType` | Zeichenfolge | Nein | Der Inhaltstyp. Beispiel: ein Trailer oder eine vollständige Folge. Der Inhaltstyp wird als Ganzzahl zwischen 0 und 3 ausgedrückt. Beispiel: „0“ = Vollständige Folge; „1“ = Vorschau/Trailer; „2“ = Clip; „3“ = Sonstige. |
| [[!UICONTROL Stream-Format]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-format) | `streamFormat` | Zeichenfolge | Nein | Das Format des Streams (HD, SD). |
| [[!UICONTROL Stream-Typ]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-type) | `streamType` | Zeichenfolge | Nein | Der Typ des Medien-Streams. |
| [[!UICONTROL version]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#sdk-version) | `appVersion` | Zeichenfolge | Nein | Die vom Player verwendete SDK-Version. Dies kann einen beliebigen benutzerdefinierten Wert enthalten, der für Ihren Player sinnvoll ist. |

{style="table-layout:auto"}
