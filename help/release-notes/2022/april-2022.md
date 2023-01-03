---
title: Adobe Experience Platform - Versionshinweise, April 2022
description: Die Versionshinweise für Adobe Experience Platform vom April 2022.
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2916'
ht-degree: 96%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 27. April 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [[!DNL Dashboards]](#dashboards)
- [Datenflüsse](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Real-Time Customer Data Platform B2B Edition](#B2B)
- [Quellen](#sources)

## [!DNL Dashboards] {#dashboards}

Platform bietet mehrere Dashboards, in denen Sie wichtige, bei täglichen Snapshots erfasste Informationen zu den Daten Ihres Unternehmens einsehen können.

Dashboards bieten vordefinierte Berichtsoptionen zu den Daten Ihres Unternehmens und sind direkt in den Marketing-Workflow von Platform integriert. Diese Dashboards sind ohne zusätzliche IT-Unterstützung und ohne den Zeit- und Arbeitsaufwand verfügbar, der sonst für den Export und die Verarbeitung von Daten mit zusätzlicher Data-Warehousing-Konzeption und Implementierung erforderlich wäre.

Die folgenden Widgets sind über die Widget-Bibliothek in den jeweiligen Dashboards verfügbar. Weitere Informationen finden Sie in der Dokumentation zum [Hinzufügen von Widgets über die Widget-Bibliothek](../../dashboards/customize/widget-library.md).

**Neue Widgets**

| Widget | Dashboard | Beschreibung |
| ------ | --------- | ----------- |
| [!UICONTROL Trend hinzugefügter Profile] | Profile | Dieses Widget verwendet ein Liniendiagramm, um die Gesamtanzahl der zusammengeführten Profile zu veranschaulichen, die in den letzten 30 Tagen, 90 Tagen oder 12 Monaten täglich zum Profilspeicher hinzugefügt wurden. |
| [!UICONTROL Zielgruppen, die einem Zielstatus zugeordnet sind] | Profile | Dieses Widget zeigt in einer einzigen Metrik die Gesamtzahl der zugeordneten und nicht zugeordneten Zielgruppen und veranschaulicht in einem Doughnut-Diagramm den proportionalen Unterschied zwischen ihren Summen. |
| [!UICONTROL Zielgruppengröße] | Profile | Dieses Widget bietet eine zweispaltige Tabelle, die bis zu 20 Segmente und die Gesamtzahl der in den einzelnen Segmenten enthaltenen Zielgruppen auflistet. Die Liste hängt von der angewendeten Zusammenführungsrichtlinie ab und ist entsprechend der Gesamtzahl der Zielgruppen von der größten bis zur kleinsten sortiert. |
| [!UICONTROL Trend der Profilanzahl] | Profile | Dieses Widget verwendet ein Liniendiagramm, um den Trend der Gesamtanzahl der im System enthaltenen Profile im Zeitverlauf zu veranschaulichen. Die Daten können über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. |
| [!UICONTROL Einzelne Identitätsprofile nach Identität] | Profile | Dieses Widget verwendet ein Balkendiagramm, um die Gesamtanzahl der Profile zu veranschaulichen, die mit nur einer eindeutigen Kennung gekennzeichnet sind. Das Widget unterstützt bis zu fünf der am häufigsten vorkommenden Identitäten. |
| [!UICONTROL Zielstatus] | Ziele | Dieses Widget zeigt die Gesamtzahl der aktivierten Ziele als einzelne Metrik an und veranschaulicht in einem Doughnut-Diagramm den proportionalen Unterschied zwischen aktivierten und deaktivierten Zielen. |
| [!UICONTROL Aktive Ziele nach Zielplattform] | Ziele | Dieses Widget verwendet eine zweispaltige Tabelle, um eine Liste der aktiven Zielplattformen und die Gesamtzahl der aktiven Ziele für jede Zielplattform anzuzeigen. |
| [!UICONTROL Aktivierte Zielgruppen für alle Ziele] | Ziele | Dieses Widget gibt in einer einzigen Metrik die Gesamtanzahl der Zielgruppen an, die für alle Ziele aktiviert sind. |
| [!UICONTROL Zielgruppenaktivierungs-Reihenfolge] | Segmente | Dieses Widget bietet eine dreispaltige Tabelle, in der der Zielname, die Plattform und das Aktivierungsdatum der Zielgruppe aufgelistet sind. |
| [!UICONTROL Trend der Zielgruppengröße] | Segmente | Dieses Widget bietet eine grafische Darstellung der Gesamtanzahl der Profile, die die Kriterien einer beliebigen Segmentdefinition über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten erfüllen. |
| [!UICONTROL Trend bei der Änderung der Zielgruppengröße] | Segmente | Dieses Widget bietet ein Liniendiagramm, das die Differenz der Gesamtzahl der Profile anzeigt, die sich im Zeitraum zwischen den jüngsten täglichen Snapshots für ein bestimmtes Segment qualifiziert haben. Der Trend kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. |
| [!UICONTROL Trend der Zielgruppengröße nach Identität] | Segmente | Dieses Widget veranschaulicht den Trend der Zielgruppengröße für ein bestimmtes Segment basierend auf einem ausgewählten Identitätstyp. Der Trend kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. |

**Neue Funktionen** {#new-features}

| Funktion | Dashboard | Beschreibung |
| ------- | --------- | ----------- |
| Bereinigung der Zugehörigkeit zu verwaisten Profilsegmenten | Profile und Lizenznutzung | Der Profil-Service entfernt jetzt täglich übrig gebliebene Segmentmitglieder, um eine genauere Darstellung Ihrer Profile in Ihrem System zu bieten. Diese Bereinigung erfolgt, nachdem alle Profilfragmente für ein bestimmtes Profil gelöscht wurden. Dies kann zu einem Rückgang der Metrik „Adressierbare Zielgruppe“ im Lizenznutzungs-Dashboard und zu einem Rückgang der Metrik „Profilanzahl“ im Profil-Dashboard führen, da diese Metriken vor dieser Version übrig gebliebene Segmentfragmente einbezogen haben. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen finden Sie in der Dokumentation zu [[!DNL Profiles]](../../dashboards/guides/profiles.md)-, [[!DNL Destinations]](../../dashboards/guides/destinations.md)- und [[!DNL Segments]](../../dashboards/guides/segments.md)-Dashboards.

## Datenflüsse {#dataflows}

In Platform werden Daten aus vielen verschiedenen Quellen erfasst, innerhalb des Systems analysiert und für eine Vielzahl von Zielen aktiviert. Plattform erleichtert das Tracking dieses potenziell nicht-linearen Datenflusses durch Transparenz.

Datenflüsse sind eine Darstellung von Aufträgen, die Daten innerhalb von Platform bewegen. Diese Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und helfen dabei, Daten aus Quell-Connectoren in Zieldatensätze zu verschieben, wo sie dann von Identity Service und Echtzeit-Kundenprofil verwendet werden, bevor sie schließlich für Ziele aktiviert werden.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Segment-Dashboard | Sie können jetzt das Monitoring-Dashboard verwenden, um Datenflüsse für Segmente zu überwachen. Weitere Informationen finden Sie in der Anleitung zur [Überwachung von Segmenten in der Benutzeroberfläche](../../dataflows/ui/monitor-segments.md) |

Weitere allgemeine Informationen zu Datenflüssen finden Sie in der [Übersicht zu Datenflüssen](../../dataflows/home.md). Weitere Informationen zur Segmentierung finden Sie unter [Segmentierung – Übersicht](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung der Adobe Analytics-Quelle | Die Adobe Analytics-Quelle unterstützt jetzt Datenvorbereitungsfunktionen, mit denen Sie Ihre Report Suite-Daten aus Analytics bei der Erstellung eines Datenflusses einem Ziel-XDM-Schema zuordnen können. Weitere Informationen finden Sie im Tutorial zum [Erstellen einer Analytics-Quellverbindung](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| Unterstützung des Imports vorhandener Zuordnungsregeln | Sie können jetzt Zuordnungsregeln aus einem vorhandenen Datenfluss importieren, um Ihre Datenflusskonfigurationen zu beschleunigen und Fehler zu vermeiden. Weitere Informationen finden Sie im Tutorial zum [Importieren vorhandener Zuordnungsregeln](../../data-prep/ui/mapping.md). |

Weitere Informationen zu [!DNL Data Prep] finden Sie in der [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ----------- | ----------- |
| Erweiterte Enterprise-Destination-Connectoren | Drei Enterprise-Destination-Connectoren sind jetzt allgemein verfügbar: [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md), [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)und [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md). <br> Die allgemeine Verfügbarkeit von Enterprise-Destination-Connectoren umfasst alle Funktionen, die zuvor in der Beta-Phase angeboten wurden, und mehr: <ul><li>Neue Authentifizierungsfunktionen, einschließlich [Shared Access Signature in Azure Event Hubs](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) und mehr [Authentifizierungstypen](../../destinations/catalog/streaming/http-destination.md#authentication-information) (Träger-Token, OAuth 2) im HTTP-API-Ziel;</li><li>[Aufstocken historischer Profildaten](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) (Versand von historischen Profilen, die für das Segment qualifiziert sind, wenn es zum ersten Mal aktiviert wird);</li><li>Metriken zu Datenflüssen werden jetzt für diese Ziele unterstützt;</li><li>[Zusätzliche Segmentmetadaten](../../destinations/catalog/streaming/http-destination.md#destination-details) sind in der Daten-Payload enthalten, einschließlich Segmentnamen und Segmentzeitstempeln;</li><li>Unterstützung für [statische IP-Adressen](/help/destinations/catalog/streaming/ip-address-allow-list.md) für Kunden, die Experience Platform auf die Zulassungsliste setzen müssen.</li></ul> |
| Kontextabhängige Warnhinweise für Zieldatenflüsse | Sie können jetzt beim Erstellen eines Ziel-Datenflusses [Warnhinweise abonnieren](../../destinations/ui/alerts.md), um Benachrichtigungen zum Status, Erfolg oder Misserfolg Ihres Datenflusses zu erhalten. Diese Benachrichtigungen können über die Experience Platform-Benutzeroberfläche oder per E-Mail empfangen werden. |

### Veröffentlichungsprozess für erweiterte Enterprise-Destination-Connectoren {#release-process-enterprise-destinations}

Für die Amazon Kinesis-, Azure Event-Hub- und HTTP-API-Ziele werden während des Veröffentlichungsprozesses (ab dem 27. April) im Zielkatalog sowohl die ehemalige Beta-Zielkarte als auch die neue allgemein verfügbare Zielkarte (GA) angezeigt. Alle Datenflüsse, die von Kunden unter Verwendung der Beta-Ziele konfiguriert wurden, werden in den nächsten Tagen auf die GA-Version desselben Ziels migriert. Diese Migration sollte am Freitag, dem 29. April, bis zum Ende des Tages abgeschlossen sein. Die Beta-Ziele sind während dieses kurzen Zeitfensters weiterhin sichtbar und als **Veraltet** („Deprecated“) gekennzeichnet.

Wenn Sie diese Ziele in der Beta-Phase verwendet haben, beachten Sie Folgendes:

- Wenn Sie die Beta-Version bereits zuvor mit einem der 3 Ziele verwendet haben, ist keine Aktion erforderlich. Alle Datenflüsse, die im Rahmen der Beta-Version eingerichtet wurden, funktionieren weiterhin und werden in die GA-Version migriert.
- Wenn Sie diese Ziele ab dem 27. April einrichten möchten, verwenden Sie dazu die neue GA-Version der Ziele.
- Die als veraltet gekennzeichneten Beta-Karten werden entfernt, sobald der Veröffentlichungsvorgang abgeschlossen ist, was voraussichtlich am Freitag, dem 29. April der Fall sein wird. Das Experience Platform-Engineering-Team überwacht sorgfältig die erfolgreiche Veröffentlichung.

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [!DNL Criteo] | Verbinden und Aktivieren von Daten mit der [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md)-Werbeplattform. |
| [!DNL Sendgrid] | Verbinden und Aktivieren von Daten mit der [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md)-Plattform für Transaktions- und Marketing-E-Mails. |

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Hinzufügen oder Entfernen einzelner Standardfelder für ein Schema | Mit der Benutzeroberfläche des Schema-Editors können Sie nun Teile von Standardfeldergruppen zu Ihren Schemas hinzufügen und haben so mehr Flexibilität bei der Auswahl der Felder, die Sie einbeziehen möchten, ohne dass Sie benutzerdefinierte Ressourcen von Grund auf neu erstellen müssen.<br><br>Sie können jetzt auch benutzerdefinierte Ad-hoc-Felder direkt in der Schemastruktur definieren und sie einer neuen oder vorhandenen benutzerdefinierten Feldergruppe zuweisen, ohne die Feldergruppe zuvor erstellen oder bearbeiten zu müssen.<br><br>Weitere Informationen zu diesen neuen Workflows finden Sie in der Anleitung zum [Erstellen und Bearbeiten von Schemas in der Benutzeroberfläche](../../xdm/ui/resources/schemas.md). |

{style=&quot;table-layout:auto&quot;}

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Globales Schema | [[!UICONTROL Datenhygiene-Anfrage]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | Erfasst die Details einer Datenbereinigungsanfrage zum Löschen oder Ändern von Datensätzen in einem bestimmten Datensatz oder einer bestimmten Sandbox. |
| Deskriptor | [[!UICONTROL Zeitreihen-Granularitätsdeskriptor]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | Gibt die Granularität von Zeitreihen- und Zusammenfassungsdaten an. Bei Anwendung auf ein Schema ist das Schemafeld `timestamp` der erste Zeitstempel in einem Zeitraum dieser Granularität. |
| Klasse | [[!UICONTROL Zusammengefasste XDM-Metriken]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | Bietet vorab zusammengefasste Metriken mit Gruppierungsdimensionen, z. B. die Ergebnisse von SQL SELECT mit GROUP BY. |
| Feldergruppe | [[!UICONTROL Zuordnung der Ergebnisse der Einverständnisrichtlinien-Evaluierung]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResults.schema.json) | Erfasst das Ergebnis der Einverständnisrichtlinien-Evaluierung für eine Person. |
| Feldergruppe | [[!UICONTROL Site-Suche]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Erfasst alle Informationen zur Site-Suche wie Suchanfragen, Filterung und Sortierung. |
| Feldergruppe | [[!UICONTROL Zusammenführen von Leads]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Erfasst die Details eines Ereignisses, bei dem zwei oder mehr Leads zusammengeführt werden. |
| Feldergruppe | [[!UICONTROL E-Mail gesendet]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Erfasst die Details eines Ereignisses, bei dem eine E-Mail an einen Empfänger gesendet wird. |
| Feldergruppe | [[!UICONTROL Zusammenführen von Feldern]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Erfasst Werte, die vom Identitätszusammenfügungsprozess für ein Ereignis berechnet werden. |
| Feldergruppe | [[!UICONTROL Sekundäres Empfängerdetail für Prüfung]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Eine Adobe Journey Optimizer-Feldergruppe, die sekundäre Empfängerdetails für eine Prüfung erfasst. |
| Feldergruppe | [[!UICONTROL Details zu Firmenkonto-Person-Beziehungen in XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Erfasst Details zu einer Konto-Person-Beziehung. |
| Feldergruppe | [[!UICONTROL Details zur Konto-Person-Beziehung]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Erfasst Details zu einer Konto-Person-Beziehung. |
| Datentyp | [[!UICONTROL Warenkorb]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Erfasst Informationen zu einem E-Commerce-Warenkorb. |
| Datentyp | [[!UICONTROL Lieferung]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Erfasst Lieferinformationen für ein oder mehrere Produkte. |
| Datentyp | [[!UICONTROL Site-Suche]](https://github.com/adobe/xdm/blob/master/components/datatypes/sitesearch.schema.json) | Erfasst Informationen zur Site-Suchaktivität. |
| Erweiterung (Workfront) | [[!UICONTROL Attribute operativer Aufgaben]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Erfasst Details zu einer operativen Aufgabe. |
| Erweiterung (Workfront) | [[!UICONTROL Arbeitsportfolio-Attribute]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Erfasst Details zu einem Arbeitsportfolio. |
| Erweiterung (Workfront) | [[!UICONTROL Arbeitsprogramm-Attribute]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Erfasst Details zu einem Arbeitsprogramm. |
| Erweiterung (Workfront) | [[!UICONTROL Arbeitsprojekt-Attribute]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Erfasst Details zu einem Arbeitsprojekt. |

{style=&quot;table-layout:auto&quot;}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung der Aktualisierung |
| --- | --- | --- |
| Globales Schema | [[!UICONTROL Ziele]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | Neue Enum-Werte für `destinationCategory`. |
| Deskriptor | [[!UICONTROL Anzeigenamen-Deskriptor]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | Die Entfernung empfohlener Werte (`meta:enum`), die nicht in Standardfeldern benötigt werden, wird nun unterstützt. |
| Feldergruppe | [[!UICONTROL Benutzeranmeldeprozess]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | Das Feld `createProfile` wurde hinzugefügt. |
| Datentyp | [[!UICONTROL Commerce]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | Mehrere Felder für den Warenkorb wurden hinzugefügt. |
| Datentyp | [[!UICONTROL Produktlistenelement]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Neue Felder für ausgewählte Optionen und Rabattbetrag wurden hinzugefügt. |
| Erweiterung (Intelligent Services) | [[!UICONTROL Intelligent Services-JourneyAI-Versandzeitoptimierung]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | Optimierung des Speicherformats für Versandzeit-Scores. |
| Erweiterung (Workfront) | [[!UICONTROL Workfront-Änderungsereignis]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Mehrere Felder wurden durch ein `workfront:customData`-Feld ersetzt, das als benutzerdefiniertes Formularfeld verwendet werden kann. |
| Erweiterung (Workfront) | [[!UICONTROL Arbeitsaufgaben-Attribute]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | Mehrere Felder wurden hinzugefügt. |
| Erweiterung (Workfront) | [[!UICONTROL Arbeitsobjekt]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | Neue Felder für den übergeordneten Objekttyp und benutzerdefinierte Formularfelder. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai/ml-services}

KI/ML-Services ermöglichen es Marketing-Analysten und -Praktikern, die Leistungsfähigkeit von künstlicher Intelligenz und maschinellem Lernen in Anwendungsfällen mit Kundenerlebnissen zu nutzen. So können Marketing-Analysten mithilfe von Konfigurationen auf Unternehmensebene spezifische Prognosen für die Anforderungen der Firma erstellen, ohne dass hierfür Kenntnisse aus der Datenwissenschaft erforderlich wären.

### Attributions-KI

Attributions-KI wird verwendet, um Touchpoints Ereignissen zuzuordnen, die zu Konversionen führen. Dies kann von Marketing-Experten genutzt werden, um die Auswirkungen jedes einzelnen Marketing-Touchpoints auf einer Customer Journey zu quantifizieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für mehrere Datensätze | Die Funktion für mehrere Datensätze unterstützt jetzt alle Experience Event-Datensätze sowie die Auswahl von Identity Map als Identität. Kunden können Identity Map und alle zugehörigen IDs auswählen, sofern es einen gemeinsamen Identity-Namespace für alle Datensätze gibt. Attributions-KI unterstützt die folgenden Schemas: Adobe Analytics, Experience Event, Consumer Experience Event. Weitere Informationen zur Unterstützung für mehrere Datensätze in Attributions-KI finden Sie im [Benutzerhandbuch für Attributions-KI](../../intelligent-services/attribution-ai/user-guide.md). |

Weitere Informationen zu [!DNL Intelligent Services] finden Sie in der [[!DNL Intelligent Services] Übersicht](../../intelligent-services/home.md).

### Kunden-KI

Die in Real-time Customer Data Platform verfügbare Kunden-KI dient dazu, in großem Umfang benutzerdefinierte Tendenzwerte wie Abwanderung und Konversion für einzelne Profile zu generieren. Dies wird erreicht, ohne dass die Geschäftsanforderungen in ein Problem des maschinellen Lernens umgewandelt werden müssen bzw. ein Algorithmus ausgewählt, trainiert oder bereitgestellt werden muss.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für mehrere Datensätze | Die Funktion für mehrere Datensätze unterstützt jetzt alle Experience Event-Datensätze sowie die Auswahl von Identity Map als Identität. Kunden können Identity Map und alle zugehörigen IDs auswählen, sofern es einen gemeinsamen Identity-Namespace für alle Datensätze gibt. Kunden-KI unterstützt die folgenden Schemata: Adobe Analytics, Erlebnisereignis, Verbrauchererlebnisereignis und das Adobe Audience Manager-Schema. Weitere Informationen zur Unterstützung von mehreren Datensätzen in Kunden-KI finden Sie im [Benutzerhandbuch für Kunden-KI](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Neue Modellevaluierungsmetriken in Kunden-KI | Neue Gewinndiagramme in Kunden-KI ermöglichen es Marketing-Experten, die Gruppengröße für das Targeting anhand ihres Budgets und ihrer ROI-Ziele zu bestimmen. In neuen Steigerungsdiagrammen wird die Qualität des Modells gemessen, was eine bessere Sichtbarkeit der Steigerung ermöglicht, die verglichen mit zufälligem Targeting auftreten würde. Weitere Informationen finden Sie im Dokument [Einblicke gewinnen mit Kunden-KI](../../intelligent-services/customer-ai/user-guide/discover-insights.md). |

Weitere Informationen zu [!DNL Intelligent Services] finden Sie in der [[!DNL Intelligent Services] Übersicht](../../intelligent-services/home.md).

## Real-Time Customer Data Platform B2B Edition {#B2B}

Die auf Real-time Customer Data Platform (Real-Time CDP) aufbauende Real-Time CDP B2B Edition wurde speziell für Marketing-Experten entwickelt, die in einem Business-to-Business-Dienstleistungsmodell arbeiten. Es führt Daten aus verschiedenen Quellen zusammen und kombiniert sie zu einer einzigen Ansicht von Personen und Account-Profilen. Diese vereinheitlichten Daten ermöglichen es Marketing-Experten, bestimmte Zielgruppen präzise anzusprechen und über alle verfügbaren Kanäle anzusprechen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für die Funktion `isDeleted` | Alle [!DNL Marketo]-Datensätze außer `Activities` unterstützen jetzt die `isDeleted`-Zuordnung. Die neue Zuordnung wird automatisch zu Ihren vorhandenen B2B-Datenflüssen hinzugefügt. Sie können die `isDeleted`-Zuordnung verwenden, um gelöschte Datensätze herauszufiltern, sodass Ihre Daten im [!DNL Data Lake] mit Ihren Quelldaten übereinstimmen. Weitere Informationen zu `isDeleted` finden Sie in der [[!DNL Marketo] Anleitung zum Zuordnen von Feldern](../../sources/connectors/adobe-applications/mapping/marketo.md). |

Weitere Informationen zu Real-time Customer Data Platform B2B Edition finden Sie in der [B2B-Übersicht](../../rtcdp/b2b-overview.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für [!DNL OneTrust Integration] | Sie können jetzt die Quelle [!DNL OneTrust Integration] verwenden, um Einverständnis- und Voreinstellungsdaten von Ihrem [!DNL OneTrust]-Konto in Platform aufzunehmen. Weitere Informationen finden Sie in der Dokumentation zur [Erstellung einer  [!DNL OneTrust Integration] -Quellverbindung](../../sources/connectors/consent-and-preferences/onetrust.md). |
| Unterstützung für [!DNL Square] | Sie können jetzt die Quelle [!DNL Square] verwenden, um Zahlungsdaten von Ihrem [!DNL Square]-Konto in Platform aufzunehmen. |
| Unterstützung für das Löschen von Kundenattribut-Datenflüssen | Sie können jetzt Datenflüsse löschen, die mit dem Kundenattribut-Quell-Connector erstellt wurden. |

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
