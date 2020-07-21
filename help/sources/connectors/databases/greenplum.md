---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: GreenPlum-Anschluss
topic: overview
translation-type: tm+mt
source-git-commit: 3b5e76afea5689dbd59f64f6192e6ef2a6acb7d3
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# (Beta) [!DNL GreenPlum] -Anschluss

>[!NOTE]
>Der [!DNL GreenPlum] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../home.md#terms-and-conditions) Quellen.

Adobe Experience Platform bietet native Konnektivität für Datenbankanbieter wie [!DNL Microsoft], MySQL und [!DNL Azure]. Sie können Ihre Daten von diesen Systemen in [!DNL Platform]importieren.

Es werden verschiedene Arten von Drittanbieter-Datenbanken unterstützt, einschließlich relationaler Datenbanken, NoSQL oder data warehouse. Die Unterstützung von Datenbankanbietern umfasst [!DNL GreenPlum].

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

Die nachstehende Dokumentation enthält Informationen zum Herstellen einer Verbindung [!DNL GreenPlum] mit [!DNL Platform] APIs oder der Benutzeroberfläche:

## Verbindung [!DNL GreenPlum] mit [!DNL Platform] APIs

- [Erstellen eines GreenPlum-Connectors mithilfe der Flow Service API](../../tutorials/api/create/databases/greenplum.md)
- [Durchsuchen eines Datenbanksystems mit der Flow Service API](../../tutorials/api/explore/database-nosql.md)
- [Erfassen von Daten aus einer Datenbank mithilfe der Flow Service API](../../tutorials/api/collect/database-nosql.md)

## Verbindung [!DNL GreenPlum] mit der [!DNL Platform] Benutzeroberfläche

- [Erstellen eines GreenPlum-Quellconnectors in der Benutzeroberfläche](../../tutorials/ui/create/databases/greenplum.md)
- [Konfigurieren eines Datenflusses für einen Datenbankanschluss in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)