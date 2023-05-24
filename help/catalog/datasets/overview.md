---
keywords: Experience Platform;Startseite;beliebte Themen;Datenspeicherort;Datenspeicherplatz;Datenmanagement;Datenverwaltung;Ursprung;Herkunft;Datentyp;Datentypen
solution: Experience Platform
title: Übersicht zu Datensätzen
description: Dieses Dokument bietet einen umfassenden Überblick über Datensätze in Experience Platform.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: dca5c9df82434d75238a0a80f15e5562cf2fa412
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 83%

---

# Übersicht zu Datensätzen

Alle Daten, die in Adobe Experience Platform erfolgreich aufgenommen werden, bleiben als Datensätze im [!DNL Data Lake] erhalten. Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, in dem Daten (in der Regel) in einer Tabelle erfasst werden, die ein Schema (Spalten) und Felder (Zeilen) beinhaltet. Datensätze enthalten auch Metadaten, die verschiedene Aspekte der in ihnen gespeicherten Daten beschreiben.

Dieses Dokument bietet einen umfassenden Überblick über Datensätze in [!DNL Experience Platform].

## Erstellen von Datensätzen und Tracking von Metadaten

[!DNL Catalog Service] ist das Aufzeichnungssystem für den Speicherort und die Herkunft von Daten innerhalb von [!DNL Experience Platform] und wird zum Erstellen und Verwalten von Datensätzen verwendet. [!DNL Catalog] verfolgt die Metadaten für jeden Datensatz. Darin enthalten ist ein Verweis auf das [!DNL Experience Data Model] (XDM)-Schema, dem der Datensatz entspricht (im nächsten Abschnitt erläutert), und die Anzahl der in diesen Datensatz aufgenommenen Datensätze.

Weitere Informationen dazu inden Sie in der [Übersicht zum Katalog-Service](../home.md).

## Durchsetzen von Einschränkungen für Datensatzdaten

Das [!DNL Experience Data Model] (XDM) ist das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert. Alle in [!DNL Platform] aufgenommene Daten müssen einem vordefinierten XDM-Schema entsprechen, bevor sie in [!DNL Data Lake] als Datensatz beibehalten werden können.

Alle Datensätze enthalten einen Verweis auf das XDM-Schema, das das Format und die Struktur der Daten einschränkt, die sie speichern können. Der Versuch, Daten in einen Datensatz hochzuladen, der nicht dem XDM-Schema des Datensatzes entspricht, führt dazu, dass die Aufnahme fehlschlägt.

Weitere Informationen zu XDM finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Aufnehmen von Daten in Datensätze

Die Adobe Experience Platform-Datenaufnahme steht für die verschiedenen Methoden, mit denen [!DNL Platform] Daten aus verschiedenen Quellen aufnimmt. Unabhängig von der Aufnahmemethode werden alle erfolgreich aufgenommenen Daten in Batch-Dateien konvertiert. Batches sind Dateneinheiten aus einer oder mehreren Dateien, die als Ganzes aufgenommen werden. Diese Batch-Dateien werden dann zu dedizierten Datensätzen hinzugefügt und innerhalb des [!DNL Data Lake] beibehalten.

Weitere Informationen finden Sie in der [Übersicht zur Datenaufnahme](../../ingestion/home.md).

## Auf Datensätze aus Schemas angewendete Beschriftungen

Mit Data Governance in Adobe Experience Platform können Sie Kundendaten verwalten, um sicherzustellen, dass die für die Verwendung von Daten geltenden Vorschriften, Einschränkungen und Richtlinien eingehalten werden. Mit dem Data Governance-Framework können Sie Nutzungskennzeichnungen anwenden, um Daten entsprechend den für diese Daten geltenden Nutzungsrichtlinien zu kategorisieren. Beschriftungen können auf einzelne Schemata, Felder innerhalb dieser Schemas und ganze einzelne Datensätze angewendet werden. Wenn Beschriftungen direkt auf ein Schema angewendet werden, werden diese Beschriftungen auf alle vorhandenen und zukünftigen Datensätze übertragen, die auf diesem Schema basieren.

