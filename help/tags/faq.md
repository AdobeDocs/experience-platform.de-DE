---
title: Handbuch zur Fehlerbehebung bei Tags
description: Erhalten Sie Antworten auf häufig gestellte Fragen zu Tags in Adobe Experience Platform.
source-git-commit: dc957372e5e8c6f034f2e0cd0283e0e997501ba8
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 26%

---

# Handbuch zur Fehlerbehebung bei Tags

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](./term-updates.md).

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Tags in Adobe Experience Platform.

## Was sind Tags?

Tags sind die in Adobe Experience Platform integrierten Tag-Management-Funktionen der nächsten Generation von Adobe. Tags ermöglichen Clients Folgendes:

- Client-seitige Web-Produkte unter Verwendung von Integrationen, die als *Erweiterungen* bezeichnet werden, bereitstellen
- Konfigurationen zur Aktualisierung von Client-Implementierungen in nativen Apps dynamisch bereitstellen
- Daten konsistent erfassen, definieren, verwalten und für Marketing- und Werbeprodukte von anderen Anbietern und von Adobe freigeben.

Tags sind ein erweitertes Bereitstellungssystem für Code und Konfiguration, das Bedingungen auswertet und Aktionen ausführt, um Client-seitige Bibliotheken und Produkte effizient und effektiv bereitzustellen. Sie bieten außerdem einen hochgradig skalierbaren Ansatz für die Verwaltung und Erstellung von Integrationen und verfügen über einen robusten Satz von APIs für programmatische Interaktionen.

## Wie viel kosten Tags?

Für Tags fallen keine zusätzlichen Gebühren an. Sie stehen jedem [!DNL Adobe Experience Cloud]-Kunden zur Verfügung.

## Ich habe gehört, dass es jetzt Plug-ins gibt. Was hat es damit auf sich?

Tags sind in Adobe Experience Platform integriert und vollständig erweiterbar. Kunden, Adobe-Partner, Agenturen und Anbieter von Marketing- oder Werbetechnologie können eine Tag-Erweiterung erstellen, die neue Funktionen hinzufügt oder vorhandene Funktionen ändert. Das System ermöglicht Partnern und Kunden das Erstellen, Verwalten und Aktualisieren eigener Integrationen. Dies ist nur eine Möglichkeit, wie die Adobe die Adobe Experience Platform öffnet, damit Kunden und Partner Produkte und Unternehmen darauf aufbauen können. Auf diese Weise kann alle Benutzer die Adobe-Technologie einfacher mit den Marketing- und Werbetechnologien anderer Anbieter verbinden.

## Sind alle Drittanbietererweiterungen sofort verfügbar?

Erweiterungen sind bereits für Adobe-Lösungen sowie eine große und wachsende Anzahl unabhängiger Anbieter und Technologien für Analyse, Marketing, Werbung und Zustimmung verfügbar. Wir arbeiten auch weiterhin mit unseren Partnern zusammen, um das Ökosystem zu erweitern. Da Erweiterungen von den Technologieeigentümern erstellt, verwaltet und aktualisiert werden können, müssen Kunden nicht warten, bis sie von der Adobe Engineering erstellt werden.

## Wann können Kunden oder Partner Erweiterungen erstellen?

Tags haben sein Self-Service-Portal geöffnet, über das Erweiterungsentwickler eigene Integrationen mit der Adobe Cloud Platform erstellen können.

Wir haben viele Kunden, die sich auch dafür entscheiden, ihre eigenen privaten Erweiterungen zu erstellen, die nur innerhalb ihres eigenen Unternehmens verwendet werden und die die gleichen Methoden zur Entwicklung von Erweiterungen verwenden.

## Erfüllen Tags die Sicherheitsstandards meines Unternehmens?

Tags sind SOC-2 und Gramm-Leach-Bliley Act bereit. Tags bieten auch die Möglichkeit, selbstständig gehostet zu werden. JavaScript-Bibliotheken und mobile Konfigurationen können von Ihren eigenen Servern oder dem CDN Ihrer Wahl bereitgestellt werden. IT- und Sicherheitsteams können dadurch automatisierte Tests durchführen, die Dateien in ihrem eigenen Versionskontrollsystem prüfen und die internen Produktionsmigrationsprozesse (sicherheitsbezogene oder anderweitige) vollständig einhalten.

## Wann kann ich zu Tags wechseln?

Jetzt ist die beste Zeit, um zu Tags zu wechseln. Der Migrationsprozess erleichtert das Kopieren Ihrer DTM-Eigenschaften in Tags. Wir empfehlen umfangreiche Tests, haben jedoch so viel wie möglich automatisiert (keine Änderungen am eingebetteten Code auf der Seite und automatisierte Migration von Regeln und Datenelementen).

## Unterstützen Tags Einzelseiten-Apps und mein bevorzugtes Framework?

