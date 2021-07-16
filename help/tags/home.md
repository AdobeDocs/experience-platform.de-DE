---
title: Übersicht über Tags
description: Tags in Adobe Experience Platform sind die nächste Generation von Tag-Management-Funktionen von Adobe. Mit Tags können Kunden alle Analyse-, Marketing- und Werbe-Tags bereitstellen und verwalten, die zur Unterstützung entsprechender Kundenerlebnisse erforderlich sind.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 62%

---

# Übersicht über Tags

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](./term-updates.md).

Tags in Adobe Experience Platform sind die nächste Generation von Tag-Management-Funktionen von Adobe. Mit Tags können Kunden alle Analyse-, Marketing- und Werbe-Tags bereitstellen und verwalten, die zur Unterstützung entsprechender Kundenerlebnisse erforderlich sind.

Mit Tags kann jeder eigene Integrationen erstellen und verwalten, die *extensions* genannt werden. Diese Erweiterungen stehen [!DNL Adobe Experience Cloud]-Kunden in einer App-Store-Oberfläche zur Verfügung, damit sie ihre Tags schnell installieren, konfigurieren und bereitstellen können.

Tags werden [!DNL Adobe Experience Cloud]-Kunden als integrierte Mehrwertfunktion angeboten.

## Wesentliche Vorteile

* Schnellere Amortisierungszeit.
* Vertrauenswürdige Daten durch zentrale Erfassung, Organisation und Bereitstellung mithilfe von Datenelementen.
* Attraktive Elebnisse durch die Integration von Daten und Marketingtechnologie mithilfe von Regel-Builder.

## Wichtigste Funktionen

### Erweiterungen

Eine Erweiterung ist ein Paket mit Code (JavaScript, HTML und CSS), das die Tag-Funktion erweitert. Erstellen, verwalten und aktualisieren Sie Ihre Integrationen mithilfe einer praktischen Self-Service-Oberfläche. Sie können sich Erweiterungen als Apps vorstellen, mit denen Sie Ihre Aufgaben erledigen.

### Erweiterungskatalog

Sie können von unabhängigen Softwareherstellern erstellte und gewartete Tools für Marketing/Werbung durchsuchen, konfigurieren und bereitstellen.

### Regel-Builder

Erstellen Sie zuverlässige Regeln, die mehrere Ereignisse miteinander kombinieren und so aufeinander folgen lassen, wie Sie es mithilfe der Wenn-dann-Logik mit Bedingungen und Ausnahmen bestimmen. Regeln bieten Optionen für:

* Ereignisse
* Bedingungen
* Ausnahmen
* Aktionen

Der Regel-Builder beinhaltet eine Echtzeit-Fehlerprüfung und Syntaxhervorhebung für Ihren benutzerspezifischen Code.

Wenn die in Ihren Regeln angegebenen Kriterien erfüllt sind und die entsprechenden Bedingungen ebenfalls erfüllt sind, werden die von Ihnen definierten Aktionen in der angegebenen Reihenfolge ausgeführt.

### Datenelemente

Sie können Daten für webbasierte Marketing- und Werbetechnologie erfassen, organisieren und bereitstellen.

### Veröffentlichung für Unternehmen

Durch den Veröffentlichungsprozess können Teams Code auf Seiten veröffentlichen. Verschiedene Personen können eine Implementierung erstellen, genehmigen und auf Ihren Seiten veröffentlichen.

* Änderungen an Ihrem Code werden in den von Ihnen definierten Bibliotheken eingekapselt.
* Sie geben an, wo und wann Ihr Code bereitgestellt werden soll.
* Mehrere Bibliotheken können gleichzeitig von verschiedenen Teams erstellt werden.
* Unbegrenzte Entwicklungsumgebungen&#x200B;
* Ein vorsätzlicher, berechtigungsbasierter Prozess zum Zusammenführen von Bibliotheken.

### Sie können APIs öffnen

Automatisieren Sie Implementierungen einzelner Technologien oder einer Gruppe von Technologien.

* Tags interagieren mit der Reactor-API.
* Bereitstellungen können über APIs automatisiert werden.
* Integrieren Sie die -APIs in Ihre eigenen internen Systeme.
* Sie können bei Bedarf Ihre eigene Benutzeroberfläche erstellen.

### Einfaches, modulares Container-Tag

Der Inhalt Ihres Containers wird minimiert, einschließlich Ihres benutzerspezifischen Codes. Alles ist modular. Wenn Sie ein Element nicht benötigen, ist es nicht in Ihrer Bibliothek enthalten. Das Ergebnis ist eine schnelle und kompakte Implementierung. Siehe [Minimierung](./ui/publishing/builds.md).

## Weitere Besonderheiten

Tags bieten verschiedene Verbesserungen im Vergleich zu ähnlichen Systemen, darunter:

* Keine Verwendung von `document.write ()`, wo Chrome dies nicht zulässt
* Die Regeln „Seitenanfang“ und „Seitenende“ sind in der Hauptbibliothek gebündelt, um unnötige HTTP-Aufrufe zu minimieren.
* Benutzerdefinierte Aktions-Skripts innerhalb einer Regel können gleichzeitig geladen werden, werden aber nacheinander ausgeführt.
* Wenn Sie die Regeln „Seitenanfang“ und „Seitenende“ vermeiden, ist der Code hauptsächlich asynchron mit einem Pfad für vollständig asynchronen Code.
