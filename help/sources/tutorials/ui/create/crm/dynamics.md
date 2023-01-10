---
keywords: Experience Platform;Startseite;beliebte Themen;Microsoft Dynamics;Mikrosoft dynamics;Dynamics;Dynamik
solution: Experience Platform
title: Erstellen einer Microsoft Dynamics-Quellverbindung in der Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung mit Microsoft Dynamics erstellen.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 37%

---

# Erstellen eines Quell-Connectors für [!DNL Microsoft Dynamics] in der Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Microsoft Dynamics] (nachstehend &quot;genannt)[!DNL Dynamics]&quot;) Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Dynamics] -Konto verwenden, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Datenfluss für eine CRM-Quelle konfigurieren](../../dataflow/crm.md).

### Sammeln erforderlicher Anmeldeinformationen

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `serviceUri` | Die Dienst-URL Ihrer [!DNL Dynamics] -Instanz. |
| `username` | Der Benutzername für Ihre [!DNL Dynamics] Benutzerkonto. |
| `password` | Das Kennwort für Ihre [!DNL Dynamics] -Konto. |
| `servicePrincipalId` | Die Client-ID Ihrer [!DNL Dynamics] -Konto. Diese ID ist bei der Verwendung der Service-Prinzipal- und schlüsselbasierten Authentifizierung erforderlich. |
| `servicePrincipalKey` | Der Geheimschlüssel des Dienstprinzips. Diese Berechtigung ist bei der Verwendung von Dienstprinzipal und schlüsselbasierter Authentifizierung erforderlich. |

Weitere Informationen zu den ersten Schritten finden Sie unter [this [!DNL Dynamics] Dokument](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Verbinden Ihres [!DNL Dynamics]-Kontos

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Dynamics]-Konto mit Platform zu verknüpfen.

Anmelden bei [Adobe Experience Platform](https://platform.adobe.com) und wählen Sie **[!UICONTROL Quellen]** über die linke Navigationsleiste, um auf die [!UICONTROL Quellen] Arbeitsbereich. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem **[!UICONTROL CRM]** category, select **[!UICONTROL Microsoft Dynamics]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Daten hinzufügen]** , um eine neue [!DNL Dynamics] Connector.

![Katalog](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Die **[!UICONTROL Verbindung zu Dynamics herstellen]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Formular einen Namen und eine optionale Beschreibung für Ihre neue [!DNL Dynamics] -Konto.

Die [!DNL Dynamics] Der Connector bietet verschiedene Authentifizierungstypen für den Zugriff. under [!UICONTROL Kontoauthentifizierung] select **[!UICONTROL Grundlegende Authentifizierung]** , um kennwortbasierte Anmeldeinformationen zu verwenden.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbindung mit Quelle herstellen]** und dann etwas Zeit für die Einrichtung des neuen Kontos.

![basic-authentication](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

Alternativ können Sie **[!UICONTROL Service-Prinzipal- und Schlüsselauthentifizierung]** und verbinden Sie Ihre [!DNL Dynamics] -Konto mit einer Kombination aus [!UICONTROL Service Prinzipal ID] und [!UICONTROL Hauptschlüssel des Dienstes].

>[!IMPORTANT]
>
> Grundlegende Authentifizierung in [!DNL Dynamics] kann durch Authentifizierung mit zwei Faktoren blockiert werden, die derzeit nicht von Platform unterstützt wird. In diesem Fall wird empfohlen, die schlüsselbasierte Authentifizierung zu verwenden, um einen Quell-Connector mit [!DNL Dynamics].

![key-based-authentication](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| [!UICONTROL Service Prinzipal ID] | Die Client-ID Ihrer [!DNL Dynamics] -Konto. Diese ID ist bei der Verwendung der Service-Prinzipal- und schlüsselbasierten Authentifizierung erforderlich. |
| [!UICONTROL Hauptschlüssel des Dienstes] | Der Geheimschlüssel des Dienstprinzips. Diese Berechtigung ist bei der Verwendung von Dienstprinzipal und schlüsselbasierter Authentifizierung erforderlich. |

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie die [!DNL Dynamics] Konto, mit dem Sie eine Verbindung herstellen möchten, wählen Sie **[!UICONTROL Nächste]** in der oberen rechten Ecke, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Dynamics]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen [Datenfluss konfigurieren, um Daten in Platform zu importieren](../../dataflow/crm.md).
