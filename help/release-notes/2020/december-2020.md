---
title: Adobe Experience Platform - Versionshinweise Dezember 2020
description: Versionshinweise Dezember 2020 für Adobe Experience Platform.
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 28%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 9. Dezember 2020**

Neue Funktionen in Adobe Experience Platform:

- [[!DNL Dataflows]](#dataflows)

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Experience Platform verschieben. Diese Datenflüsse werden über verschiedene Services konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in den Identity Service und Profil-Service sowie in Ziele.

**Wichtigste Funktion**

| Funktion | Beschreibung |
| ------- | ----------- |
| Transparenz für Datenflüsse | Sie können Datenflüsse für Quellen und Ziele überwachen. Weitere Informationen finden Sie im [Tutorial zu Überwachungsquellen](../../dataflows/ui/monitor-sources.md) oder im [Tutorial zur Überwachung von Zielen](../../dataflows/ui/monitor-destinations.md). |

Weitere Informationen zu Datenflüssen finden Sie in der [Datenflüsse - Übersicht](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace nutzt maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. Data Science Workspace ist in Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen auf der Basis Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| --- | ---|
| Adobe Experience Platform Intelligence-Paket-Add-on | Das Adobe Experience Platform Intelligence-Paket-Add-on ist ein Data Science Workspace-Upgrade, das zusätzliche wichtige Funktionen freischaltet, wie z. B.: <li> Benutzeroberflächengesteuertes Experimentieren und Auswerten von Modellen.</li><li> Möglichkeit zur Bereitstellung und Operationalisierung von Modellen mit geplanten Schulungs- und Ableitungsaufträgen.</li><li> Unterstützung für Deep Learning in TensorFlow-Modellen (GPU Compute).</li><li> Spark-basierte verteilte Datenverarbeitung zum Trainieren und Bewerten großer Datensätze (10 MM + Zeilen).</li><li>Und mehr</li> |

Weitere Informationen zum Adobe Experience Platform Intelligence-Paket-Add-on finden Sie in der Dokumentation unter [Zugriff auf und Funktionen von Data Science Workspace](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kann Daten aus externen Quellen aufnehmen und ermöglicht es Ihnen gleichzeitig, diese Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie auf einfache Weise Quellverbindungen für verschiedene Datenanbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Konto- und Verbindungsdetails für Streaming-Quellen aktualisieren | Sie können jetzt die Namen, Beschreibungen und Anmeldeinformationen vorhandener Streaming-Verbindungen mithilfe der [!DNL Flow Service]-API und der Benutzeroberfläche aktualisieren. Weitere Informationen finden Sie im Tutorial zum [Aktualisieren von Verbindungen mithilfe der API](../../sources/tutorials/api/update.md) und [Bearbeiten von Kontodetails mithilfe der Benutzeroberfläche](../../sources/tutorials/ui/monitor.md). |
| Löschen von Datenflüssen | Streaming-Datenflüsse, die Fehler enthalten oder unnötig geworden sind, können jetzt über die [!DNL Flow Service]-API und die Benutzeroberfläche gelöscht werden. Weitere Informationen finden Sie im Tutorial [Löschen von Datenflüssen mithilfe der API](../../sources/tutorials/api/delete-dataflows.md) und [Löschen von Datenflüssen mithilfe der Benutzeroberfläche](../../sources/tutorials/ui/delete.md). |

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
