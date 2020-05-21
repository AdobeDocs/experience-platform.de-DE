---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Audience Manager-Anschluss
topic: overview
translation-type: tm+mt
source-git-commit: fb4ffa2c95365905f5417586fa7ecf88523009a0
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---


# Audience Manager-Anschluss

Der Adobe Audience Manager Data Connector streamt Daten von Erstanbietern, die im Adobe Audience Manager erfasst wurden, an Adobe Experience Platform. Der Audience Manager Connector integriert drei Kategorien Daten in die Plattform:

- **Echtzeitdaten:** Daten, die in Echtzeit auf dem Datenerfassungsserver von Audience Manager erfasst werden. Diese Daten werden im Audience Manager zum Ausfüllen regelbasierter Eigenschaften verwendet und treten in kürzester Latenzzeit in der Plattform auf.
- **Integrierte (eingehende) Daten:** Dies sind die Dateien, die ein Benutzer an einen Amazon S3-Speicherort hochgeladen hat, der von Audience Manager gehostet wird. Audience Manager verwendet diese Daten, um mit der Methode &quot;Inbound file&quot;Eigenschaften an Bord zu füllen, was zu einer gewissen Latenz führt.
- **Profil-Daten:** Audience Manager nutzt Echtzeitdaten und Onboard-Daten, um Kundendaten abzuleiten. Diese Profil werden zum Ausfüllen von Identitätsdiagrammen und Eigenschaften bei Segmentrealisierungen verwendet.

Der Audience Manager-Connector ordnet diese Kategorien dem Experience Data Model (XDM)-Schema zu und sendet sie an die Plattform. Echtzeitdaten und Onboarded-Daten werden als XDM ExperienceEvent-Daten gesendet, während Profil-Daten als XDM-Profil gesendet werden.

Anweisungen zum Erstellen einer Verbindung mit Adobe Audience Manager mithilfe der Plattform-Benutzeroberfläche finden Sie im [Audience Manager Connector-Lernprogramm](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## Was ist Erlebnisdatenmodell (XDM)?

XDM ist eine öffentlich dokumentierte Spezifikation, die ein standardisiertes Framework bietet, mit dem Plattform Kundenerlebnisdaten organisiert.

Durch die Einhaltung der XDM-Standards können Kundenerlebnisdaten einheitlich integriert werden, was die Bereitstellung von Daten und das Sammeln von Informationen erleichtert.

Weitere Informationen zur Verwendung von XDM in Experience Platform finden Sie in der [XDM-Systemübersicht](../../../xdm/home.md). Weitere Informationen zur Strukturierung von XDM-Schemas wie Profil und ExperienceEvent finden Sie in den [Grundlagen der Schema-Komposition](../../../xdm/schema/composition.md).

## Beispiele für XDM-Schema

Im Folgenden finden Sie Beispiele für die Audience Manager-Struktur, die XDM ExperienceEvent und XDM Individual Profil in Platform zugeordnet ist.

### ExperienceEvent - für Echtzeitdaten und Onboarded-Daten

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM Individuelles Profil - zum Profil

![](images/aam-profile-xdm-for-profile-data.png)

## Wie werden Felder von Adobe Audience Manager zu XDM zugeordnet?

Weitere Informationen finden Sie in der Dokumentation zu [Audience Manager-Zuordnungsfeldern](./mapping/audience-manager.md) .

## Data Management auf Plattform

### Datensätze

Datasets sind ein Datenspeicherung- und Verwaltungskonstrukt für eine Datenerfassung, normalerweise eine Tabelle, die Schema (Spalten) und Felder (Zeilen) enthält und über eine Datenverbindung zur Verfügung gestellt wird. Audience Manager-Daten bestehen aus Echtzeitdaten, Inbound-Daten und Profil-Daten. Verwenden Sie zur Suche nach Ihren Audience Manager-Datensätzen die Suchfunktion in der Benutzeroberfläche mit den angegebenen Benennungsregeln für jeden Datentyp.

Audience Manager-Datensätze sind standardmäßig zum Profil deaktiviert, und Benutzer können Datensätze je nach Anwendungsfall aktivieren oder deaktivieren. Es wird nicht empfohlen, Datensätze zu deaktivieren, die für die Segmentmitgliedschaft in Profil verwendet werden.

| Dataset-Name | Beschreibung |
| ------------ | ----------- |
| Audience Manager Echtzeit | Dieser Datensatz enthält Daten, die durch direkte Treffer auf DCS-Endpunkten von Audience Manager erfasst werden, sowie Identitätskarten für Audience Manager-Profil. Lassen Sie diesen Datensatz für die Erfassung von Profilen aktiviert. |
| Audience Manager Echtzeit-Profil-Updates | Dieser Datensatz ermöglicht Echtzeit-Targeting von Eigenschaften und Segmenten von Audience Manager. Es enthält Informationen zum regionalen Edge-Routing, zu Eigenschaften und zur Segmentmitgliedschaft. Lassen Sie diesen Datensatz für die Erfassung von Profilen aktiviert. |
| Audience Manager-Gerätedaten | Gerätedaten mit ECIDs und entsprechenden Segmentzuordnungen, die im Audience Manager aggregiert werden. |
| Gerätedaten zum Audience Manager-Profil | Wird für die Connector-Diagnose von Audience Manager verwendet. |
| Authentifizierte Profil von Audience Manager | Dieser Datensatz enthält vom Audience Manager authentifizierte Profil. |
| Metadaten zu authentifizierten Profilen im Audience-Manager | Wird für die Connector-Diagnose von Audience Manager verwendet. |
| Audience Manager Inbound {Datenquellen-ID} **(nicht mehr unterstützt)** | Dieser Datensatz stellt Onboarded-Datensätze in Audience Manager über die Methode Inbound-Datei dar. Dieser Datenfluss ist veraltet und wird in einer folgenden Version entfernt. |
| Audience Manager Inbound Meta Data **(nicht mehr unterstützt)** | Wird für die Connector-Diagnose von Audience Manager verwendet. Dieser Datenfluss ist veraltet und wird in einer folgenden Version entfernt. |

### Verbindungen

Adobe Audience Manager erstellt eine Verbindung im Katalog: **Audience Manager Connection**. Catalog ist das System der Datensätze für den Speicherort und die Datenlinie in Adobe Experience Platform. Eine Verbindung ist ein Katalogobjekt, das eine kundenspezifische Instanz von Connectors ist. Weitere Informationen zu Katalogen, Verbindungen und Connectors finden Sie in der Übersicht über den [Katalogdienst](../../../catalog/home.md) .

## Welche Latenz wird für Audience Manager-Daten auf der Plattform erwartet?

| Audience Manager-Daten | Latenz | Anmerkungen |
| --- | --- | --- |
| Echtzeitdaten | &lt; 35 Minuten. | Zeit von der Erfassung am Knoten Echtzeit bis zur Anzeige auf dem Plattform Data Lake. |
| Inbound-Daten | &lt; 13 Stunden | Zeit von der Erfassung in S3-Behältern bis zur Anzeige auf dem Platform Data Lake. |
| Profil | &lt; 2 Tage | Zeit vom Erfassen von Echtzeitdaten/Inbound bis zum Hinzufügen zu einem Profil und schließlich der Anzeige auf dem Platform Data Lake. |