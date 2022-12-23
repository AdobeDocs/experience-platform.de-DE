---
title: Regeln
description: Machen Sie sich mit der Funktionsweise von Tag-Erweiterungen in Adobe Experience Platform vertraut.
exl-id: 2beca2c9-72b7-4ea0-a166-50a3b8edb9cd
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: ht
source-wordcount: '1973'
ht-degree: 100%

---

# Regeln

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

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

Die verfügbaren Ereignisse hängen davon ab, welche Erweiterungen installiert wurden. Informationen zu den Ereignissen in der Haupterweiterung finden Sie unter [Ereignistypen der Haupterweiterung](../../extensions/client/core/overview.md#core-extension-event-types).

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

Mit der Regelreihenfolge können Sie die Reihenfolge der Ausführung von Regeln steuern, die ein Ereignis gemeinsam haben. Jede Regel enthält eine Ganzzahl, die ihre Priorität in der Reihenfolge bestimmt (der Standardwert ist 50). Regeln, die niedrigere Werte für ihre Reihenfolge enthalten, werden vor Regeln mit höheren Werten ausgeführt.

Im Folgenden sehen Sie einen Satz von fünf Regeln, die alle ein Ereignis gemeinsam haben und alle Standardpriorität besitzen:

* Wenn es eine Regel gibt, die Sie als letzte ausführen möchten, können Sie diese Regelkomponente bearbeiten und ihr eine Zahl über 50 (z. B. 60) zuweisen.
* Wenn es eine Regel gibt, die Sie als erste ausführen möchten, können Sie diese Regelkomponente bearbeiten und ihr eine Zahl unter 50 (z. B. 40) zuweisen.

>[!NOTE]
>
>Letztendlich liegt die Verantwortung für die Ausführung von Aktionen in der richtigen Reihenfolge beim Entwickler der Erweiterung des Ereignistyps, den Sie verwenden. Entwickler von Adobe-Erweiterungen stellen sicher, dass ihre Erweiterungen wie vorgesehen funktionieren. Adobe bietet Entwicklern von Drittanbietererweiterungen Anleitungen, dies ordnungsgemäß zu tun, kann jedoch nicht garantieren, inwieweit diese Richtlinien befolgt werden.

Es wird dringend empfohlen, Ihre Regeln mit positiven Zahlen zwischen 1 und 100 zu sortieren (Standardwert 50). Da die Regelreihenfolge manuell gepflegt werden muss, ist es am besten, wenn Sie Ihr Ordnungsschema so einfach wie möglich halten. Sollte diese Einschränkung in bestimmten Grenzfällen zu stark sein, unterstützen die Tags Regelordnungsnummern zwischen +/- 2.147.483.648.

### Client-seitige Regelverarbeitung

Die Ladereihenfolge für Regeln hängt davon ab, ob die Regelaktion mit JavaScript, HTML oder anderem Client-seitigem Code konfiguriert wurde und ob die Regeln das Ereignis „Seitenende“ oder „Seitenanfang“ verwenden.

Sie können `document.write` in Ihren benutzerdefinierten Skripten unabhängig von den für die Regel konfigurierten Ereignissen verwenden.

Sie können verschiedene benutzerdefinierte Codetypen untereinander sortieren. Zum Beispiel können Sie nun eine Aktion vom Typ „Benutzerspezifischer Code“ für JavaScript, dann eine für HTML und anschließend wieder eine für JavaScript verwenden. Tags stellen sicher, dass sie in dieser Reihenfolge ausgeführt werden.

## Regelbündelung

Regelereignisse und -bedingungen werden immer in der Haupt-Tag-Bibliothek gebündelt. Aktionen können in der Hauptbibliothek gebündelt oder bei Bedarf später als Unterressourcen geladen werden. Anhand des Ereignistyps der Regel wird entschieden, ob die Aktionen gebündelt werden.

### Regeln mit Ereignissen vom Typ „Core - Bibliothek geladen“ oder „Core - Seitenanfang“

Diese Ereignisse müssen fast immer ausgeführt werden (es sei denn, die Bedingungen werden nicht erfüllt). Aus Effizienzgründen werden sie in der Hauptbibliothek (der Datei, auf die Ihr Einbettungscode verweist.) gebündelt.

* **JavaScript:** Das JavaScript ist in die Haupt-Tag-Bibliothek eingebettet. Das benutzerdefinierte Skript wird in ein Skript-Tag eingeschlossen und über `document.write` in das Dokument geschrieben. Wenn die Regel mehrere benutzerdefinierte Skripte enthält, werden sie der Reihe nach geschrieben.

* **HTML:** Der HTML-Code ist in die Haupt-Tag-Bibliothek eingebettet. `document.write` wird zum Schreiben des HTML-Codes in das Dokument verwendet. Wenn die Regel mehrere benutzerdefinierte Skripte enthält, werden sie der Reihe nach geschrieben.

### Regeln mit anderen Ereignissen

Adobe kann nicht garantieren, dass andere Regeln tatsächlich ausgelöst werden und ihr Aktionscode benötigt wird. Aus diesem Grund werden die Aktionen für alle Ereignistypen, die oben nicht aufgeführt sind, nicht in der Hauptbibliothek zusammengefasst. Stattdessen werden sie als Unterressourcen gespeichert und von der Hauptbibliothek nach Bedarf referenziert.

* **JavaScript:** Das JavaScript-Skript wird vom Server als normaler Text geladen, in ein Skript-Tag eingeschlossen und mit Postscribe dem Dokument hinzugefügt. Wenn die Regel mehrere benutzerdefinierte JavaScript-Skripte enthält, werden diese parallel vom Server geladen, aber in der Reihenfolge ausgeführt, die in der Regel konfiguriert wurde.
* **HTML:** Der HTML-Code wird vom Server geladen und mit Postscribe zum Dokument hinzugefügt. Wenn die Regel mehrere benutzerdefinierte HTML-Skripte enthält, werden diese parallel vom Server geladen, aber in der Reihenfolge ausgeführt, die in der Regel konfiguriert wurde.

## Sequenzierung von Regelkomponenten {#sequencing}

Das Verhalten der Laufzeitumgebung hängt davon ab, ob die Option **[!UICONTROL Regelkomponenten nacheinander ausführen]** für Ihre Eigenschaft aktiviert oder deaktiviert ist. Diese Einstellung bestimmt, ob die Komponenten einer Regel parallel (asynchron) ausgewertet werden können oder ob sie nacheinander ausgewertet werden müssen.

>[!IMPORTANT]
>
>Diese Einstellung bestimmt nur, wie Bedingungen und Aktionen innerhalb der einzelnen Regeln ausgewertet werden, und beeinflusst nicht die Reihenfolge, in der die Regeln selbst für Ihre Eigenschaft ausgeführt werden. Siehe vorherigen Abschnitt unter [Regelreihenfolge](#rule-ordering) für weitere Informationen zur Bestimmung der Ausführungsreihenfolge für mehrere Regeln.
>
>In den [Ereignisweiterleitungs](../event-forwarding/overview.md)-Eigenschaften werden Regelaktionen immer nacheinander ausgeführt, und diese Einstellung ist nicht verfügbar. Achten Sie beim Erstellen der Regel auf die richtige Reihenfolge.

### Aktiviert

Wenn die Einstellung aktiviert ist, wenn ein Ereignis zur Laufzeit ausgelöst wird, werden die Bedingungen und Aktionen der Regel einer Verarbeitungswarteschlange hinzugefügt (basierend auf der von Ihnen definierten Reihenfolge) und nacheinander nach dem Prinzip „first in, first out“ (FIFO) verarbeitet. Die Regel wartet auf den Abschluss der Komponente, bevor sie zur nächsten Komponente übergeht.

Wenn eine Bedingung nicht erfüllt wird oder ihre definierte Zeitüberschreitung erreicht, werden die nachfolgenden Bedingungen und Aktionen dieser Regel aus der Warteschlange entfernt.

Wenn eine Aktion fehlschlägt oder ihre definierte Zeitüberschreitung erreicht, werden die nachfolgenden Aktionen dieser Regel aus der Warteschlange entfernt.

### Deaktiviert

Wenn diese Option deaktiviert ist und ein Ereignis zur Laufzeit ausgelöst wird, werden die Regelbedingungen sofort ausgewertet. Mehrere Bedingungen werden parallel ausgewertet.

Wenn alle Bedingungen erfüllt (und die Ausnahmen nicht erfüllt) sind, werden die Aktionen der Regel sofort ausgeführt. Die Aktionen werden der Reihe nach aufgerufen. Tags warten jedoch nicht darauf, dass eine Aktion abgeschlossen ist, bevor die nächste aufgerufen wird. Wenn Ihre Aktionen synchron sind, werden sie weiterhin in der richtigen Reihenfolge ausgeführt. Wenn eine oder mehrere Aktionen asynchron sind, werden einige Aktionen parallel ausgeführt.
