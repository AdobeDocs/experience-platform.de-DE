---
title: Veröffentlichungsübersicht
description: Erfahren Sie mehr über den Prozess der Veröffentlichung von Änderungen an Ihren Tag-Management-Codebibliotheken in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 77%

---

# Veröffentlichungsübersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Mit Adobe Experience Platform können Sie Änderungen am Tag Management Code in einzelnen Bibliotheken kapseln. Da jetzt mehrere Bibliotheken parallel von verschiedenen Teams entwickelt werden können, müssen diese Bibliotheken einen vorsätzlichen Prozess mit Berechtigungen zum Zusammenführen von Änderungen durchführen, bevor sie in Ihre Produktionsumgebung verschoben werden.

Im Grunde genommen durchläuft jede Bibliothek den folgenden Veröffentlichungsprozess:

1. Erstellen einer neuen Bibliothek (oder Bearbeiten einer vorhandenen Bibliothek) in einer Entwicklungsumgebung.
1. Testen der Bibliotheksfunktionalität in einer Staging-Umgebung, falls erforderlich.
1. Bereitstellen der Bibliothek in der Produktionsumgebung.

Angenommen, Sie erstellen ein neues Ereignis „Checkout“ und ein Umsatzdatenelement für dieses Ereignis und ändern die Adobe Analytics-Erweiterungskonfiguration so, dass sie das neue Ereignis und das neue Datenelement unterstützt. Sie können alle diese Änderungen in eine neue Bibliothek aufnehmen und sie mithilfe des Veröffentlichungsvorgangs als eine Einheit testen, genehmigen und veröffentlichen.

Eine allgemeine Übersicht über den Workflow zum Veröffentlichen von Bibliotheken, einschließlich Informationen darüber, wie Bibliotheken Ressourcen von Upstreambuilds abhängig vom Veröffentlichungsstatus erben, finden Sie im Handbuch [Publishing-Ablauf](./publishing-flow.md).

Neben dem Publishing-Ablauf müssen Sie einige andere Komponenten und Beziehungen verstehen, um effektiv Bibliotheken entwickeln und veröffentlichen zu können. Die folgende Tabelle gibt einen Überblick über diese Schlüsselkonzepte und enthält Links zu Dokumentationen, die Ihnen helfen, mehr über jedes Konzept zu erfahren:

| Komponente | Beschreibung |
| --- | --- |
| Bibliotheken | Eine Bibliothek ist eine Reihe von Anweisungen dafür, wie Erweiterungen, Datenelemente und Regeln miteinander und mit Ihrer Website interagieren. Wenn eine Bibliothek für die Bereitstellung in einer Umgebung kompiliert wird, wird sie zu einem Build.<br><br>Weitere Informationen zum Erstellen, Verwalten und Aktivieren von Bibliotheken in der UI finden Sie in der Übersicht zu [Bibliotheken](./libraries.md). |
| Builds | Ein Build ist eine kompilierte Bibliothek. Wenn ein Build in einer Umgebung bereitgestellt wird, stellt er den eigentlichen Satz von Dateien bereit, der den Code enthält, der an den Browser jedes Benutzers geliefert wird, wenn dieser Ihre Website aufruft.<br><br>Weitere Informationen zu Inhalt und Format der Builds finden Sie in der Übersicht zu [Builds](./builds.md). |
| Umgebungen | Eine Tag-Umgebung ist eine Reihe von Implementierungsanweisungen, die Platform mitteilen, in welchem Format Sie Ihren Build einbauen möchten und wo dieser Build bereitgestellt werden soll.<br><br>Weitere Informationen zu den verschiedenen Umgebungstypen, zur Installation und Konfiguration vorhandener Umgebungen und zum Erstellen neuer Umgebungen finden Sie in der Übersicht zu [Umgebungen](./environments.md). |
| Hosts | Ein Host stellt die Verbindungsdetails für eine Umgebung dar, die einen Build für Ihre Website bereitstellen soll. Sie können festlegen, dass Adobe das Hosting Ihres Builds verwaltet, oder Informationen für Ihre eigenen Hostserver bereitstellen.<br><br>Weitere Informationen zu den einzelnen Hosting-Optionen finden Sie in der Übersicht zu [Hosts](./hosts/hosts-overview.md). |
| Client-seitiger Code | Der Client-seitige Code ist der Satz von Skripten, den Sie im Quell-Code Ihrer Site oder Anwendung platzieren und der jedem Client-Gerät mitteilt, wo der Build abgerufen werden soll. Der Code wird an eine Umgebung angehängt und kann sich ändern, wenn Sie Ihre Umgebungskonfiguration ändern.<br><br>Weitere Informationen finden Sie im Abschnitt  [Einbettungscodes in der Übersicht ](./environments.md#embed-code) zu Umgebungen . |

## Nächste Schritte

Dieses Dokument bietet einen Überblick über die verschiedenen Komponenten, die mit der Veröffentlichung von Tag-Bibliotheken in Adobe Experience Platform verbunden sind. Lesen Sie die Dokumentation, auf die in diesem Handbuch verwiesen wird, um weitere Informationen zum Veröffentlichungsprozess im Detail zu erhalten.
