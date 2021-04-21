---
keywords: Experience Platform;Startseite;beliebte Themen;Sandbox-Fehlerbehebung
solution: Experience Platform
title: Sandboxen - Fehlerbehebungshandbuch
topic-legacy: troubleshooting guide
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Sandboxes in Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 90%

---

# Handbuch zur Fehlerbehebung bei Sandboxes

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Sandboxes in Adobe Experience Platform. Fragen und Fehlerbehebungen für andere Platform-Dienste finden Sie im [Handbuch zur Fehlerbehebung in Experience Platform](../landing/troubleshooting.md).

Sandboxes unterteilen eine einzelne Platform-Instanz in separate virtuelle Umgebungen, damit sich Programme für digitale Erlebnisse entwickeln und weiterentwickeln lassen. Weiterführende Informationen dazu finden Sie in der [Sandbox-Übersicht](home.md).

## Was ist eine Sandbox?

Sandboxes sind virtuelle Partitionen innerhalb einer einzelnen Instanz von Experience Platform. Jede Sandbox unterhält eine eigene, unabhängige Bibliothek mit Platform-Ressourcen (einschließlich Schemas, Datensätzen, Profilen usw.). Alle Inhalte und Aktionen, die innerhalb einer Sandbox ausgeführt werden, sind auf diese Sandbox beschränkt und wirken sich nicht auf andere Sandboxes aus. Weiterführende Informationen dazu finden Sie unter [Sandbox-Übersicht](home.md).

## Welche Arten von Sandboxes gibt es und wie unterscheiden sie sich?

In Experience Platform gibt es zwei Arten von Sandboxes:

* Produktions-Sandbox
* Nicht-Produktions-Sandboxes

Experience Platform stellt eine einzige Produktions-Sandbox bereit, die weder gelöscht noch zurückgesetzt werden kann. Es kann nur eine Produktions-Sandbox pro Platform-Instanz geben.

Im Gegensatz dazu können Sandbox-Administratoren verschiedene Nicht-Produktions-Sandboxes für eine Platform-Instanz erstellen. Mit Nicht-Produktions-Sandboxes können Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen, ohne die Produktions-Sandbox zu beeinträchtigen. Darüber hinaus verfügen Nicht-Produktions-Sandboxes über eine Funktion zum Zurücksetzen, mit der sich alle vom Kunden erstellten Ressourcen aus der Sandbox entfernen lassen. Nicht-Produktions-Sandboxes können nicht in Produktions-Sandboxes umgewandelt werden. Mit einer Standardlizenz für Experience Platformen erhalten Sie fünf Sandboxen (eine Produktion und vier Nicht-Produktion). Sie können Pakete von zehn Nicht-Produktions-Sandboxen bis zu maximal 75 Sandboxen hinzufügen. Für weitere Informationen wenden Sie sich bitte an Ihren IMS-Organisationsadministrator oder Ihren Vertriebsmitarbeiter für Adoben.

Weiterführende Informationen dazu finden Sie in der [Sandbox-Übersicht](./home.md).

## Kann ich von verschiedenen Sandboxes aus auf eine bestimmte Ressource zugreifen?

Sandboxes sind voneinander isolierte Partitionen einer einzelnen Platform-Instanz, wobei jede Sandbox eine eigene unabhängige Ressourcenbibliothek unterhält. Eine Ressource, die in einer Sandbox vorhanden ist, kann unabhängig vom Sandbox-Typ (Produktion oder Nicht-Produktion) nicht von einer anderen Sandbox aus aufgerufen werden.

## Wie viele Produktions-Sandboxes können wir nutzen?

Experience Platform unterstützt nur eine Produktions-Sandbox pro IMS-Organisation; sie wird standardmäßig bereitgestellt. Die Produktions-Sandbox kann umbenannt, nicht aber gelöscht oder zurückgesetzt werden. Benutzer mit Sandbox-Administratorberechtigungen können ausschließlich Nicht-Produktions-Sandboxes erstellen, zurücksetzen und löschen.

## Wie viele Nicht-Produktions-Sandboxes können wir nutzen?

Experience Platform unterstützt derzeit bis zu 15 Nicht-Produktions-Sandboxes, die in einer IMS-Organisation aktiv sein können.

## Ich habe gerade eine Sandbox eingerichtet. Wie lege ich Berechtigungen für Benutzer fest, die mit dieser Sandbox arbeiten sollen?

Adobe Admin Console verknüpft Benutzer über Profile mit Sandboxes und Berechtigungen. Nachdem Sie eine neue Sandbox erstellt haben, navigieren Sie zum Tab **Berechtigungen** des Produktprofils, dem Sie Zugriff gewähren möchten, und klicken Sie dann auf **Sandboxes**. Nun können Sie Zugriff auf die neue Sandbox genauso wie bei anderen Berechtigungen hinzufügen oder entfernen.

Wenn Sie Benutzern einer bestimmten Sandbox eindeutige Berechtigungen hinzufügen möchten, müssen Sie möglicherweise ein neues Produktprofil mit den jeweiligen Sandboxes und Berechtigungen erstellen und die gewünschten Benutzer diesem Profil zuordnen.

Weiterführende Informationen zum Verwalten von Sandboxes und Berechtigungen in der Admin Console finden Sie im [Benutzerhandbuch zur Zugriffskontrolle](../access-control/ui/overview.md).
