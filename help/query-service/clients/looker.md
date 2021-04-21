---
keywords: Experience Platform;Home;beliebte Themen;Abfrage-Dienst;Abfrage-Dienst;Suche;Suche;Verbindung mit Abfrage-Dienst herstellen
solution: Experience Platform
title: Connect Looker mit dem Abfrage Service
topic-legacy: connect
description: Dieses Dokument führt Sie durch die Schritte zur Verbindung von Looker mit dem Adobe Experience Platform Abfrage Service.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 11%

---

# Verbinden Sie [!DNL Looker] mit dem Abfrage-Dienst

Dieses Dokument beschreibt die Schritte zum Verbinden von [!DNL Looker] mit Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Dieses Handbuch setzt voraus, dass Sie bereits Zugriff auf [!DNL Looker] haben und mit der Navigation in der Oberfläche vertraut sind. Weitere Informationen zu [!DNL Looker] finden Sie in der [offiziellen  [!DNL Looker] Dokumentation](https://docs.looker.com/).

Wählen Sie nach der Anmeldung bei [!DNL Looker] **[!DNL Admin]** und anschließend **[!DNL Connections]** aus.

![](../images/clients/looker/click-admin-connections.png)

Wählen Sie auf dieser Seite **[!DNL New Connection]**.

![](../images/clients/looker/click-new-connection.png)

Von hier aus können Sie die Details zu den Verbindungseinstellungen ausfüllen.

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** Der Name Ihrer Verbindung.
- **[!DNL Dialect]:** Das für die SQL-Datenbank verwendete Dialekt. [!DNL Query Service] verwendet  **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** Der Host-Endpunkt und sein Anschluss für  [!DNL Query Service].
- **[!DNL Database]:** Die zu verwendende Datenbank.
- **[!DNL Username and Password]:** Die Anmeldeinformationen, die verwendet werden. Der Benutzername lautet `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Weitere Informationen zum Auffinden von Host- und Anschluss-, Datenbank- und Anmeldedaten finden Sie auf der Seite [Anmeldedaten unter Plattform](https://platform.adobe.com/query/configuration). Melden Sie sich zur Suche nach Ihren Anmeldeinformationen bei [!DNL Platform] an, wählen Sie **[!UICONTROL Abfragen]** und anschließend **[!UICONTROL Anmeldeinformationen]**.

Nachdem Sie die Verbindungsdetails eingegeben haben, wählen Sie **[!DNL Test These Settings]**, um sicherzustellen, dass Ihre Anmeldeinformationen ordnungsgemäß funktionieren. Wenn dies der Fall ist, wird unten eine Meldung angezeigt, die angibt, dass Sie eine Verbindung herstellen können. Wenn Ihre Verbindung tatsächlich erfolgreich ist, wählen Sie **[!DNL Add Connection]**, um Ihre Verbindung zu erstellen.

![](../images/clients/looker/click-test-connection.png)

## Nächste Schritte

Nachdem Sie eine Verbindung mit [!DNL Query Service] hergestellt haben, können Sie [!DNL Looker] verwenden, um Abfragen zu schreiben. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
