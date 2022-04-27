---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: e9e4e58de454abb1fc66e07d5ad4ce18398c6a44
workflow-type: tm+mt
source-wordcount: '2378'
ht-degree: 26%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 27. April 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Dashboards]](#dashboards)
- [Datenflüsse](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [Real-time Customer Data Platform B2B Edition](#B2B)
- [Quellen](#sources)

## [!DNL Dashboards] {#dashboards}

Platform bietet mehrere Dashboards, in denen Sie wichtige Informationen zu den Daten Ihres Unternehmens sehen, basierend auf täglichen Schnappschüssen der Daten.

Dashboards bieten vorkonfigurierte Berichtsoptionen für die Daten Ihres Unternehmens und sind direkt in den Marketing-Workflow in Platform integriert. Diese Dashboards können ohne zusätzliche IT-Unterstützung genutzt werden, und es fällt hierbei auch nicht der Zeit- und Arbeitsaufwand an, der andernfalls für den Export und die Verarbeitung von Daten mit Data Warehouse-Design und -Implementierung als Zusatz erforderlich wäre.

Die folgenden Widgets sind über die Widget-Bibliothek in den jeweiligen Dashboards verfügbar. Weitere Informationen finden Sie in der Dokumentation zu [Hinzufügen von Widgets über die Widget-Bibliothek](../../dashboards/customize/widget-library.md).

| Funktion | Dashboard | Beschreibung |
| --------------------------------------------------------- | ------------- | ----------- |
| [!UICONTROL Hinzugefügte Trends bei Profilen] | Profile | Dieses Widget verwendet ein Liniendiagramm, um die Gesamtanzahl der zusammengeführten Profile zu veranschaulichen, die in den letzten 30 Tagen, 90 Tagen oder 12 Monaten täglich zum Profilspeicher hinzugefügt wurden. |
| [!UICONTROL Zielgruppen, die dem Zielstatus zugeordnet sind] | Profile | Dieses Widget zeigt die Gesamtzahl der zugeordneten und nicht zugeordneten Zielgruppen in einer einzelnen Metrik an und verwendet ein doppeltes Diagramm, um den proportionalen Unterschied zwischen den Summen zu veranschaulichen. |
| [!UICONTROL Zielgruppengröße] | Profile | Dieses Widget bietet eine zweispaltige Tabelle, die bis zu 20 Segmente und die Gesamtzahl der in den einzelnen Segmenten enthaltenen Zielgruppen auflistet. Die Liste hängt von der angewendeten und von oben nach unten sortierten Zusammenführungsrichtlinie ab, die der Gesamtzahl der Zielgruppen entspricht. |
| [!UICONTROL Trend zur Profilanzahl] | Profile | Dieses Widget verwendet ein Liniendiagramm, um den Trend der Gesamtanzahl der im System enthaltenen Profile im Zeitverlauf zu veranschaulichen. Die Daten können über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. |
| [!UICONTROL Einzelne Identitätsprofile nach Identität] | Profile | Dieses Widget verwendet ein Balkendiagramm, um die Gesamtanzahl der Profile zu veranschaulichen, die mit nur einer eindeutigen Kennung identifiziert werden. Das Widget unterstützt bis zu fünf der am häufigsten auftretenden Identitäten. |
| [!UICONTROL Zielstatus] | Ziele | Dieses Widget zeigt die Gesamtzahl der aktivierten Ziele als einzelne Metrik an und verwendet ein doppeltes Diagramm, um den proportionalen Unterschied zwischen aktivierten und deaktivierten Zielen zu veranschaulichen. |
| [!UICONTROL Aktive Ziele nach Zielplattform] | Ziele | Dieses Widget verwendet eine zweispaltige Tabelle, um eine Liste der aktiven Zielplattformen und die Gesamtzahl der aktiven Ziele für jede Zielplattform anzuzeigen. |
| [!UICONTROL Aktivierte Zielgruppen für alle Ziele] | Ziele | Dieses Widget stellt die Gesamtanzahl der Zielgruppen bereit, die für alle Ziele in einer einzelnen Metrik aktiviert sind. |
| [!UICONTROL Aktivierungsreihenfolge für Zielgruppen] | Segmente | Dieses Widget bietet eine dreiseitige Tabelle, in der der Zielname, die Plattform und das Aktivierungsdatum der Zielgruppe aufgelistet sind. |
| [!UICONTROL Zielgruppengrößentrend] | Segmente | Dieses Widget bietet eine grafische Darstellung der Gesamtanzahl der Profile, die die Kriterien einer Segmentdefinition über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten erfüllen. |
| [!UICONTROL Trend zur Änderung der Zielgruppengröße] | Segmente | Dieses Widget bietet eine Liniendiagramm, die die Differenz in der Gesamtzahl der Profile anzeigt, die sich für ein bestimmtes Segment zwischen den letzten täglichen Momentaufnahmen qualifiziert haben. Der Zeitraum der Trendanalyse kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. |
| [!UICONTROL Trend zur Zielgruppengröße nach Identität] | Segmente | Dieses Widget veranschaulicht den Trend zur Zielgruppengröße für ein bestimmtes Segment basierend auf einem ausgewählten Identitätstyp. Der Zeitraum der Trendanalyse kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. |

Weitere Informationen finden Sie in der Dokumentation zu [[!DNL Profiles]](../../dashboards/guides/profiles.md), [[!DNL Destinations]](../../dashboards/guides/destinations.md)und [[!DNL Segments]](../../dashboards/guides/segments.md) Dashboards.

## Datenflüsse {#dataflows}

In Platform werden Daten aus vielen verschiedenen Quellen erfasst, innerhalb des Systems analysiert und für eine Vielzahl von Zielen aktiviert. Plattform erleichtert das Tracking dieses potenziell nicht-linearen Datenflusses durch Transparenz.

Datenflüsse sind eine Darstellung von Aufträgen, die Daten innerhalb von Platform bewegen. Diese Datenflüsse werden über verschiedene Services konfiguriert, wodurch Daten von den Quell-Connectoren in Zieldatensätze verschoben werden können. Dort werden sie von Identity Service und vom Echtzeit-Kundenprofil verwendet, bevor sie schließlich für Ziele aktiviert werden.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Segmente-Dashboard | Sie können jetzt das Monitoring-Dashboard verwenden, um Datenflüsse auf Segmente zu überwachen. Weitere Informationen finden Sie im Handbuch unter [Überwachen von Segmenten in der Benutzeroberfläche](../../dataflows/ui/monitor-segments.md) |

Weitere allgemeine Informationen zu Datenflüssen finden Sie in der [Übersicht zu Datenflüssen](../../dataflows/home.md). Weitere Informationen zur Segmentierung finden Sie im Abschnitt [Segmentierungsübersicht](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für Adobe Analytics-Quelle | Die Adobe Analytics-Quelle unterstützt jetzt Data Prep-Funktionen, mit denen Sie Ihre Analytics Report Suite-Daten beim Erstellen eines Datenflusses einem Ziel-XDM-Schema zuordnen können. Siehe Tutorial zu [Erstellen einer Analytics-Quellverbindung](../../sources/tutorials/ui/create/adobe-applications/analytics.md) für weitere Informationen. |
| Unterstützung für den Import vorhandener Zuordnungsregeln | Sie können jetzt Zuordnungsregeln aus einem vorhandenen Datenfluss importieren, um Ihre Datenflusskonfigurationen zu beschleunigen und Fehler zu begrenzen. Siehe Tutorial zu [Importieren vorhandener Zuordnungsregeln](../../data-prep/ui/mapping.md) für weitere Informationen. |

Weitere Informationen zu [!DNL Data Prep] finden Sie in der [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ----------- | ----------- |
| [In-Kontext-Warnhinweise für Ziel-Datenflüsse](../../destinations/ui/alerts.md) | Jetzt können Sie Warnhinweise abonnieren, wenn Sie einen Ziel-Datenfluss erstellen, um Warnhinweise zum Status, Erfolg oder Misserfolg Ihres Datenflusses zu erhalten. Sie können Warnungen über die Experience Platform-Benutzeroberfläche oder per E-Mail erhalten. |

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md) | Verbinden und aktivieren Sie Daten mit der Werbeplattform von Criteo. |
| [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) | Verbinden und aktivieren Sie Daten für Transaktions- und Marketing-E-Mails mit der Sendgrid-Plattform. |

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Hinzufügen oder Entfernen einzelner Standardfelder für ein Schema | Mit der Benutzeroberfläche des Schema-Editors können Sie nun Teile von Standardfeldgruppen zu Ihren Schemas hinzufügen und so mehr Flexibilität für die Felder bieten, die Sie einbeziehen möchten, ohne dass Sie benutzerdefinierte Ressourcen von Grund auf neu erstellen müssen.<br><br>Sie können jetzt auch benutzerdefinierte Ad-hoc-Felder direkt in der Schemastruktur definieren und sie einer neuen oder vorhandenen benutzerdefinierten Feldergruppe zuweisen, ohne die Feldergruppe zuvor erstellen oder bearbeiten zu müssen.<br><br>Siehe Handbuch unter [Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche](../../xdm/ui/resources/schemas.md) für weitere Informationen zu diesen neuen Workflows. |

{style=&quot;table-layout:auto&quot;}

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Globales Schema | [[!UICONTROL Data Hygiene Operation Request]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | Erfasst die Details einer Datenbereinigungsanfrage zum Löschen oder Ändern von Datensätzen in einem bestimmten Datensatz oder einer bestimmten Sandbox. |
| Deskriptor | [[!UICONTROL Zeitreihen-Granularitätsdeskriptor]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | Gibt die Granularität von Zeitreihen- und Zusammenfassungsdaten an. Bei Anwendung auf ein Schema wird die `timestamp` ist der erste Zeitstempel in einem Zeitraum dieser Granularität. |
| Klasse | [[!UICONTROL Metriken zur XDM-Zusammenfassung]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | Bietet vorab zusammengefasste Metriken mit Gruppierungsdimensionen, z. B. die Ergebnisse einer SQL-AUSWAHL mit einer GRUPPE NACH. |
| Feldergruppe | [[!UICONTROL Zuordnung der Bewertungsergebnisse für Einverständnisrichtlinien]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Erfasst das Ergebnis der Bewertung der Zustimmungsrichtlinie für eine Person. |
| Feldergruppe | [[!UICONTROL Site-Suche]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Erfasst Site-Suchbezogene Informationen wie Suchabfrage, Filterung und Sortierung. |
| Feldergruppe | [[!UICONTROL Leads zusammenführen]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Erfasst die Details eines Ereignisses, bei dem zwei oder mehr Leads zusammengeführt werden. |
| Feldergruppe | [[!UICONTROL E-Mail gesendet]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Erfasst die Details eines Ereignisses, bei dem eine E-Mail an einen Empfänger gesendet wird. |
| Feldergruppe | [[!UICONTROL Zuordnen von Feldern]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Erfasst Werte, die durch den Identitätszusammenfügungsprozess für ein Ereignis berechnet werden. |
| Feldergruppe | [[!UICONTROL Sekundäre Empfängerdetails für Prüfung]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Eine Adobe Journey Optimizer-Feldergruppe, die sekundäre Empfängerdetails für eine Prüfung erfasst. |
| Feldergruppe | [[!UICONTROL XDM Business Account Person Relation Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Erfasst Details zu einer Konto-Person-Beziehung. |
| Feldergruppe | [[!UICONTROL Details zur Kontoperson]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Erfasst Details zu einer Konto-Person-Beziehung. |
| Datentyp | [[!UICONTROL Warenkorb]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Erfasst Informationen zu einem E-Commerce-Warenkorb. |
| Datentyp | [[!UICONTROL Versand]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Erfasst Versandinformationen für ein oder mehrere Produkte. |
| Datentyp | [[!UICONTROL Site-Suche]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Erfasst Informationen zur Site-Suchaktivität. |
| Erweiterung (Workfront) | [[!UICONTROL Operative Aufgabenattribute]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Erfasst Details zu einer operativen Aufgabe. |
| Erweiterung (Workfront) | [[!UICONTROL Work Portfolio Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Erfasst Details zu einem Arbeitsportfolio. |
| Erweiterung (Workfront) | [[!UICONTROL Arbeitsprogrammattribute]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Erfasst Details zu einem Arbeitsprogramm. |
| Erweiterung (Workfront) | [[!UICONTROL Arbeitsprojektattribute]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Erfasst Details zu einem Projekt. |

{style=&quot;table-layout:auto&quot;}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung der Aktualisierung |
| --- | --- | --- |
| Globales Schema | [[!UICONTROL Ziele]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | Neue Enum-Werte für `destinationCategory`. |
| Deskriptor | [[!UICONTROL Anzeigenamendeskriptor]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | Die Entfernung empfohlener Werte wird nun unterstützt (`meta:enum`), die nicht aus Standardfeldern benötigt werden. |
| Feldergruppe | [[!UICONTROL Benutzeranmeldungsprozess]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` -Feld hinzugefügt. |
| Datentyp | [[!UICONTROL Handel]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | Es wurden mehrere Felder für den Warenkorb hinzugefügt. |
| Datentyp | [[!UICONTROL Produktlistenelement]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Neue Felder für ausgewählte Optionen und Rabattbetrag hinzugefügt. |
| Erweiterung (Intelligent Services) | [[!UICONTROL Intelligent Services JourneyAI Sendezeitoptimierung]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | Optimieren Sie das Speicherformat für Sendezeitbewertungen. |
| Erweiterung (Workfront) | [[!UICONTROL Workfront-Änderungsereignis]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Mehrere Felder wurden durch eine `workfront:customData` für benutzerdefinierte Formularfelder. |
| Erweiterung (Workfront) | [[!UICONTROL Arbeitsaufgaben-Attribute]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | Mehrere Felder wurden hinzugefügt. |
| Erweiterung (Workfront) | [[!UICONTROL Arbeitsobjekt]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | Neue Felder für den übergeordneten Objekttyp und benutzerdefinierte Formularfelder. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu XDM in Platform finden Sie unter [XDM-System - Übersicht](../../xdm/home.md).

## [!DNL Intelligent Services] {#intelligent-services}

Mit Intelligent Services können Marketing-Analysten und -Experten die Vorteile von künstlicher Intelligenz und maschinellem Lernen in Anwendungsfällen mit Kundenerlebnissen nutzen. So können Marketing-Analysten mithilfe von Konfigurationen auf Unternehmensebene spezifische Prognosen für die Anforderungen der Firma erstellen, ohne dass hierfür Kenntnisse aus der Datenwissenschaft erforderlich wären.

Mit Attribution AI und Customer AI können Kunden erweiterte KI-/ML-Modelle für die Marketing-Attribution und die Kundenneigung konfigurieren. Mit der Funktion für mehrere Datensätze können Kunden zum Zeitpunkt der Modellkonfiguration mehrere Datensätze einbringen, ohne dass Daten im Voraus zugeordnet und vorbereitet werden müssen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für mehrere Datensätze | Die Funktion für mehrere Datensätze unterstützt jetzt alle Experience Event-Datensätze sowie die Auswahl von Identity Map als Identität. Kunden können die Identitätszuordnung und alle zugehörigen IDs auswählen, sofern es einen gemeinsamen Identitäts-Namespace für alle Datensätze gibt. Attribution AI unterstützt die folgenden Schemata: Adobe Analytics, Experience Event, Consumer Experience Event. Customer AI unterstützt alle diese Schemas sowie das Adobe Audience Manager-Schema. Weiterführende Informationen zur Unterstützung mehrerer Datensätze in Attribution AI und Customer AI finden Sie im Abschnitt [Attribution AI-Benutzerhandbuch](../../intelligent-services/attribution-ai/user-guide.md) und [Benutzerhandbuch für Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Neue Modellbewertungsmetriken in Customer AI | Neue Gewinndiagramme in Customer AI ermöglichen es Marketing-Experten, die Gruppengröße für das Targeting anhand ihres Budgets und ihrer ROI-Ziele zu bestimmen. In neuen Steigerungsdiagrammen wird die Qualität des Modells gemessen, was eine bessere Sichtbarkeit der Steigerung ermöglicht, die sie gegenüber zufälligem Targeting erhalten würden. Weitere Informationen finden Sie unter [Einblicke in Customer AI](../../intelligent-services/customer-ai/user-guide/discover-insights.md) Dokument. |

Weitere Informationen zu [!DNL Intelligent Services] finden Sie in der [[!DNL Intelligent Services] Übersicht](../../intelligent-services/home.md).

### Real-time Customer Data Platform B2B Edition {#B2B}

Real-time Customer Data Platform B2B Edition basiert auf Real-time Customer Data Platform (Real-time CDP) und wurde speziell für Marketing-Experten entwickelt, die in einem Business-to-Business-Service-Modell arbeiten. Es führt Daten aus verschiedenen Quellen zusammen und kombiniert sie zu einer einzigen Ansicht von Personen und Account-Profilen. Diese vereinheitlichten Daten ermöglichen es Marketing-Experten, bestimmte Zielgruppen präzise anzusprechen und über alle verfügbaren Kanäle anzusprechen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für `isDeleted` Funktion | Alle [!DNL Marketo] Datensätze außer `Activities` unterstützt jetzt die `isDeleted` Zuordnung. Die neue Zuordnung wird automatisch zu Ihren vorhandenen B2B-Datenflüssen hinzugefügt. Sie können die `isDeleted` -Mapping, um gelöschte Datensätze herauszufiltern, sodass Ihre Daten in der [!DNL Data Lake] mit Ihren Quelldaten konsistent ist. Siehe [[!DNL Marketo] Handbuch zu Zuordnungsfeldern](../../sources/connectors/adobe-applications/mapping/marketo.md) Weitere Informationen zu `isDeleted`. |

Weitere Informationen zu Real-time Customer Data Platform B2B Edition finden Sie in der [B2B-Übersicht](../../rtcdp/b2b-overview.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für [!DNL OneTrust Integration] | Sie können jetzt die [!DNL OneTrust Integration] Quelle zur Aufnahme von Einwilligungs- und Voreinstellungsdaten aus Ihrer [!DNL OneTrust] -Konto auf Platform. Weitere Informationen finden Sie in der Dokumentation unter [Erstellen einer [!DNL OneTrust Integration] Quellverbindung](../../sources/connectors/consent-and-preferences/onetrust.md) für weitere Informationen. |
| Unterstützung für [!DNL Square] | Sie können jetzt die [!DNL Square] -Quelle, um Zahlungsdaten von Ihrer [!DNL Square] -Konto auf Platform. |
| Unterstützung für das Löschen von Datenflüssen für Kundenattribute | Sie können jetzt mit dem Quell-Connector für Kundenattribute erstellte Datenflüsse löschen. |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
