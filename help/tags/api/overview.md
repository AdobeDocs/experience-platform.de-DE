---
title: Reactor-API-Anleitung
description: Mit der Reactor-API können Entwickler alle Ressourcen für Tags in Adobe Experience Platform programmgesteuert verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 3%

---

# [!DNL Reactor]-API-Handbuch

Die Reactor-API bietet mehrere Endpunkte, mit denen Sie alle Ressourcen für Tags in Adobe Experience Platform programmgesteuert verwalten können.

Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zur Authentifizierung bei der API finden Sie in den einzelnen Endpunkthandbüchern und im [Erste Schritte-Handbuch](./getting-started.md) .

Um alle verfügbaren Endpunkte und CRUD-Vorgänge anzuzeigen, besuchen Sie die [Reactor-API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml).

## Firmen

Ein Unternehmen stellt die Organisation eines Tags-Benutzers dar, normalerweise ein Unternehmen. Diese Unternehmen stimmen 1:1 mit den IMS-Organisations-IDs überein. API-Benutzer haben nur Einblick in die Unternehmen, auf die sie Zugriff haben.

Informationen zum Anzeigen verfügbarer Unternehmen in der API finden Sie im [Endpoint-Handbuch ](./endpoints/companies.md) für Unternehmen .

## Eigenschaften

Eine Eigenschaft ist ein Container, der die meisten anderen Ressourcen enthält, die in der Reactor-API verfügbar sind. Die einzigen Ressourcen, die keiner Property gehören, sind Prüfereignisse, Unternehmen, Erweiterungspakete und Profile. Eine Eigenschaft gehört genau zu einem Unternehmen, und ein Unternehmen kann über viele Eigenschaften verfügen.

Informationen zum Verwalten von Eigenschaften in der API finden Sie im [Eigenschaften-Endpunkthandbuch](./endpoints/properties.md) .

## Datenelemente

Ein Datenelement dient als Variable, die auf ein wichtiges Datenelement in Ihrer Anwendung verweist. Datenelemente werden in Regeln und Erweiterungskonfigurationen verwendet. Wenn die Regel zur Laufzeit in einem Browser oder einer Anwendung ausgelöst wird, wird der Wert des Datenelements aufgelöst und innerhalb der Regel verwendet.

Informationen zum Verwalten von Datenelementen in der API finden Sie im [Endpoint-Handbuch zu Datenelementen](./endpoints/data-elements.md) .

## Regeln

Regeln steuern das Verhalten der Ressourcen, die in einer bereitgestellten Bibliothek enthalten sind. Eine Regel ist eine Gruppe aus einer oder mehreren Regelkomponenten und besteht, um die Regelkomponenten logisch miteinander zu verbinden.

Informationen zum Verwalten von Regeln in der API finden Sie im [Regel-Endpunkthandbuch](./endpoints/rules.md) .

## Regel Komponenten

Regelkomponenten sind die einzelnen Elemente, aus denen eine Regel besteht. Regelkomponenten haben drei grundlegende Typen:

* **Ereignisse**: Welche Trigger eine Regel hat
* **Bedingungen**: Was wird von der Regel überprüft, um eine Aktion zu bestimmen
* **Aktionen**: Welche Regel ausgeführt wird, hängt davon ab, ob die Bedingung erfüllt ist

Informationen zum Verwalten von Regeln in der API finden Sie im [Regel-Endpunkthandbuch](./endpoints/rules.md) .

## Erweiterungspakete

Ein Erweiterungspaket stellt eine Gruppierung einzelner Funktionen dar, die einem Tag-Benutzer zur Verfügung gestellt werden können. Diese Funktionen werden meist in Form von Regelkomponenten und Datenelementen bereitgestellt, können aber auch Hauptmodule und gemeinsame Module enthalten. Die von einem Erweiterungspaket bereitgestellten Funktionen werden als Erweiterung installiert, wenn es in einer Bibliothek enthalten ist.

Informationen zum Verwalten von Erweiterungspaketen in der API finden Sie im [Endpoint-Handbuch für Erweiterungspakete](./endpoints/extension-packages.md) .

## Erweiterungen

Eine Erweiterung stellt die installierte Instanz eines Erweiterungspakets dar. Eine Erweiterung stellt die durch ein Erweiterungspaket definierten Funktionen für eine Eigenschaft zur Verfügung. Diese Funktionen werden beim Erstellen von Datenelementen und Regelkomponenten genutzt.

Informationen zum Verwalten von Erweiterungen in der API finden Sie im [Endpoint-Handbuch](./endpoints/extensions.md) .

## Bibliotheken

