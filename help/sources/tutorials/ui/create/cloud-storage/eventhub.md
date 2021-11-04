---
keywords: Experience Platform; Startseite; beliebte Themen; Azure Event-Hub; Event-Hub; azer-Event-Hubs
solution: Experience Platform
title: Erstellen einer Azure Event Hub-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung für Azure Event Hub erstellen.
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: 855b6414981c6d7ee79bc674e5a4087dd79dde5b
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 11%

---


# Erstellen Sie eine [!DNL Azure Event Hubs] Quellverbindung in der Benutzeroberfläche

Quell-Connectoren in Adobe Experience Platform bieten die Möglichkeit, extern bezogene Daten auf geplanter Basis zu erfassen. In diesem Tutorial werden Schritte zum Authentifizieren eines [!DNL Azure Event Hubs] (nachstehend &quot;genannt)[!DNL Event Hubs]&quot;) Quell-Connector mit dem [!DNL Platform] -Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Der standardisierte Rahmen, durch den [!DNL Experience Platform] organisiert Kundenerlebnisdaten.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Tutorial zum Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Event Hubs] Verbindung nutzen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Datenfluss konfigurieren](../../dataflow/streaming/cloud-storage-streaming.md).

### Erforderliche Anmeldedaten sammeln

Um Ihre [!DNL Event Hubs] Quell-Connector müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `sasKeyName` | Der Name der Autorisierungsregel, der auch als SAS-Schlüsselname bezeichnet wird. |
| `sasKey` | Der Primärschlüssel der [!DNL Event Hubs] Namespace. Die `sasPolicy` dass `sasKey` muss `manage` -Berechtigungen, die für die [!DNL Event Hubs] Liste auszufüllen. |
| `namespace` | Der Namespace des [!DNL Event Hubs] auf. |

Weitere Informationen zu diesen Werten finden Sie unter [this [!DNL Event Hubs] Dokument](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Verbinden Sie Ihre [!DNL Event Hubs] account

Nachdem Sie die erforderlichen Anmeldedaten erfasst haben, können Sie die folgenden Schritte ausführen, um Ihre [!DNL Event Hubs] Konto [!DNL Platform].

Anmelden bei [Adobe Experience Platform](https://platform.adobe.com) und wählen Sie **[!UICONTROL Quellen]** über die linke Navigationsleiste, um auf die **[!UICONTROL Quellen]** Arbeitsbereich. Die **[!UICONTROL Katalog]** enthält eine Vielzahl von Quellen, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem **[!UICONTROL Cloud-Speicher]** category, select **[!UICONTROL Azure Event Hubs]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Daten hinzufügen]** , um einen neuen Ereignis-Hubs-Connector zu erstellen.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Die **[!UICONTROL Verbindung zu Azure Event Hubs herstellen]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im angezeigten Formular einen Namen, eine optionale Beschreibung und Ihre [!DNL Event Hubs] Anmeldedaten. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und dann etwas Zeit für die Einrichtung der neuen Verbindung.

![](../../../../images/tutorials/create/eventhub/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie die [!DNL Event Hubs] Konto, mit dem Sie eine Verbindung herstellen möchten, wählen Sie **[!UICONTROL Nächste]** um fortzufahren.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Nächste Schritte

In diesem Tutorial haben Sie Ihre [!DNL Event Hubs] Konto [!DNL Platform]. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
