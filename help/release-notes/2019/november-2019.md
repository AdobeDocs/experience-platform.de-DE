---
title: Versionshinweise zu Adobe Experience Platform
description: Versionshinweise zur Experience Platform, 18. November 2019
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 29%

---

# Versionshinweise zu Adobe Experience Platform

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

Die auf Adobe Experience Platform aufbauende Echtzeit-Kundendatenplattform (Echtzeit-CDP) hilft Firmen, bekannte und unbekannte Daten zusammenzuführen, um Kundendaten mit intelligenter Entscheidungsfindung über die gesamte Journey zu aktivieren. Die Echtzeit-Kundendatenplattform fasst unterschiedliche Unternehmensdatenquellen zusammen, um in Echtzeit einheitliche Profile zu erstellen, die über alle Kanäle und Geräte hinweg ein personalisiertes Kundenerlebnis möglich machen.

[!DNL Real-time Customer Data Platform] umfasst Tools für die Datenverwaltung, Identitätsverwaltung, erweiterte Segmentierung und Datenwissenschaften, damit Sie Profil erstellen und Audiencen definieren sowie umfassende Einblicke gewinnen können, während Sie strikte Datenverwaltungs-Richtlinien durchsetzen können.

Adobe bietet Verbindungen zu einem großen Partnernetzwerk sowie native Integrationen mit Adobe Experience Cloud, damit Sie Zielgruppen nahtlos aktivieren und über alle Kanäle hinweg für herausragende Kundenerlebnisse sorgen können – von der Personalisierung vor Ort oder in Apps über E-Mail bis hin zu Paid Media, Callcentern, vernetzten Geräten und mehr.

Mit der Echtzeit-Kundendatenplattform profitieren Sie von folgenden Vorteilen:

* Verschaffen Sie sich einen Überblick über Ihre Kunden mit einer Streaming-Sammlung von Kundendaten aus dem gesamten Unternehmen.
* Sorgen Sie für eine angemessene Verwaltung von Profilen mit vertrauenswürdigen Governance- und Datenschutzkontrollen für bekannte und unbekannte Kennungen.
* Erstellen Sie mit KI und maschinellem Lernen auf Basis von Adobe Sensei – entwickelt für Marketer – praktische Einblicke und skalieren Sie Zielgruppen.
* Schaffen Sie in Echtzeit personalisierte Erlebnisse über alle Kanäle und Ziele hinweg.

Weitere Informationen finden Sie in der Dokumentation [Kundendatenplattform in Echtzeit](../../rtcdp/overview.md).

**Wichtigste Funktionen**

