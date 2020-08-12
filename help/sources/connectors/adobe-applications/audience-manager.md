---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Audience Manager-Anschluss
topic: overview
translation-type: tm+mt
source-git-commit: a1b09f3e88e489f1b0ec0c1fcb72a2a5a4356d87
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 2%

---


# Audience Manager-Anschluss

Der Adobe Audience Manager Data Connector streamt Erstanbieter-Daten, die in Adobe Audience Manager bis Adobe Experience Platform erfasst werden. Der Audience Manager Connector integriert drei Kategorien Daten in die Plattform:

- **Echtzeitdaten:** Daten, die in Echtzeit auf dem Datenerfassungsserver des Audience Managers erfasst werden. Diese Daten werden in Audience Manager verwendet, um regelbasierte Eigenschaften zu füllen, und treten in kürzester Latenzzeit auf der Plattform auf.
- **Profil-Daten:** Audience Manager nutzt Echtzeitdaten und Onboard-Daten, um Kundendaten abzuleiten. Diese Profil werden zum Ausfüllen von Identitätsdiagrammen und Eigenschaften bei Segmentrealisierungen verwendet.

The Audience Manager connector maps these data categories to Experience Data Model (XDM) schema and sends them to Platform. Realtime data are sent as XDM ExperienceEvent data, while Profile data is sent as XDM Individual Profiles.

For instructions on creating a connection with Adobe Audience Manager using the Platform UI, see the [Audience Manager connector tutorial](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## What is Experience Data Model (XDM)?

XDM ist eine öffentlich dokumentierte Spezifikation, die ein standardisiertes Framework bietet, mit dem Plattform Kundenerlebnisdaten organisiert.

Adhering to XDM standards allows customer experience data to be uniformly incorporated, making it easier to deliver data and gather information.

Weitere Informationen zur Verwendung von XDM in der Experience Platform finden Sie in der [XDM-Systemübersicht](../../../xdm/home.md). Weitere Informationen zur Strukturierung von XDM-Schemas wie Profil und ExperienceEvent finden Sie in den [Grundlagen der Schema-Komposition](../../../xdm/schema/composition.md).

## Beispiele für XDM-Schema

Im Folgenden finden Sie Beispiele für die Audience Manager-Struktur, die XDM ExperienceEvent und XDM Individual Profil in Platform zugeordnet ist.

### ExperienceEvent - für Echtzeitdaten und Onboarded-Daten

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM Individuelles Profil - zum Profil

![](images/aam-profile-xdm-for-profile-data.png)

## Wie werden Felder von Adobe Audience Manager zu XDM zugeordnet?

Weitere Informationen finden Sie in der Dokumentation zu den Feldern [für die Zuordnung von](./mapping/audience-manager.md) Audience Managern.

## Data Management auf Plattform

### Datensätze

Datasets sind ein Datenspeicherung- und Verwaltungskonstrukt für eine Datenerfassung, normalerweise eine Tabelle, die Schema (Spalten) und Felder (Zeilen) enthält und über eine Datenverbindung zur Verfügung gestellt wird. Audience Manager-Daten bestehen aus Echtzeitdaten, Inbound-Daten und Profil-Daten. Verwenden Sie zur Suche nach Ihren Audience Manager-Datensätzen die Suchfunktion in der Benutzeroberfläche mit den angegebenen Benennungsregeln für jeden Datentyp.

Audience Manager-Datasets sind standardmäßig zum Profil deaktiviert, und die Benutzer können Datensätze je nach Anwendungsfall aktivieren oder deaktivieren. Es wird nicht empfohlen, Datensätze zu deaktivieren, die für die Segmentmitgliedschaft in Profil verwendet werden.

| Dataset-Name | Beschreibung |
| ------------ | ----------- |
| Audience Manager Echtzeit | Dieser Datensatz enthält Daten, die durch direkte Treffer auf Audience Manager-DCS-Endpunkten erfasst werden, sowie Identitätskarten für Audience Manager-Profil. Lassen Sie diesen Datensatz für die Erfassung von Profilen aktiviert. |
| Audience Manager Echtzeit-Profil-Updates | Dieser Datensatz ermöglicht Echtzeit-Targeting von Audience Manager-Eigenschaften und Segmenten. It includes information for Edge regional routing, trait, and segment membership. Keep this dataset enabled for Profile ingestion. |
| Audience Manager Devices Data | Device data with ECIDs and corresponding segment realizations aggregated in Audience Manager. |
| Audience Manager Device Profile Data | Wird für die Audience Manager-Connector-Diagnose verwendet. |
| Audience Manager-Authentifizierte Profile | Dieser Datensatz enthält vom Audience Manager authentifizierte Profil. |
| Audience Manager-Authentifizierungsdaten zu Profilen | Wird für die Audience Manager Connector-Diagnose verwendet. |

### Verbindungen

Adobe Audience Manager erstellt eine Verbindung im Katalog: **Audience Manager Connection**. Catalog is the system of the records for data location and lineage within Adobe Experience Platform. Eine Verbindung ist ein Katalogobjekt, das eine kundenspezifische Instanz von Connectors ist. Please see the [Catalog Service overview](../../../catalog/home.md) for more information on Catalog, connections, and connectors.

## Welche Latenz wird für Plattformdaten von Audience Managern erwartet?

| Audience Manager-Daten | Latenz | Anmerkungen |
| --- | --- | --- |
| Echtzeitdaten | &lt; 35 Minuten. | Zeit von der Erfassung am Knoten Echtzeit bis zur Anzeige auf dem Plattform Data Lake. |
| Eingehende Daten | &lt; 13 Stunden | Time from being captured at S3 buckets to appearing on Platform Data Lake. |
| Profildaten | &lt; 2 Tage | Time from being captured from Realtime/Inbound data to being added to a user profile and finally appearing on Platform Data Lake. |