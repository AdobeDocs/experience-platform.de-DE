---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform, 10. August 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: dba7ae62b51b5cc4556f7f12d43b84e90f6c29dc
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 31%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: 12. August 2020**

Updates to existing features in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [!DNL Destinations](#destinations)
- [[!DNL-Quellen]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] nutzt maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu entfesseln. Integrated into Adobe Experience Platform, [!DNL Data Science Workspace] helps you make predictions using your content and data assets across Adobe solutions.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| VM improvements in [!DNL JupyterLab] | Improved the stability of long-running [!DNL JupyterLab notebook] virtual machines. |

For more information on [!DNL JupyterLab], please see the [[!DNL JupyterLab] user guide](../../data-science-workspace/jupyterlab/overview.md).

## Ziele {#destinations}

In der [Adobe Echtzeit-Kundendatenplattform](../../rtcdp/overview.md) sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner auf nahtlose Weise aktivieren.

**Neue Ziele**

Es stehen neue Ziele zur Verfügung, für die Sie Ihre Adobe Experience Platform-Daten aktivieren können. Weitere Informationen finden Sie hier:

| Ziel | Beschreibung |
|--- | ---|
| [!DNL Google Customer Match] | Google Customer Match lets you use your online and offline data to reach and re-engage with your customers across Google&#39;s owned and operated properties, such as: [!DNL Search], [!DNL Shopping], Gmail, and YouTube. Visit the [!DNL Google Customer Match] [page](/help/rtcdp/destinations/google-customer-match-destination.md) in the destinations catalog for more information about the destination and how to set it up in Adobe Real-time CDP. |

**Neue Funktionen**

| Funktion | Beschreibung |
|------- | -----------|
| Custom file name editor | Update to the data activation workflow for email marketing destinations and cloud storage destinations that allows you to edit the name of the exported files. For more information, refer to the [ Configure step](/help/rtcdp/destinations/activate-destinations.md#configure) in the activation workflow. |
| Empfohlene Attribute | Aktualisieren Sie auf den Arbeitsablauf für die Aktivierung von Daten für E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele, das die empfohlenen Attribute enthält, die Sie den exportierten Dateien hinzufügen können. Weitere Informationen finden Sie im Schritt [Attribute auswählen](/help/rtcdp/destinations/activate-destinations.md#select-attributes) im Arbeitsablauf für die Aktivierung. |

## Quellen {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Flusslaufüberwachung | Users can monitor all flow runs and see a detailed view of each run, including completion status, run duration, list of files processed, errors, and metrics. Weitere Informationen finden Sie im Dokument [zum Überwachen von Datenflüssen](../../sources/tutorials/ui/monitor.md) . |
| Account updating | Users can update the credentials, name, and description of any existing account to provide more meaningful information and correct any errors that may have been created. |
| Flow run notifications | Benutzer können Ereignis abonnieren und Webhooks registrieren, um Echtzeitbenachrichtigungen über Status, Metriken und Fehler bei der Ausführung von Textfluss zu erhalten. |
| Verbesserungen am UI-Katalog | Aktualisierungen des Katalogbildschirms für Quellen, um den Zugriff auf primäre Aktionen ausgewählter Objekte zu erleichtern. |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
