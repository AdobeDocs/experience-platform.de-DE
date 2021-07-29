---
title: BrightCove Video Tracking-Erweiterung – Übersicht
description: Erfahren Sie mehr über die BrightCove Video Tracking Tag-Erweiterung in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 38%

---

# BrightCove Video Tracking-Erweiterung – Übersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

## Voraussetzungen

Für jede Tag-Eigenschaft in Adobe Experience Platform müssen die folgenden Erweiterungen im Bildschirm &quot;Erweiterung&quot;installiert und konfiguriert werden:

* Adobe Analytics
* Experience Cloud-Besucher-ID-Service
* Installierte Core-Erweiterungen

Verwenden Sie das Codefragment &quot;In-Page embed code (Advanced)&quot;im HTML-Code jeder Webseite, auf der ein Videoplayer gerendert werden soll. Das HTML-Snippet &quot;In-Page Embed code (Advanced)&quot;finden Sie in der [Brightcove-Dokumentation](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage). Der folgende Link enthält weitere Informationen zum Generieren von eingebettetem Code für Vorschau- und veröffentlichte Videoplayer](https://de.studio.support.brightcove.com/players/generating-player-embed-code.html).[

Diese Erweiterungsversion 1.1.0 unterstützt das Einbetten mehrerer BrightCove-Videos auf einer einzelnen Webseite. Wenn es innerhalb der erweiterten Einbettungs-Tags mehrere `id`-Eigenschaften gibt, stellen Sie sicher, dass sie jeweils über eindeutige Werte verfügen. Zum Beispiel `player1`, `player2` usw.

>[!NOTE]
>
>Auf Seiten mit mehreren Videos verwendet jedes Video dieselbe Konfiguration, die in der auf dieser Seite ausgeführten Tag-Regel festgelegt ist. Wenn Sie beispielsweise eine Regel mit einem Ereignis erstellen, das bei 50 % Abschluss des Videos ausgelöst wird, löst jedes Video auf der Seite die Regel am 50-%-Cue-Punkt aus.

Wenn die Webseite, die diese Erweiterung verwendet, mit dem Video interagiert, bevor das entsprechende Skript vollständig geladen wurde, gibt es zwei Aktionen, die Sie ausführen können, um das Problem zu beheben. Erstens kann die Tag-Bibliothek synchron geladen werden, und zweitens kann das Element `<script type="text/javascript">\_satellite.pageBottom();\</script\>` vor der Videoeinbettung auf der Seite platziert werden.

Weitere Informationen zu den in dieser Erweiterung verwendeten Komponentenmethoden und -ereignissen finden Sie in der [BrightCove API-Dokumentation](https://docs.brightcove.com/brightcove-player/1.x/Player.html#vjsplayer) .

## Datenelemente

Es sind sieben Datenelemente innerhalb der Erweiterung verfügbar, von denen keines konfiguriert werden muss.

* **Abspielposition:** Wenn dieses Datenelement in einer Tag-Regel aufgerufen wird, wird in Sekunden der Ort der Abspielposition auf der Video-Timeline aufgezeichnet.
* **Video-Account-ID:** Dieses Datenelement zeichnet die ID des Brightcove-Accounts auf, der das Video veröffentlicht hat.
* **Videodauer:** Dieses Datenelement zeichnet die Gesamtdauer des Videoinhalts in Sekunden auf. Darüber hinaus kann in Analytics eine berechnete Metrik erstellt werden, um die Sekundenanzahl in Minuten oder Stunden umzurechnen.
* **Videoanzeigenunterstützung:**  Dieses Datenelement gibt an, ob Anzeigen im Video unterstützt werden sollen.
* **Video-ID:** Dieses Datenelement zeigt die BrightCove-ID an, die mit dem Video verknüpft ist.
* **Videoname:** Dieses Datenelement gibt den beschreibenden oder Klarnamen des Videos an.
* **Video-Tags:** Dieses Datenelement gibt die bestimmten Skripte an, die mit dem Video verknüpft sind.

## Ereignisse

In der Erweiterung sind sieben Ereignisse verfügbar. Nur das benutzerdefinierte Cue-Punkt-Tracking muss konfiguriert werden.

* **Benutzerdefiniertes Cue-Punkt-Tracking:** Dieses Ereignis wird ausgelöst, wenn das Video den angegebenen Videoschwellenprozentsatz erreicht. Wenn ein Video beispielsweise 60 Sekunden lang ist und der angegebene Cue-Punkt 50 % beträgt, wird das Ereignis bei der 30-Sekunden-Markierung Trigger.

>[!NOTE]
>
>Dieses Ereignis wird jedes Mal ausgelöst, wenn dieser Cue-Punkt erreicht wird. Wenn der Benutzer beispielsweise die 50-%-Marke erreicht, das Video vor der 50-%-Marke durchsucht und dann wieder die 50-%-Marke erreicht, wird der Auslöser erneut ausgelöst.

* **Video abgeschlossen:** Dieses Ereignis wird Trigger, wenn ein Video abgeschlossen ist.
* **Videogeladene Metadaten:** Dieses Ereignis wird ausgelöst, wenn der Player die ursprünglichen Dauer- und Dimensionsinformationen erhalten hat.
* **Videopause:** Dieses Ereignis wird ausgelöst, wenn das Video angehalten wird.
* **Videowiederaufnahme:** Dieses Ereignis wird ausgelöst, wenn das Video nach einer Pause wieder aufgenommen wird.
* **Videobildschirmänderung:** Das Ereignis wird Trigger, wenn das Video in den Vollbildmodus wechselt oder aus diesem herausgeht.
* **Videostart:** Dieses Ereignis wird ausgelöst, wenn das Video zum ersten Mal startet.

## Nutzung

Für jedes Videoereignis (die sieben oben aufgelisteten Ereignisse) kann eine Tag-Regel festgelegt werden. Erstellen Sie für jedes Ereignis, das Sie verfolgen möchten, eine bestimmte Tag-Regel. Wenn Sie ein Ereignis nicht verfolgen möchten, lassen Sie es einfach weg, eine Regel dafür zu erstellen.

Die Regeln beinhalten drei Aktionen:

1. Legen Sie die Adobe Analytics-Variablen fest. (Erstellen Sie Datenelemente für alle oder einige der oben aufgeführten Datenelemente.)
1. Senden Sie das Adobe Analytics-Beacon.
1. Löschen Sie die Adobe Analytics-Variablen.

## Beispiel-Tag-Regel für &quot;Videostart&quot;

Die folgenden Videoerweiterungsobjekte sind einzuschließen:

* **Ereignisse**

   1. „Videostart“: Dieses Ereignis löst die Regel aus, wenn der Besucher ein BrightCove-Video abspielt.

* **Bedingung**

   1. Keine

* **Aktionen**

   1. Legen Sie in der Analytics-Aktion „Variablen festlegen“ Folgendes fest:

      * Das Ereignis für **Videostart** (Beispiel: Ereignis17)
      * Eine prop/eVar für das Datenelement **Videoname** (Beispiel: eVar10)
      * Eine prop/eVar für das Datenelement **Videodauer** (Beispiel: eVar11)
      * Eine prop/eVar für das Datenelement **Aktueller Videoplatz** (Beispiel: eVar12)
   1. Die Analytics-Aktion „Beacon senden“ (`s.tl`)
   1. Die Analytics-Aktion „Variablen löschen“


>[!TIP]
>
>Diejenigen, die nicht mehrere eVars oder props für jedes Videoelement bereitstellen möchten, haben eine alternative Methode. Datenelementwerte können über die Datenerfassungs-Benutzeroberfläche verkettet werden. Anschließend werden sie mithilfe des Classification Rule Builder-Tools in Classification-Berichte analysiert. Weitere Informationen finden Sie in der Dokumentation zum [Classification Rule Builder-Tool](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=de) . Schließlich werden sie als Segment in Analysis Workspace angewendet.
>
>Erstellen Sie dazu ein neues Datenelement mit dem Namen &quot;Videometadaten&quot;und programmieren Sie es so, dass alle Videodatenelemente (oben aufgelistet) abgerufen und miteinander verkettet werden.

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
