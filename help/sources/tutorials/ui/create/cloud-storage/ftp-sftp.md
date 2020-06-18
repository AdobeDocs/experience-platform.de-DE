---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines FTP- oder SFTP-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 855f543a1cef394d121502f03471a60b97eae256
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 1%

---


# Erstellen eines FTP- oder SFTP-Quellconnectors in der Benutzeroberfläche

>[!NOTE]
>Die FTP- und SFTP-Anschlüsse befinden sich in der Betaversion. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Quellschnittstellen in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Erstellen eines FTP- oder SFTP-Quellconnectors mithilfe der Benutzeroberfläche &quot;Platform&quot;beschrieben.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung](../../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Profil](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige FTP- oder SFTP-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/batch/cloud-storage.md)fortfahren.

### Unterstützte Dateiformate

Experience Platform unterstützt die folgenden Dateiformate, die aus externen Quellen aufgenommen werden sollen:

* Trennzeichen-getrennte Werte (DSV): Die Unterstützung für DSV-formatierte Datendateien ist derzeit auf durch Kommas getrennte Werte (CSV) beschränkt. Der Wert von Feldkopfzeilen in DSV-formatierten Dateien darf nur aus alphanumerischen Zeichen und Unterstrichen bestehen. Die allgemeine DSV-Unterstützung soll in Zukunft bereitgestellt werden.
* JavaScript Object Notation (JSON): JSON-formatierte Datendateien müssen XDM-kompatibel sein.
* Apache Parquet: Parquet-formatierte Datendateien müssen XDM-konform sein.

### Erforderliche Berechtigungen erfassen

Um auf Ihren FTP- oder SFTP-Server auf der Platform zugreifen zu können, müssen Sie den **Hostnamen** des Servers, einen **Benutzernamen** und ein **Kennwort** angeben.

## Herstellen einer Verbindung mit dem FTP- oder SFTP-Server

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um ein neues FTP- oder SFTP-Konto für die Verbindung mit der Platform zu erstellen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste **[!UICONTROL Quellen]** , um auf den *[!UICONTROL Quellarbeitsbereich]* zuzugreifen. Im Anzeigebereich &quot; *[!UICONTROL Katalog]* &quot;werden verschiedene Quellen angezeigt, mit denen Sie ein eingehendes Konto erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse an, die mit ihnen verbunden sind.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie &quot; *[!UICONTROL Datenbanken]* &quot;die Option **[!UICONTROL SFTP]** durch Klicken **auf das Pluszeichen (+)** , um einen neuen FTP- oder SFTP-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/sftp/catalog.png)

Die Seite *[!UICONTROL Verbindung mit SFTP]* herstellen wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im angezeigten Eingabedatum einen Namen, eine optionale Beschreibung und Ihre FTP- oder SFTP-Anmeldeinformationen für die Verbindung ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis das neue Konto eingerichtet ist.

![connect](../../../../images/tutorials/create/sftp/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das FTP- oder SFTP-Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** , um fortzufahren.

![existing](../../../../images/tutorials/create/sftp/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem FTP- oder SFTP-Konto hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in die Platform](../../dataflow/batch/cloud-storage.md)zu bringen.