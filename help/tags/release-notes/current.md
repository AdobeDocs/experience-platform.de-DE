---
title: Versionshinweise
description: Die aktuellen Versionshinweise für Tags in Adobe Experience Platform.
source-git-commit: 7a6bec77895458cf1735bc7a00d16b78df9776a5
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 67%

---

# Versionshinweise

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../term-updates.md).

## 17. Mai 2021

**Bessere Handhabung nicht gespeicherter Änderungen**: Jedes Mal, wenn Sie eine Einstellungsansicht verlassen haben (Erweiterungen, Datenelemente und Regelkomponenten), haben Sie eine Eingabeaufforderung mit der Frage erhalten, ob Sie Ihre Änderungen verwerfen möchten. Obwohl dies nicht logisch erschien, wurden meistens Änderungen gespeichert, auch wenn es keine gab.  Dieser Fehler wurde behoben.  Von jetzt sehen Sie diese Eingabeaufforderung nur mehr, wenn Sie tatsächlich Änderungen vorgenommen haben.

## 10. Mai 2021

**Vereinfachte Veröffentlichung**: Die Erstellung in der Staging-Umgebung ist nicht mehr erforderlich.  Wenn Sie über die entsprechenden Berechtigungen verfügen, können Sie den Status „Gesendet“ vollständig überspringen und direkt in der Entwicklungsumgebung veröffentlichen, solange Sie einen erfolgreichen Build haben und es keine anderen nachgelagerten Bibliotheken gibt.

## 22. April 2021

**Datenerfassung in Adobe Experience Platform** : Beim Senden von Daten an Adobe geht es nicht nur darum, Tags auf Ihrer Site oder in Ihrer Konfiguration in Ihrer App bereitzustellen.  Die Verwendung der Experience Platform-SDKs und von Edge Network erfordert Zugriff auf andere Funktionen von Platform. Dies erforderte früher die Anmeldung bei mehreren verschiedenen Tools; diese befinden sich nun alle an einem Ort.

Die Datenerfassung in Platform besteht aus sechs Funktionen. Ihre neu optimierte Navigation enthält nur die Elemente, auf die Ihr Unternehmen und Ihr Benutzerkonto Zugriff haben.  Einige der Funktionsnamen wurden ebenfalls aktualisiert, damit sie den üblichen Benennungsmustern von Experience Platform entsprechen.

* Client (zuvor als Client-Seite aufgerufen)
* Datastreams (früher als Edge-Konfigurationen aufgerufen)
* Server (zuvor als Server-seitig aufgerufen)
* Programmkonfigurationen
* Schemas
* Identitäten

Mit der Weiterentwicklung von Experience Platform und der Datenerfassung können Sie sich auf weitere Updates freuen.

## 18. Februar 2021

* Aktualisierung der Datenerfassungs-Benutzeroberfläche auf React-Spektrum v3
* Die Karten zu Erweiterungen wurden auf die neuesten Spectrum-Muster aktualisiert.
* Im gesamten Programm wurden die Namensfelder vergrößert.

## 13. Januar 2021

**Allgemeine Verfügbarkeit: Ereignisweiterleitung** Senden Sie Daten auf Ereignisebene an das Adobe Experience Platform Edge Network und verwenden Sie dann die Ereignisweiterleitung, um diese Daten umzuwandeln, anzureichern und mit geringer Latenz an einen Endpunkt ohne Adobe zu senden, indem Sie die Server der Adobe und nicht den Client verwenden.

Weitere Informationen finden Sie im Leitfaden [Ereignisweiterleitung](../ui/event-forwarding/overview.md) und [Erste Schritte](../ui/event-forwarding/getting-started.md) .
