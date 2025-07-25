---
title: Verbinden Ihres Salesforce Service Cloud-Kontos über die Benutzeroberfläche von Experience Platform
description: Erfahren Sie, wie Sie über die Benutzeroberfläche eine Verbindung mit Ihrem Salesforce Service Cloud-Konto herstellen und Ihre Kundenerfolgsdaten zu Experience Platform übertragen.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: eab6303a3b420d4622185316922d242a4ce8a12d
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 18%

---

# Verbinden Ihres [!DNL Salesforce Service Cloud]-Kontos mit Experience Platform über die Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie mithilfe der Benutzeroberfläche von Experience Platform eine Verbindung zu Ihrem [!DNL Salesforce Service Cloud]-Konto herstellen und Ihre Kundenerfolgsdaten an Adobe Experience Platform übermitteln.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Salesforce Service Cloud]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [ eines Datenflusses für einen Customer Success fortfahren](../../dataflow/customer-success.md)

### Sammeln erforderlicher Anmeldedaten

>[!WARNING]
>
>Die Standardauthentifizierung für die [!DNL Salesforce Service Cloud] wird im Januar 2026 eingestellt. Sie müssen zur Authentifizierung mit Client-Anmeldeinformationen für OAuth 2 wechseln, um weiterhin die -Quelle verwenden und Daten von Ihrem [!DNL Salesforce Service Cloud]-Konto in Experience Platform aufnehmen zu können.

Die [!DNL Salesforce Service Cloud]-Quelle unterstützt die Standardauthentifizierung sowie OAuth2-Client-Anmeldeinformationen.

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um Ihr [!DNL Salesforce Service Cloud]-Konto mit einfacher Authentifizierung zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Umgebungs-URL | Die URL der [!DNL Salesforce Service Cloud] Quellinstanz. |
| Benutzername | Der Benutzername für das [!DNL Salesforce Service Cloud] Benutzerkonto. |
| Kennwort | Das Kennwort für das [!DNL Salesforce Service Cloud] Benutzerkonto. |
| Sicherheitstoken | Das Sicherheits-Token für das [!DNL Salesforce Service Cloud] Benutzerkonto. |
| API-Version | (Optional) Die REST-API-Version der von Ihnen verwendeten [!DNL Salesforce Service Cloud]. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version `52` verwenden, müssen Sie den Wert als `52.0` eingeben. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. |

Weiterführende Informationen zur Authentifizierung finden Sie [diesem  [!DNL Salesforce Service Cloud] -Authentifizierungshandbuch](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB OAuth2 Client-Anmeldedaten]

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um Ihr [!DNL Salesforce Service Cloud]-Konto mit OAuth2-Client-Anmeldeinformationen zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Umgebungs-URL | Die URL der [!DNL Salesforce Service Cloud] Quellinstanz. |
| Client-ID | Die Client-ID wird im Rahmen der OAuth2-Authentifizierung zusammen mit dem Client-Geheimnis verwendet. Zusammen ermöglichen die Client-ID und das Client-Geheimnis, dass Ihre Anwendung im Namen Ihres Kontos betrieben wird, indem Sie Ihre Anwendung für die [!DNL Salesforce Service Cloud] identifizieren. |
| Client-Geheimnis | Das Client-Geheimnis wird zusammen mit der Client-ID als Teil der OAuth2-Authentifizierung verwendet. Zusammen ermöglichen die Client-ID und das Client-Geheimnis, dass Ihre Anwendung im Namen Ihres Kontos betrieben wird, indem Sie Ihre Anwendung für die [!DNL Salesforce Service Cloud] identifizieren. |
| API-Version | Die REST-API-Version der von Ihnen verwendeten [!DNL Salesforce Service Cloud]. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version `52` verwenden, müssen Sie den Wert als `52.0` eingeben. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. |

Weitere Informationen zur Verwendung von OAuth für [!DNL Salesforce Service Cloud] finden Sie im [[!DNL Salesforce Service Cloud] Handbuch zu OAuth-Autorisierungsflüssen](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5).

>[!ENDTABS]

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Salesforce Service Cloud]-Konto mit Experience Platform zu verbinden.

## Verbinden Ihres [!DNL Salesforce Service Cloud]-Kontos

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie **[!DNL Salesforce Service Cloud]** unter der Kategorie *[!UICONTROL Customer Success]* und dann **[!UICONTROL Daten hinzufügen]** aus.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die Option **[!UICONTROL Einrichten]** an, wenn eine bestimmte Quelle noch kein authentifiziertes Konto hat. Sobald ein authentifiziertes Konto vorhanden ist, ändert sich diese Option in **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog auf der Experience Platform-Benutzeroberfläche mit der ausgewählten Salesforce Service Cloud-Quellkarte.](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

Die **[!UICONTROL Verbindung mit Salesforce Service Cloud herstellen]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto verwenden

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das gewünschte Konto aus der angezeigten Liste aus. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![Eine Liste der authentifizierten Salesforce Service Cloud-Konten, die bereits in Ihrer Organisation vorhanden sind.](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

### Neues Konto erstellen

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie einen Namen und eine Beschreibung für Ihr neues [!DNL Salesforce Service Cloud] Konto an.

![Die Benutzeroberfläche, in der Sie ein neues Salesforce Service Cloud-Konto erstellen können, indem Sie die entsprechenden Authentifizierungsdaten angeben.](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

Wählen Sie als Nächstes den Authentifizierungstyp aus, den Sie für Ihr neues Konto verwenden möchten.

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

Wählen Sie für die Standardauthentifizierung **[!UICONTROL Standardauthentifizierung]** und geben Sie dann Werte für die folgenden Anmeldeinformationen an:

* Umgebungs-URL
* Benutzername
* Passwort
* API-Version (optional)

Wenn Sie fertig sind, wählen **[!UICONTROL Mit Quelle verbinden]**.

![Die grundlegende Authentifizierungsschnittstelle für die Erstellung von Salesforce-Konten.](../../../../images/tutorials/create/salesforce-service-cloud/basic.png)

>[!TAB OAuth2 Client-Anmeldedaten]

Wählen Sie für Client-Anmeldeinformationen für OAuth 2 die Option **[!UICONTROL Client-Anmeldeinformationen für OAuth2]** und geben Sie dann Werte für die folgenden Anmeldeinformationen an:

* Umgebungs-URL
* Client-ID
* Client-Geheimnis
* API-Version

Wenn Sie fertig sind, wählen **[!UICONTROL Mit Quelle verbinden]**.

![Die OAuth-Schnittstelle zur Erstellung von Salesforce-Konten.](../../../../images/tutorials/create/salesforce-service-cloud/oauth2.png)

>[!ENDTABS]

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Salesforce Service Cloud]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Customer Success-Daten in Experience Platform zu importieren](../../dataflow/customer-success.md).
