---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei Sandboxen
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: f15049ca917818d325b5783c70faaa53ba669aba
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---


# Handbuch zur Fehlerbehebung bei Sandboxen

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Sandboxen in Adobe Experience Platform. Fragen und Fehlerbehebung zu anderen Plattformdiensten finden Sie im Handbuch [Experience Platform zur Fehlerbehebung](../landing/troubleshooting.md).

Sandboxes unterteilen eine einzelne Plattform-Instanz in separate virtuelle Umgebung, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln. See the [sandboxes overview](home.md) for more information.

## Was ist eine Sandbox?

Sandboxen sind virtuelle Partitionen innerhalb einer Instanz von Experience Platform. Jede Sandbox unterhält eine eigene, unabhängige Bibliothek mit Plattformressourcen (einschließlich Schemas, Datensätzen, Profilen usw.). Alle Inhalte und Aktionen, die innerhalb einer Sandbox durchgeführt werden, sind auf diese Sandbox beschränkt und wirken sich nicht auf andere Sandboxen aus. See the [sandboxes overview](home.md) for more information.

## Welche Arten von Sandboxen sind verfügbar und wie unterscheiden sie sich?

In Experience Platform stehen zwei Sandbox-Typen zur Verfügung:

* Produktions-Sandbox
* Sandbox ohne Produktion

Experience Platform bietet eine einzige **Produktions-Sandbox**, die weder gelöscht noch zurückgesetzt werden kann. Es kann nur eine Produktions-Sandbox für eine einzige Plattforminstanz vorhanden sein.

Im Gegensatz dazu können mehrere **Nicht-Produktions-Sandboxen** von Sandbox-Administratoren für eine einzige Plattforminstanz erstellt werden. Mit Sandboxen ohne Produktionsumfang können Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen, ohne die Produktionssandbox zu beeinträchtigen. Darüber hinaus verfügen Sandboxen, die keine Produktion sind, über eine Reset-Funktion, mit der alle vom Kunden erstellten Ressourcen aus der Sandbox entfernt werden. Nicht-produzierende Sandboxen können nicht in Produktions-Sandboxen konvertiert werden.

See the [sandboxes overview](./home.md) for more information.

## Kann ich von mehr als einer Sandbox auf eine Ressource zugreifen?

Sandboxen sind isolierte Partitionen einer einzelnen Plattform-Instanz, wobei jede Sandbox ihre eigene unabhängige Ressourcenbibliothek unterhält. Eine Ressource, die in einer Sandbox vorhanden ist, kann unabhängig vom Sandbox-Typ (Produktion oder Nicht-Produktion) nicht von einer anderen Sandbox aus aufgerufen werden.

## Wie viele Produktionssandboxen kann ich haben?

Experience Platform unterstützt nur eine Produktions-Sandbox pro IMS-Organisation, die standardmäßig bereitgestellt wird. Die Produktions-Sandbox kann zwar umbenannt werden, kann aber nicht gelöscht oder zurückgesetzt werden. Benutzer mit Sandbox-Administratorberechtigungen können nur Sandboxen ohne Produktionscharakter erstellen, zurücksetzen und löschen.

## Wie viele Sandboxen ohne Produktion kann ich haben?

Die Experience Platform erlaubt derzeit bis zu 15 nicht produktive Sandboxen, in einer einzigen IMS-Organisation aktiv zu sein.

## Ich habe gerade eine Sandbox erstellt. Wie stelle ich Berechtigungen für die Benutzer ein, die mit dieser Sandbox arbeiten werden?

Die Adobe Admin-Konsole verknüpft Benutzer mithilfe von **Profilen** mit Sandboxen und Berechtigungen. Nachdem Sie eine neue Sandbox erstellt haben, navigieren Sie zur Registerkarte &quot; _Berechtigungen_ &quot;des Profils, auf das Sie Zugriff gewähren möchten, und klicken Sie dann auf **Sandboxes**. Von hier aus können Sie den Zugriff auf die neue Sandbox auf dieselbe Weise wie andere Berechtigungen hinzufügen oder entfernen.

Wenn Sie Benutzern einer bestimmten Sandbox eindeutige Berechtigungen hinzufügen möchten, müssen Sie möglicherweise ein neues Profil mit den entsprechenden Sandboxen und Berechtigungen erstellen und diese Benutzer diesem Profil zuweisen.

Weitere Informationen zum Verwalten von Sandboxen und Berechtigungen in der Admin-Konsole finden Sie im Benutzerhandbuch für die [Zugriffskontrolle](../access-control/ui/overview.md) .