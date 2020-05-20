---
title: Adobe Experience Platform  – Versionshinweise
description: Versionshinweise zur Experience Platform vom 15. Januar 2020
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 9%

---


# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 15. Januar 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](#xdm)
* [Privacy Service](#privacy)
* [Quellen](#sources)
* [Ziele](#destinations)

## Erlebnis-Datenmodell (XDM)-System {#xdm}

Standardisierung und Interoperabilität sind Schlüsselkonzepte der Experience Platform. Das von Adobe unterstützte Experience Data Model (XDM) ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schema für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten auf der Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Audiencen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Feldtypeinschränkungen für Felder gleicher Hierarchie | Nachdem ein XDM-Feld als ein bestimmter Typ definiert wurde, müssen alle anderen Felder mit demselben Namen und derselben Hierarchie unabhängig von den Klassen oder Mixins, in denen sie verwendet werden, denselben Feldtyp verwenden. Wenn beispielsweise ein Mixin für die XDM-Profil-Klasse ein `profile.age` Feld vom Typ &quot;integer&quot;enthält, kann ein ähnliches Mixin für XDM ExperienceEvent kein Feld vom Typ &quot;string&quot; `profile.age` aufweisen. Um einen anderen Feldtyp zu verwenden, muss das Feld eine andere Hierarchie aufweisen als das zuvor definierte Feld (z. B. `profile.person.age`). Diese Funktion soll Konflikte verhindern, wenn Schema in einer Vereinigung zusammengeführt werden. Die Beschränkung wirkt sich nicht rückwirkend auf vorhandene Schema aus. Es wird jedoch dringend empfohlen, Ihre Schema auf Feldkonflikte zu überprüfen und sie nach Bedarf zu bearbeiten. |
| Groß-/Kleinschreibung bei der Feldüberprüfung | Benutzerdefinierte Felder auf derselben Ebene müssen unabhängig von der Groß-/Kleinschreibung unterschiedliche Namen haben. Wenn Sie beispielsweise ein benutzerdefiniertes Feld mit dem Namen &quot;E-Mail&quot;hinzufügen, können Sie kein weiteres benutzerdefiniertes Feld mit dem Namen &quot;E-Mail&quot;hinzufügen. |

**Bekannte Probleme**

* Keine

Weitere Informationen zum Arbeiten mit XDM mithilfe der Schema Registry API und Schema Editor Benutzeroberfläche finden Sie in der [XDM-Systemdokumentation](../../xdm/home.md).

## Privacy Service {#privacy}

Die neuen gesetzlichen und organisatorischen Vorschriften geben den Nutzern das Recht, auf ihre personenbezogenen Daten auf Anfrage aus Ihren Datenspeichern zuzugreifen oder sie zu löschen. Der Datenschutzdienst für Adobe Experience Platform stellt eine RESTful-API und eine Benutzeroberfläche bereit, mit der Sie diese Datenanforderungen Ihrer Kunden verwalten können. Mit dem Datenschutzdienst können Sie Anfragen zum Zugriff auf und Löschen von persönlichen oder privaten Kundendaten aus Adobe Experience Cloud-Anwendungen stellen, wodurch die automatische Einhaltung der gesetzlichen und organisatorischen Datenschutzbestimmungen erleichtert wird.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Umbenennung des Datenschutzdienstes | Der zuvor genannte &quot;GDPR-Dienst&quot;wurde in den Datenschutzdienst umbenannt, da der Dienst zunehmend andere Vorschriften zusätzlich zum GDPR unterstützt. |
| Neue API-Endpunkte | Der Basispfad für die Datenschutzdienst-API wurde von `/data/privacy/gdpr` auf aktualisiert `/data/core/privacy/jobs`. |
| Neue erforderliche `regulation` Eigenschaft | Bei der Erstellung neuer Aufträge in der Datenschutzdienst-API muss eine `regulation` Eigenschaft in der Anforderungs-Nutzlast angegeben werden, unter welcher Regel der Auftrag verfolgt werden soll. Die zulässigen Werte sind `gdpr` und `ccpa`. |
| Unterstützung der Adobe Primetime-Authentifizierung | Der Datenschutzdienst akzeptiert jetzt Zugriff-/Löschanforderungen aus der Adobe Primetime-Authentifizierung, wobei `primetimeAuthentication` als Produktwert verwendet wird. |
| Verbesserungen der Benutzeroberfläche des Datenschutzdienstes | Separate Auftragsverfolgungsseiten für GDPR- und CCPA-Regeln. Neues _Regeltyp_ -Dropdown, um zwischen den Verfolgungsdaten für GDPR und CCPA zu wechseln. |

**Bekannte Probleme**

* Keine

Weitere Informationen zum Datenschutzdienst finden Sie in der Übersicht über den [Datenschutzdienst](../../privacy-service/home.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen, während Sie diese Daten mithilfe von Plattformdiensten strukturieren, beschriften und verbessern können. Sie können Daten aus verschiedenen Quellen erfassen, z. B. Adobe-Anwendungen, Cloud-basierte Datenspeicherung, Drittanbieter-Software und Ihr CRM-System.

Experience Platform bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie Quellverbindungen für verschiedene Datenanbieter einfach einrichten können. Diese Quellverbindungen ermöglichen Ihnen die Authentifizierung und Verbindung zu externen Datenspeicherung- und CRM-Diensten, die Festlegung von Zeiten für die Erfassungsausführung und die Verwaltung des Datenaufkommens.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Unterstützung für Kundenattributdaten | UI- und API-Unterstützung zum Erstellen von Streaming-Connectors zum Erfassen von Kundenattributdaten. |
| Zusätzliche Dateiformatunterstützung für Cloud-Datenspeicherung | Die Dateierfassung aus Cloud-Datenspeicherung unterstützt jetzt XDM-konforme Dateiformate wie Parquet und JSON. |
| Unterstützung für Zugriffskontrollen | Das Zugriffskontrolle-Framework in Adobe Experience Platform bietet die erforderlichen Berechtigungen, um bei der Datenerfassung Zugriff auf die Quellen zu gewähren. Je nach Berechtigungsstufe kann ein Benutzer Ansichten- und Quelldateien ausführen, Quellen verwalten oder den Zugriff ganz verweigern. |

**Berechtigungen für Zugriffskontrollen**

| Kategorie | Berechtigung | Beschreibung |
|--- | --- | ---|
| Dateneinbindung | Quellen verwalten | Zugriff zum Lesen, Erstellen, Bearbeiten und Deaktivieren von Quellen. |
| Dateneinbindung | Ansichten-Quellen | Schreibgeschützter Zugriff auf verfügbare Quellen auf der Registerkarte &quot; *Katalog* &quot;und authentifizierte Quellen auf der Registerkarte &quot; *Durchsuchen* &quot;. |

**Bekannte Probleme**

* Keine

For more information about sources, see the [sources overview](../../sources/home.md)

## Ziele {#destinations}

In [Adobe Echtzeit-CDP](../../rtcdp/overview.md)sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten auf nahtlose Weise für diese Partner aktivieren.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Unterstützung für Zugriffskontrollen | Die Funktion Ziele in der Echtzeit-Kundendatenplattform funktioniert mit Zugangssteuerungsberechtigungen von Adobe Experience Platform. Je nach Berechtigungsstufe Ihres Anwenders können Sie Ziele anzeigen, verwalten und aktivieren. |

**Berechtigungen für Zugriffskontrollen**

| Kategorie | Berechtigung | Beschreibung |
|--- | --- | ---|
| Ziele | Ziele verwalten | Zugriff auf das Lesen, Erstellen, Bearbeiten und Deaktivieren von Zielen. |
| Ziele | Ansichten-Ziele | Schreibgeschützter Zugriff auf verfügbare Ziele auf der Registerkarte &quot; _Katalog_ &quot;und authentifizierte Ziele auf der Registerkarte &quot; _Durchsuchen_ &quot;. |
| Ziele | Ziele aktivieren | Möglichkeit, Daten an Ziele zu aktivieren. Für diese Berechtigung muss dem Profil &quot;Ansicht&quot;entweder &quot;Ziele verwalten&quot;oder &quot;Zielorte verwalten&quot;hinzugefügt werden. |

**Bekannte Probleme**

* Keine

Weiterführende Informationen dazu finden Sie unter [Ziele – Übersicht](../../rtcdp/destinations/destinations-overview.md).