Eine Bibliothek ist eine Sammlung von Ressourcen (Erweiterungen, Regeln und Datenelemente), die das gewünschte Verhalten einer Eigenschaft darstellen. Bibliotheken werden in Builds kompiliert und diese Builds werden verschiedenen Umgebungen zugewiesen, während sie den Veröffentlichungsfluss von Tests zu Produktion verkleinern.

Informationen zum Verwalten von Bibliotheken in der API finden Sie im [Bibliotheken-Endpoint-Handbuch](./endpoints/libraries.md) .

## Builds

Eine Tag-Bibliothek wird in einen Build kompiliert, damit sie einer Umgebung zum Testen und Bereitstellen zugewiesen wird. Der Inhalt eines Builds variiert je nach den in der Bibliothek enthaltenen Ressourcen, der Konfiguration der Umgebung, der der Build zugewiesen wird, und der Plattform der Eigenschaft, zu der der Build gehört.

Informationen zum Verwalten von Builds in der API finden Sie im [Builds-Endpunkthandbuch](./endpoints/builds.md) .

## Umgebungen

Eine Umgebung gibt den spezifischen Host an, auf dem ein Build bereitgestellt werden kann, und ob der Build als Dateisatz bereitgestellt oder in einem Archivformat komprimiert werden soll. In der Reactor-API sind Umgebungen getrennt von den Hosts selbst, die vom Endpunkt `/hosts` verwaltet werden.

Informationen zum Verwalten von Builds in der API finden Sie im [Builds-Endpunkthandbuch](./endpoints/builds.md) .

## Hosts

Ein Host stellt ein gehostetes Ziel dar, in dem ein Bibliotheks-Build bereitgestellt und letztendlich bereitgestellt werden kann. Hosts können entweder Akamai- oder SFTP-Server sein.

Informationen zum Verwalten von Hosts in der API finden Sie im [hosts -Endpunkthandbuch](./endpoints/hosts.md) .

## App-Konfigurationen

App-Konfigurationen ermöglichen das Speichern und Abrufen von Anmeldeinformationen zur späteren Verwendung. Informationen zum Verwalten von App-Konfigurationen in der API finden Sie im [Endpoint-Handbuch für App-Konfigurationen](./endpoints/app-configurations.md) .

## Prüfereignisse

Ein Prüfereignis ist ein Datensatz einer bestimmten Änderung an einer anderen Tag-Ressource, die zum Zeitpunkt der Änderung generiert wird. Dies sind Systemereignisse, die über eine Callback-Funktion abonniert werden können.

Informationen zum Verwalten von Prüfereignissen in der API finden Sie im [Endpoint-Handbuch zu Prüfereignissen](./endpoints/audit-events.md) .

## Rückrufe

Ein Rückruf ist eine Nachricht, die Platform bei der Erstellung eines neuen Prüfereignisses an einen URL-Host sendet. Informationen zum Verwalten von Callbacks in der API finden Sie im [Callbacks-Endpoint-Handbuch](./endpoints/callbacks.md) .

## Anmerkungen

Anmerkungen sind Kommentare in Textform, die Sie bestimmten Tag-Ressourcen hinzufügen können, z. B. Datenelementen, Erweiterungen, Bibliotheken, Eigenschaften, Regeln und Regelkomponenten. Informationen zum Verwalten von Notizen in der API finden Sie im [notes-Endpunkthandbuch](./endpoints/notes.md) .

## Profil

Ein Adobe-Profil enthält alle Informationen zum angemeldeten Benutzer, einschließlich aller Organisationen, denen er angehört, der Produktprofile, denen er in jeder Organisation angehört, und der Rechte, die ihm aus jedem Produktprofil zugewiesen sind.

Weitere Informationen zum Anzeigen dieser Informationen in der API finden Sie im [Profil-Endpunkt-Handbuch](./endpoints/profile.md) .

## Durchsuchen

Der Endpunkt `/search` bietet eine Möglichkeit, Ressourcen zu finden, die den gewünschten Kriterien entsprechen und als Abfrage ausgedrückt werden. Alle Abfragen beziehen sich auf Ihr aktuelles Unternehmen und auf verfügbare Eigenschaften. Weitere Informationen zur Verwendung dieser Funktion finden Sie im [Handbuch zum Suchendpunkt](./endpoints/search.md) .

## Nächste Schritte

Um mit der Schema Registry-API Aufrufe zu tätigen, lesen Sie das [Erste Schritte-Handbuch](./getting-started.md) und wählen Sie dann eine der Endpunkthandbücher aus, um zu erfahren, wie Sie bestimmte Endpunkte verwenden.
