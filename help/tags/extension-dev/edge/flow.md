---
title: Edge-Erweiterungsfluss
description: Erfahren Sie, wie die Komponenten einer Edge-Erweiterung in Adobe Experience Platform zur Laufzeit miteinander interagieren.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 58%

---

# Edge-Erweiterungsfluss

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

In Edge-Erweiterungen verfügt jede Bedingung, jede Aktion und jeder Datenelementtyp über eine Ansicht, die den Benutzern das Ändern von Einstellungen ermöglicht, und über ein Bibliotheksmodul, in dem diese benutzerdefinierten Einstellungen verwendet werden.

Wie das folgende allgemeine Diagramm zeigt, wird die Aktionstypansicht der Erweiterung in einem iframe innerhalb der in Adobe Experience Platform integrierten Anwendung angezeigt. Die Ansicht wird dann verwendet, um Einstellungen zu ändern, die dann in Platform gespeichert werden. Wenn die Tag-Laufzeitbibliothek erstellt wird, werden sowohl das Aktionstyp-Bibliotheksmodul der Erweiterung als auch die benutzerdefinierten Einstellungen in die Laufzeitbibliothek aufgenommen, die auf dem Edge-Knoten bereitgestellt wird. Benutzerdefinierte Einstellungen von Platform werden zur Laufzeit in das Bibliotheksmodul eingefügt.

![Flussdiagramm der Erweiterung](../images/flow/edge/event-processing-flow.png)

Im folgenden Diagramm sehen Sie die Verknüpfung zwischen Ereignissen, Bedingungen und Aktionen innerhalb des Regelverarbeitungsablaufs.

![Flussdiagramm der Regelverarbeitung](../images/flow/edge/rule-processing-flow.png)

Der Regelverarbeitungsablauf umfasst die folgenden Phasen:

1. Die Methoden `settings` und `trigger` werden dem Ereignisbibliotheksmodul beim Start zur Verfügung gestellt.
1. Wenn das Ereignisbibliotheksmodul feststellt, dass das Ereignis aufgetreten ist, ruft es die Methode `trigger` auf.
1. Platform übergibt `settings` an die Bedingungstyp-Bibliotheksmodule der Regel, in denen Bedingungen ausgewertet werden.
1. Jeder Bedingungstyp gibt zurück, ob eine Bedingung „true“ ergibt.
1. Wenn alle Bedingungen erfüllt sind, werden die Aktionen der Regel ausgeführt.
