---
title: Adobe Experience Platform – Versionshinweise
description: Experience Platform release notes August 10, 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: c64d4cc01b5125fad5f7c75914dfc1e4b20bc069
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 33%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: 12. August 2020**

Updates to existing features in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL-Quellen]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] nutzt maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu entfesseln. Integrated into Adobe Experience Platform, [!DNL Data Science Workspace] helps you make predictions using your content and data assets across Adobe solutions.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| VM improvements in [!DNL JupyterLab] | Verbesserte Stabilität langlaufender [!DNL JupyterLab notebook] virtueller Maschinen. |

Weitere Informationen zu [!DNL JupyterLab]finden Sie im [[!DNL JupyterLab] Benutzerhandbuch](../../data-science-workspace/jupyterlab/overview.md).

## Quellen {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Flusslaufüberwachung | Die Benutzer können alle Flussläufe überwachen und eine detaillierte Ansicht der einzelnen Vorgänge anzeigen, einschließlich Abschlussstatus, Laufzeit, Liste der verarbeiteten Dateien, Fehler und Metriken. See the [monitoring dataflows](../../sources/tutorials/ui/monitor.md) document for more information. |
| Kontoaktualisierung | Benutzer können die Anmeldeinformationen, den Namen und die Beschreibung eines vorhandenen Kontos aktualisieren, um aussagekräftigere Informationen bereitzustellen und ggf. erstellte Fehler zu berichtigen. |
| Flusslaufbenachrichtigungen | Benutzer können Ereignis abonnieren und Webhooks registrieren, um Echtzeitbenachrichtigungen über Status, Metriken und Fehler bei der Ausführung von Textfluss zu erhalten. |
| UI catalog improvements | Aktualisierungen des Katalogbildschirms für Quellen, um den Zugriff auf primäre Aktionen ausgewählter Objekte zu erleichtern. |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
