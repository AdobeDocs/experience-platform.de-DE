---
title: Überblick zum Entwickeln von Erweiterungen
description: Lernen Sie die Hauptkomponenten verschiedener Tag-Erweiterungstypen und den Prozess der Erweiterungsentwicklung in Adobe Experience Platform kennen.
exl-id: b72df3df-f206-488d-a690-0f086973c5b6
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: ht
source-wordcount: '949'
ht-degree: 100%

---

# Überblick zum Entwickeln von Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../term-updates.md).

Eines der Hauptziele von Tags in Adobe Experience Platform besteht darin, ein offenes Ökosystem zu schaffen, in dem Ingenieure außerhalb von Adobe zusätzliche Funktionen auf ihren Websites und mobilen Anwendungen verfügbar machen können. Dies wird durch Tag-Erweiterungen erreicht. Sobald eine Erweiterung auf einer Tag-Eigenschaft installiert wurde, werden die Funktionen dieser Erweiterung für alle Benutzer der Eigenschaft verfügbar.

In diesem Dokument werden die Hauptkomponenten einer Erweiterung erläutert, dazu werden Links zu weiterer Dokumentation angegeben, um Sie bei der Entwicklung von Erweiterungen zu unterstützen.

## Struktur einer Erweiterung

Eine Erweiterung besteht aus einem Verzeichnis von Dateien. Insbesondere besteht eine Erweiterung aus einer Manifestdatei, Bibliotheksmodulen und Ansichten.

### Manifestdatei 

