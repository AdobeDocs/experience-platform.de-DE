---
keywords: Experience Platform; Startseite; beliebte Themen; Azure Blob; Azure Blob; Azure Blob-Connector
solution: Experience Platform
title: Erstellen einer Azure Blob Source-Verbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Benutzeroberfläche von Platform einen Azure Blob-Quell-Connector erstellen.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 9%

---

# Erstellen einer [!DNL Azure Blob]-Quellverbindung in der Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Azure Blob] (nachfolgend als &quot;[!DNL Blob]&quot;bezeichnet) mithilfe der Platform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) zum Schema Editor: Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Blob]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Konfigurieren eines Datenflusses [fortfahren.](../../dataflow/batch/cloud-storage.md)

### Unterstützte Dateiformate

[!DNL Experience Platform] unterstützt die folgenden Dateiformate, die aus externen Speichern erfasst werden:

- Trennzeichen (DSV): Die Unterstützung für DSV-formatierte Datendateien ist derzeit auf kommagetrennte Werte beschränkt. Der Wert der Feldkopfzeilen in DSV-formatierten Dateien darf nur aus alphanumerischen Zeichen und Unterstrichen bestehen. Unterstützung für allgemeine DSV-Dateien wird in Zukunft bereitgestellt.
- JavaScript Object Notation (JSON): JSON-formatierte Datendateien müssen XDM-konform sein.
- Apache Parquet: Parquet formatierte Datendateien müssen XDM-konform sein.

### Erforderliche Anmeldedaten sammeln

Um auf Ihren [!DNL Blob]-Speicher in Platform zugreifen zu können, müssen Sie einen gültigen Wert für die folgenden Anmeldedaten angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Eine Zeichenfolge, die die Autorisierungsinformationen enthält, die zum Authentifizieren von [!DNL Blob] für die Experience Platform erforderlich sind. Das Verbindungszeichenfolgenmuster [!DNL Blob] lautet: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Weitere Informationen zu Verbindungszeichenfolgen finden Sie in diesem [!DNL Blob] Dokument zu [Konfigurieren von Verbindungszeichenfolgen](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | Der URI für die gemeinsame Zugriffssignatur, den Sie als alternativen Authentifizierungstyp verwenden können, um Ihr [!DNL Blob]-Konto zu verbinden. Das SAS-URI-Muster [!DNL Blob] lautet: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Weitere Informationen finden Sie in diesem [!DNL Blob] Dokument unter [URIs für freigegebene Zugriffssignaturen](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## Ihr [!DNL Blob]-Konto verbinden

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Blob]-Konto mit Platform zu verknüpfen.

Wählen Sie in der [Platform UI](https://platform.adobe.com) **[!UICONTROL Quellen]** aus der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] enthält eine Vielzahl von Quellen, für die Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle über die Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud-Speicher] die Option **[!UICONTROL Azure Blob Storage]** und klicken Sie dann auf **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/blob/catalog.png)

Die Seite **[!UICONTROL Verbindung zu Azure Blob Storage]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Blob]-Konto aus, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhandene](../../../../images/tutorials/create/blob/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine Optionsbeschreibung für Ihr neues [!DNL Blob]-Konto ein.

**Authentifizierung mit einer Verbindungszeichenfolge**

Der Connector [!DNL Blob] bietet verschiedene Authentifizierungstypen für den Zugriff. Wählen Sie unter [!UICONTROL Kontoauthentifizierung] **[!UICONTROL ConnectionString]** aus, um auf Verbindungszeichenfolgen basierende Anmeldeinformationen zu verwenden.

![Verbindungszeichenfolge](../../../../images/tutorials/create/blob/connectionstring.png)

**Authentifizierung mit einem URI für die gemeinsame Zugriffssignatur**

Eine freigegebene Zugriffssignatur (SAS)-URI ermöglicht eine sichere delegierte Autorisierung für Ihr [!DNL Blob]-Konto. Sie können SAS verwenden, um Authentifizierungsberechtigungen mit unterschiedlichem Zugriffsgrad zu erstellen, da eine SAS-basierte Authentifizierung es Ihnen ermöglicht, Berechtigungen, Start- und Ablaufdaten sowie Bestimmungen für bestimmte Ressourcen festzulegen.

Wählen Sie **[!UICONTROL SasURIAuthentication]** und geben Sie dann Ihren [!DNL Blob] SAS-URI an. Wählen Sie **[!UICONTROL Mit Quelle verbinden]** aus, um fortzufahren.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Blob]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in Platform](../../dataflow/batch/cloud-storage.md) zu übertragen.
