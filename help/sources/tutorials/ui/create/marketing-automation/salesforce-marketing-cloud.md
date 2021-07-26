---
keywords: Experience Platform; Startseite; beliebte Themen; Salesforce Marketing Cloud; Salesforce Marketing Cloud
solution: Experience Platform
title: Erstellen einer Salesforce-Marketing Cloud-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Salesforce Marketing Cloud-Quellverbindung erstellen.
source-git-commit: f196da32f67578ad1d73f3200f6050a7ddab0d88
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 12%

---

# Erstellen einer [!DNL Salesforce Marketing Cloud]-Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
> Die Quelle [!DNL Salesforce Marketing Cloud] befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie unter [Quellenübersicht](../../../../home.md#terms-and-conditions) .

Quell-Connectoren in Adobe Experience Platform bieten die Möglichkeit, extern bezogene Daten auf geplanter Basis zu erfassen. In diesem Tutorial werden die Schritte zum Erstellen eines Quell-Connectors [!DNL Salesforce Marketing Cloud] mithilfe der Platform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) zum Schema Editor: Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine [!DNL Salesforce Marketing Cloud]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Konfigurieren eines Datenflusses [fortfahren.](../../dataflow/marketing-automation.md)

### Erforderliche Anmeldedaten sammeln

Um auf Ihr [!DNL Salesforce Marketing Cloud]-Konto in Platform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Der Host-Server Ihrer Anwendung. Dies ist häufig Ihre Subdomäne. |
| `clientId` | Die Client-ID, die Ihrer [!DNL Salesforce Marketing Cloud]-Anwendung zugeordnet ist. |
| `clientSecret` | Das Client-Geheimnis, das Ihrer [!DNL Salesforce Marketing Cloud]-Anwendung zugeordnet ist. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [[!DNL Salesforce Marketing Cloud] Dokument](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Ihr [!DNL Salesforce Marketing Cloud]-Konto verbinden

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Salesforce Marketing Cloud]-Konto mit Platform zu verknüpfen.

Wählen Sie in der Platform-Benutzeroberfläche **[!UICONTROL Quellen]** aus dem linken Navigationsbereich aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] enthält eine Vielzahl von Quellen, für die Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Sie können auch die Suchleiste verwenden, um die angezeigten Connectoren einzugrenzen.

Wählen Sie unter der Kategorie [!UICONTROL Marketing-Automatisierung] die Option **[!UICONTROL Salesforce-Marketing Cloud]** und klicken Sie dann auf **[!UICONTROL Einrichten]**.

![Katalog](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

Die Seite **[!UICONTROL Verbindung mit Salesforce-Marketing Cloud]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldedaten verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Formular einen Namen, eine optionale Beschreibung und Ihre [!DNL Salesforce Marketing Cloud]-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![new](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Salesforce Marketing Cloud]-Konto aus, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhandene](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Salesforce Marketing Cloud]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten aus dem Marketing-Automatisierungssystem in Platform](../../dataflow/marketing-automation.md) zu importieren.
