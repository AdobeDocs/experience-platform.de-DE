---
title: Erstellen einer Azure Blob Source-Verbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Benutzeroberfläche von Platform einen Azure Blob-Quell-Connector erstellen.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 27%

---

# Erstellen einer [!DNL Azure Blob]-Quellverbindung in der Benutzeroberfläche

In diesem Tutorial werden die Schritte zum Erstellen einer Quellverbindung mit dem Code [!DNL Azure Blob] (nachfolgend als &quot;[!DNL Blob]&quot;bezeichnet) mithilfe der Benutzeroberfläche von Platform beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework für die Organisation von Kundenerlebnisdaten in Experience Platform.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Blob]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/batch/cloud-storage.md) fortfahren.

### Unterstützte Dateiformate

Experience Platform unterstützt die folgenden Dateiformate, die aus externen Speichern erfasst werden:

* Durch Trennzeichen getrennte Werte (DSV): Sie können ein einzelnes Spaltentrennzeichen wie Tabulatoren, Kommas, senkrechte Striche, Semikolons oder Hash verwenden, um flache Dateien in jedem beliebigen Format zu erfassen.
* JavaScript Object Notation (JSON): JSON-formatierte Datendateien müssen XDM-kompatibel sein.
* Apache Parquet: Parquet formatierte Datendateien müssen XDM-kompatibel sein.

### Sammeln erforderlicher Anmeldeinformationen

Um auf Ihren [!DNL Blob]-Speicher auf dem Experience Platform zuzugreifen, müssen Sie gültige Werte für die folgenden Anmeldedaten angeben:

>[!BEGINTABS]

>[!TAB Authentifizierung der Verbindungszeichenfolge]

| Anmeldedaten | Beschreibung |
| --- | --- |
| Verbindungszeichenfolge | Eine Zeichenfolge, die die für die Authentifizierung von [!DNL Blob] bei Experience Platform erforderlichen Autorisierungsinformationen enthält. Das Muster der Verbindungszeichenfolge [!DNL Blob] lautet: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Weitere Informationen zu Verbindungszeichenfolgen finden Sie in diesem Dokument [!DNL Blob] unter [Konfigurieren von Verbindungszeichenfolgen](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string) . |

>[!TAB SAS-URI-Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| SAS-URI | Der URI für die gemeinsame Zugriffssignatur, den Sie als alternativen Authentifizierungstyp verwenden können, um Ihr [!DNL Blob]-Konto zu verbinden. Das Muster für den SAS-URI [!DNL Blob] lautet: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Weitere Informationen finden Sie in diesem Dokument für die URIs für freigegebenen Zugriff [ ](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication).[!DNL Blob] |
| Container | Der Name des Containers, für den Sie Zugriff festlegen möchten. Beim Erstellen eines neuen Kontos mit der Quelle [!DNL Blob] können Sie einen Container-Namen angeben, um den Benutzerzugriff auf den Unterordner Ihrer Wahl anzugeben. |
| Ordnerpfad | Der Pfad zu dem Ordner, auf den Sie Zugriff gewähren möchten. |

>[!ENDTABS]

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihren [!DNL Blob]-Speicher mit Experience Platform zu verbinden

## Verbinden Ihres [!DNL Blob]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud-Speicher] den Eintrag **[!UICONTROL Azure Blob Storage]** und klicken Sie dann auf **[!UICONTROL Daten hinzufügen]**.

![Der Experience Platform-Quellkatalog mit der ausgewählten Azure Blob Storage-Quelle.](../../../../images/tutorials/create/blob/catalog.png)

Die Seite **[!UICONTROL Verbindung zu Azure Blob Storage herstellen]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Blob]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/blob/existing.png)

### Neues Konto

>[!TIP]
>
>Nach der Erstellung können Sie den Authentifizierungstyp einer Basis-Verbindung vom Typ [!DNL Blob] nicht mehr ändern. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihr neues [!DNL Blob]-Konto ein.

![Der neue Kontobildschirm für die Azure Blob Storage-Quelle.](../../../../images/tutorials/create/blob/new.png)

Die Quelle [!DNL Blob] unterstützt sowohl die Authentifizierung des Kontoschlüssels als auch die Authentifizierung für die gemeinsame Zugriffssignatur (SAS). Eine schlüsselbasierte Kontoauthentifizierung erfordert eine Verbindungszeichenfolge zur Überprüfung, während eine SAS-Authentifizierung einen URI verwendet, der eine sichere delegierte Autorisierung Ihres Kontos ermöglicht.

In diesem Schritt können Sie auch die Unterordner angeben, auf die Ihr Konto Zugriff haben soll, indem Sie den Namen des Containers und den Pfad zum Unterordner definieren.

>[!BEGINTABS]

>[!TAB Verbindungszeichenfolge]

Um sich mit einem Kontoschlüssel zu authentifizieren, wählen Sie **[!UICONTROL Authentifizierung des Kontoschlüssels]** aus und geben Sie Ihre Verbindungszeichenfolge an. Während dieses Schritts können Sie auch den Namen des Containers und den Pfad zum Unterordner angeben, auf den Sie zugreifen möchten. Wählen Sie nach Abschluss **[!UICONTROL Mit Quelle verbinden]** aus.

![Verbindungszeichenfolge](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB SAS-URI]

Sie können SAS verwenden, um Authentifizierungsberechtigungen mit unterschiedlichem Zugriffsgrad zu erstellen, da eine SAS-basierte Authentifizierung es Ihnen ermöglicht, Berechtigungen, Start- und Ablaufdaten sowie Bestimmungen für bestimmte Ressourcen festzulegen.

Um sich mit einer Signatur für freigegebenen Zugriff zu authentifizieren, wählen Sie **[!UICONTROL Authentifizierung für freigegebene Zugriffssignatur]** und geben Sie dann Ihren SAS-URI an. Während dieses Schritts können Sie auch den Namen des Containers und den Pfad zum Unterordner angeben, auf den Sie zugreifen möchten. Wählen Sie nach Abschluss **[!UICONTROL Mit Quelle verbinden]** aus.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Blob]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in Platform](../../dataflow/batch/cloud-storage.md) zu übertragen.[
