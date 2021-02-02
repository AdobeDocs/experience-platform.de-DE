---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform, 10. August 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 49c984a60fd699706eec508ec1d786340df40b57
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 28%

---


# Adobe Experience Platform – Versionshinweise

**Release-Datum: 12. August 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] nutzt maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu entfesseln. In Adobe Experience Platform integriert hilft [!DNL Data Science Workspace] Ihnen bei der Erstellung von Prognosen mit Ihren Inhalten und Daten-Assets in allen Adoben.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| VM-Verbesserungen in [!DNL JupyterLab] | Verbesserte Stabilität von langlebigen [!DNL JupyterLab notebook] virtuellen Maschinen. |

Weitere Informationen zu [!DNL JupyterLab] finden Sie im [[!DNL JupyterLab] Benutzerhandbuch](../../data-science-workspace/jupyterlab/overview.md).

## Ziele {#destinations}

In der [ Echtzeit-Kundendatenplattform](../../rtcdp/overview.md) sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner auf nahtlose Weise aktivieren.

**Neue Ziele**

Es stehen neue Ziele zur Verfügung, für die Sie Ihre Adobe Experience Platform-Daten aktivieren können. Weitere Informationen finden Sie hier:

| Ziel | Beschreibung |
|--- | ---|
| [!DNL Google Customer Match] | Mit Google Customer Match können Sie Ihre Online- und Offlinedaten verwenden, um Ihre Kunden über die eigenen und betriebenen Eigenschaften von Google zu erreichen und erneut zu kontaktieren, z. B.: [!DNL Search], [!DNL Shopping], Gmail und YouTube. <br><br> Weitere Informationen zum Ziel und zur Einrichtung in Echtzeit-CDP finden Sie auf der  [!DNL Google Customer Match] [](../../destinations/catalog/advertising/google-customer-match.md) Seite im Zielkatalog. |

**Neue Funktionen**

| Funktion | Beschreibung |
|------- | -----------|
| Benutzerdefinierter Dateinameneditor | Aktualisieren Sie auf den Arbeitsablauf für die Aktivierung von Daten für E-Mail-Marketing-Ziele und Cloud-Datenspeicherung, damit Sie den Dateinamen der exportierten Dateien bearbeiten können. Weitere Informationen finden Sie im Arbeitsablauf für die Aktivierung unter [ Konfigurieren .](../../destinations/ui/activate-destinations.md#configure) |
| Empfohlene Attribute | Aktualisieren Sie auf den Arbeitsablauf für die Aktivierung von Daten für E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele, das die empfohlenen Attribute enthält, die Sie den exportierten Dateien hinzufügen können. Weitere Informationen finden Sie im Schritt [Attribute auswählen](../../destinations/ui/activate-destinations.md#select-attributes) im Arbeitsablauf für die Aktivierung. |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Die auf Experience Platform aufbauende Echtzeit-Kundendatenplattform ([!DNL Real-time CDP]) hilft Firmen dabei, bekannte und unbekannte Daten zusammenzuführen, um Kundendaten mit einer intelligenten Entscheidungsfindung im gesamten Journey zu aktivieren. [!DNL Real-time CDP] kombiniert mehrere Unternehmensdatenquellen, um Kundendaten in Echtzeit zu erstellen. Segmente, die aus diesen Profilen erstellt wurden, können dann an nachgelagerte Ziele gesendet werden, um eine persönliche Kundenerfahrung über alle Kanal und Geräte hinweg zu bieten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| IAB TCF 2.0-Unterstützung | [!DNL Real-time CDP] ist jetzt ein registrierter Anbieter für die 2.0-Version des  [!DNL Transparency & Consent Framework] (TCF), wie im  [!DNL Interactive Advertising Bureau] (IAB) beschrieben. Sie können Ihre Datenvorgänge und Profil-Schema so konfigurieren, dass sie von einem CMP generierte Daten zur Kundengenehmigung akzeptieren und die Voreinstellungen Ihrer Kunden für die Zustimmung bei der Aktivierung von Segmenten an nachgelagerte Ziele durchsetzen. |

Weitere Informationen zu [!DNL Real-time CDP] finden Sie unter [[!DNL Real-time CDP] overview](../../rtcdp/overview.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen, während Sie diese Daten mithilfe der [!DNL Platform]-Dienste strukturieren, beschriften und erweitern können. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Flusslaufüberwachung | Die Benutzer können alle Flussläufe überwachen und eine detaillierte Ansicht der einzelnen Vorgänge anzeigen, einschließlich Abschlussstatus, Laufzeit, Liste der verarbeiteten Dateien, Fehler und Metriken. Weitere Informationen finden Sie im Dokument [Datenflüsse überwachen](../../sources/tutorials/ui/monitor.md). |
| Flusslaufbenachrichtigungen | Benutzer können Ereignis abonnieren und Webhooks registrieren, um Echtzeitbenachrichtigungen über Status, Metriken und Fehler bei der Ausführung von Textfluss zu erhalten. |
| Verbesserungen am UI-Katalog | Aktualisierungen des Katalogbildschirms für Quellen, um den Zugriff auf primäre Aktionen ausgewählter Objekte zu erleichtern. |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).