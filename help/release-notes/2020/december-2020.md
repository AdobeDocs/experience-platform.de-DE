---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise für Experience Platform vom 9. Dezember 2020
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
translation-type: tm+mt
source-git-commit: ae353e6dda3f92647c32ee8e731be5785d24e5cb
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 33%

---


# Adobe Experience Platform – Versionshinweise

**Release-Datum: Mittwoch, 9. Dezember 2020**

Neue Funktionen in Adobe Experience Platform:

- [[!DNL Dataflows]](#dataflows)

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

Datenflüsse sind eine Darstellung von Datenaufträgen, die Daten über die Plattform verschieben. Diese Datenflüsse werden über verschiedene Dienste konfiguriert und unterstützen Sie beim Verschieben von Daten von den Quellschnittstellen zu den Zielgruppen-Datensätzen, zum Identitäts- und Profil-Dienst und zu Zielen.

**Wichtigste Funktion**

| Funktion | Beschreibung |
| ------- | ----------- |
| Transparenz für Datenflüsse | Sie können Datenflüsse auf Quellen und Ziele überwachen. Weitere Informationen finden Sie im [Tutorial zu Überwachungsquellen](../../dataflows/ui/monitor-sources.md) oder im [Tutorial zu Überwachungszielen](../../dataflows/ui/monitor-destinations.md). |

Weitere Informationen zu Datenflüssen finden Sie in der Übersicht über die [Datenflüsse](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace verwendet maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. Data Science Workspace ist in Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen auf der Basis Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| --- | ---|
| Adobe Experience Platform Intelligence-Paket-Addon | Das Adobe Experience Platform Intelligence-Paket-Addon ist ein Data Science Workspace-Upgrade, mit dem zusätzliche wichtige Funktionen wie die folgenden entdeckt werden: <li> Experimentieren und Testen von benutzeroberflächengesteuerten Modellen</li><li> Möglichkeit zur Bereitstellung und Inbetriebnahme von Modellen mit geplanten Schulungen und Unterrichtsaufträgen.</li><li> Unterstützung für tiefes Lernen in Tensorflow-Modellen (GPU Compute).</li><li> Spark-basierte verteilte Berechnung zur Schulung und Bewertung mit großen Datensätzen (10MM + Zeilen).</li><li>Und mehr</li> |

Weitere Informationen zum Adobe Experience Platform Intelligence-Paket finden Sie in der Dokumentation zum Zugriff auf den [Data Science Workspace und seinen Funktionen](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Konto- und Verbindungsdetails für Streaming-Quellen aktualisieren | Sie können nun die Namen, Beschreibungen und Anmeldeinformationen der vorhandenen Streaming-Verbindungen mithilfe der [!DNL Flow Service] API und der Benutzeroberfläche aktualisieren. Weitere Informationen finden Sie im Lernprogramm zum [Aktualisieren von Verbindungen mithilfe der API](../../sources/tutorials/api/update.md) und zum [Bearbeiten von Kontodetails mithilfe der Benutzeroberfläche](../../sources/tutorials/ui/monitor.md). |
| Datenflüsse löschen | Streaming-Datenflüsse, die Fehler enthalten oder unnötig geworden sind, können jetzt mit der [!DNL Flow Service] API und der Benutzeroberfläche gelöscht werden. Weitere Informationen finden Sie im Lernprogramm zum [Löschen von Datenflüssen mithilfe der API](../../sources/tutorials/api/delete-dataflows.md) und zum [Löschen von Datenflüssen mithilfe der Benutzeroberfläche](../../sources/tutorials/ui/delete.md). |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).


