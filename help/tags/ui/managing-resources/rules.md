---
title: Regeln
description: Machen Sie sich mit der Funktionsweise von Tag-Erweiterungen in Adobe Experience Platform vertraut.
source-git-commit: 272cf2906b44ccfeca041d9620ac0780e24ad1ae
workflow-type: ht
source-wordcount: '1977'
ht-degree: 100%

---

# Regeln

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere Terminologieänderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Tags in Adobe Experience Platform folgen einem regelbasierten System. Sie suchen nach Benutzerinteraktionen und zugehörigen Daten. Wenn die in Ihren Regeln formulierten Kriterien erfüllt sind, löst die Regel die jeweils definierte Erweiterung, das Skript oder den Client-seitigen Code aus.

Erstellen Sie Regeln, um die Daten und Funktionen von Marketing- und Werbetechnologien zu integrieren, die verschiedene Produkte in einer einzigen Lösung zusammenführen.

## Regelstruktur

**Ereignisse (If):** Das Ereignis ist das Element, nach dem die Regel suchen soll. Wählen Sie hierzu ein Ereignis sowie die jeweiligen Bedingungen und etwaige Ausnahmen aus.

**Aktionen (Then):** Auslöser treten auf, nachdem die Ereignisse einer Regel aufgetreten sind und alle Bedingungen erfüllt wurden. Eine Tag-Regel kann beliebig viele einzelne Aktionen auslösen. Sie können die Reihenfolge steuern, in der diese Aktionen ausgeführt werden. So kann beispielsweise eine einzelne Regel für eine E-Commerce-Dankeschön-Seite Ihre Analyse-Tools sowie Drittanbieter-Tags auslösen. Es müssen keine separaten Regeln für die einzelnen Erweiterungen oder Tags erstellt werden.

Sie können weitere Ereignistypen hinzufügen. Mehrere Ereignisse werden mit einem OR zusammengefügt. Demzufolge werden die Bedingungen der Regel ausgewertet, wenn ein Ereignis eintritt.

>[!IMPORTANT]
>
>Änderungen werden erst wirksam, nachdem sie [veröffentlicht](../publishing/overview.md) wurden.

### Ereignisse und Bedingungen (if)

Ereignisse mit Bedingungen sind der *If*-Teil der Regel.

Wenn ein bestimmtes Ereignis eintritt, werden die Bedingungen ausgewertet und ggf. die angegebenen Aktionen ausgeführt.

* **Ereignisse**: Geben Sie ein oder mehrere Ereignisse an, die zum Auslösen der Regel auftreten müssen. Mehrere Ereignisse werden durch ein OR verbunden. Jedes der angegebenen Ereignisse löst die Regel aus.

* **Bedingungen**: Grenzen Sie das Ereignis ein, indem Sie alle Bedingungen konfigurieren, die für ein Ereignis erfüllt sein müssen, damit die Regel ausgelöst wird. Ausnahmen werden als NOT-Bedingung definiert. Mehrere Bedingungen werden durch ein AND verbunden.

