---
title: Erstellen einer Azure Blob Source-Verbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Benutzeroberfläche von Platform einen Azure Blob-Quell-Connector erstellen.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 30%

---

# Erstellen Sie eine [!DNL Azure Blob] Quellverbindung in der Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Azure Blob] (nachstehend &quot;genannt)[!DNL Blob]&quot;) Quellverbindung über die Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework für die Organisation von Kundenerlebnisdaten in Experience Platform.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Blob]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/batch/cloud-storage.md) fortfahren.

### Unterstützte Dateiformate

Experience Platform unterstützt die folgenden Dateiformate, die aus externen Speichern erfasst werden:

* Trennzeichen (DSV): Sie können ein beliebiges Trennzeichen für einzelne Spalten wie Tabulatoren, Kommas, senkrechte Striche, Semikolons oder Hash verwenden, um flache Dateien in jedem beliebigen Format zu erfassen.
* JavaScript Object Notation (JSON): JSON-formatierte Datendateien müssen XDM-konform sein.
* Apache Parquet: Parquet formatierte Datendateien müssen XDM-konform sein.

### Sammeln erforderlicher Anmeldeinformationen

Um auf Ihre [!DNL Blob] -Speicher in Platform bereitstellen, müssen Sie einen gültigen Wert für die folgenden Anmeldedaten angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| Verbindungszeichenfolge | Eine Zeichenfolge, die die für die Authentifizierung erforderlichen Autorisierungsinformationen enthält [!DNL Blob] in die Experience Platform. Die [!DNL Blob] Verbindungszeichenfolgenmuster ist: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Weitere Informationen zu Verbindungszeichenfolgen finden Sie in diesem [!DNL Blob] Dokument auf [Konfigurieren von Verbindungszeichenfolgen](https://docs.microsoft.com/de-de/azure/storage/common/storage-configure-connection-string). |
| SAS-URI | Der URI für die gemeinsame Zugriffssignatur, den Sie als alternativen Authentifizierungstyp verwenden können, um Ihre [!DNL Blob] -Konto. Die [!DNL Blob] Das SAS-URI-Muster lautet: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Weitere Informationen finden Sie in diesem [!DNL Blob] Dokument auf [URIs für freigegebene Zugriffssignatur](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| Container | Der Name des Containers, für den Sie Zugriff festlegen möchten. Beim Erstellen eines neuen Kontos mit dem [!DNL Blob] -Quelle können Sie einen Containernamen bereitstellen, um den Benutzerzugriff auf den Unterordner Ihrer Wahl anzugeben. |
| Ordnerpfad | Der Pfad zu dem Ordner, auf den Sie Zugriff gewähren möchten. |

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Blob]-Konto mit Platform zu verknüpfen.

## Verbinden Ihres [!DNL Blob]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Unter dem [!UICONTROL Cloud-Speicher] category, select **[!UICONTROL Azure Blob Storage]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Der Quellenkatalog der Experience Platform mit der ausgewählten Azure Blob Storage-Quelle.](../../../../images/tutorials/create/blob/catalog.png)

Die **[!UICONTROL Verbinden mit Azure Blob Storage]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Blob]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/blob/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihre neue [!DNL Blob] -Konto.

![Der neue Kontobildschirm für die Azure Blob Storage-Quelle.](../../../../images/tutorials/create/blob/new.png)

Die [!DNL Blob] -Quelle unterstützt sowohl die Authentifizierung des Kontoschlüssels als auch die Authentifizierung für freigegebene Zugriffssignaturen (SAS). Eine schlüsselbasierte Kontoauthentifizierung erfordert eine Verbindungszeichenfolge zur Überprüfung, während eine SAS-Authentifizierung einen URI verwendet, der eine sichere delegierte Autorisierung Ihres Kontos ermöglicht.

In diesem Schritt können Sie auch die Unterordner angeben, auf die Ihr Konto Zugriff haben soll, indem Sie den Namen des Containers und den Pfad zum Unterordner definieren.

>[!BEGINTABS]

>[!TAB Verbindungszeichenfolge]

Um sich mit einem Kontoschlüssel zu authentifizieren, wählen Sie **[!UICONTROL Kontoschlüsselauthentifizierung]** und geben Sie Ihre Verbindungszeichenfolge an. Während dieses Schritts können Sie auch den Namen des Containers und den Pfad zum Unterordner angeben, auf den Sie zugreifen möchten. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbindung mit Quelle herstellen]**.

![Verbindungszeichenfolge](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB SAS-URI]

Sie können SAS verwenden, um Authentifizierungsberechtigungen mit unterschiedlichem Zugriffsgrad zu erstellen, da eine SAS-basierte Authentifizierung es Ihnen ermöglicht, Berechtigungen, Start- und Ablaufdaten sowie Bestimmungen für bestimmte Ressourcen festzulegen.

Um sich mit einer Signatur für freigegebenen Zugriff zu authentifizieren, wählen Sie **[!UICONTROL Authentifizierung für gemeinsame Zugriffssignatur]** und geben Sie dann Ihren SAS-URI an. Während dieses Schritts können Sie auch den Namen des Containers und den Pfad zum Unterordner angeben, auf den Sie zugreifen möchten. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbindung mit Quelle herstellen]**.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Blob]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in Platform zu übertragen](../../dataflow/batch/cloud-storage.md).
