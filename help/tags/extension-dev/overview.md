---
title: Überblick zum Entwickeln von Erweiterungen
description: Erfahren Sie mehr über die Hauptkomponenten verschiedener Tag-Erweiterungstypen und den Entwicklungsprozess für Erweiterungen in Adobe Experience Platform.
source-git-commit: 421d1d0660c4c9c7280974f8a812a8f0e4f7cbea
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 65%

---

# Überblick zum Entwickeln von Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../term-updates.md).

Eines der Hauptziele von Adobe Experience Platform besteht darin, ein offenes Ökosystem zu schaffen, in dem Ingenieure außerhalb des Kernteams zusätzliche Funktionen über Tags verfügbar machen können. Dies erfolgt über Tag-Erweiterungen. Sobald eine Erweiterung von einem Benutzer in einer Tag-Eigenschaft installiert wurde, steht die Funktionalität dieser Erweiterung allen Benutzern der Eigenschaft zur Verfügung.

In diesem Dokument werden die Hauptkomponenten der verschiedenen Erweiterungstypen beschrieben und Links für weitere Dokumentationen bereitgestellt, die Sie bei der Entwicklung von Erweiterungen unterstützen.

## Bibliotheksmodule

Bibliotheksmodule sind Teile von wiederverwendbarem Code, die von einer Erweiterung bereitgestellt werden und innerhalb der Tag-Laufzeitbibliothek ausgegeben werden. Je nachdem, ob Sie eine Web-Erweiterung oder eine Edge-Erweiterung entwickeln, unterscheiden sich die verfügbaren Modultypen und ihre Anwendungsfälle. Eine Übersicht der Module für die einzelnen Erweiterungstypen finden Sie in den folgenden Unterabschnitten:

