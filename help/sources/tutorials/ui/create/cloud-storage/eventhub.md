---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Azurblauen Ereignis-Hubs-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 16%

---


# Create an [!DNL Azure Event Hubs] source connector in the UI

>[!NOTE]
> Der [!DNL Azure Event Hubs] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Authentifizieren eines [!DNL Azure Event Hubs] (im Folgenden &quot;[!DNL Event Hubs]&quot;) Quell-Connectors mithilfe der [!DNL Platform] Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Experience-Datenmodell (XDM)-System](../../../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [Echtzeit-Kundenprofil](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein [!DNL Event Hubs] Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/streaming/cloud-storage.md)fortfahren.

### Erforderliche Anmeldedaten sammeln

Um den [!DNL Event Hubs] Quellanschluss zu authentifizieren, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `sasKeyName` | Der Name der Autorisierungsregel, der auch als SAS-Schlüsselname bezeichnet wird. |
| `sasKey` | Die generierte Unterschrift für den gemeinsamen Zugriff. |
| `namespace` | Der Namensraum des [!DNL Event Hubs] Benutzers, auf den Sie zugreifen. |

Weitere Informationen zu diesen Werten finden Sie in [diesem Ereignis-Hubs-Dokument](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Verbinden Sie Ihr [!DNL Event Hubs] Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr [!DNL Event Hubs] Konto mit [!DNL Platform]zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den *Quellarbeitsbereich* zuzugreifen. Auf der Registerkarte &quot; *[!UICONTROL Katalog]* &quot;werden verschiedene Quellen angezeigt, mit denen eine Verbindung hergestellt werden kann [!DNL Platform]. Jede Quelle zeigt die Anzahl der vorhandenen Konten, die ihnen zugeordnet sind.

Wählen Sie unter der Kategorie *[!UICONTROL Cloud-Datenspeicherung]* die Option **[!UICONTROL Azurblaue Ereignis-Hubs]** , gefolgt von **[!UICONTROL Hinzufügen Daten]** , um einen neuen Ereignis-Hubs-Connector zu erstellen.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Der Dialog *[!UICONTROL Verbindung zu Azurblauer Ereignis Hubs]* wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im angezeigten Eingabedatum einen Namen, eine optionale Beschreibung und Ihre Ereignis-Hubs-Anmeldeinformationen ein. When finished, select **[!UICONTROL Connect]** and then allow some time for the new connection to establish.

![](../../../../images/tutorials/create/eventhub/new.png)

### Vorhandenes Konto

Um ein bestehendes Konto zu verknüpfen, wählen Sie das Ereignis-Hubs-Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** , um fortzufahren.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Nächste Schritte

Indem Sie diesem Tutorial folgen, haben Sie Ihr Ereignis-Hubs-Konto mit [!DNL Platform]verbunden. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in Platform](../../dataflow/streaming/cloud-storage.md)zu übertragen.