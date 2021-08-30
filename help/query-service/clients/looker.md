---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; Query Service; Looker; Looker; Verbindung mit Query Service
solution: Experience Platform
title: Verbinden von Looker mit Query Service
topic-legacy: connect
description: In diesem Dokument werden die Schritte zum Verbinden von Looker mit dem Adobe Experience Platform Query Service beschrieben.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 9%

---

# Verbinden von [!DNL Looker] mit Query Service

In diesem Dokument werden die Schritte zum Verbinden von [!DNL Looker] mit Adobe Experience Platform [!DNL Query Service] beschrieben.

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL Looker] haben und mit der Navigation in der Benutzeroberfläche vertraut sind. Weitere Informationen zu [!DNL Looker] finden Sie in der [offiziellen [!DNL Looker] Dokumentation](https://docs.looker.com/).

Klicken Sie nach der Anmeldung bei [!DNL Looker] auf **[!DNL Admin]**, gefolgt von **[!DNL Connections]**.

![](../images/clients/looker/click-admin-connections.png)

Wählen Sie auf dieser Seite **[!DNL New Connection]** aus.

![](../images/clients/looker/click-new-connection.png)

Von hier aus können Sie die Details für die Verbindungsparameter ausfüllen.

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** Der Name Ihrer Verbindung.
- **[!DNL Dialect]:** Das für die SQL-Datenbank verwendete Dialogfeld. [!DNL Query Service] verwendet  **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** Der Host-Endpunkt und sein Port für  [!DNL Query Service].
- **[!DNL Database]:** Die zu verwendende Datenbank.
- **[!DNL Username and Password]:** Die Anmeldeinformationen, die verwendet werden. Der Benutzername hat die Form `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Weitere Informationen zum Auffinden Ihres Hosts und Ports, des Datenbanknamens und der Anmeldeinformationen finden Sie im [Handbuch zu Anmeldeinformationen](../ui/credentials.md). Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei [!DNL Platform] an, wählen Sie **[!UICONTROL Abfragen]**, gefolgt von **[!UICONTROL Anmeldeinformationen]**.

Nachdem Sie Ihre Verbindungsdetails eingegeben haben, wählen Sie **[!DNL Test These Settings]** aus, um sicherzustellen, dass Ihre Anmeldedaten ordnungsgemäß funktionieren. Wenn dies der Fall ist, wird unten eine Meldung angezeigt, die angibt, dass Sie eine Verbindung herstellen können. Wenn Ihre Verbindung tatsächlich erfolgreich ist, wählen Sie **[!DNL Add Connection]** aus, um Ihre Verbindung zu erstellen.

![](../images/clients/looker/click-test-connection.png)

## Nächste Schritte

Nachdem Sie sich mit [!DNL Query Service] angemeldet haben, können Sie [!DNL Looker] verwenden, um Abfragen zu schreiben. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
