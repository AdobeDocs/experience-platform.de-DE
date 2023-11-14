---
title: Erstellen einer Amazon Redshift-Quellverbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie eine Amazon Redshift-Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche erstellen.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 41%

---

# Verbinden Sie [!DNL Amazon Redshift] Konto, das den Arbeitsbereich &quot;Quellen&quot;verwendet

>[!IMPORTANT]
>
>Die [!DNL Amazon Redshift] -Quelle ist im Quellkatalog für Benutzer verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.

In diesem Tutorial erfahren Sie, wie Sie Ihre [!DNL Amazon Redshift] (nachstehend &quot;genannt)[!DNL Redshift]&quot;) über die Benutzeroberfläche für Adobe Experience Platform.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   - [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Redshift]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/databases.md) fortfahren.

### Sammeln erforderlicher Anmeldeinformationen

Um auf Ihre [!DNL Redshift] -Konto auf Experience Platform angegeben haben, müssen Sie die folgenden Werte angeben:

| **Anmeldedaten** | **Beschreibung** |
| -------------- | --------------- |
| Server | Der mit Ihrem [!DNL Redshift] -Konto. |
| Port | Der TCP-Port, der [!DNL Redshift] -Server verwendet , um auf Client-Verbindungen zu warten. |
| Benutzername | Der mit Ihrer [!DNL Redshift] -Konto. |
| Kennwort | Das Kennwort für Ihre [!DNL Redshift] -Konto. |
| Datenbank | Die [!DNL Redshift] Datenbank, auf die Sie zugreifen. |

Weitere Informationen zu den ersten Schritten finden Sie unter [this [!DNL Redshift] Dokument](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihre [!DNL Redshift] -Konto auf Experience Platform.

## Verbinden Ihres [!DNL Redshift]-Kontos

>[!NOTE]
>
>Der standardmäßige Kodierungsstandard für [!DNL Redshift] ist Unicode. Dies kann nicht geändert werden.

Anmelden bei [Adobe Experience Platform](https://platform.adobe.com) und wählen Sie **[!UICONTROL Quellen]** über die linke Navigationsleiste auf **[!UICONTROL Quellen]** Arbeitsbereich. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem **[!UICONTROL Datenbanken]** category, select **[!UICONTROL Amazon Redshift]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Daten hinzufügen]** , um eine neue [!DNL Redshift] Connector.

![](../../../../images/tutorials/create/redshift/catalog.png)

Die **[!UICONTROL Verbinden mit Amazon Redshift]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Formular einen Namen, eine optionale Beschreibung und Ihre [!DNL Redshift] Anmeldedaten. Wählen Sie zum Abschluss **[!UICONTROL Verbinden]** und dann etwas Zeit für die Einrichtung der neuen Verbindung.

![](../../../../images/tutorials/create/redshift/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie die [!DNL Redshift] Konto, mit dem Sie eine Verbindung herstellen möchten, wählen Sie **[!UICONTROL Nächste]** um fortzufahren.

![](../../../../images/tutorials/create/redshift/existing.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Redshift]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [Datenfluss konfigurieren, um Daten in Experience Platform zu übertragen](../../dataflow/databases.md).
