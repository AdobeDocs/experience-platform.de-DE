---
keywords: Experience Platform; Startseite; beliebte Themen; Datenspeicherort; Datenspeicherort; Datenmanagement; Datenverwaltung; Lineage; Herkunft; Datentyp; Datentypen; Datentypen; Datentyp
solution: Experience Platform
title: Datensätze - Übersicht
topic-legacy: datasets
description: Dieses Dokument bietet einen allgemeinen Überblick über Datensätze in Experience Platform.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 7%

---

# Datensätze – Übersicht

Alle Daten, die erfolgreich in Adobe Experience Platform aufgenommen wurden, bleiben im [!DNL Data Lake] als Datensätze erhalten. Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, in dem Daten (in der Regel) in einer Tabelle erfasst werden, die ein Schema (Spalten) und Felder (Zeilen) beinhaltet. Datensätze enthalten auch Metadaten, die verschiedene Aspekte der in ihnen gespeicherten Daten beschreiben.

Dieses Dokument bietet einen allgemeinen Überblick über Datensätze in [!DNL Experience Platform].

## Erstellen von Datensätzen und Tracking-Metadaten

[!DNL Catalog Service] ist das Aufzeichnungssystem für Speicherort und Herkunft von Daten in  [!DNL Experience Platform]und wird zum Erstellen und Verwalten von Datensätzen verwendet. [!DNL Catalog] verfolgt die Metadaten für jeden Datensatz, der einen Verweis auf das  [!DNL Experience Data Model] (XDM)-Schema enthält, dem der Datensatz entspricht (siehe nächsten Abschnitt), und die Anzahl der Datensätze, die in diesen Datensatz aufgenommen werden.

Weitere Informationen finden Sie unter [Übersicht über den Katalogdienst](../home.md) .

## Einschränkungen für Datensatzdaten erzwingen

[!DNL Experience Data Model] (XDM) ist das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Platform] organisiert werden. Alle Daten, die in [!DNL Platform] aufgenommen werden, müssen einem vordefinierten XDM-Schema entsprechen, bevor es als Datensatz im [!DNL Data Lake] persistiert werden kann.

Alle Datensätze enthalten einen Verweis auf das XDM-Schema, der das Format und die Struktur der Daten einschränkt, die sie speichern können. Der Versuch, Daten in einen Datensatz hochzuladen, der nicht dem XDM-Schema des Datensatzes entspricht, führt dazu, dass die Aufnahme fehlschlägt.

Weitere Informationen zu XDM finden Sie in der [XDM-Systemübersicht](../../xdm/home.md).

## Erfassen von Daten in Datensätzen

Adobe Experience Platform Data Ingestion stellt die verschiedenen Methoden dar, mit denen [!DNL Platform] Daten aus verschiedenen Quellen erfasst. Unabhängig von der Erfassungsmethode werden alle erfolgreich erfassten Daten in Batch-Dateien konvertiert. Batches sind Dateneinheiten aus einer oder mehreren Dateien, die als Ganzes aufgenommen werden. Diese Batch-Dateien werden dann zu dedizierten Datensätzen hinzugefügt und im [!DNL Data Lake] beibehalten.

Weitere Informationen finden Sie unter [Datenerfassung - Übersicht](../../ingestion/home.md) .

## Anwenden von Nutzungsbezeichnungen auf Datensätze

Mit Adobe Experience Platform [!DNL Data Governance] können Sie Kundendaten verwalten, um die Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datennutzung sicherzustellen. Mit dem Framework [!DNL Data Governance] können Sie Nutzungsbezeichnungen anwenden, um Daten entsprechend den für diese Daten geltenden Nutzungsrichtlinien zu kategorisieren.

Datennutzungsbezeichnungen können auf komplette Datensätze oder einzelne Datensatzfelder angewendet werden. Auf Datensatzebene hinzugefügte Bezeichnungen werden von allen Feldern in diesem Datensatz übernommen.

Weitere Informationen zum Dienst finden Sie unter [Übersicht über Data Governance](../../data-governance/home.md) . Anweisungen zum Arbeiten mit Nutzungsbezeichnungen in [!DNL Platform] finden Sie in den folgenden Handbüchern:

* [Verwalten von Kennzeichnungen in der Benutzeroberfläche](../../data-governance/labels/user-guide.md)
* [Verwalten der Datensatzbezeichnungen in der API](../../data-governance/labels/dataset-api.md)

## Datensätze in nachgelagerten [!DNL Platform]-Diensten

Sobald Datensätze zum Speichern erfasster Daten verwendet wurden, werden diese Datensätze von nachgelagerten [!DNL Platform]-Diensten verwendet, um Kundenprofile zu aktualisieren, Einblicke durch maschinelles Lernen zu gewinnen und vieles mehr.

Im Folgenden finden Sie eine Liste der nachgelagerten Dienste, die Datensätze für verschiedene Vorgänge verwenden. Weitere Informationen finden Sie in der Dokumentation für jeden Dienst.

* [[!DNL Data Access API]](../../data-access/home.md): Ermöglicht den Zugriff auf und den Download des Inhalts von Dateien, die in Datensätzen gespeichert sind.
* [Adobe Experience Platform Identity-Dienst](../../identity-service/home.md): Brilliert Identitäten zwischen Geräten und Systemen und verknüpft Datensätze anhand der Identitätsfelder, die von den XDM-Schemas definiert werden, mit denen sie übereinstimmen.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Ermöglicht  [!DNL Identity Service] die Erstellung detaillierter Kundenprofile aus Ihren Datensätzen in Echtzeit. [!DNL Real-time Customer Profile] ruft Daten aus der ab  [!DNL Data Lake] und behält Kundenprofile in einem eigenen separaten Datenspeicher bei.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Ermöglicht Ihnen das Erstellen von Segmenten und das Generieren von Zielgruppen aus Ihren  [!DNL Real-time Customer Profile] Daten. Diese Zielgruppen können dann in ihre eigenen Datensätze innerhalb von [!DNL Data Lake] exportiert werden.
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Verwendet maschinelles Lernen und künstliche Intelligenz, um Einblicke in große Datensätze zu erhalten.
* [Adobe Experience Platform Query Service](../../query-service/home.md): Ermöglicht die Verwendung von SQL-Standard zum Abfragen von Daten in  [!DNL Experience Platform], zum Verbinden von Datensätzen innerhalb der  [!DNL Data Lake] und zum Erfassen von Abfrageergebnissen als neuen Datensatz zur Verwendung in Berichten,  [!DNL Data Science Workspace]oder  [!DNL Real-time Customer Profile].

## Nächste Schritte

Durch Lesen dieses Dokuments wurden Sie mit den Hauptverwendungen von Datensätzen in [!DNL Experience Platform] sowie den verschiedenen [!DNL Platform]-Diensten, die Datensätze verwenden, vertraut gemacht. Weitere Informationen zu den vielen Verwendungsmöglichkeiten von Datensätzen in [!DNL Platform] finden Sie in der Dienstdokumentation, die in dieser Übersicht verlinkt ist.

Anweisungen zur Interaktion mit Datensätzen in der [!DNL Experience Platform]-Benutzeroberfläche finden Sie im [Benutzerhandbuch zu Datensätzen](user-guide.md).
