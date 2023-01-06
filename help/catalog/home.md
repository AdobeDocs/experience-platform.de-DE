---
keywords: Experience Platform;Startseite;beliebte Themen;Katalog-Service;Katalog;Catalog-Service;Datenspeicherort;Datenspeicherort;Daten-Management;Daten-Management;Verlauf;Verlauf;Katalog;Datensatz aktivieren
solution: Experience Platform
title: Katalog-Service – Übersicht
description: Catalog Service ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Adobe Experience Platform. Alle Daten, die in Experience Platform aufgenommen werden, werden als Dateien und Ordner im Data Lake gespeichert. Der Katalog wiederum speichert die Metadaten und Beschreibungen dieser Dateien und Ordner für Such- und Überwachungszwecke.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 100%

---

# [!DNL Catalog Service] – Übersicht

[!DNL Catalog Service] ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Adobe Experience Platform. Alle Daten, die in [!DNL Experience Platform] aufgenommen werden, werden als Dateien und Ordner im [!DNL Data Lake] gespeichert. [!DNL Catalog] wiederum speichert die Metadaten und Beschreibungen dieser Dateien und Ordner für Such- und Überwachungszwecke.

Einfach ausgedrückt, dient [!DNL Catalog] als Metadatenspeicher oder „Katalog“, in dem Informationen zu allen in [!DNL Experience Platform] gespeicherten Daten abrufbar sind. Mithilfe von [!DNL Catalog] erhalten Sie Antworten auf folgende Fragen:

* Wo befinden sich meine Daten?
* Auf welcher Stufe der Verarbeitung befinden sich diese Daten?
* Welche Systeme oder Prozesse haben Aktionen auf meine Daten ausgeführt?
* Wie viele Daten wurden erfolgreich verarbeitet?
* Welche Fehler sind bei der Verarbeitung aufgetreten?

Im Rahmen von [!DNL Catalog] steht eine RESTful-API zur Verfügung, mit deren Hilfe Sie [!DNL Platform]-Metadaten anhand von grundlegenden CRUD-Operationen programmgesteuert verwalten können. Weitere Informationen finden Sie im [Katalog-Service-Entwicklerhandbuch](api/getting-started.md).

## [!DNL Catalog]- und [!DNL Experience Platform]-Services

