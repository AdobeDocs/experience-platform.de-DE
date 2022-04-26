---
title: Adobe Experience Platform - Versionshinweise, April 2022
description: Die Versionshinweise für Adobe Experience Platform vom April 2022.
source-git-commit: fe30444fb2d11c38433c73d88ee4c8e9a32bdff8
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 21%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 27. April 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Datenflüsse](#dataflows)
- [Experience-Datenmodell (XDM)](#xdm)

## Datenflüsse {#dataflows}

In Platform werden Daten aus vielen verschiedenen Quellen erfasst, innerhalb des Systems analysiert und für eine Vielzahl von Zielen aktiviert. Plattform erleichtert das Tracking dieses potenziell nicht-linearen Datenflusses durch Transparenz.

Datenflüsse sind eine Darstellung von Aufträgen, die Daten innerhalb von Platform bewegen. Diese Datenflüsse werden über verschiedene Services konfiguriert, wodurch Daten von den Quell-Connectoren in Zieldatensätze verschoben werden können. Dort werden sie von Identity Service und vom Echtzeit-Kundenprofil verwendet, bevor sie schließlich für Ziele aktiviert werden.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Segmente-Dashboard | Sie können jetzt das Monitoring-Dashboard verwenden, um Datenflüsse auf Segmente zu überwachen. Weitere Informationen finden Sie im Handbuch unter [Überwachen von Segmenten in der Benutzeroberfläche](../../dataflows/ui/monitor-segments.md) |

Weitere allgemeine Informationen zu Datenflüssen finden Sie in der [Übersicht zu Datenflüssen](../../dataflows/home.md). Weitere Informationen zur Segmentierung finden Sie im Abschnitt [Segmentierungsübersicht](../../segmentation/home.md).

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

