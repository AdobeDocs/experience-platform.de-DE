---
title: Überblick zum Entwickeln von Erweiterungen
description: Erfahren Sie mehr über die Hauptkomponenten verschiedener Tag-Erweiterungstypen und den Entwicklungsprozess für Erweiterungen in Adobe Experience Platform.
source-git-commit: a165f0c254885b17db734ab09bf6523175a11dfb
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 21%

---

# Überblick zum Entwickeln von Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../term-updates.md).

Eines der Hauptziele von Tags in Adobe Experience Platform besteht darin, ein offenes Ökosystem zu schaffen, in dem Ingenieure außerhalb von Adobe zusätzliche Funktionen auf ihren Websites und mobilen Anwendungen verfügbar machen können. Dies wird durch Tag-Erweiterungen erreicht. Sobald eine Erweiterung in einer Tag-Eigenschaft installiert wurde, steht die Funktionalität dieser Erweiterung allen Benutzern der Eigenschaft zur Verfügung.

In diesem Dokument werden die Hauptkomponenten einer Erweiterung beschrieben und Links zu weiteren Dokumentationen bereitgestellt, die Sie bei der Entwicklung von Erweiterungen unterstützen.

## Struktur einer Erweiterung

Eine Erweiterung besteht aus einem Verzeichnis von Dateien. Insbesondere besteht eine Erweiterung aus einer Manifestdatei, Bibliotheksmodulen und Ansichten.

### Manifestdatei 

