---
title: BrightCove Video Tracking-Erweiterung – Übersicht
description: Machen Sie sich mit der Tag-Erweiterung „BrightCove Video Tracking“ in Adobe Experience Platform vertraut.
exl-id: d27eff21-2abf-4495-8382-08cab32742e0
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 97%

---

# BrightCove Video Tracking-Erweiterung – Übersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

## Voraussetzungen

Für jede Tag-Eigenschaft in Adobe Experience Platform müssen die folgenden Erweiterungen im Erweiterungsbildschirm installiert und konfiguriert werden:

* Adobe Analytics
* Experience Cloud-Besucher-ID-Service
* Installierte Core-Erweiterungen

Verwenden Sie das Code-Fragment „In-Page embed code (Advanced)“ im HTML-Code jeder Web-Seite, auf der ein Video-Player gerendert werden soll. Das HTML-Fragment „In-Page Embed code (Advanced)“ finden Sie in der [Brightcove-Dokumentation](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage). Der folgende Link enthält weitere Informationen zum [Generieren von eingebettetem Code für Vorschau und veröffentlichte Video-Player](https://de.studio.support.brightcove.com/players/generating-player-embed-code.html).

Diese Erweiterungsversion 1.1.0 unterstützt das Einbetten mehrerer BrightCove-Videos auf einer einzelnen Web-Seite. Wenn es innerhalb der erweiterten Einbettungs-Tags mehrere `id`-Eigenschaften gibt, stellen Sie sicher, dass sie jeweils über eindeutige Werte verfügen. Beispielsweise `player1`, `player2` und so weiter.

>[!NOTE]
>
>Beachten Sie bei Seiten mit mehreren Videos, dass jedes Video dieselbe Konfiguration verwendet, die in der auf dieser Seite ausgeführten Tag-Regel festgelegt ist. Wenn Sie beispielsweise eine Regel mit einem Ereignis erstellen, das bei 50 % Abschluss des Videos ausgelöst wird, löst jedes Video auf der Seite die Regel am 50-%-Cue-Punkt aus.

Wenn die Web-Seite, die diese Erweiterung verwendet, mit dem Video interagiert, bevor das entsprechende Skript vollständig geladen wurde, gibt es zwei Aktionen, mit denen Sie dsa Problem beheben können. Zum einen kann die Tag-Bibliothek synchron geladen werden und zum anderen kann das Element `<script type="text/javascript">\_satellite.pageBottom();\</script\>` vor der Videoeinbettung auf der Seite platziert werden.

Weitere Informationen zu den in dieser Erweiterung verwendeten Komponentenmethoden und -ereignissen finden Sie in der [Dokumentation zur BrightCove-API](https://docs.brightcove.com/brightcove-player/1.x/Player.html#vjsplayer).

## Datenelemente

Es sind sieben Datenelemente innerhalb der Erweiterung verfügbar, von denen keines konfiguriert werden muss.

* **Abspielposition:** Wenn dieses Datenelement in einer Tag-Regel aufgerufen wird, wird in Sekunden der Ort der Abspielposition auf der Video-Timeline aufgezeichnet.
* **Video-Account-ID:** Dieses Datenelement zeichnet die ID des Brightcove-Accounts auf, der das Video veröffentlicht hat.
* **Videodauer:** Dieses Datenelement zeichnet die Gesamtdauer des Videoinhalts in Sekunden auf. Darüber hinaus kann in Analytics eine berechnete Metrik erstellt werden, um die Sekundenanzahl in Minuten oder Stunden umzurechnen.
* **Unterstützung für Videoanzeigen:** Dieses Datenelement gibt an, ob Anzeigen innerhalb des Videos unterstützt werden oder nicht.
* **Video-ID:** Dieses Datenelement zeigt die BrightCove-ID an, die mit dem Video verknüpft ist.
* **Videoname:** Dieses Datenelement gibt den beschreibenden oder Klarnamen des Videos an.
* **Video-Tags:** Dieses Datenelement gibt die speziellen Skripte an, die dem Video zugeordnet sind.

## Ereignisse

In der Erweiterung sind sieben Ereignisse verfügbar. Nur das benutzerdefinierte Cue-Punkt-Tracking muss konfiguriert werden.

* **Benutzerdefiniertes Cue-Punkt-Tracking:** Dieses Ereignis wird ausgelöst, wenn das Video den angegebenen Videoschwellenprozentsatz erreicht. Wenn ein Video beispielsweise 60 Sekunden dauert und der vorgegebene Cue-Punkt bei 50 % liegt, wird das Ereignis an der 30-Sekunden-Markierung ausgelöst. 

>[!NOTE]
>
>Dieses Ereignis wird jedes Mal ausgelöst, wenn dieser Cue-Punkt erreicht wird. Wenn der Benutzer beispielsweise die 50-%-Marke erreicht, das Video vor der 50-%-Marke durchsucht und dann wieder die 50-%-Marke erreicht, wird der Auslöser erneut ausgelöst.

* **Video abgeschlossen:** Dieses Ereignis wird ausgelöst, wenn ein Video vollständig abgeschlossen ist.
* **Geladene Videometadaten:** Dieses Ereignis wird ausgelöst, wenn der Player anfängliche Informationen zu Dauer und Abmessungen erhalten hat.
* **Videopause:** Dieses Ereignis wird ausgelöst, wenn das Video angehalten wird.
* **Videowiederaufnahme:** Dieses Ereignis wird ausgelöst, wenn das Video nach einer Pause wieder aufgenommen wird.
* **Änderung des Videobildschirms:** Das Ereignis wird ausgelöst, wenn das Video in den oder aus dem Vollbildmodus wechselt.
* **Videostart:** Dieses Ereignis wird ausgelöst, wenn das Video zum ersten Mal startet.

## Nutzung

Für jedes Videoereignis (die sieben oben aufgelisteten Ereignisse) kann eine Tag-Regel festgelegt werden. Erstellen Sie für jedes Ereignis, das Sie verfolgen möchten, eine spezifische Tag-Regel. Wenn Sie ein Ereignis nicht verfolgen möchten, verzichten Sie einfach darauf, eine Regel dafür zu erstellen.

Die Regeln beinhalten drei Aktionen:

1. Legen Sie die Adobe Analytics-Variablen fest. (Erstellen Sie Datenelemente für alle oder einige der oben aufgeführten Datenelemente.)
1. Senden Sie das Adobe Analytics-Beacon.
1. Löschen Sie die Adobe Analytics-Variablen.

## Beispiel für eine Tag-Regel für „Videostart“

Die folgenden Video-Erweiterungsobjekte sind einzuschließen:

* **Ereignisse**

   1. „Videostart“: Dieses Ereignis löst die Regel aus, wenn der Besucher ein BrightCove-Video abspielt.

* **Bedingung**

   1. Keine

* **Aktionen**

   1. Legen Sie in der Analytics-Aktion „Variablen festlegen“ Folgendes fest:

      * Das Ereignis für **Videostart** (Beispiel: Ereignis17)
      * Eine Prop/eVar für das Datenelement **Videoname** (Beispiel: eVar10)
      * Eine Prop/eVar für das Datenelement **Videodauer** (Beispiel: eVar11)
      * Eine Prop/eVar für das Datenelement **Aktuelle Videoposition** (Beispiel: eVar12)
   1. Die Analytics-Aktion „Beacon senden“ (`s.tl`)
   1. Die Analytics-Aktion „Variablen löschen“


>[!TIP]
>
>Diejenigen, die nicht mehrere eVars oder props für jedes Videoelement bereitstellen möchten, werden Datenelementwerte als alternative Methode verkettet. Anschließend werden sie mithilfe des Classification Rule Builder Tools in Klassifizierungsberichte übermittelt. Weitere Informationen finden Sie in der Dokumentation zum [Classification Rule Builder Tool](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=de). Schließlich werden sie als Segment in Analysis Workspace angewendet.
>
>Erstellen Sie dazu ein neues Datenelement mit einem Namen wie „Videometadaten“ und programmieren Sie es so, dass alle oben aufgelisteten Videodatenelemente abgerufen und miteinander verkettet werden.

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
