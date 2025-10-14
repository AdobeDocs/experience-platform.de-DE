---
title: Adobe Experience Platform – Versionshinweise November 2019
description: Die Versionshinweise von November 2019 für Adobe Experience Platform.
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1889'
ht-degree: 26%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: Dienstag, 18. November 2019**

Neue Funktionen in Adobe Experience Platform:
* [[!DNL Real-Time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

Aktualisierungen vorhandener Funktionen:
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-Time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Die auf Adobe Experience Platform aufbauende Real-Time Customer Data Platform (Real-Time CDP) hilft Unternehmen dabei, bekannte und unbekannte Daten zusammenzuführen, um Kundenprofile mit intelligenter Entscheidungsfindung auf der gesamten Kunden-Journey zu aktivieren. Real-Time CDP kombiniert mehrere Unternehmensdatenquellen, um in Echtzeit einheitliche Profile zu erstellen, mit denen eine personalisierte Eins-zu-eins-Kundenerfahrung über alle Kanäle und Geräte hinweg bereitgestellt werden kann.

[!DNL Real-Time Customer Data Platform] umfasst Tools für Data Governance, Identity Management, erweiterte Segmentierung und Datenwissenschaft, damit Sie Profile erstellen und Zielgruppen definieren, umfassende Einblicke gewinnen und gleichzeitig strikte Data-Governance-Richtlinien durchsetzen können.

Adobe bietet Verbindungen zu einem großen Partnernetzwerk sowie native Integrationen mit Adobe Experience Cloud, damit Sie Zielgruppen nahtlos aktivieren und über alle Kanäle hinweg für herausragende Kundenerlebnisse sorgen können – von der Personalisierung vor Ort oder in Apps über E-Mail bis hin zu Paid Media, Callcentern, vernetzten Geräten und mehr.

Mit Real-Time CDP können Sie:

* Verschaffen Sie sich einen Überblick über Ihre Kunden mit einer Streaming-Sammlung von Kundendaten aus dem gesamten Unternehmen.
* Sorgen Sie für eine angemessene Verwaltung von Profilen mit vertrauenswürdigen Governance- und Datenschutzkontrollen für bekannte und unbekannte Kennungen.
* Erstellen Sie mit KI und maschinellem Lernen auf Basis von Adobe Sensei – entwickelt für Marketer – praktische Einblicke und skalieren Sie Zielgruppen.
* Schaffen Sie in Echtzeit personalisierte Erlebnisse über alle Kanäle und Ziele hinweg.

Weitere Informationen finden Sie in der Dokumentation zu [Real-Time Customer Data Platform](../../rtcdp/overview.md).

**Wichtigste Funktionen**

| Funktion | Beschreibung |
|---|---|
| Ziele | Vordefinierte Integrationen mit Zielplattformen, die von den [!DNL Real-Time Customer Data Platform] von Adobe unterstützt werden und Daten nahtlos für diese Partner aktivieren. Weitere Informationen finden [&#x200B; unter &#x200B;](#destinations)Ziele“. |
| Dashboard der Startseitenmetriken | Die Startseite von Real-Time Customer Data Platform (Real-Time CDP) enthält ein Dashboard mit Metriken, das Informationen zu Profilen und Segmenten anzeigt. Die Startseite enthält auch Links zu Lernmaterialien. Siehe den Abschnitt [Real-Time Customer Data Platform-Metriken](#real-time-customer-data-platform-metrics) weiter unten. |
| Quellen | Sie können Daten aus einer Vielzahl von Quellen aufnehmen, z. B. aus Adobe-Lösungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM. Weitere Informationen finden Sie [&#x200B; Abschnitt &#x200B;](#sources)Quellen“ weiter unten. |

**[!DNL Real-Time Customer Data Platform]Metriken**

Die Startseite von Real-Time Customer Data Platform (Real-Time CDP), die ein Dashboard für Metriken enthält, wird angezeigt, wenn Sie sich bei Real-Time CDP anmelden.

Die Startseite ist nur einer der Orte, an denen Metrikkarten angezeigt werden. Real-Time CDP bietet Metrikkarten für Ihr gesamtes Erlebnis. Diese Metriken informieren Sie über die Daten-, Profil- und Segmentzielgruppen im System.

Wenn beim Anmelden bei Real-Time CDP keine Daten im System vorhanden sind, wird das Dashboard auf der Startseite nicht angezeigt. In dem Fall enthält die Startseite Lernmaterial für die erstmalige Nutzung. Beim Erfassen von Daten wird das Dashboard automatisch aktualisiert, um Informationen zu diesen Daten anzuzeigen.

Weitere Informationen finden Sie in der Übersicht über die [Real-Time Customer Data Platform-Metriken](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die von Real-Time Customer Data Platform von Adobe unterstützt werden und Daten nahtlos für diese Partner aktivieren. Weitere Informationen finden Sie im Artikel [Ziele - Übersicht](../../destinations/home.md) .

**Verfügbare Ziele**

Mit der November-Version unterstützt Adobe Real-Time Customer Data Platform die folgenden Ziele:

* Advertising: [!DNL Google]
* E-Mail-Marketing: Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

Informationen zu [&#x200B; einzelnen Ziele finden &#x200B;](../../destinations/catalog/overview.md) im Zielkatalog .

**Bekannte Einschränkungen**

* Das Steuerelement zum Zulassen benutzerdefinierter Aktivierungszeitpläne im Aktivierungsfluss (Zeitplanschritt) ist in der ersten Version nicht verfügbar.
* Es gibt derzeit keine Möglichkeit, eine Zielkonfiguration zu bearbeiten oder zu löschen. Um diese Einschränkung zu umgehen, können Sie das Ziel oben rechts auf der Seite mit den [&#x200B; aktivieren oder &#x200B;](../../destinations/ui/destination-details-page.md).
* Beim Herstellen einer Verbindung zu Ihrem Ziel- oder Speicherkonto ist derzeit keine Validierung für Kontodetails, Pfad oder Anmeldeinformationen vorhanden. Vergewissern Sie sich, dass Sie die richtigen Anmeldeinformationen eingeben und überprüfen Sie sie auf Rechtschreibfehler oder Tippfehler.
* Bei der ersten Version sind keine Erneuerung der Anmeldeinformationen vorhanden. Sobald ein Konto abgelaufen ist oder aktualisiert werden muss, müssen Sie eine neue Zielverbindung erstellen und Ihre zuvor zugeordneten Segmente neu zuordnen.

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen aufnehmen und ermöglicht es Ihnen gleichzeitig, diese Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Lösungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie auf einfache Weise Quellverbindungen für verschiedene Datenanbieter einrichten können. Diese Quellverbindungen ermöglichen Ihnen eine Authentifizierung mit Ihren Datenspeichern und CRM-Diensten, die Festlegung von Zeiten für Erfassungsläufe und die Verwaltung des Durchsatzes bei der Datenerfassung.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ---------- | ------------ |
| Quellen-Benutzeroberfläche | Neue Benutzeroberfläche zum Erstellen, Anzeigen und Verwalten von Quellverbindungen. |
| Überarbeitete Workflows für CRM-Connectoren | Neuer intuitiver Benutzeroberflächen-Workflow zum Erstellen und Verwalten von [!DNL Microsoft Dynamics] und [!DNL Salesforce] Connectoren. |
| Connector-Unterstützung für Cloud-basierte Speicher | Connectoren können jetzt auf Cloud-basierte Speicher zugreifen. Zu den neuen Quellen gehören [!DNL Amazon S3]-, [!DNL Azure Blob]- und FTP-/SFTP-Server. |

**Bekannte Probleme**

* Source-Connectoren für Cloud-basierte Speicher unterstützen die Aufnahme komprimierter Dateien nicht.

Weiterführende Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Mit Adobe Experience Platform [!DNL Data Science Workspace] können Datenwissenschaftler nahtlos Einblicke aus Daten und Inhalten in Adobe-Anwendungen und Drittanbietersystemen generieren, indem sie Modelle für maschinelles Lernen erstellen und umsetzen. [!DNL Data Science Workspace] ist eng in [!DNL Experience Platform] integriert und unterstützt den gesamten Datenwissenschafts-Lebenszyklus, einschließlich der Untersuchung und Vorbereitung von XDM-Daten, gefolgt von der Entwicklung und Operationalisierung von Modellen zur automatischen Anreicherung von [!DNL Real-Time Customer Profile] mit Einblicken aus maschinellem Lernen.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Datenzugriff mit [!DNL Experience Platform] SDK | Vordefinierte Rezepte und Starter-Notebooks in [!DNL Python] verwenden jetzt [!DNL Experience Platform] SDK für den Datenzugriff. |
| Unterstützung für Sandboxes | Unterstützung bevorstehender Sandbox-Funktionen (derzeit in der Beta-Phase), einschließlich der Möglichkeit, Notebooks und Rezepte in Entwicklungs- oder Produktions-Sandboxes zu isolieren. Weiterführende Informationen dazu finden Sie unter [Sandbox-Übersicht](../../sandboxes/home.md). |

Weitere Informationen finden Sie unter [Übersicht über Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Experience Data Model] (XDM)-System {#xdm}

Standardisierung und Interoperabilität sind Schlüsselkonzepte von [!DNL Experience Platform]. Das von Adobe unterstützte [!DNL Experience Data Model] (XDM)-System ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemata für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| ---------- | ------------ |
| Benachrichtigungsschema | Neues Schema, das die Benachrichtigungsdaten darstellt, die während der Datenaufnahme gesendet werden. |
| Adobe AdCloud DSP-Schemata | Es wurden fünf neue Schemata hinzugefügt, die die Metadaten der Demand-Side-Platform (DSP) von Adobe Advertising Cloud darstellen: Platzierung, Kampagne, Paket, Advertiser, Konto. |
| Schemafeldgruppen für ExperienceEvent-Implementierungsdetails | Neue ExperienceEvent-Feldergruppen, die ein Standardfeld hinzufügen, um Informationen über die Software zu speichern, die zum Erfassen des Ereignisses verwendet wird. |
| [!DNL Profile Privacy] Feldergruppen | Neue Profilfeldgruppen, die Felder hinzufügen, um allgemeine Opt-out- und Opt-out-Signale für Verkäufe/Freigabe für [!DNL Real-Time Customer Profile] zu akzeptieren. |
| Formateinschränkungen für `xdm:alternateDisplayInfo` | Die Felder „Titel“ und „Beschreibung“ für `xdm:alternateDisplayInfo` müssen beide Zeichenfolgen sein, damit die Validierung erfolgreich ist. |
| Namensänderung: XDM [!DNL Individual Profile] | Der „Titel“ der Klasse „XDM [!DNL Profile]&quot; wurde in „XDM [!DNL Individual Profile]&quot; geändert. Die formale `$id` der Klasse hat sich nicht geändert. |

**Bekannte Probleme**

* Keine.

Weitere Informationen zum Arbeiten mit XDM mithilfe der [!DNL Schema Registry]-API und [!DNL Schema Editor] Benutzeroberfläche finden Sie in der [XDM-Systemdokumentation](../../xdm/home.md).

## [!DNL Real-Time Customer Profile] {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das [!DNL Real-Time Customer Profile] ermöglicht eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen sowie anderen Kanälen miteinander kombiniert. [!DNL Profile] können Sie Ihre unterschiedlichen Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige, Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

| Funktion | Beschreibung |
| -----------| ---------- |
| Verbesserungen bei der [!DNL Profile] | Benutzer können jetzt Profile mithilfe von Referenzdeskriptoren und zugehörigen Entitäten suchen. |
| Bereinigen von Daten für einen bestimmten Datensatz | Benutzer können jetzt Daten für einen bestimmten Datensatz oder Batch mithilfe der Vorgangs-API des [!DNL Profile] löschen. |
| Verbesserungen bei Edge [!DNL Profile]-Abfragen | Programme können jetzt Edge-[!DNL Profile] nach einer beliebigen Identität eines bestimmten Profils abfragen. |
| Konfigurieren von Zusammenführungsrichtlinien pro Projektion | Anwendungen können jetzt Zusammenführungsrichtlinien pro Projektion konfigurieren, um eine Ansicht der Daten zu generieren, die von einer bestimmten Zusammenführungsrichtlinie gesteuert wird. |
| Berechnete Attribute | Berechnete Attribute berechnen den Wert von Feldern automatisch anhand anderer Werte, Berechnungen und Ausdrücke. Berechnete Attribute arbeiten auf Profilebene, um Werte wie „Gesamtkauf“, „Lebenszeitwert“ oder „Trichterstatus“ basierend auf einem eingehenden Ereignis, einem eingehenden Ereignis und Profildaten oder einem eingehenden Ereignis, Profildaten und historischen Ereignissen zu aggregieren. |

**Fehlerkorrekturen**

* Vereinfachte Liste der verfügbaren ID-Zuordnungsstrategien im Workflow zur Erstellung von Zusammenführungsrichtlinien.

**Bekannte Probleme**

* Keine.

Weitere Informationen zu [!DNL Real-Time Customer Profile], einschließlich Tutorials und Best Practices für die Arbeit mit [!DNL Profile]-Daten, finden [&#x200B; in der Übersicht zum Echtzeit-Kundenprofil](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente generieren und aus Ihren [!DNL Real-Time Customer Profile]-Daten Zielgruppen erstellen können. Diese Segmente werden zentral in [!DNL Experience Platform] konfiguriert und gepflegt, sodass sie für jede Adobe-Anwendung leicht zugänglich sind.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

| Funktion | Beschreibung |
| -----------| ---------- |
| Geplante Segmentierung | Benutzer können jetzt die geplante Segmentauswertung für alle Segmente über die Benutzeroberfläche und die API aktivieren. Nach der Aktivierung werden alle Segmente einmal täglich ausgewertet. Dies wirkt sich nicht auf die On-Demand-Segmentierungsfunktionen aus, die weiterhin wie zuvor funktionieren.<br/><br/>Hinweis: Die geplante Segmentierungsfunktion kann nicht in Sandboxes mit mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] verwendet werden. |
| Streaming-Segmentierung  | Unterstützung für die kontinuierliche Auswertung von Segmenten (Streaming-Segmentierung) ermöglicht es, die meisten Segmentregeln auszuwerten, während die Daten in [!DNL Experience Platform] übermittelt werden. Diese Funktion bedeutet, dass die Segmentzugehörigkeit auf dem neuesten Stand ist, ohne dass geplante Segmentierungsaufträge ausgeführt werden müssen. Es gelten einige Ausnahmen, z. B. Segmente, die Beziehungen mit mehreren Entitäten nutzen, oder Segmente mit angereicherten Payloads. |
| Segmente als Bausteine | Beim Erstellen von Segmenten mit der Segment Builder-Benutzeroberfläche können Benutzende jetzt zuvor definierte Segmente als Bausteine für zusätzliche Segmente verwenden. <ul><li>Referenzieren der aktuellen Zielgruppenzugehörigkeit: Aktualisierungen, wenn Personen in Zielgruppen hinein- und heraus wechseln.</li><li>Logik kopieren: Die ausgewählte Segmentdefinition nehmen und im neuen Segment duplizieren.</li></ul> |
| Anzeigen der Segmentzugehörigkeit nach ID-Namespace | Die Segmentzugehörigkeit kann jetzt nach ID-Namespace (E-Mail, ECID und Gesamtanzahl) angezeigt werden. |
| RBAC-Unterstützung | Segment Builder bietet jetzt Unterstützung für grundlegende rollenbasierte Zugriffssteuerungen und Berechtigungen. |
| Verbesserte Unterstützung für die Freigabe externer Zielgruppen zwischen [!DNL Experience Platform]- und Adobe-Lösungen | Benutzende können jetzt externe (nicht [!DNL Experience Platform]) Zielgruppen-Metadaten in Szenarien einbringen, in denen die Anzahl der Zielgruppen groß oder von vornherein nicht bekannt ist. Diese Version umfasst den Zugriff auf [!DNL Audience Manager] Metadaten für Kunden, die den Lösungs-Connector bereitgestellt haben. Diese Zielgruppen-Metadaten können in Segment Builder verwendet werden, um neue [!DNL Experience Platform] zu erstellen. <br/><br/> Darüber hinaus sind in [!DNL Experience Platform] erstellte Segmente jetzt für die Verwendung in integrierten Adobe-Lösungen verfügbar, einschließlich [!DNL Audience Manager], [!DNL Target] und [!DNL Ad Cloud]. |

**Fehlerkorrekturen**

* Es wurde ein Problem behoben, das dazu führte, dass bei der Segmentierung mehrerer Entitäten im Falle verschachtelter Beziehungen null Profile zurückgegeben wurden.
* Es wurde ein Problem behoben, bei dem die Ausschlusslogik irreführende Ergebnisse zurückgab.
* Verbesserte Lesbarkeit für Ordner mit mehreren Entitäten. Sie zeigen jetzt den Anzeigenamen der XDM-Klasse an.
* Es wurde ein zeitweiliges Problem behoben, bei dem mehrere Kopien desselben XDM-Ordners erschienen.
* Die Nachricht wird jetzt erstellt, um Benutzende darüber zu informieren, ob Segmentschätzungen für die ausgewählte Zusammenführungsrichtlinie nicht verfügbar sind.

**Bekannte Probleme**

* Keine.

Weitere Informationen zu [!DNL Segmentation Service] finden Sie unter [Segmentierungs-Service - Übersicht](../../segmentation/home.md).
