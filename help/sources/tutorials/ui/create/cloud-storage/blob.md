---
keywords: Experience Platform; Startseite; beliebte Themen; Azure Blob; Azure Blob; Azure Blob-Connector
solution: Experience Platform
title: Erstellen einer Azure Blob Source-Verbindung in der Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Benutzeroberfläche von Platform einen Azure Blob-Quell-Connector erstellen.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 39%

---

# Erstellen Sie eine [!DNL Azure Blob] Quellverbindung in der Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Azure Blob] (nachstehend &quot;genannt)[!DNL Blob]&quot;) über die Benutzeroberfläche von Platform.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   - [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Blob]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/batch/cloud-storage.md) fortfahren.

### Unterstützte Dateiformate

[!DNL Experience Platform] unterstützt die folgenden Dateiformate, die aus externen Speichern erfasst werden:

- Trennzeichen (DSV): Die Unterstützung für DSV-formatierte Datendateien ist derzeit auf kommagetrennte Werte beschränkt. Der Wert der Feldkopfzeilen in DSV-formatierten Dateien darf nur aus alphanumerischen Zeichen und Unterstrichen bestehen. Unterstützung für allgemeine DSV-Dateien wird in Zukunft bereitgestellt.
- JavaScript Object Notation (JSON): JSON-formatierte Datendateien müssen XDM-konform sein.
- Apache Parquet: Parquet formatierte Datendateien müssen XDM-konform sein.

### Sammeln erforderlicher Anmeldeinformationen

Um auf Ihre [!DNL Blob] -Speicher in Platform bereitstellen, müssen Sie einen gültigen Wert für die folgenden Anmeldedaten angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Eine Zeichenfolge, die die für die Authentifizierung erforderlichen Autorisierungsinformationen enthält [!DNL Blob] in die Experience Platform. Die [!DNL Blob] Verbindungszeichenfolgenmuster ist: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Weitere Informationen zu Verbindungszeichenfolgen finden Sie in diesem [!DNL Blob] Dokument auf [Konfigurieren von Verbindungszeichenfolgen](https://docs.microsoft.com/de-de/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | Der URI für die gemeinsame Zugriffssignatur, den Sie als alternativen Authentifizierungstyp verwenden können, um Ihre [!DNL Blob] -Konto. Die [!DNL Blob] Das SAS-URI-Muster lautet: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Weitere Informationen finden Sie in diesem [!DNL Blob] Dokument auf [URIs für freigegebene Zugriffssignatur](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## Verbinden Ihres [!DNL Blob]-Kontos

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Blob]-Konto mit Platform zu verknüpfen.

Wählen Sie in der [Platform-Benutzeroberfläche](https://platform.adobe.com) in der linken Navigationsleiste **[!UICONTROL Quellen]** aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Unter dem [!UICONTROL Cloud-Speicher] category, select **[!UICONTROL Azure Blob Storage]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/blob/catalog.png)

Die **[!UICONTROL Verbinden mit Azure Blob Storage]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Blob]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/blob/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine Optionsbeschreibung für Ihre neue [!DNL Blob] -Konto.

**Authentifizierung mit einer Verbindungszeichenfolge**

Die [!DNL Blob] -Connector bietet verschiedene Authentifizierungstypen für den Zugriff. under [!UICONTROL Kontoauthentifizierung] select **[!UICONTROL ConnectionString]** , um auf Verbindungszeichenfolgen basierende Anmeldeinformationen zu verwenden.

![Verbindungszeichenfolge](../../../../images/tutorials/create/blob/connectionstring.png)

**Authentifizierung mit einem URI für die gemeinsame Zugriffssignatur**

Eine SAS-URI (Shared Access Signature) ermöglicht die sichere delegierte Autorisierung Ihrer [!DNL Blob] -Konto. Sie können SAS verwenden, um Authentifizierungsberechtigungen mit unterschiedlichem Zugriffsgrad zu erstellen, da eine SAS-basierte Authentifizierung es Ihnen ermöglicht, Berechtigungen, Start- und Ablaufdaten sowie Bestimmungen für bestimmte Ressourcen festzulegen.

Auswählen **[!UICONTROL SasURIAuthentication]** und geben Sie dann [!DNL Blob] SAS-URI. Auswählen **[!UICONTROL Verbindung mit Quelle herstellen]** um fortzufahren.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Blob]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in Platform zu übertragen](../../dataflow/batch/cloud-storage.md).
