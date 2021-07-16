---
title: Entwickeln einer Erweiterung
description: Dieses Dokument bietet einen allgemeinen Überblick über den Entwicklungsprozess von Tag-Erweiterungen mit Links zur weiteren Dokumentation für detailliertere Prozesse.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 46%

---

# Entwickeln einer Erweiterung

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Eine Tag-Erweiterung sollte als (kleines) Produkt mit eigenen Anforderungen betrachtet werden. Wenn Sie bestimmen, wie ein Benutzer von Adobe Experience Platform Ihre Erweiterung am besten verwendet, kann Ihnen dies dabei helfen, die Funktionen nach den Ereignistypen, Bedingungstypen, Aktionstypen und Datenelementtypen zu sortieren, die Ihre Erweiterung bereitstellen sollte.

Mit diesem Wissen können Sie planen, welche Komponenten in Ihrer Erweiterung bereitgestellt werden sollen.

## Handbücher

Wenn ein Plan vorhanden ist, können diese Anleitungen Ihnen helfen, den Entwicklungsprozess einer Erweiterung besser zu verstehen:

* Die [Erste Schritte-Anleitung](../getting-started.md) und andere Dokumente unter **Erweiterungsentwicklung** im linken Navigationsbereich sind großartige Referenzmaterialien zum Verständnis von Erweiterungen. Sie enthalten Details dazu, was Erweiterungen tun können, wie Benutzerinformationen zwischen Ihrer Erweiterung und Adobe Experience Platform gespeichert und weitergegeben werden, wie Ihr Code in Bibliotheken gebündelt wird und wie Ihr Erweiterungscode zur Laufzeit im Browser interpretiert und verwendet wird.
* Das Tutorial-Video [Erweiterung](https://youtu.be/rxjtC9o4rl0) eignet sich hervorragend als Ausgangspunkt.
* Die YouTube-Wiedergabeliste [Einführung in Erweiterungen](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) führt durch den Prozess der Erstellung von Erweiterungspaketen.
* Artikel [JSON-Schema verstehen](https://spacetelescope.github.io/understanding-json-schema/index.html#).
* [JSON Lint/Validator](http://jsonlint.com/).
* [JSON-Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) Chrome-Erweiterung zum Hervorheben und Drucken von JSON &amp; JSONP.
* [jsonschema.net](https://jsonschema.net/#/editor) Editor, um ein JSON-Schema von Ihrem Objekt zu erstellen.
* [JSON-Schema-Validator](http://www.jsonschemavalidator.net/) Ein interaktiver JSON-Schema-Online-Validator.

## Werkzeuge

Es gibt auch eine Reihe von npm-Tools, die Sie bei der Entwicklung Ihres Erweiterungspakets unterstützen:

* [Das Gerüst-](https://www.npmjs.com/package/@adobe/reactor-scaffold) Toolkit für Tag-Erweiterungen erleichtert die Erstellung eines Einstiegsprojekts auf Ihrem lokalen Computer.
* [Tag-Erweiterung ](https://www.npmjs.com/package/@adobe/reactor-sandbox) Sandbox unterstützt Sie bei der Überprüfung Ihrer Erweiterungsansichten und -module auf Ihrem lokalen Computer.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-packager) Packager ist ein Befehlszeilenprogramm zum Verpacken einer Tag-Erweiterung in eine ZIP-Datei.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-uploader) Uploader ist ein interaktives Befehlszeilenwerkzeug, mit dem Sie Ihre technischen Kontoanmeldeinformationen eingeben und Ihr Erweiterungspaket auf Tags hochladen können.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-releaser) Releaser ist ein interaktives Befehlszeilenwerkzeug, mit dem Sie Ihre Erweiterung für die private Verfügbarkeit freigeben können.

## Beispiele für Erweiterungen

Es gibt Beispielerweiterungen auf GitHub, die Sie überprüfen oder als Starterprojekte verwenden können:

* [Beispielerweiterung „Hello World“](https://github.com/adobe/reactor-helloworld-extension)
* [Facebook-Beispielerweiterung](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Typekit-Beispielerweiterung](https://github.com/jeffchasin/extension-typekit)
* [Pinterest-Beispielerweiterung](https://github.com/jeffchasin/extension-pinterest)

## Slack-Arbeitsbereich

Sie können Zugriff auf den Slack-Community-Arbeitsbereich anfordern, in dem sich Erweiterungsautoren mithilfe dieses [Anforderungsformulars](http://join.launchdevelopers.chat) gegenseitig unterstützen können.

**Bitte beachten** Sie: Obwohl es in diesem Slack-Arbeitsbereich Adoben gibt, handelt es sich um eine Community-Ressource, die nicht von der Adobe gesponsert oder moderiert wird.
