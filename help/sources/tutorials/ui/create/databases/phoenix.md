---
title: Verbinden Ihres Phoenix-Kontos über die Benutzeroberfläche von Experience Platform
description: Erfahren Sie, wie Sie über die Benutzeroberfläche eine Verbindung mit Ihrem Phoenix-Konto herstellen und Daten aus Ihrer Phoenix-Datenbank in Experience Platform übertragen.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 21%

---

# Verbinden Ihres [!DNL Phoenix]-Kontos mit Experience Platform über die Benutzeroberfläche

>[!WARNING]
>
>Die [!DNL Phoenix] wird Ende Juni 2025 eingestellt.

In diesem Tutorial erfahren Sie, wie Sie Ihr [!DNL Phoenix]-Konto verbinden und Daten aus Ihrer [!DNL Phoenix]-Datenbank in Experience Platform übertragen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein authentifiziertes [!DNL Phoenix]-Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [ eines Datenflusses für eine Datenbank fortfahren](../../dataflow/databases.md).

### Sammeln erforderlicher Anmeldedaten

Um auf Ihr [!DNL Phoenix]-Konto in Experience Platform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Host | Die IP-Adresse oder der Hostname des [!DNL Phoenix]. |
| Port | Der TCP-Port, den der [!DNL Phoenix]-Server verwendet, um auf Client-Verbindungen zu warten. Wenn Sie eine Verbindung zu [!DNL Azure HDInsights] herstellen, geben Sie den Port als 443 an. Wenn dieser Parameter nicht angegeben wird, ist der Standardwert 8765. |
| HTTP-Pfad | Die dem [!DNL Phoenix]-Server entsprechende Teil-URL. Geben Sie /hbasephoenix0 an, wenn Sie den [!DNL Azure HDInsights] Cluster verwenden. |
| Benutzername | Der Benutzername, mit dem Sie auf den [!DNL Phoenix] zugreifen. |
| Kennwort | Das Kennwort, das dem Benutzer entspricht. |
| Enable SSL | Ein Umschalter, der angibt, ob die Verbindungen zum Server mit SSL verschlüsselt werden. |

Weitere Informationen zu den ersten Schritten finden Sie [diesem [!DNL Phoenix] Dokument](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Phoenix]-Konto mit Experience Platform zu verbinden.

## Verbinden Ihres [!DNL Phoenix]-Kontos

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL linken Navigationsbereich die Option]** Quellen“ aus, um auf den Arbeitsbereich Quellen zuzugreifen. Der *[!UICONTROL Katalog]* zeigt eine Vielzahl von Quellen an, die im Experience Platform-Quellkatalog verfügbar sind.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie eine bestimmte Quelle mithilfe der Suchoption finden.

Wählen Sie **[!UICONTROL Datenbanken]** aus der Liste der Quellkategorien und dann **[!UICONTROL Daten hinzufügen]** aus der [!DNL Phoenix] aus.

>[!TIP]
>
>Quellen im Quellkatalog können je nach Status der Quelle unterschiedliche Eingabeaufforderungen anzeigen.
> 
>* **[!UICONTROL Daten hinzufügen]** bedeutet, dass bereits authentifizierte Konten mit Ihrer ausgewählten Quelle verknüpft sind.
>
>* **[!UICONTROL Einrichten]** bedeutet, dass Sie Anmeldeinformationen angeben und ein neues Konto authentifizieren müssen, um Ihre ausgewählte Quelle verwenden zu können.

![Der Quellkatalog auf der Experience Platform-Benutzeroberfläche mit der ausgewählten Phoenix-Quellkarte.](../../../../images/tutorials/create/phoenix/catalog.png)

Die **[!UICONTROL Verbindung zu Phoenix herstellen]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

>[!BEGINTABS]

>[!TAB Vorhandenes Phoenix-Konto verwenden]

Um ein vorhandenes Konto zu verwenden, wählen Sie [!UICONTROL Vorhandenes Konto] und dann das Konto, das Sie verwenden möchten, aus der angezeigten Liste aus. Wenn Sie fertig sind, wählen Sie [!UICONTROL Weiter] aus, um fortzufahren.

![Eine Liste der authentifizierten Phoenix-Datenbankkonten, die bereits in Ihrer Organisation vorhanden sind.](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB Erstellen Sie ein neues Phoenix-Konto]

Um ein neues Konto zu verwenden, wählen Sie [!UICONTROL Neues Konto] und geben Sie einen Namen, eine Beschreibung und Ihre [!DNL Phoenix] Authentifizierungsdaten an. Wenn Sie fertig sind, wählen [!UICONTROL Mit Quelle verbinden] und warten Sie einige Sekunden, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle, über die Sie Authentifizierungsdaten angeben und ein Phoenix-Konto erstellen können.](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Phoenix]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in Experience Platform zu importieren](../../dataflow/databases.md).
