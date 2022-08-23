---
title: Adobe Experience Platform - Versionshinweise, August 2022
description: Die Versionshinweise für Adobe Experience Platform vom August 2022.
source-git-commit: 2a507b4fe5b7c9dc523ceb5b2f39becf9e574ed9
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 49%

---

# Adobe Experience Platform – Versionshinweise

**Release-Datum: 24. August 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Datenvorbereitung](#data-prep)
- [Quellen](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für die Aufnahme von Datensätzen mit Warnungen | Die Datenvorbereitung lokalisiert nun Warnungen (nicht kritische Fehler) in die Felder und ermöglicht die Erfassung des restlichen Teils der Zeile. Alle Mapper-Transformationsfehler werden jetzt als Warnungen und teilweise aufgenommene Zeilen als erfolgreich gemeldet, mit einer Warnung.  Die Überwachung wird auch für Datensätze mit Warnungen und Diagnosedetails unterstützt. Die partielle Erfassung von Datensätzen mit Warnungen ist derzeit nur für Streaming-Daten verfügbar. Lesen Sie die Dokumentation unter [Erfassen von Datensätzen mit Warnungen](../../sources/tutorials/ui/monitor-streaming.md) für weitere Informationen. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen über [!DNL Data Prep] finden Sie in der [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Regionsübergreifende Unterstützung für Adobe Analytics-Quellen | Sie können jetzt Report Suites aus einer beliebigen Region (USA, Großbritannien oder Singapur) erfassen. Report Suites müssen derselben Organisation wie die Experience Platform-Sandbox-Instanz zugeordnet sein, in der die Quellverbindung erstellt wird. Weitere Informationen finden Sie im Handbuch unter [Erstellen einer Adobe Analytics-Quellverbindung in der Benutzeroberfläche](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
