---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: b616a0c0d49d980644f82bc3af5995b3b17b4c80
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 59%

---

# Adobe Experience Platform – Versionshinweise

**Release-Datum: 29. September 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [Quellen](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für Streaming-Datenflüsse | Sie können jetzt Datenvorbereitungsfunktionen beim Erstellen eines Streaming-Datenflusses für [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] und [!DNL Google PubSub] verwenden. Weitere Informationen finden Sie im Tutorial zum Erstellen eines Streaming-Datenflusses für Cloud-Speicherquellen](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) .[ |

Weitere Informationen zu [!DNL Data Prep] finden Sie unter [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| [!DNL Data Landing Zone] | Sie können jetzt eine [!DNL Data Landing Zone] Quellverbindung mit der [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) oder der [Benutzeroberfläche](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) erstellen. [!DNL Data Landing Zone] ist eine von Platform bereitgestellte  [!DNL Azure Blob] Speicherschnittstelle, über die Sie auf eine sichere, Cloud-basierte Dateispeicheranlage zugreifen können, um Dateien in und aus Platform aufzunehmen und zu extrahieren. Weitere Informationen finden Sie in der [[!DNL Data Landing Zone] Übersicht über ](../../sources/connectors/cloud-storage/data-landing-zone.md). |
| [!DNL Snowflake] | Sie können jetzt eine [!DNL Snowflake] Quellverbindung mit der [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) oder der [Benutzeroberfläche](../../sources/tutorials/ui/create/databases/snowflake.md) erstellen, um Daten aus Ihrer [!DNL Snowflake]-Datenbank in Platform zu übertragen. Weitere Informationen finden Sie in der [[!DNL Snowflake] Übersicht über ](../../sources/connectors/databases/snowflake.md). |
| [!DNL SFTP] Quellverbesserungen | Sie können beim Erstellen einer [!DNL SFTP]-Quellverbindung manuell eine benutzerdefinierte Portnummer festlegen. Weitere Informationen finden Sie in der [[!DNL SFTP] Übersicht über ](../../sources/connectors/cloud-storage/sftp.md). |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
