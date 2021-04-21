---
keywords: Experience Platform;Home;beliebte Themen;Azurblauer Data Explorer;Azure Data Explorer
solution: Experience Platform
title: Übersicht über den Avocent Data Explorer Source Connector
topic-legacy: overview
description: Erfahren Sie, wie Sie Azurblase-Data Explorer mit APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 869bd8bb-51e6-4e0c-a3ec-ff083dda5789
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# (Beta) [!DNL Azure Data Explorer] Connector

>[!NOTE]
>
>Der [!DNL Azure Data Explorer]-Anschluss befindet sich in der Betaversion. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../home.md#terms-and-conditions).

Adobe Experience Platform bietet native Konnektivität für Datenbankanbieter wie [!DNL Microsoft], MySQL und [!DNL Azure]. Sie können Ihre Daten von diesen Systemen in [!DNL Platform] übertragen.

Es werden verschiedene Arten von Drittanbieter-Datenbanken unterstützt, einschließlich relationaler Datenbanken, NoSQL-Datenbanken oder Data Warehouse. Die Unterstützung für Datenbankanbieter umfasst [!DNL Azure Data Explorer].

## Zulassungsliste der IP-Adresse

Eine Liste von IP-Adressen muss einer Zulassungsliste hinzugefügt werden, bevor Sie mit Quellschnittstellen arbeiten können. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Zulassungsliste [IP-Adresse](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>Der [!DNL Azure Data Explorer]-Quellanschluss unterstützt derzeit keine Verbindung mit Plattform für dieselbe Region. Das bedeutet, dass eine Verbindung zu Plattformquellen nicht hergestellt werden kann, wenn Ihre Azurblase-Instanz denselben Netzwerkbereich wie Platform verwendet. Derzeit wird nur die regionenübergreifende Konnektivität unterstützt. Weitere Informationen erhalten Sie von Ihrem Kundenbetreuer für Adoben.

Die nachstehende Dokumentation enthält Informationen dazu, wie [!DNL Azure Data Explorer] mithilfe von APIs oder der Benutzeroberfläche mit [!DNL Platform] verbunden wird:

## Verbinden Sie [!DNL Azure Data Explorer] mit [!DNL Platform] mithilfe von APIs

- [Erstellen einer Azurblauer Data Explorer-Quellverbindung mit der Flow Service API](../../tutorials/api/create/databases/data-explorer.md)
- [Durchsuchen eines Datenbanksystems mit der Flow Service API](../../tutorials/api/explore/database-nosql.md)
- [Erfassen von Daten aus einer Datenbank mithilfe der Flow Service API](../../tutorials/api/collect/database-nosql.md)

## Verbinden Sie [!DNL Azure Data Explorer] mit [!DNL Platform] mithilfe der Benutzeroberfläche

- [Erstellen einer Azurblauer Data Explorer-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/databases/data-explorer.md)
- [Konfigurieren eines Datenflusses für eine Datenbankverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
