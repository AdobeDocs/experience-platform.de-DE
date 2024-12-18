---
title: Adobe Experience Platform - Versionshinweise, Dezember 2020
description: Die Versionshinweise für Adobe Experience Platform vom Dezember 2020.
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 31%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 9. Dezember 2020**

Neue Funktionen in Adobe Experience Platform:

- [[!DNL Dataflows]](#dataflows)

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Platform verschieben. Diese Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und ermöglichen so das Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in den Identitäts- und Profildienst und in Ziele.

**Schlüsselfunktion**

| Funktion | Beschreibung |
| ------- | ----------- |
| Transparenz für Datenflüsse | Sie können Datenflüsse auf Quellen und Ziele überwachen. Weitere Informationen finden Sie im [Tutorial zu Überwachungsquellen](../../dataflows/ui/monitor-sources.md) oder im [Tutorial zum Überwachen von Zielen](../../dataflows/ui/monitor-destinations.md). |

Weitere Informationen zu Datenflüssen finden Sie in der [Übersicht über Datenflüsse](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace nutzt maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. Data Science Workspace ist in Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen auf der Basis Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| --- | ---|
| Adobe Experience Platform Intelligence Package-Add-on | Das Adobe Experience Platform Intelligence-Package-Add-on ist ein Data Science Workspace-Upgrade, das zusätzliche wichtige Funktionen wie z. B. Folgendes freischaltet: <li> Experimentieren und Auswerten benutzeroberflächengesteuerter Modelle.</li><li> Möglichkeit zur Bereitstellung und Inbetriebnahme von Modellen mit geplanten Schulungs- und Unterrichtsvorgängen.</li><li> Unterstützung für tiefes Lernen in TensorFlow-Modellen (GPU Compute).</li><li> Spark-basierte verteilte Berechnung, um mit großen Datensätzen (10MM + Zeilen) zu trainieren und zu bewerten.</li><li>Und mehr</li> |

Weitere Informationen zum Adobe Experience Platform Intelligence-Paket-Add-on finden Sie in der Dokumentation zu [Zugriff und Funktionen von Data Science Workspace](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen und gleichzeitig diese Daten mithilfe von [!DNL Platform] -Diensten strukturieren, beschriften und erweitern. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie auf einfache Weise Quellverbindungen für verschiedene Datenanbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Aktualisieren von Konto- und Verbindungsdetails für Streaming-Quellen | Sie können jetzt die Namen, Beschreibungen und Anmeldeinformationen vorhandener Streaming-Verbindungen mithilfe der [!DNL Flow Service] -API und der Benutzeroberfläche aktualisieren. Weitere Informationen finden Sie im Tutorial zum Aktualisieren von Verbindungen mithilfe der API](../../sources/tutorials/api/update.md) und zum Bearbeiten von Kontodetails mithilfe der Benutzeroberfläche ](../../sources/tutorials/ui/monitor.md).[[ |
| Löschen von Datenflüssen | Streaming-Datenflüsse, die Fehler enthalten oder unnötig geworden sind, können jetzt mit der [!DNL Flow Service] -API und der Benutzeroberfläche gelöscht werden. Weitere Informationen finden Sie im Tutorial zum [Löschen von Datenflüssen mithilfe der API](../../sources/tutorials/api/delete-dataflows.md) und [ Löschen von Datenflüssen mithilfe der Benutzeroberfläche](../../sources/tutorials/ui/delete.md). |

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