Die verfügbaren Ereignisse hängen davon ab, welche Erweiterungen installiert wurden. Informationen zu den Ereignissen in der Haupterweiterung finden Sie unter [Ereignistypen der Haupterweiterung](../../extensions/web/core/overview.md#core-extension-event-types).

### Aktionen (then)

Aktionen sind der *Then*-Teil einer Regel. Sie definieren, was beim Ausführen der Regel passieren soll. Wenn ein Ereignis ausgelöst wird und hierbei die Bedingungen erfüllt sowie die Ausnahmen nicht erfüllt werden, werden die Aktionen ausgeführt. Sie können Aktionen beliebig per Drag-and-Drop sortieren.

## Erstellen einer Regel

Erstellen Sie eine Regel, indem Sie angeben, welche Aktionen ausgeführt werden sollen, wenn eine Bedingung erfüllt wird.

1. Öffnen Sie die Registerkarte [!UICONTROL Regeln] und wählen Sie **[!UICONTROL Neue Regel erstellen]** aus.

   ![](../../images/launch-rule-builder.jpg)

1. Geben Sie einen Namen für die Regel ein.
1. Klicken Sie unter „Ereignisse“ auf das Symbol **[!UICONTROL Hinzufügen]**.
1. Wählen Sie Ihre Erweiterung und einen der für diese Erweiterung verfügbaren Ereignistyp aus und konfigurieren Sie dann die Einstellungen für das Ereignis.

   ![](../../images/rule-event-config.png)

   Die verfügbaren Ereignistypen hängen von der ausgewählten Erweiterung ab. Die Ereigniseinstellungen unterscheiden sich je nach Ereignistyp. Einige Ereignisse verfügen nicht über Eigenschaften, die konfiguriert werden müssen.

   >[!IMPORTANT]
   >
   >In einer Client-seitigen Regel werden Datenelemente mit einem `%`-Token am Anfang und am Ende des Datenelementnamens versehen. Beispiel: `%viewportHeight%`. In einer Ereignisweiterleitungsregel werden Datenelemente mit einem `{{`-Token am Anfang und einem `}}`-Token am Ende des Datenelementnamens versehen. Beispiel: `{{viewportHeight}}`.

   Um Daten aus dem Edge-Netzwerk zu referenzieren, muss der Datenelementpfad `arc.event._<element>_` sein.

   `arc` steht für Adobe Response Context.

   Beispiel: `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >Wenn dieser Pfad falsch angegeben wird, werden keine Daten erfasst.

1. Legen Sie den Parameter „Reihenfolge“ fest und klicken Sie auf **[!UICONTROL Änderungen beibehalten]**.

   Die Standardpriorität aller Regelkomponenten lautet 50. Wenn sie früher ausgeführt werden sollen, geben Sie eine Zahl unter 50 an.

   * Die Regeln werden in der aufsteigenden Reihenfolge dieser Zahlen ausgeführt. 1 wird vor 3 ausgeführt, 3 wird vor 10 ausgeführt, 10 vor 100 usw.
   * Regeln mit derselben Priorität werden ohne bestimmte Reihenfolge ausgeführt.
   * Regeln werden in der angegebenen Reihenfolge ausgelöst, enden jedoch nicht unbedingt in dieser Reihenfolge. Wenn die Regeln A und B sich ein Ereignis teilen, Sie die Reihenfolge so zuweisen, dass Regel A zuerst eintritt, und Regel A asynchron ausgeführt wird, gibt es keine Garantie, dass Regel A abgeschlossen ist, bevor Regel B beginnt.

      Wenn sie später ausgeführt werden soll, geben Sie eine Zahl über 50 an. Weitere Informationen zur Reihenfolge finden Sie unter [Regelreihenfolge](rules.md#rule-ordering).

1. Klicken Sie auf das Symbol **[!UICONTROL Hinzufügen]** für Bedingungen, wählen Sie dann einen Logiktyp, eine Erweiterung sowie einen Bedingungstyp aus und konfigurieren Sie die Einstellungen für Ihre Bedingung. Wählen Sie als Nächstes **[!UICONTROL Änderungen beibehalten]** aus.

   ![](../../images/condition-settings.png)

   Die verfügbaren Bedingungstypen hängen von der ausgewählten Erweiterung ab. Die Bedingungseinstellungen unterscheiden sich je nach Bedingungstyp.

   Logiktyp:

   * Der Logiktyp „Regulär“ ermöglicht die Ausführung von Aktionen, wenn die Bedingung erfüllt wird.
   * Der Logiktyp „Ausnahme“ verhindert die Ausführung von Aktionen, wenn die Bedingung erfüllt wird.

   (Erweitert) Zeitüberschreitung: Diese Option ist verfügbar, wenn die Sequenzierung von Regelkomponenten für Ihre Eigenschaft aktiviert ist. Dieses Attribut definiert die maximale Zeitspanne, die für die Ausführung der Bedingung zulässig ist. Wenn die Zeitüberschreitung erreicht wird, schlägt die Bedingung fehl und der Rest der Bedingungen und Aktionen der Regel wird aus der Verarbeitungswarteschlange entfernt. Der Standardwert beträgt 2000 ms.

   Sie können beliebig viele Bedingungen hinzufügen. Mehrere Bedingungen innerhalb derselben Regel werden durch AND verknüpft.

1. Klicken Sie auf das Symbol **[!UICONTROL Hinzufügen]** für Aktionen, wählen Sie dann Ihre Erweiterung und einen für diese Erweiterung verfügbaren Aktionstyp aus, konfigurieren Sie die Einstellungen für die Aktion und klicken Sie auf **[!UICONTROL Änderungen beibehalten]**.

   ![](../../images/action-settings.png)

   Die verfügbaren Aktionstypen hängen von der ausgewählten Erweiterung ab. Die Aktionseinstellungen unterscheiden sich je nach Aktionstyp.

   (Erweitert) Mit Ausführung der nächsten Aktion warten: Diese Option ist verfügbar, wenn die Sequenzierung von Regelkomponenten für Ihre Eigenschaft aktiviert ist. Wenn diese Option aktiviert ist, rufen Tags die nächste Aktion erst nach Abschluss dieser Aktion auf. Wenn diese Option deaktiviert ist, wird die nächste Aktion sofort ausgeführt. Standardmäßig ist die Option **[!UICONTROL aktiviert]**.

   (Erweitert) Zeitüberschreitung: Diese Option ist verfügbar, wenn die Sequenzierung von Regelkomponenten für Ihre Eigenschaft aktiviert ist. Sie definiert die maximale Zeitspanne, die für die Ausführung der Aktion zulässig ist. Wenn die Zeitüberschreitung erreicht wird, schlägt die Aktion fehl und alle nachfolgenden Aktionen für diese Regel werden aus der Verarbeitungswarteschlange entfernt. Der Standardwert beträgt 2000 ms.


1. Überprüfen Sie Ihre Regel und wählen Sie **[!UICONTROL Regel speichern]** aus.

   Wenn Sie die Regel später [veröffentlichen](../publishing/overview.md), fügen Sie sie einer Bibliothek hinzu und stellen sie bereit.

Beim Erstellen oder Bearbeiten von Regeln können Sie diese Regeln in Ihrer [aktiven Bibliothek](../publishing/libraries.md#active-library) speichern und erstellen. Dadurch werden Ihre Änderungen direkt in Ihrer Bibliothek gespeichert, und ein Build wird ausgeführt. Der Build-Status wird angezeigt.

## Regelsortierung {#rule-ordering}

Mit der Regelsortierung können Sie steuern, in welcher Reihenfolge Regeln, die sich ein Ereignis teilen, ausgeführt werden.

In vielen Fällen ist es erforderlich, dass Ihre Regeln in einer bestimmten Reihenfolge ausgelöst werden. Beispiele: (1) Sie verfügen über mehrere Regeln, die bedingt [!DNL Analytics]-Variablen festlegen, und müssen sicherstellen, dass die Regel mit „Beacon senden“ zuletzt ausgeführt wird. (2) Sie nutzen eine Regel, die [!DNL Target] auslöst, und eine andere, die [!DNL Analytics] auslöst. Die [!DNL Target]-Regel soll hierbei zuerst ausgeführt werden.

Letztendlich ist der Entwickler des von Ihnen verwendeten Ereignistyps für die Ausführung von Aktionen in der richtigen Reihenfolge verantwortlich. Entwickler von Adobe-Erweiterungen stellen sicher, dass ihre Erweiterungen wie vorgesehen funktionieren. Bei Drittanbieter-Erweiterungen stellt Adobe Erweiterungsentwicklern Informationen dazu bereit, wie sie dies ordnungsgemäß implementieren können. Die Verantwortung liegt jedoch bei den Entwicklern.

Adobe empfiehlt dringend, Ihre Regeln mit positiven Zahlen zwischen 1 und 100 zu sortieren (der Standardwert lautet 50). Denn einfacher ist immer besser. Denken Sie daran, dass die Reihenfolge eingehalten werden muss. Adobe berücksichtigt jedoch auch Sonderfälle, in denen hierdurch Einschränkungen auftreten. Deshalb sind auch andere Zahlen zulässig. Tags unterstützen Zahlen zwischen +/- 2.147.483.648. Sie können auch ca. ein Dutzend Dezimalstellen verwenden. Wenn Sie sich jedoch in einem Szenario befinden, in dem dies nötig ist, sollten Sie einige der Entscheidungen überdenken, die Sie bis zu diesem Punkt getroffen haben.

>[!IMPORTANT]
>
>Im Aktionsabschnitt einer Regel werden Server-seitige Regeln nacheinander ausgeführt. Achten Sie beim Erstellen der Regel auf die richtige Reihenfolge.

### Szenarios

* Fünf Regeln teilen sich ein Ereignis. Alle haben Standardpriorität. Ich möchte, dass eine der Regeln zuletzt ausgeführt wird. Ich muss nur diese eine Regelkomponente bearbeiten und ihr eine Zahl über 50 (z. B. 60) zuweisen.
* Fünf Regeln teilen sich ein Ereignis. Alle haben Standardpriorität. Ich möchte, dass eine der Regeln zuerst ausgeführt wird. Ich muss nur diese eine Regelkomponente bearbeiten und ihr eine Zahl unter 50 (z. B. 40) zuweisen.

### Client-seitige Regelverarbeitung

Die Ladereihenfolge für Regeln hängt davon ab, ob die Regelaktion mit JavaScript, HTML oder anderem Client-seitigem Code konfiguriert wurde und ob die Regeln das Ereignis „Seitenende“ oder „Seitenanfang“ verwenden.

Sie können `document.write` in Ihren benutzerdefinierten Skripten unabhängig von den für die Regel konfigurierten Ereignissen verwenden.

Sie können verschiedene benutzerdefinierte Codetypen untereinander sortieren. Zum Beispiel können Sie nun eine Aktion vom Typ „Benutzerspezifischer Code“ für JavaScript, dann eine für HTML und anschließend wieder eine für JavaScript verwenden. Tags stellen sicher, dass sie in dieser Reihenfolge ausgeführt werden.

## Regelbündelung

Regelereignisse und -bedingungen werden immer in der Haupt-Tag-Bibliothek gebündelt. Aktionen können in der Hauptbibliothek gebündelt oder bei Bedarf später als Unterressourcen geladen werden. Anhand des Ereignistyps der Regel wird entschieden, ob die Aktionen gebündelt werden.

### Regeln mit Ereignissen vom Typ „Core - Bibliothek geladen“ oder „Core - Seitenanfang“

Diese Ereignisse müssen fast immer ausgeführt werden (es sei denn, die Bedingungen werden nicht erfüllt). Aus Effizienzgründen werden sie in der Hauptbibliothek (der Datei, auf die Ihr Einbettungscode verweist.) gebündelt.

* **JavaScript:** Das JavaScript ist in die Haupt-Tag-Bibliothek eingebettet. Das benutzerdefinierte Skript wird in ein Skript-Tag eingeschlossen und über `document.write` in das Dokument geschrieben. Wenn die Regel mehrere benutzerdefinierte Skripte enthält, werden sie der Reihe nach geschrieben.

   >[!NOTE]
   >
   >Tags verwenden ES5-JavaScript. Die Ereignisweiterleitung verwendet ES6.

* **HTML:** Der HTML-Code ist in die Haupt-Tag-Bibliothek eingebettet. `document.write` wird zum Schreiben des HTML-Codes in das Dokument verwendet. Wenn die Regel mehrere benutzerdefinierte Skripte enthält, werden sie der Reihe nach geschrieben.

### Regeln mit anderen Ereignissen

Adobe kann nicht garantieren, dass andere Regeln tatsächlich ausgelöst werden und ihr Aktionscode benötigt wird. Aus diesem Grund werden die Aktionen für alle Ereignistypen, die oben nicht aufgeführt sind, nicht in der Hauptbibliothek zusammengefasst. Stattdessen werden sie als Unterressourcen gespeichert und von der Hauptbibliothek nach Bedarf referenziert.

* **JavaScript:** Das JavaScript-Skript wird vom Server als normaler Text geladen, in ein Skript-Tag eingeschlossen und mit Postscribe dem Dokument hinzugefügt. Wenn die Regel mehrere benutzerdefinierte JavaScript-Skripte enthält, werden diese parallel vom Server geladen, aber in der Reihenfolge ausgeführt, die in der Regel konfiguriert wurde.
* **HTML:** Der HTML-Code wird vom Server geladen und mit Postscribe zum Dokument hinzugefügt. Wenn die Regel mehrere benutzerdefinierte HTML-Skripte enthält, werden diese parallel vom Server geladen, aber in der Reihenfolge ausgeführt, die in der Regel konfiguriert wurde.

## Sequenzierung von Regelkomponenten {#sequencing}

Das Verhalten der Tag-Laufzeitumgebung hängt davon ab, ob die Option **[!UICONTROL Regelkomponenten in der Sequenz ausführen]** für Ihre Eigenschaft aktiviert oder deaktiviert ist.

### Aktiviert

Wenn diese Option aktiviert ist, werden beim Auslösen eines Ereignisses zur Laufzeit die Regelbedingungen und -aktionen einer Verarbeitungswarteschlange hinzugefügt – basierend auf der von Ihnen definierten Reihenfolge – und nacheinander auf FIFO-Basis verarbeitet. Das Tag wartet auf den Abschluss der Komponente, bevor es zur nächsten Komponente wechselt.

Wenn eine Bedingung nicht erfüllt wird oder ihre definierte Zeitüberschreitung erreicht, werden die nachfolgenden Bedingungen und Aktionen dieser Regel aus der Warteschlange entfernt.

Wenn eine Aktion fehlschlägt oder ihre definierte Zeitüberschreitung erreicht, werden die nachfolgenden Aktionen dieser Regel aus der Warteschlange entfernt.

>[!NOTE]
>
>Wenn diese Einstellung aktiviert ist, werden alle Bedingungen und Aktionen asynchron ausgeführt, auch wenn Sie die Tag-Bibliothek synchron geladen haben.

### Deaktiviert

Wenn diese Option deaktiviert ist und ein Ereignis zur Laufzeit ausgelöst wird, werden die Regelbedingungen sofort ausgewertet. Mehrere Bedingungen werden parallel ausgewertet.

Wenn alle Bedingungen erfüllt (und die Ausnahmen nicht erfüllt) sind, werden die Aktionen der Regel sofort ausgeführt. Die Aktionen werden der Reihe nach aufgerufen. Tags warten jedoch nicht darauf, dass eine Aktion abgeschlossen ist, bevor die nächste aufgerufen wird. Wenn Ihre Aktionen synchron sind, werden sie weiterhin in der richtigen Reihenfolge ausgeführt. Wenn eine oder mehrere Aktionen asynchron sind, werden einige Aktionen parallel ausgeführt.
