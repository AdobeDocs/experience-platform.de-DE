---
keywords: Experience Platform;Home;beliebte Themen;Azurblübe;Azurblübe;Azurblauch-Stecker
solution: Experience Platform
title: Erstellen einer Azurblauch-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie einen Azurblauch-Quellanschluss mithilfe der Plattform-Benutzeroberfläche erstellen.
exl-id: 0e54569b-7305-4065-981e-951623717648
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 7%

---

# Erstellen einer [!DNL Azure Blob]-Quellverbindung in der Benutzeroberfläche

In diesem Lernprogramm werden Schritte zum Erstellen eines [!DNL Azure Blob] (nachfolgend als &quot;[!DNL Blob]&quot;bezeichnet) mithilfe der Plattform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Blob]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial [Konfigurieren eines Datenniedrig](../../dataflow/batch/cloud-storage.md) fortfahren.

### Unterstützte Dateiformate

[!DNL Experience Platform] unterstützt die folgenden Dateiformate, die von externen Datenspeicherung erfasst werden:

- Trennzeichen-getrennte Werte (DSV): Die Unterstützung für DSV-formatierte Datendateien ist derzeit auf kommagetrennte Werte beschränkt. Der Wert von Feldkopfzeilen in DSV-formatierten Dateien darf nur aus alphanumerischen Zeichen und Unterstrichen bestehen. Die Unterstützung für allgemeine DSV-Dateien wird in Zukunft bereitgestellt.
- JavaScript Object Notation (JSON): JSON-formatierte Datendateien müssen XDM-kompatibel sein.
- Apache Parquet: Parquet-formatierte Datendateien müssen XDM-konform sein.

### Erforderliche Anmeldedaten sammeln

Um auf Ihre [!DNL Blob]-Datenspeicherung auf Plattform zugreifen zu können, müssen Sie einen gültigen Wert für die folgende Berechtigung angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Eine Zeichenfolge, die die Autorisierungsinformationen enthält, die zum Authentifizieren von [!DNL Blob] für die Experience Platform erforderlich sind. Das Verbindungszeichenfolgen-Muster [!DNL Blob] lautet: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Weitere Informationen zu Verbindungszeichenfolgen finden Sie in diesem [!DNL Blob]-Dokument unter [Konfigurieren von Verbindungszeichenfolgen](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | Der URI für die Unterschrift für den gemeinsamen Zugriff, den Sie als alternativen Authentifizierungstyp verwenden können, um Ihr [!DNL Blob]-Konto zu verbinden. Das SAS-URI-Muster ist: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Weitere Informationen finden Sie in diesem [!DNL Blob] Dokument unter [URIs für freigegebene Zugriffssignaturen](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication).[!DNL Blob] |

## Verbinden Sie Ihr [!DNL Blob]-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr [!DNL Blob]-Konto mit der Plattform zu verknüpfen.

Wählen Sie in der [Plattform-Benutzeroberfläche](https://platform.adobe.com) **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Reihe von Quellen an, für die Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle über die Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud-Datenspeicherung] die Option **[!UICONTROL Azurblase-Datenspeicherung]** und wählen Sie **[!UICONTROL Hinzufügen Daten]**.

![Katalog](../../../../images/tutorials/create/blob/catalog.png)

Die Seite **[!UICONTROL Verbindung mit der Azurblauch-Datenspeicherung]** herstellen wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Blob]-Konto, mit dem Sie einen neuen Datenflug erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![existing](../../../../images/tutorials/create/blob/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine Optionsbeschreibung für Ihr neues [!DNL Blob]-Konto ein.

**Authentifizieren mit einer Verbindungszeichenfolge**

Der [!DNL Blob]-Connector bietet verschiedene Authentifizierungstypen für den Zugriff. Wählen Sie unter [!UICONTROL Kontoauthentifizierung] **[!UICONTROL ConnectionString]** aus, um die auf einer Verbindungszeichenfolge basierenden Anmeldeinformationen zu verwenden.

![connection string](../../../../images/tutorials/create/blob/connectionstring.png)

**Authentifizieren Sie sich mit einem URI für eine freigegebene Zugriffssignatur**

Eine SAS-URI (shared access signature) ermöglicht eine sichere delegierte Autorisierung für Ihr [!DNL Blob]-Konto. Sie können SAS verwenden, um Authentifizierungsberechtigungen mit unterschiedlichem Zugriffsgrad zu erstellen, da eine SAS-basierte Authentifizierung Ihnen das Festlegen von Berechtigungen, Beginns- und Ablaufdaten sowie von Bestimmungen für bestimmte Ressourcen ermöglicht.

Wählen Sie **[!UICONTROL SasURIAuthentication]** und geben Sie dann Ihren [!DNL Blob] SAS-URI ein. Wählen Sie **[!UICONTROL Mit Quelle verbinden]** verbinden, um fortzufahren.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Blob]-Konto hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in Platform](../../dataflow/batch/cloud-storage.md) zu übertragen.
