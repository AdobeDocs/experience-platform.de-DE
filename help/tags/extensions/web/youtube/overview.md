---
title: YouTube Video Tracking-Erweiterung – Übersicht
description: Erfahren Sie mehr über die YouTube Video Tracking Tag-Erweiterung in Adobe Experience Platform.
source-git-commit: 5da1fd18e0032c5e3d6695639f98a7ee683819f1
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 51%

---

# YouTube Video Tracking-Erweiterung – Übersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

**Voraussetzungen**

Für jede Tag-Eigenschaft in Adobe Experience Platform müssen die folgenden Erweiterungen über den Bildschirm &quot;Erweiterungen&quot;installiert und konfiguriert werden:

* Adobe Analytics
* Experience Cloud-Besucher-ID-Service
* Haupterweiterung

Verwenden Sie das Codefragment [&quot;Einbetten eines Players mithilfe eines \&lt;iframe\>-Tags&quot;](https://developers.google.com/youtube/player_parameters#Manual_IFrame_Embeds) aus den Google-Entwicklerdokumenten in den HTML-Code jeder Webseite, auf der ein Videoplayer gerendert werden soll.

Diese Erweiterung, Version 2.0.1, unterstützt das Einbetten eines oder mehrerer YouTube-Videos auf einer einzelnen Webseite, indem ein `id` -Attribut mit einem eindeutigen Wert im iframe-Skript-Tag eingefügt und `enablejsapi=1` und `rel=0` an das Ende des `src` -Attributwerts angehängt werden, falls noch nicht vorhanden. Beispiel:

`<iframe id="player1" width="560" height="315" src="https://www.youtube.com/embed/xpatB77BzYE?enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>`

Diese Erweiterung wurde auch entwickelt, um dynamisch nach einem eindeutigen ID-Attributwert wie `player1` zu suchen, unabhängig davon, ob die Abfragezeichenfolgenparameter `enablejsapi` und `rel` vorhanden sind und ob die erwarteten Werte korrekt sind. Daher kann das YouTube-Skript-Tag zu einer Website mit oder ohne das `id`-Attribut hinzugefügt werden und unabhängig davon, ob die Abfragezeichenfolgenparameter `enablejsapi` und `rel` enthalten sind oder nicht.

>[!NOTE]
>
>Bei Seiten mit mehr als einem Video verwendet jedes Video denselben Konfigurationssatz in der auf dieser Seite ausgeführten Tag-Regel. Wenn Sie beispielsweise eine Regel mit einem Ereignis erstellen, das beim Ansehen von 50 % eines Videos ausgelöst wird, löst jedes Video auf der Seite am 50-%-Cue-Punkt diese Regel aus.

Die Erweiterung nutzt die folgende Logik zum Umschreiben der iFrames:

```javascript
document.onreadystatechange = function () {
 if (document.readyState === 'complete') {
```

Daher tritt nach dem Laden der Seite ein leichtes Flackern auf. Dieses Verhalten ist zu erwarten.

## Datenelemente

Innerhalb der Erweiterung sind sechs Datenelemente verfügbar, von denen keines konfiguriert werden muss.

* **Abspielposition:** Zeichnet die Abspielposition auf der Video-Timeline in Sekunden auf, wenn sie in einer Tag-Regel aufgerufen wird.
* **Video-ID:** Gibt die mit dem Video verknüpfte YouTube-ID an.
* **Videoname:** Gibt den beschreibenden oder Anzeigenamen des Videos an.
* **Video-URL:** Gibt die URL von YouTube.com für das derzeit geladene/wiedergegebene Video zurück.
* **Videodauer:** Zeichnet die Gesamtdauer des Videos in Sekunden auf.
* **Erweiterungsversion:** Dieses Datenelement zeichnet die YouTube-Tracking-Erweiterungsversion auf, z. B. „Video Tracking_YouTube_2.0.0“.

## Ereignisse

In der Erweiterung sind acht Ereignisse verfügbar, von denen nur das benutzerdefinierte Cue-Punkt-Tracking konfiguriert werden muss.

* **Video bereit:** Wird ausgelöst, wenn das Video angezeigt wird und zur Wiedergabe bereit ist.
* **Videobeginn:** Wird ausgelöst, wenn das Video zum ersten Mal gestartet wird und `player.getCurrentTime() === 0`
* **Erneute Videowiedergabe:** Wird ausgelöst, wenn das Video angezeigt und nach dem ersten Beginn erneut abgespielt wird. Dieser Trigger wird bei jeder erneuten Wiedergabe ausgelöst.
* **Video-Pause:** Wird ausgelöst, wenn das Video angehalten wird.
* **Videofortsetzung:** Wird ausgelöst, wenn das Video fortgesetzt wird und wenn `player.getCurrentTime() !== 0`
* **Benutzerspezifisches Cue-Punkt-Tracking:** Wird ausgelöst, wenn das Video den vorgegebenen Video-Schwellenwert erreicht. Wenn ein Video beispielsweise 60 Sekunden dauert und der angegebene Cue-Punkt 50 % beträgt, wird das Ereignis Trigger, wenn die Abspielposition 30 Sekunden beträgt. Das Cue-Punkt-Tracking gilt sowohl für die Erstwiedergabe als auch für eine Wiederholung. Beachten Sie, dass das Ereignis nicht ausgelöst wird, wenn der Benutzer über einen Cue-Punkt springt. Cue-Punkt-Ereignisse werden nur ausgelöst, wenn die Abspielleiste den berechneten Cue-Punkt auf der Timeline passiert und der Video-Player wiedergegeben wird.
* **Videopuffer:** Wird ausgelöst, wenn der Player eine bestimmte Datenmenge herunterlädt, bevor die Wiedergabe des Videos beginnt.
* **Video beendet:** Wird ausgelöst, wenn ein Video abgeschlossen ist.

## Nutzung

Für jedes Videoereignis (die sieben oben aufgelisteten Ereignisse) kann eine Tag-Regel festgelegt werden. Erstellen Sie für jedes Ereignis, das Sie verfolgen möchten, eine bestimmte Tag-Regel. Wenn Sie ein Ereignis nicht verfolgen möchten, lassen Sie es einfach weg, eine Regel dafür zu erstellen.

Die Regeln umfassen drei Aktionen:

* **Variablen festlegen:** Festlegen der Adobe Analytics-Variablen (Zuordnen zu allen oder einigen enthaltenen Datenelementen).
* **Beacon senden:** Senden des Adobe Analytics-Beacons als benutzerspezifischer Linktracking-Aufruf und Angeben eines Wertes „Linkname“.
* **Variablen löschen:** Löschen der Adobe Analytics-Variablen.

## Beispiel-Tag-Regel für &quot;Videostart&quot;

Die folgenden Videoerweiterungsobjekte sind einzuschließen.

* **Ereignisse**: &quot;Videostart&quot;(Dieses Ereignis löst die Regel aus, wenn der Besucher mit der Wiedergabe eines YouTube-Videos beginnt.)

* **Bedingung**: Keine

* **Aktionen**: Verwenden Sie die Aktion **Analytics-Erweiterung** zum Festlegen von Variablen, um zuzuordnen:

   * Das Ereignis für Videostart,
   * Eine prop/eVar für das Datenelement „Videodauer“
   * Eine prop/eVar für das Datenelement „Video-ID“
   * Eine prop/eVar für das Datenelement „Videoname“
   * Ein prop/eVar für das Datenelement „Video-URL“

   Schließen Sie dann die Aktion &quot;Beacon senden&quot;(`s.tl`) mit dem Linknamen &quot;Videostart&quot;ein, gefolgt von der Aktion &quot;Variablen löschen&quot;.

>[!TIP]
> 
>Bei Implementierungen, bei denen nicht mehrere eVars oder Props für jedes Videoelement verwendet werden können, können Datenelementwerte innerhalb von Platform verkettet, mithilfe des Classification Rule Builder-Tools in Classification-Berichte gegliedert werden, wie unter [https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=de) erläutert, und dann als Segment in Analysis Workspace angewendet werden.

Um Videoinformationswerte zu verketten, erstellen Sie ein neues Datenelement mit dem Namen „Videometadaten“ und programmieren es so, dass es alle Videodatenelemente (oben aufgeführt) abruft und zusammenfügt. Beispiel:

```javascript
var r = ””;

r.push('YouTube'); //Player Name
r.push(_satellite.getVar('Video ID'));
r.push(_satellite.getVar('Video Name'));
r.push(_satellite.getVar('Video Duration'));
r.push(_satellite.getVar('Extension Version'));

return r.join('|');
```
