---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über Datasets
topic: datasets
translation-type: tm+mt
source-git-commit: 06733eb374d1b9409102a7cf13d61ed266cedaad
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---


# Übersicht über Datasets

Alle Daten, die erfolgreich in Adobe Experience Platform aufgenommen wurden, bleiben im Data Lake als Datensätze erhalten. Ein Datensatz ist ein Datenspeicherung- und Verwaltungskonstrukt für eine Datenerfassung, normalerweise eine Tabelle, die ein Schema (Spalten) und Felder (Zeilen) enthält. Datasets enthalten auch Metadaten, die verschiedene Aspekte der von ihnen gespeicherten Daten beschreiben.

Dieses Dokument bietet einen Überblick über Datensätze auf hoher Ebene in Experience Platform.

## Erstellen von Datensätzen und Verfolgen von Metadaten

Der Katalogdienst ist das Datensatzsystem für die Datenposition und -linie innerhalb der Experience Platform und wird zum Erstellen und Verwalten von Datensätzen verwendet. Catalog verfolgt die Metadaten für jeden Datensatz, der einen Verweis auf das XDM-Schema (Experience Data Model) enthält, dem der Datensatz entspricht (im nächsten Abschnitt erläutert), und die Anzahl der in diesen Datensatz erfassten Datensätze.

See the [Catalog Service overview](../home.md) for more information.

## Einschränkungen für Datensatzdaten erzwingen

Experience Data Model (XDM) ist das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert. Alle Daten, die in Platform aufgenommen werden, müssen mit einem vordefinierten XDM-Schema übereinstimmen, bevor sie im Data Lake als Datensatz beibehalten werden können.

Alle Datensätze enthalten einen Verweis auf das XDM-Schema, das Format und Struktur der Daten, die gespeichert werden können, einschränkt. Wenn Sie versuchen, Daten in einen Datensatz hochzuladen, der nicht dem XDM-Schema des Datensatzes entspricht, schlägt die Erfassung fehl.

Weitere Informationen zu XDM finden Sie in der [XDM-Systemübersicht](../../xdm/home.md).

## Daten in Datensätze aufnehmen

Adobe Experience Platform Data Ingestion stellt die verschiedenen Methoden dar, mit denen Plattform Daten aus verschiedenen Quellen erfasst. Unabhängig von der Erfassungsmethode werden alle erfolgreich erfassten Daten in Stapeldateien konvertiert. Stapel sind Dateneinheiten, die aus einer oder mehreren Dateien bestehen, die als eine Einheit erfasst werden sollen. Diese Stapeldateien werden dann zu dedizierten Datensätzen hinzugefügt und bleiben im Data Lake erhalten.

See the [Data Ingestion overview](../../ingestion/home.md) for more information.

## Anwenden von Nutzungsbezeichnungen auf Datasets

Mit Adobe Experience Platform Data Governance können Sie Kundendaten verwalten, um die Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datenverwendung sicherzustellen. Mithilfe der Datenbenennung und -durchsetzung (DULE) als Kernframework ermöglicht die Datenverwaltung die Anwendung von Nutzungsbezeichnungen, um Daten entsprechend den für diese Daten geltenden Nutzungsrichtlinien zu kategorisieren.

Datenverwendungsbeschriftungen können auf ganze Datensätze oder einzelne Datensatzfelder angewendet werden. Auf Datensatzebene hinzugefügte Bezeichnungen werden von allen Feldern in diesem Datensatz übernommen.

Weitere Informationen zum Dienst finden Sie in der Übersicht über die [Datenverwaltung](../../data-governance/home.md) . Anweisungen zum Arbeiten mit Nutzungsbeschriftungen in der Benutzeroberfläche der Experience Platform finden Sie im Benutzerhandbuch [zu den](../../data-governance/labels/user-guide.md)Datenverwendungsbeschriftungen.

## Datenbestände in nachgelagerten Plattformdiensten

Sobald Datasets zur Speicherung von erfassten Daten verwendet wurden, werden diese Datensätze von den Diensten der nachgeschalteten Plattform verwendet, um Kundendaten zu aktualisieren, Erkenntnisse durch maschinelles Lernen zu gewinnen und vieles mehr.

Im Folgenden finden Sie eine Liste nachgelagerter Dienste, die Datasets für verschiedene Vorgänge verwenden. Weitere Informationen finden Sie in der Dokumentation zu den einzelnen Diensten.

* [Datenzugriff-API](../../data-access/home.md): Ermöglicht Ihnen den Zugriff auf und das Herunterladen der Inhalte von Dateien, die in Datasets gespeichert sind.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Überbrückt Identitäten zwischen Geräten und Systemen und verknüpft Datensätze anhand der Identitätsfelder, die von den XDM-Schemas definiert werden, denen sie entsprechen.
* [Echtzeit-Profil](../../profile/home.md): Nutzen Sie den Identitätsdienst, um detaillierte Profil aus Ihren Datensätzen in Echtzeit zu erstellen. Der Echtzeit-Kunde ruft Daten aus dem Data Lake ab und behält die Profil der Kunden in seinem eigenen separaten Datenspeicher bei.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Ermöglicht Ihnen das Erstellen von Segmenten und das Generieren von Audiencen aus Ihren Echtzeit-Daten zum Profil von Kunden. Diese Audiencen können dann in ihre eigenen Datensätze innerhalb des Data Lake exportiert werden.
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Verwendet maschinelles Lernen und künstliche Intelligenz, um Einblicke in große Datensätze zu entdecken.
* [Adobe Experience Platform Abfrage Service](../../query-service/home.md): Ermöglicht Ihnen die Verwendung von SQL-Standarddaten zur Abfrage in Experience Platform, indem Sie beliebige Datensätze in den Data Lake integrieren und die Ergebnisse der Abfrage als neuer Datensatz für die Verwendung in Berichte, Data Science Workspace oder dem Echtzeit-Customer-Profil erfassen.
* [Adobe Experience Platform - Entscheidungsdienst](../../decisioning-service/home.md): Nutzt Echtzeit-Kundendaten, um die wahrscheinlichste Auswahl zu ermitteln, die ein Kunde aus einer Reihe von Optionen treffen wird, basierend auf den Verhaltensdaten, die Profil aus aktivierten Datensätzen abruft.

## Nächste Schritte

Durch das Lesen dieses Dokuments wurden Sie in die Kernverwendungen von Datensätzen in Experience Platform sowie in den verschiedenen Plattformdiensten, die Datasets verwenden, eingeführt. Weitere Informationen zu den zahlreichen Verwendungsmöglichkeiten von Datensätzen in der Plattform finden Sie in der Servicedokumentation, die Sie in diesem Überblick finden.

Anweisungen zur Interaktion mit Datensätzen in der Benutzeroberfläche der Experience Platform finden Sie im Benutzerhandbuch zu [Datensätzen](user-guide.md).