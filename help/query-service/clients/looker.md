---
keywords: Experience Platform;home;popular topics;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: Verbindung mit Suchmaschine
topic: connect
description: Dieses Dokument führt Sie durch die Schritte zur Verbindung von Looker mit dem Adobe Experience Platform Abfrage Service.
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 13%

---


# Verbinden mit [!DNL Looker]

Gehen Sie wie folgt vor, um [!DNL Looker] mit [!DNL Query Service] unter Adobe Experience Platform zu verbinden:

Klicken Sie nach der Anmeldung bei [!DNL Looker] auf **[!UICONTROL Admin]**, gefolgt von **[!UICONTROL Verbindungen]**.

![](../images/clients/looker/click-admin-connections.png)

Klicken Sie auf dieser Seite auf **Neue Verbindung**.

![](../images/clients/looker/click-new-connection.png)

Von hier aus können Sie die Details zu den Verbindungseinstellungen ausfüllen.

![](../images/clients/looker/new-connection.png)

- **Name:** Der Name Ihrer Verbindung.
- **Dialekt:** Das für die SQL-Datenbank verwendete Dialekt. [!DNL Query Service] verwendet  **[!DNL PostgreSQL]**.
- **Host und Anschluss:** Der Host-Endpunkt und dessen Anschluss  [!DNL Query Service].
- **Datenbank**: Die zu verwendende Datenbank.
- **Benutzername und Kennwort:** Die Anmeldeinformationen, die verwendet werden. Der Benutzername lautet `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Weitere Informationen zum Auffinden von Host- und Anschluss-, Datenbank- und Anmeldedaten finden Sie auf der Seite [Anmeldedaten unter Plattform](https://platform.adobe.com/query/configuration). Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei [!DNL Platform] an, klicken Sie auf **[!UICONTROL Abfragen]** und dann auf **[!UICONTROL Anmeldeinformationen]**.

Klicken Sie nach Eingabe der Verbindungsdetails auf **[!UICONTROL Diese Einstellungen testen]**, um sicherzustellen, dass Ihre Anmeldedaten ordnungsgemäß funktionieren. Wenn dies der Fall ist, wird unten eine Meldung angezeigt, die Ihnen mitteilt, dass Sie eine Verbindung herstellen können. Wenn Ihre Verbindung tatsächlich erfolgreich ist, klicken Sie auf **[!UICONTROL Hinzufügen Verbindung]**, um Ihre Verbindung zu erstellen.

![](../images/clients/looker/click-test-connection.png)

## Nächste Schritte

Nachdem Sie eine Verbindung mit [!DNL Query Service] hergestellt haben, können Sie [!DNL Looker] verwenden, um Abfragen zu schreiben. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).