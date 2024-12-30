---
title: Erste Schritte bei der Entwicklung von Erweiterungen
description: So beginnen Sie mit der Entwicklung Ihrer eigenen Tag-Erweiterungen in Adobe Experience Platform.
exl-id: 3925b928-0180-4a4f-aaa6-42f342089560
source-git-commit: 077d3ac5a34f052ef6293927d67e3cc8afb27563
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 80%

---

# Erste Schritte bei der Entwicklung von Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../term-updates.md).

Um Ihnen den Einstieg und die Erstellung von Erweiterungen zu erleichtern, verwenden wir das Open-Source-Tool für Strukturvorlagen, das von Entwicklern von Adobe zur Verfügung gestellt wird, um die erforderlichen Dateien und Dateistrukturen für Ihr Erweiterungspaket zu erstellen, sodass Sie nur noch den entscheidenden Teil beitragen müssen: den eigentlichen Code schreiben.

## Voraussetzungen

* Installieren Sie [Node.js](https://nodejs.org/de/download/).

## Setup der Erweiterung

Erstellen Sie einen Ordner, in dem die Erweiterungsdateien gespeichert werden.

```shell
mkdir example && cd example
```

In dieser Anleitung wird das Tool zum Erstellen einer Strukturvorlage für Erweiterungen verwendet, um die anfängliche Erweiterungsstruktur zu erstellen, damit Entwickler schnell mit der Codierung beginnen können. Falls gewünscht, kann dieser Vorgang manuell ohne das scaffold-Tool durchgeführt werden.

Führen Sie das scaffold-Tool aus.

```shell
npx @adobe/reactor-scaffold
```

Das scaffold-Tool fordert Sie zur Eingabe folgender anfänglicher Konfigurationsoptionen auf:

* Anzeigename: Der sichtbare Name der Erweiterung
* Platform - Gibt an, ob die Erweiterung für Web, Mobile oder Edge entwickelt wurde
* Version: Die Version der Erweiterung
* Beschreibung: Eine kurze Beschreibung des Zwecks der Erweiterung
* Autor: Der Name des Autors der Erweiterung

>[!NOTE]
> Bei Erweiterungen für Mobilgeräte werden mehrere Fragen zur Struktur Ihrer Android- und iOS-Anwendungen gestellt.

Das scaffold-Tool stellt anschließend Optionen zum Erstellen der Erweiterungsstruktur bereit:

* [Erweiterungskonfigurationsansicht](./configuration.md): Die Ansicht, HTML-Datei, über die eine Erweiterung globale Einstellungen eines Benutzers erfasst.
* [Ereignistypen](./web/event-types.md): Definiert eine zu überwachende Aktivität. Sie erfahren beispielsweise, wenn ein Benutzer schnell scrollt oder mit einem Seitenelement interagiert. Ereignisse können in Regeln zum Ausführen von Aktionen verwendet werden.
* [Bedingungstypen](./web/condition-types.md): Bedingungstypen auswerten, ob etwas wahr oder falsch ist.
So kann beispielsweise ermittelt werden, ob der Benutzer den Browser Chrome verwendet, ob er ein iPad benutzt oder ob er sich in einer bestimmten Domain befindet.
* [Aktionstypen](./web/action-types.md): Die Aktion, die ausgeführt werden soll, wenn ein Ereignis eintritt. So können Sie beispielsweise einen Analytics-Beacon senden, ein Angebot anzeigen, ein Cookie speichern oder einen Support-Chat öffnen.
* [Datenelementtypen](./web/data-element-types.md): Datenelementtypen rufen Daten ab. Diese Daten können sich in einem lokalen Datenspeicher, in einem Cookie, in einem DOM-Element oder an einem benutzerdefinierten Speicherort befinden.
* [Freigegebene Module](./web/shared.md) (nur Web): Ein freigegebenes Modul ist ein Mechanismus, durch den Erweiterungen mit anderen Erweiterungen kommunizieren können.
* [Ansichten](./web/views.md): Jedes Ereignis, jede Bedingung, jede Aktion und jeder Datenelementtyp kann eine Ansicht bereitstellen, in der Benutzer Einstellungen angeben können.
* Exchange-URL (nur Web und Edge): Wenn eine Erweiterung in einem öffentlichen Adobe-Katalog veröffentlicht wird, geben Sie die Auflistungs-URL hier an.
* Symbolpfad: Ein Pfad zu einer Symboldatei für die Erweiterung.

>[!NOTE]
>
>* Bei jeder nachfolgenden Ausführung des scaffold-Tools wird die anfängliche Konfiguration übersprungen.
>* Es können mehrere Ereignisse, Bedingungen und Aktionen hinzugefügt werden.
>* Es darf nur eine Konfigurationsansicht vorhanden sein.

## Nächste Schritte

* Befolgen Sie die [Übersicht über den Einreichungsprozess](./submit/overview.md) und bereiten Sie [ (](./submit/upload-and-test.md#validate)) und [Upload](./submit/upload-and-test.md#integration) Erweiterung vor, um sie im Tag-Ökosystem zu testen.
