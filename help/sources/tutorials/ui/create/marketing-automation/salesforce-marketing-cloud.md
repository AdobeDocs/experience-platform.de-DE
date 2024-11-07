---
title: Verbinden Ihres Salesforce-Marketing Cloud-Kontos mit dem Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie über die Benutzeroberfläche Ihr Salesforce Marketing Cloud-Konto mit Experience Platform verbinden.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: a32d0d7ed7d18454099d2b55b3f6809cfbcd9b62
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 27%

---

# Verbinden Ihres [!DNL Salesforce Marketing Cloud]-Kontos mit Experience Platform über die Benutzeroberfläche

>[!IMPORTANT]
>
>Die Quelle [!DNL Salesforce Marketing Cloud] wird Ende Mai 2025 nicht mehr unterstützt.

In diesem Tutorial erfahren Sie, wie Sie Ihr [!DNL Salesforce Marketing Cloud]-Konto über die Benutzeroberfläche mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein [!DNL Salesforce Marketing Cloud] -Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Thema [Bringen von Daten zur Marketing-Automatisierung über die Benutzeroberfläche](../../dataflow/marketing-automation.md) an Experience Platform fortfahren.

### Sammeln erforderlicher Anmeldedaten

Um auf Ihr [!DNL Salesforce Marketing Cloud]-Konto in Platform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| Host | Der Host-Server Ihrer Anwendung. Dies ist häufig Ihre Subdomäne. **Hinweis:** Bei der Eingabe Ihres `host` -Werts müssen Sie den `{subdomain}.rest.marketingcloudapis.com` angeben. Wenn Ihre Host-URL beispielsweise `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/` ist, müssen Sie `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` als Hostwert eingeben. |
| Client-ID | Die mit Ihrer [!DNL Salesforce Marketing Cloud] -Anwendung verknüpfte Client-ID. |
| Client-Geheimnis | Das Client-Geheimnis, das Ihrer [!DNL Salesforce Marketing Cloud]-Anwendung zugeordnet ist. |

Weitere Informationen zur Authentifizierung für [!DNL Salesforce Marketing Cloud] finden Sie in der [[!DNL Salesforce] Authentifizierungsdokumentation](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Verbinden Ihres [!DNL Salesforce Marketing Cloud]-Kontos

>[!IMPORTANT]
>
>Die Erfassung benutzerdefinierter Objekte wird von der Quellintegration für [!DNL Salesforce Marketing Cloud] derzeit nicht unterstützt.

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, die von Experience Platform unterstützt werden.

Sie können die gewünschte Kategorie aus der Liste der Kategorien auswählen. Sie können auch die Suchleiste verwenden, um nach einer bestimmten Quelle zu filtern.

Wählen Sie unter der Kategorie [!UICONTROL Marketing-Automatisierung] die Option **[!UICONTROL Salesforce-Marketing Cloud]** und dann **[!UICONTROL Einrichten]** aus.

![Der Quellkatalog mit der ausgewählten Salesforce-Marketing Cloud-Quelle.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

Die Seite **[!UICONTROL Verbindung mit Salesforce Marketing Cloud herstellen]** wird angezeigt. Auf dieser Seite können Sie entweder ein neues Konto erstellen oder ein vorhandenes Konto verwenden.

### Neues Konto

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** aus und geben Sie einen Namen für Ihr Konto, eine optionale Beschreibung und die Authentifizierungsberechtigungen an, die Ihrem [!DNL Salesforce Marketing Cloud]-Konto entsprechen.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle, über die Sie ein neues Konto für Salesforce Marketing Cloud authentifizieren können.](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Vorhandenes Konto

Wenn Sie bereits über ein vorhandenes Konto verfügen, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das Konto, das Sie verwenden möchten, aus der angezeigten Liste aus.

![Die vorhandene Kontoschnittstelle, über die Sie aus einer Liste vorhandener Salesforce Marketing Cloud-Konten auswählen können.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zwischen Ihrem [!DNL Salesforce Marketing Cloud]-Konto und Experience Platform hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss erstellen, um Ihre Daten zur Marketing-Automatisierung in Experience Platform](../../dataflow/marketing-automation.md) zu importieren.
