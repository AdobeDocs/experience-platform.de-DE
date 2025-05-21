---
title: Verbinden von MariaDB mit Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie Ihr MariaDB-Konto mithilfe des Arbeitsbereichs „Quellen“ in der Benutzeroberfläche von Experience Platform mit Experience Platform verbinden.
exl-id: 259ca112-01f1-414a-bf9f-d94caf4c69df
source-git-commit: bca4f40d452f0a5e70a388872a65640d1fd58533
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 19%

---

# Verbinden von [!DNL MariaDB] mit Experience Platform über die Benutzeroberfläche

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihr [!DNL MariaDB]-Konto mithilfe des Arbeitsbereichs „Quellen“ in der Benutzeroberfläche von Experience Platform mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [Echtzeit-Kundenprofil](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine [!DNL MariaDB] Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [ eines Datenflusses ](../../dataflow/databases.md).

### Sammeln erforderlicher Anmeldedaten

Informationen zur Authentifizierung [[!DNL MariaDB]  Sie in ](../../../../connectors/databases/mariadb.md#prerequisites)Übersicht“.

## Navigieren im Quellkatalog

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich *[!UICONTROL Quellen]* zuzugreifen. Wählen Sie die entsprechende Kategorie im Bedienfeld *[!UICONTROL Kategorien]* aus Alternativ können Sie die Suchleiste verwenden, um zur gewünschten Quelle zu navigieren.

Um [!DNL MariaDB] zu verwenden, wählen Sie die Quellkarte **[!UICONTROL MariaDB]** unter *[!UICONTROL Datenbanken]* und dann **[!UICONTROL Einrichten]**.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die Option **[!UICONTROL Einrichten]** an, wenn eine bestimmte Quelle noch kein authentifiziertes Konto hat. Nachdem ein authentifiziertes Konto erstellt wurde, ändert sich diese Option in **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog in der Benutzeroberfläche mit der ausgewählten MariaDB-Karte.](../../../../images/tutorials/create/maria-db/catalog.png)

## Vorhandenes Konto verwenden {#existing}

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das [!DNL MariaDB] Konto aus, das Sie verwenden möchten.

![Die Schnittstelle „Vorhandene Konten“ im Quell-Workflow mit ausgewähltem „Vorhandenes Konto“.](../../../../images/tutorials/create/maria-db/existing.png)

## Neues Konto erstellen {#create}

Wenn Sie noch kein -Konto haben, müssen Sie ein neues Konto erstellen, indem Sie die Authentifizierungsdaten angeben, die Ihrer Quelle entsprechen.

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen an und fügen Sie optional eine Beschreibung für Ihr Konto hinzu.

![Die neue Kontoschnittstelle im Quell-Workflow mit einem Kontonamen und einer optionalen Beschreibung.](../../../../images/tutorials/create/maria-db/new.png)

### Verbindung mit Experience Platform herstellen

Sie können Ihr [!DNL MariaDB]-Konto entweder mit dem Kontoschlüssel oder mit der Standardauthentifizierung mit Experience Platform verbinden.

>[!BEGINTABS]

>[!TAB Authentifizierung mit Kontoschlüssel]

Um die Kontoschlüsselauthentifizierung zu verwenden, wählen Sie **[!UICONTROL Kontoschlüsselauthentifizierung]**, geben Sie Ihre [Verbindungszeichenfolge](../../../../connectors/databases/mariadb.md#azure) an und wählen Sie dann **[!UICONTROL Mit Quelle verbinden]**.

![Die neue Kontoschnittstelle im Quell-Workflow mit ausgewählter „Authentifizierung des Kontoschlüssels“.](../../../../images/tutorials/create/maria-db/account-key.png)

>[!TAB Einfache Authentifizierung]

Um die Standardauthentifizierung zu verwenden, wählen Sie **[!UICONTROL Standardauthentifizierung]** aus, geben Sie Werte für Ihre [Authentifizierungsdaten](../../../../connectors/databases/mariadb.md#azure) ein und wählen Sie dann **[!UICONTROL Mit Quelle verbinden]** aus.

![Die neue Kontoschnittstelle im Quell-Workflow mit ausgewählter „Standardauthentifizierung“.](../../../../images/tutorials/create/maria-db/basic-auth.png)

>[!ENDTABS]

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL MariaDB]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in Experience Platform zu importieren](../../dataflow/databases.md).
