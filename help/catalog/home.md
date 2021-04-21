---
keywords: Experience Platform;Home;beliebte Themen;Katalogdienst;Katalog;Katalogdienst;Datenspeicherort;Datenposition;Data Management;Data Management;Lineage;Linie;Katalog;Datensatz aktivieren
solution: Experience Platform
title: Übersicht über den Katalogdienst
topic-legacy: overview
description: Catalog Service ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Adobe Experience Platform. Alle Daten, die in Experience Platform aufgenommen werden, werden als Dateien und Ordner im Data Lake gespeichert. Der Katalog wiederum speichert die Metadaten und Beschreibungen dieser Dateien und Ordner für Such- und Überwachungszwecke.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 43%

---

# [!DNL Catalog Service]Übersicht

[!DNL Catalog Service] ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Experience Platform. Während alle Daten, die in [!DNL Experience Platform] aufgenommen werden, im [!DNL Data Lake] als Dateien und Ordner gespeichert werden, enthält [!DNL Catalog] die Metadaten und Beschreibungen dieser Dateien und Ordner für die Suche und Überwachung.

Einfach ausgedrückt: [!DNL Catalog] fungiert als Metadatenspeicher oder &quot;Katalog&quot;, in dem Sie Informationen zu Ihren Daten in [!DNL Experience Platform] finden können. Sie können [!DNL Catalog] verwenden, um die folgenden Fragen zu beantworten:

* Wo befinden sich meine Daten?
* Auf welcher Stufe der Verarbeitung befinden sich diese Daten?
* Welche Systeme oder Prozesse haben Aktionen auf meine Daten ausgeführt?
* Wie viele Daten wurden erfolgreich verarbeitet?
* Welche Fehler sind bei der Verarbeitung aufgetreten?

[!DNL Catalog] stellt eine RESTful-API bereit, mit der Sie  [!DNL Platform] Metadaten programmgesteuert mithilfe einfacher CRUD-Vorgänge verwalten können. Weitere Informationen finden Sie im [Katalog-Service-Entwicklerhandbuch](api/getting-started.md).

## [!DNL Catalog] und  [!DNL Experience Platform] Dienstleistungen

Die Ressourcen, die von [!DNL Catalog Service] verfolgt werden, werden von mehreren [!DNL Experience Platform]-Diensten verwendet. Um die Funktionen von [!DNL Catalog's] optimal nutzen zu können, sollten Sie sich mit diesen Diensten und ihrer Interaktion mit [!DNL Catalog] vertraut machen.

### [!DNL Experience Data Model] (XDM) System

[!DNL Experience Data Model] (XDM) System ist das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Platform] organisiert werden. [!DNL Experience Platform]XDM-Schemas dienen in zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten.

Wenn Daten in [!DNL Platform] aufgenommen werden, wird die Struktur dieser Daten einem XDM-Schema zugeordnet und im [!DNL Data Lake]-Datensatz gespeichert. Die Metadaten für jeden Datensatz werden von [!DNL Catalog Service] verfolgt, was einen Verweis auf das XDM-Schema enthält, dem der Datensatz entspricht.

Informationen zum XDM-System im Allgemeinen finden Sie in der [Übersicht über das XDM-System](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] erfasst Daten aus mehreren Quellen und speichert Datensätze als Datensätze innerhalb der  [!DNL Data Lake]. [!DNL Catalog] verfolgt die Metadaten für diese Datensätze, unabhängig von ihrer Quelle oder Methode der Erfassung.

Bei Verwendung der Stapelverarbeitungsmethode verfolgt [!DNL Catalog] auch zusätzliche Metadaten für Stapeldateien. Batches sind Dateneinheiten aus einer oder mehreren Dateien, die als Ganzes aufgenommen werden. [!DNL Catalog] verfolgt die Metadaten für diese Stapeldateien sowie die Datensätze, in denen sie nach der Erfassung beibehalten werden. Batch-Metadaten umfassen Informationen zur Anzahl der erfolgreich aufgenommenen Datensätze sowie zu fehlgeschlagenen Datensätzen und zugehörige Fehlermeldungen.

