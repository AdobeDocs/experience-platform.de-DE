---
title: Asynchrone Implementierung
description: Erfahren Sie, wie Sie Tag-Bibliotheken von Adobe Experience Platform asynchron auf Ihrer Website bereitstellen.
exl-id: ed117d3a-7370-42aa-9bc9-2a01b8e7794e
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: ht
source-wordcount: '1079'
ht-degree: 100%

---

# Asynchrone Implementierung {#asynchronous-deployment}

>[!CONTEXTUALHELP]
>id="platform_tags_asynchronous_deployment"
>title="Asynchrone Implementierung"
>abstract="Wenn diese Option aktiviert ist, beginnt der Browser beim Parsen dieses Skript-Tags mit dem Laden der JavaScript-Datei, aber anstatt darauf zu warten, dass die Bibliothek geladen und ausgeführt wird, fährt er mit dem Parsen und Rendern des restlichen Dokuments fort. Dies kann die Leistung der Web-Seite verbessern, hat jedoch wichtige Auswirkungen auf die Ausführung bestimmter Regeln. Einzelheiten finden Sie in der Dokumentation."

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Performance und blockierungsfreie Implementierung der von unseren Produkten benötigten JavaScript-Bibliotheken sind für Adobe Experience Cloud-Anwender zunehmend wichtig. Tools wie [[!DNL Google PageSpeed]](https://developers.google.com/speed/pagespeed/insights/) empfehlen, dass die Benutzer die Art und Weise der Bereitstellung der Adobe Bibliotheken auf ihrer Site ändern. Dieser Artikel erklärt, wie Sie die Adobe-JavaScript-Bibliotheken asynchron verwenden können.

## Synchron und asynchron im Vergleich

### Synchrone Implementierung

Häufig werden Bibliotheken synchron im `<head>`-Tag einer Seite geladen. Beispiel:

```markup
<script src="example.js"></script>
```

Standardmäßig analysiert der Browser das Dokument, erreicht diese Zeile und ruft dann die JavaScript-Datei vom Server ab. Der Browser wartet, bis die Datei zurückgegeben wird, analysiert die JavaScript-Datei und führt sie aus. Schließlich wird die Analyse des übrigen HTML-Dokuments fortgesetzt.

Wenn der Parser vor dem Rendern sichtbarer Inhalte zum `<script>`-Tag gelangt, wird die Inhaltsanzeige verzögert. Wenn die geladene JavaScript-Datei nicht absolut erforderlich ist, um Ihren Benutzern Inhalte anzuzeigen, müssen Ihre Besucher unnötig auf Inhalte warten. Je größer die Bibliothek, desto länger die Verzögerung. Deshalb kennzeichnen Benchmark-Tools für Webperformance, wie z. B. [!DNL Google PageSpeed]oder [!DNL Lighthouse], häufig synchron geladene Skripte.

Tag-Management-Bibliotheken können schnell unübersichtlich werden, wenn viele Tags zu verwalten sind.

### Asynchrone Implementierung

Sie können jede Bibliothek asynchron laden, indem Sie dem `<script>`-Tag ein `async`-Attribut hinzufügen. Beispiel:

```markup
<script src="example.js" async></script>
```

Dies zeigt dem Browser an, dass er beim Analysieren dieses Skript-Tags mit dem Laden der JavaScript-Datei beginnen muss. Statt darauf zu warten, dass die Bibliothek geladen und ausgeführt wird, sollte der Browser den Rest des Dokuments analysieren und rendern.

## Überlegungen zur asynchronen Implementierung

Wie oben beschrieben, hält der Browser bei synchronen Implementierungen Analyse und Rendern der Seite an, während die Tag-Bibliothek von Adobe Experience Platform geladen und ausgeführt wird. In asynchronen Implementierungen hingegen fährt der Browser mit dem Analysieren und Rendern der Seite fort, während die Bibliothek geladen wird. Diese Varianz zwischen dem Zeitpunkt, zu dem die Tag-Bibliothek fertig geladen wurde, und dem Analysieren und Rendern der Seite muss berücksichtigt werden.

Da die Tag-Bibliothek vor oder nach Analyse des Seitenendes vollständig geladen und ausgeführt werden kann, sollten Sie `_satellite.pageBottom()` nicht mehr aus Ihrem Seiten-Code aufrufen (`_satellite` ist erst nach dem Laden der Bibliothek verfügbar). Dies wird unter [Asynchrones Laden des Tag-Einbettungs-Codes](#loading-the-tags-embed-code-asynchronously) näher erläutert.

Außerdem kann das Laden der Tag-Bibliothek abgeschlossen werden, bevor oder nachdem das Browser-Ereignis [`DOMContentLoaded`](https://developer.mozilla.org/de-DE/docs/Web/Events/DOMContentLoaded) (DOM bereit) eingetreten ist.

Aufgrund dieser beiden Punkte ist es sinnvoll, zu veranschaulichen, wie die Ereignistypen [Bibliothek geladen](../../extensions/client/core/overview.md#library-loaded-page-top), [Seitenende](../../extensions/client/core/overview.md#page-bottom), [DOM bereit](../../extensions/client/core/overview.md#page-bottom) und [Fenster geladen](../../extensions/client/core/overview.md#window-loaded) aus der Haupterweiterung funktionieren, wenn eine Tag-Bibliothek asynchron geladen wird.

Wenn Ihre Tag-Eigenschaft die folgenden vier Regeln enthält:

* Regel A: Verwendet den Ereignistyp „Bibliothek geladen“
* Regel B: Verwendet den Ereignistyp „Seitenende“
* Regel C: Verwendet den Ereignistyp „DOM bereit“
* Regel D: Verwendet den Ereignistyp „Fenster geladen“

Unabhängig davon, wann die Tag-Bibliothek fertig geladen ist, werden alle Regeln garantiert in der folgenden Reihenfolge ausgeführt:

Regel A → Regel B → Regel C → Regel D

Obwohl die Reihenfolge immer durchgesetzt wird, können einige Regeln sofort nach dem Laden der Tag-Bibliothek ausgeführt werden, während andere möglicherweise erst später ausgeführt werden. Folgendes tritt auf, wenn die Tag-Bibliothek geladen wird:

1. Regel A wird sofort ausgeführt.
1. Wenn das Browserereignis `DOMContentLoaded` (DOM bereit) bereits eingetreten ist, werden Regeln B und C sofort ausgeführt. Andernfalls werden Regel B und Regel C später ausgeführt, wenn das Browser-Ereignis [`DOMContentLoaded`](https://developer.mozilla.org/de-DE/docs/Web/Events/DOMContentLoaded) eintritt.
1. Wenn das Browser-Ereignis [`load`](https://developer.mozilla.org/de-DE/docs/Web/Events/load) (Fenster geladen) bereits eingetreten ist, wird Regel D sofort ausgeführt. Andernfalls wird Regel D später ausgeführt, wenn das Browser-Ereignis [`load`](https://developer.mozilla.org/de-DE/docs/Web/Events/load) eintritt. Beachten Sie, dass – wenn Sie die Tag-Bibliothek gemäß Anweisungen installiert haben – der Ladevorgang der Tag-Bibliothek *immer* abgeschlossen wird, bevor das Browser-Ereignis [`load`](https://developer.mozilla.org/de-DE/docs/Web/Events/load) auftritt.

Beachten Sie beim Anwenden dieser Prinzipien auf Ihre eigene Website folgende Punkte:

* **Regeln, die den Ereignistyp „Bibliothek geladen“ verwenden, werden möglicherweise ausgeführt, bevor die Datenschicht vollständig geladen ist.**  Dies kann dazu führen, dass die Aktionen der Regel mit fehlenden Daten ausgeführt werden, da die Daten noch nicht auf der Seite verfügbar sind. Diese Art von Problemen können Sie durch die Optimierung Ihrer Regelkonfiguration verhindern. Statt eine Regel durch den Ereignistyp „Bibliothek geladen“ auszulösen, können Sie die Ereignistypen „Benutzerspezifisches Ereignis“ oder „Direktaufruf“ verwenden. Diese werden vom Seiten-Code ausgelöst, sobald die Datenschicht geladen wurde.
* **Der Ereignistyp „Seitenende“ bietet keinen echten Mehrwert, wenn die Bibliothek asynchron geladen wird.**  Verwenden Sie stattdessen „Bibliothek geladen“, „DOM bereit“, „Fenster geladen“ oder andere Ereignistypen.

Wenn es zu einer Fehlermeldung kommt, liegen wahrscheinlich einige Timing-Probleme vor. Bereitstellungen, die ein präzises Timing erfordern, müssen möglicherweise Ereignis-Listener sowie den Ereignistyp „Benutzerspezifisches Ereignis“ oder „Direktaufruf“ verwenden, um ihre Implementierungen stabiler und einheitlicher zu gestalten.

## Asynchrones Laden des Tag-Einbettungs-Codes

Tags sind mit einer Schaltfläche versehen, über die Sie das asynchrone Laden aktivieren können, wenn Sie bei der Konfiguration einer [Umgebung](../publishing/environments.md) einen Einbettungs-Code erstellen. Sie können das asynchrone Laden auch selbst konfigurieren:

1. Fügen Sie dem `<script>`-Tag das Attribut „async“ hinzu, um das Skript asynchron zu laden.

   Im Tags-Einbettungs-Code bedeutet das eine Änderung von:

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

   Dieser Code informiert Platform darüber, dass der Browser-Parser das Seitenende erreicht hat. Da Tags vor diesem Zeitpunkt wahrscheinlich nicht geladen und ausgeführt wurden, führt der Aufruf von `_satellite.pageBottom()` zu einem Fehler, und der Ereignistyp „Seitenende“ verhält sich möglicherweise nicht wie erwartet.
