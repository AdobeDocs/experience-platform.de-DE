---
keywords: Experience Platform; Startseite; beliebte Themen; Audience Manager-Connector; Audience Manager; Audience Manager
solution: Experience Platform
title: Übersicht über den Audience Manager Source Connector
topic-legacy: overview
description: Der Adobe Audience Manager-Quell-Connector streamt Erstanbieterdaten, die im Audience Manager erfasst wurden, an Adobe Experience Platform.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: d0b6885b6e8606692cfe1173b75c7d3537800a5f
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 1%

---

# Audience Manager-Connector

Der Adobe Audience Manager-Data Connector streamt Erstanbieterdaten, die in Adobe Audience Manager erfasst wurden, an Adobe Experience Platform. Der Audience Manager-Connector erfasst zwei Datenkategorien in Platform:

- **Echtzeitdaten:** Daten, die in Echtzeit auf dem Datenerfassungsserver des Audience Managers erfasst werden. Diese Daten werden in Audience Manager zum Ausfüllen regelbasierter Eigenschaften verwendet und werden in Platform in der kürzesten Latenzzeit angezeigt.
- **Profildaten:** Audience Manager verwendet Echtzeitdaten und integrierte Daten, um Kundenprofile abzuleiten. Diese Profile werden zum Ausfüllen von Identitätsdiagrammen und Eigenschaften in Segmentrealisierungen verwendet.

Der Audience Manager-Connector ordnet diese Datenkategorien dem Experience-Datenmodell (XDM)-Schema zu und sendet sie an Platform. Echtzeitdaten werden als XDM ExperienceEvent-Daten gesendet, während Profildaten als XDM Individual Profiles gesendet werden.

