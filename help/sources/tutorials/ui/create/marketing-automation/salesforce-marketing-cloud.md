---
keywords: Experience Platform; Startseite; beliebte Themen; Salesforce Marketing Cloud; Salesforce Marketing Cloud
solution: Experience Platform
title: Erstellen einer Salesforce-Marketing Cloud-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Salesforce Marketing Cloud-Quellverbindung erstellen.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 45%

---

# Erstellen eines Quell-Connectors für [!DNL Salesforce Marketing Cloud] in der Benutzeroberfläche

>[!NOTE]
>
> Die [!DNL Salesforce Marketing Cloud]-Quelle befindet sich in der Beta-Phase. Siehe [Quellen – Übersicht](../../../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-gekennzeichneten Quellen.

Quell-Connectoren in Adobe Experience Platform bieten die Möglichkeit, extern bezogene Daten auf geplanter Basis zu erfassen. In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Salesforce Marketing Cloud] Quell-Connector über die Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine [!DNL Salesforce Marketing Cloud] Verbindung nutzen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Datenfluss konfigurieren](../../dataflow/marketing-automation.md).

### Sammeln erforderlicher Anmeldeinformationen

Um auf Ihr [!DNL Salesforce Marketing Cloud]-Konto in Platform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `host` | Der Host-Server Ihrer Anwendung. Dies ist häufig Ihre Subdomäne. **Hinweis:** Wenn Sie `host` -Wert, müssen Sie nur die Subdomain und nicht die gesamte URL angeben. Wenn Ihre Host-URL beispielsweise `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`eingeben, müssen Sie nur `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` als Hostwert. |
| `clientId` | Die mit Ihrer [!DNL Salesforce Marketing Cloud] Anwendung. |
| `clientSecret` | Das Client-Geheimnis, das mit Ihrem [!DNL Salesforce Marketing Cloud] Anwendung. |

Weiterführende Informationen zu den ersten Schritten finden Sie in diesem Abschnitt [[!DNL Salesforce Marketing Cloud] Dokument](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Verbinden Ihres [!DNL Salesforce Marketing Cloud]-Kontos

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Salesforce Marketing Cloud]-Konto mit Platform zu verknüpfen.

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Sie können auch die Suchleiste verwenden, um die angezeigten Connectoren einzugrenzen.

Unter dem [!UICONTROL Marketing-Automatisierung] category, select **[!UICONTROL Salesforce-Marketing Cloud]** und wählen Sie **[!UICONTROL Einrichten]**.

![Katalog](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

Die **[!UICONTROL Mit Salesforce-Marketing Cloud verbinden]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Formular einen Namen, eine optionale Beschreibung und Ihre [!DNL Salesforce Marketing Cloud] Anmeldedaten. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und dann etwas Zeit für die Einrichtung der neuen Verbindung.

![neu](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie die [!DNL Salesforce Marketing Cloud] Konto, mit dem Sie eine Verbindung herstellen möchten, wählen Sie **[!UICONTROL Nächste]** um fortzufahren.

![vorhanden](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Salesforce Marketing Cloud]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Systemdaten der Marketing-Automatisierung in Platform zu importieren](../../dataflow/marketing-automation.md).
