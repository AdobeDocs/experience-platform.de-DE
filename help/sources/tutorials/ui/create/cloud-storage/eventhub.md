---
title: Erstellen einer Azure Event Hub-Quellverbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung für Azure Event Hub erstellen.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: 1680cc4e1d5c1576767053a74e560bc2eb8c24cb
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 25%

---

# Erstellen Sie eine [!DNL Azure Event Hubs] Quellverbindung in der Benutzeroberfläche

>[!IMPORTANT]
>
>Die [!DNL Azure Event Hubs] -Quelle ist im Quellkatalog für Benutzer verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Azure Event Hubs] -Konto über die Benutzeroberfläche von Adobe Experience Platform.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Event Hubs]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/streaming/cloud-storage-streaming.md) fortfahren.

### Sammeln erforderlicher Anmeldeinformationen

Um Ihre [!DNL Event Hubs] Quell-Connector müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

>[!BEGINTABS]

>[!TAB Standardauthentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| SAS-Schlüsselname | Der Name der Autorisierungsregel, der auch als SAS-Schlüsselname bezeichnet wird. |
| SAS-Schlüssel | Der Primärschlüssel der [!DNL Event Hubs] Namespace. Die `sasPolicy` dass `sasKey` muss `manage` -Berechtigungen, die für die [!DNL Event Hubs] Liste auszufüllen. |
| Namespace | Der Namespace des [!DNL Event Hubs] auf die Sie zugreifen. Ein [!DNL Event Hubs] Der Namespace stellt einen eindeutigen Scoping-Container bereit, in dem Sie einen oder mehrere [!DNL Event Hubs]. |

>[!TAB SAS-Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| SAS-Schlüsselname | Der Name der Autorisierungsregel, der auch als SAS-Schlüsselname bezeichnet wird. |
| SAS-Schlüssel | Der Primärschlüssel der [!DNL Event Hubs] Namespace. Die `sasPolicy` dass `sasKey` muss `manage` -Berechtigungen, die für die [!DNL Event Hubs] Liste auszufüllen. |
| Namespace | Der Namespace des [!DNL Event Hubs] auf die Sie zugreifen. Ein [!DNL Event Hubs] Der Namespace stellt einen eindeutigen Scoping-Container bereit, in dem Sie einen oder mehrere [!DNL Event Hubs]. |
| Ereignis-Hub-Name | Der Name für Ihre [!DNL Event Hubs] -Quelle. |

>[!ENDTABS]

Weitere Informationen zu diesen Werten finden Sie unter [Dieses Ereignis-Hubs-Dokument](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihre [!DNL Event Hubs] -Konto auf Experience Platform.

## Verbinden Ihres [!DNL Event Hubs]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem [!UICONTROL Cloud-Speicher] category, select **[!UICONTROL Azure Event Hubs]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog mit ausgewählten Azure Event-Hubs.](../../../../images/tutorials/create/eventhub/catalog.png)

Die **[!UICONTROL Verbindung zu Azure Event Hubs herstellen]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie die [!DNL Event Hubs] Konto, das Sie verwenden möchten, wählen Sie **[!UICONTROL Nächste]** um fortzufahren.

![Eine Liste der vorhandenen Azure Event Hubs-Quellkonten.](../../../../images/tutorials/create/eventhub/existing.png)

### Neues Konto

>[!TIP]
>
>Nach der Erstellung können Sie den Authentifizierungstyp eines [!DNL Event Hubs] Basisverbindung. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihre neue [!DNL Event Hubs] -Konto.

![Die neue Benutzeroberfläche zur Kontoerstellung für Azure Event Hubs.](../../../../images/tutorials/create/eventhub/new.png)

>[!BEGINTABS]

>[!TAB Standardauthentifizierung]

So erstellen Sie eine [!DNL Event Hubs] Konto mit Standardauthentifizierung auswählen **[!UICONTROL Standardauthentifizierung]** und dann Werte für Ihre [!UICONTROL SAS-Schlüsselname], [!UICONTROL SAS-Schlüssel], und [!UICONTROL Namespace].

Nachdem Sie Ihre Authentifizierungsberechtigungen eingegeben haben, wählen Sie **[!UICONTROL Verbindung mit Quelle herstellen]**.

![Die Standard-Authentifizierungsschnittstelle für Azure Event-Hubs.](../../../../images/tutorials/create/eventhub/standard.png)

>[!TAB SAS-Authentifizierung]

So erstellen Sie eine [!DNL Event Hubs] Konto mit SAS-Authentifizierung auswählen **[!UICONTROL SAS-Authentifizierung]** und dann Werte für Ihre [!UICONTROL SAS-Schlüsselname], [!UICONTROL SAS-Schlüssel], [!UICONTROL Namespace], und [!UICONTROL Name der Ereignis-Hubs].

Nachdem Sie Ihre Authentifizierungsberechtigungen eingegeben haben, wählen Sie **[!UICONTROL Verbindung mit Quelle herstellen]**.

![Die SAS-Authentifizierungsschnittstelle für Azure Event Hubs.](../../../../images/tutorials/create/eventhub/sas.png)

>[!ENDTABS]


## Nächste Schritte

In diesem Tutorial haben Sie Ihre [!DNL Event Hubs] -Konto auf Experience Platform. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in Experience Platform zu übertragen](../../dataflow/streaming/cloud-storage-streaming.md).
