---
title: Adobe Experience Platform – Versionshinweise August 2020
description: Versionshinweise August 2020 für Adobe Experience Platform.
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
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

[!DNL Data Science Workspace] nutzt maschinelles Lernen und künstliche Intelligenz, um Einblicke aus Ihren Daten zu gewinnen. [!DNL Data Science Workspace] ist in Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen auf der Basis Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| VM-Verbesserungen in [!DNL JupyterLab] | Verbesserte Stabilität langlaufender virtueller [!DNL JupyterLab notebook] Maschinen. |

Weitere Informationen zu [!DNL JupyterLab] finden Sie im [[!DNL JupyterLab] Benutzerhandbuch](../../data-science-workspace/jupyterlab/overview.md).

## Ziele {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md) sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner nahtlos aktivieren.

**Neue Ziele**

Es stehen neue Ziele zur Verfügung, für die Sie Ihre Adobe Experience Platform-Daten aktivieren können. Weitere Informationen finden Sie hier:

| Ziel | Beschreibung |
|--- | ---|
| [!DNL Google Customer Match] | Mit Google-Kundenabgleich können Sie Ihre Online- und Offline-Daten verwenden, um Ihre Kunden über die eigenen und betriebenen Eigenschaften von Google zu erreichen und erneut mit ihnen zu interagieren, z. B.: [!DNL Search], [!DNL Shopping], Gmail und YouTube. <br><br> Besuchen Sie die Seite [!DNL Google Customer Match] [Seite](../../destinations/catalog/advertising/google-customer-match.md) im Zielkatalog, um weitere Informationen zum Ziel und dessen Einrichtung in Real-Time CDP zu erhalten. |

**Neue Funktionen**

| Funktion | Beschreibung |
|------- | -----------|
| Benutzerdefinierter Dateinameneditor | Aktualisierung des Workflows zur Datenaktivierung für E-Mail-Marketing-Ziele und Cloud-Speicher-Ziele, mit dem Sie den Namen der exportierten Dateien bearbeiten können. Weitere Informationen finden Sie im Schritt [Konfigurieren](../../destinations/ui/activate-batch-profile-destinations.md) im Aktivierungs-Workflow. |
| Empfohlene Attribute | Aktualisierung des Datenaktivierungs-Workflows für E-Mail-Marketing-Ziele und Cloud-Speicher-Ziele, der die empfohlenen Attribute anzeigt, die Sie zu den exportierten Dateien hinzufügen können. Weitere Informationen finden Sie im Schritt [Attribute auswählen](../../destinations/ui/activate-batch-profile-destinations.md) im Aktivierungs-Workflow. |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Die auf Experience Platform aufbauende Real-Time Customer Data Platform ([!DNL Real-Time CDP]) hilft Unternehmen dabei, bekannte und unbekannte Daten zusammenzuführen, sodass sich während der gesamten Customer Journey Kundenprofile mit intelligenten Entscheidungen aktivieren lassen. [!DNL Real-Time CDP] kombiniert mehrere Unternehmensdatenquellen, um Kundenprofile in Echtzeit zu erstellen. Segmente, die aus diesen Profilen erstellt wurden, können dann an nachgelagerte Ziele gesendet werden, um eine personalisierte Eins-zu-Eins-Kundenerfahrung über alle Kanäle und Geräte hinweg bereitzustellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| IAB TCF 2.0-Unterstützung | [!DNL Real-Time CDP] ist jetzt ein registrierter Anbieter für die 2.0-Version des [!DNL Transparency & Consent Framework] (TCF), wie in der [!DNL Interactive Advertising Bureau] (IAB) beschrieben. Sie können Ihre Datenvorgänge und Profilschemata so konfigurieren, dass von einer CMP generierte Kundenzustimmungsdaten akzeptiert und die Zustimmungseinstellungen Ihrer Kunden bei der Aktivierung von Segmenten für nachgelagerte Ziele durchgesetzt werden. |

Weitere Informationen zu [!DNL Real-Time CDP] finden Sie im [[!DNL Real-Time CDP] Überblick](../../rtcdp/overview.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen und gleichzeitig diese Daten mithilfe von [!DNL Platform] -Diensten strukturieren, beschriften und erweitern. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie auf einfache Weise Quellverbindungen für verschiedene Datenanbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Flusslaufüberwachung | Benutzer können alle Durchsatzausführungen überwachen und eine detaillierte Ansicht der einzelnen Ausführungen anzeigen, einschließlich Abschlussstatus, Ausführungsdauer, Liste der verarbeiteten Dateien, Fehler und Metriken. Weitere Informationen finden Sie im Dokument [Überwachen von Datenflüssen](../../sources/tutorials/ui/monitor.md) . |
| Flusslaufbenachrichtigungen | Benutzer können Ereignisse abonnieren und Webhooks registrieren, um Echtzeit-Benachrichtigungen zu Status, Metriken und Fehlern in Bezug auf Flussergebnisse zu erhalten. |
| Verbesserungen am UI-Katalog | Aktualisierungen des Katalogbildschirms der Quellen, um den Zugriff auf die primären Aktionen ausgewählter Objekte zu erleichtern. |

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
