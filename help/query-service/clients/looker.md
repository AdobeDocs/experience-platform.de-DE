---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verbindung mit Suchmaschine
topic: connect
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Verbindung mit Suchmaschine

Gehen Sie wie folgt vor, um Looker mit dem Adobe Abfrage Service auf Adobe Experience Platform zu verbinden:

Klicken Sie nach der Anmeldung bei Looker auf **Admin**, gefolgt von **Verbindungen**.

![](../images/clients/looker/click-admin-connections.png)

Klicken Sie auf dieser Seite auf **Neue Verbindung**.

![](../images/clients/looker/click-new-connection.png)

Von hier aus können Sie die Details zu den Verbindungseinstellungen ausfüllen.

![](../images/clients/looker/new-connection.png)

- **Name:** Der Name Ihrer Verbindung.
- **Dialekt:** Das für die SQL-Datenbank verwendete Dialekt. Abfrage Service verwendet **PostgreSQL**.
- **Host und Anschluss:** Der Host-Endpunkt und sein Anschluss für den Abfrage-Dienst.
- **Datenbank:** Die zu verwendende Datenbank.
- **Benutzername und Kennwort:** Die Anmeldeinformationen, die verwendet werden. Der Benutzername wird in Form von `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Weitere Informationen zum Auffinden von Host- und Anschluss-, Datenbanknamen- und Anmeldedaten finden Sie auf der Seite &quot; [Anmeldeinformationen&quot;in der Platform](https://platform.adobe.com/query/configuration). Melden Sie sich zur Suche nach Ihren Anmeldeinformationen bei der Platform an, klicken Sie auf **Abfragen** und dann auf **Anmeldeinformationen**.

Klicken Sie nach Eingabe der Verbindungsdetails auf **Diese Einstellungen** testen, um sicherzustellen, dass Ihre Anmeldedaten ordnungsgemäß funktionieren. Wenn dies der Fall ist, wird unten eine Meldung angezeigt, die Ihnen mitteilt, dass Sie eine Verbindung herstellen können. Wenn Ihre Verbindung wirklich erfolgreich ist, klicken Sie auf **Hinzufügen Verbindung** , um Ihre Verbindung zu erstellen.

![](../images/clients/looker/click-test-connection.png)

## Nächste Schritte

Nachdem Sie sich mit dem Abfrage Service verbunden haben, können Sie mit Looker Abfragen schreiben. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Handbuch [laufender Abfragen](../creating-queries/creating-queries.md).