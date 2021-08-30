---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Aqua Data Studio; Aqua Data Studio; Verbindung mit Query Service;
solution: Experience Platform
title: Aqua Data Studio mit Query Service verbinden
topic-legacy: connect
description: In diesem Dokument werden die Schritte zum Verbinden von Aqua Data Studio mit Query Service von Adobe Experience Platform erläutert.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 20%

---

# Verbinden von [!DNL Aqua Data Studio] mit Query Service

In diesem Dokument werden die Schritte zum Verbinden von [!DNL Aqua Data Studio] mit Adobe Experience Platform [!DNL Query Service] beschrieben.

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL Aqua Data Studio] haben und mit der Navigation in der Benutzeroberfläche vertraut sind. Weitere Informationen zu [!DNL Aqua Data Studio] finden Sie in der [offiziellen [!DNL Aqua Data Studio] Dokumentation](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

Nach der Installation von [!DNL Aqua Data Studio] müssen Sie zunächst den Server registrieren. Wählen Sie im Hauptmenü **[!DNL Server]**, gefolgt von **[!DNL Register Server]** aus.

![](../images/clients/aqua-data-studio/register-server.png)

Das Dialogfeld **[!DNL Register Server]** wird angezeigt. Wählen Sie auf der Registerkarte **[!DNL General]** die Option **[!DNL PostgreSQL]** aus der Liste auf der linken Seite aus. Ein Dialogfeld wird angezeigt. Geben Sie darin die folgenden Details für die Servereinstellungen ein.

- **[!DNL Name]**: Der Name Ihrer Verbindung.
- **[!DNL Login Name and Password]**: Die Anmeldeinformationen, die verwendet werden. Der Benutzername hat die Form `ORG_ID@AdobeOrg`.
- **[!DNL Host and Port]**: Der Host-Endpunkt und sein Port für  [!DNL Query Service]. Sie müssen Port 80 verwenden, um eine Verbindung mit [!DNL Query Service] herzustellen.
- **[!DNL Database]:** Die zu verwendende Datenbank.

>[!NOTE]
>
>Weitere Informationen zum Auffinden Ihrer Anmeldedaten, des Hosts, Ports und des Datenbanknamens finden Sie im Handbuch [Anmeldeinformationen](../ui/credentials.md). Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei [!DNL Platform] an, wählen Sie **[!UICONTROL Abfragen]**, gefolgt von **[!UICONTROL Anmeldeinformationen]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Wählen Sie die Registerkarte **[!DNL Driver]** aus. Legen Sie unter **[!DNL Parameters]** den Wert auf `?sslmode=require` fest.

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Nachdem Sie Ihre Verbindungsdetails eingegeben haben, wählen Sie **[!DNL Test Connection]** aus, um sicherzustellen, dass Ihre Anmeldedaten ordnungsgemäß funktionieren. Wenn Ihre Verbindung erfolgreich hergestellt wurde, wählen Sie **[!DNL Save]** aus, um den Server zu registrieren. Die Verbindung wird nach erfolgreicher Registrierung im Dashboard angezeigt und bestätigt, dass Sie jetzt eine Verbindung zum Server herstellen und dessen Schemaobjekte anzeigen können.

## Nächste Schritte

Nachdem Sie eine Verbindung zu [!DNL Query Service] hergestellt haben, können Sie die **[!DNL Query Analyzer]** innerhalb von [!DNL Aqua Data Studio] verwenden, um SQL-Anweisungen auszuführen und zu bearbeiten. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
