---
keywords: Experience Platform;Startseite;beliebte Themen;Datenposition;Datenposition;Data Management;Data Management;Lineage;Datentyp;Datentypen;Datentypen;Datentyp
solution: Experience Platform
title: Übersicht über Datasets
topic-legacy: datasets
description: Dieses Dokument bietet einen Überblick über Datensätze in der Experience Platform.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 3%

---

# Datensätze – Übersicht

Alle Daten, die erfolgreich in Adobe Experience Platform aufgenommen wurden, bleiben innerhalb der [!DNL Data Lake] als Datensätze erhalten. Ein Datensatz ist ein Datenspeicherung- und Verwaltungskonstrukt für eine Datenerfassung, normalerweise eine Tabelle, die ein Schema (Spalten) und Felder (Zeilen) enthält. Datasets enthalten auch Metadaten, die verschiedene Aspekte der von ihnen gespeicherten Daten beschreiben.

Dieses Dokument bietet eine allgemeine Übersicht über Datensätze in [!DNL Experience Platform].

## Erstellen von Datensätzen und Verfolgen von Metadaten

[!DNL Catalog Service] ist das Datensatzsystem für die Datenposition und -linie innerhalb  [!DNL Experience Platform]und wird zum Erstellen und Verwalten von Datensätzen verwendet. [!DNL Catalog] verfolgt die Metadaten für jeden Datensatz, der einen Verweis auf das XDM-Schema enthält, dem der Datensatz entspricht (im nächsten Abschnitt erläutert), und die Anzahl der Datensätze, die in diesen Datensatz aufgenommen werden.  [!DNL Experience Data Model] 

Weitere Informationen finden Sie unter [Übersicht über den Katalogdienst](../home.md).

## Einschränkungen für Datensatzdaten erzwingen

[!DNL Experience Data Model] (XDM) ist das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Platform] organisiert werden. Alle Daten, die in [!DNL Platform] aufgenommen werden, müssen mit einem vordefinierten XDM-Schema übereinstimmen, bevor sie im [!DNL Data Lake] als Datensatz beibehalten werden können.

Alle Datensätze enthalten einen Verweis auf das XDM-Schema, das Format und Struktur der Daten, die gespeichert werden können, einschränkt. Wenn Sie versuchen, Daten in einen Datensatz hochzuladen, der nicht dem XDM-Schema des Datensatzes entspricht, schlägt die Erfassung fehl.

Weitere Informationen zu XDM finden Sie unter [XDM-Systemübersicht](../../xdm/home.md).

## Daten in Datensätze aufnehmen

Adobe Experience Platform Data Ingestion stellt die verschiedenen Methoden dar, mit denen [!DNL Platform] Daten aus verschiedenen Quellen erfasst. Unabhängig von der Erfassungsmethode werden alle erfolgreich erfassten Daten in Stapeldateien konvertiert. Batches sind Dateneinheiten aus einer oder mehreren Dateien, die als Ganzes aufgenommen werden. Diese Stapeldateien werden dann zu dedizierten Datensätzen hinzugefügt und bleiben innerhalb von [!DNL Data Lake] erhalten.

Weitere Informationen finden Sie unter [Übersicht über die Dateneinbettung](../../ingestion/home.md).

## Anwenden von Nutzungsbezeichnungen auf Datasets

Mit Adobe Experience Platform [!DNL Data Governance] können Sie Kundendaten verwalten, um die Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datenverwendung sicherzustellen. Mit dem [!DNL Data Governance]-Framework können Sie Verwendungsbeschriftungen anwenden, um Daten entsprechend den für diese Daten geltenden Nutzungsrichtlinien zu kategorisieren.

Datenverwendungsbeschriftungen können auf ganze Datensätze oder einzelne Datensatzfelder angewendet werden. Auf Datensatzebene hinzugefügte Bezeichnungen werden von allen Feldern in diesem Datensatz übernommen.

Weitere Informationen zum Dienst finden Sie unter [Übersicht über die Datenverwaltung](../../data-governance/home.md). Anweisungen zum Arbeiten mit Gebrauchsbeschriftungen in [!DNL Platform] finden Sie in den folgenden Handbüchern:

* [Verwalten von Beschriftungen in der Benutzeroberfläche](../../data-governance/labels/user-guide.md)
* [Verwalten von Datenbeschriftungen in der API](../../data-governance/labels/dataset-api.md)

## Datasets in nachgelagerten [!DNL Platform]-Diensten

Sobald Datasets zur Speicherung von erfassten Daten verwendet wurden, werden diese Datensätze von den nachgeschalteten [!DNL Platform]-Diensten verwendet, um Kundendaten zu aktualisieren, Einblicke durch maschinelles Lernen zu gewinnen und vieles mehr.

Im Folgenden finden Sie eine Liste nachgelagerter Dienste, die Datasets für verschiedene Vorgänge verwenden. Weitere Informationen finden Sie in der Dokumentation zu den einzelnen Diensten.

* [[!DNL Data Access API]](../../data-access/home.md): Ermöglicht Ihnen den Zugriff auf und das Herunterladen der Inhalte von Dateien, die in Datasets gespeichert sind.
* [Adobe Experience Platform-Identitätsdienst](../../identity-service/home.md): Überbrückt Identitäten zwischen Geräten und Systemen und verknüpft Datensätze anhand der Identitätsfelder, die von den XDM-Schemas definiert werden, denen sie entsprechen.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Ermöglicht  [!DNL Identity Service] die Erstellung detaillierter Kundendaten aus Ihren Datensätzen in Echtzeit. [!DNL Real-time Customer Profile] ruft Daten aus dem Formular ab  [!DNL Data Lake] und behält die Profil von Kunden in einem eigenen separaten Datenspeicher bei.
* [Adobe Experience Platform-Segmentierungsdienst](../../segmentation/home.md): Ermöglicht Ihnen das Erstellen von Segmenten und das Generieren von Audiencen aus Ihren  [!DNL Real-time Customer Profile] Daten. Diese Audiencen können dann in ihre eigenen Datensätze innerhalb von [!DNL Data Lake] exportiert werden.
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Verwendet maschinelles Lernen und künstliche Intelligenz, um Einblicke in große Datensätze zu entdecken.
* [Adobe Experience Platform Abfrage Service](../../query-service/home.md): Ermöglicht Ihnen die Verwendung von SQL zur Abfrage von Daten in  [!DNL Experience Platform]Datasets innerhalb der Abfrage  [!DNL Data Lake] und die Erfassung der Ergebnisse als neuer Datensatz zur Verwendung in Berichte,  [!DNL Data Science Workspace]oder  [!DNL Real-time Customer Profile].

## Nächste Schritte

Durch Lesen dieses Dokuments wurden Sie in die Kernverwendungen von Datensätzen in [!DNL Experience Platform] sowie in den verschiedenen [!DNL Platform]-Diensten, die Datasets verwenden, eingeführt. Weitere Informationen zu den zahlreichen Verwendungsmöglichkeiten von Datensätzen in [!DNL Platform] finden Sie in der Dienstdokumentation, die in diesem Überblick verlinkt ist.

Anweisungen zur Interaktion mit Datensätzen in der [!DNL Experience Platform]-Benutzeroberfläche finden Sie im [Benutzerhandbuch für Datensätze](user-guide.md).
