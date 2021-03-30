---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform für den 31. März 2021.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 8d4270d9168a570fcf92ba60d70dbc8e9af98136
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 50%

---


# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 31. März 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Sources]](#sources)

## [!DNL Sources] {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

Die folgenden Aktualisierungen der Quellen sind in der Experience Platform vom März 2021 enthalten:

| Funktion | Beschreibung |
| ------- | ----------- |
| Beta-Quellen wechseln zu GA | Die folgenden Quellen wurden von der Beta-Version zur GA-Version beworben: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| API-Unterstützung für die Erfassung von komprimierten Dateien | Sie können jetzt komprimierte JSON- oder durch Trennzeichen getrennte Dateien mithilfe von Cloud-Datenspeicherung-Quellen Vorschau und erfassen. Weitere Informationen finden Sie im Lernprogramm zum Erfassen von Cloud-Datenspeicherung-Daten mit APIs](../../sources/tutorials/api/collect/cloud-storage.md).[ |
| Unterstützung für rekursives Hochladen von Dateien in der Benutzeroberfläche | Bei Verwendung einer Cloud-Datenspeicherung können Sie jetzt ganze Ordner rekursiv erfassen. Beim Einfügen eines ganzen Ordners müssen Sie sicherstellen, dass sein Inhalt dasselbe Schema verwendet. Weitere Informationen finden Sie im Tutorial zu [Konfigurieren eines Datenflusses für Cloud-Datenspeicherung-Connectors in der Benutzeroberfläche](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
