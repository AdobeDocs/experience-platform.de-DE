---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Create an Amazon Kinesis source connector in the UI
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 17%

---


# Create an [!DNL Amazon Kinesis] source connector in the UI

>[!NOTE]
>The [!DNL Amazon Kinesis] connector is in beta. See the [Sources overview](../../../../home.md#terms-and-conditions) for more information on using beta-labelled connectors.

Source connectors in Adobe Experience Platform provide the ability to ingest externally sourced data on a scheduled basis. Dieses Lernprogramm enthält Schritte zum Authentifizieren eines [!DNL Amazon Kinesis] (im Folgenden &quot; [!DNL "Kinesis"]) Quell-Connectors über die [!DNL Platform] Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Experience-Datenmodell (XDM)-System](../../../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [Echtzeit-Kundenprofil](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein [!DNL Kinesis] Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/streaming/cloud-storage.md)fortfahren.

### Erforderliche Anmeldedaten sammeln

Um den [!DNL Kinesis] Quellanschluss zu authentifizieren, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `accessKeyId` | Die Zugriffsschlüssel-ID für Ihr [!DNL Kinesis] Konto. |
| `Secret access key` | Der geheime Zugriffsschlüssel für Ihr [!DNL Kinesis] Konto. |
| `region` | Der Bereich Ihres AWS-Servers. |

Weitere Informationen zu diesen Werten finden Sie in [diesem Kinesis-Dokument](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Verbinden Sie Ihr [!DNL Kinesis] Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr [!DNL Kinesis] Konto mit [!DNL Platform]zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den *Quellarbeitsbereich* zuzugreifen. Auf der Registerkarte &quot; *Katalog* &quot;werden verschiedene Quellen angezeigt, mit denen eine Verbindung hergestellt werden kann [!DNL Platform]. Jede Quelle zeigt die Anzahl der vorhandenen Konten, die ihnen zugeordnet sind.

Wählen Sie unter der Kategorie *[!UICONTROL Cloud-Datenspeicherung]* die Option **[!UICONTROL Amazon Kinesis]** , gefolgt von **[!UICONTROL Hinzufügen Daten]** , um einen neuen [!DNL Kinesis] Connector zu erstellen.

![](../../../../images/tutorials/create/kinesis/catalog.png)

Das Dialogfeld &quot; *[!UICONTROL Verbindung mit Amazon Kinesis]* herstellen&quot;wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

If you are using new credentials, select **[!UICONTROL New Account]**. Geben Sie im eingeblendeten Eingabefeld einen Namen, eine optionale Beschreibung und Ihre [!DNL Kinesis] Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![](../../../../images/tutorials/create/kinesis/new.png)

### Existing account

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Kinesis] Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** , um fortzufahren.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Nächste Schritte

By following this tutorial, you have connected to your [!DNL Kinesis] account to [!DNL Platform]. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in Platform](../../dataflow/streaming/cloud-storage.md)zu übertragen.