>[!IMPORTANT]
>
>Beschriftungen können nicht mehr auf Felder auf Datensatzebene angewendet werden. Dieser Workflow wird nicht mehr für die Anwendung von Bezeichnungen auf Schemaebene unterstützt. Alle Bezeichnungen, die zuvor auf Datensatzobjektebene angewendet wurden, werden bis zum 31. Mai 2024 weiterhin über die Platform-Benutzeroberfläche unterstützt. Um sicherzustellen, dass Ihre Bezeichnungen über alle Schemas hinweg konsistent sind, müssen alle Bezeichnungen, die zuvor auf Datensatzebene an Felder angehängt wurden, von Ihnen im Laufe des kommenden Jahres auf Schemaebene migriert werden. Siehe Abschnitt zu [Migration zuvor angewendeter Bezeichnungen](../../data-governance/e2e.md#migrate-labels) für Anweisungen dazu.

Weitere Informationen zu dem Service finden Sie in der [Übersicht zu Data Governance](../../data-governance/home.md). Schrittweise Anweisungen zum Arbeiten mit Nutzungskennzeichnungen in [!DNL Platform] finden Sie in den folgenden Handbüchern:

* [Verwalten von Kennzeichnungen in der Benutzeroberfläche](../../data-governance/labels/user-guide.md)
* [Verwalten von Datensatzkennzeichnungen in der API](../../data-governance/labels/dataset-api.md)

## Datensätze in nachgelagerten [!DNL Platform]-Services

Sobald Datensätze zum Speichern aufgenommener Daten verwendet wurden, werden diese Datensätze von nachgelagerten [!DNL Platform]-Services verwendet, um Kundenprofile zu aktualisieren, Erkenntnisse durch maschinelles Lernen zu gewinnen und vieles mehr.

Im Folgenden finden Sie eine Liste nachgelagerter Services, die Datensätze für verschiedene Vorgänge verwenden. Weitere Informationen finden Sie in der Dokumentation für den jeweiligen Service.

* [[!DNL Data Access API]](../../data-access/home.md): Ermöglicht den Zugriff auf und den Download der Inhalte von Dateien, die in Datensätzen gespeichert sind.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Führt Identitäten zwischen Geräten und Systemen zusammen und verknüpft Datensätze anhand der Identitätsfelder, die von den entsprechenden XDM-Schemata definiert werden.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Nutzt den [!DNL Identity Service], um aus Ihren Datensätzen in Echtzeit detaillierte Kundenprofile zu erstellen. Das [!DNL Real-Time Customer Profile] ruft Daten aus dem [!DNL Data Lake] ab und speichert Kundenprofile in einem eigenen separaten Datenspeicher.
* [Segmentierungs-Service von Adobe Experience Platform](../../segmentation/home.md): Ermöglicht Ihnen das Erstellen von Segmenten und das Generieren von Zielgruppen aus Ihren [!DNL Real-Time Customer Profile]-Daten. Diese Audiences können dann in ihre eigenen Datensätze im [!DNL Data Lake] exportiert werden.
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Nutzt maschinelles Lernen und künstliche Intelligenz, um Einblicke aus großen Datensätzen zu gewinnen.
* [Abfrage-Service von Adobe Experience Platform](../../query-service/home.md): Ermöglicht die Verwendung standardmäßiger SQL zur Abfrage von Daten in [!DNL Experience Platform], führt so beliebige Datensätze im [!DNL Data Lake] zusammen und erfasst Abfrageergebnisse als neuen Datensatz für Berichte, [!DNL Data Science Workspace] oder [!DNL Real-Time Customer Profile].
* [Ziel-Service von Adobe Experience Platform](../../destinations/home.md): Ermöglicht Ihnen das [Exportieren von Datensätzen](/help/destinations/ui/export-datasets.md) an Ihre gewünschten Cloud-Speicher- oder E-Mail-Marketing-Ziele für Reporting- oder Datenwissenschaftsaktivitäten.

## Nächste Schritte

Durch das Lesen dieses Dokuments haben Sie sich mit den wichtigsten Verwendungen von Datensätzen in [!DNL Experience Platform] sowie mit den verschiedenen [!DNL Platform]-Services, die Datensätze verwenden, vertraut gemacht. Weitere Informationen zu den zahlreichen Verwendungsmöglichkeiten von Datensätzen in [!DNL Platform] finden Sie in den Service-Dokumentationen, zu denen im Verlauf dieser Übersicht verlinkt wird.

Anweisungen zur Interaktion mit Datensätzen in der [!DNL Experience Platform]-Benutzeroberfläche finden Sie im [Benutzerhandbuch zu Datensätzen](user-guide.md).
