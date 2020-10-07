---
keywords: Experience Platform;home;popular topics;Audience Manager connector;Audience manager;audience manager
solution: Experience Platform
title: Audience Manager-Anschluss
topic: overview
description: Der Adobe Audience Manager Data Connector streamt Erstanbieter-Daten, die in Adobe Audience Manager bis Adobe Experience Platform erfasst werden. Der Audience Manager-Connector fasst drei Kategorien Daten in die Plattform ein.
translation-type: tm+mt
source-git-commit: 9bd893820c7ab60bf234456fdd110fb2fbe6697c
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 2%

---


# Audience Manager-Anschluss

Der Adobe Audience Manager Data Connector streamt Erstanbieter-Daten, die in Adobe Audience Manager bis Adobe Experience Platform erfasst werden. Der Audience Manager Connector integriert drei Kategorien Daten in die Plattform:

- **Echtzeitdaten:** Daten, die in Echtzeit auf dem Datenerfassungsserver des Audience Managers erfasst werden. Diese Daten werden in Audience Manager verwendet, um regelbasierte Eigenschaften zu füllen, und treten in kürzester Latenzzeit auf der Plattform auf.
- **Profil-Daten:** Audience Manager nutzt Echtzeitdaten und Onboard-Daten, um Kundendaten abzuleiten. Diese Profil werden zum Ausfüllen von Identitätsdiagrammen und Eigenschaften bei Segmentrealisierungen verwendet.

Der Audience Manager Connector ordnet diese Kategorien dem Experience Data Model (XDM)-Schema zu und sendet sie an die Plattform. Echtzeitdaten werden als XDM ExperienceEvent-Daten gesendet, während Profil-Daten als XDM-Profil gesendet werden.

For instructions on creating a connection with Adobe Audience Manager using the Platform UI, see the [Audience Manager connector tutorial](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## Was ist Erlebnisdatenmodell (XDM)?

XDM ist eine öffentlich dokumentierte Spezifikation, die ein standardisiertes Framework bietet, mit dem Plattform Kundenerlebnisdaten organisiert.

Durch die Einhaltung der XDM-Standards können Kundenerlebnisdaten einheitlich integriert werden, was die Bereitstellung von Daten und das Sammeln von Informationen erleichtert.

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
| Audience Manager Echtzeit-Profil-Updates | Dieser Datensatz ermöglicht Echtzeit-Targeting von Audience Manager-Eigenschaften und Segmenten. Es enthält Informationen zum regionalen Edge-Routing, zu Eigenschaften und zur Segmentmitgliedschaft. Lassen Sie diesen Datensatz für die Erfassung von Profilen aktiviert. |
| Audience Manager-Gerätedaten | Gerätedaten mit ECIDs und entsprechenden Segmentzuordnungen, die in Audience Manager aggregiert werden. |
| Profil-Daten des Audience Managers | Wird für die Audience Manager-Connector-Diagnose verwendet. |
| Authentifizierte Profile für Audience Manager | Dieser Datensatz enthält vom Audience Manager authentifizierte Profil. |
| Audience Manager-Authentifizierungsdaten zu Profilen | Wird für die Audience Manager Connector-Diagnose verwendet. |

### Verbindungen

Adobe Audience Manager erstellt eine Verbindung im Katalog: Audience Manager Connection. Catalog ist das System der Datensätze für die Datenposition und -reihenfolge in Adobe Experience Platform. Eine Verbindung ist ein Katalogobjekt, das eine kundenspezifische Instanz von Connectors ist. Weitere Informationen zu Katalogen, Verbindungen und Connectors finden Sie in der Übersicht über den [Katalogdienst](../../../catalog/home.md) .

## Welche Latenz wird für Plattformdaten von Audience Managern erwartet?

| Audience Manager-Daten | Latenz | Anmerkungen |
| --- | --- | --- |
| Echtzeitdaten | &lt; 35 Minuten. | Zeit von der Erfassung am Knoten Echtzeit bis zur Anzeige auf dem Plattform Data Lake. |
| Eingehende Daten | &lt; 13 Stunden | Zeit von der Erfassung in S3-Behältern bis zur Anzeige auf dem Platform Data Lake. |
| Profildaten | &lt; 2 Tage | Zeit vom Erfassen von Echtzeitdaten/Inbound bis zum Hinzufügen zu einem Profil und schließlich der Anzeige auf dem Platform Data Lake. |