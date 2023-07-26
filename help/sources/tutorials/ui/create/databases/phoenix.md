---
title: Verbinden Ihres Phoenix-Kontos über die Experience Platform-Benutzeroberfläche
description: Erfahren Sie, wie Sie Ihr Phoenix-Konto verbinden und Daten aus Ihrer Phoenix-Datenbank über die Benutzeroberfläche in die Experience Platform übertragen können.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: b7e42eb180b8f16344afedadf763c33bcf22fa35
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 25%

---

# Verbinden Sie [!DNL Phoenix] Konto für die Experience Platform über die Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie Ihre [!DNL Phoenix] -Konto und -Daten aus Ihrem [!DNL Phoenix] Datenbank zu Experience Platform.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine authentifizierte [!DNL Phoenix] -Konto verwenden, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Datenfluss für eine Datenbank konfigurieren](../../dataflow/databases.md).

### Sammeln erforderlicher Anmeldeinformationen

Um auf Ihre [!DNL Phoenix] -Konto in Experience Platform verwenden, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Host | Die IP-Adresse oder der Hostname der [!DNL Phoenix] Server. |
| Port | Der TCP-Port, der die [!DNL Phoenix] -Server verwendet , um auf Client-Verbindungen zu warten. Wenn Sie eine Verbindung zu [!DNL Azure HDInsights], und geben Sie dann den Anschluss als 443 an. Wenn dieser Parameter nicht angegeben wird, wird der Standardwert 8765 verwendet. |
| HTTP-Pfad | Die Teil-URL, die der [!DNL Phoenix] Server. Geben Sie /hbasephoenix0 an, wenn Sie die [!DNL Azure HDInsights] Cluster. |
| Benutzername | Der Benutzername, mit dem Sie auf die [!DNL Phoenix] Server. |
| Kennwort | Das dem Benutzer entsprechende Kennwort. |
| Enable SSL | Ein Umschalter, der angibt, ob die Verbindungen zum Server mit SSL verschlüsselt sind. |

Weitere Informationen zu den ersten Schritten finden Sie unter [this [!DNL Phoenix] Dokument](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

Nachdem Sie die erforderlichen Anmeldedaten erfasst haben, können Sie die folgenden Schritte ausführen, um Ihre [!DNL Phoenix] -Konto in die Experience Platform.

## Verbinden Ihres [!DNL Phoenix]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** über das linke Navigationsmenü aus, um auf den Arbeitsbereich &quot;Quellen&quot;zuzugreifen. Die *[!UICONTROL Katalog]* -Bildschirm zeigt eine Vielzahl von Quellen an, die im Experience Platform-Quellkatalog verfügbar sind.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie eine bestimmte Quelle mithilfe der Suchoption finden.

Auswählen **[!UICONTROL Datenbanken]** aus der Liste der Quellkategorien und wählen Sie **[!UICONTROL Daten hinzufügen]** aus dem [!DNL Phoenix] Karte.

>[!TIP]
>
>Quellen im Quellkatalog können abhängig vom Status der Quelle unterschiedliche Eingabeaufforderungen anzeigen.
> 
>* **[!UICONTROL Daten hinzufügen]** bedeutet, dass der ausgewählten Quelle bereits authentifizierte Konten zugeordnet sind.
>
>* **[!UICONTROL Einrichten]** bedeutet, dass Sie Anmeldeinformationen angeben und ein neues Konto authentifizieren müssen, um die ausgewählte Quelle verwenden zu können.

![Der Quellkatalog auf der Experience Platform-Benutzeroberfläche mit der ausgewählten Phoenix-Quellkarte.](../../../../images/tutorials/create/phoenix/catalog.png)

Die **[!UICONTROL Verbindung zu Phoenix herstellen]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

>[!BEGINTABS]

>[!TAB Vorhandenes Phoenix-Konto verwenden]

Um ein vorhandenes Konto zu verwenden, wählen Sie [!UICONTROL Vorhandenes Konto] und dann das Konto, das Sie verwenden möchten, aus der angezeigten Liste aus. Wählen Sie zum Abschluss [!UICONTROL Nächste] um fortzufahren.

![Eine Liste authentifizierter Phoenix-Datenbankkonten, die bereits in Ihrem Unternehmen vorhanden sind.](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB Neues Phoenix-Konto erstellen]

Um ein neues Konto zu verwenden, wählen Sie [!UICONTROL Neues Konto] und geben Sie einen Namen, eine Beschreibung und Ihre [!DNL Phoenix] Authentifizierungsberechtigungen. Wählen Sie zum Abschluss [!UICONTROL Verbindung mit Quelle herstellen] und lassen einige Sekunden zu, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle, in der Sie Authentifizierungsberechtigungen angeben und ein Phoenix-Konto erstellen können.](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Phoenix]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [Datenfluss konfigurieren, um Daten in Experience Platform zu übertragen](../../dataflow/databases.md).
