---
title: Erstellen einer Azure Event Hub Source-Verbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung für Azure Event Hub erstellen.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: 1256f0c76b29edad4808fc4be1d61399bfbae8fa
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 17%

---

# Erstellen einer [!DNL Azure Event Hubs]-Quellverbindung in der Benutzeroberfläche

>[!IMPORTANT]
>
>Die Quelle &quot;[!DNL Azure Event Hubs]&quot; steht Benutzern, die Real-time Customer Data Platform Ultimate erworben haben, im Quellkatalog zur Verfügung.

In diesem Tutorial erfahren Sie, wie Sie mit der Adobe Experience Platform-Benutzeroberfläche ein [!DNL Azure Event Hubs] -Konto erstellen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Event Hubs]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/streaming/cloud-storage-streaming.md) fortfahren.

### Sammeln erforderlicher Anmeldeinformationen

Um den Quell-Connector [!DNL Event Hubs] zu authentifizieren, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

>[!BEGINTABS]

>[!TAB Standardauthentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| SAS-Schlüsselname | Der Name der Autorisierungsregel, der auch als SAS-Schlüsselname bezeichnet wird. |
| SAS-Schlüssel | Der Primärschlüssel des Namespace [!DNL Event Hubs] . Die `sasPolicy`, denen die `sasKey` entspricht, müssen über die `manage` -Rechte verfügen, damit die [!DNL Event Hubs] -Liste ausgefüllt werden kann. |
| Namespace | Der Namespace der [!DNL Event Hub] , auf die Sie zugreifen. Ein Namespace [!DNL Event Hub] bietet einen eindeutigen Scoping-Container, in dem Sie einen oder mehrere [!DNL Event Hubs] erstellen können. |

>[!TAB SAS-Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| SAS-Schlüsselname | Der Name der Autorisierungsregel, der auch als SAS-Schlüsselname bezeichnet wird. |
| SAS-Schlüssel | Der Primärschlüssel des Namespace [!DNL Event Hub] . Die `sasPolicy`, denen die `sasKey` entspricht, müssen über die `manage` -Rechte verfügen, damit die [!DNL Event Hubs] -Liste ausgefüllt werden kann. |
| Namespace | Der Namespace der [!DNL Event Hub] , auf die Sie zugreifen. Ein Namespace [!DNL Event Hub] bietet einen eindeutigen Scoping-Container, in dem Sie einen oder mehrere [!DNL Event Hubs] erstellen können. |
| Ereignis-Hub-Name | Geben Sie Ihren [!DNL Azure Event Hub] Namen ein. Weitere Informationen zu [!DNL Event Hub] -Namen finden Sie in der [Microsoft-Dokumentation](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) . |

>[!TAB Ereignis-Hub Azure Active Directory Auth]

| Anmeldedaten | Beschreibung |
| --- | --- |
| Mandanten-ID | Die Mandantenkennung, von der Sie die Berechtigung anfordern möchten. Ihre Mandantenkennung kann als GUID oder als benutzerfreundlicher Name formatiert werden. **Hinweis**: Die Mandanten-ID wird in der [!DNL Microsoft Azure] -Benutzeroberfläche als &quot;Verzeichnis-ID&quot;bezeichnet. |
| Client-ID | Die Ihrer App zugewiesene Anwendungs-ID. Sie können diese ID aus dem [!DNL Microsoft Entra ID]-Portal abrufen, in dem Sie Ihre [!DNL Azure Active Directory] registriert haben. |
| Geheimer Client-Wert | Das Client-Geheimnis, das zusammen mit der Client-ID zur Authentifizierung Ihrer App verwendet wird. Sie können Ihr Client-Geheimnis aus dem [!DNL Microsoft Entra ID]-Portal abrufen, in dem Sie Ihre [!DNL Azure Active Directory] registriert haben. |
| Namespace | Der Namespace der [!DNL Event Hub] , auf die Sie zugreifen. Ein Namespace [!DNL Event Hub] bietet einen eindeutigen Scoping-Container, in dem Sie einen oder mehrere [!DNL Event Hubs] erstellen können. |

Weitere Informationen zu [!DNL Azure Active Directory] finden Sie im Leitfaden [Azure zur Verwendung der Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB Ereignis-Hub-Scoped Azure Active Directory Auth]

| Anmeldedaten | Beschreibung |
| --- | --- |
| Mandanten-ID | Die Mandantenkennung, von der Sie die Berechtigung anfordern möchten. Ihre Mandantenkennung kann als GUID oder als benutzerfreundlicher Name formatiert werden. **Hinweis**: Die Mandanten-ID wird in der [!DNL Microsoft Azure] -Benutzeroberfläche als &quot;Verzeichnis-ID&quot;bezeichnet. |
| Client-ID | Die Ihrer App zugewiesene Anwendungs-ID. Sie können diese ID aus dem [!DNL Microsoft Entra ID]-Portal abrufen, in dem Sie Ihre [!DNL Azure Active Directory] registriert haben. |
| Geheimer Client-Wert | Das Client-Geheimnis, das zusammen mit der Client-ID zur Authentifizierung Ihrer App verwendet wird. Sie können Ihr Client-Geheimnis aus dem [!DNL Microsoft Entra ID]-Portal abrufen, in dem Sie Ihre [!DNL Azure Active Directory] registriert haben. |
| Namespace | Der Namespace der [!DNL Event Hub] , auf die Sie zugreifen. Ein Namespace [!DNL Event Hub] bietet einen eindeutigen Scoping-Container, in dem Sie einen oder mehrere [!DNL Event Hubs] erstellen können. |
| Ereignis-Hub-Name | Geben Sie Ihren [!DNL Azure Event Hub] Namen ein. Weitere Informationen zu [!DNL Event Hub] -Namen finden Sie in der [Microsoft-Dokumentation](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) . |

Weitere Informationen zu [!DNL Azure Active Directory] finden Sie im Leitfaden [Azure zur Verwendung der Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!ENDTABS]

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Event Hubs]-Konto mit Experience Platform zu verknüpfen.

## Verbinden Ihres [!DNL Event Hubs]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] enthält verschiedene Quellen, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud-Speicher] die Option **[!UICONTROL Azure Event Hub]** und klicken Sie dann auf **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog mit ausgewählten Azure Event Hubs.](../../../../images/tutorials/create/eventhub/catalog.png)

Das Dialogfeld **[!UICONTROL Verbindung zu Azure Event Hubs herstellen]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das gewünschte [!DNL Event Hubs]-Konto aus und klicken Sie dann auf **[!UICONTROL Weiter]** , um fortzufahren.

![Eine Liste der vorhandenen Quell-Konten der Azure Event-Hubs.](../../../../images/tutorials/create/eventhub/existing.png)

### Neues Konto

>[!TIP]
>
>Nach der Erstellung können Sie den Authentifizierungstyp einer Basis-Verbindung vom Typ [!DNL Event Hubs] nicht mehr ändern. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihr neues [!DNL Event Hubs]-Konto ein.

![Die neue Benutzeroberfläche zur Kontoerstellung für Azure Event-Hub.](../../../../images/tutorials/create/eventhub/new.png)

>[!BEGINTABS]

>[!TAB Standardauthentifizierung]

Um ein [!DNL Event Hubs] -Konto mit Standardauthentifizierung zu erstellen, verwenden Sie das Dropdown-Menü [!UICONTROL Kontoauthentifizierung] und wählen Sie dann **[!UICONTROL Standardauthentifizierung]** aus. Geben Sie als Nächstes Werte für den Namen Ihres [!UICONTROL SAS-Schlüssels], den [!UICONTROL SAS-Schlüssel] und den [!UICONTROL Namespace] an.

Nachdem Sie Ihre Authentifizierungsberechtigungen eingegeben haben, wählen Sie **[!UICONTROL Mit Quelle verbinden]** aus.

![ Die standardmäßige Authentifizierungsschnittstelle für Azure Event-Hub.](../../../../images/tutorials/create/eventhub/standard.png)

>[!TAB SAS-Authentifizierung]

Um ein [!DNL Event Hubs] -Konto mit SAS-Authentifizierung zu erstellen, verwenden Sie das Dropdown-Menü [!UICONTROL Kontoauthentifizierung] und wählen Sie dann **[!UICONTROL SAS-Authentifizierung]** aus. Geben Sie als Nächstes Werte für den Namen Ihres [!UICONTROL SAS-Schlüssels], den [!UICONTROL SAS-Schlüssel], den [!UICONTROL Namespace] und den [!UICONTROL Ereignis-Hubs-Namen] an.

Nachdem Sie Ihre Authentifizierungsberechtigungen eingegeben haben, wählen Sie **[!UICONTROL Mit Quelle verbinden]** aus.

![Die SAS-Authentifizierungsschnittstelle für Azure Event-Hub.](../../../../images/tutorials/create/eventhub/sas.png)

>[!TAB Ereignis-Hub Azure Active Directory Auth]

Um ein [!DNL Event Hubs] -Konto mit der Azure Directory-Authentifizierung für Event Hub Azure zu erstellen, verwenden Sie das Dropdown-Menü [!UICONTROL Kontoauthentifizierung] und wählen Sie dann **[!UICONTROL Event Hub Azure Active Directory]** aus. Geben Sie als Nächstes Werte für die [!UICONTROL Mandanten-ID], die [!UICONTROL Client-ID], den [!UICONTROL Client-Geheimniswert] und den [!UICONTROL Namespace] an.

![Azure Event Hub Azure Active Directory Authentication](../../../../images/tutorials/create/eventhub/active-directory.png)

>[!TAB Ereignis-Hub-Scoped Azure Active Directory Auth]

Um ein [!DNL Event Hubs] -Konto mit Event Hub Scoped Azure Active Directory-Authentifizierung zu erstellen, verwenden Sie das Dropdown-Menü [!UICONTROL Kontoauthentifizierung] und wählen Sie dann **[!UICONTROL Event Hub Scoped Azure Active Directory]** aus. Geben Sie als Nächstes Werte für die [!UICONTROL Mandanten-ID], die [!UICONTROL Client-ID], den [!UICONTROL Client Secret Value], den [!UICONTROL Namespace] und den [!UICONTROL Ereignis-Hub-Namen] an.

![Azure Event Hub Scoped Azure Activity Directory Authentication](../../../../images/tutorials/create/eventhub/scoped.png)

>[!ENDTABS]


## Nächste Schritte

In diesem Tutorial haben Sie Ihr [!DNL Event Hubs]-Konto mit Experience Platform verbunden. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in Experience Platform](../../dataflow/streaming/cloud-storage-streaming.md) zu übertragen.[
