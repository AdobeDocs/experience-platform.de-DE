---
title: Adobe Experience Platform  – Versionshinweise
description: Versionshinweise zur Experience Platform - 18. November 2019
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498
workflow-type: tm+mt
source-wordcount: '2019'
ht-degree: 19%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: 18. November 2019**

Neue Funktionen in Adobe Experience Platform:
* [Echtzeit-Kundendatenplattform](#rtcdp)
* [Ziele](#destinations)
* [Quellen](#sources)

Aktualisierungen vorhandener Funktionen:
* [Data Science-Arbeitsbereich](#dsw)
* [Erlebnis-Datenmodell (XDM)-System](#xdm)
* [Echtzeit-Kundenprofil](#profile)
* [Segmentierungsdienst](#segmentation)

## Echtzeit-Kundendatenplattform {#rtcdp}

Die auf der Adobe Experience Platform aufbauende Echtzeit-Kundendatenplattform (Echtzeit-CDP) von Adobe hilft Firmen, bekannte und unbekannte Daten zusammenzuführen, um Profil mit intelligenten Entscheidungen während der gesamten Customer Journey zu aktivieren. Die Echtzeit-Kundendatenplattform fasst unterschiedliche Unternehmensdatenquellen zusammen, um in Echtzeit einheitliche Profile zu erstellen, die über alle Kanäle und Geräte hinweg ein personalisiertes Kundenerlebnis möglich machen.

Die Echtzeit-Kundendatenplattform umfasst Tools für Data Governance, Identitäts-Management, erweiterte Segmentierung und Datenwissenschaft, sodass Sie Profile erstellen und Zielgruppen definieren, umfassende Einblicke gewinnen und gleichzeitig strikte Richtlinien zur Datenverwaltung durchsetzen können.

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
| Ziele | Vordefinierte Integrationen mit Zielplattformen, die von der Echtzeit-Kundendatenplattform von Adobe unterstützt werden und die Daten für diese Partner nahtlos aktivieren. See [Destinations](#destinations) below for more information. |
| Dashboard zu Startseiten-Metriken | Die Startseite zur Adobe Echtzeit-Kundendatenplattform (Echtzeit-CDP) enthält ein Dashboard mit Metriken, in dem Informationen zu Profilen und Segmenten angezeigt werden. Die Startseite enthält auch Links zu Lernmaterialien. Siehe den Abschnitt zu den Metriken [der](#real-time-customer-data-platform-metrics) Echtzeit-Kundendatenplattform. |
| Quellen | Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Lösungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System. Weitere Informationen finden Sie im Abschnitt [Quellen](#sources) . |

**Echtzeit-Metriken zur Kundendatenplattform**

Die Startseite der Echtzeit-Kundendatenplattform von Adobe, die ein Metriken-Dashboard enthält, wird angezeigt, sobald Sie sich bei der Echtzeit-Kundendatenplattform anmelden.

Die Startseite ist nur einer der Orte, an denen Metrikkarten angezeigt werden. Die Echtzeit-Kundendatenplattform stellt Metrikkarten während des gesamten Erlebnisses bereit. Diese Metriken informieren Sie über die Daten-, Profil- und Segmentzielgruppen im System.

Wenn zum Zeitpunkt der Anmeldung bei der Echtzeit-Kundendatenplattform keine Daten im System vorhanden sind, wird das Dashboard auf der Startseite nicht angezeigt. In dem Fall enthält die Startseite Lernmaterial für die erstmalige Nutzung. Bei der Datenerfassung wird das Dashboard automatisch aktualisiert, um Informationen zu diesen Daten anzuzeigen.

Weitere Informationen finden Sie in der Übersicht über die Metriken der [Echtzeit-Kundendatenplattform](../../rtcdp/home-page-dashboards.md)

## Ziele {#destinations}

Ziele sind vordefinierte Integrationen mit Zielplattformen, die von der Echtzeit-Kundendatenplattform von Adobe unterstützt werden und die Daten nahtlos für diese Partner aktivieren. Weitere Informationen finden Sie im Artikel [Ziele-Übersicht](../../rtcdp/destinations/destinations-overview.md) .

**Verfügbare Ziele**

Ab der November-Version unterstützt die Echtzeit-Kundendatenplattform von Adobe die folgenden Ziele:

* Werbung: Google
* E-Mail-Marketing: Adobe Campaign, Salesforce Marketing Cloud, Oracle-Antworten, Oracle Eloqua

Informationen zu den einzelnen Zielen finden Sie im [Zielkatalog](../../rtcdp/destinations/destinations-catalog.md) .

**Bekannte Einschränkungen**

* Das Steuerelement zum Zulassen von Zeitplänen für benutzerdefinierte Aktivierungen im [Aktivierungen-Fluss](../../rtcdp/destinations/activate-destinations.md#activate-data) (Planschritt) ist in der ersten Version nicht verfügbar.
* Es gibt derzeit keine Möglichkeit, eine Zielkonfiguration zu bearbeiten oder zu löschen. Um diese Einschränkung zu umgehen, können Sie das Ziel oben rechts auf der Seite mit den [Zieldetails aktivieren oder deaktivieren](../../rtcdp/destinations/destination-details-page.md).
* Es gibt derzeit keine Überprüfung für Kontodetails, Pfad oder Anmeldeinformationen, wenn eine Verbindung mit Ihrem Ziel- oder Datenspeicherung-Konto hergestellt wird. Vergewissern Sie sich, dass Sie die richtigen Anmeldeinformationen eingeben und die Dublette auf Rechtschreibfehler oder Tippfehler überprüfen.
* Mit der ersten Version wurden keine Anmeldeinformationen verlängert. Nachdem ein Konto abgelaufen ist oder aktualisiert werden muss, müssen Sie eine neue Zielverbindung erstellen und Ihre zuvor zugeordneten Segmente neu zuordnen.

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen, während Sie diese Daten mithilfe von Plattformdiensten strukturieren, beschriften und verbessern können. Sie können Daten aus verschiedenen Quellen erfassen, z. B. Adobe Solutions, Cloud-basierte Datenspeicherung, Drittanbieter-Software und Ihr CRM-System.

Experience Platform bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie Quellverbindungen für verschiedene Datenanbieter einfach einrichten können. Mit diesen Quellverbindungen können Sie sich bei Ihren Datenspeicherung- und CRM-Diensten authentifizieren, die Erfassungsdauer festlegen und den Datendurchsatz verwalten.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ---------- | ------------ |
| Quellbenutzeroberfläche | Neue Benutzeroberfläche zum Erstellen, Anzeigen und Verwalten von Quellverbindungen. |
| Überarbeitete Workflows für CRM-Connectors | Neuer intuitiver Arbeitsablauf für die Benutzeroberfläche zum Erstellen und Verwalten von Microsoft Dynamics und Salesforce Connectors. |
| Connector-Unterstützung für Cloud-basierte Datenspeicherung | Connectors können jetzt auf Cloud-basierte Datenspeicherung zugreifen. Zu den neuen Quellen zählen Amazon S3, Azurblase und FTP/SFTP-Server. |

**Bekannte Probleme**

* Quellschnittstellen für Cloud-basierte Datenspeicherung unterstützen nicht die Erfassung komprimierter Dateien.

Weiterführende Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md).

## Data Science-Arbeitsbereich {#dsw}

Mit dem Data Science Workspace der Adobe Experience Platform können Datenwissenschaftler Einblicke aus Daten und Inhalten in Adobe-Anwendungen und Drittanbietersystemen nahtlos erstellen, indem sie maschinelle Lernmodelle erstellen und operationalisieren. Data Science Workspace ist eng mit der Plattform integriert und ermöglicht den End-to-End-Data Science-Lebenszyklus, einschließlich der Erforschung und Vorbereitung von XDM-Daten, gefolgt von der Entwicklung und Inbetriebnahme von Modellen, um das Echtzeit-Profil von Kunden automatisch mit Machine Learning Insights zu bereichern.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Datenzugriff mit Platform SDK | Vorgefertigte Rezepte und Starter-Notebooks in Python verwenden jetzt Platform SDK für den Zugriff auf Daten. |
| Unterstützung für Sandboxen | Unterstützung für kommende Sandbox-Funktionen (aktuell in Beta), einschließlich der Möglichkeit, Notebooks und Rezepte in Entwicklungs- oder Produktionssandboxes zu isolieren. See the [sandboxes overview](../../sandboxes/home.md) for more information. |

Weitere Informationen finden Sie in der Übersicht über den Arbeitsbereich für [Datenwissenschaften](../../data-science-workspace/home.md).

## Erlebnis-Datenmodell (XDM)-System {#xdm}

Standardisierung und Interoperabilität sind Schlüsselkonzepte der Experience Platform. Das von Adobe unterstützte Experience Data Model (XDM) ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schema für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten auf der Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Audiencen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| ---------- | ------------ |
| Benachrichtigungs-Schema | Neues Schema, das Benachrichtigungsdaten darstellt, die während des Datenerfassungsprozesses gesendet werden. |
| Adobe AdCloud DSP-Schema | Zur Darstellung der DSP-Metadaten (Adobe Advertising Cloud-Nachfrageseite Platform) wurden fünf neue Schema hinzugefügt: Platzierung, Kampagne, Paket, Advertiser, Konto. |
| ExperienceEvent-Implementierungsdetails-Mixin | Neues ExperienceEvent-Mixin, das ein Standardfeld zum Speichern von Informationen über die Software zum Erfassen des Ereignisses hinzufügt. |
| Profil Privacy mixin | Neue Profil-Mischung, die Felder zur Akzeptanz allgemeiner Ausschluss- und Vertriebs-/Freigabe-Abmeldesignale für Echtzeit-Kundendaten hinzufügt. |
| Formatbeschränkungen für `xdm:alternateDisplayInfo` | Die Felder &quot;Titel&quot;und &quot;Beschreibung&quot;für `xdm:alternateDisplayInfo` müssen beide Zeichenfolgen sein, um die Überprüfung zu bestehen. |
| Namensänderung: XDM Individuelles Profil | Der &quot;title&quot; der Klasse &quot;XDM Profil&quot; wurde auf &quot;XDM Individuelles Profil&quot; aktualisiert. Die Form `$id` der Klasse hat sich nicht geändert. |

**Bekannte Probleme**

* Keine.

Weitere Informationen zum Arbeiten mit XDM mithilfe der Schema Registry API und Schema Editor Benutzeroberfläche finden Sie in der [XDM-Systemdokumentation](../../xdm/home.md).

## Echtzeit-Kundenprofil {#profile}

Mit der Adobe Experience Platform können Sie koordinierte, konsistente und relevante Erlebnisse für Ihre Kunden bereitstellen, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Mit Echtzeit-Kundendaten können Sie eine ganzheitliche Ansicht jedes einzelnen Profils anzeigen, die Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieterdaten, kombiniert. Mit dem Profil können Sie Ihre unterschiedlichen Kundendaten in einer einheitlichen Sicht zusammenfassen, die ein umsetzbares Konto mit Zeitstempel für jede Kundeninteraktion bietet.

| Funktion | Beschreibung |
| -----------| ---------- |
| Verbesserungen bei der Profil-Suche | Benutzer haben jetzt die Möglichkeit, Profil mithilfe von Referenz-Deskriptoren und verwandten Entitäten nachzuschlagen. |
| Daten für einen bestimmten Datensatz bereinigen | Benutzer können jetzt Daten für einen bestimmten Datensatz oder Stapel mit der Profil-Systemauftrags-API löschen. |
| Verbesserungen an der Abfrage von Edge Profil | Anwendungen können jetzt Edge Profil an einer beliebigen ID eines bestimmten Profils Abfrage werden. |
| Zusammenführungsrichtlinien pro Projektion konfigurieren | Anwendungen können jetzt Zusammenführungsrichtlinien pro Projektion konfigurieren, um eine Ansicht der Daten zu generieren, die von einer bestimmten Zusammenführungsrichtlinie bestimmt wird. |
| Berechnete Attribute | Berechnete Attribute berechnen den Feldwert automatisch anhand anderer Werte, Berechnungen und Ausdruck. Berechnete Attribute werden auf Profil-/Aggregat-Ebene verwendet, z. B. &quot;Gesamtkauf&quot;, &quot;Lebenszeitwert&quot;oder &quot;Trichterstatus&quot;, basierend auf einem eingehenden Ereignis, einem eingehenden Ereignis und einem eingehenden Profil oder einem eingehenden Ereignis, Profil-Daten und historischen Ereignissen. |

**Fehlerkorrekturen**

* Vereinfachte Liste der verfügbaren ID-Zuordnungsstrategien im Arbeitsablauf zur Erstellung von Zusammenführungsrichtlinien.

**Bekannte Probleme**

* Keine.

Weitere Informationen zum Echtzeit-Profil von Kunden, einschließlich Übungen und Best Practices für die Arbeit mit Profil-Daten, finden Sie in der Übersicht über das [Echtzeit-Profil](../../profile/home.md).

## Segmentierungsdienst {#segmentation}

Der Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und Audiencen aus Ihren Echtzeit-Daten zum Profil von Kunden generieren können. Diese Segmente werden zentral auf der Plattform konfiguriert und gepflegt, sodass sie von jeder Adobe-Anwendung leicht zugänglich sind.

Der Segmentierungsdienst definiert eine bestimmte Untergruppe von Profilen, indem er die Kriterien beschreibt, die eine vermarktbare Personengruppe innerhalb Ihrer Kundenbasis unterscheiden. Segmente können auf Datensatzdaten (z. B. demografische Informationen) oder Zeitreihen-Ereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

| Funktion | Beschreibung |
| -----------| ---------- |
| Geplante Segmentierung | Benutzer können nun die geplante Segmentauswertung für alle Segmente über die Benutzeroberfläche und die API aktivieren. Nach der Aktivierung werden alle Segmente einmal pro Tag ausgewertet. Dies wirkt sich nicht auf die Segmentierungsfunktionen auf Abruf aus, die weiterhin wie zuvor funktionieren.<br/><br/>Hinweis: Die Funktion für die geplante Segmentierung kann nicht in Sandboxen mit mehr als fünf Zusammenführungsrichtlinien für das individuelle XDM-Profil verwendet werden. |
| Streaming-Segmentierung | Die Unterstützung für die kontinuierliche Bewertung von Segmenten (Streaming-Segmentierung) ermöglicht die Bewertung der meisten Segmentregeln, während die Daten an die Plattform weitergeleitet werden. Diese Funktion bedeutet, dass die Segmentmitgliedschaft auf dem neuesten Stand ist, ohne dass geplante Segmentierungsaufträge ausgeführt werden müssen. Es gelten einige Ausnahmen, z. B. Segmente, die Beziehungen mit mehreren Entitäten oder erweiterte Nutzlasten verwenden. |
| Segmente als Bausteine | Beim Erstellen von Segmenten mithilfe der Benutzeroberfläche des Segmentaufbaus können Benutzer jetzt zuvor definierte Segmente als Bausteine für weitere Segmente verwenden. <ul><li>Referenz zur aktuellen Audience: aktualisiert, wenn Benutzer Audiencen ein- und aussteigen.</li><li>Logik kopieren: nimmt die ausgewählte Segmentdefinition und Duplikat sie im neuen Segment.</li></ul> |
| Ansicht der Segmentmitgliedschaft nach ID-Namensraum | Die Segmentmitgliedschaft kann nun nach ID-Namensraum (E-Mail, ECID und Gesamtanzahl) angezeigt werden. |
| RBAC-Unterstützung | Segmentaufbau unterstützt jetzt grundlegende rollenbasierte Zugriffskontrollen und Berechtigungen. |
| Erweiterte Unterstützung für die Freigabe externer Audiencen zwischen Plattform- und Adobe-Lösungen | Benutzer können jetzt externe Metadaten (ohne Plattform) für Audiencen in Szenarien einbringen, in denen die Anzahl der Audiencen a priori groß oder nicht bekannt ist. Diese Version enthält Zugriff auf Audience Manager-Metadaten für Kunden, die den Lösungsanschluss bereitgestellt haben. Diese Audience-Metadaten können im Segmentaufbau verwendet werden, um neue Erlebnisplattformsegmente zu erstellen. <br/><br/> Darüber hinaus stehen in Experience Platform erstellte Segmente jetzt zur Verwendung in integrierten Adobe-Lösungen zur Verfügung, einschließlich Audience Manager, Zielgruppe und Ad Cloud. |

**Fehlerkorrekturen**

* Es wurde ein Fehler behoben, der dazu führte, dass bei der Segmentierung mehrerer Entitäten bei verschachtelten Beziehungen keine Profil zurückgegeben wurden.
* Es wurde ein Problem behoben, bei dem die Ausschlusslogik irreführende Ergebnisse zurückgab.
* Verbesserte Lesbarkeit von Ordnern mit mehreren Entitäten. Jetzt wird der Anzeigename der XDM-Klasse angezeigt.
* Es wurde ein zeitweiliger Fehler behoben, durch den mehrere Kopien desselben XDM-Ordners angezeigt wurden.
* Es werden nun Nachrichten erzeugt, die einen Benutzer darüber informieren, wenn Segmentschätzungen für die ausgewählte Zusammenführungsrichtlinie nicht verfügbar sind.

**Bekannte Probleme**

* Keine.

Weitere Informationen zum Segmentierungsdienst finden Sie in der Übersicht über den [Segmentierungsdienst](../../segmentation/home.md).