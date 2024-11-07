---
title: Verbinden Ihres Phoenix-Kontos über die Experience Platform-Benutzeroberfläche
description: Erfahren Sie, wie Sie Ihr Phoenix-Konto verbinden und Daten aus Ihrer Phoenix-Datenbank über die Benutzeroberfläche zum Experience Platform übertragen.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: a32d0d7ed7d18454099d2b55b3f6809cfbcd9b62
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 21%

---

# Verbinden Sie Ihr [!DNL Phoenix]-Konto über die Benutzeroberfläche mit Experience Platform.

>[!IMPORTANT]
>
>Die Quelle [!DNL Phoenix] wird Ende Mai 2025 nicht mehr unterstützt.

In diesem Tutorial erfahren Sie, wie Sie Ihr [!DNL Phoenix]-Konto verbinden und Daten aus Ihrer [!DNL Phoenix]-Datenbank an Experience Platform übertragen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein authentifiziertes [!DNL Phoenix] -Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Konfigurieren eines Datenflusses für eine Datenbank [ fortfahren.](../../dataflow/databases.md)

### Sammeln erforderlicher Anmeldedaten

Um auf Ihr [!DNL Phoenix] -Konto auf dem Experience Platform zuzugreifen, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Host | Die IP-Adresse oder der Hostname des [!DNL Phoenix] -Servers. |
| Port | Der TCP-Port, den der [!DNL Phoenix] -Server verwendet, um auf Clientverbindungen zu warten. Wenn Sie eine Verbindung zu [!DNL Azure HDInsights] herstellen, geben Sie den Port als 443 an. Wenn dieser Parameter nicht angegeben wird, wird der Standardwert 8765 verwendet. |
| HTTP-Pfad | Die Teil-URL, die dem [!DNL Phoenix] -Server entspricht. Geben Sie /hbasephoenix0 an, wenn Sie den [!DNL Azure HDInsights]-Cluster verwenden. |
| Benutzername | Der Benutzername, mit dem Sie auf den [!DNL Phoenix] -Server zugreifen. |
| Kennwort | Das dem Benutzer entsprechende Kennwort. |
| Enable SSL | Ein Umschalter, der angibt, ob die Verbindungen zum Server mit SSL verschlüsselt sind. |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem [!DNL Phoenix] Dokument](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Phoenix]-Konto mit Experience Platform zu verbinden.

## Verbinden Ihres [!DNL Phoenix]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Quellen]** aus, um auf den Arbeitsbereich &quot;Quellen&quot;zuzugreifen. Der Bildschirm *[!UICONTROL Katalog]* enthält eine Vielzahl von Quellen, die im Experience Platform-Quellkatalog verfügbar sind.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie eine bestimmte Quelle mithilfe der Suchoption finden.

Wählen Sie **[!UICONTROL Datenbanken]** aus der Liste der Quellkategorien und dann **[!UICONTROL Daten hinzufügen]** aus der Karte [!DNL Phoenix].

>[!TIP]
>
>Quellen im Quellkatalog können abhängig vom Status der Quelle unterschiedliche Eingabeaufforderungen anzeigen.
> 
>* **[!UICONTROL Daten hinzufügen]** bedeutet, dass Ihrer ausgewählten Quelle vorhandene authentifizierte Konten zugeordnet sind.
>
>* **[!UICONTROL Einrichten]** bedeutet, dass Sie Anmeldeinformationen angeben und ein neues Konto authentifizieren müssen, um die ausgewählte Quelle verwenden zu können.

![Der Quellkatalog auf der Experience Platform-Benutzeroberfläche mit ausgewählter Phoenix-Quellkarte.](../../../../images/tutorials/create/phoenix/catalog.png)

Die Seite **[!UICONTROL Verbindung zu Phoenix herstellen]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

>[!BEGINTABS]

>[!TAB Vorhandenes Phoenix-Konto verwenden]

Um ein vorhandenes Konto zu verwenden, wählen Sie [!UICONTROL Vorhandenes Konto] und dann das Konto, das Sie verwenden möchten, aus der angezeigten Liste aus. Wenn Sie fertig sind, wählen Sie [!UICONTROL Weiter] aus, um fortzufahren.

![Eine Liste authentifizierter Phoenix-Datenbankkonten, die bereits in Ihrem Unternehmen vorhanden sind.](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB Erstellen eines neuen Phoenix-Kontos]

Um ein neues Konto zu verwenden, wählen Sie [!UICONTROL Neues Konto] aus und geben Sie einen Namen, eine Beschreibung und Ihre [!DNL Phoenix]-Authentifizierungsberechtigungen ein. Wenn Sie fertig sind, wählen Sie [!UICONTROL Mit Quelle verbinden] und warten Sie einige Sekunden, bis die neue Verbindung hergestellt wird.

![Die neue Kontoschnittstelle, über die Sie Authentifizierungsberechtigungen angeben und ein Phoenix-Konto erstellen können.](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Phoenix]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen Datenfluss [konfigurieren, um Daten in Experience Platform](../../dataflow/databases.md) zu importieren.
