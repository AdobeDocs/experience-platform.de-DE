---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform vom 27. Januar 2021
doc-type: release notes
last-update: January 27, 2021
author: ens60013
translation-type: tm+mt
source-git-commit: 18712835b2408b24cd2735b19c94bf1b1fe50df1
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 30%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: 27. Januar 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten dem Experience Data Model (XDM) zuzuordnen, umzuformen und zu validieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Regelmäßige Ausdruck-Funktionen | [!DNL Data Prep] Mapper unterstützt jetzt das Abgleichen und Extrahieren eines Teils des Eingabefelds auf Grundlage von regulären Ausdrücken. |

Weitere Informationen finden Sie unter [[!DNL Data Prep] overview](../../data-prep/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vordefinierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Sie können Ziele verwenden, um bekannte und unbekannte Daten für Cross-Kanal-Marketing-Kampagnen, E-Mail-Kampagnen, gezielte Werbung und viele andere Anwendungsfälle zu aktivieren.

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] ist die Objektlösung von Microsoft für die Cloud. |

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Erweiterte ID-Übereinstimmung | Die Funktionen für Übereinstimmungsraten bei Audiencen in [!DNL Facebook Custom Audiences] und [!DNL Google Customer Match] wurden verbessert, indem zusätzliche Identitätszuordnungen wie externe IDs, Telefonnummern und Mobilgeräte-IDs unterstützt werden. Weitere Informationen finden Sie in der folgenden Dokumentation: <ul><li>[Facebook-Ziel](../../destinations/catalog/social/facebook.md)</li><li>[Google-Kundenübereinstimmungsziel](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Profile und Segmente für ein Ziel aktivieren](../../destinations/ui/activate-destinations.md)</li></ul> |

Weitere Informationen finden Sie in [Ziele – Übersicht](../../destinations/home.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen und anderen Kanälen miteinander kombiniert. [!DNL Profile] ermöglicht Ihnen die Konsolidierung von Kundendaten in einer einheitlichen Ansicht, die eine umsetzbare und zeitgestempelte Kundeninteraktion ermöglicht.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Datensatz aus Profil Store löschen | Wenn Sie einen Datensatz aus dem Data Lake der Experience Platform löschen, wird er automatisch auch aus dem Profil-Store gelöscht. Sie müssen nicht mehr den API-Endpunkt für Systemaufträge verwenden, um eine Löschanforderung zu erstellen, um den Datensatz explizit aus dem Profil Store zu löschen. Weitere Informationen finden Sie im Handbuch [API-Endpunkt für Systemaufträge](../../profile/api/profile-system-jobs.md) des Profils. |
| Geschätzte Anzahl der ID-Namensraum für ein bestimmtes Segment | Die Vorschauen-API meldet nun für geschätzte Profil Folgendes:<ul><li>Gesamtanzahl der geschätzten Profil in einem Segment für einen bestimmten Namensraum.</li><li>Gesamtanzahl der geschätzten Profil im Schema der Profil-Vereinigung für einen bestimmten Namensraum.</li></ul>Weitere Informationen finden Sie im Handbuch [Profil Vorschau API endpoint guide](../../profile/api/preview-sample-status.md). |

Weitere Informationen zum Echtzeit-Profil von Kunden, einschließlich Schulungen und Best Practices für die Arbeit mit [!DNL Profile]-Daten, finden Sie im [Überblick über das Echtzeit-Profil von Kunden](../../profile/home.md).

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
| Benutzeroberflächenunterstützung für benutzerdefinierte Trennzeichen in Cloud-Datenspeicherung-Quellen | Sie können jetzt ein benutzerdefiniertes Spaltentrennzeichen wie ein Komma (`,`), ein Tabulator (`\t`) oder ein Pipe (`|`) festlegen, um durch Trennzeichen getrennte Dateien in der Benutzeroberfläche zu erfassen. Weitere Informationen finden Sie im Tutorial [Erstellen eines Datenflusses mit einem Cloud-Datenspeicherung-Quellanschluss](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
