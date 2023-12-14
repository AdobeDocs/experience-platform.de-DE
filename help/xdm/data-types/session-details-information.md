---
title: Datentyp "Sitzungsdetails"
description: Erfahren Sie mehr über den Datentyp "Sitzungsdetails-Informationen - Experience-Datenmodell (XDM)".
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 20%

---

# [!UICONTROL Sitzungsdetails - Informationen] Datentyp

[!UICONTROL Sitzungsdetails - Informationen] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Daten im Zusammenhang mit Medienwiedergabesitzungen verfolgt. Das Schema umfasst eine breite Palette von Eigenschaften, die Einblicke in die Verwendung von Medieninhalten bieten. Verwenden Sie die [!UICONTROL Sitzungsdetails - Informationen] Datentyp zum Erfassen der Benutzerinteraktion durch Protokollierung von Wiedergabeereignissen, Anzeigeninteraktionen, Fortschrittsmarken, Pausen und anderen Metriken. Dies bietet wertvolle Einblicke in das Benutzerverhalten und die Konsummuster von Inhalten.

+++Auswählen , um ein Diagramm des Datentyps Sitzungsdetails anzuzeigen.
![Ein Diagramm des Datentyps Sitzungsdetails .](../images/data-types/session-details-information.png)
+++

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Mediensitzungs-ID] | `ID` | Zeichenfolge | Die [!UICONTROL Mediensitzungs-ID] identifiziert eine Instanz eines Inhalts-Streams, die für eine einzelne Wiedergabe eindeutig ist. |
| [!UICONTROL Inhalts-ID] | `name` | Zeichenfolge | **Erforderlich** Die [!UICONTROL Inhalts-ID] ist eine eindeutige Kennung des Inhalts. Sie kann verwendet werden, um eine Verknüpfung mit anderen Branchen- oder CMS-IDs herzustellen. |
| [!UICONTROL Inhaltsname] | `friendlyName` | Zeichenfolge | Die [!UICONTROL Inhaltsname] ist der (für Menschen lesbare) Anzeigename des Inhalts. |
| [!UICONTROL Länge des Medieninhalts] | `length` | Ganzzahl | **Erforderlich** Die [!UICONTROL Länge des Medieninhalts] enthält die Cliplänge/-laufzeit - Dies ist die maximale Länge (oder Dauer) des konsumierten Inhalts (in Sekunden). |
| [!UICONTROL Broadcast Content Type] | `contentType` | Zeichenfolge | **Erforderlich** Die [!UICONTROL Broadcast Content Type] der Stream-Bereitstellung. Verfügbare Werte pro [!UICONTROL Streamtyp] include:<br>Audio: &quot;Song&quot;, &quot;Podcast&quot;, &quot;audiobook&quot; und &quot;Radio&quot;;<br>Video: &quot;VoD&quot;, &quot;Live&quot;, &quot;Linear&quot;, &quot;UGC&quot;und &quot;DVoD&quot;.<br>Kunden können für diesen Parameter benutzerdefinierte Werte bereitstellen. |
| [!UICONTROL Inhalts-Player-Name] | `playerName` | Zeichenfolge | **Erforderlich** Der Name des Inhaltsplayers. |
| [!UICONTROL Inhaltskanal] | `channel` | Zeichenfolge | **Erforderlich** Die [!UICONTROL Inhaltskanal] ist der Verteilungskanal, von dem aus der Inhalt wiedergegeben wurde. |
| [!UICONTROL Version] | `appVersion` | Zeichenfolge | Die vom Player verwendete SDK-Version. Dies kann einen beliebigen benutzerdefinierten Wert haben, der für Ihren Player sinnvoll ist. |
| [!UICONTROL Serienname] | `show` | Zeichenfolge | Der Name des Programms/der Serie. Der Programmname ist nur erforderlich, wenn die Sendung Teil einer Serie ist. |
| [!UICONTROL Staffelnummer] | `season` | Zeichenfolge | Die [!UICONTROL Staffelnummer] , zu dem die Sendung gehört. Die Staffelserie ist nur erforderlich, wenn die Sendung Teil einer Serie ist. |
| [!UICONTROL Episode Number] | `episode` | Zeichenfolge | Die Nummer der Folge. |
| [!UICONTROL Asset-ID] | `assetID` | Zeichenfolge | Die [!UICONTROL Asset-ID] ist die eindeutige Kennung für den Inhalt des Medien-Assets, z. B. die Kennung einer Serienfolge, eines Film-Assets oder eines Live-Events. Normalerweise stammen diese IDs von Metadatensystemen wie EIDR, TMS/Gracenote oder Rovi. Diese Kennungen können auch von anderen proprietären oder internen Systemen stammen. |
| [!UICONTROL Genre] | `genre` | Zeichenfolge | Der Typ oder die Gruppierung des Inhalts entsprechend der Definition des Inhaltserstellers. Werte sollten bei der Variablenimplementierung durch Kommas getrennt sein. |
| [!UICONTROL Erstes Sendedatum] | `firstAirDate` | Zeichenfolge | Das Datum der Erstausstrahlung des Inhalts im Fernsehen. Jedes Datumsformat ist akzeptabel, Adobe empfiehlt jedoch: JJJJ-MM-TT. |
| [!UICONTROL Erstes digitales Datum] | `firstDigitalDate` | Zeichenfolge | Das Datum der Erstausstrahlung des Inhalts auf einem digitalen Kanal oder einer digitalen Plattform. Jedes Datumsformat ist akzeptabel, Adobe empfiehlt jedoch: JJJJ-MM-TT. |
| [!UICONTROL Bewertungswert] | `rating` | Zeichenfolge | Die von TV Parental Guidelines definierte Bewertung. |
| [!UICONTROL  Name des Erstellers] | `originator` | Zeichenfolge | Der Name des Inhaltserstellers. |
| [!UICONTROL Übertragungsnetz] | `network` | Zeichenfolge | Der Netzwerk-/Kanalname. |
| [!UICONTROL Sendungstyp] | `showType` | Zeichenfolge | Der Inhaltstyp, z. B. Trailer oder vollständige Folge. |
| [!UICONTROL Anzeigenladetyp] | `adLoad` | Zeichenfolge | Die Art der geladenen Anzeige, wie durch die interne Darstellung jedes Kunden definiert. |
| [!UICONTROL MVPD-Kennung] | `mvpd` | Zeichenfolge | Die [!UICONTROL MVPD-Kennung] die über Adobe-Authentifizierung bereitgestellt wurde. |
| [!UICONTROL Medien autorisiert] | `authorized` | Zeichenfolge | Bestätigt, ob der Benutzer über Adobe-Authentifizierung autorisiert wurde. |
| [!UICONTROL Tagesteil] | `dayPart` | Zeichenfolge | Eine Eigenschaft, die die Tageszeit definiert, zu der der Inhalt gesendet oder wiedergegeben wurde. Dies kann dazu führen, dass Kunden jeden erforderlichen Wert festlegen |
| [!UICONTROL Feed-Typ] | `feed` | Zeichenfolge | Der Feed-Typ, der entweder tatsächliche Feed-bezogene Daten wie EAST HD oder SD oder die Quelle des Feeds wie eine URL darstellen kann. |
| [!UICONTROL Stream-Format] | `streamFormat` | Zeichenfolge | Das Format des Streams (HD, SD). |
| [!UICONTROL Fortsetzen] | `hasResume` | Boolesch | Markiert jede Wiedergabe, die nach mehr als 30 Minuten Puffer-, Pause- oder Anhaltezeit wieder aufgenommen wurde. |
| [!UICONTROL Streamtyp] | `streamType` | Zeichenfolge | Der Typ des Medien-Streams. |
| [!UICONTROL Künstler] | `artist` | Zeichenfolge | Der Name des Album-Künstlers oder der Gruppe, der/die die Musikaufnahme oder das Video abspielt. |
| [!UICONTROL Album] | `album` | Zeichenfolge | Der Name des Albums, zu dem die Musikaufnahme oder das Video gehört. |
| [!UICONTROL Record Label] | `label` | Zeichenfolge | Der Name der Datensatzbeschriftung. |
| [!UICONTROL Autor] | `author` | Zeichenfolge | Der Name des Medienautors. |
| [!UICONTROL Funkstation] | `station` | Zeichenfolge | Der Name des Radiosenders, auf dem das Audio abgespielt wird. |
| [!UICONTROL Veröffentlicher] | `publisher` | Zeichenfolge | Der Name des Herausgebers des Audioinhalts. |
| [!UICONTROL Videosegment] | `segment` | Zeichenfolge | Das Intervall, das den Teil des Inhalts beschreibt, der in Minuten angezeigt wurde. |
| [!UICONTROL Flag &quot;Medien heruntergeladen&quot;] | `isDownloaded` | Boolesch | Der Stream wurde nach dem Herunterladen lokal auf dem Gerät wiedergegeben. |
| [!UICONTROL Federated Data] | `isFederated` | Boolesch | [!UICONTROL Federated Data] auf &quot;true&quot;gesetzt ist, wenn der Treffer verknüpft ist (d. h. vom Kunden als Teil einer verknüpften Datenfreigabe empfangen wird und nicht als eigene Implementierung). |
| [!UICONTROL Medienstarts] | `isViewed` | Boolesch | Das Ladeereignis für das Medium. Dies tritt auf, wenn der Viewer die Wiedergabeschaltfläche auswählt. Dies zählt auch, wenn Pre-Roll-Anzeigen, Pufferung, Fehler usw. vorhanden sind. |
| [!UICONTROL Inhaltsstarts] | `isPlayed` | Boolesch | [!UICONTROL Inhaltsstarts] wird &quot;true&quot;(wahr), wenn der erste Frame des Mediums verwendet wird. Wenn der Benutzer während einer Anzeige, einer Pufferung usw. abbricht, gibt es keine [!UICONTROL Inhaltsstarts] -Ereignis. |
| [!UICONTROL Inhaltsbeendigungen] | `isCompleted` | Boolesch | [!UICONTROL Inhaltsbeendigungen] gibt an, ob ein zeitgesteuertes Medien-Asset bis zum Ende angesehen wurde. Dieses Ereignis bedeutet nicht unbedingt, dass der Betrachter das gesamte Video angesehen hat. Der Betrachter hätte vorausspringen können. |
| [!UICONTROL Besuchszeit für Inhalt] | `timePlayed` | Ganzzahl | [!UICONTROL Besuchszeit für Inhalt] summiert die Ereignisdauer (in Sekunden) für alle Ereignisse des Typs &quot;PLAY&quot;im Hauptinhalt. |
| [!UICONTROL Besuchszeit für Medien] | `totalTimePlayed` | Ganzzahl | Beschreibt die Gesamtzeit, die ein Benutzer mit einem bestimmten zeitgesteuerten Media-Asset verbringt, einschließlich der Zeit, die er mit dem Ansehen von Anzeigen verbringt. |
| [!UICONTROL Eindeutige Wiedergabedauer] | `uniqueTimePlayed` | Ganzzahl | Beschreibt die Summe der eindeutigen Intervalle, die ein Benutzer für ein zeitgesteuertes Medien-Asset sieht - d. h., die mehrmals angezeigten Zeitabspielintervalle für die Längenwiedergabe werden nur einmal gezählt. |
| [!UICONTROL Zielgruppendurchschnitt pro Minute] | `averageMinuteAudience` | Zahl | Beschreibt die durchschnittliche Besuchszeit für einen bestimmten Medienelement, d. h. die insgesamt aufgewendete Inhaltsdauer dividiert durch die Länge aller Wiedergabesitzungen. |
| [!UICONTROL Anzeigenanzahl] | `adCount` | Ganzzahl | Die Anzahl der Anzeigen, die während der Wiedergabe gestartet werden. |
| [!UICONTROL Kapitelanzahl] | `chapterCount` | Ganzzahl | Die Anzahl der Kapitel, die während der Wiedergabe gestartet wurden. |
| [!UICONTROL 10 % Fortschrittsmarkierung] | `hasProgress10` | Boolesch | Gibt an, dass die Abspielleiste die 10 %-Markierung des Mediums basierend auf der Stream-Länge überschritten hat. Die Markierung wird nur einmal gezählt, auch wenn eine rückwärts gerichtete Suche stattfindet. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet. |
| [!UICONTROL 25 % Fortschrittsmarkierung] | `hasProgress25` | Boolesch | Gibt an, dass die Abspielleiste die 25%-Markierung des Mediums basierend auf der Stream-Länge überschritten hat. Marker wurde nur einmal gezählt, auch wenn er nach hinten springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet. |
| [!UICONTROL 50 % Fortschrittsmarkierung] | `hasProgress50` | Boolesch | Gibt an, dass die Abspielleiste die 50%-Markierung des Mediums basierend auf der Stream-Länge überschritten hat. Marker wurde nur einmal gezählt, auch wenn er nach hinten springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet. |
| [!UICONTROL 75 % Fortschrittsmarkierung] | `hasProgress75` | Boolesch | Gibt an, dass die Abspielleiste die 75%-Markierung des Mediums basierend auf der Stream-Länge überschritten hat. Marker wurde nur einmal gezählt, auch wenn er nach hinten springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet. |
| [!UICONTROL 95 % Fortschrittsmarkierung] | `hasProgress95` | Boolesch | Gibt an, dass die Abspielleiste die 95%-Markierung des Mediums basierend auf der Stream-Länge überschritten hat. Marker wurde nur einmal gezählt, auch wenn er nach hinten springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet. |
| [!UICONTROL Geschätzte Streams] | `estimatedStreams` | Zahl | Die geschätzte Anzahl von Video- oder Audio-Streams für jedes einzelne Inhaltselement. |
| [!UICONTROL Betroffene Streams pausieren] | `hasPauseImpactedStreams` | Boolesch | Gibt an, ob während der Wiedergabe eines einzelnen Mediums eine oder mehrere Pausen aufgetreten sind. |
| [!UICONTROL Pausierung - Ereignisse] | `pauseCount` | Ganzzahl | [!UICONTROL Pausierung - Ereignisse] zählt die Anzahl der Pausenperioden, die während der Wiedergabe aufgetreten sind. |
| [!UICONTROL Pausierung - Gesamtdauer] | `pauseTime` | Ganzzahl | [!UICONTROL Pausierung - Gesamtdauer] beschreibt die Dauer in Sekunden, in der die Wiedergabe vom Benutzer angehalten wurde. |
| [!UICONTROL Mediensegmentansichten] | `hasSegmentView` | Boolesch | [!UICONTROL Mediensegmentansichten] gibt an, wann mindestens ein Frame, nicht unbedingt der erste, angezeigt wurde. |
| [!UICONTROL Zeitüberschreitung für Mediensitzungsserver] | `secondsSinceLastCall` | Zahl | Die [!UICONTROL Zeitüberschreitung für Mediensitzungsserver] gibt die Zeit in Sekunden an, die zwischen der letzten bekannten Interaktion des Benutzers und dem Zeitpunkt des Schließen der Sitzung vergangen ist. |
| [!UICONTROL Netzwerk zur Inhaltsbereitstellung] | `cdn` | Zeichenfolge | Die [!UICONTROL Netzwerk zur Inhaltsbereitstellung] des wiedergegebenen Inhalts. |
| [!UICONTROL pev3] | `pev3` | Zeichenfolge | [!UICONTROL pev3] ist der Typ des für die Berichterstellung verwendeten Medien-Streams. |
| [!UICONTROL Pccr] | `pccr` | Boolesch | [!UICONTROL Pccr] gibt an, dass eine Umleitung erfolgt ist. |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json)
