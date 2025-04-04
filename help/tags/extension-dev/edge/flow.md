---
title: Edge-Erweiterungsfluss
description: Erfahren Sie, wie die Komponenten einer Edge-Erweiterung in Adobe Experience Platform zur Laufzeit miteinander interagieren.
exl-id: 99058e22-3e14-4ec6-858e-bb1c1fafdb7c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 85%

---

# Edge-Erweiterungsfluss

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

In Edge-Erweiterungen verfügt jede Bedingung, jede Aktion und jeder Datenelementtyp über eine Ansicht, die den Benutzern das Ändern von Einstellungen ermöglicht, und über ein Bibliotheksmodul, in dem diese benutzerdefinierten Einstellungen verwendet werden.

Wie das folgende Übersichtsdiagramm zeigt, wird die Aktionstypansicht der Erweiterung in einem iframe innerhalb des in Adobe Experience Platform integrierten Programms angezeigt. Die Ansicht wird dann verwendet, um Einstellungen zu ändern, die dann in Experience Platform gespeichert werden. Beim Erstellen der Tag-Laufzeitbibliothek werden sowohl das Aktionstyp-Bibliotheksmodul der Erweiterung als auch die benutzerdefinierten Einstellungen in die Laufzeitbibliothek aufgenommen, die auf dem Edge-Knoten bereitgestellt wird. Benutzerdefinierte Einstellungen aus Experience Platform werden zur Laufzeit in das Bibliotheksmodul eingefügt.

![Flussdiagramm der Erweiterung](../images/flow/edge/event-processing-flow.png)

Im folgenden Diagramm sehen Sie die Verknüpfung zwischen Ereignissen, Bedingungen und Aktionen innerhalb des Regelverarbeitungsablaufs.

![Flussdiagramm der Regelverarbeitung](../images/flow/edge/rule-processing-flow.png)

Der Regelverarbeitungsablauf umfasst die folgenden Phasen:

1. Die Methoden `settings` und `trigger` werden dem Ereignisbibliotheksmodul beim Start zur Verfügung gestellt.
1. Wenn das Ereignisbibliotheksmodul feststellt, dass das Ereignis aufgetreten ist, ruft es die Methode `trigger` auf.
1. Experience Platform übergibt `settings` an die Bedingungstyp-Bibliotheksmodule der Regel, in denen Bedingungen ausgewertet werden.
1. Jeder Bedingungstyp gibt zurück, ob eine Bedingung als „true“ ausgewertet wird.
1. Wenn alle Bedingungen erfüllt sind, werden die Aktionen der Regel ausgeführt.
