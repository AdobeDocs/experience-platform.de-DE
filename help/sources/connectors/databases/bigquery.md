---
title: Übersicht über den Google BigQuery Source Connector
description: Erfahren Sie, wie Sie Google BigQuery mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 2136ace3e3c1157ac7bbfe56071af3dc9bc66fd6
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 2%

---

# [!DNL Google BigQuery]

>[!IMPORTANT]
>
>Die [!DNL Google BigQuery] ist im Quellkatalog für Benutzende verfügbar, die Real-Time Customer Data Platform Ultimate erworben haben.

Lesen Sie dieses Dokument, um die erforderlichen Schritte zu erfahren, die Sie durchführen müssen, um Ihr [!DNL Google BigQuery]-Konto erfolgreich mit Adobe Experience Platform über Azure oder Amazon Web Services (AWS) zu verbinden.

## Voraussetzungen {#prerequisites}

Lesen Sie die folgenden Abschnitte für die erforderliche Einrichtung, die Sie durchführen müssen, bevor Sie Ihr [!DNL Google BigQuery]-Konto mit Experience Platform verbinden können.

### Zulassungsliste von IP-Adressen

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform über Azure oder Amazon Web Services (AWS) verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform in Azure und AWS](../../ip-address-allow-list.md) .

### Authentifizierung bei Experience Platform auf Azure {#azure}

Sie müssen die folgenden Anmeldeinformationen angeben, um Ihr [!DNL Google BigQuery]-Konto mit Experience Platform auf Azure zu verbinden.

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

Um sich mit einer Kombination aus OAuth 2.0 und einfacher Authentifizierung zu authentifizieren, geben Sie die entsprechenden Werte für die folgenden Anmeldeinformationen an.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `project` | Das Projekt ist die Organisationseinheit auf Basisebene für Ihre [!DNL Google Cloud] Ressourcen, einschließlich [!DNL Google BigQuery]. |
| `clientID` | Die Client-ID ist die Hälfte Ihrer [!DNL Google BigQuery] OAuth 2.0-Anmeldeinformationen. |
| `clientSecret` | Das Client-Geheimnis ist die andere Hälfte Ihrer [!DNL Google BigQuery] OAuth 2.0-Anmeldeinformationen. |
| `refreshToken` | Mit dem Aktualisierungstoken können Sie neue Zugriffstoken für Ihre API abrufen. Zugriffstoken haben eine begrenzte Lebensdauer und können im Laufe Ihres Projekts ablaufen. Sie können das Aktualisierungstoken verwenden, um sich zu authentifizieren und bei Bedarf nachfolgende Zugriffstoken für Ihr Projekt anzufordern. Stellen Sie sicher, dass Ihr Aktualisierungs-Token die folgenden [!DNL Google] OAuth-Bereiche enthält: <ul><li>`https://www.googleapis.com/auth/bigquery`</li><li>`https://www.googleapis.com/auth/cloud-platform`</li></ul> Diese Bereiche ermöglichen es Experience Platform, BigQuery-Aufträge zu senden und Daten aus dem konfigurierten Projekt zu lesen. |
| `largeResultsDataSetId` | (Optional) Die vorab erstellte [!DNL Google BigQuery]-Datensatz-ID, die erforderlich ist, um Unterstützung für große Ergebnismengen zu ermöglichen.<ul><li>Der `largeResultsDataSetId` muss sich auf einen vorab erstellten [!DNL BigQuery]-Datensatz beziehen, der zum Speichern temporärer Tabellen für große Ergebnismengen verwendet wird.</li><li>Der Wert darf nur die Datensatz-ID enthalten (z. B. `marketing_temp_results`), nicht den projektqualifizierten Namen (`my-project.marketing_temp_results` nicht verwenden).</li><li>Der Speicherort (die Region) des Datensatzes, der in `largeResultsDataSetId` angegeben ist, muss mit dem Speicherort der abgefragten Tabellen übereinstimmen.</li><li>Das vom Connector verwendete Konto muss über Berechtigungen zum Lesen und Schreiben temporärer Ergebnisse in diesem Datensatz verfügen. Weisen Sie mindestens die Rolle [!DNL BigQuery Data Editor] für den in `largeResultsDataSetId` angegebenen Datensatz zu.</li></ul> |

#### Erforderliche IAM-Rollen für die [!DNL Google] Identität

Die [!DNL Google] Identität, die zum Generieren der OAuth-Anmeldeinformationen (Client-ID, Client-Geheimnis und refreshToken) verwendet wird, muss im [!DNL Google Cloud] über die folgenden IAM-Rollen verfügen:

- [!DNL BigQuery Job User]
- [!DNL BigQuery Data Viewer]
- [!DNL BigQuery Read Session User]

