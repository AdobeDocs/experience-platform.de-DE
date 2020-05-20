---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verbindung mit Aqua Data Studio
topic: connect
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# Verbindung mit Aqua Data Studio

In diesem Dokument werden die Schritte zum Verbinden von Aqua Data Studio mit dem Adobe Experience Platform Abfrage Service beschrieben.

Nach der Installation von Aqua Data Studio müssen Sie zunächst den Server registrieren. Klicken Sie im Hauptmenü auf **Server** und dann auf Server **registrieren**.

![](../images/clients/aqua-data-studio/register-server.png)

Das Dialogfeld Server *registrieren* wird angezeigt. Wählen Sie auf der Registerkarte &quot; *Allgemein* &quot;links in der Liste die Option &quot; **PostgreSQL** &quot;aus. Geben Sie im angezeigten Dialogfeld die folgenden Details für die Servereinstellungen ein.

- **Name**: Der Name Ihrer Verbindung.
- **Anmeldename und Kennwort**: Die Anmeldeinformationen, die verwendet werden. Der Benutzername hat die Form `ORG_ID@AdobeOrg`.
- **Host und Anschluss**: Der Host-Endpunkt und sein Anschluss für den Abfrage-Dienst.
- **Datenbank:** Die zu verwendende Datenbank.

>[!NOTE] Weitere Informationen zum Auffinden Ihrer Anmeldeinformationen, des Host-, Port- und Datenbanknamens finden Sie auf der Seite &quot; [Anmeldeinformationen&quot;auf der Plattform](https://platform.adobe.com/query/configuration). Melden Sie sich zur Suche nach Ihren Anmeldeinformationen bei Platform an, klicken Sie auf **Abfragen** und dann auf **Anmeldeinformationen**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Select the **Driver** tab. Legen Sie unter *Parameter* den Wert als `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Klicken Sie nach Eingabe der Verbindungsdetails auf **Verbindung** testen, um sicherzustellen, dass Ihre Anmeldeinformationen ordnungsgemäß funktionieren. Wenn Ihre Verbindung erfolgreich hergestellt wurde, klicken Sie auf **Speichern** , um den Server zu registrieren. Die Verbindung wird nach erfolgreicher Registrierung auf dem *Dashboard* angezeigt und bestätigt, dass Sie jetzt eine Verbindung mit dem Server herstellen und die zugehörigen Schema-Objekte Ansichten vornehmen können.

## Nächste Schritte

Nachdem Sie mit dem Abfrage Service verbunden sind, können Sie mit dem *Abfrage Analyzer* in Aqua Data Studio SQL-Anweisungen ausführen und bearbeiten. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Handbuch [laufender Abfragen](../creating-queries/creating-queries.md).