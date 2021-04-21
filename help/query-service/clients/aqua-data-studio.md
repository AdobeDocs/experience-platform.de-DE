---
keywords: Experience Platform;Home;beliebte Themen;Abfrage-Dienst;Abfrage-Dienst;Aqua Data Studio;Aqua-Datenstudio;Verbindung zum Abfrage-Dienst
solution: Experience Platform
title: Verbinden von Aqua Data Studio mit Abfrage Service
topic-legacy: connect
description: In diesem Dokument werden die Schritte zum Verbinden von Aqua Data Studio mit Query Service von Adobe Experience Platform erläutert.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 27%

---

# Verbinden Sie [!DNL Aqua Data Studio] mit dem Abfrage-Dienst

Dieses Dokument beschreibt die Schritte zum Verbinden von [!DNL Aqua Data Studio] mit Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Dieses Handbuch setzt voraus, dass Sie bereits Zugriff auf [!DNL Aqua Data Studio] haben und mit der Navigation in der Oberfläche vertraut sind. Weitere Informationen zu [!DNL Aqua Data Studio] finden Sie in der [offiziellen  [!DNL Aqua Data Studio] Dokumentation](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

Nach der Installation von [!DNL Aqua Data Studio] müssen Sie zunächst den Server registrieren. Wählen Sie im Hauptmenü **[!DNL Server]**, gefolgt von **[!DNL Register Server]**.

![](../images/clients/aqua-data-studio/register-server.png)

Das Dialogfeld **[!DNL Register Server]** wird angezeigt. Wählen Sie auf der Registerkarte **[!DNL General]** in der Liste links **[!DNL PostgreSQL]** aus. Ein Dialogfeld wird angezeigt. Geben Sie darin die folgenden Details für die Servereinstellungen ein.

- **[!DNL Name]**: Der Name Ihrer Verbindung.
- **[!DNL Login Name and Password]**: Die Anmeldeinformationen, die verwendet werden. Der Benutzername hat die Form `ORG_ID@AdobeOrg`.
- **[!DNL Host and Port]**: Der Host-Endpunkt und sein Anschluss für  [!DNL Query Service]. Sie müssen Port 80 verwenden, um eine Verbindung mit [!DNL Query Service] herzustellen.
- **[!DNL Database]:** Die zu verwendende Datenbank.

>[!NOTE]
>
> Weitere Informationen dazu, wie Sie Ihre Anmeldeinformationen sowie Host, Port und Datenbankname finden, finden Sie auf der [Seite zu Anmeldeinformationen auf Platform](https://platform.adobe.com/query/configuration). Melden Sie sich zur Suche nach Ihren Anmeldeinformationen bei [!DNL Platform] an, wählen Sie **[!UICONTROL Abfragen]** und anschließend **[!UICONTROL Anmeldeinformationen]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Wählen Sie die Registerkarte **[!DNL Driver]**. Legen Sie unter **[!DNL Parameters]** den Wert auf `?sslmode=require` fest.

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Nachdem Sie die Verbindungsdetails eingegeben haben, wählen Sie **[!DNL Test Connection]**, um sicherzustellen, dass Ihre Anmeldeinformationen ordnungsgemäß funktionieren. Wenn Ihre Verbindung erfolgreich hergestellt wurde, wählen Sie **[!DNL Save]** aus, um den Server zu registrieren. Die Verbindung wird nach erfolgreicher Registrierung auf dem Dashboard angezeigt und bestätigt, dass Sie jetzt eine Verbindung mit dem Server herstellen und die zugehörigen Schema-Objekte Ansicht geben können.

## Nächste Schritte

Nachdem Sie eine Verbindung zu [!DNL Query Service] hergestellt haben, können Sie die **[!DNL Query Analyzer]** innerhalb von [!DNL Aqua Data Studio] verwenden, um SQL-Anweisungen auszuführen und zu bearbeiten. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
