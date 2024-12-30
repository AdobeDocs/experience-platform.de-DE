---
title: Adobe Experience Platform - Versionshinweise Dezember 2019
description: Versionshinweise Dezember 2019 für Adobe Experience Platform.
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 68%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: Donnerstag, 11. Dezember 2019**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und aus Ihren [!DNL Real-Time Customer Profile]-Daten Zielgruppen generieren können. Diese Segmente werden zentral in [!DNL Platform] konfiguriert und gepflegt, sodass sie für jede Adobe-Anwendung leicht zugänglich sind.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Registerkarte „Zusammengeführte Zielgruppen“ in [!DNL Segment Builder] | Die [!UICONTROL Segmente] und [!UICONTROL Audiences] in der [!DNL Segment Builder] wurden in einer einzigen [!UICONTROL Audiences]-Registerkarte kombiniert. Auf dieser Registerkarte können Sie nach vorhandenen Zielgruppen suchen, die Sie dann per Drag-and-Drop in die Arbeitsfläche von Rule Builder ziehen können, um eine neue Segmentdefinition zu erstellen. Beim Referenzieren einer Zielgruppe kann der neuen Segmentdefinition einer der folgenden Regellogiksätze hinzugefügt werden: Die Zielgruppenzugehörigkeit als Regel. Der vollständige Satz an Regellogik, der die referenzierte Zielgruppe definiert hat. |
| Neuer Ort für die Auswahl von Zusammenführungsrichtlinien | Der Speicherort der Auswahl für die Zusammenführungsrichtlinie im [!DNL Segment Builder] wurde geändert. Um eine Zusammenführungsrichtlinie für eine Segmentdefinition auszuwählen, wählen Sie auf der Registerkarte **[!UICONTROL Felder]** das Zahnradsymbol und dann im Dropdown-Menü **[!UICONTROL Zusammenführungsrichtlinie]** die gewünschte Zusammenführungsrichtlinie aus. |

**Bekannte Probleme**

* Keine

Weitere Informationen finden Sie unter [Segmentation Service – Übersicht](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] bietet die Möglichkeit, aus einer Reihe verfügbarer Optionen für eine bestimmte Person programmatisch und intelligent das „nächstbeste Erlebnis“ auszuwählen, es für einen beliebigen Kanal oder eine beliebige Anwendung bereitzustellen sowie Reporting und Analysen durchzuführen.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Ranking-Funktionen | Die Reihenfolge von Angeboten für Profile wird nun über eine Ranking-Funktion und nicht einen festen Satz von Angeboten für alle Profile abgeleitet. |

**Bekannte Probleme**

* Keine.

## [!DNL Sources] {#sources}

Adobe Experience Platform kann Daten aus externen Quellen aufnehmen und ermöglicht es Ihnen gleichzeitig, diese Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Lösungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie auf einfache Weise Quellverbindungen für verschiedene Datenanbieter einrichten können. Diese Quellverbindungen ermöglichen Ihnen eine Authentifizierung mit Ihren Datenspeichern und CRM-Diensten, die Festlegung von Zeiten für Erfassungsläufe und die Verwaltung des Durchsatzes bei der Datenerfassung.

**Neue Funktionen**

| Funktion | Beschreibung |
| ---------- | ------------ |
| Streaming-Verbindung | Mit der Streaming-Aufnahme können Sie Daten von Client- und Server-seitigen Geräten in Echtzeit an [!DNL Experience Platform] senden. Die Version enthält eine neue Benutzeroberfläche für Streaming-Verbindungen. |
| Connector-Unterstützung für [!DNL Google Cloud Store] | Unterstützung für die Erfassung von Daten aus [!DNL Google Cloud Store]. |

**Bekannte Probleme**

* Keine.

Weiterführende Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md).

## [!DNL Experience Data Model] (XDM)-System {#xdm}

Standardisierung und Interoperabilität sind Schlüsselkonzepte von [!DNL Experience Platform]. Das von Adobe unterstützte [!DNL Experience Data Model] (XDM)-System ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemata für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Verbesserte Schemavalidierung | Neue Prüfungen, um sicherzustellen, dass Verweise erwartungsgemäß in zusätzliche Felder aufgelöst werden. Zusätzliche Prüfungen für Felder, die als Gruppe von Objekten definiert wurden, um sicherzustellen, dass die Objekte vollständig definiert sind. Verbesserte Fehlermeldungen zur Ermittlung und Behebung von Problemen. |

**Fehlerkorrekturen**

* Wartung und Verbesserungen in Bezug auf Zugriffskontrolle und Sandboxes.
* Unterstützung für `eTag` für den `/descriptors`-Endpunkt in der [!DNL Schema Registry]-API.

**Bekannte Probleme**

* Keine

Weitere Informationen zum Arbeiten mit XDM mithilfe der [!DNL Schema Registry]-API und [!DNL Schema Editor] Benutzeroberfläche finden Sie in der [XDM-Systemdokumentation](../../xdm/home.md).
