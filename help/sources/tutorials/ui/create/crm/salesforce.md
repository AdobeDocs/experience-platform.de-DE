---
title: Salesforce-Konto über die Experience Platform-Benutzeroberfläche verbinden
description: Erfahren Sie, wie Sie Ihr Salesforce-Konto verbinden und Ihre CRM-Daten mithilfe der Benutzeroberfläche an die Experience Platform übertragen können.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: c543590ef1806e5259da2ffb6833cd030d573ca7
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 18%

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

>[!TAB Standardauthentifizierung]

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um Ihre [!DNL Salesforce] Konto mit einfacher Authentifizierung.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Umgebungs-URL | Die URL der [!DNL Salesforce] Quellinstanz. |
| Benutzername | Der Benutzername für die [!DNL Salesforce] Benutzerkonto. |
| Kennwort | Das Kennwort für die [!DNL Salesforce] Benutzerkonto. |
| Sicherheits-Token | Das Sicherheits-Token für [!DNL Salesforce] Benutzerkonto. |
| API-Version | (Optional) Die REST-API-Version der [!DNL Salesforce] -Instanz, die Sie verwenden. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version verwenden `52`eingeben, müssen Sie den Wert als `52.0` Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. |

Weitere Informationen zur Authentifizierung finden Sie unter [this [!DNL Salesforce] Authentifizierungshandbuch](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB OAuth2 Client Credential]

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um Ihre [!DNL Salesforce] -Konto mit OAuth2-Client-Anmeldedaten verwenden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Umgebungs-URL | Die URL der [!DNL Salesforce] Quellinstanz. |
| Client-ID | Die Client-ID wird zusammen mit dem Client-Geheimnis als Teil der OAuth2-Authentifizierung verwendet. Gemeinsam ermöglicht die Client-ID und das Client-Geheimnis Ihrer Anwendung, im Namen Ihres Kontos zu arbeiten, indem Sie Ihre Anwendung identifizieren auf [!DNL Salesforce]. |
| Client-Geheimnis | Das Client-Geheimnis wird zusammen mit der Client-ID als Teil der OAuth2-Authentifizierung verwendet. Gemeinsam ermöglicht die Client-ID und das Client-Geheimnis Ihrer Anwendung, im Namen Ihres Kontos zu arbeiten, indem Sie Ihre Anwendung identifizieren auf [!DNL Salesforce]. |
| API-Version | (Optional) Die REST-API-Version der [!DNL Salesforce] -Instanz, die Sie verwenden. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version verwenden `52`eingeben, müssen Sie den Wert als `52.0` Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. |

Weitere Informationen zur Verwendung von OAuth für [!DNL Salesforce], lesen Sie die [[!DNL Salesforce] Handbuch zu OAuth-Autorisierungsflüssen](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

Nachdem Sie die erforderlichen Anmeldedaten erfasst haben, können Sie die folgenden Schritte ausführen, um Ihre [!DNL Salesforce] -Konto auf Experience Platform.

## Verbinden Ihres [!DNL Salesforce]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** über das linke Navigationsmenü aus, um auf den Arbeitsbereich &quot;Quellen&quot;zuzugreifen. Die *[!UICONTROL Katalog]* zeigt eine Vielzahl von Quellen an, die im Experience Platform-Quellkatalog verfügbar sind.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie eine bestimmte Quelle mithilfe der Suchoption finden.

Auswählen **[!UICONTROL CRM]** aus der Liste der Quellkategorien und wählen Sie **[!UICONTROL Daten hinzufügen]** aus dem [!DNL Salesforce] Karte.

![Der Quellkatalog auf der Experience Platform-Benutzeroberfläche mit der ausgewählten Salesforce-Quellkarte.](../../../../images/tutorials/create/salesforce/catalog.png)

Die **[!UICONTROL Mit Salesforce verbinden]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

>[!BEGINTABS]

>[!TAB Vorhandenes Salesforce-Konto verwenden]

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und wählen Sie dann das Konto, das Sie verwenden möchten, aus der angezeigten Liste aus. Wählen Sie zum Abschluss **[!UICONTROL Nächste]** um fortzufahren.

![Eine Liste authentifizierter Salesforce-Konten, die bereits in Ihrem Unternehmen vorhanden sind.](../../../../images/tutorials/create/salesforce/existing.png)

>[!TAB Neues Salesforce-Konto erstellen]

Um ein neues Konto zu verwenden, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie einen Namen, eine Beschreibung und Ihre [!DNL Salesforce] Authentifizierungsberechtigungen. Wählen Sie zum Abschluss **[!UICONTROL Verbindung mit Quelle herstellen]** und lassen einige Sekunden zu, bis die neue Verbindung hergestellt ist.

![Die Oberfläche, in der Sie ein neues Salesforce-Konto erstellen können, indem Sie die entsprechenden Authentifizierungsberechtigungen angeben.](../../../../images/tutorials/create/salesforce/new.png)

>[!ENDTABS]

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Salesforce]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in [!DNL Platform]](../../dataflow/crm.md).
