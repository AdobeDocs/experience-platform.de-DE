---
title: Erstellen einer Amazon Redshift Source-Verbindung über die Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Amazon Redshift-Quellverbindung erstellen.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 41%

---

# Verbinden Ihres [!DNL Amazon Redshift]-Kontos mithilfe des Arbeitsbereichs Quellen

>[!IMPORTANT]
>
>Die [!DNL Amazon Redshift] ist im Quellkatalog für Benutzende verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.

In diesem Tutorial erfahren Sie, wie Sie Ihr [!DNL Amazon Redshift]-Konto (im Folgenden als &quot;[!DNL Redshift]&quot; bezeichnet) über die Benutzeroberfläche mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   - [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Redshift]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/databases.md) fortfahren.

### Sammeln erforderlicher Anmeldedaten

Um auf Ihr [!DNL Redshift]-Konto auf Experience Platform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| **Anmeldedaten** | **Beschreibung** |
| -------------- | --------------- |
| Server | Der mit Ihrem [!DNL Redshift]-Konto verknüpfte Server. |
| Port | Der TCP-Port, den ein [!DNL Redshift]-Server verwendet, um auf Client-Verbindungen zu warten. |
| Benutzername | Der Benutzername, der Ihrem [!DNL Redshift]-Konto zugeordnet ist. |
| Kennwort | Das mit Ihrem [!DNL Redshift]-Konto verknüpfte Kennwort. |
| Datenbank | Die [!DNL Redshift] Datenbank, auf die Sie zugreifen. |

Weitere Informationen zu den ersten Schritten finden Sie [diesem [!DNL Redshift] Dokument](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Redshift]-Konto mit Experience Platform zu verknüpfen.

## Verbinden Ihres [!DNL Redshift]-Kontos

>[!NOTE]
>
>Der Standardcodierungsstandard für [!DNL Redshift] ist Unicode. Dies kann nicht geändert werden.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der **[!UICONTROL Datenbanken]** die Option **[!UICONTROL Amazon Redshift]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]** aus. Wählen Sie andernfalls **[!UICONTROL Daten hinzufügen]** aus, um einen neuen [!DNL Redshift]-Connector zu erstellen.

![](../../../../images/tutorials/create/redshift/catalog.png)

Die **[!UICONTROL Mit Amazon Redshift verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldedaten verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Eingabeformular einen Namen, eine optionale Beschreibung und Ihre [!DNL Redshift] Anmeldeinformationen ein. Wenn Sie fertig sind, wählen **[!UICONTROL Verbinden]** und warten Sie dann einige Zeit, bis die neue Verbindung hergestellt ist.

![](../../../../images/tutorials/create/redshift/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Redshift] Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![](../../../../images/tutorials/create/redshift/existing.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Redshift]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten auf Experience Platform zu übertragen](../../dataflow/databases.md).
