---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; Query Service; Looker; Looker; Verbindung mit Query Service
solution: Experience Platform
title: Verbinden von Looker mit Query Service
topic-legacy: connect
description: In diesem Dokument werden die Schritte zum Verbinden von Looker mit dem Adobe Experience Platform Query Service beschrieben.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 5%

---

# Verbinden [!DNL Looker] zu Query Service

In diesem Dokument werden die Schritte zum Verbinden von [!DNL Looker] mit Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL Looker] und sind mit dem Navigieren in der Benutzeroberfläche vertraut. Weitere Informationen [!DNL Looker] finden Sie im Abschnitt [offiziell [!DNL Looker] Dokumentation](https://docs.looker.com/).

Nach der Anmeldung bei [!DNL Looker]auswählen **[!DNL Admin]**, gefolgt von **[!DNL Connections]**.

![Die [!DNL Looker] Dashboard mit im Admin-Dropdown-Menü hervorgehobenen Verbindungen.](../images/clients/looker/click-admin-connections.png)

Wählen Sie auf dieser Seite **[!DNL New Connection]**.

![Der Arbeitsbereich Verbindungen mit neuer Verbindung wurde hervorgehoben.](../images/clients/looker/click-new-connection.png)

Von hier aus können Sie die Details für die Verbindungsparameter ausfüllen.

![Die Seite mit den Verbindungsparametern für eine neue Verbindung.](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** Der Name Ihrer Verbindung.
- **[!DNL Dialect]:** Das für die SQL-Datenbank verwendete Dialogfeld. [!DNL Query Service] uses **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** Der Host-Endpunkt und sein Port für [!DNL Query Service].
- **[!DNL Database]:** Die zu verwendende Datenbank.
- **[!DNL Username and Password]:** Die Anmeldeinformationen, die verwendet werden. Der Benutzername lautet wie folgt: `ORG_ID@AdobeOrg`.
- **SSL**: Aktivieren Sie SSL, um eine sichere Verbindung im Netzwerk sicherzustellen.

>[!IMPORTANT]
>
>Siehe [[!DNL Query Service] SSL-Dokumentation](./ssl-modes.md) Erfahren Sie mehr über die SSL-Unterstützung für Drittanbieterverbindungen zu Adobe Experience Platform Query Service und über die Verbindung mit `verify-full` SSL-Modus.

Weitere Informationen zum Auffinden Ihres Hosts und Ports, des Datenbanknamens und der Anmeldeinformationen finden Sie in der [Handbuch zu Anmeldeinformationen](../ui/credentials.md). Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei [!DNL Platform], wählen Sie **[!UICONTROL Abfragen]**, gefolgt von **[!UICONTROL Anmeldeinformationen]**.

Nachdem Sie Ihre Verbindungsdetails eingegeben haben, wählen Sie **[!DNL Test These Settings]** , um sicherzustellen, dass Ihre Anmeldeinformationen ordnungsgemäß funktionieren. Wenn dies der Fall ist, wird unten eine Meldung angezeigt, die angibt, dass Sie eine Verbindung herstellen können. Wenn Ihre Verbindung tatsächlich erfolgreich hergestellt wurde, wählen Sie **[!DNL Add Connection]** , um Ihre Verbindung herzustellen.

![Die Seite Verbindungsparameter für eine neue Verbindung mit Test Diese Einstellungen wurden hervorgehoben.](../images/clients/looker/click-test-connection.png)

## Nächste Schritte

Jetzt, da Sie mit [!DNL Query Service]können Sie [!DNL Looker] , um Abfragen zu schreiben. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
