---
title: Adobe Experience Platform – Versionshinweise Januar 2021
description: Versionshinweise Januar 2021 für Adobe Experience Platform.
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 96%

---

# Adobe Experience Platform – Versionshinweise

**Releasedatum: 27. Januar 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Funktionen mit reguläreren Ausdrücken | [!DNL Data Prep] Mapper unterstützt jetzt das Abgleichen und Extrahieren eines Teils des Eingabefelds auf Grundlage von regulären Ausdrücken. |

Weitere Informationen finden Sie unter [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] ist die Objektspeicherlösung von Microsoft für die Cloud. |

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Erweiterter ID-Abgleich | Die Möglichkeiten der Übereinstimmungsrate von Zielgruppen in [!DNL Facebook Custom Audiences] und [!DNL Google Customer Match] wurden verbessert, indem nun auch weitere Parameter zur Identitätszuordnungen, wie externe IDs, Telefonnummern und IDs von Smartphones und Tablets unterstützt werden. Weiterführende Informationen finden Sie in der folgenden Dokumentation: <ul><li>[Facebook-Ziel](../../destinations/catalog/social/facebook.md)</li><li>[Ziel von Google Customer Match](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

Weitere Informationen finden Sie in [Ziele – Übersicht](../../destinations/home.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus verschiedenen Kanälen, darunter Online-, Offline-, CRM- und Drittanbieter-Datenquellen, miteinander kombiniert. Mit [!DNL Profile] können Sie Ihre unterschiedlichen Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige, im Zeitverlauf gezeichnete Darstellung jeder Kundeninteraktion bietet.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Löschen eines Datensatzes aus dem Profilspeicher | Wenn Sie einen Datensatz aus Experience Platform Data Lake löschen, wird er automatisch auch aus dem Profilspeicher gelöscht. Sie müssen nicht mehr den Vorgangs-API-Endpunkt von Profile System verwenden, um eine Löschanfrage zu erstellen und den Datensatz aus dem Profilspeicher zu löschen. Weitere Informationen finden Sie im [Handbuch zum Vorgangs-API-Endpunkt von Profile System](../../profile/api/profile-system-jobs.md). |
| Geschätzte Anzahl der IDs pro Namespace für ein bestimmtes Segment | Die Vorschau-API meldet nun Folgendes für die Anzahl der geschätzten Profile:<ul><li>Gesamtanzahl der geschätzten Profile in einem Segment für einen bestimmten Namespace.</li><li>Gesamtanzahl der geschätzten Profil im Profil-Vereinigungsschema für einen bestimmten Namespace.</li></ul>Weitere Informationen finden Sie im [Handbuch zum Profilvorschau-API-Endpunkt](../../profile/api/preview-sample-status.md). |

Weitere Informationen zum Echtzeit-Kundenprofil, einschließlich Tutorials und Best Practices für die Arbeit mit [!DNL Profile] Daten, lesen Sie bitte zunächst die [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).

## [!DNL Sources] {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbesserungen am Quell-Connector von Adobe Audience Manager | Sie können jetzt in Audience Manager einzelne First-Party-Segmente zur Aufnahme in Platform filtern und auswählen sowie First-Party-Eigenschaften herausfiltern. Weitere Informationen finden Sie im Tutorial zum [Erstellen eines Audience Manager-Quell-Connectors](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). |
| Verbesserungen am [!DNL Google BigQuery]-Quell-Connector | Mit dem [!DNL BigQuery]-Quell-Connector können Sie jetzt Dateien mit mehr als 10 GB in einem Durchgang aufnehmen. Informationen dazu finden Sie in der [[!DNL BigQuery] Übersicht zum Quell-Connector](../../sources/connectors/databases/bigquery.md). |
| Unterstützung komplexer Datentypen für die Cloud-Datenspeicherung | Sie können jetzt komplexe Datentypen, wie z. B. Arrays in JSON-Dateien, aufnehmen, wenn Sie einen Cloud-Quell-Connector verwenden. Weitere Informationen finden Sie in den Tutorials zum Erstellen eines Cloud-Datenspeicherungs-Datenflusses [in der Benutzeroberfläche](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) oder [mit der  [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md). |
| Unterstützung der Authentifizierung über einen Schlüssel für die [!DNL Microsoft Dynamics]-Quelle | Alternativ zur kennwortbasierten Authentifizierung können Sie sich jetzt mit einem Schlüssel bei Ihrem [!DNL Dynamics]-Konto authentifizieren. Weitere Informationen dazu finden Sie in der [[!DNL Dynamics] Übersicht zum Quell-Connector](../../sources/connectors/crm/ms-dynamics.md). |
| Benutzeroberflächenunterstützung für benutzerdefinierte Trennzeichen in Cloud-Datenspeicherungsquellen | Sie können jetzt ein benutzerdefiniertes Spaltentrennzeichen wie Komma (`,`), Tabulator (`\t`) oder Pipe (`|`) festlegen, um durch Trennzeichen getrennte Dateien in der Benutzeroberfläche zu erfassen. Weitere Informationen finden Sie im Tutorial zum [Erstellen eines Datenflusses mit einem Quell-Connector für die Cloud-Datenspeicherung](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
