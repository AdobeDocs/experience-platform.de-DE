---
title: Adobe Experience Platform – Versionshinweise August 2020
description: Versionshinweise August 2020 für Adobe Experience Platform.
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 38%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: Donnerstag, 12. August 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] nutzt maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. [!DNL Data Science Workspace] ist in Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen auf der Basis Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| VM-Verbesserungen in [!DNL JupyterLab] | Die Stabilität von virtuellen Maschinen mit langer Laufzeit [!DNL JupyterLab notebook] wurde verbessert. |

Weitere Informationen zu [!DNL JupyterLab] finden Sie im [[!DNL JupyterLab] Benutzerhandbuch](../../data-science-workspace/jupyterlab/overview.md).

## Ziele {#destinations}

In [Real-Time Customer Data Platform](../../rtcdp/overview.md) sind Ziele vorgefertigte Integrationen mit Zielplattformen, die Daten nahtlos für diese Partner aktivieren.

**Neue Ziele**

Es stehen neue Ziele zur Verfügung, für die Sie Ihre Adobe Experience Platform-Daten aktivieren können. Weitere Informationen finden Sie hier:

| Ziel | Beschreibung |
|--- | ---|
| [!DNL Google Customer Match] | Mit Google Customer Match können Sie Ihre Online- und Offline-Daten verwenden, um Ihre Kunden über die von Google verwalteten und betriebenen Eigenschaften wie [!DNL Search], [!DNL Shopping], Gmail und YouTube zu erreichen und erneut mit ihnen zu interagieren. <br><br> Besuchen Sie die [!DNL Google Customer Match] [Seite](../../destinations/catalog/advertising/google-customer-match.md) im Zielkatalog, um weitere Informationen über das Ziel und dessen Einrichtung in Real-Time CDP zu erhalten. |

**Neue Funktionen**

| Funktion | Beschreibung |
|------- | -----------|
| Editor für benutzerdefinierte Dateinamen | Aktualisierung des Datenaktivierungs-Workflows für E-Mail-Marketing- und Cloud-Speicher-Ziele, mit dem Sie den Namen der exportierten Dateien bearbeiten können. Weitere Informationen finden Sie im [ „Konfigurieren](../../destinations/ui/activate-batch-profile-destinations.md) im Aktivierungs-Workflow. |
| Empfohlene Attribute | Aktualisierung des Datenaktivierungs-Workflows für E-Mail-Marketing- und Cloud-Speicher-Ziele, der empfohlene Attribute anzeigt, die Sie den exportierten Dateien hinzufügen können. Weitere Informationen finden Sie im Schritt [Auswählen von Attributen](../../destinations/ui/activate-batch-profile-destinations.md) im Aktivierungs-Workflow. |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Die auf Experience Platform aufbauende Real-Time Customer Data Platform ([!DNL Real-Time CDP]) hilft Unternehmen dabei, bekannte und unbekannte Daten zusammenzuführen, sodass sich während der gesamten Customer Journey Kundenprofile mit intelligenten Entscheidungen aktivieren lassen. [!DNL Real-Time CDP] kombiniert mehrere Unternehmensdatenquellen, um Kundenprofile in Echtzeit zu erstellen. Segmente, die aus diesen Profilen erstellt wurden, können dann an nachgelagerte Ziele gesendet werden, um eine personalisierte Eins-zu-Eins-Kundenerfahrung über alle Kanäle und Geräte hinweg bereitzustellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| IAB TCF 2.0-Unterstützung | [!DNL Real-Time CDP] ist jetzt ein registrierter Anbieter für die Version 2.0 des [!DNL Transparency & Consent Framework] (TCF), wie vom [!DNL Interactive Advertising Bureau] (IAB) beschrieben. Sie können Ihre Datenvorgänge und Profilschemata so konfigurieren, dass sie von einer CMP generierte Kundeneinverständnisdaten akzeptieren, und die Einverständnisvoreinstellungen Ihrer Kunden durchsetzen, wenn Sie Segmente für nachgelagerte Ziele aktivieren. |

Weitere Informationen zu [!DNL Real-Time CDP] finden Sie im [[!DNL Real-Time CDP] Überblick](../../rtcdp/overview.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen aufnehmen und ermöglicht es Ihnen gleichzeitig, diese Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie auf einfache Weise Quellverbindungen für verschiedene Datenanbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Überwachung des Flussdurchgangs | Benutzer können alle Flussausführungen überwachen und eine detaillierte Ansicht jeder Ausführung anzeigen, einschließlich Abschlussstatus, Ausführungsdauer, Liste der verarbeiteten Dateien, Fehler und Metriken. Weitere Informationen finden [ im Dokument ](../../sources/tutorials/ui/monitor.md)Überwachen von Datenflüssen“. |
| Flusslaufbenachrichtigungen | Benutzer können Ereignisse abonnieren und Webhooks registrieren, um Echtzeitbenachrichtigungen über Status, Metriken und Fehler bei Flussausführungen zu erhalten. |
| Verbesserungen am UI-Katalog | Der Quellkatalogbildschirm wurde aktualisiert, um den Zugriff auf primäre Aktionen ausgewählter Objekte zu erleichtern. |

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
