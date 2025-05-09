---
title: Handbuch zur Fehlerbehebung bei Tags
description: Erhalten Sie Antworten auf häufig gestellte Fragen zu Tags in Adobe Experience Platform.
exl-id: c06b8e25-4d79-4a11-94da-94ac096b5e33
source-git-commit: 9701a14dc2915e0d6dcc6051c15d5113f305487f
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 89%

---

# Handbuch zur Fehlerbehebung bei Tags

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](./term-updates.md).

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Tags in Adobe Experience Platform.

## Was sind Tags?

Tags sind die in Adobe Experience Platform integrierten Tag-Management-Funktionen der nächsten Generation von Adobe. Tags bieten Clients folgende Möglichkeiten:

- Client-seitige Web-Produkte unter Verwendung von Integrationen, die als *Erweiterungen* bezeichnet werden, bereitstellen
- Konfigurationen zur Aktualisierung von Client-Implementierungen in nativen Apps dynamisch bereitstellen
- Daten konsistent erfassen, definieren, verwalten und für Marketing- und Werbeprodukte von anderen Anbietern und von Adobe freigeben.

Tags sind ein erweitertes Bereitstellungssystem für Code und Konfiguration, das Bedingungen auswertet und Aktionen ausführt, damit Client-seitige Bibliotheken und Produkte effizient bereitgestellt werden können. Sie bieten außerdem einen hochgradig skalierbaren Ansatz zum Verwalten und Erstellen von Integrationen und verfügen über einen robusten Satz von APIs für die programmgesteuerte Interaktion.

## Welche Kosten fallen für Tags an?

Durch Tags entstehen Ihnen keine zusätzlichen Kosten. Sie stehen jedem [!DNL Adobe Experience Cloud]-Kunden zur Verfügung.

## Ich habe gehört, dass es jetzt Plug-ins gibt. Was hat es damit auf sich?

Tags sind in Adobe Experience Platform integriert und vollständig erweiterbar. Kunden, Adobe-Partner, Agenturen und Anbieter von Marketing- oder Werbetechnologie können eine Tag-Erweiterung erstellen, die neue Funktionen hinzufügt oder vorhandene Funktionen ändert. Das System ermöglicht Partnern und Kunden das Erstellen, Verwalten und Aktualisieren eigener Integrationen. Dies ist nur eine Möglichkeit, wie wir Adobe Experience Platform öffnen, damit Kunden und Partner Produkte und Unternehmen darauf aufbauen können. Auf diese Weise kann alle Benutzer die Adobe-Technologie einfacher mit den Marketing- und Werbetechnologien anderer Anbieter verbinden.

## Sind alle Drittanbietererweiterungen sofort verfügbar?

Erweiterungen sind bereits für Lösungen von Adobe und eine große und wachsende Anzahl unabhängiger Anbieter und Technologien für Analyse, Marketing, Werbung und Zustimmung verfügbar. Wir arbeiten auch weiterhin mit unseren Partnern zusammen, um das Ökosystem zu erweitern. Da Erweiterungen von den Inhabern der Technologien erstellt, verwaltet und aktualisiert werden können, müssen Kunden nicht warten, bis sie von Adobe-Technikern erstellt werden.

## Wann können Kunden oder Partner Erweiterungen erstellen?

Das virtuelle Self-Service-Portal von Tags ermöglicht es Entwicklern von Erweiterungen, ihre eigenen Integrationen mit Adobe Cloud Platform zu erstellen.

Wir haben viele Kunden, die sich auch dafür entscheiden, ihre eigenen privaten Erweiterungen zu erstellen, die nur innerhalb ihres eigenen Unternehmens verwendet werden und die die gleichen Methoden zur Entwicklung von Erweiterungen verwenden.

Informationen zum Entwickeln einer Erweiterung finden Sie auf der Seite [Übersicht über die Entwicklung ](./extension-dev/overview.md) Erweiterungen“.

## Erfüllen Tags die Sicherheitsstandards meines Unternehmens?

Tags sind mit SOC-2 und dem Gramm-Leach-Bliley Act kompatibel. Tags bieten auch die Möglichkeit des Selbst-Hostings. JavaScript-Bibliotheken und mobile Konfigurationen können von Ihren eigenen Servern oder dem CDN Ihrer Wahl bereitgestellt werden. IT- und Sicherheitsteams können dadurch automatisierte Tests durchführen, die Dateien in ihrem eigenen Versionskontrollsystem prüfen und die internen Produktionsmigrationsprozesse (sicherheitsbezogene oder anderweitige) vollständig einhalten.

## Wann kann ich zu Tags wechseln?

