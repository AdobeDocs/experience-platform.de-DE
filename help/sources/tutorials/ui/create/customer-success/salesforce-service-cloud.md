---
title: Verbinden Ihres Salesforce Service Cloud-Kontos über die Benutzeroberfläche von Experience Platform
description: Erfahren Sie, wie Sie über die Benutzeroberfläche eine Verbindung mit Ihrem Salesforce Service Cloud-Konto herstellen und Ihre Kundenerfolgsdaten zu Experience Platform übertragen.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: b9a9b00114b3c1159a14b7e39484d250fa7563ba
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 36%

---

# Verbinden Ihres [!DNL Salesforce Service Cloud]-Kontos mit Experience Platform über die Benutzeroberfläche

Folgen Sie dieser Schritt-für-Schritt-Anleitung, um Ihr [!DNL Salesforce Service Cloud]-Konto nahtlos zu verbinden und Ihre Kundenerfolgsdaten in Adobe Experience Platform zu importieren.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Salesforce Service Cloud]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [&#x200B; eines Datenflusses für einen Customer Success fortfahren](../../dataflow/customer-success.md)

### Sammeln erforderlicher Anmeldedaten

Lesen Sie das [Authentifizierungshandbuch](../../../../connectors/customer-success/salesforce-service-cloud.md#credentials) für weitere Informationen zum Abrufen Ihrer Anmeldeinformationen.

## Verbinden Ihres [!DNL Salesforce Service Cloud]-Kontos

Wählen Sie in der Benutzeroberfläche von Experience Platform in der linken Navigationsleiste die Option **[!UICONTROL Sources]** , um auf den [!UICONTROL Sources]-Arbeitsbereich zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie **[!DNL Salesforce Service Cloud]** unter der Kategorie *[!UICONTROL Customer success]* und dann **[!UICONTROL Add data]** aus.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die **[!UICONTROL Set up]** an, wenn eine bestimmte Quelle noch kein authentifiziertes Konto hat. Sobald ein authentifiziertes Konto vorhanden ist, ändert sich diese Option in **[!UICONTROL Add data]**.

![Der Quellkatalog auf der Experience Platform-Benutzeroberfläche mit der ausgewählten Salesforce Service Cloud-Quellkarte.](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

Die Seite **[!UICONTROL Connect to Salesforce Service Cloud]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto verwenden

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Existing account]** und dann das gewünschte Konto aus der angezeigten Liste aus. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Next]** aus, um fortzufahren.

![Eine Liste der authentifizierten Salesforce Service Cloud-Konten, die bereits in Ihrer Organisation vorhanden sind.](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

### Neues Konto erstellen

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL New account]** aus und geben Sie einen Namen und eine Beschreibung für Ihr neues [!DNL Salesforce Service Cloud] Konto an. Wählen Sie als Nächstes **[!UICONTROL OAuth2 Client Credential]** aus und geben Sie dann Werte für die folgenden Anmeldeinformationen an:

* Umgebungs-URL
* Client-ID
* Client-Geheimnis
* API-Version

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Connect to source]** aus.

![Die OAuth-Schnittstelle zur Erstellung von Salesforce-Konten.](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Salesforce Service Cloud]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Customer Success-Daten in Experience Platform zu importieren](../../dataflow/customer-success.md).
