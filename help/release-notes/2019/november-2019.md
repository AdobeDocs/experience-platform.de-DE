---
title: Adobe Experience Platform - Versionshinweise, November 2019
description: Versionshinweise von November 2019 für Adobe Experience Platform.
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 28%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 18. November 2019**

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

Die auf Adobe Experience Platform aufbauende Real-time Customer Data Platform (Real-Time CDP) hilft Unternehmen dabei, bekannte und unbekannte Daten zusammenzuführen, um Kundenprofile durch intelligente Entscheidungen auf der gesamten Journey zu aktivieren. Real-Time CDP kombiniert mehrere Unternehmensdatenquellen, um in Echtzeit einheitliche Profile zu erstellen, die über alle Kanäle und Geräte hinweg personalisierte Kundenerlebnisse bieten.

[!DNL Real-Time Customer Data Platform] umfasst Tools für Data Governance, Identitätsverwaltung, erweiterte Segmentierung und Datenwissenschaft, damit Sie Profile erstellen und Zielgruppen definieren sowie umfassende Einblicke gewinnen und gleichzeitig strikte Data Governance-Richtlinien durchsetzen können.

Adobe bietet Verbindungen zu einem großen Partnernetzwerk sowie native Integrationen mit Adobe Experience Cloud, damit Sie Zielgruppen nahtlos aktivieren und über alle Kanäle hinweg für herausragende Kundenerlebnisse sorgen können – von der Personalisierung vor Ort oder in Apps über E-Mail bis hin zu Paid Media, Callcentern, vernetzten Geräten und mehr.

Mit Real-Time CDP können Sie:

* Verschaffen Sie sich einen Überblick über Ihre Kunden mit einer Streaming-Sammlung von Kundendaten aus dem gesamten Unternehmen.
* Sorgen Sie für eine angemessene Verwaltung von Profilen mit vertrauenswürdigen Governance- und Datenschutzkontrollen für bekannte und unbekannte Kennungen.
* Erstellen Sie mit KI und maschinellem Lernen auf Basis von Adobe Sensei – entwickelt für Marketer – praktische Einblicke und skalieren Sie Zielgruppen.
* Schaffen Sie in Echtzeit personalisierte Erlebnisse über alle Kanäle und Ziele hinweg.

Weitere Informationen finden Sie unter [Real-time Customer Data Platform-Dokumentation](../../rtcdp/overview.md).

**Wichtigste Funktionen**

