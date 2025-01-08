---
title: Übersicht über den Amazon Redshift Source Connector
description: Erfahren Sie, wie Sie Amazon Redshift mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 75e577dd-a0b0-4f82-a371-5ec9255544f8
source-git-commit: dbeeab9182ae67e5c9c691707faeddf04f4e94b2
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 41%

---

# [!DNL Amazon Redshift]

>[!IMPORTANT]
>
>Die [!DNL Amazon Redshift] ist im Quellkatalog für Benutzende verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. Platform kann eine Verbindung zu verschiedenen Datenbanktypen herstellen, z. B. relationale Datenbanken, NoSQL oder Data Warehouses. Die Unterstützung für Datenbankanbieter umfasst [!DNL Amazon Redshift].

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Einrichten einer [!DNL Amazon Redshift] für das Experience Platform auf Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform-Multi-Cloud](../../../landing/multi-cloud.md).

Fügen Sie die folgenden IP-Adressen zu Ihrer Zulassungsliste hinzu, um Ihr [!DNL Amazon Redshift]-Konto mit Experience Platform auf Amazon Web Services (AWS) zu verbinden:

- `34.193.63.59`
- `44.217.93.240`
- `44.194.79.229`

## Verbinden von [!DNL Amazon Redshift] mit Platform mithilfe von APIs

- [Erstellen einer Amazon Redshift-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/databases/redshift.md)
- [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

## Verbinden von [!DNL Amazon Redshift] mit Platform über die Benutzeroberfläche

- [Erstellen einer Amazon Redshift-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/databases/redshift.md)
- [Erstellen eines Datenflusses für eine Datenbank-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
