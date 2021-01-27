---
keywords: Experience Platform;home;popular topics;query service;Query service;Aqua Data Studio;Aqua data studio;connect to query service;
solution: Experience Platform
title: Anbinden an Aqua Data Studio
topic: connect
description: In diesem Dokument werden die Schritte zum Verbinden von Aqua Data Studio mit Query Service von Adobe Experience Platform erläutert.
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 74%

---


# Verbinden mit [!DNL Aqua Data Studio]

Dieses Dokument führt Sie durch die Schritte zum Verbinden von [!DNL Aqua Data Studio] mit Adobe Experience Platform [!DNL Query Service].

Nach der Installation von [!DNL Aqua Data Studio] müssen Sie zunächst den Server registrieren. Klicken Sie im Hauptmenü auf **[!UICONTROL Server]** und dann auf **[!UICONTROL Server registrieren]**.

![](../images/clients/aqua-data-studio/register-server.png)

Das Dialogfeld **[!UICONTROL Server registrieren]** wird angezeigt. Wählen Sie auf der Registerkarte **[!UICONTROL Allgemein]** die Option **[!UICONTROL PostgreSQL]** aus der Liste links aus. Ein Dialogfeld wird angezeigt. Geben Sie darin die folgenden Details für die Servereinstellungen ein.

- **[!UICONTROL Name]**: Der Name Ihrer Verbindung.
- **[!UICONTROL Anmeldename und Passwort]**: Die Anmeldeinformationen, die verwendet werden. Der Benutzername hat die Form `ORG_ID@AdobeOrg`.
- **[!UICONTROL Host und Port]**: Der Host-Endpunkt und sein Port für [!DNL Query Service]. Sie müssen Port 80 verwenden, um eine Verbindung mit [!DNL Query Service] herzustellen.
- **[!UICONTROL Datenbank]:** Die zu verwendende Datenbank.

>[!NOTE]
>
> Weitere Informationen dazu, wie Sie Ihre Anmeldeinformationen sowie Host, Port und Datenbankname finden, finden Sie auf der [Seite zu Anmeldeinformationen auf Platform](https://platform.adobe.com/query/configuration). Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei [!DNL Platform] an, klicken Sie auf **[!UICONTROL Abfragen]** und dann auf **[!UICONTROL Anmeldeinformationen]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Wählen Sie die Registerkarte **[!UICONTROL Treiber]** aus. Legen Sie unter **[!UICONTROL Parameter]** den Wert `?sslmode=require` fest.

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Klicken Sie nach Eingabe der Verbindungsdetails auf **[!UICONTROL Verbindung testen]**, um sicherzustellen, dass Ihre Anmeldeinformationen ordnungsgemäß funktionieren. Wenn Ihre Verbindung erfolgreich hergestellt wurde, klicken Sie auf **[!UICONTROL Speichern]**, um den Server zu registrieren. Die Verbindung wird nach erfolgreicher Registrierung auf dem **Dashboard** angezeigt und bestätigt, dass Sie jetzt eine Verbindung mit dem Server herstellen und die ihm zugehörigen Schema-Objekte einsehen können.

## Nächste Schritte

Nachdem Sie eine Verbindung zu [!DNL Query Service] hergestellt haben, können Sie den **[!UICONTROL Abfrage Analyzer]** in [!DNL Aqua Data Studio] verwenden, um SQL-Anweisungen auszuführen und zu bearbeiten. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).