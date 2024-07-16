---
title: Verbinden Ihres Salesforce Service Cloud-Kontos über die Experience Platform-Benutzeroberfläche
description: Erfahren Sie, wie Sie Ihr Salesforce Service Cloud-Konto verbinden und Ihre Kundenerfolgsdaten über die Benutzeroberfläche an Experience Platform übermitteln.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 21%

---

# Verbinden Sie Ihr [!DNL Salesforce Service Cloud]-Konto über die Benutzeroberfläche mit Experience Platform.

In diesem Tutorial erfahren Sie, wie Sie Ihr [!DNL Salesforce Service Cloud]-Konto verbinden und Ihre Kundenerfolgsdaten mithilfe der Experience Platform-Benutzeroberfläche mit Adobe Experience Platform bringen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Salesforce Service Cloud] -Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Konfigurieren eines Datenflusses für einen Kundenerfolg fortfahren](../../dataflow/customer-success.md)[

### Sammeln erforderlicher Anmeldeinformationen

Die Quelle [!DNL Salesforce Service Cloud] unterstützt grundlegende Authentifizierung und OAuth2 Client Credential.

>[!BEGINTABS]

>[!TAB Grundlegende Authentifizierung]

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um Ihr [!DNL Salesforce Service Cloud]-Konto mithilfe der einfachen Authentifizierung zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Umgebungs-URL | Die URL der Quellinstanz [!DNL Salesforce Service Cloud]. |
| Benutzername | Der Benutzername für das [!DNL Salesforce Service Cloud] -Benutzerkonto. |
| Kennwort | Das Kennwort für das [!DNL Salesforce Service Cloud] -Benutzerkonto. |
| Sicherheitstoken | Das Sicherheits-Token für das [!DNL Salesforce Service Cloud] -Benutzerkonto. |
| API-Version | (Optional) Die REST-API-Version der von Ihnen verwendeten [!DNL Salesforce Service Cloud]-Instanz. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version `52` verwenden, müssen Sie den Wert als `52.0` eingeben. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. |

Weitere Informationen zur Authentifizierung finden Sie in [diesem [!DNL Salesforce Service Cloud] Authentifizierungshandbuch](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB OAuth2 Client Credential]

Sie müssen Werte für die folgenden Anmeldedaten angeben, um Ihr [!DNL Salesforce Service Cloud]-Konto mithilfe von OAuth2-Client-Anmeldedaten zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Umgebungs-URL | Die URL der Quellinstanz [!DNL Salesforce Service Cloud]. |
| Client-ID | Die Client-ID wird zusammen mit dem Client-Geheimnis als Teil der OAuth2-Authentifizierung verwendet. Gemeinsam ermöglichen es die Client-ID und das Client-Geheimnis Ihrer Anwendung, im Namen Ihres Kontos zu arbeiten, indem Sie Ihre Anwendung mit [!DNL Salesforce Service Cloud] identifizieren. |
| Client-Geheimnis | Das Client-Geheimnis wird zusammen mit der Client-ID als Teil der OAuth2-Authentifizierung verwendet. Gemeinsam ermöglichen es die Client-ID und das Client-Geheimnis Ihrer Anwendung, im Namen Ihres Kontos zu arbeiten, indem Sie Ihre Anwendung mit [!DNL Salesforce Service Cloud] identifizieren. |
| API-Version | Die REST-API-Version der von Ihnen verwendeten [!DNL Salesforce Service Cloud]-Instanz. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version `52` verwenden, müssen Sie den Wert als `52.0` eingeben. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. |

Weitere Informationen zur Verwendung von OAuth für [!DNL Salesforce Service Cloud] finden Sie im [[!DNL Salesforce Service Cloud] Handbuch zu OAuth-Autorisierungsflüssen](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Salesforce Service Cloud]-Konto mit Experience Platform zu verbinden.

## Verbinden Ihres [!DNL Salesforce Service Cloud]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie **[!DNL Salesforce Service Cloud]** unter der Kategorie *[!UICONTROL Kundenerfolg]* und dann **[!UICONTROL Daten hinzufügen]** aus.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die Option **[!UICONTROL Einrichten]** an, wenn eine Quelle noch kein authentifiziertes Konto hat. Sobald ein authentifiziertes Konto vorhanden ist, wird diese Option in **[!UICONTROL Daten hinzufügen]** geändert.

![Der Quellkatalog auf der Experience Platform-Benutzeroberfläche mit ausgewählter Salesforce Service Cloud-Quellkarte.](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

Die Seite **[!UICONTROL Verbindung zu Salesforce Service Cloud herstellen]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto verwenden

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das gewünschte Konto aus der angezeigten Liste aus. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![Eine Liste authentifizierter Salesforce Service Cloud-Konten, die bereits in Ihrem Unternehmen vorhanden sind.](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

### Neues Konto erstellen

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** aus und geben Sie einen Namen und eine Beschreibung für Ihr neues [!DNL Salesforce Service Cloud]-Konto ein.

![Die Benutzeroberfläche, in der Sie ein neues Salesforce Service Cloud-Konto erstellen können, indem Sie die entsprechenden Authentifizierungsberechtigungen angeben.](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

Wählen Sie anschließend den Authentifizierungstyp aus, den Sie für Ihr neues Konto verwenden möchten.

>[!BEGINTABS]

>[!TAB Grundlegende Authentifizierung]

Wählen Sie zur einfachen Authentifizierung **[!UICONTROL Grundlegende Authentifizierung]** und geben Sie dann Werte für die folgenden Anmeldeinformationen ein:

* Umgebungs-URL
* Benutzername
* Passwort
* API-Version (optional)

Wählen Sie nach Abschluss **[!UICONTROL Mit Quelle verbinden]** aus.

![Die grundlegende Authentifizierungsschnittstelle für die Salesforce-Kontoerstellung.](../../../../images/tutorials/create/salesforce-service-cloud/basic.png)

>[!TAB OAuth2 Client Credential]

Wählen Sie für OAuth 2 Client Credential **[!UICONTROL OAuth2 Client Credential]** und geben Sie dann Werte für die folgenden Anmeldedaten ein:

* Umgebungs-URL
* Client-ID
* Client-Geheimnis
* API-Version

Wählen Sie nach Abschluss **[!UICONTROL Mit Quelle verbinden]** aus.

![Die OAuth-Schnittstelle für die Salesforce-Kontoerstellung.](../../../../images/tutorials/create/salesforce-service-cloud/oauth2.png)

>[!ENDTABS]

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Salesforce Service Cloud]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen Datenfluss konfigurieren, um Kundenerfolgsdaten in Experience Platform](../../dataflow/customer-success.md) zu importieren.[
