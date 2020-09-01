---
keywords: Experience Platform;home;popular topics;Azure File Storage;Azure File Storage connector
solution: Experience Platform
title: Erstellen eines Azurblase-Datenspeicherung-Quellconnectors in der Benutzeroberfläche
topic: overview
description: In diesem Lernprogramm werden Schritte zum Authentifizieren eines Azurblauen File Datenspeicherung-Quellconnectors mithilfe der Plattform-Benutzeroberfläche beschrieben.
translation-type: tm+mt
source-git-commit: 0da686743e8bc57d310f7eff6f1bf812a8f31238
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 9%

---


# Create an [!DNL Azure File Storage] source connector in the UI

>[!NOTE]
>
>Der [!DNL Azure File Storage] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Authentifizieren eines [!DNL Azure File Storage] Quell-Connectors über die [!DNL Platform] Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model] (XDM) System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [[!DNL Echtzeit-Profil]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Azure File Storage] Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Lernprogramm zur [Konfiguration eines Datenflusses](../../dataflow/batch/cloud-storage.md)fortfahren.

### Erforderliche Anmeldedaten sammeln

Um den [!DNL Azure File Storage] Quellanschluss zu authentifizieren, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Der Endpunkt der [!DNL Azure File Storage] Instanz, auf die Sie zugreifen. |
| `userId` | Der Benutzer mit ausreichendem Zugriff auf den [!DNL Azure File Storage] Endpunkt. |
| `password` | Der [!DNL Azure File Storage] Zugriffsschlüssel. |

Weitere Informationen zum Einstieg finden Sie in [ [!DNL Azure File Storage] diesem Dokument](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

## Verbinden Sie Ihr [!DNL Azure File Storage] Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr [!DNL Azure File Storage] Konto mit [!DNL Platform]zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den **[!UICONTROL Quellarbeitsbereich]** zuzugreifen. Im Anzeigebereich &quot; **[!UICONTROL Katalog]** &quot;werden verschiedene Quellen angezeigt, mit denen Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie &quot; **[!UICONTROL Datenbanken]** &quot;die Option &quot; **[!UICONTROL Azurblase-Datenspeicherung]**&quot;aus. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie &quot; **[!UICONTROL Konfigurieren]**&quot;aus. Andernfalls wählen Sie **[!UICONTROL Hinzufügen Daten]** aus, um einen neuen [!DNL Azure File Storage] Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/azure-file-storage/catalog.png)

Die Seite &quot; **[!UICONTROL Verbindung mit der Datenspeicherung]** der leeren Datei herstellen&quot;wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im eingeblendeten Eingabefeld einen Namen, eine optionale Beschreibung und Ihre [!DNL Azure File Storage] Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![connect](../../../../images/tutorials/create/azure-file-storage/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Azure File Storage] Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** , um fortzufahren.

![existing](../../../../images/tutorials/create/azure-file-storage/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Azure File Storage] Konto hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in [!DNL Platform]](../../dataflow/batch/cloud-storage.md)zu importieren.