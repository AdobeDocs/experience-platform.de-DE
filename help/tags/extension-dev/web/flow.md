---
title: Web-Erweiterungsfluss
description: Hier erfahren Sie, wie Web-Erweiterungskomponenten in Adobe Experience Platform zur Laufzeit miteinander interagieren.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: ht
source-wordcount: '270'
ht-degree: 100%

---

# Web-Erweiterungsfluss

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere Terminologieänderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Wie bereits beschrieben, verfügt in Web-Erweiterungen jedes Ereignis, jede Bedingung, jede Aktion und jeder Datenelementtyp über eine Ansicht, die den Benutzern das Ändern von Einstellungen ermöglicht, und über ein Bibliotheksmodul, in dem diese benutzerdefinierten Einstellungen verwendet werden.

Wie das folgende Übersichtsdiagramm zeigt, wird die Ereignistypansicht der Erweiterung in einem iframe innerhalb des in Adobe Experience Platform integrierten Programms angezeigt. Der Benutzer verwendet dann die Ansicht, um Einstellungen zu ändern, die dann innerhalb von Platform gespeichert werden. Beim Erstellen der Tag-Laufzeitbibliothek werden sowohl das Ereignistyp-Bibliotheksmodul der Erweiterung als auch die benutzerdefinierten Einstellungen in die Laufzeitbibliothek aufgenommen. Zur Laufzeit injiziert Platform die benutzerdefinierten Einstellungen in das Bibliotheksmodul.

![Flussdiagramm der Erweiterung](../images/flow/web/extension-flow.png)

Im folgenden Diagramm sehen Sie die Verknüpfung zwischen Ereignissen, Bedingungen und Aktionen innerhalb des Regelverarbeitungsablaufs.

![Flussdiagramm der Regelverarbeitung](../images/flow/web/rule-processing-flow.png)

Der Regelverarbeitungsablauf umfasst die folgenden Phasen:

1. Die Methoden `settings` und `trigger` werden dem Ereignisbibliotheksmodul beim Start zur Verfügung gestellt.
1. Wenn das Ereignisbibliotheksmodul feststellt, dass das Ereignis aufgetreten ist, ruft es die Methode `trigger` auf.
1. Tags übergibt `settings` an die Bedingungsbibliotheksmodule der Regel, in denen Bedingungen ausgewertet werden.
1. Jedes Bedingungsbibliotheksmodul gibt zurück, ob eine Bedingung „true“ ergibt.
1. Wenn alle Bedingungen erfüllt sind, werden die Aktionen der Regel ausgeführt.
