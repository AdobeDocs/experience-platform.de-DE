---
title: Verbinden Ihres Salesforce-Kontos über die Benutzeroberfläche von Experience Platform
description: Erfahren Sie, wie Sie Ihr Salesforce-Konto verbinden und Ihre CRM-Daten über die Benutzeroberfläche in Experience Platform übertragen.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 17%

---

# Verbinden Ihres [!DNL Salesforce]-Kontos mit Experience Platform über die Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie Ihr [!DNL Salesforce]-Konto verbinden und Ihre CRM-Daten über die Benutzeroberfläche von Experience Platform in Adobe Experience Platform übertragen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein authentifiziertes [!DNL Salesforce]-Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [ eines Datenflusses für CRM-Daten ](../../dataflow/crm.md).

### Sammeln erforderlicher Anmeldedaten {#gather-required-credentials}

Die [!DNL Salesforce]-Quelle unterstützt die Standardauthentifizierung sowie OAuth2-Client-Anmeldeinformationen.

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um Ihr [!DNL Salesforce]-Konto mit einfacher Authentifizierung zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Umgebungs-URL | Die URL der [!DNL Salesforce] Quellinstanz. Das Format für die Umgebungs-URL ist `https://[domain].my.salesforce.com`. |
| Benutzername | Der Benutzername für das [!DNL Salesforce] Benutzerkonto. |
| Kennwort | Das Kennwort für das [!DNL Salesforce] Benutzerkonto. |
| Sicherheitstoken | Das Sicherheits-Token für das [!DNL Salesforce] Benutzerkonto. |
| API-Version | (Optional) Die REST-API-Version der von Ihnen verwendeten [!DNL Salesforce]. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version `52` verwenden, müssen Sie den Wert als `52.0` eingeben. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. |

Weiterführende Informationen zur Authentifizierung finden Sie [diesem  [!DNL Salesforce] -Authentifizierungshandbuch](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB OAuth2 Client-Anmeldedaten]

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um Ihr [!DNL Salesforce]-Konto mit OAuth2-Client-Anmeldeinformationen zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Umgebungs-URL | Die URL der [!DNL Salesforce] Quellinstanz. Das Format für die Umgebungs-URL ist `https://[domain].my.salesforce.com`. |
| Client-ID | Die Client-ID wird im Rahmen der OAuth2-Authentifizierung zusammen mit dem Client-Geheimnis verwendet. Zusammen ermöglichen die Client-ID und das Client-Geheimnis, dass Ihre Anwendung im Namen Ihres Kontos betrieben wird, indem Sie Ihre Anwendung für die [!DNL Salesforce] identifizieren. |
| Client-Geheimnis | Das Client-Geheimnis wird zusammen mit der Client-ID als Teil der OAuth2-Authentifizierung verwendet. Zusammen ermöglichen die Client-ID und das Client-Geheimnis, dass Ihre Anwendung im Namen Ihres Kontos betrieben wird, indem Sie Ihre Anwendung für die [!DNL Salesforce] identifizieren. |
| API-Version | Die REST-API-Version der von Ihnen verwendeten [!DNL Salesforce]. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version `52` verwenden, müssen Sie den Wert als `52.0` eingeben. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. |

Weitere Informationen zur Verwendung von OAuth für [!DNL Salesforce] finden Sie im [[!DNL Salesforce] Handbuch zu OAuth-Autorisierungsflüssen](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Salesforce]-Konto mit Experience Platform zu verbinden.

## Verbinden Ihres [!DNL Salesforce]-Kontos

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie **[!DNL Salesforce]** unter der Kategorie *[!UICONTROL CRM]* und dann **[!UICONTROL Daten hinzufügen]**.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die Option **[!UICONTROL Einrichten]** an, wenn eine bestimmte Quelle noch kein authentifiziertes Konto hat. Sobald ein authentifiziertes Konto vorhanden ist, ändert sich diese Option in **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog auf der Experience Platform-Benutzeroberfläche mit der ausgewählten Salesforce-Quellkarte.](../../../../images/tutorials/create/salesforce/catalog.png)

Die **[!UICONTROL Verbindung zu Salesforce herstellen]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto verwenden

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das Konto, das Sie verwenden möchten, aus der angezeigten Liste aus. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![Eine Liste der authentifizierten Salesforce-Konten, die bereits in Ihrer Organisation vorhanden sind.](../../../../images/tutorials/create/salesforce/existing.png)

### Neues Konto erstellen

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie einen Namen und eine Beschreibung für Ihr neues [!DNL Salesforce] Konto an.

![Die Benutzeroberfläche, in der Sie ein neues Salesforce-Konto erstellen können, indem Sie die entsprechenden Authentifizierungsdaten angeben.](../../../../images/tutorials/create/salesforce/new.png)

Wählen Sie als Nächstes den Authentifizierungstyp aus, den Sie für Ihr neues Konto verwenden möchten.

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

Wählen Sie für die Standardauthentifizierung **[!UICONTROL Standardauthentifizierung]** und geben Sie dann Werte für die folgenden Anmeldeinformationen an:

* Umgebungs-URL
* Benutzername
* Passwort
* API-Version (optional)

Wenn Sie fertig sind, wählen **[!UICONTROL Mit Quelle verbinden]**.

![Die grundlegende Authentifizierungsschnittstelle für die Erstellung von Salesforce-Konten.](../../../../images/tutorials/create/salesforce/basic.png)

>[!TAB OAuth2 Client-Anmeldedaten]

Wählen Sie für Client-Anmeldeinformationen für OAuth 2 die Option **[!UICONTROL Client-Anmeldeinformationen für OAuth2]** und geben Sie dann Werte für die folgenden Anmeldeinformationen an:

* Umgebungs-URL
* Client-ID
* Client-Geheimnis
* API-Version

Wenn Sie fertig sind, wählen **[!UICONTROL Mit Quelle verbinden]**.

![Die OAuth-Schnittstelle zur Erstellung von Salesforce-Konten.](../../../../images/tutorials/create/salesforce/oauth2.png)

>[!ENDTABS]

### Vorschau der Beispieldaten überspringen {#skip-preview-of-sample-data}

Während des Datenauswahlschritts kann es bei der Aufnahme großer Datentabellen oder -dateien zu einer Zeitüberschreitung kommen. Sie können die Datenvorschau überspringen, um die Zeitüberschreitung zu umgehen, und Ihr Schema dennoch anzeigen, wenn auch ohne Beispieldaten. Um die Datenvorschau zu überspringen, aktivieren Sie den Umschalter **[!UICONTROL Vorschau von Beispieldaten überspringen]**.

Der Rest des Workflows bleibt unverändert. Der einzige Nachteil besteht darin, dass das Überspringen der Datenvorschau verhindert, dass berechnete und erforderliche Felder während des Zuordnungsschritts automatisch validiert werden. Diese Felder müssen dann während der Zuordnung manuell validiert werden.

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Salesforce]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in zu importieren [!DNL Experience Platform]](../../dataflow/crm.md).
