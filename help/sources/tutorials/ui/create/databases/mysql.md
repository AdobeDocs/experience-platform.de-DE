---
title: Verbinden von MySQL mit Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie Ihre MySQL-Datenbank über die Benutzeroberfläche mit Experience Platform verbinden.
exl-id: 75e74bde-6199-4970-93d2-f95ec3a59aa5
source-git-commit: f4200ca71479126e585ac76dd399af4092fdf683
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 14%

---

# Verbinden von [!DNL MySQL] mit Experience Platform über die Benutzeroberfläche

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihre [!DNL MySQL]-Datenbank mithilfe des Arbeitsbereichs „Quellen“ in der Benutzeroberfläche von Experience Platform mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine [!DNL MySQL] Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [&#x200B; eines Datenflusses &#x200B;](../../dataflow/databases.md).

### Sammeln erforderlicher Anmeldedaten

Informationen zur Authentifizierung [[!DNL MySQL]  Sie in &#x200B;](../../../../connectors/databases/mysql.md#prerequisites)Übersicht“.

## Navigieren im Quellkatalog

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich *[!UICONTROL Quellen]* zuzugreifen. Wählen Sie eine Kategorie aus oder verwenden Sie die Suchleiste, um Ihre Quelle zu finden.

Um eine Verbindung zu [!DNL MySQL] herzustellen, wechseln Sie zur Kategorie *[!UICONTROL Datenbanken]*, wählen Sie die Quellkarte **[!UICONTROL MySQL]** aus und klicken Sie dann auf **[!UICONTROL Einrichten]**.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die Option **[!UICONTROL Einrichten]** an, wenn eine bestimmte Quelle noch kein authentifiziertes Konto hat. Nachdem ein authentifiziertes Konto erstellt wurde, ändert sich diese Option in **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog mit der ausgewählten MySQL-Quellkarte.](../../../../images/tutorials/create/my-sql/catalog.png)

## Vorhandenes Konto verwenden {#existing}

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das [!DNL MySQL] Konto aus, das Sie verwenden möchten.

![Die Schnittstelle „Vorhandene Konten“ im Quell-Workflow mit ausgewähltem „Vorhandenes Konto“.](../../../../images/tutorials/create/my-sql/existing.png)

## Neues Konto erstellen {#new}

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen an und fügen Sie optional eine Beschreibung für Ihr Konto hinzu.

![Die neue Kontoschnittstelle im Quell-Workflow mit einem Kontonamen und einer optionalen Beschreibung.](../../../../images/tutorials/create/my-sql/new.png)

### Verbindung zu Experience Platform auf Azure herstellen {#azure}

Sie können Ihre [!DNL MySQL] mit Experience Platform auf Azure verbinden, indem Sie entweder den Kontoschlüssel oder die Standardauthentifizierung verwenden.

>[!BEGINTABS]

>[!TAB Authentifizierung mit Kontoschlüssel]

Um die Kontoschlüsselauthentifizierung zu verwenden, wählen Sie **[!UICONTROL Kontoschlüsselauthentifizierung]**, geben Sie Ihre [Verbindungszeichenfolge](../../../../connectors/databases/mysql.md#azure) an und wählen Sie dann **[!UICONTROL Mit Quelle verbinden]**.

![Die neue Kontoschnittstelle im Quell-Workflow mit ausgewählter „Authentifizierung des Kontoschlüssels“.](../../../../images/tutorials/create/my-sql/account-key.png)

>[!TAB Einfache Authentifizierung]

Um die Standardauthentifizierung zu verwenden, wählen Sie **[!UICONTROL Standardauthentifizierung]** aus, geben Sie Werte für Ihre [Authentifizierungsdaten](../../../../connectors/databases/mysql.md#azure) ein und wählen Sie dann **[!UICONTROL Mit Quelle verbinden]** aus.

![Die neue Kontoschnittstelle im Quell-Workflow mit ausgewählter „Standardauthentifizierung“.](../../../../images/tutorials/create/my-sql/basic-auth.png)

>[!ENDTABS]

### Verbinden mit Experience Platform auf Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../../../landing/multi-cloud.md).

Um ein neues [!DNL MySQL]-Konto zu erstellen und eine Verbindung zu Experience Platform auf AWS herzustellen, stellen Sie sicher, dass Sie sich in einer VA6-Sandbox befinden, und geben Sie dann die erforderlichen [&#x200B; (Anmeldeinformationen für die Authentifizierung) &#x200B;](../../../../connectors/databases/mysql.md#aws).

![Die neue Kontoschnittstelle im Quell-Workflow zum Herstellen einer Verbindung mit AWS.](../../../../images/tutorials/create/my-sql/aws.png)

## Erstellen eines Datenflusses für [!DNL MySQL] Daten

Nachdem Sie Ihre [!DNL MySQL] erfolgreich verbunden haben, können Sie jetzt [einen Datenfluss erstellen und Daten aus Ihrer Datenbank in Experience Platform aufnehmen](../../dataflow/databases.md).
