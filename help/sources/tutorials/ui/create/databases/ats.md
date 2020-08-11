---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Quellconnectors für die Datenspeicherung eines Blauen Diagramms in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 14%

---


# Create an [!DNL Azure Table Storage] source connector in the UI

>[!NOTE]
>Der [!DNL Azure Table Storage] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Erstellen eines [!DNL Azure Table Storage] (im Folgenden &quot;ATS&quot;) Quell-Connectors mithilfe der [!DNL Platform] Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)-System](../../../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Kundenprofil](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige ATS-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/databases.md)fortfahren.

### Erforderliche Anmeldedaten sammeln

Um auf Ihr ATS-Konto zugreifen zu können, müssen Sie [!DNL Platform]folgende Werte angeben:

| Credential | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Eine Verbindungszeichenfolge, die mit Ihrer [!DNL Azure Table Storage] Instanz verbunden werden soll. Die Verbindungszeichenfolge, mit der eine Verbindung zur ATS-Instanz hergestellt werden soll. Das Verbindungszeichenfolgen-Muster für ATS ist `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`festgelegt. |

For more information about getting started refer to [this Azure Table Storage document](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

## Verbinden Sie Ihr [!DNL Azure Table Storage] Konto

Once you have gathered your required credentials, you can follow the steps below to create a new ATS account to connect to [!DNL Platform].

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den *[!UICONTROL Quellarbeitsbereich]* zuzugreifen. Im Anzeigebereich &quot; *[!UICONTROL Katalog]* &quot;werden eine Reihe von Quellen angezeigt, für die Sie ein Inbound-Konto erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse, die ihnen zugeordnet sind.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternatively, you can find the specific source you wish to work with using the search option.

Wählen Sie unter der Kategorie &quot; *[!UICONTROL Datenbanken]* &quot;die Option &quot; **[!UICONTROL Blaue Datenspeicherung]** &quot;, um eine Informationsleiste auf der rechten Seite Ihres Bildschirms anzuzeigen. The information bar provides a brief description for the selected source as well as options to connect with the source or view its documentation. To create a new inbound connection, select **[!UICONTROL Add data]**.

![catalog](../../../../images/tutorials/create/ats/catalog.png)

Die Seite &quot; *[!UICONTROL Verbindung mit der Datenspeicherung]* des Blauen Tischs herstellen&quot;wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### New account

If you are using new credentials, select **[!UICONTROL New account]**. Geben Sie im angezeigten Eingabedatum einen Namen, eine optionale Beschreibung und Ihre ATS-Anmeldeinformationen für die Verbindung ein. When finished, select **[!UICONTROL Connect]** and then allow some time for the new account to establish.

![connect](../../../../images/tutorials/create/ats/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das ATS-Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** , um fortzufahren.

![existing](../../../../images/tutorials/create/ats/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem ATS-Konto hergestellt. You can now continue on to the next tutorial and [configure a dataflow to bring data into Platform](../../dataflow/databases.md).