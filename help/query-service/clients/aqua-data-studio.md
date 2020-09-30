---
keywords: Experience Platform;home;popular topics;query service;Query service;Aqua Data Studio;Aqua data studio;connect to query service;
solution: Experience Platform
title: Anbinden an Aqua Data Studio
topic: connect
description: In diesem Dokument werden die Schritte zum Verbinden von Aqua Data Studio mit Query Service von Adobe Experience Platform erläutert.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 74%

---


# Connect with [!DNL Aqua Data Studio]

This document walks through the steps for connecting [!DNL Aqua Data Studio] with Adobe Experience Platform [!DNL Query Service].

After installing [!DNL Aqua Data Studio], you must first register the server. Klicken Sie im Hauptmenü auf **[!UICONTROL Server]** und dann auf **[!UICONTROL Server registrieren]**.

![](../images/clients/aqua-data-studio/register-server.png)

Das Dialogfeld **[!UICONTROL Server registrieren]** wird angezeigt. Wählen Sie auf der Registerkarte **[!UICONTROL Allgemein]** die Option **[!UICONTROL PostgreSQL]** aus der Liste links aus. Ein Dialogfeld wird angezeigt. Geben Sie darin die folgenden Details für die Servereinstellungen ein.

- **[!UICONTROL Name]**: Der Name Ihrer Verbindung.
- **[!UICONTROL Anmeldename und Passwort]**: Die Anmeldeinformationen, die verwendet werden. Der Benutzername hat die Form `ORG_ID@AdobeOrg`.
- **[!UICONTROL Host und Port]**: Der Host-Endpunkt und sein Port für [!DNL Query Service]. Sie müssen Port 80 verwenden, um eine Verbindung herzustellen [!DNL Query Service].
- **[!UICONTROL Datenbank]:** Die zu verwendende Datenbank.

>[!NOTE]
>
> Weitere Informationen dazu, wie Sie Ihre Anmeldeinformationen sowie Host, Port und Datenbankname finden, finden Sie auf der [Seite zu Anmeldeinformationen auf Platform](https://platform.adobe.com/query/configuration). To find your credentials, log in to [!DNL Platform], click **[!UICONTROL Queries]**, then click **[!UICONTROL Credentials]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Wählen Sie die Registerkarte **[!UICONTROL Treiber]** aus. Legen Sie unter **[!UICONTROL Parameter]** den Wert `?sslmode=require` fest.

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Klicken Sie nach Eingabe der Verbindungsdetails auf **[!UICONTROL Verbindung testen]**, um sicherzustellen, dass Ihre Anmeldeinformationen ordnungsgemäß funktionieren. Wenn Ihre Verbindung erfolgreich hergestellt wurde, klicken Sie auf **[!UICONTROL Speichern]**, um den Server zu registrieren. Die Verbindung wird nach erfolgreicher Registrierung auf dem *Dashboard* angezeigt und bestätigt, dass Sie jetzt eine Verbindung mit dem Server herstellen und die ihm zugehörigen Schema-Objekte einsehen können.

## Nächste Schritte

Now that you have connected to [!DNL Query Service], you can use the **[!UICONTROL Query Analyzer]** within [!DNL Aqua Data Studio] to execute and edit SQL statements. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../creating-queries/creating-queries.md).