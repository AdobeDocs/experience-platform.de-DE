---
keywords: Experience Platform;home;popular topics;Azure Table Storage;azure table storage;ATS;ats
solution: Experience Platform
title: Datenspeicherung-Stecker
topic: overview
description: Die nachstehende Dokumentation beschreibt, wie Sie die Datenspeicherung von Blauen Tabellen mit APIs oder der Benutzeroberfläche mit der Plattform verbinden.
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 11%

---


# (Beta) [!DNL Azure Table Storage] -Anschluss

>[!NOTE]
>
>Der [!DNL Azure Table Storage] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../home.md#terms-and-conditions) Quellen.

Adobe Experience Platform allows data to be ingested from external sources while providing you with the ability to structure, label, and enhance incoming data using [!DNL Platform] services. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. [!DNL Platform] kann eine Verbindung zu verschiedenen Arten von Datenbanken wie z. B. relationale Datenbanken, NoSQL oder Data Warehouse herstellen. Zu den Datenbankanbietern zählen [!DNL Azure Table Storage].

## ZULASSUNGSLISTE der IP-Adresse

Die folgenden IP-Adressen müssen einer Zulassungsliste hinzugefügt werden, bevor Sie mit Quellschnittstellen arbeiten können. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen.

### Ost-USA-Region

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### Westeuropa

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Australien Osten

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

Die nachstehende Dokumentation enthält Informationen zum Herstellen einer Verbindung [!DNL Azure Table Storage] mit [!DNL Platform] APIs oder der Benutzeroberfläche:

## Verbindung [!DNL Azure Table Storage] mit [!DNL Platform] APIs

- [Erstellen eines Azurblauen Datenspeicherung-Connectors mit der Flow Service API](../../tutorials/api/create/databases/ats.md)
- [Durchsuchen eines Datenbanksystems mit der Flow Service API](../../tutorials/api/explore/database-nosql.md)
- [Erfassen von Daten aus einer Datenbank mithilfe der Flow Service API](../../tutorials/api/collect/database-nosql.md)

## Verbindung [!DNL Azure Table Storage] mit der [!DNL Platform] Benutzeroberfläche

- [Erstellen eines Quellconnectors für die Datenspeicherung eines Blauen Diagramms in der Benutzeroberfläche](../../tutorials/ui/create/databases/ats.md)
- [Konfigurieren eines Datenflusses für einen Datenbankanschluss in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)