Die Ressourcen, die von [!DNL Catalog Service] verfolgt werden, werden von mehreren [!DNL Experience Platform]-Services verwendet. Um die Möglichkeiten von [!DNL Catalog's] optimal zu nutzen, sollten Sie sich mit diesen Services vertraut machen und auch damit, wie sie mit [!DNL Catalog] interagieren.

### [!DNL Experience Data Model] (XDM)-System

Das [!DNL Experience Data Model] (XDM)-System ist das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert. [!DNL Experience Platform]XDM-Schemas dienen in zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten.

Bei der Aufnahme von Daten in [!DNL Platform] wird die Struktur dieser Daten einem XDM-Schema zugeordnet und in [!DNL Data Lake] als Teil eines Datensatzes gespeichert. Die Metadaten der einzelnen Datensätze werden von [!DNL Catalog Service] dokumentiert, wobei ein Verweis auf das dem Datensatz entsprechende XDM-Schema enthalten ist.

Informationen zum XDM-System im Allgemeinen finden Sie in der [Übersicht über das XDM-System](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] nimmt Daten aus verschiedenen Quellen auf und legt diese Aufzeichnungen als Datensätze in [!DNL Data Lake] ab. Die Metadaten für diese Datensätze werden allesamt in [!DNL Catalog] dokumentiert, unabhängig von ihrer Quelle oder der Methode ihrer Aufnahme.

Bei Verwendung der Batch-Erfassungsmethode werden in [!DNL Catalog] außerdem zusätzliche Metadaten für Batch-Dateien festgehalten. Batches sind Dateneinheiten aus einer oder mehreren Dateien, die als Ganzes aufgenommen werden. [!DNL Catalog] dokumentiert die Metadaten für diese Batch-Dateien sowie die Datensätze, in denen sie nach der Aufnahme festgehalten werden. Batch-Metadaten umfassen Informationen zur Anzahl der erfolgreich aufgenommenen Datensätze sowie zu fehlgeschlagenen Datensätzen und zugehörige Fehlermeldungen.

Weitere Informationen finden Sie in der [Datenerfassung – Übersicht](../ingestion/home.md).

## [!DNL Catalog]-Objekte

Wie im vorherigen Abschnitt erläutert, werden in [!DNL Catalog] Metadaten für verschiedene Arten von Ressourcen und Vorgänge dokumentiert, die von anderen [!DNL Platform]-Services genutzt werden. [!DNL Catalog] Der Katalog unterhält einen eigenen „Objektspeicher“, in dem diese Metadaten eingekapselt werden. [!DNL Catalog]-Objekte sind abfragbare Darstellungen von [!DNL Platform]-Daten, über die Sie Ihre Daten suchen, überwachen und beschriften können, ohne auf die Daten an sich zugreifen zu müssen.

In der folgenden Tabelle sind die verschiedenen von [!DNL Catalog] unterstützten Objekttypen aufgeführt:

| Objekt | API-Endpunkt | Definition |
|---|---|---|
| Konto | `/accounts` | Beim Erstellen von Quellverbindungen müssen Authentifizierungsberechtigungen angegeben werden. Ein Konto ist eine Sammlung von Anmeldeinformationen, die zur Authentifizierung für das Herstellen einer Verbindung bestimmten Typs verwendet wurden. Jede Verbindung verfügt über einen Satz eindeutiger Parameter, die von [!DNL Catalog] festgehalten und in einem [!DNL Azure Key Vault] gesichert werden. |
| Batch | `/batches` | Batches sind Dateneinheiten aus einer oder mehreren Dateien, die als Ganzes aufgenommen werden. Ein Batch-Objekt in [!DNL Catalog] erfasst Metriken zur Batch-Aufnahme (beispielsweise die Anzahl der verarbeiteten Datensätze oder ihre Größe auf der Festplatte) und kann außerdem Links zu Datensätzen, Ansichten und andere Ressourcen enthalten, die von der Batch-Operation betroffen waren. |
| Verbindung | `/connections` | Eine Verbindung ist eine einzelne Instanz eines Quell-Connectors, die für Ihr Unternehmen eindeutig ist und unter Verwendung der entsprechenden Anmeldeinformationen zur Authentifizierung für den Connector-Typ konfiguriert wurde. |
| Connector | `/connectors` | Connectoren definieren, wie Quellverbindungen Daten aus anderen Adobe-Programmen (beispielsweise Adobe Analytics und Adobe Audience Manager), Cloud-Speichern von Drittanbietern (beispielsweise [!DNL Azure Blob], [!DNL Amazon S3], FTP-Server und SFTP-Server) und Drittanbieter-CRM-Systemen (beispielsweise [!DNL Microsoft Dynamics] und [!DNL Salesforce]) erfassen sollen. |
| Datensatz | `/dataSets` | Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, in dem Daten (in der Regel) in einer Tabelle erfasst werden, die ein Schema (Spalten) und Felder (Zeilen) beinhaltet. Weiterführende Informationen dazu finden Sie in der [Übersicht zu Datensätzen](./datasets/overview.md). |
| Datensatzdatei | `/datasetFiles` | Datensatzdateien repräsentieren Datenblöcke, die auf [!DNL Platform] gespeichert wurden. Sie stellen Aufzeichnungen von Literaldateien und liefern als solches Informationen zur Dateigröße, zur Anzahl der darin enthaltenen Datensätze und einen Verweis auf den Batch, in dem die Datei aufgenommen wurde. |

## Nächste Schritte

Dieses Dokument diente als Einführung in [!DNL Catalog Service] und seine Funktionsweise in [!DNL Experience Platform]. Die einzelnen Schritte für die Interaktion mit den verschiedenen Endpunkten der zugehörigen [!DNL Catalog]-API finden Sie im [[!DNL Catalog] Entwicklerhandbuch](api/getting-started.md). Es wird empfohlen, auch das Handbuch zum Thema [Filtern von Katalogdaten](api/filter-data.md) durchzugehen, da darin Best Practices für die Beschränkung der in API-Antworten zurückgegebenen Daten erläutert werden.
