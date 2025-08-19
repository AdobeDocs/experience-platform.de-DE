---
title: Verbinden von Azure Blob Storage mit Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie Ihr Azure Blob Storage-Konto mithilfe des Quellarbeitsbereichs in der Benutzeroberfläche mit Experience Platform verbinden.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 7acdc090c020de31ee1a010d71a2969ec9e5bbe1
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 18%

---

# Verbinden von [!DNL Azure Blob Storage] mit Experience Platform über die Benutzeroberfläche

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihre [!DNL Azure Blob Storage]-Instanz mithilfe des Arbeitsbereichs „Quellen“ in der Benutzeroberfläche von Experience Platform mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework für die Organisation von Kundenerlebnisdaten in Experience Platform.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Azure Blob Storage]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/batch/cloud-storage.md) fortfahren.

### Unterstützte Dateiformate

Experience Platform unterstützt die folgenden Dateiformate, die aus externen Speichern aufgenommen werden können:

* Durch Trennzeichen getrennte Werte (DSV): Sie können jedes einzelne Spaltentrennzeichen wie Tabulator, Komma, senkrechte Striche, Semikolon oder Hash verwenden, um einfache Dateien in jedem Format zu erfassen.
* JavaScript Object Notation (JSON): JSON-formatierte Datendateien müssen XDM-kompatibel sein.
* Apache Parquet: Dateien im Parquet-Format müssen XDM-kompatibel sein.

### Sammeln erforderlicher Anmeldedaten

Informationen zur Authentifizierung [[!DNL Azure Blob Storage]  Sie in ](../../../../connectors/cloud-storage/blob.md#authentication)Übersicht“.

## Navigieren im Quellkatalog

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich *[!UICONTROL Quellen]* zuzugreifen. Wählen Sie eine Kategorie aus oder verwenden Sie die Suchleiste, um Ihre Quelle zu finden.

Um eine Verbindung zu [!DNL Azure Blob Storage] herzustellen, wechseln Sie zur Kategorie *[!UICONTROL Cloud-Speicher]*, wählen Sie die Quellkarte **[!UICONTROL Azure Blob Storage]** aus und klicken Sie dann auf **[!UICONTROL Einrichten]**.

>[!TIP]
>
>Quellen zeigen **[!UICONTROL Einrichten]** für neue Verbindungen und **[!UICONTROL Daten hinzufügen]** an, wenn bereits ein Konto vorhanden ist.

![Der Quellkatalog mit der ausgewählten Azure Blob Storage-Quelle.](../../../../images/tutorials/create/blob/catalog.png)

## Vorhandenes Konto verwenden

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das [!DNL Azure Blob Storage] Konto aus, das Sie verwenden möchten.

![Die vorhandene Quellschnittstelle für Azure Blob Storage.](../../../../images/tutorials/create/blob/existing.png)

## Neues Konto erstellen

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen an und fügen Sie optional eine Beschreibung für Ihr Konto hinzu. Sie können Ihr [!DNL Azure Blob Storage]-Konto mit Experience Platform verbinden, indem Sie die folgenden Authentifizierungstypen verwenden:

* **Kontoschlüsselauthentifizierung**: Verwendet den Zugriffsschlüssel des Speicherkontos zur Authentifizierung und Verbindung mit Ihrem [!DNL Azure Blob Storage].
* **Shared Access Signature (SAS)**: Verwendet einen SAS-URI, um delegierten, zeitlich begrenzten Zugriff auf Ressourcen in Ihrem [!DNL Azure Blob Storage]-Konto bereitzustellen.
* **Service-Prinzipal-basierte Authentifizierung**: Verwendet einen Azure Active Directory (AAD)-Service-Prinzipal (Client-ID und Geheimnis) zur sicheren Authentifizierung bei Ihrem Azure Blob Storage-Konto.

>[!BEGINTABS]

>[!TAB Authentifizierung mit Kontoschlüssel]

Wählen Sie **[!UICONTROL Authentifizierung mit Kontoschlüssel]** und geben Sie Ihre `connectionString`, `container` und `folderPath` an. Wählen Sie als Nächstes **[!UICONTROL Mit Quelle verbinden]** und warten Sie einen Augenblick, bis die Verbindung hergestellt ist.

![Die Option zur Authentifizierung des Kontoschlüssels im Schritt zur Erstellung eines neuen Kontos.](../../../../images/tutorials/create/blob/account-key.png)

>[!TAB Shared Access Signature]

Wählen Sie **[!UICONTROL Shared Access Signature]** aus und geben Sie Ihre `sasUri`, `container` und `folderPath` an. Wählen Sie als Nächstes **[!UICONTROL Mit Quelle verbinden]** und warten Sie einen Augenblick, bis die Verbindung hergestellt ist.

![Die Authentifizierungsoption für freigegebene Zugriffssignaturen im Schritt zur Erstellung eines neuen Kontos.](../../../../images/tutorials/create/blob/sas.png)

>[!TAB Auf Service-Prinzipalen basierende Authentifizierung]

Wählen Sie **[!UICONTROL Service-Prinzipal-basierte]** aus und geben Sie Ihre `serviceEndpoint`, `servicePrincipalId`, `servicePrincipalKey`, `accountKind`, `tenant`, `container` und `folderPath` an. Wählen Sie als Nächstes **[!UICONTROL Mit Quelle verbinden]** und warten Sie einen Augenblick, bis die Verbindung hergestellt ist.

![Die auf dem Service-Prinzipal basierende Authentifizierungsoption im Schritt zur Erstellung eines neuen Kontos.](../../../../images/tutorials/create/blob/service-principal.png)

>[!ENDTABS]

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Azure Blob Storage]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in Experience Platform zu übertragen](../../dataflow/batch/cloud-storage.md).
