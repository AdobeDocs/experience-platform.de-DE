---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform, 18. November 2019
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: f881c1365684b1ca9e6bf9a8ce866d234dc54128
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 30%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: 18. November 2019**

Neue Funktionen in Adobe Experience Platform:
* [!DNL Real-time Customer Data Platform](#rtcdp)
* [!DNL Destinations](#destinations)
* [!DNL Sources](#sources)

Aktualisierungen vorhandener Funktionen:
* [!DNL Data Science Workspace](#dsw)
* [!DNL Experience Data Model (XDM) System](#xdm)
* [!DNL Real-time Customer Profile](#profile)
* [!DNL Segmentation Service](#segmentation)

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Die auf der Adobe Experience Platform aufbauende Adobe Echtzeit-Kundendatenplattform (Echtzeit-CDP) hilft Firmen, bekannte und unbekannte Daten zusammenzuführen, um Profil während der gesamten Customer Journey mit intelligenten Entscheidungen zu aktivieren. Die Echtzeit-Kundendatenplattform fasst unterschiedliche Unternehmensdatenquellen zusammen, um in Echtzeit einheitliche Profile zu erstellen, die über alle Kanäle und Geräte hinweg ein personalisiertes Kundenerlebnis möglich machen.

[!DNL Real-time Customer Data Platform] umfasst Tools für die Datenverwaltung, Identitätsverwaltung, erweiterte Segmentierung und Datenwissenschaften, damit Sie Profil erstellen und Audiencen definieren sowie umfassende Einblicke gewinnen können, während Sie strikte Datenverwaltungs-Richtlinien durchsetzen können.

Adobe bietet Verbindungen zu einem großen Partnernetzwerk sowie native Integrationen mit Adobe Experience Cloud, damit Sie Zielgruppen nahtlos aktivieren und über alle Kanäle hinweg für herausragende Kundenerlebnisse sorgen können – von der Personalisierung vor Ort oder in Apps über E-Mail bis hin zu Paid Media, Callcentern, vernetzten Geräten und mehr.

Mit der Echtzeit-Kundendatenplattform profitieren Sie von folgenden Vorteilen:

* Verschaffen Sie sich einen Überblick über Ihre Kunden mit einer Streaming-Sammlung von Kundendaten aus dem gesamten Unternehmen.
* Sorgen Sie für eine angemessene Verwaltung von Profilen mit vertrauenswürdigen Governance- und Datenschutzkontrollen für bekannte und unbekannte Kennungen.
* Erstellen Sie mit KI und maschinellem Lernen auf Basis von Adobe Sensei – entwickelt für Marketer – praktische Einblicke und skalieren Sie Zielgruppen.
* Schaffen Sie in Echtzeit personalisierte Erlebnisse über alle Kanäle und Ziele hinweg.

Weitere Informationen finden Sie in der Dokumentation [zur](../../rtcdp/overview.md)Adobe Echtzeit-Kundendatenplattform.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
|---|---|
| Ziele | Vordefinierte Integrationen mit von Adobe unterstützten Zielplattformen, [!DNL Real-time Customer Data Platform] die Daten nahtlos an diese Partner aktivieren. See [Destinations](#destinations) below for more information. |
| Dashboard zu Startseiten-Metriken | Die Startseite zur Adobe Echtzeit-Kundendatenplattform (Echtzeit-CDP) enthält ein Dashboard mit Metriken, in dem Informationen zu Profilen und Segmenten angezeigt werden. Die Startseite enthält auch Links zu Lernmaterialien. Siehe den Abschnitt zu den Metriken [der](#real-time-customer-data-platform-metrics) Echtzeit-Kundendatenplattform. |
| Quellen | Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Lösungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System. Weitere Informationen finden Sie im Abschnitt [Quellen](#sources) . |

**[!DNL Real-time Customer Data Platform]Metriken **

Die Startseite der Echtzeit-Kundendatenplattform von Adobe, die ein Metriken-Dashboard enthält, wird angezeigt, sobald Sie sich bei der Echtzeit-Kundendatenplattform anmelden.

Die Startseite ist nur einer der Orte, an denen Metrikkarten angezeigt werden. Die Echtzeit-Kundendatenplattform stellt Metrikkarten während des gesamten Erlebnisses bereit. Diese Metriken informieren Sie über die Daten-, Profil- und Segmentzielgruppen im System.

Wenn zum Zeitpunkt der Anmeldung bei der Echtzeit-Kundendatenplattform keine Daten im System vorhanden sind, wird das Dashboard auf der Startseite nicht angezeigt. In dem Fall enthält die Startseite Lernmaterial für die erstmalige Nutzung. Bei der Datenerfassung wird das Dashboard automatisch aktualisiert, um Informationen zu diesen Daten anzuzeigen.

Weitere Informationen finden Sie in der Übersicht über die Metriken der [Echtzeit-Kundendatenplattform](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorgefertigte Integrationen mit Zielplattformen, die von der Echtzeit-Kundendatenplattform von Adobe unterstützt werden und die Daten für diese Partner nahtlos aktivieren. Weitere Informationen finden Sie im Artikel [Ziele-Übersicht](../../rtcdp/destinations/destinations-overview.md) .

**Verfügbare Ziele**

Ab der November-Version unterstützt die Echtzeit-Kundendatenplattform von Adobe die folgenden Ziele:

* Werbung: [!DNL Google]
* E-Mail-Marketing: Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua
   ]
Informationen zu den einzelnen Zielen finden Sie im [Zielkatalog](../../rtcdp/destinations/destinations-catalog.md) .

**Bekannte Einschränkungen**

* Das Steuerelement zum Zulassen von Zeitplänen für benutzerdefinierte Aktivierungen im [Aktivierungen-Fluss](../../rtcdp/destinations/activate-destinations.md#activate-data) (Planschritt) ist in der ersten Version nicht verfügbar.
* Es gibt derzeit keine Möglichkeit, eine Zielkonfiguration zu bearbeiten oder zu löschen. Um diese Einschränkung zu umgehen, können Sie das Ziel oben rechts auf der Seite mit den [Zieldetails aktivieren oder deaktivieren](../../rtcdp/destinations/destination-details-page.md).
* Es gibt derzeit keine Überprüfung für Kontodetails, Pfad oder Anmeldeinformationen, wenn eine Verbindung mit Ihrem Ziel- oder Datenspeicherung-Konto hergestellt wird. Vergewissern Sie sich, dass Sie die richtigen Anmeldeinformationen eingeben und die Dublette auf Rechtschreibfehler oder Tippfehler überprüfen.
* Mit der ersten Version wurden keine Anmeldeinformationen verlängert. Nachdem ein Konto abgelaufen ist oder aktualisiert werden muss, müssen Sie eine neue Zielverbindung erstellen und Ihre zuvor zugeordneten Segmente neu zuordnen.

## Quellen {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Lösungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, damit Sie für verschiedene Datenanbieter bequem Quellverbindungen einrichten können. Diese Quellverbindungen ermöglichen Ihnen eine Authentifizierung mit Ihren Speichersystemen und CRM-Diensten, die Festlegung von Zeiten für Erfassungsläufe und die Verwaltung des Durchsatzes bei der Datenerfassung.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ---------- | ------------ |
| Quellbenutzeroberfläche | Neue Benutzeroberfläche zum Erstellen, Anzeigen und Verwalten von Quellverbindungen. |
| Überarbeitete Workflows für CRM-Connectors | Neuer intuitiver Arbeitsablauf für die Benutzeroberfläche zum Erstellen und Verwalten von [!DNL Microsoft Dynamics] und [!DNL Salesforce] Connectors. |
| Connector-Unterstützung für Cloud-basierte Datenspeicherung | Connectors können jetzt auf Cloud-basierte Datenspeicherung zugreifen. Zu den neuen Quellen gehören [!DNL Amazon S3]FTP- [!DNL Azure Blob]und SFTP-/SFTP-Server. |

**Bekannte Probleme**

* Quellschnittstellen für Cloud-basierte Datenspeicherung unterstützen nicht die Erfassung komprimierter Dateien.

Weiterführende Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] ermöglicht es Datenwissenschaftlern, Einblicke aus Daten und Inhalten in verschiedenen Adobe-Anwendungen und Drittanbietersystemen nahtlos zu generieren, indem sie maschinelle Lernmodelle erstellen und operationalisieren. [!DNL Data Science Workspace] ist eng in den End-to-End-Datenwissenschaftslebenszyklus integriert [!DNL Platform] [!DNL Real-time Customer Profile] und ermöglicht diese, einschließlich der Erforschung und Vorbereitung von XDM-Daten, gefolgt von der Entwicklung und Inbetriebnahme von Modellen, um automatisch mit Machine Learning Insights zu bereichern.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Datenzugriff mit [!DNL Platform] SDK | Vorgefertigte Rezepte und Starter-Notebooks verwenden [!DNL Python] jetzt [!DNL Platform] SDK für den Zugriff auf Daten. |
| Unterstützung für Sandboxen | Unterstützung für kommende Sandbox-Funktionen (aktuell in Beta), einschließlich der Möglichkeit, Notebooks und Rezepte in Entwicklungs- oder Produktionssandboxes zu isolieren. Weiterführende Informationen dazu finden Sie unter [Sandbox-Übersicht](../../sandboxes/home.md). |

For more information, see the [Data Science Workspace overview](../../data-science-workspace/home.md).

## [!DNL Experience Data Model] (XDM) System {#xdm}

Standardization and interoperability are key concepts behind [!DNL Experience Platform]. [!DNL Experience Data Model]Das von Adobe unterstützte  (XDM) ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| ---------- | ------------ |
| Benachrichtigungs-Schema | Neues Schema, das Benachrichtigungsdaten darstellt, die während des Datenerfassungsprozesses gesendet werden. |
| Adobe AdCloud DSP-Schema | Es wurden fünf neue Schemas zur Darstellung der DSP-Metadaten (Adobe Advertising Cloud Demside Platform) hinzugefügt: Platzierung, Kampagne, Paket, Advertiser, Konto. |
| ExperienceEvent-Implementierungsdetails-Mixin | Neues ExperienceEvent-Mixin, das ein Standardfeld zum Speichern von Informationen über die Software zum Erfassen des Ereignisses hinzufügt. |
| [!DNL Profile Privacy] mixin | Neue Profil-Mischung, die Felder hinzufügt, für die allgemeine Ausschluss- und Verkaufsabmeldesignale für [!DNL Real-time Customer Profile]die Freigabe akzeptiert werden können. |
| Formatbeschränkungen für `xdm:alternateDisplayInfo` | Die Felder &quot;Titel&quot;und &quot;Beschreibung&quot;für `xdm:alternateDisplayInfo` müssen beide Zeichenfolgen sein, um die Überprüfung zu bestehen. |
| Namensänderung: XDM [!DNL Individual Profile] | Der &quot;title&quot; der &quot;XDM [!DNL Profile]&quot;-Klasse wurde auf &quot;XDM [!DNL Individual Profile]&quot; aktualisiert. Die Form `$id` der Klasse hat sich nicht geändert. |

**Bekannte Probleme**

* Keine.

To learn more about working with XDM using the [!DNL Schema Registry] API and [!DNL Schema Editor] user interface, please read the [XDM System documentation](../../xdm/home.md).

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. With [!DNL Real-time Customer Profile], you can see a holistic view of each individual customer that combines data from multiple channels, including online, offline, CRM, and third party data. [!DNL Profile] ermöglicht es Ihnen, Ihre unterschiedlichen Kundendaten zu einer einheitlichen Ansicht zusammenzuführen, die Ihnen einen umsetzbaren Zeitstempel für jede Kundeninteraktion bietet.

| Funktion | Beschreibung |
| -----------| ---------- |
| Verbesserungen bei der [!DNL Profile] Suche | Benutzer haben jetzt die Möglichkeit, Profil mithilfe von Referenz-Deskriptoren und verwandten Entitäten nachzuschlagen. |
| Daten für einen bestimmten Datensatz bereinigen | Benutzer können jetzt Daten für einen bestimmten Datensatz oder Stapel mit der [!DNL Profile] System-Aufträge-API löschen. |
| Verbesserungen [!DNL Profile] an der Edge-Abfrage | Anwendungen können jetzt Edge [!DNL Profile] an einer beliebigen ID eines bestimmten Profils Abfrage werden. |
| Zusammenführungsrichtlinien pro Projektion konfigurieren | Anwendungen können jetzt Zusammenführungsrichtlinien pro Projektion konfigurieren, um eine Ansicht der Daten zu generieren, die von einer bestimmten Zusammenführungsrichtlinie bestimmt wird. |
| Berechnete Attribute | Berechnete Attribute berechnen den Feldwert automatisch anhand anderer Werte, Berechnungen und Ausdruck. Berechnete Attribute werden auf Profil-/Aggregat-Ebene verwendet, z. B. &quot;Gesamtkauf&quot;, &quot;Lebenszeitwert&quot;oder &quot;Trichterstatus&quot;, basierend auf einem eingehenden Ereignis, einem eingehenden Ereignis und einem eingehenden Profil oder einem eingehenden Ereignis, Profil-Daten und historischen Ereignissen. |

**Fehlerkorrekturen**

* Vereinfachte Liste der verfügbaren ID-Zuordnungsstrategien im Arbeitsablauf zur Erstellung von Zusammenführungsrichtlinien.

**Bekannte Probleme**

* Keine.

Weitere Informationen [!DNL Real-time Customer Profile]einschließlich Übungen und Best Practices für die Arbeit mit [!DNL Profile] Daten finden Sie in der Übersicht über das [Echtzeit-Profil](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] provides a user interface and RESTful API that allows you to build segments and generate audiences from your [!DNL Real-time Customer Profile] data. These segments are centrally configured and maintained on [!DNL Platform], making them readily accessible by any Adobe application.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

| Funktion | Beschreibung |
| -----------| ---------- |
| Geplante Segmentierung | Benutzer können nun die geplante Segmentauswertung für alle Segmente über die Benutzeroberfläche und die API aktivieren. Nach der Aktivierung werden alle Segmente einmal pro Tag ausgewertet. Dies wirkt sich nicht auf die Segmentierungsfunktionen auf Abruf aus, die weiterhin wie zuvor funktionieren.<br/><br/>Hinweis: Die Funktion für die geplante Segmentierung kann nicht in Sandboxen mit mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile]verwendet werden. |
| Streaming-Segmentierung | Die Unterstützung für die kontinuierliche Bewertung von Segmenten (Streaming-Segmentierung) ermöglicht die Bewertung der meisten Segmentregeln, während die Daten weitergegeben werden [!DNL Platform]. Diese Funktion bedeutet, dass die Segmentmitgliedschaft auf dem neuesten Stand ist, ohne dass geplante Segmentierungsaufträge ausgeführt werden müssen. Es gelten einige Ausnahmen, z. B. Segmente, die Beziehungen mit mehreren Entitäten oder erweiterte Nutzlasten verwenden. |
| Segmente als Bausteine | Beim Erstellen von Segmenten mithilfe der Benutzeroberfläche des Segmentaufbaus können Benutzer jetzt zuvor definierte Segmente als Bausteine für weitere Segmente verwenden. <ul><li>Referenz zur aktuellen Audience: aktualisiert, wenn Benutzer Audiencen ein- und aussteigen.</li><li>Logik kopieren: nimmt die ausgewählte Segmentdefinition und Duplikat sie im neuen Segment.</li></ul> |
| Ansicht der Segmentmitgliedschaft nach ID-Namensraum | Die Segmentmitgliedschaft kann nun nach ID-Namensraum (E-Mail, ECID und Gesamtanzahl) angezeigt werden. |
| RBAC-Unterstützung | Segmentaufbau unterstützt jetzt grundlegende rollenbasierte Zugriffskontrollen und Berechtigungen. |
| Verbesserte Unterstützung für die Freigabe externer Audiencen zwischen [!DNL Platform] und Adobe-Lösungen | Benutzer können nun externe Metadaten (nicht[!DNL Experience Platform]) der Audience in Szenarien einbringen, in denen die Anzahl der Audiencen a priori groß oder nicht bekannt ist. Diese Version enthält Zugriff auf [!DNL Audience Manager] Metadaten für Kunden, die den Lösungsanschluss bereitgestellt haben. Diese Segmentmetadaten können im Segmentaufbau zum Erstellen neuer [!DNL Experience Platform] Audiencen verwendet werden. <br/><br/> Darüber hinaus [!DNL Experience Platform] werden in erstellte Segmente jetzt für die Verwendung in integrierten Adobe-Lösungen einschließlich [!DNL Audience Manager], [!DNL Target]und [!DNL Ad Cloud]verfügbar sein. |

**Fehlerkorrekturen**

* Es wurde ein Fehler behoben, der dazu führte, dass bei der Segmentierung mehrerer Entitäten bei verschachtelten Beziehungen keine Profil zurückgegeben wurden.
* Es wurde ein Problem behoben, bei dem die Ausschlusslogik irreführende Ergebnisse zurückgab.
* Verbesserte Lesbarkeit von Ordnern mit mehreren Entitäten. Jetzt wird der Anzeigename der XDM-Klasse angezeigt.
* Es wurde ein zeitweiliger Fehler behoben, durch den mehrere Kopien desselben XDM-Ordners angezeigt wurden.
* Es werden nun Nachrichten erzeugt, die einen Benutzer darüber informieren, wenn Segmentschätzungen für die ausgewählte Zusammenführungsrichtlinie nicht verfügbar sind.

**Bekannte Probleme**

* Keine.

Weitere Informationen [!DNL Segmentation Service]finden Sie in der Übersicht über den [Segmentierungsdienst](../../segmentation/home.md).