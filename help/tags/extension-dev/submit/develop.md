---
title: Entwickeln einer Erweiterung
description: Dieses Dokument bietet einen allgemeinen Überblick über den Entwicklungsprozess von Tag-Erweiterungen mit Links zu weiterführender Dokumentation für detailliertere Prozesse.
exl-id: fb2f7275-a5da-4a41-b915-822c71c02e5c
source-git-commit: 3f5e432ef381c10d8197724783135637d01a120e
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 92%

---

# Entwickeln einer Erweiterung

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Eine Tag-Erweiterung sollte als (kleines) Produkt mit eigenen Anforderungen angesehen werden. Wenn Sie bestimmen, wie ein Benutzer von Adobe Experience Platform Ihre Erweiterung am besten verwendet, kann Ihnen dies dabei helfen, die Funktionen nach den Ereignistypen, Bedingungstypen, Aktionstypen und Datenelementtypen zu sortieren, die Ihre Erweiterung bereitstellen sollte.

Mit diesem Wissen können Sie planen, welche Komponenten in Ihrer Erweiterung bereitgestellt werden sollen.

## Handbücher

Wenn ein Plan vorhanden ist, können diese Anleitungen Ihnen helfen, den Entwicklungsprozess einer Erweiterung besser zu verstehen:

* Das [Erste-Schritte-Handbuch](../getting-started.md) und andere Dokumente unter **Erweiterungsentwicklung** im linken Navigationsbereich sind großartige Referenzmaterialien zum Verständnis von Erweiterungen. Sie enthalten Details dazu, was Erweiterungen tun können, wie Benutzerinformationen zwischen Ihrer Erweiterung und Adobe Experience Platform gespeichert und weitergegeben werden, wie Ihr Code in Bibliotheken gebündelt wird und wie Ihr Erweiterungs-Code zur Laufzeit im Browser interpretiert und verwendet wird.
* Artikel [JSON-Schema verstehen](https://spacetelescope.github.io/understanding-json-schema/index.html#).
* [JSON-Link/Validator](https://jsonlint.com/).
* [JSON-Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) Chrome-Erweiterung zum Hervorheben und Drucken von JSON &amp; JSONP.
* [jsonschema.net](https://jsonschema.net/#/editor)-Editor, mit dem Sie ein JSON-Schema aus Ihrem -Objekt erstellen können.
* [JSON-Schema-Validator](https://www.jsonschemavalidator.net) Ein interaktiver JSON-Schema-Online-Validator.

## Werkzeuge

Es gibt auch eine Reihe von npm-Tools, die Sie bei der Entwicklung Ihres Erweiterungspakets unterstützen:

* Mit dem [Strukturvorlagen-Tool für Tag-Erweiterungen](https://www.npmjs.com/package/@adobe/reactor-scaffold) können Sie auf Ihrem lokalen Computer leicht ein Einstiegsprojekt erstellen.
* Die [Tag-Erweiterungs-Sandbox](https://www.npmjs.com/package/@adobe/reactor-sandbox) unterstützt Sie bei der Überprüfung der Ansichten und Module Ihrer Erweiterungen auf Ihrem lokalen Computer.
* [Tag Extension Packager](https://www.npmjs.com/package/@adobe/reactor-packager) ist ein Befehlszeilenprogramm zum Verpacken einer Tag-Erweiterung in eine ZIP-Datei.
* [Tag Extension Uploader](https://www.npmjs.com/package/@adobe/reactor-uploader) ist ein interaktives Befehlszeilen-Tool, mit dem Sie die Anmeldedaten für Ihr technisches Konto eingeben und Ihr Erweiterungspaket zu Tags hochladen können.
* [Tag Extension Releaser](https://www.npmjs.com/package/@adobe/reactor-releaser) ist ein interaktives Befehlszeilen-Tool, mit dem Sie Ihre Erweiterung für die private Verfügbarkeit freigeben können.

## Beispiele für Erweiterungen

Sie können Beispielerweiterungen von GitHub, wie z. B. die [Hello World-Beispielerweiterung](https://github.com/adobe/reactor-helloworld-extension), als Ausgangsprojekte überprüfen oder verwenden.

## Slack-Arbeitsbereich

Sie können Zugriff auf den Slack-Community-Arbeitsbereich anfordern, in dem sich Erweiterungsautoren mithilfe dieses [Anfrageformulars](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform) gegenseitig unterstützen können.

**Bitte beachten Sie**: Obwohl es in diesem Slack-Arbeitsbereich auch Mitglieder von Adobe gibt, handelt es sich hier um eine Community-Ressource, die nicht von Adobe gesponsert oder moderiert wird.
