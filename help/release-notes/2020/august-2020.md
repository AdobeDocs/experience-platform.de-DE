---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform 10. August 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 33%

---

# Adobe Experience Platform – Versionshinweise

**Release-Datum: 12. August 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] nutzt maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. [!DNL Data Science Workspace] ist in Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen auf der Basis Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| VM-Verbesserungen in [!DNL JupyterLab] | Verbesserte Stabilität langlaufender [!DNL JupyterLab notebook] virtueller Maschinen. |

Weitere Informationen zu [!DNL JupyterLab] finden Sie im [[!DNL JupyterLab] Benutzerhandbuch](../../data-science-workspace/jupyterlab/overview.md).

## Ziele {#destinations}

In der [ Echtzeit-Kundendatenplattform](../../rtcdp/overview.md) sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner auf nahtlose Weise aktivieren.

**Neue Ziele**

Es stehen neue Ziele zur Verfügung, für die Sie Ihre Adobe Experience Platform-Daten aktivieren können. Weitere Informationen finden Sie hier:

| Ziel | Beschreibung |
|--- | ---|
| [!DNL Google Customer Match] | Mit Google Customer Match können Sie Ihre Online- und Offline-Daten verwenden, um Ihre Kunden über die eigenen und betriebenen Eigenschaften von Google zu erreichen und erneut mit ihnen zu interagieren, z. B.: [!DNL Search], [!DNL Shopping], Gmail und YouTube. <br><br> Weitere Informationen zum Ziel und dessen Einrichtung in der Echtzeit-Kundendatenplattform finden Sie auf der  [!DNL Google Customer Match] [](../../destinations/catalog/advertising/google-customer-match.md) Seite im Zielkatalog . |

**Neue Funktionen**

| Funktion | Beschreibung |
|------- | -----------|
| Benutzerdefinierter Dateinameneditor | Aktualisierung des Workflows zur Datenaktivierung für E-Mail-Marketing-Ziele und Cloud-Speicher-Ziele, mit dem Sie den Namen der exportierten Dateien bearbeiten können. Weitere Informationen finden Sie im Schritt [ Konfigurieren](../../destinations/ui/activate-batch-profile-destinations.md) im Aktivierungs-Workflow. |
| Empfohlene Attribute | Aktualisierung des Datenaktivierungs-Workflows für E-Mail-Marketing-Ziele und Cloud-Speicher-Ziele, der die empfohlenen Attribute anzeigt, die Sie zu den exportierten Dateien hinzufügen können. Weitere Informationen finden Sie im Schritt [Attribute auswählen](../../destinations/ui/activate-batch-profile-destinations.md) im Aktivierungs-Workflow. |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Real-time Customer Data Platform ([!DNL Real-time CDP]) basiert auf Experience Platform und hilft Unternehmen dabei, bekannte und unbekannte Daten zusammenzuführen, um Kundenprofile durch intelligente Entscheidungen auf der gesamten Journey zu aktivieren. [!DNL Real-time CDP] kombiniert mehrere Unternehmensdatenquellen, um Kundenprofile in Echtzeit zu erstellen. Segmente, die aus diesen Profilen erstellt wurden, können dann an nachgelagerte Ziele gesendet werden, um eine Eins-zu-Eins-Kundenerfahrung über alle Kanäle und Geräte hinweg bereitzustellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| IAB TCF 2.0-Unterstützung | [!DNL Real-time CDP] ist jetzt ein registrierter Anbieter für die 2.0-Version des  [!DNL Transparency & Consent Framework] (TCF), wie im  [!DNL Interactive Advertising Bureau] (IAB) beschrieben. Sie können Ihre Datenvorgänge und Profilschemata so konfigurieren, dass von einer CMP generierte Kundenzustimmungsdaten akzeptiert und die Zustimmungseinstellungen Ihrer Kunden bei der Aktivierung von Segmenten für nachgelagerte Ziele durchgesetzt werden. |

Weitere Informationen zu [!DNL Real-time CDP] finden Sie in der [[!DNL Real-time CDP] Übersicht](../../rtcdp/overview.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen und gleichzeitig diese Daten mithilfe von [!DNL Platform]-Diensten strukturieren, beschriften und erweitern. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Flusslaufüberwachung | Benutzer können alle Durchsatzausführungen überwachen und eine detaillierte Ansicht der einzelnen Ausführungen anzeigen, einschließlich Abschlussstatus, Ausführungsdauer, Liste der verarbeiteten Dateien, Fehler und Metriken. Weitere Informationen finden Sie im Dokument [Überwachen von Datenflüssen](../../sources/tutorials/ui/monitor.md) . |
| Flusslaufbenachrichtigungen | Benutzer können Ereignisse abonnieren und Webhooks registrieren, um Echtzeit-Benachrichtigungen zu Status, Metriken und Fehlern in Bezug auf Flussergebnisse zu erhalten. |
| Verbesserungen am UI-Katalog | Aktualisierungen des Katalogbildschirms der Quellen, um den Zugriff auf die primären Aktionen ausgewählter Objekte zu erleichtern. |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
