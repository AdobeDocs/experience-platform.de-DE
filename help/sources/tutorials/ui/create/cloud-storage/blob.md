---
title: Erstellen einer Azure Blob Source-Verbindung über die Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Experience Platform-Benutzeroberfläche einen Azure Blob-Quell-Connector erstellen.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 25%

---

# Erstellen einer [!DNL Azure Blob]-Quellverbindung über die Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen einer [!DNL Azure Blob]-Quellverbindung (im Folgenden als &quot;[!DNL Blob]&quot; bezeichnet) über die Benutzeroberfläche von Experience Platform beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework für die Organisation von Kundenerlebnisdaten in Experience Platform.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Blob]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/batch/cloud-storage.md) fortfahren.

### Unterstützte Dateiformate

Experience Platform unterstützt die folgenden Dateiformate, die aus externen Speichern aufgenommen werden können:

* Durch Trennzeichen getrennte Werte (DSV): Sie können jedes einzelne Spaltentrennzeichen wie Tabulator, Komma, senkrechte Striche, Semikolon oder Hash verwenden, um einfache Dateien in jedem Format zu erfassen.
* JavaScript Object Notation (JSON): JSON-formatierte Datendateien müssen XDM-kompatibel sein.
* Apache Parquet: Dateien im Parquet-Format müssen XDM-kompatibel sein.

### Sammeln erforderlicher Anmeldedaten

Um auf Ihren [!DNL Blob] auf Experience Platform zugreifen zu können, müssen Sie gültige Werte für die folgenden Anmeldeinformationen angeben:

>[!BEGINTABS]

>[!TAB Authentifizierung für Verbindungszeichenfolge]

| Anmeldedaten | Beschreibung |
| --- | --- |
| Verbindungszeichenfolge | Eine Zeichenfolge, die die Autorisierungsinformationen enthält, die zum Authentifizieren von [!DNL Blob] bei Experience Platform erforderlich sind. Das [!DNL Blob]-Verbindungszeichenfolgenmuster ist: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Weitere Informationen zu Verbindungszeichenfolgen finden Sie in diesem [!DNL Blob] Dokument unter [Konfigurieren von Verbindungszeichenfolgen](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |

>[!TAB SAS-URI-Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| SAS-URI | Der URI für die Signatur mit freigegebenem Zugriff, den Sie als alternativen Authentifizierungstyp zum Verbinden Ihres [!DNL Blob]-Kontos verwenden können. Das [!DNL Blob] SAS-URI-Muster lautet: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Weitere Informationen finden Sie in diesem [!DNL Blob] Dokument zu [Shared Access Signature URIs](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| Container | Der Name des Containers, auf den Sie Zugriff gewähren möchten. Beim Erstellen eines neuen Kontos mit der [!DNL Blob] können Sie einen Container-Namen angeben, um den Benutzerzugriff auf den Unterordner Ihrer Wahl anzugeben. |
| Ordnerpfad | Der Pfad zum Ordner, auf den Sie Zugriff gewähren möchten. |

>[!ENDTABS]

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihren [!DNL Blob] mit Experience Platform zu verbinden

## Verbinden Ihres [!DNL Blob]-Kontos

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud] die Option **[!UICONTROL Azure Blob Storage]** und dann **[!UICONTROL Daten hinzufügen]**.

![Der Experience Platform-Quellkatalog mit der ausgewählten Azure Blob Storage-Quelle.](../../../../images/tutorials/create/blob/catalog.png)

Die **[!UICONTROL Mit Azure Blob Storage verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Blob]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/blob/existing.png)

### Neues Konto

>[!TIP]
>
>Nach der Erstellung können Sie den Authentifizierungstyp einer [!DNL Blob] Basisverbindung nicht mehr ändern. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihr neues [!DNL Blob]-Konto an.

![Der Bildschirm „Neues Konto“ für die Azure Blob Storage-Quelle.](../../../../images/tutorials/create/blob/new.png)

Die [!DNL Blob]-Quelle unterstützt sowohl die Authentifizierung mit dem Kontoschlüssel als auch die SAS-Authentifizierung (Shared Access Signature). Eine Authentifizierung über einen Kontoschlüssel erfordert eine Verbindungszeichenfolge zur Überprüfung, während eine SAS-Authentifizierung einen URI verwendet, der eine sichere delegierte Autorisierung Ihres Kontos ermöglicht.

In diesem Schritt können Sie auch die Unterordner festlegen, auf die Ihr Konto Zugriff haben soll, indem Sie den Namen des Containers und den Pfad zum Unterordner definieren.

>[!BEGINTABS]

>[!TAB Verbindungszeichenfolge]

Um sich mit einem Kontoschlüssel zu authentifizieren, wählen Sie **[!UICONTROL Kontoschlüsselauthentifizierung]** und geben Sie Ihre Verbindungszeichenfolge an. In diesem Schritt können Sie auch den Namen des Containers und den Pfad zum Unterordner festlegen, auf den Sie Zugriff haben möchten. Wenn Sie fertig sind, wählen **[!UICONTROL Mit Quelle verbinden]**.

![Verbindungszeichenfolge](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB SAS-URI]

Sie können SAS verwenden, um Authentifizierungsdaten mit unterschiedlichem Zugriffsgrad zu erstellen, da Sie bei einer SAS-basierten Authentifizierung Berechtigungen, Start- und Ablaufdaten sowie Bestimmungen zu bestimmten Ressourcen festlegen können.

Um sich mit einer freigegebenen Zugriffssignatur zu authentifizieren, wählen Sie **[!UICONTROL Authentifizierung mit freigegebener Zugriffssignatur]** und geben Sie dann Ihren SAS-URI an. In diesem Schritt können Sie auch den Namen des Containers und den Pfad zum Unterordner festlegen, auf den Sie Zugriff haben möchten. Wenn Sie fertig sind, wählen **[!UICONTROL Mit Quelle verbinden]**.

![SAS-URI](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Blob]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in Experience Platform zu übertragen](../../dataflow/batch/cloud-storage.md).
