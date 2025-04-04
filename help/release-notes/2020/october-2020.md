---
title: Adobe Experience Platform – Versionshinweise, Oktober 2020
description: Versionshinweise von Oktober 2020 für Adobe Experience Platform.
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 23%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 14. Oktober 2020**

- [Datenvorbereitung](#data-prep)
- [Echtzeit-Kundenprofil](#profile)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)
- [Time to Value](#time-to-value)

## Datenvorbereitung {#data-prep}

Die Datenvorbereitung ermöglicht es Dateningenieurinnen und -ingenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| `is_set`-Funktion | Mit der Funktion `is_set` können Sie überprüfen, ob in den Quelldaten ein -Attribut vorhanden ist. `is_set` kann in Kombination mit `is_empty` verwendet werden, um sowohl das Vorhandensein des -Attributs als auch das Vorhandensein des -Werts innerhalb des -Attributs zu überprüfen. |
| `get_values`-Funktion | Mit der Funktion `get_values` können Sie die Werte aus der Eingabezuordnung für einen beliebigen Schlüssel abrufen. |

Weitere Informationen finden Sie unter [Datenvorbereitung - Übersicht](../../data-prep/home.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das [!DNL Real-Time Customer Profile] ermöglicht eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen sowie anderen Kanälen miteinander kombiniert. [!DNL Profile] können Sie Ihre unterschiedlichen Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige, Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

| Funktion | Beschreibung |
| ------- | ----------- |
| Hinzufügungen zur Profilvorschau-API | Die Profilvorschau-API (`/previewsamplestatus`) bietet jetzt die Möglichkeit, eine Aufschlüsselung der gesamten Profilfragmente in Ihrer Organisation sowie die Verteilung der Profilfragmente über Identity-Namespaces anzuzeigen. |
| Aktualisierungen der Vereinigungsschemaansicht | In der Experience Platform-Benutzeroberfläche können Benutzende Informationen zu allen Schemata und Datensätzen, die zum Vereinigungsschema beitragen, sowie Attribute von Oberflächenschlüsseln wie Identitäts- und Beziehungsfelder leichter finden. Diese Aktualisierungen verbessern die Möglichkeit, Probleme zu beheben und zu überprüfen, ob Profile korrekt konfiguriert und Identitäten korrekt zugeordnet wurden und Daten erfolgreich aufgenommen wurden. |

Weitere Informationen zu [!DNL Real-Time Customer Profile], einschließlich Tutorials und Best Practices für die Arbeit mit [!DNL Profile]-Daten, finden [ in der Übersicht zum Echtzeit-Kundenprofil](../../profile/home.md).

## Segmentierungs-Service {#segmentation}

Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und aus Ihren [!DNL Real-Time Customer Profile]-Daten Zielgruppen generieren können. Diese Segmente werden zentral in [!DNL Experience Platform] konfiguriert und gepflegt, sodass sie für jede Adobe-Anwendung leicht zugänglich sind.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Entfernung des Streaming-Segmentierungslimits | Das Sieben-Tage-Limit für den Lookback-Zeitraum wurde entfernt. |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Segmentierung - Übersicht](../../segmentation/home.md)

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen aufnehmen und ermöglicht es Ihnen gleichzeitig, diese Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie auf einfache Weise Quellverbindungen für verschiedene Datenanbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung der SSH-Authentifizierung für SFTP | Sie können Ihr SFTP-Konto mit [!DNL Experience Platform] verbinden, indem Sie RSA/DSA Open SSH-Schlüssel verwenden. Weitere Informationen finden Sie [ „SFTP](../../sources/connectors/cloud-storage/sftp.md)Übersicht“. |
| UX-Verbesserungen | Sie können Ihren Datensatz während der Datenaufnahme für die [!DNL Profile] aktivieren. Weitere Informationen finden Sie [ Tutorial zum ](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)Cloud-Datenspeicherungs-Workflow) . |

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).

## Time to Value {#time-to-value}

Adobe Experience Platform ermöglicht es Marketing-Teams, eine 360-Grad-Sicht auf ihre Kunden zu erstellen, ohne dass umfangreiche Daten-Engineering-Kenntnisse erforderlich sind. Das Ziel besteht darin, Teams zu beschleunigen und durch Datengeschwindigkeit einen Mehrwert zu erzielen.

Die „Time to Value“ erstreckt sich über Personas hinweg. Dateningenieure können Aufgaben effizient und schneller mit Transparenz der Datenaktivität erledigen, sodass ein robustes, skalierbares Echtzeit-Kundenprofil früher verfügbar ist. Marketing-Experten können dann das vollständige, robuste Kundenprofil für die Segmentierung und Aktivierung verwenden.

### Feature-Highlights

#### Schema

Aktualisiert die Benutzerfreundlichkeit und den Workflow und bietet vordefinierte Einblicke, Standardisierung und Transparenz von Schlüsselfeldern in Schemakompositionen. Zeigt die Datenherkunft für die Kombination von einzelnen Datenmodellen, die als „Vereinigungsschema“ dargestellt werden, wobei insight in die Struktur und die Inhaltsstoffe für das Echtzeit-Kundenprofil bereitgestellt wird.

- Upgrade des Schema-Workflows
   - Verwenden Sie Tastaturbefehle für den häufigsten Typ von XDM-Schemata mit automatisierten Einstellungen im Schema-Editor und Schemafeldgruppenempfehlungen basierend auf Ihren Zielen
   - Steigerung der Workflow-Effizienz durch Auswahl und Vorschau mehrerer Feldergruppen
   - Transparenz bei Schlüsselattributen der Schemakomposition, einschließlich Identität, Beziehung und erforderlichen und verworfenen Feldern
- Transparenz der Datenherkunft und der Schlüsselattribute des Vereinigungsschemas

#### Datenaufnahme und -erfassung

Die automatische Zuordnung, die Zuordnungsvorschau und die Benutzerfreundlichkeits-Aktualisierung bringen Daten von jeder Plattform oder Quelle für die Verwendung im Profil, in der nachgelagerten Segmentierung und bei der Aktivierung ein. Das System verfügt über die Effizienz und Intelligenz, um diesen Prozess einfacher zu verwenden, auch für Personen außerhalb der IT.

- Einfacherer Zugriff auf Datenquellen mit einer Katalogseitenkarte und einem Inline-Aktionsmuster-Upgrade für Datentabellen
- Berechnetes Feld/Ausdruck für die Datenaufnahme
- Empfehlungen zur Datenzuordnung beschleunigen den Aufnahmeprozess
- Zuordnungsvorschau und Validierungen

#### Profilkonfiguration

Ein marketerfreundlicher Profil-Viewer mit Anpassung hilft Ihnen, die Komposition eines Profils zur Verwendung in Segmentierungs-, Planungs- und Aktivierungsfällen zu verstehen. Der konsolidierte Workflow hydriert das Profil auf kontrollierte und effiziente Weise, indem er einen schrittweisen Workflow für Zusammenführungsrichtlinien bereitstellt.

- Zeigen Sie jedes einzelne Profil in einem erweiterten Profil-Viewer an, der ein Dashboard mit vollständiger Anpassung anzeigt, sodass kanalübergreifende Daten basierend auf den Geschäftszielen des Marketing-Experten gruppiert werden können.
- Bearbeiten Sie die standardmäßigen und benutzerdefinierten Attribute im Widget Basisinformationen entsprechend den Geschäftsanforderungen.
- Passen Sie Widgets mit Attributen aus dem Echtzeit-Kundenprofil mithilfe der Vereinigungsschema-Auswahl an. Das Vereinigungsschema wird von den zugrunde liegenden Datenmodellen abgeleitet, die bei der Profildatenaufnahme verwendet werden.


#### Überwachung

Stellt die Transparenz des Datenflusses sicher und gibt insight Informationen zum Zustand des Datenverkehrs, der von den Quell-Connectoren in das System fließt, wodurch mehr Self-Service und schnellere Reaktionsfähigkeit für die Fehlerbehebung bereitgestellt werden.

- Überwachen Sie alle Flussausführungen und sehen Sie eine detaillierte Ansicht jedes Durchgangs, einschließlich Abschlussstatus, Ausführungsdauer, Liste der verarbeiteten Dateien, Fehler und ausführbaren Diagnosen