| Funktion | Beschreibung |
|---|---|
| Ziele | Vorgefertigte Integrationen mit Zielplattformen, die von der Adobe [!DNL Real-time Customer Data Platform] unterstützt werden und die Daten nahtlos für diese Partner aktivieren. Weitere Informationen finden Sie unter [Ziele](#destinations) weiter unten. |
| Dashboard zu Startseiten-Metriken | Die Startseite zur Echtzeit- der Kundendatenplattform (Echtzeit-CDP) enthält ein Dashboard mit Metriken, in dem Informationen zu Profilen und Segmenten angezeigt werden. Die Startseite enthält auch Links zu Lernmaterialien. Siehe den Abschnitt [Metriken der Kundendatenplattform in Echtzeit](#real-time-customer-data-platform-metrics) weiter unten. |
| Quellen | Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Lösungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System. Weitere Informationen finden Sie im Abschnitt [Quellen](#sources). |

**[!DNL Real-time Customer Data Platform]Metriken**

Die Startseite der Echtzeit-Kundendatenplattform von , die ein Metriken-Dashboard enthält, wird angezeigt, sobald Sie sich bei der Echtzeit-Kundendatenplattform anmelden.

Die Startseite ist nur einer der Orte, an denen Metrikkarten angezeigt werden. Die Echtzeit-Kundendatenplattform stellt Metrikkarten während des gesamten Erlebnisses bereit. Diese Metriken informieren Sie über die Daten-, Profil- und Segmentzielgruppen im System.

Wenn zum Zeitpunkt der Anmeldung bei der Echtzeit-Kundendatenplattform keine Daten im System vorhanden sind, wird das Dashboard auf der Startseite nicht angezeigt. In dem Fall enthält die Startseite Lernmaterial für die erstmalige Nutzung. Bei der Datenerfassung wird das Dashboard automatisch aktualisiert, um Informationen zu diesen Daten anzuzeigen.

Weitere Informationen finden Sie unter [Übersicht über die Metriken der Kundendatenplattform in Echtzeit](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorgefertigte Integrationen mit Zielplattformen, die von der Echtzeit-Kundendatenplattform der Adobe unterstützt werden und die Daten nahtlos für diese Partner aktivieren. Weitere Informationen finden Sie im Artikel [Ziele - Übersicht](../../destinations/home.md).

**Verfügbare Ziele**

Ab der November-Version unterstützt die Echtzeit-Kundendatenplattform der Adobe die folgenden Ziele:

* Werbung: [!DNL Google]
* E-Mail-Marketing: Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

Informationen zu den einzelnen Zielen finden Sie im [Zielkatalog](../../destinations/catalog/overview.md).

**Bekannte Einschränkungen**

* Das Steuerelement zum Zulassen von Zeitplänen für benutzerdefinierte Aktivierungen im [Aktivierung-Fluss](../../destinations/ui/activate-destinations.md#activate-data) (Planschritt) ist mit der ersten Version nicht verfügbar.
* Es gibt derzeit keine Möglichkeit, eine Zielkonfiguration zu bearbeiten oder zu löschen. Um diese Einschränkung zu umgehen, können Sie das Ziel in der oberen rechten Ecke der [Seite mit den Zieldetails](../../destinations/ui/destination-details-page.md) aktivieren oder deaktivieren.
* Es gibt derzeit keine Überprüfung für Kontodetails, Pfad oder Anmeldeinformationen, wenn eine Verbindung mit Ihrem Ziel- oder Datenspeicherung-Konto hergestellt wird. Vergewissern Sie sich, dass Sie die richtigen Anmeldeinformationen eingeben und die Dublette auf Rechtschreibfehler oder Tippfehler überprüfen.
* Mit der ersten Version wurden keine Anmeldeinformationen verlängert. Nachdem ein Konto abgelaufen ist oder aktualisiert werden muss, müssen Sie eine neue Zielverbindung erstellen und Ihre zuvor zugeordneten Segmente neu zuordnen.

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen, während Sie diese Daten mithilfe der [!DNL Platform]-Dienste strukturieren, beschriften und erweitern können. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Lösungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Diese Quellverbindungen ermöglichen Ihnen eine Authentifizierung mit Ihren Datenspeichern und CRM-Diensten, die Festlegung von Zeiten für Erfassungsläufe und die Verwaltung des Durchsatzes bei der Datenerfassung.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ---------- | ------------ |
| Quellbenutzeroberfläche | Neue Benutzeroberfläche zum Erstellen, Anzeigen und Verwalten von Quellverbindungen. |
| Überarbeitete Workflows für CRM-Connectors | Neuer intuitiver Arbeitsablauf für die Benutzeroberfläche zum Erstellen und Verwalten von [!DNL Microsoft Dynamics]- und [!DNL Salesforce]-Connectors. |
| Connector-Unterstützung für Cloud-basierte Datenspeicherung | Connectors können jetzt auf Cloud-basierte Datenspeicherung zugreifen. Zu den neuen Quellen zählen [!DNL Amazon S3], [!DNL Azure Blob] und FTP/SFTP-Server. |

**Bekannte Probleme**

* Quellschnittstellen für Cloud-basierte Datenspeicherung unterstützen nicht die Erfassung komprimierter Dateien.

Weiterführende Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Mit Adobe Experience Platform [!DNL Data Science Workspace] können Datenwissenschaftler Einblicke aus Daten und Inhalten nahtlos in Adoben- und Drittanbietersysteme generieren, indem sie maschinelle Lernmodelle erstellen und operationalisieren. [!DNL Data Science Workspace] ist eng in den End-to-End-Datenwissenschaftslebenszyklus integriert  [!DNL Platform] und ermöglicht diese, einschließlich der Erforschung und Vorbereitung von XDM-Daten, gefolgt von der Entwicklung und Operationalisierung von Modellen, um automatisch  [!DNL Real-time Customer Profile] mit Machine Learning Insights zu bereichern.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Datenzugriff mit dem SDK [!DNL Platform] | Vorgefertigte Rezepte und Starter-Notebooks in [!DNL Python] verwenden jetzt das [!DNL Platform]-SDK für den Zugriff auf Daten. |
| Unterstützung für Sandboxen | Unterstützung für kommende Sandbox-Funktionen (aktuell in Beta), einschließlich der Möglichkeit, Notebooks und Rezepte in Entwicklungs- oder Produktionssandboxes zu isolieren. Weiterführende Informationen dazu finden Sie unter [Sandbox-Übersicht](../../sandboxes/home.md). |

Weitere Informationen finden Sie unter [Übersicht über den Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Experience Data Model] (XDM) System  {#xdm}

Normung und Interoperabilität sind Schlüsselkonzepte hinter [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), angetrieben von der Adobe, ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schema für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| ---------- | ------------ |
| Benachrichtigungs-Schema | Neues Schema, das Benachrichtigungsdaten darstellt, die während des Datenerfassungsprozesses gesendet werden. |
| Adobe AdCloud DSP Schema | Es wurden fünf neue Schemas zur Darstellung der Adobe Advertising Cloud-DSP-Metadaten hinzugefügt: Platzierung, Kampagne, Paket, Advertiser, Konto. |
| ExperienceEvent-Implementierungsdetails - Schema-Feldgruppen | Neue ExperienceEvent-Feldgruppen, die ein Standardfeld hinzufügen, um Informationen über die Software zu speichern, mit der das Ereignis erfasst wird. |
| [!DNL Profile Privacy] Feldgruppen | Neue Feldgruppen für Profile, die Felder hinzufügen, um allgemeine Ausschluss- und Abmeldesignale für [!DNL Real-time Customer Profile] zu akzeptieren. |
| Formatbeschränkungen für `xdm:alternateDisplayInfo` | Die Felder &quot;Titel&quot;und &quot;Beschreibung&quot;für `xdm:alternateDisplayInfo` müssen beide Zeichenfolgen sein, um die Überprüfung zu bestehen. |
| Namensänderung: XDM [!DNL Individual Profile] | Der &quot;Titel&quot;der Klasse &quot;XDM [!DNL Profile]&quot;wurde auf &quot;XDM [!DNL Individual Profile]&quot;aktualisiert. Das formale `$id` der Klasse wurde nicht geändert. |

**Bekannte Probleme**

* Keine.

Weitere Informationen zum Arbeiten mit XDM mit der [!DNL Schema Registry]-API und [!DNL Schema Editor]-Benutzeroberfläche finden Sie in der [XDM-Systemdokumentation](../../xdm/home.md).

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. Mit [!DNL Real-time Customer Profile] können Sie eine ganzheitliche Ansicht jedes einzelnen Kunden sehen, die Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieterdaten, kombiniert. [!DNL Profile] ermöglicht es Ihnen, Ihre unterschiedlichen Kundendaten zu einer einheitlichen Ansicht zusammenzuführen, die Ihnen einen umsetzbaren Zeitstempel für jede Kundeninteraktion bietet.

| Funktion | Beschreibung |
| -----------| ---------- |
| Verbesserungen bei der [!DNL Profile]-Suche | Benutzer haben jetzt die Möglichkeit, Profil mithilfe von Referenz-Deskriptoren und verwandten Entitäten nachzuschlagen. |
| Daten für einen bestimmten Datensatz bereinigen | Benutzer können jetzt Daten für einen bestimmten Datensatz oder Stapel mit der API für Systemaufträge löschen.[!DNL Profile] |
| Edge [!DNL Profile] - Abfrage-Verbesserungen | Anwendungen können jetzt Edge [!DNL Profile] durch eine beliebige ID eines bestimmten Profils Abfrage werden. |
| Zusammenführungsrichtlinien pro Projektion konfigurieren | Anwendungen können jetzt Zusammenführungsrichtlinien pro Projektion konfigurieren, um eine Ansicht der Daten zu generieren, die von einer bestimmten Zusammenführungsrichtlinie bestimmt wird. |
| Berechnete Attribute | Berechnete Attribute berechnen den Feldwert automatisch anhand anderer Werte, Berechnungen und Ausdruck. Berechnete Attribute werden auf Profil-/Aggregat-Ebene verwendet, z. B. &quot;Gesamtkauf&quot;, &quot;Lebenszeitwert&quot;oder &quot;Trichterstatus&quot;, basierend auf einem eingehenden Ereignis, einem eingehenden Ereignis und einem eingehenden Profil oder einem eingehenden Ereignis, Profil-Daten und historischen Ereignissen. |

**Fehlerkorrekturen**

* Vereinfachte Liste der verfügbaren ID-Zuordnungsstrategien im Arbeitsablauf zur Erstellung von Zusammenführungsrichtlinien.

**Bekannte Probleme**

* Keine.

Weitere Informationen zu [!DNL Real-time Customer Profile], einschließlich Übungen und Best Practices für die Arbeit mit [!DNL Profile]-Daten, finden Sie unter [Übersicht über das Echtzeit-Profil von Kunden](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und Audiencen aus Ihren [!DNL Real-time Customer Profile]-Daten generieren können. Diese Adoben werden zentral auf [!DNL Platform] konfiguriert und gepflegt, sodass sie für jede Anwendung leicht zugänglich sind.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

| Funktion | Beschreibung |
| -----------| ---------- |
| Geplante Segmentierung | Benutzer können nun die geplante Segmentauswertung für alle Segmente über die Benutzeroberfläche und die API aktivieren. Nach der Aktivierung werden alle Segmente einmal pro Tag ausgewertet. Dies wirkt sich nicht auf die Segmentierungsfunktionen auf Abruf aus, die weiterhin wie zuvor funktionieren.<br/><br/>Hinweis: Die Funktion für die geplante Segmentierung kann nicht in Sandboxen mit mehr als fünf Zusammenführungsrichtlinien für  [!DNL XDM Individual Profile]verwendet werden. |
| Streaming-Segmentierung | Die Unterstützung für die kontinuierliche Bewertung von Segmenten (Streaming-Segmentierung) ermöglicht die Bewertung der meisten Segmentregeln, während die Daten an [!DNL Platform] weitergeleitet werden. Diese Funktion bedeutet, dass die Segmentmitgliedschaft auf dem neuesten Stand ist, ohne dass geplante Segmentierungsaufträge ausgeführt werden müssen. Es gelten einige Ausnahmen, z. B. Segmente, die Beziehungen mit mehreren Entitäten oder erweiterte Nutzlasten verwenden. |
| Segmente als Bausteine | Beim Erstellen von Segmenten mithilfe der Benutzeroberfläche des Segmentaufbaus können Benutzer jetzt zuvor definierte Segmente als Bausteine für weitere Segmente verwenden. <ul><li>Referenz zur aktuellen Audience: aktualisiert, wenn Benutzer Audiencen ein- und aussteigen.</li><li>Logik kopieren: nimmt die ausgewählte Segmentdefinition und Duplikat sie im neuen Segment.</li></ul> |
| Ansicht der Segmentmitgliedschaft nach ID-Namensraum | Die Segmentmitgliedschaft kann nun nach ID-Namensraum (E-Mail, ECID und Gesamtanzahl) angezeigt werden. |
| RBAC-Unterstützung | Segmentaufbau unterstützt jetzt grundlegende rollenbasierte Zugriffskontrollen und Berechtigungen. |
| Erweiterte Unterstützung für die Freigabe externer Audiencen zwischen [!DNL Platform]- und Adobe-Lösungen | Benutzer können nun externe Metadaten (nicht-[!DNL Experience Platform]) für Audiencen in Szenarien einbringen, in denen die Anzahl der Audiencen groß oder nicht von vornherein bekannt ist. Diese Version enthält Zugriff auf [!DNL Audience Manager]-Metadaten für Kunden, die den Lösungsanschluss bereitgestellt haben. Diese Metadaten der Audience können im Segmentaufbau verwendet werden, um neue [!DNL Experience Platform]-Segmente zu erstellen. <br/><br/> Darüber hinaus  [!DNL Experience Platform] werden in erstellte Adoben jetzt auch in integrierten Lösungen wie  [!DNL Audience Manager],  [!DNL Target]und  [!DNL Ad Cloud]zur Verfügung stehen. |

**Fehlerkorrekturen**

* Es wurde ein Fehler behoben, der dazu führte, dass bei der Segmentierung mehrerer Entitäten bei verschachtelten Beziehungen keine Profil zurückgegeben wurden.
* Es wurde ein Problem behoben, bei dem die Ausschlusslogik irreführende Ergebnisse zurückgab.
* Verbesserte Lesbarkeit von Ordnern mit mehreren Entitäten. Jetzt wird der Anzeigename der XDM-Klasse angezeigt.
* Es wurde ein zeitweiliger Fehler behoben, durch den mehrere Kopien desselben XDM-Ordners angezeigt wurden.
* Es werden nun Nachrichten erzeugt, die einen Benutzer darüber informieren, wenn Segmentschätzungen für die ausgewählte Zusammenführungsrichtlinie nicht verfügbar sind.

**Bekannte Probleme**

* Keine.

Weitere Informationen zu [!DNL Segmentation Service] erhalten Sie im Abschnitt [Übersicht über den Segmentdienst](../../segmentation/home.md).
