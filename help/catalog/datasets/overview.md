---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datensätze – Übersicht
topic: datasets
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 3%

---


# Datensätze – Übersicht

Alle Daten, die erfolgreich in die Adobe Experience Platform aufgenommen wurden, bleiben im [!DNL Data Lake] Datensatz erhalten. Ein Datensatz ist ein Datenspeicherung- und Verwaltungskonstrukt für eine Datenerfassung, normalerweise eine Tabelle, die ein Schema (Spalten) und Felder (Zeilen) enthält. Datasets enthalten auch Metadaten, die verschiedene Aspekte der von ihnen gespeicherten Daten beschreiben.

This document provides a high-level overview of datasets in [!DNL Experience Platform].

## Erstellen von Datensätzen und Verfolgen von Metadaten

[!DNL Catalog Service] ist das Datensatzsystem für die Datenposition und -linie innerhalb [!DNL Experience Platform]und wird zum Erstellen und Verwalten von Datensätzen verwendet. [!DNL Catalog] verfolgt die Metadaten für jeden Datensatz, der einen Verweis auf das [!DNL Experience Data Model] (XDM-)Schema enthält, dem der Datensatz entspricht (im nächsten Abschnitt erläutert), und die Anzahl der Datensätze, die in diesen Datensatz aufgenommen werden.

See the [Catalog Service overview](../home.md) for more information.

## Einschränkungen für Datensatzdaten erzwingen

[!DNL Experience Data Model] (XDM) ist das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Platform] organisiert werden. Alle Daten, in die aufgenommen wird, [!DNL Platform] müssen einem vordefinierten XDM-Schema entsprechen, bevor sie im [!DNL Data Lake] Datensatz beibehalten werden können.

Alle Datensätze enthalten einen Verweis auf das XDM-Schema, das Format und Struktur der Daten, die gespeichert werden können, einschränkt. Wenn Sie versuchen, Daten in einen Datensatz hochzuladen, der nicht dem XDM-Schema des Datensatzes entspricht, schlägt die Erfassung fehl.

For more information on XDM, see the [XDM System overview](../../xdm/home.md).

## Daten in Datensätze aufnehmen

Adobe Experience Platform Data Ingestion stellt die verschiedenen Methoden dar, mit denen Daten aus verschiedenen Quellen [!DNL Platform] erfasst werden. Unabhängig von der Erfassungsmethode werden alle erfolgreich erfassten Daten in Stapeldateien konvertiert. Batches sind Dateneinheiten aus einer oder mehreren Dateien, die als Ganzes aufgenommen werden. Diese Stapeldateien werden dann zu dedizierten Datensätzen hinzugefügt und bleiben im [!DNL Data Lake]Ordner erhalten.

See the [Data Ingestion overview](../../ingestion/home.md) for more information.

## Anwenden von Nutzungsbezeichnungen auf Datasets

Adobe Experience Platform [!DNL Data Governance] allows you to manage customer data in order to ensure compliance with regulations, restrictions, and policies applicable to data use. Mithilfe der Datenbenennung und -durchsetzung (DULE) als Kernframework [!DNL Data Governance] können Sie Nutzungsbezeichnungen anwenden, um Daten entsprechend den für diese Daten geltenden Nutzungsrichtlinien zu kategorisieren.

Datenverwendungsbeschriftungen können auf ganze Datensätze oder einzelne Datensatzfelder angewendet werden. Auf Datensatzebene hinzugefügte Bezeichnungen werden von allen Feldern in diesem Datensatz übernommen.

Weitere Informationen zum Dienst finden Sie in der Übersicht über die [Datenverwaltung](../../data-governance/home.md) . Anweisungen zum Arbeiten mit Nutzungsbeschriftungen finden Sie in [!DNL Platform]den folgenden Handbüchern:

* [Verwalten von Beschriftungen in der Benutzeroberfläche](../../data-governance/labels/user-guide.md)
* [Verwalten von Beschriftungen in der API](../../data-governance/labels/api.md)

## Datenbestände in nachgelagerten [!DNL Platform] Diensten

Sobald Datasets zur Speicherung von erfassten Daten verwendet wurden, werden diese Datensätze von den nachgelagerten [!DNL Platform] Diensten zur Aktualisierung von Kundendaten, zur Erzielung von Einblicken durch maschinelles Lernen und mehr verwendet.

Im Folgenden finden Sie eine Liste nachgelagerter Dienste, die Datasets für verschiedene Vorgänge verwenden. Weitere Informationen finden Sie in der Dokumentation zu den einzelnen Diensten.

* [!DNL Data Access API](../../data-access/home.md): Ermöglicht Ihnen den Zugriff auf und das Herunterladen der Inhalte von Dateien, die in Datasets gespeichert sind.
* [Identitätsdienst](../../identity-service/home.md)der Adobe Experience Platform: Überbrückt Identitäten zwischen Geräten und Systemen und verknüpft Datensätze anhand der Identitätsfelder, die von den XDM-Schemas definiert werden, denen sie entsprechen.
* [!DNL Real-time Customer Profile](../../profile/home.md): Ermöglicht [!DNL Identity Service] die Erstellung detaillierter Kundendaten aus Ihren Datensätzen in Echtzeit. [!DNL Real-time Customer Profile] ruft Daten aus dem [!DNL Data Lake] und speichert Kundendaten in einem eigenen separaten Datenspeicher.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Ermöglicht Ihnen das Erstellen von Segmenten und das Generieren von Audiencen aus Ihren [!DNL Real-time Customer Profile] Daten. Diese Audiencen können dann in ihre eigenen Datensätze innerhalb des [!DNL Data Lake]Berichts exportiert werden.
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Verwendet maschinelles Lernen und künstliche Intelligenz, um Einblicke in große Datensätze zu entdecken.
* [Adobe Experience Platform Abfrage Service](../../query-service/home.md): Ermöglicht Ihnen die Verwendung von SQL zur Abfrage von Daten in [!DNL Experience Platform]Datasets innerhalb der Abfrage [!DNL Data Lake] und die Erfassung der Ergebnisse als neuer Datensatz zur Verwendung in Berichte, [!DNL Data Science Workspace]oder [!DNL Real-time Customer Profile].
* [Entscheidungsdienst](../../decisioning-service/home.md)für Adobe Experience Platformen: Nutzen Sie diese Optionen, [!DNL Real-time Customer Profile] um die wahrscheinlichste Auswahl zu ermitteln, die ein Kunde anhand von Verhaltensdaten treffen wird, die aus aktivierten Datensätzen [!DNL Profile] abgerufen werden.

## Nächste Schritte

Durch das Lesen dieses Dokuments wurden Sie in die Kernverwendungen von Datensätzen in [!DNL Experience Platform]sowie in den verschiedenen [!DNL Platform] Diensten, die Datasets verwenden, eingeführt. Weitere Informationen zu den zahlreichen Verwendungsmöglichkeiten von Datensätzen [!DNL Platform]finden Sie in der Servicedokumentation.

Anweisungen zur Interaktion mit Datensätzen in der [!DNL Experience Platform] Benutzeroberfläche finden Sie im Benutzerhandbuch zu [Datensätzen](user-guide.md).