Eine Manifestdatei ([`extension.json`](./manifest.md)) muss im Stammverzeichnis vorhanden sein. Diese Datei beschreibt das Makeup der Erweiterung und wo sich bestimmte Dateien im Verzeichnis befinden. Das Manifest funktioniert ähnlich wie eine [`package.json`](https://docs.npmjs.com/files/package.json)-Datei in einem [npm](https://www.npmjs.com/)-Projekt.

### Bibliotheksmodule

Bibliotheksmodule sind die Dateien, die die verschiedenen [Komponenten](#components) beschreiben, die eine Erweiterung bereitstellt (d. h. die Logik, die in der Tag-Laufzeitbibliothek ausgegeben werden soll). Der Inhalt jeder Bibliotheksmoduldatei muss dem [CommonJS-Modulstandard](http://wiki.commonjs.org/wiki/Modules/1.1.1) entsprechen.

Wenn Sie beispielsweise einen Aktionstyp namens &quot;Signal senden&quot;erstellen, müssen Sie über eine Datei verfügen, die die Logik zum Senden des Beacons enthält. Bei Verwendung von JavaScript könnte die Datei `sendBeacon.js` heißen. Der Inhalt dieser Datei wird in der Tag-Laufzeitbibliothek ausgegeben.

Sie können Bibliotheksmoduldateien an einer beliebigen Stelle im Erweiterungsordner ablegen, sofern Sie deren Speicherorte in `extension.json` beschreiben.

### Ansichten

Eine Ansicht ist eine HTML-Datei, die in ein [`iframe`-Element](https://developer.mozilla.org/de-DE/docs/Web/HTML/Element/iframe) innerhalb der Tags-Anwendung geladen werden kann, insbesondere über die Datenerfassungs-Benutzeroberfläche. Die Ansicht muss ein von der Erweiterung bereitgestelltes Skript enthalten und mit einer kleinen API konform sein, um mit der Anwendung kommunizieren zu können.

Die wichtigste Ansichtsdatei für eine Erweiterung ist ihre Konfiguration. Weitere Informationen finden Sie im Abschnitt [Erweiterungskonfigurationen](#configuration) .

Es gibt keine Einschränkungen hinsichtlich der Verwendung von Bibliotheken in Ihren Ansichten. Mit anderen Worten: Sie können jQuery, Underscore, React, Angular, Bootstrap oder andere verwenden. Es wird jedoch dennoch empfohlen, dafür zu sorgen, dass Ihre Erweiterung ein ähnliches Erscheinungsbild wie die Datenerfassungs-Benutzeroberfläche hat.

Es wird empfohlen, alle ansichtsbezogenen Dateien (HTML, CSS, JavaScript) in einem einzigen Unterverzeichnis abzulegen, das von den Bibliotheksmoduldateien getrennt ist. In `extension.json` können Sie beschreiben, wo sich dieser Unterordner für Ansichten befindet. Platform beliefert dann dieses Unterverzeichnis (und nur dieses Unterverzeichnis) von seinen Webservern.

## Bibliothekskomponenten {#components}

Jede Erweiterung definiert eine Reihe von Funktionen. Diese Funktionen werden implementiert, indem sie in eine [Bibliothek](../ui/publishing/libraries.md) eingefügt werden, die auf Ihrer Website oder in Ihrer App bereitgestellt wird. Bibliotheken sind eine Sammlung einzelner Komponenten, einschließlich Bedingungen, Aktionen, Datenelementen und mehr. Jede Bibliothekskomponente ist ein wiederverwendbarer Code (bereitgestellt von einer Erweiterung), der innerhalb der Tag-Laufzeit ausgegeben wird.

Je nachdem, ob Sie eine Web-Erweiterung oder eine Edge-Erweiterung entwickeln, unterscheiden sich die verfügbaren Komponententypen und ihre Anwendungsfälle. In den folgenden Unterabschnitten finden Sie eine Übersicht darüber, welche Komponenten für jeden Erweiterungstyp verfügbar sind.

### Komponenten für Web-Erweiterungen {#web}

In Web-Erweiterungen werden Regeln durch Ereignisse ausgelöst, die dann bestimmte Aktionen ausführen können, wenn ein bestimmter Bedingungssatz erfüllt ist. Weitere Informationen finden Sie in der Übersicht über [Modulfluss in Web-Erweiterungen](./web/flow.md).

Zusätzlich zu den von Adobe bereitgestellten [Kernmodulen](./web/core.md) können Sie die folgenden Bibliothekskomponenten in Ihren Web-Erweiterungen definieren:

* [Ereignisse](./web/event-types.md)
* [Bedingungen](./web/condition-types.md)
* [Aktionen](./web/action-types.md)
* [Datenelemente](./web/data-element-types.md)
* [Gemeinsame Module](./web/shared.md)

>[!NOTE]
>
>Weitere Informationen zum erforderlichen Format für die Implementierung von Bibliothekskomponenten in Web-Erweiterungen finden Sie unter [Übersicht über das Modulformat](./web/format.md).

### Komponenten für Kantenerweiterungen {#edge}

In Edge-Erweiterungen werden Regeln durch Bedingungsprüfungen ausgelöst, die dann bestimmte Aktionen ausführen, wenn diese Prüfungen erfolgreich sind. Weitere Informationen finden Sie in der Übersicht zum Fluss der Kantenerweiterung [a1/> .](./edge/flow.md)

Sie können die folgenden Bibliothekskomponenten in Ihren Edge-Erweiterungen definieren:

* [Bedingungen](./edge/condition-types.md)
* [Aktionen](./edge/action-types.md)
* [Datenelemente](./edge/data-element-types.md)

>[!NOTE]
>
>Details zum erforderlichen Format für die Implementierung von Bibliotheksmodulen in Edge-Erweiterungen finden Sie unter [Überblick über das Modulformat](./edge/format.md).

## Erweiterungskonfiguration {#configuration}

Die Konfiguration einer Erweiterung bezieht sich auf die Art und Weise, wie globale Einstellungen eines Benutzers erfasst werden. Die Konfiguration besteht aus einer Ansichtskomponente, die Einstellungen in der Tag-Laufzeitbibliothek als Standardobjekt exportiert und ausgibt.

Betrachten Sie beispielsweise eine Erweiterung, die es dem Benutzer ermöglicht, ein Beacon mit der Aktion &quot;Beacon senden&quot;zu senden, und das Beacon muss immer eine Konto-ID enthalten. Anstatt Benutzer jedes Mal, wenn sie die Aktion &quot;Beacon senden&quot;konfigurieren, um eine Konto-ID zu bitten, sollte die Erweiterung in der Erweiterungskonfigurationsansicht einmal nach der Konto-ID fragen. Jedes Mal, wenn ein Beacon gesendet werden soll, kann die Aktion &quot;Beacon senden&quot;die Konto-ID aus der Erweiterungskonfiguration abrufen und zum Beacon hinzufügen.

Wenn Benutzer eine Erweiterung in einer Eigenschaft in der Benutzeroberfläche installieren, wird ihnen die Ansicht für die Erweiterungskonfiguration angezeigt, die sie abschließen müssen, um die Installation abzuschließen.

Weitere Informationen finden Sie im Handbuch zu [Erweiterungskonfigurationen](./configuration.md).

## Übermitteln von Erweiterungen

Nachdem Sie die Erweiterung fertig erstellt haben, können Sie sie zur Auflistung im Erweiterungskatalog in Platform übermitteln. Weitere Informationen finden Sie unter [Übersicht über den Prozess zur Übermittlung von Erweiterungen](./submit/overview.md) .