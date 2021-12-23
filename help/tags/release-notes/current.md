---
title: Versionshinweise
description: Die neuesten Versionshinweise für Tags in Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: 2056f7f6e7372fa1dee2e975a75e7ba3b8dfe518
workflow-type: ht
source-wordcount: '658'
ht-degree: 100%

---

# Versionshinweise

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../term-updates.md).

## 15. November 2021

**Akzeptieren von ES6-Code in Tags** - Erweiterungen und benutzerdefinierter Code, der ES6-Code enthält, können jetzt in Tags verwendet werden. Im Erweiterungskatalog sehen Sie einen ES6+-Titel innerhalb der Karte jeder Erweiterung, die ES6-Code enthält. IE10 und IE11 unterstützen ES6-Code nicht. Bevor Sie ES6-Code in Ihren Tags-Bibliotheken verwenden, lassen Sie die erforderliche Sorgfalt walten.

**Verwenden von Terser als JavaScript-Kompressor** - Uglifier wurde durch Terser ersetzt. Ab dieser Version werden alle Tags-Bibliotheken von Terser minifiziert.

## 21. Oktober 2021

**Senden von Daten an authentifizierte Endpunkte bei der Ereignisweiterleitung** - Mithilfe von geheimen Daten können Sie Daten an Endpunkte senden, für die die folgenden Authentifizierungsprotokolle erforderlich sind:

* **[!UICONTROL Token]** - Eine einzelne Zeichenfolge, die den Wert eines Authentifizierungs-Token darstellt.
* **[!UICONTROL Einfaches HTTP]** - Enthält zwei Zeichenfolgen-Attribute für einen Benutzernamen und ein Kennwort.
* **[!UICONTROL OAuth2]** - Enthält mehrere Attribute zur Unterstützung der [OAuth2](https://datatracker.ietf.org/doc/html/rfc6749)-Spezifikation.

Weitere Informationen finden Sie in den Handbüchern unter [Verwalten von geheimen Daten in der Datenerfassungs-Benutzeroberfläche](../ui/event-forwarding/secrets.md) oder [Verwalten von geheimen Daten in der Reactor-API](../api/guides/secrets.md).

## 19. Juli 2021

**Anpassungen des Rechts „Eigenschaften verwalten“** - Bei dem Recht „Eigenschaften verwalten“ trat ein Problem auf, bei dem ein Benutzer berechtigt war, eine neue Eigenschaft zu erstellen, sie jedoch nach der Erstellung nicht sehen konnte (wie [hier](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/technical-advisory-adjustments-to-the-manage-properties/ba-p/399176?profile.language=de) im Community-Thread beschrieben). Eine Korrektur ist jetzt verfügbar mit Berechtigungen, die erzwungen werden, wie im Artikel beschrieben.

>[!NOTE]
>
>Wenn Sie einer Benutzergruppe das neue Recht „Eigenschaft bearbeiten“ zuweisen, wird die Benutzeroberfläche nicht aktualisiert, um die Felder im Eigenschaftenkonfigurations-Bildschirm zu aktivieren. Eine Korrektur dieses Problems wird in einer kommenden Version implementiert.

## 17. Mai 2021

**Bessere Handhabung nicht gespeicherter Änderungen** - Jedes Mal, wenn Sie eine Einstellungsansicht verlassen haben (Erweiterungen, Datenelemente und Regelkomponenten), haben Sie eine Eingabeaufforderung mit der Frage erhalten, ob Sie Ihre Änderungen verwerfen möchten. Obwohl dies nicht logisch erschien, wurden meistens Änderungen gespeichert, auch wenn es keine gab. Dieser Fehler wurde behoben. Von jetzt sehen Sie diese Eingabeaufforderung nur mehr, wenn Sie tatsächlich Änderungen vorgenommen haben.

## 10. Mai 2021

**Vereinfachte Veröffentlichung** - Die Erstellung in der Staging-Umgebung ist nicht mehr erforderlich. Wenn Sie über die entsprechenden Berechtigungen verfügen, können Sie den Status „Gesendet“ vollständig überspringen und direkt in der Entwicklungsumgebung veröffentlichen, solange Sie einen erfolgreichen Build haben und es keine anderen nachgelagerten Bibliotheken gibt.

## 22. April 2021

**Datenerfassung in Adobe Experience Platform** - Beim Senden von Daten an Adobe geht es nicht nur darum, Tags auf Ihrer Site bereitzustellen oder Ihre App zu konfigurieren. Die Verwendung der Experience Platform-SDKs und von Edge Network erfordert Zugriff auf andere Funktionen von Platform. Dies erforderte früher die Anmeldung bei mehreren verschiedenen Tools; diese befinden sich nun alle an einem Ort.

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

**Allgemeine Verfügbarkeit: Ereignisweiterleitung** - Senden Sie Daten auf Ereignisebene an das Adobe Experience Platform Edge Network und verwenden Sie dann die Ereignisweiterleitung, um diese Daten mithilfe der Server von Adobe und nicht des Clients mit geringer Latenz zu transformieren, anzureichern und an einen Drittanbieter-Endpunkt zu senden.

Weitere Informationen finden Sie in der [Übersicht über die Ereignisweiterleitung](../ui/event-forwarding/overview.md) und im [Erste-Schritte-Handbuch](../ui/event-forwarding/getting-started.md).
