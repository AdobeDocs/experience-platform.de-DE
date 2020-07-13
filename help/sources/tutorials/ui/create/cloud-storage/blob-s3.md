---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Quell-Connectors für Amazon S3 über die Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 16%

---


# Create an [!DNL Azure Blob] or [!DNL Amazon] S3 source connector in the UI

Quellschnittstellen in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Erstellen eines [!DNL Azure Blob] (im Folgenden &quot;Blob&quot; genannt) oder [!DNL Amazon] S3-Quellconnectors (im Folgenden &quot;S3&quot; genannt) mithilfe der [!DNL Platform] Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [XDM-System (Experience-Datenmodell)](../../../../../xdm/home.md): Das standardisierte Framework, nach dem Daten zum Kundenerlebnis in Experience Platform organisiert werden.
   - [Grundlagen zum Aufbau von Schemas](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [Echtzeit-Kundenprofil](../../../../../profile/home.md): Ein durch die Zusammenführung von Daten aus verschiedenen Quellen erstelltes Profil, das eine zentrale Echtzeit-Sicht auf Kunden liefert.

Wenn Sie bereits über eine Blob- oder S3-Basisverbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/batch/cloud-storage.md)fortfahren.

### Unterstützte Dateiformate

[!DNL Experience Platform] unterstützt die folgenden Dateiformate, die von externen Datenspeicherung erfasst werden:

- Trennzeichen-getrennte Werte (DSV): Die Unterstützung für DSV-formatierte Datendateien ist derzeit auf kommagetrennte Werte beschränkt. Der Wert von Feldkopfzeilen in DSV-formatierten Dateien darf nur aus alphanumerischen Zeichen und Unterstrichen bestehen. Die Unterstützung für allgemeine DSV-Dateien wird in Zukunft bereitgestellt.
- JavaScript Object Notation (JSON): JSON-formatierte Datendateien müssen XDM-kompatibel sein.
- Apache Parquet: Parquet-formatierte Datendateien müssen XDM-konform sein.

### Erforderliche Anmeldedaten sammeln

Um auf Ihre Blob-Datenspeicherung zugreifen zu können, müssen Sie einen gültigen Wert für die folgende Berechtigung angeben: [!DNL Platform]

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die Verbindungszeichenfolge, die für den Zugriff auf Daten in Ihrer Blob-Datenspeicherung erforderlich ist. Das Muster für die Zeichenfolge der Blob-Verbindung lautet: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Für weitere Informationen über den Einstieg besuchen Sie [dieses blaue Blob Dokument](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string).

Für den Zugriff auf den S3-Behälter unter [!DNL Platform] müssen Sie außerdem gültige Werte für die folgenden Anmeldeinformationen angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `s3AccessKey` | Die Zugriffsschlüssel-ID für Ihre S3-Datenspeicherung. |
| `s3SecretKey` | Die geheime Schlüssel-ID für Ihre S3-Datenspeicherung. |

Weitere Informationen zum Einstieg finden Sie in [diesem AWS-Dokument](https://aws.amazon.com/blogs/security/wheres-my-secret-access-key/).

## Verbinden Sie Ihr Blob- oder S3-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues Blob- oder S3-Konto zu erstellen, mit dem eine Verbindung hergestellt werden soll [!DNL Platform].

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste **[!UICONTROL Quellen]** , um auf den *[!UICONTROL Quellarbeitsbereich]* zuzugreifen. Im Anzeigebereich &quot; *[!UICONTROL Katalog]* &quot;werden verschiedene Quellen angezeigt, mit denen Sie ein eingehendes Konto erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse an, die mit ihnen verbunden sind.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie &quot; *[!UICONTROL Datenbanken]* &quot;die Option **[!UICONTROL Azurblase-Datenspeicherung]** oder **[!UICONTROL Amazon S3]** , indem Sie **auf das +-Symbol (+)** klicken, um einen neuen [!DNL Blob] oder S3-Anschluss zu erstellen.

![Katalog](../../../../images/tutorials/create/blob/catalog.png)

Die Seite &quot; *[!UICONTROL Verbindung mit der Blase-Datenspeicherung]* herstellen&quot;wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im angezeigten Eingabedatum einen Namen, eine optionale Beschreibung und Ihre [!DNL Blob] oder S3-Anmeldeinformationen für die Verbindung ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis das neue Konto eingerichtet ist.

![connect](../../../../images/tutorials/create/blob/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Blob] oder S3-Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** , um fortzufahren.

![existing](../../../../images/tutorials/create/blob/existing.png)

## Nächste Schritte und zusätzliche Ressourcen

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Blob] oder S3-Konto hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in Platform](../../dataflow/batch/cloud-storage.md)zu übertragen.