---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Apache HDFS-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 12%

---


# Create an [!DNL Apache] HDFS source connector in the UI

>[!NOTE]
>Der [!DNL Apache] HDFS-Anschluss befindet sich in der Betaphase. See the [Sources overview](../../../../home.md#terms-and-conditions) for more information on using beta-labelled connectors.

Source connectors in [!DNL Adobe Experience Platform] provide the ability to ingest externally sourced data on a scheduled basis. In diesem Lernprogramm werden Schritte zum Authentifizieren eines [!DNL Apache Hadoop Distributed File System] (im Folgenden &quot;HDFS&quot;) Quellconnectors über die [!DNL Platform] Benutzeroberfläche beschrieben.

## Erste Schritte

This tutorial requires a working understanding of the following components of [!DNL Platform]:

- [Experience-Datenmodell (XDM)-System](../../../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema Editor tutorial](../../../../../xdm/tutorials/create-schema-ui.md): Learn how to create custom schemas using the Schema Editor UI.
- [Echtzeit-Kundenprofil](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine HDFS-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/batch/cloud-storage.md)fortfahren.

### Erforderliche Anmeldedaten sammeln

In order to authenticate your HDFS source connector, you must provide values for the following connection property:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `url` | Die URL definiert Authentifizierungsparameter, die für eine anonyme Verbindung mit HDFS erforderlich sind. Weitere Informationen zum Abrufen dieses Wertes finden Sie im folgenden Dokument zur [HTTPS-Authentifizierung für HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Connect your HDFS account

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues HDFS-Konto zu erstellen, mit dem eine Verbindung hergestellt werden soll [!DNL Platform].

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den *[!UICONTROL Quellarbeitsbereich]* zuzugreifen. Im Anzeigebereich &quot; *[!UICONTROL Katalog]* &quot;werden verschiedene Quellen angezeigt, mit denen Sie ein eingehendes Konto erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse an, die mit ihnen verbunden sind.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternatively, you can find the specific source you wish to work with using the search option.

Wählen Sie unter der Kategorie *[!UICONTROL Cloud-Datenspeicherung]* die Option **[!UICONTROL Apache HDFS]** gefolgt von **[!UICONTROL Hinzufügen Daten]** , um einen neuen HDFS-Anschluss zu erstellen.

![Katalog](../../../../images/tutorials/create/hdfs/catalog.png)

Die Seite *[!UICONTROL Verbindung zu HDFS]* herstellen wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im eingeblendeten Eingabebild einen Namen, eine optionale Beschreibung und Ihre Anmeldeinformationen für die Datenspeicherung ein. Wenn Sie fertig sind, wählen Sie &quot;Mit Quelle **[!UICONTROL verbinden&quot;]** und lassen Sie dann etwas Zeit für die Einrichtung des neuen Kontos zu.

![connect](../../../../images/tutorials/create/hdfs/new.png)

### Vorhandenes Konto

To connect an existing account, select the HDFS account you want to connect with, then select **[!UICONTROL Next]** to proceed.

![existing](../../../../images/tutorials/create/hdfs/existing.png)

## Nächste Schritte

By following this tutorial, you have established a connection to your HDFS account. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in Platform](../../dataflow/batch/cloud-storage.md)zu übertragen.