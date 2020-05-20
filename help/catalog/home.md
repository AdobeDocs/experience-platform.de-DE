---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über den Katalogdienst
topic: overview
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---


# Übersicht über den Katalogdienst

Der Katalogdienst ist das Datensatzsystem für die Datenposition und -leitung innerhalb der Adobe Experience Platform. Während alle Daten, die in Experience Platform erfasst werden, als Dateien und Ordner im Data Lake gespeichert werden, speichert Catalog die Metadaten und Beschreibungen dieser Dateien und Ordner für Such- und Überwachungszwecke.

Einfach ausgedrückt handelt der Katalog als Metadatenspeicher oder &quot;Katalog&quot;, in dem Sie Informationen zu Ihren Daten in Experience Platform finden können. Mit dem Katalog können Sie die folgenden Fragen beantworten:

* Wo befinden sich meine Daten?
* In welchem Stadium der Verarbeitung befinden sich diese Daten?
* Welche Systeme oder Prozesse haben auf meine Daten reagiert?
* Wie viele Daten wurden erfolgreich verarbeitet?
* Welche Fehler sind bei der Verarbeitung aufgetreten?

Catalog bietet eine RESTful-API, mit der Sie Plattformmetadaten programmgesteuert mithilfe einfacher CRUD-Vorgänge verwalten können. Weitere Informationen finden Sie im Entwicklerhandbuch für [Kataloge](api/getting-started.md) .

## Dienste für Kataloge und Erlebnisplattformen

Die vom Catalog-Dienst nachverfolgten Ressourcen werden von mehreren Experience Platform-Diensten verwendet. Um die Möglichkeiten des Katalogs optimal zu nutzen, sollten Sie sich mit diesen Diensten und ihrer Interaktion mit dem Katalog vertraut machen.

### Erlebnis-Datenmodell (XDM)-System

Experience Data Model (XDM) System ist das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert. Die Experience Platform nutzt XDM-Schema, um die Datenstruktur konsistent und wiederverwendbar zu beschreiben.

Wenn Daten in Plattform erfasst werden, wird die Struktur dieser Daten einem XDM-Schema zugeordnet und im Data Lake als Teil eines **Datensatzes** gespeichert. Die Metadaten für jeden Datensatz werden vom Katalogdienst verfolgt, der einen Verweis auf das XDM-Schema enthält, dem der Datensatz entspricht.

Weitere allgemeine Informationen zum XDM-System finden Sie in der [XDM-Systemübersicht](../xdm/home.md).

### Dateneinbindung

Experience Platform erfasst Daten aus mehreren Quellen und behält Datensätze als Datensätze innerhalb des Data Lake bei. Der Katalog verfolgt die Metadaten für diese Datensätze, unabhängig von ihrer Quelle oder Methode der Erfassung.

Bei Verwendung der Stapelverarbeitungsmethode verfolgt Catalog auch zusätzliche Metadaten für **Stapeldateien** . Stapel sind Dateneinheiten, die aus einer oder mehreren Dateien bestehen, die als eine Einheit erfasst werden sollen. Der Katalog verfolgt die Metadaten für diese Stapeldateien sowie die Datensätze, in denen sie nach der Erfassung beibehalten werden. Stapelmetadaten enthalten Informationen zur Anzahl der erfolgreich erfassten Datensätze sowie alle fehlgeschlagenen Datensätze und zugehörigen Fehlermeldungen.

See the [data ingestion overview](../ingestion/home.md) for more information.

## Katalogobjekte

Wie im vorherigen Abschnitt erläutert, verfolgt Catalog Metadaten für verschiedene Arten von Ressourcen und Vorgängen, die von anderen Plattformdiensten verwendet werden. Katalog unterhält einen eigenen Speicher von &quot;Objekten&quot;, die diese Metadaten kapseln. Katalogobjekte sind abfragliche Darstellungen von Plattformdaten, mit denen Sie Ihre Daten suchen, überwachen und beschriften können, ohne selbst auf die Daten zugreifen zu müssen.

In der folgenden Tabelle sind die verschiedenen vom Katalog unterstützten Objektarten aufgeführt:

| Objekt | API-Endpunkt | Definition |
|---|---|---|
| Konto | `/accounts` | Beim Erstellen von Quellverbindungen müssen Authentifizierungsberechtigungen angegeben werden. Ein Konto stellt eine Sammlung von Authentifizierungsberechtigungen dar, die zum Erstellen einer Verbindung eines bestimmten Typs verwendet wurden. Jede Verbindung verfügt über eine Reihe von eindeutigen Parametern, die vom Katalog beibehalten und in einem Azurblauen Schlüssel-Vault gesichert werden. |
| Stapel | `/batches` | Stapel sind Dateneinheiten, die aus einer oder mehreren Dateien bestehen, die als eine Einheit erfasst werden sollen. Ein Stapelobjekt im Katalog skizziert die Erfassungsmetriken des Stapels (z. B. die Anzahl der verarbeiteten Datensätze oder die Größe auf der Festplatte) und kann auch Links zu Datensätzen, Ansichten und anderen Ressourcen enthalten, die von dem Stapelvorgang betroffen waren. |
| Verbindung | `/connections` | Eine Verbindung ist eine einzelne Instanz eines Quell-Connectors, die für Ihr Unternehmen eindeutig ist und mit den entsprechenden Authentifizierungsberechtigungen für den Connector-Typ konfiguriert wurde. |
| Connector | `/connectors` | Connectors definieren, wie Quellverbindungen Daten aus anderen Adobe-Anwendungen (z. B. Adobe Analytics und Adobe Audience Manager), Cloud-Datenspeicherung-Quellen von Drittanbietern (z. B. Blue Blob, Amazon S3, FTP-Server und SFTP-Server) und CRM- von Drittanbietern (z. B. Microsoft Dynamics und Salesforce) erfassen sollen. |
| Datenbestand | `/dataSets` | Ein Datensatz ist ein Datenspeicherung- und Verwaltungskonstrukt, das für die Datenerfassung (normalerweise eine Tabelle) mit einem Schema (Spalten) und Feldern (Zeilen) verwendet wird. |
| Datenbestand-Datei | `/datasetFiles` | Datenaset-Dateien stellen Datenblöcke dar, die auf der Plattform gespeichert wurden. Als Datensätze von Literaldateien finden Sie hier die Dateigröße, die Anzahl der darin enthaltenen Datensätze und einen Verweis auf den Stapel, der die Datei erfasst hat. |

## Nächste Schritte

Dieses Dokument bietet eine Einführung in den Katalogdienst und seine Funktionsweise im größeren Rahmen der Erlebnisplattform. Schritte zur Interaktion mit den verschiedenen Endpunkten der jeweiligen Katalog-API finden Sie im [Catalog Developer Guide](api/getting-started.md) . Es wird empfohlen, sich auch an das Handbuch zum [Filtern von Katalogdaten](api/filter-data.md) zu wenden, um bewährte Verfahren zur Beschränkung der in API-Antworten zurückgegebenen Daten zu befolgen.