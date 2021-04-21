---
keywords: Experience Platform;Home;beliebte Themen;Azurblauer Ereignis Hubs;Ereignis Hubs;Azurblauer Ereignis Hubs
solution: Experience Platform
title: Erstellen einer Azurblauen Ereignis-Hubs-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie eine Azurblase-Ereignis-Hubs-Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche erstellen.
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 9%

---

# Erstellen einer [!DNL Azure Event Hubs]-Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
> Der [!DNL Azure Event Hubs]-Anschluss befindet sich in der Betaversion. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../../../home.md#terms-and-conditions).

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Authentifizieren eines [!DNL Azure Event Hubs]-Quellconnectors (nachstehend &quot;a1/>&quot;genannt) mithilfe der [!DNL Platform]-Benutzeroberfläche beschrieben.[!DNL Event Hubs]

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Event Hubs]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial [Konfigurieren eines Datenniedrig](../../dataflow/streaming/cloud-storage-streaming.md) fortfahren.

### Erforderliche Anmeldedaten sammeln

Um den [!DNL Event Hubs]-Quellanschluss zu authentifizieren, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `sasKeyName` | Der Name der Autorisierungsregel, der auch als SAS-Schlüsselname bezeichnet wird. |
| `sasKey` | Die generierte Unterschrift für den gemeinsamen Zugriff. |
| `namespace` | Der Namensraum der [!DNL Event Hubs], auf die Sie zugreifen. |

Weitere Informationen zu diesen Werten finden Sie unter [this [!DNL Event Hubs] Dokument](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Verbinden Sie Ihr [!DNL Event Hubs]-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr [!DNL Event Hubs]-Konto mit [!DNL Platform] zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Auf der Registerkarte **[!UICONTROL Katalog]** werden eine Reihe von Quellen angezeigt, mit denen Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Cloud-Datenspeicherung]** die Option **[!UICONTROL Blaue Ereignis-Hubs]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Hinzufügen Daten]** aus, um einen neuen Ereignis-Hubs-Connector zu erstellen.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Das Dialogfeld **[!UICONTROL Verbindung zu den Azurblauen Ereignis-Hubs]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im eingeblendeten Eingabeformular einen Namen, eine optionale Beschreibung und Ihre [!DNL Event Hubs]-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![](../../../../images/tutorials/create/eventhub/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Event Hubs]-Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Nächste Schritte

Durch Befolgen dieses Lernprogramms haben Sie Ihr [!DNL Event Hubs]-Konto mit [!DNL Platform] verbunden. Sie können nun mit dem nächsten Lernprogramm fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md) zu übertragen.
