---
title: Salesforce-Konto über die Experience Platform-Benutzeroberfläche verbinden
description: Erfahren Sie, wie Sie Ihr Salesforce-Konto verbinden und Ihre CRM-Daten mithilfe der Benutzeroberfläche in die Experience Platform bringen.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: 57cdcbd5018e7f57261f09c6bddf5e2a8dcfd0d5
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 31%

---

# Verbinden Sie [!DNL Salesforce] Konto für die Experience Platform über die Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie Ihre [!DNL Salesforce] und bringen Sie Ihre CRM-Daten über die Experience Platform-Benutzeroberfläche in Adobe Experience Platform mit.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine authentifizierte [!DNL Salesforce] -Konto verwenden, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Datenfluss für CRM-Daten konfigurieren](../../dataflow/crm.md).

### Sammeln erforderlicher Anmeldeinformationen {#gather-required-credentials}

Um Ihre [!DNL Salesforce] -Konto und -Experience Platform vergleichen, müssen Sie Werte angeben, die den folgenden [!DNL Salesforce] Anmeldeinformationen:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `environmentUrl` | Die URL der [!DNL Salesforce] Quellinstanz. |
| `username` | Der Benutzername für die [!DNL Salesforce] Benutzerkonto. |
| `password` | Das Kennwort für die [!DNL Salesforce] Benutzerkonto. |
| `securityToken` | Das Sicherheits-Token für [!DNL Salesforce] Benutzerkonto. |
| `apiVersion` | (Optional) Die REST-API-Version der [!DNL Salesforce] -Instanz, die Sie verwenden. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. |

Weitere Informationen zur Authentifizierung finden Sie unter [this [!DNL Salesforce] Authentifizierungshandbuch](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

Nachdem Sie die erforderlichen Anmeldedaten erfasst haben, können Sie die folgenden Schritte ausführen, um Ihre [!DNL Salesforce] -Konto in die Experience Platform.

## Verbinden Ihres [!DNL Salesforce]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** über das linke Navigationsmenü aus, um auf den Arbeitsbereich &quot;Quellen&quot;zuzugreifen. Die *[!UICONTROL Katalog]* -Bildschirm zeigt eine Vielzahl von Quellen an, die im Experience Platform-Quellkatalog verfügbar sind.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie eine bestimmte Quelle mithilfe der Suchoption finden.

Auswählen **[!UICONTROL CRM]** aus der Liste der Quellkategorien und wählen Sie **[!UICONTROL Daten hinzufügen]** aus dem [!DNL Salesforce] Karte.

![Der Quellkatalog auf der Experience Platform-Benutzeroberfläche mit der ausgewählten Salesforce-Quellkarte.](../../../../images/tutorials/create/salesforce/catalog.png)

Die **[!UICONTROL Mit Salesforce verbinden]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

>[!BEGINTABS]

>[!TAB Vorhandenes Salesforce-Konto verwenden]

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das Konto, das Sie verwenden möchten, aus der angezeigten Liste aus. Wählen Sie zum Abschluss **[!UICONTROL Nächste]** um fortzufahren.

![Eine Liste authentifizierter Salesforce-Konten, die bereits in Ihrem Unternehmen vorhanden sind.](../../../../images/tutorials/create/salesforce/existing.png)

>[!TAB Neues Salesforce-Konto erstellen]

Um ein neues Konto zu verwenden, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie einen Namen, eine Beschreibung und Ihre [!DNL Salesforce] Authentifizierungsberechtigungen. Wählen Sie zum Abschluss **[!UICONTROL Verbindung mit Quelle herstellen]** und lassen einige Sekunden zu, bis die neue Verbindung hergestellt ist.

![Die Oberfläche, in der Sie ein neues Salesforce-Konto erstellen können, indem Sie die entsprechenden Authentifizierungsberechtigungen angeben.](../../../../images/tutorials/create/salesforce/new.png)

>[!ENDTABS]

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Salesforce]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen [Datenfluss konfigurieren, um Daten in zu importieren [!DNL Platform]](../../dataflow/crm.md).
