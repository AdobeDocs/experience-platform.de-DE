---
title: Adobe Experience Platform  – Versionshinweise
description: Versionshinweise zur Experience Platform vom 11. Dezember 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 5%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: 11. Dezember 2019**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

* [Segmentierungsdienst](#segmentation)
* [Entscheidungsdienst](#decisioning)
* [Quellen](#sources)
* [Erlebnis-Datenmodell (XDM)-System](#xdm)

## Segmentierungsdienst {#segmentation}

Der Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und Audiencen aus Ihren Echtzeit-Daten zum Profil von Kunden generieren können. Diese Segmente werden zentral auf der Plattform konfiguriert und gepflegt, sodass sie von jeder Adobe-Anwendung leicht zugänglich sind.

Der Segmentierungsdienst definiert eine bestimmte Untergruppe von Profilen, indem er die Kriterien beschreibt, die eine vermarktbare Personengruppe innerhalb Ihrer Kundenbasis unterscheiden. Segmente können auf Datensatzdaten (z. B. demografische Informationen) oder Zeitreihen-Ereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Registerkarte &quot;Zusammengeführte Audiencen&quot;im Segmentaufbau | Die Registerkarten _Segmente_ und _Audiencen_ im Segmentaufbau wurden zu einer einzigen Registerkarte für _Audiencen_ zusammengefasst. Auf dieser Registerkarte können Sie nach vorhandenen Audiencen suchen und suchen, die Sie dann per Drag &amp; Drop in die Arbeitsfläche des Regelaufbaus ziehen können, um eine neue Segmentdefinition zu erstellen. Beim Referenzieren einer Audience kann der neuen Segmentdefinition einer der folgenden Regellogikresätze hinzugefügt werden: Die Audience Mitgliedschaft als Regel. Der vollständige Satz der Regellogik, die die referenzierte Audience definiert. |
| Neuer Speicherort für die Auswahl der Richtlinie zum Zusammenführen | Der Speicherort der Auswahl für die Richtlinie zum Zusammenführen im Segmentaufbau wurde geändert. Um eine Richtlinie zum Zusammenführen für eine Segmentdefinition auszuwählen, klicken Sie auf das Zahnradsymbol auf der Registerkarte &quot; _Felder_ &quot;und wählen Sie dann im Dropdown-Menü &quot; _Richtlinie_ zusammenführen&quot;die gewünschte Richtlinie aus. |

**Bekannte Probleme**

* Keine

Weitere Informationen finden Sie in der Übersicht über den [Segmentierungsdienst](../../segmentation/home.md).

## Entscheidungsdienst {#decisioning}

Der Entscheidungsdienst für Adobe Experience Platform bietet die Möglichkeit, programmatisch und intelligent die Option &quot;Nächstes bestes Erlebnis&quot;aus einer Reihe verfügbarer Optionen für eine bestimmte Person auszuwählen, sie an einen beliebigen Kanal oder eine Anwendung zu senden und Berichte und Analyse auszuführen.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Rangfunktionen | Die Reihenfolge der Angebot für Profil wird nun über eine Rangfunktion und nicht über einen festen Satz von Angeboten über alle Profil hinweg abgeleitet. |

**Bekannte Probleme**

* Keine.

Eine vollständige Einführung in den Dienst finden Sie in der Übersicht über den [Entscheidungsdienst](../../decisioning-service/home.md) .

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen, während Sie diese Daten mithilfe von Plattformdiensten strukturieren, beschriften und verbessern können. Sie können Daten aus verschiedenen Quellen erfassen, z. B. Adobe Solutions, Cloud-basierte Datenspeicherung, Drittanbieter-Software und Ihr CRM-System.

Experience Platform bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie Quellverbindungen für verschiedene Datenanbieter einfach einrichten können. Mit diesen Quellverbindungen können Sie sich bei Ihren Datenspeicherung- und CRM-Diensten authentifizieren, die Erfassungsdauer festlegen und den Datendurchsatz verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ---------- | ------------ |
| Streaming-Verbindung | Mit der Streaming-Erfassung können Sie Daten von client- und serverseitigen Geräten in Echtzeit an Experience Platform senden. Version enthält eine neue Benutzeroberfläche für Streaming-Verbindungen. |
| Connector-Unterstützung für Google Cloud Store | Unterstützung für das Erfassen von Daten aus dem Google Cloud Store. |

**Bekannte Probleme**

* Keine.

For more information about sources, see the [sources overview](../../sources/home.md).

## Erlebnis-Datenmodell (XDM)-System {#xdm}

Standardisierung und Interoperabilität sind Schlüsselkonzepte der Experience Platform. Das von Adobe unterstützte Experience Data Model (XDM) ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schema für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten auf der Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Audiencen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Verbesserte Schema-Validierung | Neue Prüfungen, um sicherzustellen, dass Verweise erwartungsgemäß in zusätzliche Felder aufgelöst werden. Zusätzliche Prüfungen zu Feldern, die als Array von Objekten definiert wurden, wurden hinzugefügt, um sicherzustellen, dass die Objekte vollständig definiert sind. Verbesserte Fehlermeldungen zur Identifizierung und Behebung von Problemen. |

**Fehlerkorrekturen**

* Wartung und Verbesserung in Bezug auf Zugriffskontrolle und Sandboxen.
* Unterstützung `eTag` für den `/descriptors` Endpunkt in der Schema Registry-API.

**Bekannte Probleme**

* Keine

Weitere Informationen zum Arbeiten mit XDM mithilfe der Schema Registry API und Schema Editor Benutzeroberfläche finden Sie in der [XDM-Systemdokumentation](../../xdm/home.md).