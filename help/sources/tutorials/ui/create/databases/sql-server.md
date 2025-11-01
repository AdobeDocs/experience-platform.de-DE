---
title: Erstellen einer Microsoft SQL Server-Source-Verbindung über die Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Microsoft SQL Server-Quellverbindung erstellen.
exl-id: aba4e317-1c59-4999-a525-dba15f8d4df9
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 39%

---

# Erstellen eines Quell-Connectors für [!DNL Microsoft SQL Server] in der Benutzeroberfläche

Lesen Sie dieses Tutorial, um zu erfahren, wie Sie Ihr [!DNL Microsoft SQL Server]-Konto über die Benutzeroberfläche mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL SQL Server]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/databases.md) fortfahren.

### Sammeln erforderlicher Anmeldedaten

Um eine Verbindung zu [!DNL SQL Server] auf [!DNL Experience Platform] herzustellen, müssen Sie die folgende Verbindungseigenschaft angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| Verbindungszeichenfolge | Die mit Ihrem [!DNL Microsoft SQL Server]-Konto verknüpfte Verbindungszeichenfolge. Ihr Verbindungszeichenfolgenmuster hängt davon ab, ob Sie den Servernamen oder Instanznamen für Ihre Datenquelle verwenden:<ul><li>Verbindungszeichenfolge unter Verwendung des Server-Namens: `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Verbindungszeichenfolge mit Instanzname: `Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` <br> `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` </li></ul> |

Weitere Informationen zu den ersten Schritten finden Sie [diesem [!DNL SQL Server] Dokument](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

## Verbinden Ihres [!DNL SQL Server]-Kontos

Wählen Sie in der Benutzeroberfläche von Experience Platform in der linken Navigationsleiste die Option **[!UICONTROL Sources]** , um auf den [!UICONTROL Sources]-Arbeitsbereich zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter *Kategorie* die Option **[!DNL Microsoft SQL Server]** und dann **[!UICONTROL Set up]** aus.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die **[!UICONTROL Set up]** an, wenn eine bestimmte Quelle noch kein authentifiziertes Konto hat. Sobald ein authentifiziertes Konto vorhanden ist, ändert sich diese Option in **[!UICONTROL Add data]**.

![Der Quellkatalog mit der ausgewählten Microsoft SQL Server-Quelle.](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

Die Seite **[!UICONTROL Connect to Microsoft SQL Server]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

>[!BEGINTABS]

>[!TAB Neues Konto erstellen]

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL New account]** aus und geben Sie einen Namen, eine optionale Beschreibung und Ihre -Anmeldeinformationen an.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Connect to source]** aus und warten Sie dann einige Zeit, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle mit den eingegebenen und hervorgehobenen Details zur Quellverbindung.](../../../../images/tutorials/create/microsoft-sql-server/new.png)

>[!TAB Vorhandenes Konto verwenden]

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Existing account]** und dann das Konto, das Sie verwenden möchten, aus dem vorhandenen Kontenkatalog aus.

Wählen Sie **[!UICONTROL Next]** aus, um fortzufahren.

![Die vorhandene Kontoschnittstelle, die eine Liste der vorhandenen Konten anzeigt.](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

>[!ENDTABS]

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL SQL Server]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in zu importieren [!DNL Experience Platform]](../../dataflow/databases.md).