Weitere Informationen finden Sie in der [Datenerfassung – Übersicht](../ingestion/home.md).

## [!DNL Catalog] Objekte

Wie im vorherigen Abschnitt erläutert, verfolgt [!DNL Catalog] Metadaten für verschiedene Arten von Ressourcen und Vorgängen, die von anderen [!DNL Platform]-Diensten verwendet werden. [!DNL Catalog] verwaltet einen eigenen Speicher von &quot;Objekten&quot;, die diese Metadaten kapseln. [!DNL Catalog] Objekte sind abfragliche Darstellungen von  [!DNL Platform] Daten, mit denen Sie Ihre Daten suchen, überwachen und beschriften können, ohne selbst auf die Daten zugreifen zu müssen.

Die folgende Tabelle zeigt die verschiedenen Objekttypen, die von [!DNL Catalog] unterstützt werden:

| Objekt | API-Endpunkt | Definition |
|---|---|---|
| Konto | `/accounts` | Beim Erstellen von Quellverbindungen müssen Authentifizierungsberechtigungen angegeben werden. Ein Konto ist eine Sammlung von Anmeldeinformationen, die zur Authentifizierung für das Herstellen einer Verbindung bestimmten Typs verwendet wurden. Jede Verbindung verfügt über einen Satz eindeutiger Parameter, die von [!DNL Catalog] beibehalten und in einem [!DNL Azure Key Vault] gesichert werden. |
| Batch | `/batches` | Batches sind Dateneinheiten aus einer oder mehreren Dateien, die als Ganzes aufgenommen werden. Ein Stapelobjekt in [!DNL Catalog] zeigt die Erfassungsmetriken des Stapels an (z. B. die Anzahl der verarbeiteten Datensätze oder die Größe auf der Festplatte) und kann auch Links zu Datensätzen, Ansichten und anderen Ressourcen enthalten, die von dem Stapelvorgang betroffen waren. |
| Verbindung | `/connections` | Eine Verbindung ist eine einzelne Instanz eines Quell-Connectors, die für Ihr Unternehmen eindeutig ist und unter Verwendung der entsprechenden Anmeldeinformationen zur Authentifizierung für den Connector-Typ konfiguriert wurde. |
| Connector | `/connectors` | Connectors definieren, wie Quellverbindungen Daten aus anderen Anwendungen der Adobe (z. B. Adobe Analytics und Adobe Audience Manager), Cloud-Datenspeicherung von Drittanbietern (z. B. [!DNL Azure Blob], [!DNL Amazon S3], FTP-Server und SFTP-Server) und CRM-Systemen von Drittanbietern (z. B. [!DNL Microsoft Dynamics] und [!DNL Salesforce]) erfassen sollen. |
| Datensatz | `/dataSets` | Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, in dem Daten (in der Regel) in einer Tabelle erfasst werden, die ein Schema (Spalten) und Felder (Zeilen) beinhaltet. Weitere Informationen finden Sie unter [Übersicht über Datensätze](./datasets/overview.md). |
| Datensatzdatei | `/datasetFiles` | Datenbearbeitungsdateien stellen Datenblöcke dar, die unter [!DNL Platform] gespeichert wurden. Sie stellen Aufzeichnungen von Literaldateien und liefern als solches Informationen zur Dateigröße, zur Anzahl der darin enthaltenen Datensätze und einen Verweis auf den Batch, in dem die Datei aufgenommen wurde. |

## Nächste Schritte

Dieses Dokument gab eine Einführung in [!DNL Catalog Service] und wie es im größeren Bereich von [!DNL Experience Platform] funktioniert. Anweisungen zur Interaktion mit den verschiedenen Endpunkten dieser [!DNL Catalog]-API finden Sie im [[!DNL Catalog] Entwicklerhandbuch](api/getting-started.md). Es wird empfohlen, auch das Handbuch zum Thema [Filtern von Katalogdaten](api/filter-data.md) durchzugehen, da darin Best Practices für die Beschränkung der in API-Antworten zurückgegebenen Daten erläutert werden.
