---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform vom 27. Januar 2021
doc-type: release notes
last-update: January 27, 2021
author: ens60013
translation-type: tm+mt
source-git-commit: cf70b21f3a8c02b25e5acd3be8c8feaa3f52a5e3
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 40%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: 27. Januar 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten dem Experience Data Model (XDM) zuzuordnen, umzuformen und zu validieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Regelmäßige Ausdruck-Funktionen | [!DNL Data Prep] Mapper unterstützt jetzt das Abgleichen und Extrahieren eines Teils des Eingabefelds auf Grundlage von regulären Ausdrücken. |

Weitere Informationen finden Sie unter [[!DNL Data Prep] overview](../../data-prep/home.md).

## [!DNL Sources] {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbesserungen am Adobe Audience Manager-Quell-Connector | Sie können jetzt einzelne Erstanbietersegmente von Audience Manager bis zur Erfassung in Plattform filtern und auswählen sowie Erstanbieter-Eigenschaften herausfiltern. Weitere Informationen finden Sie im Lernprogramm unter [Erstellen eines Audience Manager-Quellconnectors](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). |
| [!DNL Google BigQuery] Verbesserungen am Quellanschluss | Mit dem [!DNL BigQuery]-Quell-Connector können Sie jetzt Dateien mit einer Auflösung von mehr als 10 GB in einem Fluss erfassen. Weitere Informationen finden Sie unter [[!DNL BigQuery] Übersicht über den Quellanschluss](../../sources/connectors/databases/bigquery.md). |
| Unterstützung komplexer Datentypen für Cloud-Datenspeicherung | Sie können jetzt komplexe Datentypen, wie z. B. Arrays in JSON-Datenspeicherung, erfassen, wenn Sie einen Cloud-Quell-Connector verwenden. Weitere Informationen finden Sie in den Tutorials zum Erstellen eines Cloud-Datenspeicherung-Datenflusses [in der Benutzeroberfläche](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) oder [mit der  [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md). |
| Unterstützung der Hauptschlüssel-basierten Authentifizierung für [!DNL Microsoft Dynamics]-Quelle | Sie können sich jetzt mit einem Hauptschlüssel als Alternative zur kennwortbasierten Authentifizierung bei Ihrem [!DNL Dynamics]-Konto authentifizieren. Weitere Informationen finden Sie unter [[!DNL Dynamics] Übersicht über den Quellanschluss](../../sources/connectors/crm/ms-dynamics.md). |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
