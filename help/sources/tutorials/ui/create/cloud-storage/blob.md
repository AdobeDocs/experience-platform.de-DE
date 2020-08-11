---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Azurblauch-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 598b29f681ac930a4e1781f7f298608c8344d807
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 15%

---


# Create an [!DNL Azure Blob] source connector in the UI

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Erstellen eines [!DNL Azure Blob] (im Folgenden &quot;Blob&quot; genannt) mithilfe der [!DNL Platform] Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Experience-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [Echtzeit-Kundenprofil](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

If you already have a Blob base connection, you may skip the remainder of this document and proceed to the tutorial on [configuring a dataflow](../../dataflow/batch/cloud-storage.md).

### Unterstützte Dateiformate

[!DNL Experience Platform] unterstützt die folgenden Dateiformate, die von externen Datenspeicherung erfasst werden:

- Delimiter-separated values (DSV): Support for DSV formatted data files is currently limited to comma-separated values. The value of field headers within DSV formatted files must only consist of alphanumeric characters and underscores. Die Unterstützung für allgemeine DSV-Dateien wird in Zukunft bereitgestellt.
- JavaScript Object Notation (JSON): JSON-formatierte Datendateien müssen XDM-kompatibel sein.
- Apache Parquet: Parquet-formatierte Datendateien müssen XDM-konform sein.

### Erforderliche Anmeldedaten sammeln

In order to access your Blob storage on [!DNL Platform], you must provide a valid value for the following credential:

| Credential | Beschreibung |
| ---------- | ----------- |
| `connectionString` | The connection string required to access data in your Blob storage. The Blob connection string pattern is: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Für weitere Informationen über den Einstieg besuchen Sie [dieses blaue Blob Dokument](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string).

## Connect your Blob account

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues Blob-Konto für die Verbindung zu erstellen [!DNL Platform].

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den *[!UICONTROL Quellarbeitsbereich]* zuzugreifen. Im Anzeigebereich &quot; *[!UICONTROL Katalog]* &quot;werden verschiedene Quellen angezeigt, mit denen Sie ein eingehendes Konto erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse an, die mit ihnen verbunden sind.

You can select the appropriate category from the catalog on the left-hand side of your screen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie &quot; *[!UICONTROL Datenbanken]* &quot;die Option **[!UICONTROL Azurblase-Datenspeicherung]** gefolgt von **[!UICONTROL Hinzufügen Daten]** , um einen neuen [!DNL Blob]Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/blob/catalog.png)

Die Seite &quot; *[!UICONTROL Verbindung mit der Blase-Datenspeicherung]* herstellen&quot;wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im angezeigten Eingabedatum einen Namen, eine optionale Beschreibung und Ihre [!DNL Blob] Anmeldeinformationen für die Verbindung ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis das neue Konto eingerichtet ist.

![connect](../../../../images/tutorials/create/blob/new.png)

### Existing account

To connect an existing account, select the [!DNL Blob] account you want to connect with, then select **[!UICONTROL Next]** to proceed.

![existing](../../../../images/tutorials/create/blob/existing.png)

## Nächste Schritte und zusätzliche Ressourcen

By following this tutorial, you have established a connection to your [!DNL Blob] account. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in Platform](../../dataflow/batch/cloud-storage.md)zu übertragen.