Eine Manifestdatei ([`extension.json`](./manifest.md)) muss im Stammverzeichnis vorhanden sein. Diese Datei beschreibt unter anderem den Aufbau der Erweiterung und gibt an, wo sich bestimmte Dateien im Verzeichnis befinden. Das Manifest funktioniert ähnlich wie eine [`package.json`](https://docs.npmjs.com/files/package.json)-Datei in einem [npm](https://www.npmjs.com/)-Projekt.

### Bibliotheksmodule

Bibliotheksmodule sind die Dateien, die die verschiedenen [Komponenten](#components) beschreiben, die eine Erweiterung bereitstellt (d. h. die Logik, die in der Tag-Laufzeitbibliothek ausgegeben werden soll). Der Inhalt jeder Bibliotheksmoduldatei muss dem [CommonJS-Modulstandard](https://nodejs.org/api/modules.html#modules-commonjs-modules) entsprechen.

Wenn Sie beispielsweise einen Aktionstyp namens „Beacon senden“ erstellen, müssen Sie über eine Datei verfügen, die die Logik zum Senden des Beacons enthält. Bei Verwendung von JavaScript könnte die Datei `sendBeacon.js` heißen. Der Inhalt dieser Datei wird innerhalb der Tag-Laufzeitbibliothek ausgegeben.

Sie können Bibliotheksmoduldateien an einer beliebigen Stelle im Erweiterungsordner ablegen, sofern Sie deren Speicherorte in `extension.json` beschreiben.

### Ansichten 

Eine Ansicht ist eine HTML-Datei, die in ein [`iframe`-Element](https://developer.mozilla.org/de-DE/docs/Web/HTML/Element/iframe) innerhalb des Tags-Programms geladen werden kann, insbesondere über die Datenerfassungs-Benutzeroberfläche. Die Ansicht muss ein von der Erweiterung bereitgestelltes Skript enthalten und mit einer kleinen API konform sein, um mit dem Programm kommunizieren zu können.

Die wichtigste Ansichtsdatei für eine Erweiterung ist ihre Konfiguration. Weitere Informationen finden Sie im Abschnitt [Erweiterungskonfigurationen](#configuration).

Es gibt keine Einschränkungen hinsichtlich der Verwendung von Bibliotheken in Ihren Ansichten. Mit anderen Worten: Sie können jQuery, Underscore, React, Angular, Bootstrap oder andere verwenden. Es wird jedoch dennoch empfohlen, Ihre Erweiterung so zu gestalten, dass sie ein ähnliches Erscheinungsbild wie die Datenerfassungs-Benutzeroberfläche hat.

Es wird empfohlen, alle ansichtsbezogenen Dateien (HTML, CSS, JavaScript) in einem einzigen Unterverzeichnis abzulegen, das von den Bibliotheksmoduldateien getrennt ist. In `extension.json` können Sie beschreiben, wo sich dieser Unterordner für die Ansichten befindet. Platform bedient dann dieses Unterverzeichnis (und nur dieses Unterverzeichnis) von seinen Webservern aus.

## Bibliothekskomponenten {#components}

Jede Erweiterung definiert eine Reihe von Funktionen. Diese Funktionen werden implementiert, indem sie in eine [Bibliothek](../ui/publishing/libraries.md) eingefügt werden, die auf Ihrer Website oder in Ihrem Programm bereitgestellt wird. Bibliotheken sind eine Sammlung einzelner Komponenten, einschließlich Bedingungen, Aktionen, Datenelementen und mehr. Jede Bibliothekskomponente ist ein Stück wiederverwendbarer Code (bereitgestellt von einer Erweiterung), der innerhalb der Tag-Laufzeit ausgegeben wird.

Je nachdem, ob Sie eine Web-Erweiterung oder eine Edge-Erweiterung entwickeln, unterscheiden sich die verfügbaren Komponententypen und ihre Anwendungsfälle. In den folgenden Unterabschnitten finden Sie eine Übersicht darüber, welche Komponenten für jeden Erweiterungstyp verfügbar sind.

### Komponenten für Web-Erweiterungen {#web}

In Web-Erweiterungen werden Regeln durch Ereignisse ausgelöst, die dann bestimmte Aktionen ausführen können, wenn ein bestimmter Bedingungssatz erfüllt ist. Weitere Informationen finden Sie in der Übersicht über [Modulfluss in Web-Erweiterungen](./web/flow.md).

Zusätzlich zu den [Kernmodulen](./web/core.md), die von Adobe zur Verfügung gestellt werden, können Sie die folgenden Bibliothekskomponenten in Ihren Web-Erweiterungen definieren:

* [Ereignisse](./web/event-types.md)
* [Bedingungen](./web/condition-types.md)
* [Aktionen](./web/action-types.md)
* [Datenelemente](./web/data-element-types.md)
* [Gemeinsame Module](./web/shared.md)

>[!NOTE]
>
>Details zum erforderlichen Format für die Implementierung von Bibliotheksmodulen in Web-Erweiterungen finden Sie im [Überblick über die Modulformate](./web/format.md).

### Module für Edge-Erweiterungen {#edge}

In Edge-Erweiterungen werden Regeln durch Bedingungsprüfungen ausgelöst, die dann bestimmte Aktionen ausführen, wenn diese Prüfungen erfolgreich sind. Weitere Informationen finden Sie im Überblick zum [Fluss der Edge-Erweiterungen](./edge/flow.md).

Sie können die folgenden Bibliothekskomponenten in Ihren Edge-Erweiterungen definieren:

* [Bedingungen](./edge/condition-types.md)
* [Aktionen](./edge/action-types.md)
* [Datenelemente](./edge/data-element-types.md)

>[!NOTE]
>
>Details zum erforderlichen Format für die Implementierung von Bibliotheksmodulen in Edge-Erweiterungen finden Sie unter [Überblick über das Modulformat](./edge/format.md).

## Erweiterungskonfiguration {#configuration}

Die Konfiguration einer Erweiterung bezieht sich auf die Art und Weise, wie globale Einstellungen eines Benutzers erfasst werden. Die Konfiguration besteht aus einer Ansichtskomponente, die Einstellungen in der Tag-Laufzeitbibliothek als Standardobjekt exportiert und ausgibt.

Betrachten Sie beispielsweise eine Erweiterung, die es dem Benutzer ermöglicht, ein Beacon mit der Aktion „Beacon senden“ zu senden, wobei das Beacon immer eine Konto-ID enthalten muss. Anstatt Benutzer jedes Mal um eine Konto-ID zu bitten, wenn sie die Aktion „Beacon senden“ konfigurieren, sollte die Erweiterung in der Erweiterungskonfigurationsansicht nur einmal nach der Konto-ID fragen. Jedes Mal, wenn ein Beacon gesendet werden soll, kann das Bibliotheksmodul für die Aktion „Beacon senden“ die Konto-ID aus der Erweiterungskonfiguration abrufen und dem Beacon hinzufügen.

Wenn Benutzer eine Erweiterung in einer Eigenschaft in der Benutzeroberfläche installieren, wird ihnen die Ansicht für die Erweiterungskonfiguration angezeigt, welche sie vervollständigen müssen, um die Installation abzuschließen.

Weitere Informationen finden Sie im Handbuch zu [Erweiterungskonfigurationen](./configuration.md).

## Übermitteln von Erweiterungen

Nachdem Sie die Erweiterung fertig erstellt haben, können Sie sie zur Auflistung im Erweiterungskatalog in Platform übermitteln. Weiterführende Informationen dazu finden Sie unter [Übermittlungsprozess von Erweiterungen – Überblick](./submit/overview.md).
