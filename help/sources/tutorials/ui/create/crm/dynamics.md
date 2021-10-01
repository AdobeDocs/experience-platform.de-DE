---
keywords: Experience Platform;Startseite;beliebte Themen;Microsoft Dynamics;Microsoft Dynamics;Microsoft Dynamics;Dynamics;Dynamik
solution: Experience Platform
title: Erstellen einer Microsoft Dynamics-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung mit Microsoft Dynamics erstellen.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 10%

---

# Erstellen einer [!DNL Microsoft Dynamics]-Quellverbindung in der Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung mit dem Namen [!DNL Microsoft Dynamics] (im Folgenden &quot;a1/>&quot;) erstellen.[!DNL Dynamics]

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) zum Schema Editor: Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein gültiges [!DNL Dynamics]-Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Konfigurieren eines Datenflusses für eine CRM-Quelle](../../dataflow/crm.md) fortfahren.[

### Erforderliche Anmeldedaten sammeln

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `serviceUri` | Die Dienst-URL Ihrer [!DNL Dynamics]-Instanz. |
| `username` | Der Benutzername für Ihr [!DNL Dynamics]-Benutzerkonto. |
| `password` | Das Kennwort für Ihr [!DNL Dynamics]-Konto. |
| `servicePrincipalId` | Die Client-ID Ihres [!DNL Dynamics]-Kontos. Diese ID ist bei der Verwendung der Service-Prinzipal- und schlüsselbasierten Authentifizierung erforderlich. |
| `servicePrincipalKey` | Der Geheimschlüssel des Dienstprinzips. Diese Berechtigung ist bei der Verwendung von Dienstprinzipal und schlüsselbasierter Authentifizierung erforderlich. |

Weitere Informationen zu den ersten Schritten finden Sie unter [this [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Ihr [!DNL Dynamics]-Konto verbinden

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Dynamics]-Konto mit Platform zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** aus der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** enthält eine Vielzahl von Quellen, für die Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL CRM]** **[!UICONTROL Microsoft Dynamics]** aus. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]** aus. Klicken Sie andernfalls auf **[!UICONTROL Daten hinzufügen]** , um einen neuen [!DNL Dynamics]-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Die Seite **[!UICONTROL Verbindung zu Dynamics]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldedaten verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Formular einen Namen und eine optionale Beschreibung für Ihr neues [!DNL Dynamics]-Konto ein.

Der Connector [!DNL Dynamics] bietet verschiedene Authentifizierungstypen für den Zugriff. Wählen Sie unter [!UICONTROL Kontoauthentifizierung] **[!UICONTROL Standardauthentifizierung]** aus, um kennwortbasierte Anmeldeinformationen zu verwenden.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** aus und lassen Sie dann etwas Zeit für die Einrichtung des neuen Kontos zu.

![basic-authentication](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

Alternativ können Sie **[!UICONTROL Dienstprinzipal und Schlüsselauthentifizierung]** auswählen und Ihr [!DNL Dynamics]-Konto mit einer Kombination aus [!UICONTROL Dienstprinzipal-ID] und [!UICONTROL Dienstprinzipalschlüssel] verbinden.

>[!IMPORTANT]
>
> Die grundlegende Authentifizierung in [!DNL Dynamics] kann durch eine Zwei-Faktor-Authentifizierung blockiert werden, die derzeit von Platform nicht unterstützt wird. In diesem Fall wird empfohlen, die schlüsselbasierte Authentifizierung zu verwenden, um einen Quell-Connector mit [!DNL Dynamics] zu erstellen.

![key-based-authentication](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| [!UICONTROL Service Prinzipal ID] | Die Client-ID Ihres [!DNL Dynamics]-Kontos. Diese ID ist bei der Verwendung der Service-Prinzipal- und schlüsselbasierten Authentifizierung erforderlich. |
| [!UICONTROL Hauptschlüssel des Dienstes] | Der Geheimschlüssel des Dienstprinzips. Diese Berechtigung ist bei der Verwendung von Dienstprinzipal und schlüsselbasierter Authentifizierung erforderlich. |

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Dynamics]-Konto aus, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann in der oberen rechten Ecke auf **[!UICONTROL Weiter]** , um fortzufahren.

![vorhandene](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Dynamics]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in Platform](../../dataflow/crm.md) zu importieren.
