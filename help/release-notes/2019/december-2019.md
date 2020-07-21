---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise für Experience Platform vom 11. Dezember 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 72%

---


# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 11. Dezember 2019**

Aktualisierungen vorhandener Funktionen in der Adobe Experience Platform:

* [!DNL Segmentation Service](#segmentation)
* [!DNL Decisioning Service](#decisioning)
* [!DNL Sources](#sources)
* [!DNL Experience Data Model (XDM) System](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform Segmentation Service provides a user interface and RESTful API that allows you to build segments and generate audiences from your [!DNL Real-time Customer Profile] data. These segments are centrally configured and maintained on [!DNL Platform], making them readily accessible by any Adobe application.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Merged Audiences tab in [!DNL Segment Builder] | Die Registerkarten [!UICONTROL _Segmente _]und[!UICONTROL _Audiences_][!DNL Segment Builder] im wurden zu einer Registerkarte namens [!UICONTROL _Audiences _]zusammengefasst. Auf dieser Registerkarte können Sie nach vorhandenen Audiences suchen, die Sie dann per Drag-and-Drop in die Arbeitsfläche von Rule Builder ziehen können, um eine neue Segmentdefinition zu erstellen. Beim Referenzieren einer Audience kann der neuen Segmentdefinition einer der folgenden Regellogiksätze hinzugefügt werden: Die Audience-Zugehörigkeit als Regel. Der vollständige Satz an Regellogik, der die referenzierte Audience definiert hat. |
| Neuer Ort für die Auswahl von Zusammenführungsrichtlinien | The location of the merge policy selector in the [!DNL Segment Builder] has been changed. Um eine Zusammenführungsrichtlinie für eine Segmentdefinition auszuwählen, klicken Sie auf das Zahnradsymbol auf der Registerkarte [!UICONTROL _Felder _]und wählen Sie dann im Dropdown-Menü_[!UICONTROL  Zusammenführungsrichtlinie]_ die gewünschte Zusammenführungsrichtlinie aus. |

**Bekannte Probleme**

* Keine

Weiterführende Informationen finden Sie in der [Übersicht zum Segmentation Service](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] provides the ability to programmatically and intelligently select the &quot;Next Best Experience&quot; from a set of available options for a given individual, deliver them to any channel or application, and perform reporting and analysis.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Ranking-Funktionen | Die Reihenfolge von Angeboten für Profile wird nun über eine Ranking-Funktion und nicht einen festen Satz von Angeboten für alle Profile abgeleitet. |

**Bekannte Probleme**

* Keine.

Eine ausführliche Einführung zu dem Dienst finden Sie in der [Übersicht zum Decisioning Service](../../decisioning-service/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Lösungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, damit Sie für verschiedene Datenanbieter bequem Quellverbindungen einrichten können. Diese Quellverbindungen ermöglichen Ihnen eine Authentifizierung mit Ihren Speichersystemen und CRM-Diensten, die Festlegung von Zeiten für Erfassungsläufe und die Verwaltung des Durchsatzes bei der Datenerfassung.

**Neue Funktionen**

| Funktion | Beschreibung |
| ---------- | ------------ |
| Streaming-Verbindung | Streaming ingestion enables you to send data from client- and server-side devices to [!DNL Experience Platform] in real-time. Die Version enthält eine neue Benutzeroberfläche für Streaming-Verbindungen. |
| Connector-Unterstützung für [!DNL Google Cloud Store] | Support for collecting data from [!DNL Google Cloud Store]. |

**Bekannte Probleme**

* Keine.

Weiterführende Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md).

## [!DNL Experience Data Model] (XDM) System {#xdm}

Standardization and interoperability are key concepts behind [!DNL Experience Platform]. [!DNL Experience Data Model]Das von Adobe unterstützte  (XDM) ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Verbesserte Schemavalidierung | Neue Prüfungen, um sicherzustellen, dass Verweise erwartungsgemäß in zusätzliche Felder aufgelöst werden. Zusätzliche Prüfungen für Felder, die als Gruppe von Objekten definiert wurden, um sicherzustellen, dass die Objekte vollständig definiert sind. Verbesserte Fehlermeldungen zur Ermittlung und Behebung von Problemen. |

**Fehlerkorrekturen**

* Wartung und Verbesserungen in Bezug auf Zugriffskontrolle und Sandboxes.
* Support for `eTag` for the `/descriptors` endpoint in the [!DNL Schema Registry] API.

**Bekannte Probleme**

* Keine

To learn more about working with XDM using the [!DNL Schema Registry] API and [!DNL Schema Editor] user interface, please read the [XDM System documentation](../../xdm/home.md).