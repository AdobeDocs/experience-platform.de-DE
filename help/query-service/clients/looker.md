---
keywords: Experience Platform;home;popular topics;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: Verbindung mit Suchmaschine
topic: connect
description: Dieses Dokument führt Sie durch die Schritte zur Verbindung von Looker mit dem Adobe Experience Platform Abfrage Service.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 13%

---


# Connect with [!DNL Looker]

Gehen Sie wie folgt vor, um eine Verbindung [!DNL Looker] mit [!DNL Query Service] Adobe Experience Platform herzustellen:

Klicken Sie nach der Anmeldung [!DNL Looker]auf **[!UICONTROL Admin]**, gefolgt von **[!UICONTROL Verbindungen]**.

![](../images/clients/looker/click-admin-connections.png)

Klicken Sie auf dieser Seite auf **Neue Verbindung**.

![](../images/clients/looker/click-new-connection.png)

Von hier aus können Sie die Details zu den Verbindungseinstellungen ausfüllen.

![](../images/clients/looker/new-connection.png)

- **Name:** Der Name Ihrer Verbindung.
- **Dialekt:** Das für die SQL-Datenbank verwendete Dialekt. [!DNL Query Service] verwendet **[!DNL PostgreSQL]**.
- **Host und Anschluss:** Der Host-Endpunkt und sein Anschluss für [!DNL Query Service].
- **Datenbank**: Die zu verwendende Datenbank.
- **Benutzername und Kennwort:** Die Anmeldeinformationen, die verwendet werden. Der Benutzername wird in Form von `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>For more information on finding your host and port, database name, and login credentials, visit the [credentials page on Platform](https://platform.adobe.com/query/configuration). To find your credentials, log in to [!DNL Platform], click **[!UICONTROL Queries]**, then click **[!UICONTROL Credentials]**.

After inputting your connection details, click on **[!UICONTROL Test These Settings]** to ensure your credentials work properly. Wenn dies der Fall ist, wird unten eine Meldung angezeigt, die Ihnen mitteilt, dass Sie eine Verbindung herstellen können. Wenn Ihre Verbindung wirklich erfolgreich ist, klicken Sie auf **[!UICONTROL Hinzufügen Verbindung]** , um Ihre Verbindung zu erstellen.

![](../images/clients/looker/click-test-connection.png)

## Nächste Schritte

Jetzt, wo Sie mit verbunden sind [!DNL Query Service], können Sie Abfragen [!DNL Looker] schreiben. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../creating-queries/creating-queries.md).