---
keywords: Azure Blob; Blob-Ziel; s3; Azure Blob-Ziel
title: Azure Blob-Verbindung
description: Erstellen Sie eine ausgehende Live-Verbindung zu Ihrem Azure Blob-Speicher, um in regelmäßigen Abständen tabulatorgetrennte oder CSV-Datendateien aus Adobe Experience Platform zu exportieren.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 14%

---

# [!DNL Azure Blob] connection

## Übersicht {#overview}

[!DNL Azure Blob] (nachfolgend als  [!DNL Blob] bezeichnet) ist die Objektspeicherlösung von Microsoft für die Cloud. In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Blob]-Ziels mithilfe der [!DNL Platform]-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Tutorial](../../../xdm/tutorials/create-schema-ui.md) zum Schema Editor: Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
* [[!DNL Real-time Customer Profile]](../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein gültiges [!DNL Blob]-Ziel verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Aktivieren von Segmenten für Ihr Ziel](../../ui/activate-batch-profile-destinations.md) fortfahren.[

## Unterstützte Dateiformate {#file-formats}

[!DNL Experience Platform] unterstützt das folgende Dateiformat für den Export in  [!DNL Blob]:

* Trennzeichen (DSV): Die Unterstützung für DSV-formatierte Datendateien ist derzeit auf kommagetrennte Werte beschränkt. Unterstützung für allgemeine DSV-Dateien wird in Zukunft bereitgestellt.

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Verbindungszeichenfolge]**: Die Verbindungszeichenfolge ist erforderlich, um auf Daten in Ihrem Blob-Speicher zuzugreifen. Das Verbindungszeichenfolgen-Muster [!DNL Blob] beginnt mit: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Weitere Informationen zum Konfigurieren der Verbindungszeichenfolge [!DNL Blob] finden Sie unter [Konfigurieren einer Verbindungszeichenfolge für ein Azure-Speicherkonto](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) in der Microsoft-Dokumentation.

* Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien Verschlüsselung hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierte Zeichenfolge geschrieben werden.
* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung dieses Ziels ein.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, der die exportierten Dateien hosten soll.
* **[!UICONTROL Container]**: Geben Sie den Namen des  [!DNL Azure Blob Storage] Containers ein, der von diesem Ziel verwendet werden soll.

Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien Verschlüsselung hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierte Zeichenfolge geschrieben werden.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profilexportziele](../../ui/activate-batch-profile-destinations.md) .
