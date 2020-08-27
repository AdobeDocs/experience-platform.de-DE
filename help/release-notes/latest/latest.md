---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform, 10. August 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 32%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: 12. August 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL-Ziele]](#destinations)
- [[!DNL-Quellen]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] nutzt maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu entfesseln. Integrated into Adobe Experience Platform, [!DNL Data Science Workspace] helps you make predictions using your content and data assets across Adobe solutions.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| VM-Verbesserungen in [!DNL JupyterLab] | Verbesserte Stabilität langlaufender [!DNL JupyterLab notebook] virtueller Maschinen. |

Weitere Informationen zu [!DNL JupyterLab]finden Sie im [[!DNL JupyterLab] Benutzerhandbuch](../../data-science-workspace/jupyterlab/overview.md).

## Ziele {#destinations}

In der [Adobe Echtzeit-Kundendatenplattform](../../rtcdp/overview.md) sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner auf nahtlose Weise aktivieren.

**Neue Ziele**

Es stehen neue Ziele zur Verfügung, für die Sie Ihre Adobe Experience Platform-Daten aktivieren können. Weitere Informationen finden Sie hier:

| Ziel | Beschreibung |
|--- | ---|
| [!DNL Google Customer Match] | Mit Google Customer Match können Sie Ihre Online- und Offlinedaten verwenden, um Ihre Kunden über die eigenen und betriebenen Eigenschaften von Google zu erreichen und erneut zu kontaktieren, z. B.: [!DNL Search], [!DNL Shopping]Gmail und YouTube. <br><br> Auf der [!DNL Google Customer Match] Seite [](/help/rtcdp/destinations/google-customer-match-destination.md) im Zielkatalog finden Sie weitere Informationen zum Ziel und zur Einrichtung in Adobe Echtzeit-CDP. |

**Neue Funktionen**

| Funktion | Beschreibung |
|------- | -----------|
| Benutzerdefinierter Dateinameneditor | Aktualisieren Sie auf den Arbeitsablauf für die Aktivierung von Daten für E-Mail-Marketing-Ziele und Cloud-Datenspeicherung, damit Sie den Dateinamen der exportierten Dateien bearbeiten können. Weitere Informationen finden Sie im Schritt [ &quot;](/help/rtcdp/destinations/activate-destinations.md#configure) Konfigurieren&quot;im Arbeitsablauf für die Aktivierung. |
| Empfohlene Attribute | Aktualisieren Sie auf den Arbeitsablauf für die Aktivierung von Daten für E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele, das die empfohlenen Attribute enthält, die Sie den exportierten Dateien hinzufügen können. Weitere Informationen finden Sie im Schritt [Attribute auswählen](/help/rtcdp/destinations/activate-destinations.md#select-attributes) im Arbeitsablauf für die Aktivierung. |

## Quellen {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Flusslaufüberwachung | Die Benutzer können alle Flussläufe überwachen und eine detaillierte Ansicht der einzelnen Vorgänge anzeigen, einschließlich Abschlussstatus, Laufzeit, Liste der verarbeiteten Dateien, Fehler und Metriken. Weitere Informationen finden Sie im Dokument [zum Überwachen von Datenflüssen](../../sources/tutorials/ui/monitor.md) . |
| Flusslaufbenachrichtigungen | Benutzer können Ereignis abonnieren und Webhooks registrieren, um Echtzeitbenachrichtigungen über Status, Metriken und Fehler bei der Ausführung von Textfluss zu erhalten. |
| Verbesserungen am UI-Katalog | Aktualisierungen des Katalogbildschirms für Quellen, um den Zugriff auf primäre Aktionen ausgewählter Objekte zu erleichtern. |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
