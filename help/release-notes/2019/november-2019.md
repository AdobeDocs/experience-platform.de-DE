---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform 18. November 2019
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 31%

---

# Adobe Experience Platform – Versionshinweise

**Releasedatum: 18. November 2019**

Neue Funktionen in Adobe Experience Platform:
* [[!DNL Real-time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

Aktualisierungen vorhandener Funktionen:
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Die auf Adobe Experience Platform aufbauende Echtzeit-Kundendatenplattform (Real-time CDP) hilft Unternehmen dabei, bekannte und unbekannte Daten zusammenzuführen, um Kundenprofile durch intelligente Entscheidungen auf der gesamten Journey zu aktivieren. Die Echtzeit-Kundendatenplattform fasst unterschiedliche Unternehmensdatenquellen zusammen, um in Echtzeit einheitliche Profile zu erstellen, die über alle Kanäle und Geräte hinweg ein personalisiertes Kundenerlebnis möglich machen.

[!DNL Real-time Customer Data Platform] umfasst Tools für Data Governance, Identitätsverwaltung, erweiterte Segmentierung und Datenwissenschaft, damit Sie Profile erstellen und Zielgruppen definieren sowie umfassende Einblicke gewinnen und gleichzeitig strikte Data Governance-Richtlinien durchsetzen können.

Adobe bietet Verbindungen zu einem großen Partnernetzwerk sowie native Integrationen mit Adobe Experience Cloud, damit Sie Zielgruppen nahtlos aktivieren und über alle Kanäle hinweg für herausragende Kundenerlebnisse sorgen können – von der Personalisierung vor Ort oder in Apps über E-Mail bis hin zu Paid Media, Callcentern, vernetzten Geräten und mehr.

Mit der Echtzeit-Kundendatenplattform profitieren Sie von folgenden Vorteilen:

* Verschaffen Sie sich einen Überblick über Ihre Kunden mit einer Streaming-Sammlung von Kundendaten aus dem gesamten Unternehmen.
* Sorgen Sie für eine angemessene Verwaltung von Profilen mit vertrauenswürdigen Governance- und Datenschutzkontrollen für bekannte und unbekannte Kennungen.
* Erstellen Sie mit KI und maschinellem Lernen auf Basis von Adobe Sensei – entwickelt für Marketer – praktische Einblicke und skalieren Sie Zielgruppen.
* Schaffen Sie in Echtzeit personalisierte Erlebnisse über alle Kanäle und Ziele hinweg.

Weitere Informationen finden Sie in der [Dokumentation zur Echtzeit-Kundendatenplattform](../../rtcdp/overview.md).

**Wichtigste Funktionen**

| Funktion | Beschreibung |
|---|---|
| Ziele | Vordefinierte Integrationen mit Zielplattformen, die von [!DNL Real-time Customer Data Platform] der Adobe unterstützt werden und die Daten nahtlos für diese Partner aktivieren. Weitere Informationen finden Sie unten unter [Ziele](#destinations) . |
| Dashboard für Metriken auf der Startseite | Die Startseite der Echtzeit-Kundendatenplattform (Echtzeit-Kundendatenplattform) enthält ein Metriken-Dashboard, das Informationen zu Profilen und Segmenten anzeigt. Die Startseite enthält auch Links zu Lernmaterialien. Siehe den Abschnitt [Metriken der Echtzeit-Kundendatenplattform](#real-time-customer-data-platform-metrics) weiter unten. |
| Quellen | Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Lösungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System. Weitere Informationen finden Sie unten im Abschnitt [Quellen](#sources) . |

**[!DNL Real-time Customer Data Platform]Metriken**

Die Startseite der Echtzeit-Kundendatenplattform von , die ein Metriken-Dashboard enthält, wird angezeigt, sobald Sie sich bei der Echtzeit-Kundendatenplattform anmelden.

Die Startseite ist nur einer der Orte, an denen Metrikkarten angezeigt werden. Die Echtzeit-Kundendatenplattform stellt Metrikkarten während des gesamten Erlebnisses bereit. Diese Metriken informieren Sie über die Daten-, Profil- und Segmentzielgruppen im System.

Wenn zum Zeitpunkt der Anmeldung bei der Echtzeit-Kundendatenplattform keine Daten im System vorhanden sind, wird das Dashboard auf der Startseite nicht angezeigt. In dem Fall enthält die Startseite Lernmaterial für die erstmalige Nutzung. Bei der Datenerfassung wird das Dashboard automatisch aktualisiert, um Informationen zu diesen Daten anzuzeigen.

Weitere Informationen finden Sie unter [Übersicht über Metriken der Echtzeit-Kundendatenplattform](../../rtcdp/home-page-dashboards.md) .

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vordefinierte Integrationen mit Zielplattformen, die von der Echtzeit-Kundendatenplattform von Adobe unterstützt werden und die Daten nahtlos für diese Partner aktivieren. Weitere Informationen finden Sie im Artikel [Ziele - Übersicht](../../destinations/home.md) .

**Verfügbare Ziele**

Mit der November-Version unterstützt die Echtzeit-Kundendatenplattform von Adobe die folgenden Ziele:

* Adobe Advertising Cloud: [!DNL Google]
* E-Mail-Marketing: Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

Weitere Informationen zu den einzelnen Zielen finden Sie im [Zielkatalog](../../destinations/catalog/overview.md) .

**Bekannte Einschränkungen**

* Das Steuerelement zum Ermöglichen benutzerdefinierter Aktivierungszeitpläne im Aktivierungsfluss (Schritt &quot;Planung&quot;) ist bei der ersten Version nicht verfügbar.
* Es gibt derzeit keine Möglichkeit, eine Zielkonfiguration zu bearbeiten oder zu löschen. Um diese Einschränkung zu umgehen, können Sie das Ziel in der oberen rechten Ecke der [Zieldetailseite](../../destinations/ui/destination-details-page.md) aktivieren oder deaktivieren.
* Es gibt derzeit keine Überprüfung für Kontodetails, Pfad oder Anmeldeinformationen, wenn eine Verbindung zu Ihrem Ziel- oder Speicherkonto hergestellt wird. Vergewissern Sie sich, dass Sie die richtigen Anmeldeinformationen eingeben und auf Rechtschreibfehler oder Tippfehler prüfen.
* Mit der ersten Veröffentlichung wurden keine Anmeldeinformationen erneuert. Sobald ein Konto abgelaufen ist oder aktualisiert werden muss, müssen Sie eine neue Zielverbindung erstellen und Ihre zuvor zugeordneten Segmente neu erstellen.

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen und gleichzeitig diese Daten mithilfe von [!DNL Platform]-Diensten strukturieren, beschriften und erweitern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Lösungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Diese Quellverbindungen ermöglichen Ihnen eine Authentifizierung mit Ihren Datenspeichern und CRM-Diensten, die Festlegung von Zeiten für Erfassungsläufe und die Verwaltung des Durchsatzes bei der Datenerfassung.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ---------- | ------------ |
| Quellen-Benutzeroberfläche | Neue Benutzeroberfläche zum Erstellen, Anzeigen und Verwalten von Quellverbindungen. |
| Überarbeitete Workflows für CRM-Connectoren | Neuer intuitiver UI-Workflow für die Erstellung und Verwaltung von [!DNL Microsoft Dynamics]- und [!DNL Salesforce]-Connectoren. |
| Connector-Unterstützung für Cloud-basierte Speicher | Connectoren können jetzt auf Cloud-basierte Speicher zugreifen. Zu den neuen Quellen gehören [!DNL Amazon S3], [!DNL Azure Blob] und FTP/SFTP-Server. |

**Bekannte Probleme**

* Quell-Connectoren für Cloud-basierte Speicher unterstützen nicht die Erfassung komprimierter Dateien.

Weiterführende Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] ermöglicht es Datenwissenschaftlern, nahtlos Einblicke aus Daten und Inhalten in Adobe Apps und Drittanbietersystemen zu generieren, indem sie Modelle für maschinelles Lernen erstellen und umsetzen. [!DNL Data Science Workspace] ist eng in den durchgängigen Datenwissenschaftslebenszyklus integriert  [!DNL Platform] und ermöglicht ihn, einschließlich der Erforschung und Vorbereitung von XDM-Daten, gefolgt von der Entwicklung und Inbetriebnahme von Modellen zur automatischen Anreicherung  [!DNL Real-time Customer Profile] mit Insights für maschinelles Lernen.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Datenzugriff mit dem [!DNL Platform]-SDK | Vordefinierte Rezepte und Starter-Notebooks in [!DNL Python] verwenden jetzt das [!DNL Platform]-SDK für den Zugriff auf Daten. |
| Unterstützung für Sandboxes | Unterstützung bevorstehender Sandbox-Funktionen (aktuell in Beta-Version), einschließlich der Möglichkeit, Notebooks und Rezepte in Entwicklungs- oder Produktions-Sandboxes zu isolieren. Weiterführende Informationen dazu finden Sie unter [Sandbox-Übersicht](../../sandboxes/home.md). |

Weitere Informationen finden Sie unter [Übersicht über Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Experience Data Model] (XDM)-System {#xdm}

Standardisierung und Interoperabilität sind Schlüsselkonzepte von [!DNL Experience Platform]. Das von Adobe unterstützte [!DNL Experience Data Model] (XDM)-System ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| ---------- | ------------ |
| Benachrichtigungsschema | Neues Schema für Benachrichtigungsdaten, die während des Datenerfassungsprozesses gesendet werden. |
| Adobe AdCloud-DSP | Es wurden fünf neue Schemata hinzugefügt, die Adobe Advertising Cloud-DSP-Metadaten (Demand Side Platform) darstellen: Platzierung, Kampagne, Paket, Advertiser, Konto. |
| Schemafelder für ExperienceEvent-Implementierungsdetails | Neue ExperienceEvent-Feldergruppen, die ein Standardfeld hinzufügen, um Informationen über die Software zu speichern, mit der das Ereignis erfasst wird. |
| [!DNL Profile Privacy] Feldergruppen | Neue Profilfeldgruppen, die Felder hinzufügen, um allgemeine Opt-out- und Verkaufs-/Freigabe-Opt-out-Signale für [!DNL Real-time Customer Profile] zu akzeptieren. |
| Formateinschränkungen für `xdm:alternateDisplayInfo` | Die Felder &quot;Titel&quot;und &quot;Beschreibung&quot;für `xdm:alternateDisplayInfo` müssen beide Zeichenfolgen sein, um die Validierung zu bestehen. |
| Namensänderung: XDM [!DNL Individual Profile] | Der &quot;Titel&quot;der Klasse &quot;XDM [!DNL Profile]&quot;wurde auf &quot;XDM [!DNL Individual Profile]&quot;aktualisiert. Die formale `$id` der Klasse wurde nicht geändert. |

**Bekannte Probleme**

* Keine.

Weitere Informationen zum Arbeiten mit XDM unter Verwendung der [!DNL Schema Registry]-API und der [!DNL Schema Editor]-Benutzeroberfläche finden Sie in der [XDM-Systemdokumentation](../../xdm/home.md).

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. Mit [!DNL Real-time Customer Profile] können Sie eine ganzheitliche Ansicht jedes einzelnen Kunden anzeigen, die Daten aus mehreren Kanälen kombiniert, einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten. [!DNL Profile] ermöglicht es Ihnen, Ihre unterschiedlichen Kundendaten in einer einheitlichen Ansicht zusammenzufassen, die eine umsetzbare, mit Zeitstempel versehene Übersicht über jede Kundeninteraktion bietet.

| Funktion | Beschreibung |
| -----------| ---------- |
| Verbesserungen der [!DNL Profile]-Suche | Benutzer können jetzt Profile mithilfe von Referenzdeskriptoren und verwandten Entitäten nachschlagen. |
| Daten für einen bestimmten Datensatz bereinigen | Benutzer können jetzt Daten für einen bestimmten Datensatz oder Batch mithilfe der [!DNL Profile]-Systemaufträge-API löschen. |
| Edge [!DNL Profile]-Abfrageverbesserungen | Anwendungen können jetzt Edge [!DNL Profile] anhand einer der Identitäten eines bestimmten Profils abfragen. |
| Zusammenführungsrichtlinien pro Projektion konfigurieren | Anwendungen können jetzt Zusammenführungsrichtlinien für jede Projektion konfigurieren, um eine Ansicht der Daten zu generieren, die von einer bestimmten Zusammenführungsrichtlinie verwaltet werden. |
| Berechnete Attribute | Berechnete Attribute berechnen automatisch den Wert von Feldern basierend auf anderen Werten, Berechnungen und Ausdrücken. Berechnete Attribute dienen auf der Profilebene dazu, Werte wie &quot;Gesamtkauf&quot;, &quot;Lebenszeitwert&quot;oder &quot;Trichterstatus&quot;basierend auf einem eingehenden Ereignis, einem eingehenden Ereignis und Profildaten oder einem eingehenden Ereignis, Profildaten und historischen Ereignissen zu aggregieren. |

**Fehlerkorrekturen**

* Vereinfachte Liste der verfügbaren ID-Zuordnungsstrategien im Workflow zur Erstellung von Zusammenführungsrichtlinien.

**Bekannte Probleme**

* Keine.

Weitere Informationen zu [!DNL Real-time Customer Profile], einschließlich Tutorials und Best Practices für die Arbeit mit [!DNL Profile]-Daten, finden Sie in der [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und aus Ihren [!DNL Real-time Customer Profile]-Daten Zielgruppen generieren können. Diese Segmente werden zentral in [!DNL Platform] konfiguriert und gepflegt, sodass sie für jede Adobe-Anwendung leicht zugänglich sind.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

| Funktion | Beschreibung |
| -----------| ---------- |
| Geplante Segmentierung | Benutzer können jetzt die geplante Segmentbewertung für alle Segmente über die Benutzeroberfläche und die API aktivieren. Nach der Aktivierung werden alle Segmente einmal täglich ausgewertet. Dies hat keine Auswirkungen auf die On-Demand-Segmentierungsfunktionen, die weiterhin wie bisher funktionieren.<br/><br/>Hinweis: Die Funktion für die geplante Segmentierung kann nicht in Sandboxes mit mehr als fünf Zusammenführungsrichtlinien für  [!DNL XDM Individual Profile]verwendet werden. |
| Streaming-Segmentierung | Die Unterstützung für die kontinuierliche Auswertung von Segmenten (Streaming-Segmentierung) ermöglicht die Auswertung der meisten Segmentregeln, da die Daten an [!DNL Platform] übergeben werden. Diese Funktion bedeutet, dass die Segmentzugehörigkeit aktuell ist, ohne dass geplante Segmentierungsaufträge ausgeführt werden müssen. Es gelten einige Ausnahmen, z. B. Segmente, die Beziehungen mit mehreren Entitäten nutzen, oder mit angereicherten Payloads. |
| Segmente als Bausteine | Beim Erstellen von Segmenten mithilfe der Segment Builder-Benutzeroberfläche können Benutzer jetzt zuvor definierte Segmente als Bausteine für weitere Segmente verwenden. <ul><li>Aktuelle Zielgruppenzugehörigkeit referenzieren: aktualisiert, wenn Benutzer in Zielgruppen einsteigen und aus ihnen aussteigen.</li><li>Logik kopieren: nehmen Sie die ausgewählte Segmentdefinition und duplizieren Sie sie im neuen Segment.</li></ul> |
| Anzeigen der Segmentmitgliedschaft nach ID-Namespace | Die Segmentzugehörigkeit kann jetzt nach ID-Namespace (E-Mail, ECID und Gesamtanzahl) angezeigt werden. |
| RBAC-Unterstützung | Segment Builder bietet jetzt Unterstützung für grundlegende rollenbasierte Zugriffssteuerungen und Berechtigungen. |
| Erweiterte Unterstützung für die Freigabe externer Zielgruppen zwischen [!DNL Platform] und Adobe-Lösungen | Benutzer können jetzt externe (nicht-[!DNL Experience Platform]) Zielgruppen-Metadaten in Szenarien einbringen, in denen die Anzahl der Zielgruppen groß oder nicht von vornherein bekannt ist. Diese Version enthält Zugriff auf [!DNL Audience Manager]-Metadaten für Kunden, die den Lösungs-Connector bereitgestellt haben. Diese Zielgruppen-Metadaten können in Segment Builder verwendet werden, um neue [!DNL Experience Platform]-Segmente zu erstellen. <br/><br/> Darüber hinaus  [!DNL Experience Platform] werden Segmente, die in erstellt wurden, jetzt für die Verwendung in integrierten Adobe-Lösungen wie  [!DNL Audience Manager],  [!DNL Target] und  [!DNL Ad Cloud]verfügbar sein. |

**Fehlerkorrekturen**

* Es wurde ein Fehler behoben, der dazu führte, dass bei der Segmentierung mit mehreren Entitäten bei verschachtelten Beziehungen Nullprofile zurückgegeben wurden.
* Es wurde ein Problem behoben, bei dem die Ausschlusslogik irreführende Ergebnisse zurückgab.
* Verbesserte Lesbarkeit für Ordner mit mehreren Entitäten. Jetzt wird der Anzeigename der XDM-Klasse angezeigt.
* Es wurde ein zeitweiliger Fehler behoben, bei dem mehrere Kopien desselben XDM-Ordners angezeigt wurden.
* Nachrichten werden jetzt erzeugt, um einen Benutzer zu informieren, wenn für die ausgewählte Zusammenführungsrichtlinie keine Segmentschätzungen verfügbar sind.

**Bekannte Probleme**

* Keine.

Weitere Informationen zu [!DNL Segmentation Service] finden Sie unter [Übersicht über den Segmentation Service](../../segmentation/home.md).
