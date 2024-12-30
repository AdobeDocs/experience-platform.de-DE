---
keywords: Experience Platform;Startseite;beliebte Themen;Azure Table Storage;Azure Table Storage;ats;ATS
solution: Experience Platform
title: Erstellen einer Azure Table Storage-Source-Verbindung über die Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Azure Table Storage-Quellverbindung erstellen.
exl-id: 045cb954-e3e1-439d-a3cd-170d688dfbc8
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 34%

---

# Erstellen einer [!DNL Azure Table Storage]-Quellverbindung über die Benutzeroberfläche

Source-Connectoren in Adobe Experience Platform bieten die Möglichkeit, Daten aus externen Quellen nach einem bestimmten Zeitplan aufzunehmen. In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Azure Table Storage]-Quell-Connectors (im Folgenden als „ATS“ bezeichnet) über die [!DNL Platform]-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige ATS-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [ eines Datenflusses ](../../dataflow/databases.md).

### Sammeln erforderlicher Anmeldedaten

Um auf Ihr ATS-Konto in [!DNL Platform] zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Eine Verbindungszeichenfolge für die Verbindung mit Ihrer [!DNL Azure Table Storage]. Die Verbindungszeichenfolge für die Verbindung zur ATS-Instanz. Das Verbindungszeichenfolgenmuster für ATS ist `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Weitere Informationen zu den ersten Schritten finden Sie [diesem [!DNL Azure Table Storage] Dokument](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

## Verbinden Ihres [!DNL Azure Table Storage]-Kontos

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihr ATS-Konto mit [!DNL Platform] zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter **[!UICONTROL Kategorie]** die Option **[!UICONTROL Azure Table Storage]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]** aus. Wählen Sie andernfalls **[!UICONTROL Daten hinzufügen]**, um einen neuen ATS-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/ats/catalog.png)

Die **[!UICONTROL Mit Azure Table Storage verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldedaten verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Eingabeformular einen Namen, eine optionale Beschreibung und Ihre ATS-Anmeldeinformationen ein. Wenn Sie fertig sind, wählen **[!UICONTROL Verbinden]** und warten Sie dann einige Zeit, bis die neue Verbindung hergestellt ist.

![Verbinden](../../../../images/tutorials/create/ats/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das ATS-Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/ats/existing.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem ATS-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in zu importieren [!DNL Platform]](../../dataflow/databases.md).