| Funktion | Beschreibung |
|---|---|
| Ziele | Vorgefertigte Integrationen mit Zielplattformen, die von der Adobe [!DNL Real-Time Customer Data Platform] die Daten für diese Partner nahtlos aktivieren. Siehe [Ziele](#destinations) unten finden Sie weitere Informationen. |
| Dashboard für Metriken auf der Startseite | Die Startseite von Real-time Customer Data Platform (Real-Time CDP) enthält ein Metrik-Dashboard, das Informationen zu Profilen und Segmenten anzeigt. Die Startseite enthält auch Links zu Lernmaterialien. Siehe Abschnitt zu [Real-time Customer Data Platform-Metriken](#real-time-customer-data-platform-metrics) unten. |
| Quellen | Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Lösungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System. Siehe [Quellen](#sources) weiter unten, um mehr zu erfahren. |

**[!DNL Real-Time Customer Data Platform]Metriken**

Die Startseite von Real-time Customer Data Platform (Real-Time CDP) mit einem Metriken-Dashboard wird angezeigt, wenn Sie sich bei Real-Time CDP anmelden.

Die Startseite ist nur einer der Orte, an denen Metrikkarten angezeigt werden. Real-Time CDP bietet Metrikkarten für das gesamte Erlebnis. Diese Metriken informieren Sie über die Daten-, Profil- und Segmentzielgruppen im System.

Wenn bei der Anmeldung bei Real-Time CDP keine Daten im System vorhanden sind, wird das Dashboard auf der Startseite nicht angezeigt. In dem Fall enthält die Startseite Lernmaterial für die erstmalige Nutzung. Bei der Datenerfassung wird das Dashboard automatisch aktualisiert, um Informationen zu diesen Daten anzuzeigen.

Weitere Informationen finden Sie unter [Übersicht über Real-time Customer Data Platform-Metriken](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vordefinierte Integrationen mit Zielplattformen, die von Real-time Customer Data Platform von Adobe unterstützt werden und die Daten nahtlos für diese Partner aktivieren. Weitere Informationen finden Sie im Abschnitt [Ziele - Übersicht](../../destinations/home.md) Artikel.

**Verfügbare Ziele**

Mit der November-Version unterstützt Real-time Customer Data Platform der Adobe die folgenden Ziele:

* Advertising: [!DNL Google]
* E-Mail-Marketing: Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

Siehe [Zielkatalog](../../destinations/catalog/overview.md) für Informationen zu den einzelnen Zielen.

**Bekannte Einschränkungen**

* Das Steuerelement zum Ermöglichen benutzerdefinierter Aktivierungszeitpläne im Aktivierungsfluss (Schritt &quot;Planung&quot;) ist bei der ersten Version nicht verfügbar.
* Es gibt derzeit keine Möglichkeit, eine Zielkonfiguration zu bearbeiten oder zu löschen. Um diese Einschränkung zu umgehen, können Sie das Ziel in der oberen rechten Ecke der [Zieldetailseite](../../destinations/ui/destination-details-page.md).
* Es gibt derzeit keine Überprüfung für Kontodetails, Pfad oder Anmeldeinformationen, wenn eine Verbindung zu Ihrem Ziel- oder Speicherkonto hergestellt wird. Vergewissern Sie sich, dass Sie die richtigen Anmeldeinformationen eingeben und auf Rechtschreibfehler oder Tippfehler prüfen.
* Mit der ersten Veröffentlichung wurden keine Anmeldeinformationen erneuert. Sobald ein Konto abgelaufen ist oder aktualisiert werden muss, müssen Sie eine neue Zielverbindung erstellen und Ihre zuvor zugeordneten Segmente neu erstellen.

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen und gleichzeitig diese Daten strukturieren, beschriften und erweitern, indem es [!DNL Platform] Dienste. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Lösungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Diese Quellverbindungen ermöglichen Ihnen eine Authentifizierung mit Ihren Datenspeichern und CRM-Diensten, die Festlegung von Zeiten für Erfassungsläufe und die Verwaltung des Durchsatzes bei der Datenerfassung.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ---------- | ------------ |
| Quellen-Benutzeroberfläche | Neue Benutzeroberfläche zum Erstellen, Anzeigen und Verwalten von Quellverbindungen. |
| Überarbeitete Workflows für CRM-Connectoren | Neuer intuitiver UI-Arbeitsablauf für die Erstellung und Verwaltung [!DNL Microsoft Dynamics] und [!DNL Salesforce] Connectoren. |
| Connector-Unterstützung für Cloud-basierte Speicher | Connectoren können jetzt auf Cloud-basierte Speicher zugreifen. Neue Quellen umfassen [!DNL Amazon S3], [!DNL Azure Blob]und FTP-/SFTP-Server. |

**Bekannte Probleme**

* Quell-Connectoren für Cloud-basierte Speicher unterstützen nicht die Erfassung komprimierter Dateien.

Weiterführende Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] ermöglicht es Datenwissenschaftlern, nahtlos Einblicke aus Daten und Inhalten in Adobe Apps und Drittanbietersystemen zu generieren, indem sie Modelle für maschinelles Lernen erstellen und umsetzen. [!DNL Data Science Workspace] eng in [!DNL Platform] und ermöglicht den durchgängigen Data Science-Lebenszyklus, einschließlich der Erforschung und Vorbereitung von XDM-Daten, gefolgt von der Entwicklung und Inbetriebnahme von Modellen zur automatischen Anreicherung [!DNL Real-Time Customer Profile] mit Insights für maschinelles Lernen.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Datenzugriff mithilfe von [!DNL Platform] SDK | Vordefinierte Rezepte und Starter-Notebooks in [!DNL Python] jetzt verwenden [!DNL Platform] SDK für den Zugriff auf Daten. |
| Unterstützung für Sandboxes | Unterstützung bevorstehender Sandbox-Funktionen (aktuell in Beta-Version), einschließlich der Möglichkeit, Notebooks und Rezepte in Entwicklungs- oder Produktions-Sandboxes zu isolieren. Weiterführende Informationen dazu finden Sie unter [Sandbox-Übersicht](../../sandboxes/home.md). |

Weitere Informationen finden Sie unter [Data Science Workspace - Übersicht](../../data-science-workspace/home.md).

## [!DNL Experience Data Model] (XDM)-System {#xdm}

Standardisierung und Interoperabilität sind Schlüsselkonzepte von [!DNL Experience Platform]. Das von Adobe unterstützte [!DNL Experience Data Model] (XDM)-System ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| ---------- | ------------ |
| Benachrichtigungsschema | Neues Schema für Benachrichtigungsdaten, die während des Datenerfassungsprozesses gesendet werden. |
| Adobe AdCloud-DSP | Es wurden fünf neue Schemata hinzugefügt, die Adobe Advertising Cloud-DSP-Metadaten (Demand Side Platform) darstellen: Platzierung, Kampagne, Paket, Advertiser, Konto. |
| Schemafelder für ExperienceEvent-Implementierungsdetails | Neue ExperienceEvent-Feldergruppen, die ein Standardfeld hinzufügen, um Informationen über die Software zu speichern, mit der das Ereignis erfasst wird. |
| [!DNL Profile Privacy] Feldergruppen | Neue Profilfeldgruppen, die Felder hinzufügen, um allgemeine Opt-out- und Verkaufs-/Freigabe-Opt-out-Signale für [!DNL Real-Time Customer Profile]. |
| Formatbeschränkungen für `xdm:alternateDisplayInfo` | Die Felder &quot;Titel&quot;und &quot;Beschreibung&quot;für `xdm:alternateDisplayInfo` müssen beide Zeichenfolgen sein, um die Validierung zu bestehen. |
| Namensänderung: XDM [!DNL Individual Profile] | Der &quot;Titel&quot;des &quot;XDM&quot; [!DNL Profile]&quot;-Klasse wurde auf &quot;XDM&quot;aktualisiert. [!DNL Individual Profile]&quot;. Die formelle `$id` der Klasse hat sich nicht geändert. |

**Bekannte Probleme**

* Keine.

Weitere Informationen zum Arbeiten mit XDM unter Verwendung der [!DNL Schema Registry] API und [!DNL Schema Editor] Die Benutzeroberfläche finden Sie in der [XDM-Systemdokumentation](../../xdm/home.md).

## [!DNL Real-Time Customer Profile] {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. Mit [!DNL Real-Time Customer Profile]können Sie eine ganzheitliche Ansicht jedes einzelnen Kunden anzeigen, die Daten aus mehreren Kanälen kombiniert, einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten. [!DNL Profile] ermöglicht es Ihnen, Ihre unterschiedlichen Kundendaten in einer einheitlichen Ansicht zusammenzufassen, die eine umsetzbare, mit Zeitstempel versehene Übersicht über jede Kundeninteraktion bietet.

| Funktion | Beschreibung |
| -----------| ---------- |
| Verbesserungen an [!DNL Profile] Nachschlagen | Benutzer können jetzt Profile mithilfe von Referenzdeskriptoren und verwandten Entitäten nachschlagen. |
| Daten für einen bestimmten Datensatz bereinigen | Benutzer können jetzt Daten für einen bestimmten Datensatz oder Batch mithilfe der [!DNL Profile] Systemaufträge-API. |
| Edge [!DNL Profile] Abfrageverbesserungen | Anwendungen können jetzt Edge abfragen [!DNL Profile] durch eine der Identitäten eines bestimmten Profils. |
| Zusammenführungsrichtlinien pro Projektion konfigurieren | Anwendungen können jetzt Zusammenführungsrichtlinien für jede Projektion konfigurieren, um eine Ansicht der Daten zu generieren, die von einer bestimmten Zusammenführungsrichtlinie verwaltet werden. |
| Berechnete Attribute | Berechnete Attribute berechnen automatisch den Wert von Feldern basierend auf anderen Werten, Berechnungen und Ausdrücken. Berechnete Attribute dienen auf der Profilebene dazu, Werte wie &quot;Gesamtkauf&quot;, &quot;Lebenszeitwert&quot;oder &quot;Trichterstatus&quot;basierend auf einem eingehenden Ereignis, einem eingehenden Ereignis und Profildaten oder einem eingehenden Ereignis, Profildaten und historischen Ereignissen zu aggregieren. |

**Fehlerkorrekturen**

* Vereinfachte Liste der verfügbaren ID-Zuordnungsstrategien im Workflow zur Erstellung von Zusammenführungsrichtlinien.

**Bekannte Probleme**

* Keine.

Weitere Informationen finden Sie unter [!DNL Real-Time Customer Profile], einschließlich Tutorials und Best Practices für die Arbeit mit [!DNL Profile] Daten lesen Sie bitte die [Echtzeit-Kundenprofil - Überblick](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente generieren und aus Ihren [!DNL Real-Time Customer Profile]-Daten Zielgruppen erstellen können. Diese Segmente werden zentral in [!DNL Platform] konfiguriert und gepflegt, sodass sie für jede Adobe-Anwendung leicht zugänglich sind.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

| Funktion | Beschreibung |
| -----------| ---------- |
| Geplante Segmentierung | Benutzer können jetzt die geplante Segmentbewertung für alle Segmente über die Benutzeroberfläche und die API aktivieren. Nach der Aktivierung werden alle Segmente einmal täglich ausgewertet. Dies hat keine Auswirkungen auf die On-Demand-Segmentierungsfunktionen, die weiterhin wie bisher funktionieren.<br/><br/>Hinweis: Die Funktion für die geplante Segmentierung kann nicht in Sandboxes mit mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile]. |
| Streaming-Segmentierung  | Die Unterstützung für die kontinuierliche Auswertung von Segmenten (Streaming-Segmentierung) ermöglicht die Auswertung der meisten Segmentregeln, da die Daten an [!DNL Platform]. Diese Funktion bedeutet, dass die Segmentzugehörigkeit aktuell ist, ohne dass geplante Segmentierungsaufträge ausgeführt werden müssen. Es gelten einige Ausnahmen, z. B. Segmente, die Beziehungen mit mehreren Entitäten nutzen, oder mit angereicherten Payloads. |
| Segmente als Bausteine | Beim Erstellen von Segmenten mithilfe der Segment Builder-Benutzeroberfläche können Benutzer jetzt zuvor definierte Segmente als Bausteine für weitere Segmente verwenden. <ul><li>Aktuelle Zielgruppenzugehörigkeit referenzieren: aktualisiert, wenn Benutzer in Zielgruppen einsteigen und aus ihnen aussteigen.</li><li>Logik kopieren: nehmen Sie die ausgewählte Segmentdefinition und duplizieren Sie sie im neuen Segment.</li></ul> |
| Anzeigen der Segmentmitgliedschaft nach ID-Namespace | Die Segmentzugehörigkeit kann jetzt nach ID-Namespace (E-Mail, ECID und Gesamtanzahl) angezeigt werden. |
| RBAC-Unterstützung | Segment Builder bietet jetzt Unterstützung für grundlegende rollenbasierte Zugriffssteuerungen und Berechtigungen. |
| Erweiterte Unterstützung für die Freigabe externer Zielgruppen zwischen [!DNL Platform] und Adobe | Benutzer können jetzt externe Inhalte (nicht[!DNL Experience Platform]) Zielgruppen-Metadaten in Szenarien, in denen die Anzahl der Zielgruppen a priori groß oder nicht bekannt ist. Diese Version beinhaltet Zugriff auf [!DNL Audience Manager] Metadaten für Kunden, die den Lösungs-Connector bereitgestellt haben. Diese Zielgruppen-Metadaten können in Segment Builder zum Erstellen neuer [!DNL Experience Platform] Segmente. <br/><br/> Darüber hinaus werden Segmente, die in [!DNL Experience Platform] künftig in integrierten Adobe-Lösungen verfügbar sein, darunter [!DNL Audience Manager], [!DNL Target]und [!DNL Ad Cloud]. |

**Fehlerkorrekturen**

* Es wurde ein Fehler behoben, der dazu führte, dass bei der Segmentierung mit mehreren Entitäten bei verschachtelten Beziehungen Nullprofile zurückgegeben wurden.
* Es wurde ein Problem behoben, bei dem die Ausschlusslogik irreführende Ergebnisse zurückgab.
* Verbesserte Lesbarkeit für Ordner mit mehreren Entitäten. Jetzt wird der Anzeigename der XDM-Klasse angezeigt.
* Es wurde ein zeitweiliger Fehler behoben, bei dem mehrere Kopien desselben XDM-Ordners angezeigt wurden.
* Nachrichten werden jetzt erzeugt, um einen Benutzer zu informieren, wenn für die ausgewählte Zusammenführungsrichtlinie keine Segmentschätzungen verfügbar sind.

**Bekannte Probleme**

* Keine.

Weitere Informationen finden Sie unter [!DNL Segmentation Service], lesen Sie bitte die [Übersicht über den Segmentierungsdienst](../../segmentation/home.md).
