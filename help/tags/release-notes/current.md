---
title: Versionshinweise
description: Die neuesten Versionshinweise für Tags in Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 100%

---

# Versionshinweise

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../term-updates.md).

## 19. Juli 2021

**Anpassungen des Rechts „Eigenschaften verwalten“**: Bei dem Recht „Eigenschaften verwalten“ trat ein Problem auf, bei dem ein Benutzer berechtigt war, eine neue Eigenschaft zu erstellen, sie jedoch nach der Erstellung nicht sehen konnte (wie [hier](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/technical-advisory-adjustments-to-the-manage-properties/ba-p/399176?profile.language=de) im Community-Thread beschrieben). Eine Korrektur ist jetzt verfügbar mit Berechtigungen, die erzwungen werden, wie im Artikel beschrieben.

>[!NOTE]
>
>Wenn Sie einer Benutzergruppe das neue Recht „Eigenschaft bearbeiten“ zuweisen, wird die Benutzeroberfläche nicht aktualisiert, um die Felder im Eigenschaftenkonfigurations-Bildschirm zu aktivieren. Eine Korrektur dieses Problems wird in einer kommenden Version implementiert.

## 17. Mai 2021

**Bessere Handhabung nicht gespeicherter Änderungen**: Jedes Mal, wenn Sie eine Einstellungsansicht verlassen haben (Erweiterungen, Datenelemente und Regelkomponenten), haben Sie eine Eingabeaufforderung mit der Frage erhalten, ob Sie Ihre Änderungen verwerfen möchten. Obwohl dies nicht logisch erschien, wurden meistens Änderungen gespeichert, auch wenn es keine gab.  Dieser Fehler wurde behoben.  Von jetzt sehen Sie diese Eingabeaufforderung nur mehr, wenn Sie tatsächlich Änderungen vorgenommen haben.

## 10. Mai 2021

**Vereinfachte Veröffentlichung**: Die Erstellung in der Staging-Umgebung ist nicht mehr erforderlich.  Wenn Sie über die entsprechenden Berechtigungen verfügen, können Sie den Status „Gesendet“ vollständig überspringen und direkt in der Entwicklungsumgebung veröffentlichen, solange Sie einen erfolgreichen Build haben und es keine anderen nachgelagerten Bibliotheken gibt.

## 22. April 2021

**Datenerfassung in Adobe Experience Platform** - Beim Senden von Daten an Adobe geht es nicht nur darum, Tags auf Ihrer Site bereitzustellen oder Ihre App zu konfigurieren.  Die Verwendung der Experience Platform-SDKs und von Edge Network erfordert Zugriff auf andere Funktionen von Platform. Dies erforderte früher die Anmeldung bei mehreren verschiedenen Tools; diese befinden sich nun alle an einem Ort.

Die Datenerfassung in Platform umfasst sechs Funktionen. Ihre neu optimierte Navigation enthält nur die Elemente, auf die Ihr Unternehmen und Ihr Benutzerkonto Zugriff haben. Einige der Funktionsnamen wurden ebenfalls aktualisiert, damit sie den üblichen Benennungsmustern von Experience Platform entsprechen.

* Client (zuvor als Client-Seite aufgerufen)
* Datastreams (früher als Edge-Konfigurationen aufgerufen)
* Server (zuvor als Server-seitig aufgerufen)
* Programmkonfigurationen
* Schemas
* Identitäten

Mit der Weiterentwicklung von Experience Platform und der Datenerfassung können Sie sich auf weitere Updates freuen.

## 18. Februar 2021

* Aktualisierung der Datenerfassungs-Benutzeroberfläche auf React Spectrum v3
* Die Karten zu Erweiterungen wurden auf die neuesten Spectrum-Muster aktualisiert.
* Im gesamten Programm wurden die Namensfelder vergrößert.

## 13. Januar 2021

**Allgemeine Verfügbarkeit: Ereignisweiterleitung** Senden Sie Daten auf Ereignisebene an das Adobe Experience Platform Edge Network und verwenden Sie dann die Ereignisweiterleitung, um diese Daten mithilfe der Server von Adobe und nicht des Clients mit geringer Latenz zu transformieren, anzureichern und an einen Drittanbieter-Endpunkt zu senden.

Weitere Informationen finden Sie in der [Übersicht über die Ereignisweiterleitung](../ui/event-forwarding/overview.md) und im [Erste-Schritte-Handbuch](../ui/event-forwarding/getting-started.md).