Ja. Tags bieten Benutzern und Entwicklern von Erweiterungen die Möglichkeit, Daten innerhalb von Einzelseiten-App-Erlebnissen oder Ajax-lastigen Seiten oder Sites zu erfassen, zu verwalten und zu verteilen. Dies gilt unabhängig von den Voreinstellungen für das Entwicklungs-Framework. Dabei ist es unerheblich, ob es sich um Angular, React. js, Ember, Meteor o. Ä. handelt.

## Unterstützen Tags dynamische Datenschichten?

Ja. Tags enthalten eine Erweiterung, die auf das Überwachen von Änderungen in dynamischen Datenschichten spezialisiert ist.

## Welche Ereignistypen unterstützen Tags?

Ereignistypen sind über Erweiterungen verfügbar. Die Anzahl der unterstützten Ereignistypen variiert je nach Erweiterung. Die YouTube-Erweiterung umfasst beispielsweise vier Videoereignistypen: Wiedergabe, Pause, Ende und verstrichene Wiedergabezeit. Über Erweiterungen können Tags beliebige andere Browserereignistypen oder künstliche Ereignistypen unterstützen, z. B. bestimmte Besucheraktivitätssequenzen.

## Werden Tags meine Website beschleunigen (oder verlangsamen)?

Mit Tags können Sie mithilfe der heutigen Best Practices so effizient wie möglich Marketing- und Werbetechnologien auf Ihrer Website bereitstellen und ausführen. Bei ordnungsgemäßer Verwendung wurde nachgewiesen, dass Tags die Leistung von Websites gegenüber alternativen Methoden, die ähnliche Funktionen bieten, verbessern.

## Welche Browser werden von Tags unterstützt?

Browserunterstützung für Tags:

- [!DNL Chrome] (neueste Version)
- [!DNL Safari] (neueste Version)
- [!DNL Firefox] (neueste Version)
- [!DNL Microsoft Edge] (neueste Version)
- [!DNL Internet Explorer] (10 und höher)
- [!DNL iOS Safari] (neueste Version)
- [!DNL Android Chrome] (neueste Version)

Browserunterstützung für die Benutzeroberfläche der Tags-Anwendung:

- [!DNL Chrome] (neueste Version)
- [!DNL Safari] (neueste Version)
- [!DNL Firefox] (neueste Version)
- [!DNL Microsoft Edge] (neueste Version)

Die meisten Adobe-Clients nutzen modernere Webplattformfunktionen in aktuellen Browsern, um bessere Benutzererlebnisse zu bieten, einschließlich Einzelseitenanwendungen und interaktiver Ajax-lastiger Websites und Seiten. Da die meisten Kunden zu moderneren Ansätzen für ihre Sites wechseln, fordern sie eine Lösung wie Tags, die diese Ansätze ermöglicht.

## Funktionieren Tags in nativen mobilen Apps?

Ja! Tags unterstützen jetzt mobile Eigenschaften und Konfigurationen für die neuen Adobe Experience Platform [Mobile SDKs](https://sdkdocs.com), um die Datenerfassung und -bereitstellung in einer nativen mobilen App-Umgebung zu implementieren. Weitere Informationen finden Sie in der [Dokumentation](https://sdkdocs.com).

## Warum gibt die Benutzeroberfläche an, dass beim Laden meines Kontos ein Fehler aufgetreten ist?

Wenn Sie eine Meldung erhalten, dass beim Laden Ihres Kontos ein Fehler aufgetreten ist, bedeutet dies, dass Ihr Konto nicht zu Produktprofilen für Tags gehört. Informationen zum Konfigurieren eines Produktprofils in Adobe Admin Console, um Zugriff auf die Datenerfassungs-Benutzeroberfläche zu gewähren, finden Sie im Handbuch zu [Verwalten von Berechtigungen](./ui/administration/manage-permissions.md) .

## Warum kann ich in der Benutzeroberfläche keine Eigenschaften hinzufügen?

Wenn Sie keine neuen Eigenschaften erstellen können, wenn Sie bei der Datenerfassungs-Benutzeroberfläche angemeldet sind, bedeutet dies, dass Ihr Konto nicht zu einem Produktprofil gehört, das über das Recht &quot;Eigenschaften verwalten&quot;verfügt.

Informationen zum Konfigurieren eines Produktprofils in Adobe Admin Console, um das Recht &quot;Eigenschaften verwalten&quot;zu gewähren, finden Sie im Handbuch zu [Verwalten von Berechtigungen](./ui/administration/manage-permissions.md) . Weitere Informationen zu den unterschiedlichen Berechtigungen für Tags finden Sie in der Übersicht zu [Benutzerberechtigungen für Tags](./ui/administration/user-permissions.md).

## Was ist, wenn ich weitere Fragen habe?

Wenn Sie weitere Fragen haben, stellen Sie bitte in der Adobe Community auf der Haupt-Tag-Seite unter [https://adobe.com/go/launchme](https://adobe.com/go/launchme).

Tags sind nur ein Beispiel dafür, wohin unsere Plattform führt: offener, stärker integriert und wie immer dem Kundenerfolg gewidmet.