* [Module für Web-Erweiterungen](#web-modules)
* [Module für Edge-Erweiterungen](#edge-modules)

### Module für Web-Erweiterungen {#web-modules}

In Web-Erweiterungen werden Regeln durch Ereignisse ausgelöst, die dann bestimmte Aktionen ausführen können, wenn ein bestimmter Bedingungssatz erfüllt ist. Weitere Informationen finden Sie in der Übersicht über [Modulfluss in Web-Erweiterungen](./web/flow.md).

Zusätzlich zu den [Kernmodulen](./web/core.md), die von Adobe zur Verfügung gestellt werden, können Sie die folgenden Bibliotheksmodultypen in Ihren Web-Erweiterungen definieren:

* [Ereignistypen](#web-event)
* [Bedingungstypen](#web-condition)
* [Aktionstypen](#web-action)
* [Datenelementtypen](#web-data-element)
* [Gemeinsame Module](#shared)

>[!NOTE]
>
>Details zum erforderlichen Format für die Implementierung von Bibliotheksmodulen in Web-Erweiterungen finden Sie unter [Überblick über das Modulformat](./web/format.md).

#### Ereignistypen {#web-event}

Ein Regelereignis ist eine Aktivität, die vor dem Auslösen einer Regel auftreten muss.

Beispielsweise könnte eine Erweiterung einen Ereignistyp „Geste“ bereitstellen, der überwacht, ob eine bestimmte Maus- oder Berührungsgeste auftritt. Sobald die Geste auftritt, löst die Logik dieses Ereignisses die Regel aus.

Ereignistypen bestehen in der Regel aus (1) einer Ansicht, die in der Datenerfassungs-Benutzeroberfläche angezeigt wird und es Benutzern ermöglicht, die Einstellungen für das Ereignis zu ändern, und (2) einem Bibliotheksmodul, das in der Tag-Laufzeitbibliothek ausgegeben wird, um die Einstellungen zu interpretieren und darauf zu achten, dass eine bestimmte Aktivität eintritt.

[Weitere Infos](./web/event-types.md)

#### Bedingungstypen {#web-condition}

Eine Regelbedingung wird ausgewertet, nachdem ein Regelereignis aufgetreten ist. Alle Bedingungen müssen „true“ zurückgeben, damit die Regel weiter verarbeitet wird. Eine Ausnahme besteht, wenn Benutzer Bedingungen explizit in einem „Ausnahme“-Bereich platzieren. In diesem Fall müssen alle Bedingungen innerhalb dieses Bereichs „false“ zurückgeben, damit die Regel weiter verarbeitet werden kann.

Beispielsweise könnte eine Erweiterung einen Bedingungstyp &quot;Viewport enthält&quot;bereitstellen, in dem der Benutzer einen CSS-Selektor angeben könnte. Wenn diese Bedingung auf der Website des Kunden ausgewertet wird, kann die Erweiterung nach Elementen suchen, die mit der CSS-Auswahl übereinstimmen, und die Information zurückgeben, ob sich eines davon im Ansichtsfenster des Benutzers befindet.

Bedingungstypen bestehen in der Regel aus (1) einer Ansicht, die in der Datenerfassungs-Benutzeroberfläche angezeigt wird und es Benutzern ermöglicht, die Einstellungen für die Bedingung zu ändern, und (2) einem Bibliotheksmodul, das in der Tag-Laufzeitbibliothek ausgegeben wird, um die Einstellungen zu interpretieren und eine Bedingung auszuwerten.

[Weitere Infos](./web/condition-types.md)

#### Aktionstypen {#web-action}

Eine Regelaktion ist eine Aktion, die ausgeführt wird, nachdem das Regelereignis aufgetreten ist und die Auswertung gezeigt hat, dass die Bedingungen erfüllt sind.

Beispielsweise könnte eine Erweiterung einen Aktionstyp „Support-Chat anzeigen“ bereitstellen, der einen Dialog mit dem Support-Chat anzeigen könnte, um Benutzern zu helfen, die beim Auschecken Probleme haben.

Aktionstypen bestehen in der Regel aus (1) einer Ansicht, die in der Datenerfassungs-Benutzeroberfläche angezeigt wird und es Benutzern ermöglicht, die Einstellungen für die Aktion zu ändern, und (2) einem Bibliotheksmodul, das in der Tag-Laufzeitbibliothek ausgegeben wird, um die Einstellungen zu interpretieren und eine Aktion durchzuführen.

[Weitere Infos](./web/action-types.md)

#### Datenelementtypen {#web-data-element}

Bei Datenelementen handelt es sich im Wesentlichen um Aliase zu Datenteilen auf einer Seite, unabhängig davon, ob diese Daten in den Parametern von Abfragezeichenfolgen, Cookies, DOM-Elementen oder an einem anderen Ort gefunden werden. Ein Datenelement kann durch Regeln referenziert werden und dient als Abstraktion für den Zugriff auf diese Daten. Wenn sich der Speicherort der Daten in Zukunft ändert (z. B. vom `innerHTML` eines DOM-Elements in den Wert einer JavaScript-Variablen), kann ein einzelnes Datenelement neu konfiguriert werden, wobei alle Regeln, die auf dieses Datenelement verweisen, unverändert bleiben können.

Ein Datenelementtyp ermöglicht es Benutzern, Datenelemente so zu konfigurieren, dass auf eine bestimmte Art und Weise auf ein Datenelement zugegriffen werden kann. Beispielsweise könnte eine Erweiterung einen Datenelementtyp &quot;Lokales Datenspeicherungselement&quot;bereitstellen, in dem der Benutzer einen Elementnamen für die lokale Datenspeicherung angeben könnte. Wenn das Datenelement durch eine Regel referenziert wird, kann die Erweiterung den Elementwert der lokalen Datenspeicherung mithilfe des Elementnamens der lokalen Datenspeicherung nachschlagen, den der Benutzer beim Konfigurieren des Datenelements angegeben hat.

Datenelementtypen bestehen in der Regel aus (1) einer Ansicht, die in der Datenerfassungs-Benutzeroberfläche angezeigt wird und es Benutzern ermöglicht, die Einstellungen für das Datenelement zu ändern, und (2) einem Bibliotheksmodul, das in der Tag-Laufzeitbibliothek ausgegeben wird, um die Einstellungen zu interpretieren und Datenteile abzurufen.

[Weitere Infos](./web/data-element-types.md)

#### Gemeinsame Module {#shared}

Ein gemeinsames Modul ist ein Modul, das durch eine Erweiterung verfügbar gemacht wird und auf das eine andere zugreifen kann. Dies kann ein sehr nützlicher Mechanismus für die Kommunikation zwischen Erweiterungen sein. Beispielsweise kann Erweiterung A ein Datenelement asynchron laden und es über ein [Versprechen](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise) für Erweiterung B verfügbar machen.

Gemeinsame Module werden auch dann in die Bibliothek eingeschlossen, wenn sie nie von anderen Erweiterungen aus aufgerufen werden. Um die Bibliotheksgröße nicht unnötig zu erhöhen, sollten Sie vorsichtig damit sein, was Sie als gemeinsames Modul bereitstellen.

Gemeinsame Module verfügen nicht über eine Ansicht-Komponente.

[Weitere Infos](./web/shared.md)

### Module für Edge-Erweiterungen {#edge-modules}

In Edge-Erweiterungen werden Regeln durch Bedingungsprüfungen ausgelöst, die dann bestimmte Aktionen ausführen, wenn diese Prüfungen erfolgreich sind. Weitere Informationen finden Sie in der Übersicht über [Modulfluss in Edge-Erweiterungen](./edge/flow.md).

Sie können in Ihren Edge-Erweiterungen eigene Bibliotheksmodule definieren. Diese können in die folgenden Typen kategorisiert werden:

* [Bedingungstypen](#condition)
* [Aktionstypen](#action)
* [Datenelementtypen](#data-element)

>[!NOTE]
>
>Details zum erforderlichen Format für die Implementierung von Bibliotheksmodulen in Edge-Erweiterungen finden Sie unter [Überblick über das Modulformat](./edge/format.md).

#### Bedingungstypen {#condition}

Eine Regelbedingung wird ausgewertet, nachdem ein Regelereignis aufgetreten ist. Alle Bedingungen müssen „true“ zurückgeben, damit die Regel weiter verarbeitet wird. Eine Ausnahme besteht, wenn Benutzer Bedingungen explizit in einem „Ausnahme“-Bereich platzieren. In diesem Fall müssen alle Bedingungen innerhalb dieses Bereichs „false“ zurückgeben, damit die Regel weiter verarbeitet werden kann.

Beispielsweise könnte eine Erweiterung einen Bedingungstyp &quot;Viewport enthält&quot;bereitstellen, in dem der Benutzer einen CSS-Selektor angeben könnte. Wenn diese Bedingung auf der Website des Kunden ausgewertet wird, kann die Erweiterung nach Elementen suchen, die mit der CSS-Auswahl übereinstimmen, und die Information zurückgeben, ob sich eines davon im Ansichtsfenster des Benutzers befindet.

Bedingungstypen bestehen in der Regel aus (1) einer Ansicht, die in der Datenerfassungs-Benutzeroberfläche angezeigt wird und es Benutzern ermöglicht, die Einstellungen für die Bedingung zu ändern, und (2) einem Bibliotheksmodul, das in der Tag-Laufzeitbibliothek ausgegeben wird, um die Einstellungen zu interpretieren und eine Bedingung auszuwerten.

[Weitere Infos](./web/condition-types.md)

#### Aktionstypen {#action}

Eine Regelaktion ist eine Aktion, die ausgeführt wird, nachdem die Auswertung der Regelbedingungen erfolgreich war.

Beispielsweise könnte eine Erweiterung einen Aktionstyp „Support-Chat anzeigen“ bereitstellen, der einen Dialog mit dem Support-Chat anzeigen könnte, um Benutzern zu helfen, die beim Auschecken Probleme haben.

Aktionstypen bestehen in der Regel aus (1) einer Ansicht, die in der Datenerfassungs-Benutzeroberfläche angezeigt wird und es Benutzern ermöglicht, die Einstellungen für die Aktion zu ändern, und (2) einem Bibliotheksmodul, das in der Tag-Laufzeitbibliothek ausgegeben wird, um die Einstellungen zu interpretieren und eine Aktion durchzuführen.

[Weitere Infos](./web/action-types.md)

#### Datenelementtypen {#data-element}

Bei Datenelementen handelt es sich im Wesentlichen um Aliase zu Datensegmenten auf einer Seite, unabhängig davon, wo sich diese Daten im vom Server empfangenen Ereignis befinden. Ein Datenelement kann durch Regeln referenziert werden und dient als Abstraktion für den Zugriff auf diese Daten. Wenn sich der Speicherort der Daten in Zukunft ändert (beispielsweise wird der Ereignisschlüssel, der den Wert enthält, geändert), kann ein einzelnes Datenelement neu konfiguriert werden, wobei alle Regeln, die auf dieses Datenelement verweisen, unverändert bleiben können.

Datenelementtypen bestehen in der Regel aus (1) einer Ansicht, die in der Datenerfassungs-Benutzeroberfläche angezeigt wird und es Benutzern ermöglicht, die Einstellungen für das Datenelement zu ändern, und (2) einem Bibliotheksmodul, das in der Tag-Laufzeitbibliothek ausgegeben wird, um die Einstellungen zu interpretieren und Datenteile abzurufen.

[Weitere Infos](./web/data-element-types.md)

## Erweiterungskonfiguration

Die Konfiguration einer Erweiterung bezieht sich auf die Art und Weise, wie globale Einstellungen eines Benutzers erfasst werden. Betrachten Sie beispielsweise eine Erweiterung, die es dem Benutzer ermöglicht, mit der Aktion „Beacon senden“ ein Beacon zu senden, wobei das Beacon immer eine Konto-ID enthalten muss. Wir möchten den Benutzern ersparen, dass sie jedes Mal, wenn sie eine Aktion „Beacon senden“ konfigurieren, zur Eingabe der Konto-ID aufgefordert werden. Stattdessen sollte die Erweiterung die Konto-ID einmal in der Erweiterungskonfigurationsansicht abfragen. Jedes Mal, wenn ein Beacon gesendet werden soll, kann das Bibliotheksmodul für die Aktion „Beacon senden“ die Konto-ID aus der Erweiterungskonfiguration abrufen und dem Beacon hinzufügen.

Wenn Benutzer eine Erweiterung für eine Tag-Eigenschaft installieren, wird ihnen die Ansicht für die Erweiterungskonfiguration angezeigt. Sie können die Installation der Erweiterung nicht abschließen, ohne die Erweiterungskonfiguration abzuschließen.

Die Erweiterungskonfiguration besteht aus einer Ansichtskomponente, die Einstellungen exportiert, die dann in der Tag-Laufzeitbibliothek als Standardobjekt ausgegeben werden.

[Weitere Infos](./configuration.md)

## Struktur einer Erweiterung

Eine Erweiterung besteht aus einem Verzeichnis von Dateien. Eine Übersicht, wie diese Dateien strukturiert sein sollten, finden Sie im Folgenden. Details zum Dateiinhalt finden Sie in anderen Abschnitten.

Eine [`extension.json`](./manifest.md)-Datei muss im Stammverzeichnis vorhanden sein. Diese Datei beschreibt unter anderem den Aufbau der Erweiterung und wo sich bestimmte Dateien im Verzeichnis befinden. Dies weist einige Ähnlichkeiten zu einer [`package.json`](https://docs.npmjs.com/files/package.json)-Datei in [npm](https://www.npmjs.com/) auf.

Jedes Bibliotheksmodul (die Logik, die innerhalb der Tag-Laufzeitbibliothek ausgegeben wird) muss eine eigene Datei sein, deren Inhalt dem [CommonJS-Modulstandard](http://wiki.commonjs.org/wiki/Modules/1.1.1) folgt. Wenn wir zum Beispiel einen Aktionstyp „Beacon senden“ erstellen, muss eine Datei vorhanden sein, die die Logik zum Senden des Beacons enthält. Der Inhalt dieser Datei wird in der Tag-Laufzeitbibliothek ausgegeben. Sie könnten sie `sendBeacon.js` nennen. Der Speicherort der Datei im Verzeichnis ist nicht wichtig, da in `extension.json` beschrieben wird, wo sie sich befindet.

Jede Ansicht muss eine HTML-Datei sein, die in einen iframe innerhalb der Tags-Anwendung geladen werden kann. Die Ansicht muss ein von Tags bereitgestelltes Skript enthalten und mit einer kleinen API konform sein, um mit der Anwendung kommunizieren zu können. Es gibt keine Einschränkungen hinsichtlich der Verwendung von Bibliotheken in Ihren Ansichten. Mit anderen Worten, Sie können jQuery, Underscore, React, Angular, Bootstrap oder andere Bibliotheken verwenden. Wir hoffen jedoch, dass Ihre Erweiterung ein ähnliches Aussehen und eine ähnliche Bedienung wie die Applikation haben wird.

Es wird empfohlen, alle ansichtsbezogenen Dateien (HTML, CSS, JavaScript) in einem einzigen Unterverzeichnis abzulegen, das von den Bibliotheksmoduldateien getrennt ist. In `extension.json` beschreiben Sie, wo sich dieser Unterordner für die Ansichten befindet. Platform beliefert dann dieses Unterverzeichnis (und nur dieses Unterverzeichnis) von seinen Webservern.
