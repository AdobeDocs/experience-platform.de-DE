---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise für Experience Platform vom 9. Dezember 2020
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
translation-type: tm+mt
source-git-commit: 908b9e6e8b548dea8e39f9f9a5de396d4c9520f4
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 38%

---


# Adobe Experience Platform – Versionshinweise

**Release-Datum: Mittwoch, 9. Dezember 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace verwendet maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. Data Science Workspace ist in Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen auf der Basis Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen.

### Wichtigste Funktionen

| Funktion | Beschreibung |
|--- | ---|
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


