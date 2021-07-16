---
title: Asynchrone Implementierung
description: Erfahren Sie, wie Sie Adobe Experience Platform-Tag-Bibliotheken asynchron auf Ihrer Website bereitstellen.
source-git-commit: 5f810ada57eeb12a56de603d974a091b888dc9d2
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 59%

---

# Asynchrone Implementierung

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Die Leistung und nicht blockierende Bereitstellung der für unsere Produkte erforderlichen JavaScript-Bibliotheken wird für Adobe Experience Cloud-Benutzer immer wichtiger. Tools wie [[!DNL Google PageSpeed]](https://developers.google.com/speed/pagespeed/insights/) empfehlen Benutzern, die Art und Weise der Bereitstellung der Adobe-Bibliotheken auf ihrer Site zu ändern. In diesem Artikel wird erläutert, wie Sie die JavaScript-Bibliotheken der Adobe asynchron verwenden.

## Synchron und asynchron im Vergleich

### Synchrone Implementierung

Häufig werden Bibliotheken synchron im `<head>`-Tag einer Seite geladen. Beispiel:

```markup
<script src="example.js"></script>
```

Standardmäßig analysiert der Browser das Dokument, erreicht diese Zeile und ruft dann die JavaScript-Datei vom Server ab. Der Browser wartet, bis die Datei zurückgegeben wird, analysiert sie und führt sie aus. Schließlich wird die Analyse des übrigen HTML-Dokuments fortgesetzt.

Wenn der Parser vor dem Rendern sichtbarer Inhalte zum `<script>`-Tag gelangt, wird die Inhaltsanzeige verzögert. Wenn die geladene JavaScript-Datei nicht absolut erforderlich ist, um Ihren Benutzern Inhalte anzuzeigen, müssen Ihre Besucher unnötig auf Inhalte warten. Je größer die Bibliothek, desto länger die Verzögerung. Deshalb kennzeichnen Benchmark-Tools für Webperformance, wie z. B. [!DNL Google PageSpeed]oder [!DNL Lighthouse], häufig synchron geladene Skripte.

Tag Management-Bibliotheken können schnell groß werden, wenn Sie viele Tags verwalten müssen.

### Asynchrone Implementierung

Sie können jede Bibliothek asynchron laden, indem Sie dem `<script>`-Tag ein `async`-Attribut hinzufügen. Beispiel:

```markup
<script src="example.js" async></script>
```

Dies zeigt dem Browser an, dass er beim Analysieren dieses Skript-Tags mit dem Laden der JavaScript-Datei beginnen muss. Statt darauf zu warten, dass die Bibliothek geladen und ausgeführt wird, sollte der Browser den Rest des Dokuments analysieren und rendern.

## Überlegungen zur asynchronen Implementierung

Wie oben beschrieben, hält der Browser bei synchronen Bereitstellungen das Analysieren und Rendern der Seite an, während die Adobe Experience Platform-Tag-Bibliothek geladen und ausgeführt wird. In asynchronen Bereitstellungen hingegen fährt der Browser mit dem Analysieren und Rendern der Seite fort, während die Bibliothek geladen wird. Die Variabilität des Zeitpunkts, zu dem die Tag-Bibliothek fertig geladen wurde, im Verhältnis zum Parsen und Rendern der Seite muss berücksichtigt werden.

Da die Tag-Bibliothek das Laden beenden kann, bevor oder nachdem das Ende der Seite analysiert und ausgeführt wurde, sollten Sie `_satellite.pageBottom()` nicht mehr aus Ihrem Seiten-Code aufrufen (`_satellite` ist erst verfügbar, nachdem die Bibliothek geladen wurde). Dies wird unter [Asynchrones Laden des eingebetteten Tags-Codes](#loading-the-tags-embed-code-asynchronously) erläutert.

Außerdem kann das Laden der Tag-Bibliothek abgeschlossen sein, bevor oder nachdem das Browserereignis [`DOMContentLoaded`](https://developer.mozilla.org/de-DE/docs/Web/Events/DOMContentLoaded) (DOM bereit) eingetreten ist.

Aufgrund dieser beiden Punkte ist es sinnvoll zu demonstrieren, wie die Ereignistypen [Bibliothek geladen](../../extensions/web/core/overview.md#library-loaded-page-top), [Seite unten](../../extensions/web/core/overview.md#page-bottom), [DOM bereit](../../extensions/web/core/overview.md#page-bottom) und [Fenster geladen](../../extensions/web/core/overview.md#window-loaded) aus der Haupterweiterung funktionieren, wenn eine Tag-Bibliothek asynchron geladen wird.

Wenn Ihre Tag-Eigenschaft die folgenden vier Regeln enthält:

* Regel A: Verwendet den Ereignistyp „Bibliothek geladen“
* Regel B: Verwendet den Ereignistyp „Seitenende“
* Regel C: Verwendet den Ereignistyp „DOM bereit“
* Regel D: Verwendet den Ereignistyp „Fenster geladen“

Unabhängig davon, wann die Tag-Bibliothek geladen wird, werden alle Regeln garantiert in der folgenden Reihenfolge ausgeführt:

Regel A → Regel B → Regel C → Regel D

Obwohl die Reihenfolge immer durchgesetzt wird, können einige Regeln sofort ausgeführt werden, wenn die Tag-Bibliothek geladen wird, während andere später ausgeführt werden. Folgendes tritt auf, wenn das Laden der Tag-Bibliothek abgeschlossen ist:

1. Regel A wird sofort ausgeführt.
1. Wenn das Browserereignis `DOMContentLoaded` (DOM bereit) bereits eingetreten ist, werden Regeln B und C sofort ausgeführt. Andernfalls werden Regel B und Regel C später ausgeführt, wenn das Browser-Ereignis [`DOMContentLoaded`](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded) eintritt.
1. Wenn das Browser-Ereignis [`load`](https://developer.mozilla.org/de-DE/docs/Web/Events/load) (Fenster geladen) bereits eingetreten ist, wird Regel D sofort ausgeführt. Andernfalls wird Regel D später ausgeführt, wenn das Browser-Ereignis [`load`](https://developer.mozilla.org/en-US/docs/Web/Events/load) eintritt. Beachten Sie, dass - wenn Sie die Tag-Bibliothek gemäß Anweisungen installiert haben - der Ladevorgang der Tag-Bibliothek *always* abgeschlossen wird, bevor das Browserereignis [`load`](https://developer.mozilla.org/en-US/docs/Web/Events/load) auftritt.

Beachten Sie beim Anwenden dieser Prinzipien auf Ihre eigene Website folgende Punkte:

* **Regeln, die den Ereignistyp „Bibliothek geladen“ verwenden, werden möglicherweise ausgeführt, bevor die Datenschicht vollständig geladen ist.**  Dies kann dazu führen, dass die Aktionen der Regel mit fehlenden Daten ausgeführt werden, da die Daten noch nicht auf der Seite verfügbar sind. Diese Art von Problemen können Sie durch die Optimierung Ihrer Regelkonfiguration verhindern. Statt eine Regel durch den Ereignistyp „Bibliothek geladen“ auszulösen, können Sie die Ereignistypen „Benutzerspezifisches Ereignis“ oder „Direktaufruf“ verwenden. Diese werden vom Seiten-Code ausgelöst, sobald die Datenschicht geladen wurde.
* **Der Ereignistyp „Seitenende“ bietet keinen echten Mehrwert, wenn die Bibliothek asynchron geladen wird.**  Verwenden Sie stattdessen „Bibliothek geladen“, „DOM bereit“, „Fenster geladen“ oder andere Ereignistypen.

Wenn es zu einer Fehlermeldung kommt, liegen wahrscheinlich einige Timing-Probleme vor. Bereitstellungen, die ein präzises Timing erfordern, müssen möglicherweise Ereignis-Listener sowie den Ereignistyp „Benutzerspezifisches Ereignis“ oder „Direktaufruf“ verwenden, um ihre Implementierungen stabiler und einheitlicher zu gestalten.

## Asynchrones Laden des eingebetteten Tags-Codes

Tags bieten einen Umschalter zum Aktivieren des asynchronen Ladens beim Erstellen eines Einbettungscodes, wenn Sie eine [Umgebung](../publishing/environments.md) konfigurieren. Sie können das asynchrone Laden auch selbst konfigurieren:

1. Fügen Sie dem `<script>`-Tag das Attribut „async“ hinzu, um das Skript asynchron zu laden.

   Für den eingebetteten Tag-Code muss dies geändert werden:

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js"></script>
   ```

   ... wie folgt ändern:

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js" async></script>
   ```

1. Entfernen Sie sämtlichen Code, den Sie zuvor unten im Tag hinzugefügt haben:

   ```markup
   <script type="text/javascript">_satellite.pageBottom();</script>
   ```

   Dieser Code teilt Platform mit, dass der Browser-Parser den unteren Seitenrand erreicht hat. Es ist wahrscheinlich, dass Tags vor diesem Zeitpunkt nicht geladen und ausgeführt wurden. Daher führt der Aufruf von `_satellite.pageBottom()` zu einem Fehler und der Ereignistyp &quot;Seitenende&quot;verhält sich möglicherweise nicht wie erwartet.
