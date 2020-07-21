---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: MariaDB-Anschluss
topic: overview
translation-type: tm+mt
source-git-commit: 3b5e76afea5689dbd59f64f6192e6ef2a6acb7d3
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 17%

---


# (Beta) [!DNL MariaDB] -Anschluss

>[!NOTE]
>Der [!DNL MariaDB] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../home.md#terms-and-conditions) Quellen.

Adobe Experience Platform allows data to be ingested from external sources while providing you with the ability to structure, label, and enhance incoming data using [!DNL Platform] services. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. [!DNL Platform] kann eine Verbindung zu verschiedenen Datenbanktypen wie relationaler Datenbank, NoSQL oder data warehouse herstellen. Zu den Datenbankanbietern zählen [!DNL MariaDB].

## Zulassungsliste der IP-Adresse

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

Die nachstehende Dokumentation enthält Informationen zum Herstellen einer Verbindung [!DNL MariaDB] mit [!DNL Platform] APIs oder der Benutzeroberfläche:

## Verbindung [!DNL MariaDB] mit [!DNL Platform] APIs

- [Erstellen eines MariaDB-Connectors mit der Flow Service API](../../tutorials/api/create/databases/mariadb.md)
- [Durchsuchen eines Datenbanksystems mit der Flow Service API](../../tutorials/api/explore/database-nosql.md)
- [Erfassen von Daten aus einer Datenbank mithilfe der Flow Service API](../../tutorials/api/collect/database-nosql.md)

## Verbindung [!DNL MariaDB] mit der [!DNL Platform] Benutzeroberfläche

- [Erstellen eines Quell-Connectors für MariaDB über die Benutzeroberfläche](../../tutorials/ui/create/databases/mariadb.md)
- [Konfigurieren eines Datenflusses für einen Datenbankanschluss in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)