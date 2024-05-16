---
title: Erstellen einer Microsoft SQL Server-Quellverbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Microsoft SQL Server-Quellverbindung erstellen.
exl-id: aba4e317-1c59-4999-a525-dba15f8d4df9
source-git-commit: 1828dd76e9ff317f97e9651331df3e49e44efff5
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 45%

---

# Erstellen eines Quell-Connectors für [!DNL Microsoft SQL Server] in der Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie Ihre [!DNL Microsoft SQL Server] -Konto in der -Benutzeroberfläche zu Adobe Experience Platform hinzugefügt.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL SQL Server]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/databases.md) fortfahren.

### Sammeln erforderlicher Anmeldeinformationen

Um eine Verbindung zu [!DNL SQL Server] on [!DNL Platform]müssen Sie die folgende Verbindungseigenschaft angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| Verbindungszeichenfolge | Die Verbindungszeichenfolge, die Ihrer [!DNL Microsoft SQL Server] -Konto. Ihr Verbindungszeichenfolgen-Muster hängt davon ab, ob Sie den Servernamen oder Instanznamen für Ihre Datenquelle verwenden:<ul><li>Verbindungszeichenfolge mit dem Servernamen: `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Verbindungszeichenfolge mit Instanzname:`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |

Weitere Informationen zu den ersten Schritten finden Sie unter [this [!DNL SQL Server] Dokument](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

## Verbinden Ihres [!DNL SQL Server]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem *Datenbanken* category, select **[!DNL Microsoft SQL Server]** und wählen Sie **[!UICONTROL Einrichten]**.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die **[!UICONTROL Einrichten]** -Option, wenn eine bestimmte Quelle noch kein authentifiziertes Konto hat. Sobald ein authentifiziertes Konto existiert, wird diese Option in **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog mit der ausgewählten Microsoft SQL Server-Quelle.](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

Die **[!UICONTROL Verbindung zu Microsoft SQL Server herstellen]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

>[!BEGINTABS]

>[!TAB Neues Konto erstellen]

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie einen Namen, eine optionale Beschreibung und Ihre Anmeldeinformationen ein.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle mit den eingegebenen und hervorgehobenen Details zur Quellverbindung.](../../../../images/tutorials/create/microsoft-sql-server/new.png)

>[!TAB Vorhandenes Konto verwenden]

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und wählen Sie dann das Konto aus, das Sie verwenden möchten, aus dem vorhandenen Kontokatalog.

Klicken Sie auf **[!UICONTROL Weiter]**, um fortzufahren.

![Die vorhandene Kontoschnittstelle, in der eine Liste der vorhandenen Konten angezeigt wird.](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

>[!ENDTABS]

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL SQL Server]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in [!DNL Platform]](../../dataflow/databases.md).
