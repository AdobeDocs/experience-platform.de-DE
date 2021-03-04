---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise für Experience Platform vom 11. Dezember 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 65%

---


# Adobe Experience Platform – Versionshinweise

**Release-Datum: Mittwoch, 11. Dezember 2019**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Der Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und Audiencen aus Ihren [!DNL Real-time Customer Profile]-Daten generieren können. Diese Adoben werden zentral auf [!DNL Platform] konfiguriert und gepflegt, sodass sie für jede Anwendung leicht zugänglich sind.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Registerkarte &quot;Zusammengeführte Audiencen&quot;in [!DNL Segment Builder] | Die Registerkarten [!UICONTROL Segmente] und [!UICONTROL Audiences][!DNL Segment Builder] im wurden zu einer Registerkarte namens [!UICONTROL Audiences] zusammengefasst. Auf dieser Registerkarte können Sie nach vorhandenen Zielgruppen suchen, die Sie dann per Drag-and-Drop in die Arbeitsfläche von Rule Builder ziehen können, um eine neue Segmentdefinition zu erstellen. Beim Referenzieren einer Zielgruppe kann der neuen Segmentdefinition einer der folgenden Regellogiksätze hinzugefügt werden: Die Zielgruppenzugehörigkeit als Regel. Der vollständige Satz an Regellogik, der die referenzierte Zielgruppe definiert hat. |
| Neuer Ort für die Auswahl von Zusammenführungsrichtlinien | Der Speicherort der Auswahl für die Richtlinie zum Zusammenführen in [!DNL Segment Builder] wurde geändert. Um eine Richtlinie zum Zusammenführen für eine Segmentdefinition auszuwählen, wählen Sie auf der Registerkarte **[!UICONTROL Felder]** das Zahnradsymbol aus und wählen Sie dann im Dropdownmenü **[!UICONTROL Richtlinie zusammenführen]** die anzuwendende Richtlinie aus. |

**Bekannte Probleme**

* Keine

Weitere Informationen finden Sie unter [Segmentation Service – Übersicht](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] bietet die Möglichkeit, programmatisch und intelligent die &quot;Nächstes bestes Erlebnis&quot;aus einer Reihe verfügbarer Optionen für eine bestimmte Person auszuwählen, sie an einen beliebigen Kanal oder eine Anwendung zu senden und Berichte und Analyse auszuführen.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Ranking-Funktionen | Die Reihenfolge von Angeboten für Profile wird nun über eine Ranking-Funktion und nicht einen festen Satz von Angeboten für alle Profile abgeleitet. |

**Bekannte Probleme**

* Keine.

## [!DNL Sources] {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen, während Sie diese Daten mithilfe der [!DNL Platform]-Dienste strukturieren, beschriften und erweitern können. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Lösungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Diese Quellverbindungen ermöglichen Ihnen eine Authentifizierung mit Ihren Datenspeichern und CRM-Diensten, die Festlegung von Zeiten für Erfassungsläufe und die Verwaltung des Durchsatzes bei der Datenerfassung.

**Neue Funktionen**

| Funktion | Beschreibung |
| ---------- | ------------ |
| Streaming-Verbindung | Mit der Streaming-Erfassung können Sie Daten von client- und serverseitigen Geräten in Echtzeit an [!DNL Experience Platform] senden. Die Version enthält eine neue Benutzeroberfläche für Streaming-Verbindungen. |
| Connector-Unterstützung für [!DNL Google Cloud Store] | Unterstützung für die Datenerfassung von [!DNL Google Cloud Store]. |

**Bekannte Probleme**

* Keine.

Weiterführende Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md).

## [!DNL Experience Data Model] (XDM) System  {#xdm}

Normung und Interoperabilität sind Schlüsselkonzepte hinter [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), angetrieben von der Adobe, ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schema für das Kundenerlebnis-Management zu definieren.

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

Weitere Informationen zum Arbeiten mit XDM mit der [!DNL Schema Registry]-API und [!DNL Schema Editor]-Benutzeroberfläche finden Sie in der [XDM-Systemdokumentation](../../xdm/home.md).