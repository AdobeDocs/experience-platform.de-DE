---
title: Salesforce-Konto über die Experience Platform-Benutzeroberfläche verbinden
description: Erfahren Sie, wie Sie Ihr Salesforce-Konto verbinden und Ihre CRM-Daten mithilfe der Benutzeroberfläche an die Experience Platform übertragen können.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 21%

---

# Verbinden Sie [!DNL Salesforce] Konto für Experience Platform über die Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie Ihre [!DNL Salesforce] und bringen Sie Ihre CRM-Daten über die Experience Platform-Benutzeroberfläche in Adobe Experience Platform mit.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine authentifizierte [!DNL Salesforce] -Konto verwenden, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Datenfluss für CRM-Daten konfigurieren](../../dataflow/crm.md).

### Sammeln erforderlicher Anmeldeinformationen {#gather-required-credentials}

Die [!DNL Salesforce] -Quelle unterstützt grundlegende Authentifizierung und OAuth2 Client Credential.

>[!BEGINTABS]

>[!TAB Grundlegende Authentifizierung]

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um Ihre [!DNL Salesforce] Konto mit einfacher Authentifizierung.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Umgebungs-URL | Die URL der [!DNL Salesforce] Quellinstanz. |
| Benutzername | Der Benutzername für die [!DNL Salesforce] Benutzerkonto. |
| Kennwort | Das Kennwort für die [!DNL Salesforce] Benutzerkonto. |
| Sicherheitstoken | Das Sicherheits-Token für [!DNL Salesforce] Benutzerkonto. |
| API-Version | (Optional) Die REST-API-Version der [!DNL Salesforce] -Instanz, die Sie verwenden. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version verwenden `52`eingeben, müssen Sie den Wert als `52.0`. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. |

Weitere Informationen zur Authentifizierung finden Sie unter [this [!DNL Salesforce] Authentifizierungshandbuch](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB OAuth2 Client Credential]

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um Ihre [!DNL Salesforce] -Konto mit OAuth2-Client-Anmeldedaten verwenden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Umgebungs-URL | Die URL der [!DNL Salesforce] Quellinstanz. |
| Client-ID | Die Client-ID wird zusammen mit dem Client-Geheimnis als Teil der OAuth2-Authentifizierung verwendet. Gemeinsam ermöglichen es die Client-ID und das Client-Geheimnis Ihrer Anwendung, im Namen Ihres Kontos zu arbeiten, indem Sie Ihre Anwendung identifizieren auf [!DNL Salesforce]. |
| Client-Geheimnis | Das Client-Geheimnis wird zusammen mit der Client-ID als Teil der OAuth2-Authentifizierung verwendet. Gemeinsam ermöglichen es die Client-ID und das Client-Geheimnis Ihrer Anwendung, im Namen Ihres Kontos zu arbeiten, indem Sie Ihre Anwendung identifizieren auf [!DNL Salesforce]. |
| API-Version | Die REST-API-Version der [!DNL Salesforce] -Instanz, die Sie verwenden. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version verwenden `52`eingeben, müssen Sie den Wert als `52.0`. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. |

Weitere Informationen zur Verwendung von OAuth für [!DNL Salesforce], lesen Sie die [[!DNL Salesforce] Handbuch zu OAuth-Autorisierungsflüssen](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

Nachdem Sie die erforderlichen Anmeldedaten erfasst haben, können Sie die folgenden Schritte ausführen, um Ihre [!DNL Salesforce] -Konto auf Experience Platform.

## Verbinden Ihres [!DNL Salesforce]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Auswählen **[!DNL Salesforce]** unter *[!UICONTROL CRM]* und wählen Sie **[!UICONTROL Daten hinzufügen]**.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die **[!UICONTROL Einrichten]** -Option, wenn eine bestimmte Quelle noch kein authentifiziertes Konto hat. Sobald ein authentifiziertes Konto existiert, wird diese Option in **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog auf der Experience Platform-Benutzeroberfläche mit der ausgewählten Salesforce-Quellkarte.](../../../../images/tutorials/create/salesforce/catalog.png)

Die **[!UICONTROL Mit Salesforce verbinden]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto verwenden

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und wählen Sie dann das Konto, das Sie verwenden möchten, aus der angezeigten Liste aus. Wählen Sie zum Abschluss **[!UICONTROL Nächste]** um fortzufahren.

![Eine Liste authentifizierter Salesforce-Konten, die bereits in Ihrem Unternehmen vorhanden sind.](../../../../images/tutorials/create/salesforce/existing.png)

### Neues Konto erstellen

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie einen Namen und eine Beschreibung für Ihre neue [!DNL Salesforce] -Konto.

![Die Oberfläche, in der Sie ein neues Salesforce-Konto erstellen können, indem Sie die entsprechenden Authentifizierungsberechtigungen angeben.](../../../../images/tutorials/create/salesforce/new.png)

Wählen Sie anschließend den Authentifizierungstyp aus, den Sie für Ihr neues Konto verwenden möchten.

>[!BEGINTABS]

>[!TAB Grundlegende Authentifizierung]

Wählen Sie zur einfachen Authentifizierung **[!UICONTROL Grundlegende Authentifizierung]** und geben Sie dann Werte für die folgenden Anmeldedaten an:

* Umgebungs-URL
* Benutzername
* Passwort
* API-Version (optional)

Wählen Sie zum Abschluss **[!UICONTROL Verbindung mit Quelle herstellen]**.

![Die grundlegende Authentifizierungsschnittstelle für die Erstellung von Salesforce-Konten.](../../../../images/tutorials/create/salesforce/basic.png)

>[!TAB OAuth2 Client Credential]

Wählen Sie für OAuth 2 Client Credential die Option **[!UICONTROL OAuth2 Client Credential]** und geben Sie dann Werte für die folgenden Anmeldedaten an:

* Umgebungs-URL
* Client-ID
* Client-Geheimnis
* API-Version

Wählen Sie zum Abschluss **[!UICONTROL Verbindung mit Quelle herstellen]**.

![Die OAuth-Schnittstelle für die Erstellung von Salesforce-Konten.](../../../../images/tutorials/create/salesforce/oauth2.png)

>[!ENDTABS]

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Salesforce]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in [!DNL Platform]](../../dataflow/crm.md).
