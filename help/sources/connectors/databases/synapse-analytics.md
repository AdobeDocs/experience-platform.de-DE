---
keywords: Experience Platform;Startseite;beliebte Themen;Azure synapse Analytics;azure synapse-Analyse;Zusammenfassung;Zusammenfassung
solution: Experience Platform
title: Übersicht über den azure synapse Analytics-Quell-Connector
topic-legacy: overview
description: Erfahren Sie, wie Sie mit APIs oder der Benutzeroberfläche Azure synapse Analytics mit Adobe Experience Platform verbinden.
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 9%

---

# (Beta) [!DNL Azure Synapse Analytics] Connector

Adobe Experience Platform ermöglicht die Erfassung von Daten aus externen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform]-Diensten zu strukturieren, zu beschriften und zu verbessern. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. [!DNL Platform] kann eine Verbindung zu verschiedenen Arten von Datenbanken wie z. B. relationale Datenbanken, NoSQL oder Data Warehouse herstellen. Zu den Datenbankanbietern zählen [!DNL Azure Synapse Analytics].

## Zulassungsliste der IP-Adresse

Eine Liste von IP-Adressen muss einer Zulassungsliste hinzugefügt werden, bevor Sie mit Quellschnittstellen arbeiten können. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Zulassungsliste [IP-Adresse](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>Der [!DNL Azure Synapse Analytics]-Quellanschluss unterstützt derzeit keine Verbindung mit Plattform für dieselbe Region. Das bedeutet, dass eine Verbindung zu Plattformquellen nicht hergestellt werden kann, wenn Ihre Azurblase-Instanz denselben Netzwerkbereich wie Platform verwendet. Derzeit wird nur die regionenübergreifende Konnektivität unterstützt. Weitere Informationen erhalten Sie von Ihrem Kundenbetreuer für Adoben.

Die nachstehende Dokumentation enthält Informationen dazu, wie [!DNL Azure Synapse Analytics] mithilfe von APIs oder der Benutzeroberfläche mit [!DNL Platform] verbunden wird:

## Verbinden Sie [!DNL Azure Synapse Analytics] mit [!DNL Platform] mithilfe von APIs

- [Erstellen einer Azure synapse Analytics-Quellverbindung mit der Flow Service API](../../tutorials/api/create/databases/synapse-analytics.md)
- [Durchsuchen eines Datenbanksystems mit der Flow Service API](../../tutorials/api/explore/database-nosql.md)
- [Erfassen von Daten aus einer Datenbank mithilfe der Flow Service API](../../tutorials/api/collect/database-nosql.md)

## Verbinden Sie [!DNL Azure Synapse Analytics] mit [!DNL Platform] mithilfe der Benutzeroberfläche

- [Erstellen einer Azure synapse Analytics-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/databases/synapse-analytics.md)
- [Konfigurieren eines Datenflusses für eine Datenbankverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
