---
title: Übersicht über Tags
description: Tags in Adobe Experience Platform sind die nächste Generation von Funktionen für das Tag-Management von Adobe. Tags bieten Kunden eine einfache Möglichkeit, alle Analyse-, Marketing- und Werbe-Tags bereitzustellen und zu verwalten, die für relevante Kundenerlebnisse notwendig sind.
exl-id: 23d882a5-1ddd-404b-a7e9-3000f1804971
source-git-commit: 13c02dd5930905e3851ff147c0ea4d914e3dc6c7
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 100%

---

# Übersicht über Tags

>[!NOTE]
>
>Die Ereignisweiterleitung ist eine gebührenpflichtige Funktion, die im Rahmen von Adobe Real-time Customer Data Platform Connections, Prime und Ultimate angeboten wird.

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](./term-updates.md).

Tags in Adobe Experience Platform sind die nächste Generation von Funktionen für das Tag-Management von Adobe. Tags bieten Kunden eine einfache Möglichkeit, alle Analyse-, Marketing- und Werbe-Tags bereitzustellen und zu verwalten, die für relevante Kundenerlebnisse notwendig sind.

Tags ermöglichen jedem das Aufbauen und Verwalten eigener Integrationen (auch *Erweiterungen* genannt). Diese Erweiterungen stehen [!DNL Adobe Experience Cloud]-Kunden in einer App-Store-Oberfläche zur Verfügung, damit sie ihre Tags schnell installieren, konfigurieren und bereitstellen können.

Tags werden [!DNL Adobe Experience Cloud]-Kunden als inbegriffene Mehrwertfunktion angeboten.

## Wesentliche Vorteile {#key-benefits}

* Schnellere Amortisierungszeit.
* Vertrauenswürdige Daten durch zentrale Erfassung, Organisation und Bereitstellung mithilfe von Datenelementen.
* Attraktive Erlebnisse durch die Integration von Daten und Marketing-Technologie mithilfe von Regel-Builder.

## Wichtigste Funktionen {#key-features}

### Erweiterungen {#extensions}

Eine Erweiterung ist ein Paket mit Code (JavaScript, HTML und CSS) zur Erweiterung der Tag-Funktionalität. Erstellen, verwalten und aktualisieren Sie Ihre Integrationen mithilfe einer praktischen Self-Service-Oberfläche. Sie können sich Erweiterungen als Programme vorstellen, mit denen Sie Ihre Aufgaben erledigen.

### Erweiterungskatalog {#extension-catalog}

Sie können von unabhängigen Softwareherstellern erstellte und gewartete Tools für Marketing/Werbung durchsuchen, konfigurieren und bereitstellen.

### Regel-Builder {#rule-builder}

Erstellen Sie zuverlässige Regeln, die mehrere Ereignisse miteinander kombinieren und so aufeinander folgen lassen, wie Sie es mithilfe der Wenn-dann-Logik mit Bedingungen und Ausnahmen bestimmen. Regeln bieten Optionen für:

* Ereignisse
* Bedingungen
* Ausnahmen
* Aktionen

Der Regel-Builder beinhaltet eine Echtzeit-Fehlerprüfung und Syntaxhervorhebung für Ihren benutzerspezifischen Code.

Wenn die in Ihren Regeln angegebenen Kriterien erfüllt sind und die entsprechenden Bedingungen ebenfalls erfüllt sind, werden die von Ihnen definierten Aktionen in der angegebenen Reihenfolge ausgeführt.

### Datenelemente {#data-elements}

Sie können Daten für webbasierte Marketing- und Werbetechnologie erfassen, organisieren und bereitstellen.

### Veröffentlichung für Unternehmen {#enterprise-publishing}

Durch den Veröffentlichungsprozess können Teams Code auf Seiten veröffentlichen. Unterschiedliche Personen können eine Implementierung erstellen, genehmigen und auf Ihren Seiten veröffentlichen.

* Änderungen an Ihrem Code werden in von Ihnen definierten Bibliotheken gekapselt.
* Sie geben an, wo und wann Ihr Code bereitgestellt werden soll.
* Mehrere Bibliotheken können gleichzeitig von verschiedenen Teams erstellt werden.
* Unbegrenzte Entwicklungsumgebungen&#x200B;
* Ein absichtlicher, berechtigungsbasierter Prozess zum Zusammenführen von Bibliotheken.

### Sie können APIs öffnen {#open-apis}

Sie können Implementierungen einzelner Technologien oder einer Gruppe von Technologien automatisieren.

* Tags interagieren mit der Reactor-API.
* Bereitstellungen können über APIs automatisiert werden.
* Integrieren Sie die -APIs in Ihre eigenen internen Systeme.
* Sie können bei Bedarf Ihre eigene Benutzeroberfläche erstellen.

### Einfaches, modulares Container-Tag {#modular-tag}

Der Inhalt Ihres Containers wird minimiert, einschließlich Ihres benutzerspezifischen Codes. Alles ist modular. Wenn Sie ein Element nicht benötigen, ist es nicht in Ihrer Bibliothek enthalten. Das Ergebnis ist eine schnelle und kompakte Implementierung. Siehe [Minimierung](./ui/publishing/builds.md).

## Weitere Besonderheiten {#other-highlights}

Tags bieten verschiedene Verbesserungen im Vergleich zu ähnlichen Systemen. Dazu zählen unter anderem folgende:

* Keine Verwendung von `document.write ()`, wo Chrome dies nicht zulässt
* Die Regeln „Seitenanfang“ und „Seitenende“ sind in der Hauptbibliothek gebündelt, um unnötige HTTP-Aufrufe zu minimieren.
* Benutzerdefinierte Aktions-Skripts innerhalb einer Regel können gleichzeitig geladen werden, werden aber nacheinander ausgeführt.
* Wenn Sie die Regeln „Seitenanfang“ und „Seitenende“ vermeiden, ist der Code hauptsächlich asynchron mit einem Pfad für vollständig asynchronen Code.
