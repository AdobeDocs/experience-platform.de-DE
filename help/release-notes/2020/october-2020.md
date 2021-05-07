---
title: Versionshinweise zu Adobe Experience Platform
description: Versionshinweise zur Experience Platform Oktober 2020
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 18%

---

# Versionshinweise zu Adobe Experience Platform

**Release-Datum: 14. Oktober 2020**

- [Datenvorbereitung](#data-prep)
- [Echtzeit-Kundenprofil](#profile)
- [Segmentierungsdienst](#segmentation)
- [Quellen](#sources)
- [Zeit bis zum Wert](#time-to-value)

## Datenvorbereitung {#data-prep}

Data Prep ermöglicht es Datenentwicklern, Daten dem Experience Data Model (XDM) zuzuordnen, umzuformen und zu validieren.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| `is_set` durchführen | Mit der Funktion `is_set` können Sie überprüfen, ob ein Attribut in den Quelldaten vorhanden ist. `is_set` kann in Verbindung mit  `is_empty` der Überprüfung sowohl des Vorkommens des Attributs als auch des Vorkommens des Werts innerhalb des Attributs verwendet werden. |
| `get_values` durchführen | Mit der Funktion `get_values` können Sie die Werte aus der Eingabemap für einen beliebigen Schlüssel abrufen. |

Weitere Informationen finden Sie im Abschnitt [Datenvorbereitung](../../data-prep/home.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. Mit [!DNL Real-time Customer Profile] können Sie eine ganzheitliche Ansicht jedes einzelnen Kunden sehen, die Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieterdaten, kombiniert. [!DNL Profile] ermöglicht es Ihnen, Ihre unterschiedlichen Kundendaten zu einer einheitlichen Ansicht zusammenzuführen, die Ihnen einen umsetzbaren Zeitstempel für jede Kundeninteraktion bietet.

| Funktion | Beschreibung |
| ------- | ----------- |
| API-Ergänzungen zur Profil-Vorschau | Die Profil Vorschau API (`/previewsamplestatus`) bietet jetzt die Möglichkeit, eine Aufschlüsselung der gesamten Profil-Fragmente in Ihrer IMS-Organisation Ansicht sowie die Ansicht der Verteilung von Profil-Fragmenten über Identitäts-Namensraum hinweg. |
| Updates der Vereinigung Schema Ansicht | In der Benutzeroberfläche &quot;Experience Platform&quot;können Benutzer leichter Informationen zu allen Schemas und Datensätzen finden, die zum Schema der Vereinigung beitragen, sowie zu Oberflächenattributen wie Identitäts- und Beziehungsfeldern. Diese Updates verbessern die Fehlerbehebung und die Überprüfung der ordnungsgemäßen Konfiguration von Profilen, der richtigen Zuordnung von Identitäten und der erfolgreichen Erfassung von Daten. |

Weitere Informationen zu [!DNL Real-time Customer Profile], einschließlich Übungen und Best Practices für die Arbeit mit [!DNL Profile]-Daten, finden Sie im [Überblick über das Echtzeit-Profil des Kunden](../../profile/home.md).

## Segmentierungs-Service {#segmentation}

Der Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und Audiencen aus Ihren [!DNL Real-time Customer Profile]-Daten generieren können. Diese Adoben werden zentral auf [!DNL Platform] konfiguriert und gepflegt, sodass sie für jede Anwendung leicht zugänglich sind.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Entfernung der Segmentierungsgrenze für Streaming | Die Beschränkung für den Lookback-Zeitraum von sieben Tagen wurde entfernt. |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Segmentierungsübersicht](../../segmentation/home.md)

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen, während Sie diese Daten mithilfe der [!DNL Platform]-Dienste strukturieren, beschriften und erweitern können. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| SSH-Authentifizierungsunterstützung für SFTP | Sie können Ihr SFTP-Konto mit [!DNL Platform] über RSA/DSA Open SSH-Schlüssel verbinden. Weitere Informationen finden Sie unter [SFTP overview](../../sources/connectors/cloud-storage/sftp.md). |
| UX-Verbesserungen | Sie können Ihr Dataset während der Datenerfassung für [!DNL Profile] aktivieren. Weitere Informationen finden Sie im Tutorial [Cloud-Datenspeicherung DataFlow-Workflow](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).

## Zeit bis zum Wert {#time-to-value}

Adobe Experience Platform ermöglicht es Marketing Operations Teams, eine 360-Grad-Ansicht ihrer Kunden zu entwickeln, ohne dass umfangreiche Daten-Engineering-Kenntnisse erforderlich sind. Ziel ist es, Teams und Werte durch Datengeschwindigkeit zu beschleunigen.

&quot;Time to Value&quot; schneidet über Personas hinweg. Data Engineers können Aufgaben effizient und schnell mit Transparenz in der Aktivität von Daten abschließen, sodass schneller ein robustes, skalierbares Echtzeit-Profil verfügbar ist. Marketingexperten können dann das vollständige, robuste Profil für die Segmentierung und Aktivierung verwenden.

### Funktionsmerkmale

#### Schema

Verbessert die Benutzerfreundlichkeit und den Arbeitsablauf und bietet sofort verfügbare Einblicke, Standardisierung und Transparenz von Schlüsselfeldern in Schema-Kompositionen. Stellt Datenlinien für die Kombination einzelner Datenmodelle, die als &quot;Vereinigung-Schema&quot;dargestellt werden, bereit und bietet so Einblicke in die Struktur und die Inhaltsstoffe des Echtzeit-Kunden-Profils.

- Aktualisierung des Schema-Workflows
   - Verwenden Sie Tastenkombinationen für die am häufigsten verwendeten XDM-Schema mit automatisierten Einstellungen im Schema- und Schema-Feldgruppenempfehlungen, die auf Ihren Zielsetzungen basieren
   - Erhöhen Sie die Effizienz des Arbeitsablaufs durch Auswahl und Vorschau mehrerer Feldgruppen.
   - Transparenz bei Schlüsselattributen der Schema-Komposition, einschließlich Identitäts-, Beziehungs- sowie erforderlichen und nicht mehr unterstützten Feldern
- Vereinigung-Schema-Datenlineare und Schlüsselattribute-Transparenz

#### Dateneinbettung und -erfassung

Bei der Aktualisierung der automatischen Zuordnung, Zuordnungsfunktion und Benutzerfreundlichkeit werden Daten von jeder Plattform oder Quelle zur Verwendung in Profil, nachfolgender Segmentierung und Aktivierung eingefügt. Das System verfügt über die Effizienz und Intelligenz, um diesen Prozess auch für Menschen außerhalb der IT einfacher zu verwenden.

- Einfacherer Zugriff auf Datenquellen mit der Katalogseitenkarte und der Datentabelle Inline-Aktionsmuster-Aktualisierung
- Berechnete Felder/Ausdruck für die Datenverarbeitung
- Empfehlungen zur Datenzuordnung beschleunigen den Erfassungsvorgang
- Vorschau und Überprüfungen zuordnen

#### Profil-Konfiguration

Mit dem marketingfreundlichen Profil-Viewer mit Anpassung können Sie die Zusammensetzung eines Profils für die Segmentierung, Planung und Aktivierung verstehen. Der konsolidierte Arbeitsablauf verbessert das Profil durch einen schrittweisen Arbeitsablauf für die Richtlinie zum Zusammenführen.

- Ansicht jedes einzelnen Profils in einem verbesserten Profil-Viewer, der ein Dashboard mit vollständiger Anpassung anzeigt und gruppierte Daten zu Kanälen basierend auf den Geschäftszielen des Marketingexperten ermöglicht.
- Bearbeiten Sie standardmäßige und benutzerdefinierte Attribute im Widget &quot;Grundlegende Informationen&quot;entsprechend den geschäftlichen Anforderungen.
- Passen Sie Widgets mit Attributen aus dem Echtzeit-Profil des Kunden mithilfe der Vereinigung-Schema-Auswahl an. Das Vereinigung-Schema wird von den zugrunde liegenden Datenmodellen abgeleitet, die bei der Datenerfassung von Profilen verwendet werden.


#### Überwachung

Gewährleistet Transparenz des Datenflusses und gibt Einblick in den Zustand des Datenverkehrs von den Quellschnittstellen in das System, wodurch mehr Selbstbedienung und schnellere Reaktionsfähigkeit bei der Fehlerbehebung gewährleistet sind.

- Überwachen Sie die Ausführung des gesamten Datenflusses und sehen Sie eine detaillierte Ansicht der einzelnen Vorgänge, einschließlich Abschlussstatus, Laufzeit, Liste der verarbeiteten Dateien, Fehler und ausführbare Diagnosen.
