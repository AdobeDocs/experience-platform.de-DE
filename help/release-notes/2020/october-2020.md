---
title: Adobe Experience Platform – Versionshinweise, Oktober 2020
description: Versionshinweise von Oktober 2020 für Adobe Experience Platform.
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 26%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 14. Oktober 2020**

- [Datenvorbereitung](#data-prep)
- [Echtzeit-Kundenprofil](#profile)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)
- [Zeit bis Wert](#time-to-value)

## Datenvorbereitung {#data-prep}

Die Datenvorbereitung ermöglicht es Dateningenieurinnen und -ingenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| `is_set`-Funktion | Die `is_set` -Funktion können Sie überprüfen, ob ein Attribut in den Quelldaten vorhanden ist. `is_set` kann in Kombination mit `is_empty` , um sowohl das Vorhandensein des Attributs als auch das Vorhandensein des Werts im Attribut zu überprüfen. |
| `get_values`-Funktion | Die `get_values` -Funktion können Sie die Werte aus der Eingabezuordnung für einen beliebigen Schlüssel abrufen. |

Weitere Informationen finden Sie im [Datenvorbereitung - Übersicht](../../data-prep/home.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Mit [!DNL Real-Time Customer Profile]können Sie eine ganzheitliche Ansicht jedes einzelnen Kunden anzeigen, die Daten aus mehreren Kanälen kombiniert, einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten. [!DNL Profile] ermöglicht es Ihnen, Ihre unterschiedlichen Kundendaten in einer einheitlichen Ansicht zusammenzufassen, die eine umsetzbare, mit Zeitstempel versehene Übersicht über jede Kundeninteraktion bietet.

| Funktion | Beschreibung |
| ------- | ----------- |
| API-Ergänzungen zur Profilvorschau | Die Profilvorschau-API (`/previewsamplestatus`) bietet jetzt die Möglichkeit, eine Aufschlüsselung der gesamten Profilfragmente in Ihrer Organisation anzuzeigen und die Verteilung der Profilfragmente über Identitäts-Namespaces hinweg anzuzeigen. |
| Aktualisierungen der Schema-Ansicht von Vereinigungen | In der Experience Platform-Benutzeroberfläche können Benutzer leichter Informationen zu allen Schemas und Datensätzen finden, die zum Vereinigungsschema beitragen, sowie wichtige Oberflächenattribute wie Identitäts- und Beziehungsfelder. Diese Aktualisierungen verbessern die Fehlerbehebung und die Überprüfung der korrekten Konfiguration von Profilen, der korrekten Zuordnung von Identitäten und der erfolgreichen Erfassung von Daten. |

Weitere Informationen finden Sie unter [!DNL Real-Time Customer Profile], einschließlich Tutorials und Best Practices für die Arbeit mit [!DNL Profile] Daten lesen Sie bitte die [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).

## Segmentierungs-Service {#segmentation}

Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und aus Ihren [!DNL Real-Time Customer Profile]-Daten Zielgruppen generieren können. Diese Segmente werden zentral in [!DNL Platform] konfiguriert und gepflegt, sodass sie für jede Adobe-Anwendung leicht zugänglich sind.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Entfernung der Streaming-Segmentierung begrenzen | Die Beschränkung von sieben Tagen für den Lookback-Zeitraum wurde entfernt. |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md)

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen und gleichzeitig diese Daten strukturieren, beschriften und erweitern, indem es [!DNL Platform] Dienste. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| SSH-Authentifizierungsunterstützung für SFTP | Sie können Ihr SFTP-Konto mit [!DNL Platform] mithilfe von RSA/DSA Open SSH-Schlüsseln. Siehe [SFTP-Übersicht](../../sources/connectors/cloud-storage/sftp.md) für weitere Informationen. |
| UX-Verbesserungen | Sie können Ihren Datensatz für [!DNL Profile] während des Datenerfassungsprozesses. Siehe [Cloud-Speicher-Datenfluss-Workflow](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) Tutorial für weitere Informationen. |

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).

## Zeit bis Wert {#time-to-value}

Mit Adobe Experience Platform können Marketingbetriebsteams eine 360-Grad-Ansicht ihrer Kunden erstellen, ohne dass umfangreiche Data Engineering-Kenntnisse erforderlich sind. Ziel ist es, Teams und Wert durch Datengeschwindigkeit zu beschleunigen.

&quot;Time to Value&quot;schneidet Personas zwischen. Data Engineers können Aufgaben effizient und beschleunigt mit Transparenz der Datenaktivität erledigen, sodass ein robustes, skalierbares Echtzeit-Kundenprofil schneller verfügbar ist. Marketingexperten können dann das vollständige, zuverlässige Kundenprofil für die Segmentierung und Aktivierung verwenden.

### Funktionsmerkmale

#### Schema

Verbessert die Benutzerfreundlichkeit und den Arbeitsablauf und bietet vordefinierte Einblicke, Standardisierung und Transparenz von Schlüsselfeldern in Schemakompositionen. Stellt die Datenherkunft für die Kombination einzelner Datenmodelle, die als &quot;Vereinigungsschema&quot;dargestellt werden, bereit und bietet Einblicke in die Struktur und die Inhaltsstoffe des Echtzeit-Kundenprofils.

- Schema-Workflow-Aktualisierung
   - Verwenden Sie Verknüpfungen für den gängigsten Typ von XDM-Schemas mit automatisierten Einstellungen im Schema-Editor und in den Empfehlungen für Schemafelder basierend auf Ihren Zielen.
   - Steigerung der Workflow-Effizienz durch Auswahl und Vorschau mehrerer Feldergruppen
   - Transparenz in Bezug auf die Schlüsselattribute der Schemakomposition, einschließlich Identität, Beziehung sowie erforderliche und veraltete Felder
- Unionschema-Datenherkunft und Transparenz der Schlüsselattribute

#### Datenerfassung und -erfassung

Bei der Aktualisierung der automatischen Zuordnung, Zuordnungsvorschau und Benutzerfreundlichkeit werden Daten von jeder Plattform oder Quelle zur Verwendung in Profil, nachfolgender Segmentierung und Aktivierung eingefügt. Das System verfügt über die Effizienz und Intelligenz, um diesen Prozess auch für Personen außerhalb der IT zu vereinfachen.

- Einfacherer Zugriff auf Datenquellen mit der Katalogseitenkarte und dem Inline-Aktionsmuster der Datentabelle
- Berechnetes Feld/Ausdruck für die Datenerfassung
- Empfehlungen zur Datenzuordnung beschleunigen den Aufnahmeprozess
- Zuordnen von Vorschau und Validierungen

#### Profilkonfiguration

Mit dem marketerfreundlichen Profil-Viewer mit Anpassung können Sie die Zusammensetzung eines Profils für die Verwendung in Segmentierung, Planung und Aktivierungsfällen verstehen. Der konsolidierte Workflow optimiert das Profil in kontrollierter und effizienter Weise, indem er einen schrittweisen Workflow für die Zusammenführungsrichtlinie bereitstellt.

- Zeigen Sie jedes einzelne Profil in einem erweiterten Profil-Viewer an, der ein Dashboard mit vollständiger Anpassung anzeigt und so gruppierte kanalübergreifende Daten basierend auf den Geschäftszielen des Marketing-Experten ermöglicht.
- Bearbeiten Sie die standardmäßigen und benutzerdefinierten Attribute im Widget Grundlegende Informationen entsprechend den Geschäftsanforderungen.
- Passen Sie Widgets mit Attributen aus dem Echtzeit-Kundenprofil mithilfe der Vereinigungsschemaauswahl an. Das Vereinigungsschema wird von den zugrunde liegenden Datenmodellen abgeleitet, die bei der Profildatenerfassung verwendet werden.


#### Überwachung

Gewährt Transparenz des Datenflusses und gibt Einblicke in den Zustand des Datenverkehrs, der über Quell-Connectoren in das System geleitet wird. So erhalten Sie mehr Self-Service und schnellere Handlungsmöglichkeiten bei der Fehlerbehebung.

- Überwachen Sie alle Durchsatzausführungen und sehen Sie sich eine detaillierte Ansicht jedes Durchlaufs an, einschließlich Abschlussstatus, Ausführungsdauer, Liste der verarbeiteten Dateien, Fehler und ausführbarer Diagnosen.