Diese Rollen stellen sicher, dass Experience Platform [!DNL BigQuery] Aufträge erstellen und ausführen, Daten aus den konfigurierten Tabellen lesen und Lesesitzungen verwenden kann, die vom Connector benötigt werden. Stellen Sie sicher, dass diese Rollen im selben Projekt gewährt werden, das die [!DNL BigQuery] Datensätze enthält, die Sie mit der Quelle verwenden möchten.

Detaillierte Anweisungen zum Generieren von OAuth 2.0-Anmeldeinformationen für [!DNL Google]-APIs finden Sie im folgenden [[!DNL Google] OAuth 2.0-Authentifizierungshandbuch](https://developers.google.com/identity/protocols/oauth2).

>[!TAB Service-Authentifizierung]

Um sich mit der Service-Authentifizierung zu authentifizieren, geben Sie die entsprechenden Werte für die folgenden Anmeldeinformationen an.

**Hinweis**: Ihr Service-Konto muss über ausreichende Berechtigungen verfügen, z. B.: **[!DNL BigQuery Job User]**, **[!DNL BigQuery Data Viewer]**, **[!DNL BigQuery Read Session User]** und **[!DNL BigQuery Data Owner]**, um sich erfolgreich mit der Service-Authentifizierung zu authentifizieren.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `projectId` | Die ID der [!DNL Google BigQuery], für die Sie eine Abfrage durchführen möchten. |
| `keyFileContent` | Die Schlüsseldatei, die zum Authentifizieren des Service-Kontos verwendet wird. Sie können diesen Wert aus dem [[!DNL Google Cloud service accounts] Dashboard](https://console.cloud.google.com) abrufen. Der Inhalt der Schlüsseldatei liegt im JSON-Format vor. Sie müssen dies bei der Authentifizierung bei Experience Platform in [!DNL Base64] kodieren. |
| `largeResultsDataSetId` | (Optional) Die vorab erstellte [!DNL Google BigQuery]-Datensatz-ID, die erforderlich ist, um Unterstützung für große Ergebnismengen zu ermöglichen.<ul><li>Der `largeResultsDataSetId` muss sich auf einen vorab erstellten [!DNL BigQuery]-Datensatz beziehen, der zum Speichern temporärer Tabellen für große Ergebnismengen verwendet wird.</li><li>Der Wert darf nur die Datensatz-ID enthalten (z. B. `marketing_temp_results`), nicht den projektqualifizierten Namen (`my-project.marketing_temp_results` nicht verwenden).</li><li>Der Speicherort (die Region) des Datensatzes, der in `largeResultsDataSetId` angegeben ist, muss mit dem Speicherort der abgefragten Tabellen übereinstimmen.</li><li>Das vom Connector verwendete Konto muss über Berechtigungen zum Lesen und Schreiben temporärer Ergebnisse in diesem Datensatz verfügen. Weisen Sie mindestens die Rolle [!DNL BigQuery Data Editor] für den in `largeResultsDataSetId` angegebenen Datensatz zu.</li></ul> |

Weitere Informationen zur Verwendung von Dienstkonten in [!DNL Google BigQuery] finden Sie im Handbuch unter [Verwendung von Dienstkonten in [!DNL Google BigQuery]](https://cloud.google.com/bigquery/docs/use-service-accounts).

>[!ENDTABS]

### Authentifizierung bei Experience Platform auf AWS {#aws}

Sie müssen die folgenden Anmeldeinformationen angeben, um Ihr [!DNL Google BigQuery]-Konto mit Experience Platform auf AWS zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `projectId` | Die ID der [!DNL Google BigQuery], für die Sie eine Abfrage durchführen möchten. |
| `keyFileContent` | Die Schlüsseldatei, die zum Authentifizieren des Service-Kontos verwendet wird. Sie können diesen Wert aus dem [[!DNL Google Cloud service accounts] Dashboard](https://console.cloud.google.com) abrufen. Der Inhalt der Schlüsseldatei liegt im JSON-Format vor. Sie müssen dies bei der Authentifizierung bei Experience Platform in [!DNL Base64] kodieren. |
| `datasetId` | Die [!DNL Google BigQuery] Datensatz-ID. Diese ID stellt dar, wo sich Ihre Datentabellen befinden. |

## Verbinden von [!DNL Google BigQuery] mit Experience Platform

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Google BigQuery] mit Experience Platform mithilfe von APIs oder der Benutzeroberfläche:

### Verwenden von APIs

- [Erstellen einer Google BigQuery-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/databases/bigquery.md)
- [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

### Verwenden der Benutzeroberfläche

- [Erstellen einer Google BigQuery-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/databases/bigquery.md)
- [Erstellen eines Datenflusses für eine Datenbank-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
