---
title: Verbinden Ihres Salesforce-Marketing Cloud-Kontos mit dem Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie über die Benutzeroberfläche Ihr Salesforce-Marketing Cloud-Konto mit Experience Platform verbinden.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 997a9dc70145a8cfd5d6da20ba788a4610e5c257
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 27%

---

# Verbinden Sie [!DNL Salesforce Marketing Cloud] Experience Platform über die Benutzeroberfläche

>[!IMPORTANT]
>
>Die Erfassung benutzerdefinierter Objekte wird derzeit nicht von der [!DNL Salesforce Marketing Cloud] Quellintegration.


In diesem Tutorial erfahren Sie, wie Sie Ihre [!DNL Salesforce Marketing Cloud] -Konto über die Benutzeroberfläche in Adobe Experience Platform.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine [!DNL Salesforce Marketing Cloud] -Konto verwenden, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Einbringen von Daten zur Marketing-Automatisierung zum Experience Platform über die Benutzeroberfläche](../../dataflow/marketing-automation.md).

### Sammeln erforderlicher Anmeldeinformationen

Um auf Ihr [!DNL Salesforce Marketing Cloud]-Konto in Platform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| Host | Der Host-Server Ihrer Anwendung. Dies ist häufig Ihre Subdomäne. **Hinweis:** Wenn Sie `host` -Wert, müssen Sie nur die Subdomain und nicht die gesamte URL angeben. Wenn Ihre Host-URL beispielsweise `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`eingeben, müssen Sie nur `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` als Hostwert. |
| Client-ID | Die mit Ihrer [!DNL Salesforce Marketing Cloud] Anwendung. |
| Client-Geheimnis | Das Client-Geheimnis, das mit Ihrem [!DNL Salesforce Marketing Cloud] Anwendung. |

Weitere Informationen zur Authentifizierung für [!DNL Salesforce Marketing Cloud], besuchen Sie die [[!DNL Salesforce] Authentifizierungsdokumentation](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Verbinden Ihres [!DNL Salesforce Marketing Cloud]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, die von Experience Platform unterstützt werden.

Sie können die gewünschte Kategorie aus der Liste der Kategorien auswählen. Sie können auch die Suchleiste verwenden, um nach einer bestimmten Quelle zu filtern.

Unter dem [!UICONTROL Marketing-Automatisierung] category, select **[!UICONTROL Salesforce-Marketing Cloud]** und wählen Sie **[!UICONTROL Einrichten]**.

![Der Quellkatalog mit der ausgewählten Salesforce-Marketing Cloud-Quelle.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

Die **[!UICONTROL Mit Salesforce-Marketing Cloud verbinden]** angezeigt. Auf dieser Seite können Sie entweder ein neues Konto erstellen oder ein vorhandenes Konto verwenden.

### Neues Konto

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie einen Namen für Ihr Konto, eine optionale Beschreibung und die Authentifizierungsberechtigungen an, die Ihrer [!DNL Salesforce Marketing Cloud] -Konto.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle, über die Sie ein neues Konto für Salesforce Marketing Cloud authentifizieren können.](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Vorhandenes Konto

Wenn Sie bereits über ein bestehendes Konto verfügen, wählen Sie **[!UICONTROL Vorhandenes Konto]** und wählen Sie dann das Konto, das Sie verwenden möchten, aus der angezeigten Liste aus.

![Die bestehende Kontoschnittstelle, über die Sie aus einer Liste vorhandener Salesforce Marketing Cloud-Konten auswählen können.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zwischen Ihrem [!DNL Salesforce Marketing Cloud] Konto und Experience Platform. Sie können jetzt mit dem nächsten Tutorial fortfahren und [Erstellen eines Datenflusses, um Ihre Daten zur Marketing-Automatisierung in Experience Platform zu bringen](../../dataflow/marketing-automation.md).
