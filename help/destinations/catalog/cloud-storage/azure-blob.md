---
keywords: Azure Blob; Blob-Ziel; s3; Azure Blob-Ziel
title: Azure Blob-Verbindung
description: Erstellen Sie eine ausgehende Live-Verbindung zu Ihrem Azure Blob-Speicher, um regelmäßig CSV-Datendateien aus Adobe Experience Platform zu exportieren.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 14%

---

# [!DNL Azure Blob] connection

## Übersicht {#overview}

[!DNL Azure Blob] (nachstehend: [!DNL Blob]) ist die Objektspeicherlösung von Microsoft für die Cloud. In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Blob] Ziel, das [!DNL Platform] -Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Tutorial zum Schema Editor](../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
* [[!DNL Real-time Customer Profile]](../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Blob] Ziel, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Aktivieren von Segmenten für Ihr Ziel](../../ui/activate-batch-profile-destinations.md).

## Unterstützte Dateiformate {#file-formats}

[!DNL Experience Platform] unterstützt das folgende Dateiformat, in das exportiert werden soll [!DNL Blob]:

* Trennzeichen (DSV): Die Unterstützung für DSV-formatierte Datendateien ist derzeit auf kommagetrennte Werte beschränkt. Unterstützung für allgemeine DSV-Dateien wird in Zukunft bereitgestellt.

## Mit Ziel verbinden {#connect}

Gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md).

### Verbindungsparameter {#parameters}

while [Einrichten](../../ui/connect-destination.md) An diesem Ziel müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Verbindungszeichenfolge]**: Die Verbindungszeichenfolge ist erforderlich, um auf Daten in Ihrem Blob-Speicher zuzugreifen. Die [!DNL Blob] Verbindungszeichenfolgenmuster beginnt mit: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Weitere Informationen zur Konfiguration der [!DNL Blob] Verbindungszeichenfolge, siehe [Verbindungszeichenfolge für ein Azure-Speicherkonto konfigurieren](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) in der Microsoft-Dokumentation.

* Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien Verschlüsselung hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierter String.
* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung dieses Ziels ein.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, der die exportierten Dateien hosten soll.
* **[!UICONTROL Container]**: den Namen der [!DNL Azure Blob Storage] Container, der von diesem Ziel verwendet werden soll.

Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien Verschlüsselung hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierter String.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Siehe [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.