Jetzt ist die beste Zeit, um zu Tags zu wechseln. Der Migrationsprozess macht es einfach, Ihre DTM-Eigenschaften in Tags zu kopieren. Wir empfehlen umfangreiche Tests, haben jedoch so viel wie möglich automatisiert (keine Änderungen am eingebetteten Code auf der Seite und automatisierte Migration von Regeln und Datenelementen).

## Unterstützen Tags Single Page Applications und mein bevorzugtes Framework?

Ja. Tags verfügen über Funktionen, mit denen Benutzer und Entwickler von Erweiterungen Daten in Single Page Applications oder Ajax-lastigen Seiten oder Sites flexibel sammeln, verwalten und verteilen können. Dies gilt unabhängig von den Voreinstellungen für das Entwicklungs-Framework. Dabei ist es unerheblich, ob es sich um Angular, React. js, Ember, Meteor o. Ä. handelt.

## Unterstützen Tags dynamische Datenschichten?

Ja. Tags enthalten eine Erweiterung, die auf das Überwachen von Änderungen in dynamischen Datenschichten spezialisiert ist.

## Welche Ereignistypen unterstützen Tags?

Ereignistypen sind über Erweiterungen verfügbar. Die Anzahl der unterstützten Ereignistypen variiert je nach Erweiterung. Die YouTube-Erweiterung umfasst beispielsweise vier Videoereignistypen: Wiedergabe, Pause, Ende und verstrichene Wiedergabezeit. Über Erweiterungen können Tags beliebige andere Browser-Eereignistypen oder künstliche Ereignistypen unterstützen, z. B. spezifische Besucheraktivitätssequenzen.

## Werden Tags meine Website beschleunigen (oder verlangsamen)?

Tags sind so konzipiert, dass Marketing- und Werbetechnologien mithilfe moderner Best-Practice-Verfahren auf Ihrer Website so effizient wie möglich bereitgestellt und ausgeführt werden. Es wurde nachgewiesen, dass Tags bei ordnungsgemäßer Verwendung die Performance von Websites gegenüber alternativen Methoden verbessern, die ähnliche Funktionen bieten.

## Welche Browser werden von Tags unterstützt?

Die unterstützten Browser ansehen [hier](./extension-dev/browsers.md).

Die meisten Adobe-Kunden nutzen mittlerweile modernere Web-Plattformfunktionen in aktuellen Browsern, um bessere Benutzererlebnisse zu erstellen, einschließlich Single Page Applications und interaktiver Ajax-lastiger Websites und Seiten. Da die meisten Kunden zu moderneren Konzepten für ihre Sites wechseln, fordern sie eine Lösung wie Tags, die diese Ansätze ermöglicht.

## Funktionieren Tags in nativen Mobile Apps?

Ja! Tags unterstützen jetzt mobile Eigenschaften und Konfiguration für die neuen Adobe Experience Platform [Mobile SDKs](https://sdkdocs.com), um die Datenerfassung und -bereitstellung in einer nativen Mobile-App-Umgebung zu implementieren. Weitere Informationen finden Sie in der [Dokumentation](https://sdkdocs.com).

## Warum gibt die Benutzeroberfläche an, dass beim Laden meines Kontos ein Fehler aufgetreten ist?

Wenn Sie eine Meldung erhalten, dass beim Laden Ihres Kontos ein Fehler aufgetreten ist, bedeutet dies, dass Ihr Konto zu keinem Produktprofil für Tags gehört. Informationen zum Konfigurieren eines Produktprofils in Adobe Admin Console[ um Zugriff auf Datenerfassungsfunktionen in der Benutzeroberfläche zu gewähren](../collection/permissions.md) finden Sie im Handbuch zum Verwalten von Berechtigungen .

## Warum kann ich in der Benutzeroberfläche keine Eigenschaften hinzufügen?

Wenn Sie bei der Benutzeroberfläche angemeldet sind und keine neuen Eigenschaften erstellen können, bedeutet dies, dass Ihr Konto zu keinem Produktprofil gehört, das über das Recht „Eigenschaften verwalten“ verfügt.

Informationen zum Konfigurieren eines Produktprofils in Adobe Admin Console, um das Recht „Eigenschaften verwalten“ zu gewähren, finden Sie im Handbuch zum [Verwalten von Berechtigungen](../collection/permissions.md). Weitere Informationen zu den unterschiedlichen Rechten für Tags finden Sie in der Übersicht zu [Benutzerberechtigungen für Tags](./ui/administration/user-permissions.md).

## Was ist, wenn ich weitere Fragen habe?

Wenn Sie weitere Fragen haben, können Sie diese auf der [Adobe Experience Platform-Datenerfassungs-Community](https://adobe.com/go/launchme)Seite auf Experience League stellen oder dem [Community-Slack-](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform)&quot; für Entwickler und technische Implementierungsthemen beitreten.