Anweisungen zum Erstellen einer Verbindung mit Adobe Audience Manager mithilfe der Platform-Benutzeroberfläche finden Sie in der [Audience Manager-Connector-Tutorial](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## Was ist Experience-Datenmodell (XDM)?

XDM ist eine öffentlich dokumentierte Spezifikation, die ein standardisiertes Framework bereitstellt, mit dem Platform Kundenerlebnisdaten organisiert.

Durch die Einhaltung von XDM-Standards können Kundenerlebnisdaten einheitlich integriert werden, was die Bereitstellung von Daten und das Sammeln von Informationen erleichtert.

Weitere Informationen zur Verwendung von XDM in Experience Platform finden Sie unter [XDM-System - Übersicht](../../../xdm/home.md). Weitere Informationen zur Struktur von XDM-Schemas wie Profil und ExperienceEvent finden Sie in der [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md).

## Beispiele für XDM-Schemas

Im Folgenden finden Sie Beispiele für die Audience Manager-Struktur, die XDM ExperienceEvent und XDM Individual Profile in Platform zugeordnet ist.

### ExperienceEvent - für Echtzeitdaten und integrierte Daten

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM Individual Profile - für Profildaten

![](images/aam-profile-xdm-for-profile-data.png)

## Wie werden Felder von Adobe Audience Manager XDM zugeordnet?

Weitere Informationen finden Sie in der Dokumentation für [Audience Manager-Zuordnungsfelder](./mapping/audience-manager.md) für weitere Informationen.

## Daten-Management in Platform

### Datensätze

Datensätze sind ein Speicher- und Verwaltungskonstrukt für eine Datenerfassung, normalerweise eine Tabelle, die Schema (Spalten) und Felder (Zeilen) enthält und durch eine Datenverbindung zur Verfügung gestellt wird. Audience Manager-Daten bestehen aus Echtzeitdaten, eingehenden Daten und Profildaten. Um Ihre Audience Manager-Datensätze zu finden, verwenden Sie die Suchfunktion in der Benutzeroberfläche mit den angegebenen Benennungskonventionen für jeden Datentyp.

Audience Manager-Datensätze sind standardmäßig für Profil deaktiviert und Benutzer können Datensätze anhand ihrer Anwendungsfälle aktivieren oder deaktivieren. Es wird nicht empfohlen, Datensätze zu deaktivieren, die für die Segmentzugehörigkeit in Profil verwendet werden.

>[!NOTE]
>
>AAM Echtzeit ist der einzige Datensatz, der an die [!DNL Data Lake]. Alle anderen Audience Manager-Datensätze werden an [!DNL Profile], wenn sie für [!DNL Profile]. Wenn sie nicht aktiviert sind für [!DNL Profile], erhalten sie keine Daten und werden als leer angezeigt.

| Datensatzname | Beschreibung | Klasse |
| --- | --- | --- |
| AAM Echtzeit | Dieser Datensatz enthält Daten, die von direkten Treffern auf Audience Manager-DCS-Endpunkten erfasst werden, und Identitätszuordnungen für Audience Manager-Profile. Lassen Sie diesen Datensatz für die Profilaufnahme aktiviert. | Erlebnisereignis |
| AAM Echtzeit-Profilaktualisierungen | Dieser Datensatz ermöglicht das Echtzeit-Targeting von Audience Manager-Eigenschaften und -Segmenten. Sie enthält Informationen zum regionalen Routing, zu Eigenschaften und zur Segmentzugehörigkeit von Edge. Lassen Sie diesen Datensatz für die Profilaufnahme aktiviert. Daten sind nicht als Batches im Datensatz sichtbar. Sie können die **[!UICONTROL Profil]** umschalten, um die Daten direkt in Profil zu erfassen. | Datensatz |
| AAM Gerätedaten | Gerätedaten mit ECIDs und entsprechenden Segmentrealisierungen, die in Audience Manager aggregiert werden. Daten sind nicht als Batches im Datensatz sichtbar. Sie können die **[!UICONTROL Profil]** umschalten, um die Daten direkt in Profil zu erfassen. | Datensatz |
| AAM Geräteprofildaten | Wird für die Audience Manager-Connector-Diagnose verwendet. Daten sind nicht als Batches im Datensatz sichtbar. Sie können die **[!UICONTROL Profil]** umschalten, um die Daten direkt in Profil zu erfassen. | Datensatz |
| AAM authentifizierte Profile | Dieser Datensatz enthält vom Audience Manager authentifizierte Profile. Daten sind nicht als Batches im Datensatz sichtbar. Sie können die **[!UICONTROL Profil]** umschalten, um die Daten direkt in Profil zu erfassen. | Datensatz |
| AAM Authentifizierte Profilmetrikdaten | Wird für die Audience Manager Connector-Diagnose verwendet. Daten sind nicht als Batches im Datensatz sichtbar. Sie können die **[!UICONTROL Profil]** umschalten, um die Daten direkt in Profil zu erfassen. | Datensatz |
| Datenaufstockung für AAM Geräte | Datensatz aus dem Einbringen von Daten früherer Geräte. Dies umfasst ECIDs und entsprechende in Audience Manager aggregierte Segmentrealisierungen. Daten sind nicht als Batches im Datensatz sichtbar. Sie können die **[!UICONTROL Profil]** umschalten, um die Daten direkt in Profil zu erfassen. | Datensatz |
| Aufstockung authentifizierter AAM | Datensatz aus dem Einbringen authentifizierter Daten in die Vergangenheit. Hier sind vom Audience Manager authentifizierte Profile enthalten. Daten sind nicht als Batches im Datensatz sichtbar. Sie können die **[!UICONTROL Profil]** umschalten, um die Daten direkt in Profil zu erfassen. | Datensatz |

### Verbindungen

Adobe Audience Manager erstellt eine Verbindung im Katalog: Audience Manager-Verbindung. Catalog ist das System der Datensätze für Speicherort und Herkunft von Daten in Adobe Experience Platform. Eine Verbindung ist ein Catalog-Objekt, das eine kundenspezifische Instanz von Connectoren ist. Siehe [Catalog Service - Übersicht](../../../catalog/home.md) Weitere Informationen zu Katalog, Verbindungen und Connectoren.

## Wie hoch ist die erwartete Latenz für Audience Manager Data on Platform?

| Audience Manager Data | Latenz | Anmerkungen |
| --- | --- | --- |
| Echtzeitdaten | &lt; 35 Minuten. | Zeit vom Erfassen im Audience Manager Edge-Knoten bis zum Anzeigen im Platform Data Lake. |
| Profildaten | &lt; 2 Tage | Zeit von der Erfassung über DCS-/PCS-Edge-Daten und integrierte Daten, der Verarbeitung zu einem Benutzerprofil bis zur Anzeige im Profil. Diese Daten werden heute nicht direkt im Platform Data Lake landen. Die Profilumschaltung kann für Audience Manager-Profil-Datensätze aktiviert werden, um diese Daten direkt in das Profil aufzunehmen. |
