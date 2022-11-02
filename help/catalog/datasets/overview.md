---
keywords: Experience Platform; Startseite; beliebte Themen; Datenspeicherort; Datenspeicherort; Datenmanagement; Datenverwaltung; Lineage; Herkunft; Datentyp; Datentypen; Datentypen; Datentyp
solution: Experience Platform
title: Datensätze - Übersicht
topic-legacy: datasets
description: Dieses Dokument bietet einen umfassenden Überblick über Datensätze in Experience Platform.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: 02002c9530074b8b05664ff9eab5bc2fe4b7d5d4
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 16%

---

# Datensätze – Übersicht

Alle Daten, die erfolgreich in Adobe Experience Platform aufgenommen wurden, bleiben im [!DNL Data Lake] als Datensätze. Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, in dem Daten (in der Regel) in einer Tabelle erfasst werden, die ein Schema (Spalten) und Felder (Zeilen) beinhaltet. Datensätze enthalten auch Metadaten, die verschiedene Aspekte der in ihnen gespeicherten Daten beschreiben.

Dieses Dokument bietet einen umfassenden Überblick über Datensätze in [!DNL Experience Platform].

## Erstellen von Datensätzen und Tracking-Metadaten

[!DNL Catalog Service] ist das Aufzeichnungssystem für Speicherort und Herkunft von Daten in [!DNL Experience Platform]und wird zum Erstellen und Verwalten von Datensätzen verwendet. [!DNL Catalog] verfolgt die Metadaten für jeden Datensatz, der einen Verweis auf die [!DNL Experience Data Model] (XDM) Schema, dem der Datensatz entspricht (im nächsten Abschnitt erläutert), und der Anzahl der in diesen Datensatz erfassten Datensätze.

Siehe [Catalog Service - Übersicht](../home.md) für weitere Informationen.

## Einschränkungen für Datensatzdaten erzwingen

[!DNL Experience Data Model] (XDM) ist das standardisierte Framework, mit dem [!DNL Platform] organisiert Kundenerlebnisdaten. Alle Daten, die erfasst werden [!DNL Platform] muss einem vordefinierten XDM-Schema entsprechen, bevor es im [!DNL Data Lake] als Datensatz.

Alle Datensätze enthalten einen Verweis auf das XDM-Schema, der das Format und die Struktur der Daten einschränkt, die sie speichern können. Der Versuch, Daten in einen Datensatz hochzuladen, der nicht dem XDM-Schema des Datensatzes entspricht, führt dazu, dass die Aufnahme fehlschlägt.

Weitere Informationen zu XDM finden Sie unter [XDM-System - Übersicht](../../xdm/home.md).

## Erfassen von Daten in Datensätzen

Die Adobe Experience Platform-Datenerfassung stellt mehrere Methoden dar, mit denen [!DNL Platform] erfasst Daten aus verschiedenen Quellen. Unabhängig von der Erfassungsmethode werden alle erfolgreich erfassten Daten in Batch-Dateien konvertiert. Batches sind Dateneinheiten aus einer oder mehreren Dateien, die als Ganzes aufgenommen werden. Diese Batch-Dateien werden dann zu dedizierten Datensätzen hinzugefügt und bleiben im [!DNL Data Lake].

Siehe [Datenerfassung - Übersicht](../../ingestion/home.md) für weitere Informationen.

## Anwenden von Nutzungsbezeichnungen auf Datensätze

Mit Adobe Experience Platform Data Governance können Sie Kundendaten verwalten, um die Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datennutzung sicherzustellen. Mit dem Data Governance-Framework können Sie Nutzungsbezeichnungen anwenden, um Daten entsprechend den für diese Daten geltenden Nutzungsrichtlinien zu kategorisieren.

Datennutzungsbezeichnungen können auf komplette Datensätze oder einzelne Datensatzfelder angewendet werden. Auf Datensatzebene hinzugefügte Bezeichnungen werden von allen Feldern in diesem Datensatz übernommen.

Weitere Informationen zu dem Service finden Sie in der [Übersicht zu Data Governance. ](../../data-governance/home.md) Anweisungen zum Arbeiten mit Nutzungsbezeichnungen finden Sie unter [!DNL Platform], siehe die folgenden Handbücher:

* [Verwalten von Kennzeichnungen in der Benutzeroberfläche](../../data-governance/labels/user-guide.md)
* [Verwalten der Datensatzbezeichnungen in der API](../../data-governance/labels/dataset-api.md)

## Datensätze in nachgelagerten Bereichen [!DNL Platform] Dienstleistungen

Sobald Datensätze zum Speichern erfasster Daten verwendet wurden, werden diese Datensätze von nachgelagerten Datensätzen verwendet [!DNL Platform] -Services, um Kundenprofile zu aktualisieren, Einblicke durch maschinelles Lernen zu gewinnen und vieles mehr.

Im Folgenden finden Sie eine Liste der nachgelagerten Dienste, die Datensätze für verschiedene Vorgänge verwenden. Weitere Informationen finden Sie in der Dokumentation für jeden Dienst.

* [[!DNL Data Access API]](../../data-access/home.md): Ermöglicht den Zugriff auf und den Download des Inhalts von Dateien, die in Datensätzen gespeichert sind.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Führt Identitäten zwischen Geräten und Systemen zusammen und verknüpft Datensätze anhand der Identitätsfelder, die von den entsprechenden XDM-Schemas definiert werden.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Nutzung [!DNL Identity Service] , um aus Ihren Datensätzen in Echtzeit detaillierte Kundenprofile zu erstellen. [!DNL Real-time Customer Profile] ruft Daten aus der [!DNL Data Lake] und speichert Kundenprofile in einem eigenen separaten Datenspeicher.
* [Adobe Experience Platform-Segmentierungsdienst](../../segmentation/home.md): Ermöglicht Ihnen das Erstellen von Segmenten und das Generieren von Zielgruppen aus Ihrer [!DNL Real-time Customer Profile] Daten. Diese Zielgruppen können dann in ihre eigenen Datensätze innerhalb der [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Verwendet maschinelles Lernen und künstliche Intelligenz, um Einblicke in große Datensätze zu erhalten.
* [Adobe Experience Platform Query Service](../../query-service/home.md): Ermöglicht die Verwendung von SQL zur Abfrage von Daten in [!DNL Experience Platform], indem Sie beliebige Datensätze innerhalb der [!DNL Data Lake] und Erfassen von Abfrageergebnissen als neuen Datensatz zur Verwendung in Berichten, [!DNL Data Science Workspace]oder [!DNL Real-time Customer Profile].
* [Adobe Experience Platform Destinations-Dienst](../../destinations/home.md): Ermöglicht Ihnen Folgendes: [Datensätze exportieren](/help/destinations/ui/export-datasets.md) für Ihre gewünschten Cloud-Speicher- oder E-Mail-Marketing-Ziele, für Reporting- oder Datenwissenschaftsaktivitäten.

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie sich mit den wichtigsten Verwendungen von Datensätzen in [!DNL Experience Platform]sowie die verschiedenen [!DNL Platform] Dienste, die Datensätze verwenden. Weitere Informationen zu den zahlreichen Verwendungsmöglichkeiten von Datensätzen finden Sie unter [!DNL Platform], lesen Sie bitte die Dienstdokumentation in dieser Übersicht.

Anweisungen zur Interaktion mit Datensätzen in der [!DNL Experience Platform] Benutzeroberfläche, siehe [Benutzerhandbuch zu Datensätzen](user-guide.md).
