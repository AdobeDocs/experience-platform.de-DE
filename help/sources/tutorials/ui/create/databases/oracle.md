---
title: Verbinden von Oracle DB mit Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie Ihre Oracle DB-Instanz über die Benutzeroberfläche mit Experience Platform verbinden.
exl-id: 4ca6ecc6-0382-4cee-acc5-1dec7eeb9443
source-git-commit: 7acdc090c020de31ee1a010d71a2969ec9e5bbe1
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 17%

---

# Verbinden von [!DNL Oracle DB] mit Experience Platform über die Benutzeroberfläche

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihre [!DNL Oracle DB]-Instanz mithilfe des Arbeitsbereichs „Quellen“ in der Benutzeroberfläche von Experience Platform mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine [!DNL Oracle DB] Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [&#x200B; eines Datenflusses &#x200B;](../../dataflow/databases.md).

### Sammeln erforderlicher Anmeldedaten

Informationen zur Authentifizierung [[!DNL Oracle DB]  Sie in &#x200B;](../../../../connectors/databases/oracle.md#prerequisites)Übersicht“.

## Navigieren im Quellkatalog

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich *[!UICONTROL Quellen]* zuzugreifen. Wählen Sie eine Kategorie aus oder verwenden Sie die Suchleiste, um Ihre Quelle zu finden.

Um eine Verbindung zu [!DNL Oracle DB] herzustellen, wechseln Sie zur Kategorie *[!UICONTROL Datenbanken]*, wählen Sie die Quellkarte **[!UICONTROL Oracle]** DB&rbrace; aus und klicken Sie dann auf **[!UICONTROL Einrichten]**.

>[!TIP]
>
>Quellen zeigen **[!UICONTROL Einrichten]** für neue Verbindungen und **[!UICONTROL Daten hinzufügen]** an, wenn bereits ein Konto vorhanden ist.

![Der Quellkatalog mit der ausgewählten Option &quot;Oracle DB“.](../../../../images/tutorials/create/oracle/catalog.png)

## Vorhandenes Konto verwenden {#existing}

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das [!DNL Oracle DB] Konto aus, das Sie verwenden möchten.

![Die Schnittstelle „Vorhandene Konten“ im Quell-Workflow mit ausgewähltem „Vorhandenes Konto“.](../../../../images/tutorials/create/oracle/existing.png)

## Neues Konto erstellen {#new}

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen an und fügen Sie optional eine Beschreibung für Ihr Konto hinzu.

### Verbindung zu Experience Platform auf Azure herstellen {#azure}

Sie können Ihre [!DNL Oracle DB] mit Experience Platform auf Azure über eine Verbindungszeichenfolge verbinden.

Um die Authentifizierung für Verbindungszeichenfolgen zu verwenden, geben Sie Ihre [Verbindungszeichenfolge](../../../../connectors/databases/oracle.md#azure) an und wählen Sie **[!UICONTROL Mit Quelle verbinden]**.

![Die neue Kontoschnittstelle im Quell-Workflow mit ausgewählter „Authentifizierung der Verbindungszeichenfolge“.](../../../../images/tutorials/create/oracle/azure.png)

### Verbinden mit Experience Platform auf Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../../../landing/multi-cloud.md).

Um ein neues [!DNL Oracle DB]-Konto zu erstellen und eine Verbindung zu Experience Platform auf AWS herzustellen, stellen Sie sicher, dass Sie sich in einer VA6-Sandbox befinden, und geben Sie dann die erforderlichen [&#x200B; (Anmeldeinformationen für die Authentifizierung) &#x200B;](../../../../connectors/databases/oracle.md#aws).

![Die neue Kontoschnittstelle im Quell-Workflow zum Herstellen einer Verbindung mit AWS.](../../../../images/tutorials/create/oracle/aws.png)

## Erstellen eines Datenflusses für [!DNL Oracle DB] Daten

Nachdem Sie Ihre [!DNL Oracle DB] erfolgreich verbunden haben, können Sie jetzt [einen Datenfluss erstellen und Daten aus Ihrer Datenbank in Experience Platform aufnehmen](../../dataflow/databases.md).
