---
title: Snowflake Source Connector - Übersicht
description: Erfahren Sie, wie Sie Snowflake über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 8b0f6eca87deedd8090830e3375d5099bfb0dfc0
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 48%

---

# [!DNL Snowflake] source

>[!IMPORTANT]
>
>* Die [!DNL Snowflake] -Quelle ist im Quellkatalog für Benutzer verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.
>* Standardmäßig wird die Variable [!DNL Snowflake] Quell-Interpreten `null` als leere Zeichenfolge. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um sicherzustellen, dass Ihre `null` Werte richtig geschrieben als `null` in Adobe Experience Platform.
>* Damit Experience Platform Daten erfassen kann, müssen Zeitzonen für alle tabellenbasierten Batch-Quellen auf UTC konfiguriert werden. Der einzige für die [!DNL Snowflake] Quelle ist TIMESTAMP_NTZ mit UTC-Zeit.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. Platform kann eine Verbindung zu verschiedenen Arten von Datenbanken wie z. B. relationalen, NoSQL- oder Data Warehouse-Datenbanken herstellen. Unterstützung für Datenbankanbieter umfasst [!DNL Snowflake].

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

Die folgende Dokumentation enthält Informationen zur Verbindung von [!DNL Snowflake] mit Platform mithilfe von APIs oder der Benutzeroberfläche:

## Verbinden von [!DNL Snowflake] mit Platform mithilfe von APIs

* [Erstellen einer Snowflake-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/databases/snowflake.md)
* [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
* [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

## Verbinden von [!DNL Snowflake] mit Platform über die Benutzeroberfläche

* [Erstellen einer Snowflake-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/databases/snowflake.md)
* [Erstellen eines Datenflusses für eine Datenbankquellenverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
