---
title: Übersicht über den Amazon Redshift Source Connector
description: Erfahren Sie, wie Sie Amazon Redshift mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 75e577dd-a0b0-4f82-a371-5ec9255544f8
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 17%

---

# [!DNL Amazon Redshift]

>[!IMPORTANT]
>
>- Die [!DNL Amazon Redshift] ist im Quellkatalog für Benutzende verfügbar, die Real-Time CDP Ultimate erworben haben.
>
>- Sie können jetzt die [!DNL Amazon Redshift]-Quelle verwenden, wenn Sie Adobe Experience Platform auf Amazon Web Services (AWS) ausführen. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../landing/multi-cloud.md).


Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Experience Platform-Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. Experience Platform kann eine Verbindung zu verschiedenen Datenbanktypen herstellen, z. B. relationale Datenbanken, NoSQL oder Data Warehouses. Die Unterstützung für Datenbankanbieter umfasst [!DNL Amazon Redshift].

## Einrichten der [!DNL Amazon Redshift] für Experience Platform auf Azure {#azure}

Gehen Sie wie folgt vor, um zu erfahren, wie Sie Ihr [!DNL Amazon Redshift] für Experience Platform auf Azure einrichten können.

### Zulassungsliste von IP-Adressen

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform auf Azure verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform auf Azure](../../ip-address-allow-list.md) .

## Einrichten der [!DNL Amazon Redshift] für Experience Platform auf Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../landing/multi-cloud.md).

### AUF DIE ZULASSUNGSLISTE SETZEN IP-Adresse für die Verbindung mit AWS

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform in AWS verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform auf AWS](../../ip-address-allow-list.md) .

## Verbinden von [!DNL Amazon Redshift] mit Experience Platform mithilfe von APIs

- [Verbinden von Amazon Redshift mit Experience Platform mithilfe der Flow Service-API](../../tutorials/api/create/databases/redshift.md)
- [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

## Verbinden von [!DNL Amazon Redshift] mit Experience Platform über die Benutzeroberfläche

- [Erstellen einer Amazon Redshift-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/databases/redshift.md)
- [Erstellen eines Datenflusses für eine Datenbank-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
