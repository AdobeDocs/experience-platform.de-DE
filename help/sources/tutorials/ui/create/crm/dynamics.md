---
keywords: Experience Platform;Startseite;beliebte Themen;Microsoft Dynamics;Microsoft Dynamics;Dynamics;Dynamics
solution: Experience Platform
title: Erstellen einer Microsoft Dynamics Source-Verbindung über die Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Microsoft Dynamics-Quellverbindung erstellen.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 25%

---

# Erstellen eines Quell-Connectors für [!DNL Microsoft Dynamics] in der Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine [!DNL Microsoft Dynamics]-Quellverbindung (im Folgenden als &quot;[!DNL Dynamics]&quot; bezeichnet) erstellen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein gültiges [!DNL Dynamics]-Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [ eines Datenflusses für eine CRM-Quelle fortfahren](../../dataflow/crm.md).

### Sammeln erforderlicher Anmeldedaten

Um Ihre [!DNL Dynamics] zu authentifizieren, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `serviceUri` | Die Service-URL Ihrer [!DNL Dynamics]. |
| `username` | Der Benutzername für Ihr [!DNL Dynamics] Benutzerkonto. |
| `password` | Das Kennwort für Ihr [!DNL Dynamics]. |

>[!TAB Service-Prinzipal- und Schlüsselauthentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `servicePrincipalId` | Die Client-ID Ihres [!DNL Dynamics]. Diese ID ist erforderlich, wenn die Service-Prinzipal- und schlüsselbasierte Authentifizierung verwendet wird. |
| `servicePrincipalKey` | Der geheime Schlüssel des Service-Prinzipals. Diese Berechtigung ist erforderlich, wenn die Authentifizierung über einen Service-Prinzipal und einen Schlüssel verwendet wird. |

>[!ENDTABS]

Weitere Informationen zu den ersten Schritten finden Sie [diesem  [!DNL Dynamics] Dokument](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Verbinden Ihres [!DNL Dynamics]-Kontos

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter [!UICONTROL CRM]-Kategorie **[!UICONTROL Microsoft Dynamics]** und dann **[!UICONTROL Daten hinzufügen]** aus.

![Der Quellkatalog, wobei Microsoft Dynamics ausgewählt wurde.](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Die **[!UICONTROL Microsoft Dynamics-Konto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Dynamics] Konto, das Sie verwenden möchten, und wählen Sie dann **[!UICONTROL Weiter]** in der oberen rechten Ecke, um fortzufahren.

![Die vorhandene Kontoschnittstelle.](../../../../images/tutorials/create/ms-dynamics/existing.png)

### Neues Konto

>[!TIP]
>
>Nach der Erstellung können Sie den Authentifizierungstyp einer [!DNL Dynamics] Basisverbindung nicht mehr ändern. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihr neues [!DNL Dynamics]-Konto an.

![Die Benutzeroberfläche zur Erstellung neuer Konten.](../../../../images/tutorials/create/ms-dynamics/new.png)

Sie können beim Erstellen eines [!DNL Dynamics]-Kontos entweder die Standardauthentifizierung oder die Service-Prinzipal- und Schlüsselauthentifizierung verwenden.

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

Um ein [!DNL Dynamics] Konto mit einfacher Authentifizierung zu erstellen, wählen Sie [!UICONTROL Standardauthentifizierung] und geben Sie dann Werte für Ihren [!UICONTROL Service-URI], [!UICONTROL Benutzername] und [!UICONTROL Kennwort] an. **Hinweis**: Die Standardauthentifizierung in [!DNL Dynamics] kann durch die Zwei-Faktor-Authentifizierung blockiert werden, die derzeit von Experience Platform nicht unterstützt wird. In diesem Fall wird empfohlen, eine schlüsselbasierte Authentifizierung zu verwenden, um einen Quell-Connector mithilfe von [!DNL Dynamics] zu erstellen.

Wenn Sie fertig sind, wählen **[!UICONTROL Mit Quelle verbinden]** und warten Sie dann einige Zeit, bis das neue Konto eingerichtet ist.

![Die grundlegende Authentifizierungsschnittstelle.](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB Service-Prinzipal- und Schlüsselauthentifizierung]

Um ein [!DNL Dynamics] Konto mit Service-Prinzipal- und Schlüsselauthentifizierung zu erstellen, wählen Sie **[!UICONTROL Service-Prinzipal- und Schlüsselauthentifizierung]** aus und geben Sie dann Werte für Ihre [!UICONTROL Service-Prinzipal-ID] und [!UICONTROL Service-Prinzipalschlüssel] an.

Wenn Sie fertig sind, wählen **[!UICONTROL Mit Quelle verbinden]** und warten Sie dann einige Zeit, bis das neue Konto eingerichtet ist.

![Die Authentifizierungsschnittstelle für den Service-Prinzipal-Schlüssel.](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Dynamics]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in Experience Platform zu importieren](../../dataflow/crm.md).
