---
title: Handbuch zur Reactor-API
description: Mit der Reactor-API können Entwickler alle Ressourcen für Tags in Adobe Experience Platform programmgesteuert verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: 153eab11-db08-499e-80d1-c56f254372ce
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 100%

---

# [!DNL Reactor]-API-Handbuch

Die Reactor-API bietet mehrere Endpunkte, mit denen Sie alle Ressourcen für Tags in Adobe Experience Platform programmgesteuert verwalten können.

Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zur Authentifizierung bei der API finden Sie in den Handbüchern zu den einzelnen Endpunkten und im [Erste Schritte-Handbuch](./getting-started.md).

Um alle verfügbaren Endpunkte und CRUD-Vorgänge anzuzeigen, konsultieren Sie die [Reactor API-Referenz](https://www.adobe.io/experience-platform-apis/references/reactor/).

## Firmen

Ein Unternehmen stellt die Organisation eines Tags-Benutzers dar, normalerweise eine Firma. Diese Unternehmen stimmen 1:1 mit den IMS-Organisations-IDs überein. API-Benutzer haben nur Einblick in die Unternehmen, auf die sie Zugriff haben.

Informationen zum Anzeigen verfügbarer Unternehmen in der API finden Sie im [Handbuch zum companies-Endpunkt](./endpoints/companies.md).

## Eigenschaften

Eine Eigenschaft ist ein Container, der die meisten anderen Ressourcen enthält, die in der Reactor-API verfügbar sind. Die einzigen Ressourcen, die keiner Eigenschaft gehören, sind Audit-Ereignisse, Unternehmen, Erweiterungspakete und Profile. Eine Eigenschaft gehört zu genau einem Unternehmen und ein Unternehmen kann über viele Eigenschaften verfügen.

Informationen zum Verwalten von Eigenschaften in der API finden Sie im [Handbuch zum properties-Endpunkt](./endpoints/properties.md).

## Datenelemente

Ein Datenelement fungiert als Variable, die auf wichtige Daten innerhalb Ihres Programms verweist. Datenelemente werden in Regeln und Erweiterungskonfigurationen verwendet. Wenn die Regel zur Laufzeit in einem Browser oder einem Programm ausgelöst wird, wird der Wert des Datenelements aufgelöst und innerhalb der Regel verwendet.

Informationen zum Verwalten von Datenelementen in der API finden Sie im [Handbuch zu data elements-Endpunkt](./endpoints/data-elements.md).

## Regeln

Regeln steuern das Verhalten der Ressourcen, die in einer bereitgestellten Bibliothek enthalten sind. Eine Regel ist eine Gruppe aus einer oder mehreren Regelkomponenten, die dazu dient, die Regelkomponenten logisch miteinander zu verbinden.

Informationen zum Verwalten von Regeln in der API finden Sie im [Handbuch zum rules-Endpunkt](./endpoints/rules.md).

## Regel Komponenten

Regelkomponenten sind die einzelnen Elemente, aus denen eine Regel besteht. Regelkomponenten haben drei grundlegende Typen:

* **Ereignisse**: Wodurch eine Regel ausgelöst wird
* **Bedingungen**: Was von der Regel überprüft wird, um eine Aktion zu bestimmen
* **Aktionen**: Was von der Regel abhängig davon ausgeführt wird, ob die Bedingung erfüllt ist

Informationen zum Verwalten von Regeln in der API finden Sie im [Handbuch zum rules-Endpunkt](./endpoints/rules.md).

## Erweiterungspakete

Ein Erweiterungspaket stellt eine Gruppierung einzelner Funktionen dar, die einem Tag-Benutzer zur Verfügung gestellt werden können. Diese Funktionen werden meist in Form von Regelkomponenten und Datenelementen bereitgestellt, können aber auch Hauptmodule und gemeinsame Module enthalten. Die von einem Erweiterungspaket bereitgestellten Funktionen werden als Erweiterung installiert, wenn es in einer Bibliothek enthalten ist.

Informationen zum Verwalten von Erweiterungspaketen in der API finden Sie im [Handbuch zum extension packages-Endpunkt](./endpoints/extension-packages.md).

## Erweiterungen

Eine Erweiterung stellt die installierte Instanz eines Erweiterungspakets dar. Eine Erweiterung stellt die durch ein Erweiterungspaket definierten Funktionen für eine Eigenschaft zur Verfügung. Diese Funktionen werden beim Erstellen von Datenelementen und Regelkomponenten genutzt.

Informationen zum Verwalten von Erweiterungen in der API finden Sie im [Handbuch zum extensions-Endpunkt](./endpoints/extensions.md).

## Bibliotheken

Eine Bibliothek ist eine Sammlung von Ressourcen (Erweiterungen, Regeln und Datenelemente), die das gewünschte Verhalten einer Eigenschaft darstellen. Bibliotheken werden in Builds kompiliert und diese Builds werden verschiedenen Umgebungen zugewiesen, während sie sich im Veröffentlichungsablauf von Tests zur Produktion bewegen.

Informationen zum Verwalten von Bibliotheken in der API finden Sie im [Handbuch zum libraries-Endpunkt](./endpoints/libraries.md).

## Builds

Eine Tag-Bibliothek wird in einen Build kompiliert, damit sie einer Umgebung zum Testen und zur Implementierung zugewiesen werden kann. Der Inhalt eines Builds variiert je nach den in der Bibliothek enthaltenen Ressourcen, der Konfiguration der Umgebung, der der Build zugewiesen ist, und der Plattform der Eigenschaft, zu der der Build gehört.

Informationen zum Verwalten von Builds in der API finden Sie im [Handbuch zum builds-Endpunkt](./endpoints/builds.md).

## Umgebungen

Eine Umgebung gibt den spezifischen Host an, auf dem ein Build bereitgestellt werden kann, und ob der Build als Dateisatz bereitgestellt oder in einem Archivformat komprimiert werden soll. In der Reactor-API sind Umgebungen getrennt von den Hosts selbst, die vom `/hosts`-Endpunkt verwaltet werden.

Informationen zum Verwalten von Builds in der API finden Sie im [Handbuch zum builds-Endpunkt](./endpoints/builds.md).

## Hosts

Ein Host stellt ein gehostetes Ziel dar, in dem ein Bibliotheks-Build bereitgestellt und letztendlich implementiert werden kann. Hosts können entweder Akamai- oder SFTP-Server sein.

Informationen zum Verwalten von Hosts in der API finden Sie im [Handbuch zum hosts-Endpunkt](./endpoints/hosts.md).

## Programmkonfigurationen

App-Konfigurationen ermöglichen das Speichern und Abrufen von Anmeldeinformationen zur späteren Verwendung. Informationen zum Verwalten von App-Konfigurationen in der API finden Sie im [Handbuch zum app configurations-Endpunkt](./endpoints/app-configurations.md).

## Audit-Ereignisse

Ein Prüfereignis ist ein Datensatz einer bestimmten Änderung an einer anderen Tag-Ressource, der zum Zeitpunkt der Änderung generiert wird. Dies sind Systemereignisse, die über eine Callback-Funktion abonniert werden können.

Informationen zum Verwalten von Audit-Ereignissen in der API finden Sie im [Handbuch zum audit events-Endpunkt](./endpoints/audit-events.md).

## Callbacks

Ein Callback ist eine Nachricht, die Platform bei der Erstellung eines neuen Audit-Ereignisses an einen URL-Host sendet. Informationen zum Verwalten von Callbacks in der API finden Sie im [Handbuch zum callbacks-Endpunkt](./endpoints/callbacks.md).

## Anmerkungen

Anmerkungen sind Kommentare in Textform, die Sie bestimmten Tag-Ressourcen hinzufügen können, z. B. Datenelementen, Erweiterungen, Bibliotheken, Eigenschaften, Regeln und Regelkomponenten. Informationen zum Verwalten von Notizen in der API finden Sie im [Handbuch zum notes-Endpunkt](./endpoints/notes.md).

## Profil

Ein Profil enthält alle Informationen zum angemeldeten Benutzer, einschließlich aller Adobe-Organisationen, denen er angehört, der Produktprofile, denen er in jeder Organisation angehört, und der Rechte, die ihm aus jedem Produktprofil zugewiesen sind.

Weitere Informationen zum Anzeigen dieser Informationen in der API finden Sie im [Handbuch zum profile-Endpunkt](./endpoints/profile.md).

## Durchsuchen

Der `/search`-Endpunkt bietet eine Möglichkeit, Ressourcen zu finden, die den gewünschten Kriterien entsprechen und als Abfrage ausgedrückt werden. Alle Abfragen beziehen sich auf Ihr aktuelles Unternehmen und auf verfügbare Eigenschaften. Weitere Informationen zur Verwendung dieser Funktion finden Sie im [Handbuch zum search-Endpunkt](./endpoints/search.md).

## Geheime Daten

Geheime Daten enthalten Anmeldeinformationen, mit denen sich die Ereignisweiterleitung für einen sicheren Datenaustausch bei einem anderen System authentifizieren kann. Im [Handbuch zu geheimen Daten](./guides/secrets.md) finden Sie einen Überblick darüber, wie geheime Daten in der Ereignisweiterleitung funktionieren. Zudem erhalten Sie im [Endpunktleitfaden für geheime Daten](./endpoints/secrets.md) weitere Informationen darüber, wie Sie geheime Daten in der Reactor-API verwalten.

## Nächste Schritte

Um mit der Durchführung von Aufrufen mit der Schema Registry API zu beginnen, lesen Sie das [Erste-Schritte-Handbuch](./getting-started.md) und wählen Sie dann eines der Endpunkt-Handbücher aus, um zu erfahren, wie Sie bestimmte Endpunkte verwenden.
