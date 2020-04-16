---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Azurblauch- oder Amazon S3-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Erstellen eines Azurblauch- oder Amazon S3-Quellconnectors in der Benutzeroberfläche

Source Connectors in Adobe Experience Platform bieten die Möglichkeit, Daten aus externen Quellen planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Erstellen eines Azurblauch- (im Folgenden &quot;Blob&quot; genannt) oder Amazon S3-Quellconnectors (im Folgenden &quot;S3&quot; genannt) mithilfe der Plattform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung](../../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Profil](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine Blob- oder S3-Basisverbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/cloud-storage.md)fortfahren.

### Unterstützte Dateiformate

Experience Platform unterstützt die folgenden Dateiformate, die aus externen Datenspeicherung erfasst werden:

* Trennzeichen-getrennte Werte (DSV): Die Unterstützung für DSV-formatierte Datendateien ist derzeit auf kommagetrennte Werte beschränkt. Der Wert von Feldkopfzeilen in DSV-formatierten Dateien darf nur aus alphanumerischen Zeichen und Unterstrichen bestehen. Die Unterstützung für allgemeine DSV-Dateien wird in Zukunft bereitgestellt.
* JavaScript Object Notation (JSON): JSON-formatierte Datendateien müssen XDM-kompatibel sein.
* Apache Parquet: Parquet-formatierte Datendateien müssen XDM-konform sein.

### Erforderliche Berechtigungen erfassen

Um auf Ihre Blob-Datenspeicherung auf Platform zugreifen zu können, müssen Sie eine gültige Verbindungszeichenfolge für die **Datenspeicherung** bereitstellen. Sie können mehr über Verbindungs-Zeichenfolgen erfahren, einschließlich Möglichkeiten, sie durch <a href="https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string" target="_blank">dieses Microsoft-Azurblase-Dokument</a>zu erhalten.

Für den Zugriff auf den S3-Behälter auf der Plattform müssen Sie Ihren **S3-Zugriffsschlüssel** und **S3-Geheimschlüssel** angeben. For more information, refer to <a href="https://aws.amazon.com/blogs/security/wheres-my-secret-access-key/" target="_blank">this AWS document</a>.

## Verbinden Sie Ihr Blob- oder S3-Konto

Wenn die Anmeldeinformationen Ihrer Cloud-Datenspeicherung fertig sind, können Sie die folgenden Schritte ausführen, um eine neue eingehende Basisverbindung zu erstellen, um Ihr Blob- oder S3-Konto mit Platform zu verknüpfen.

Melden Sie sich bei <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **Quellen** &quot;, um auf den Quellarbeitsbereich zuzugreifen. Im Anzeigebereich &quot; *Katalog* &quot;werden eine Vielzahl von Quellen angezeigt, mit denen Sie eingehende Basisverbindungen erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Basisverbindungen an, die mit ihnen verbunden sind.

Wählen Sie unter der Kategorie &quot; *Cloud-Datenspeicherung* &quot;entweder **Azurblase-Datenspeicherung** oder **Amazon S3** , um eine Informationsleiste auf der rechten Seite Ihres Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zur Ansicht der Dokumentation oder zur Verbindung mit der Quelle. Um eine neue eingehende Basisverbindung zu erstellen, klicken Sie auf Quelle **verbinden**.

![](../../../../images/tutorials/create/s3/s3_sources_catalog.png)

Geben Sie im Eingabefeld einen Namen, eine optionale Beschreibung und Ihre Blob- oder S3-Anmeldeinformationen für die Basisverbindung ein. Klicken Sie schließlich auf **Verbinden** und lassen Sie dann etwas Zeit, bis die neue Basisverbindung hergestellt ist.

![](../../../../images/tutorials/create/s3/s3_credentials.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Basis-Verbindung zu Ihrem Blue Blob oder Amazon S3 Konto eingerichtet. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten in Plattform](../../dataflow/cloud-storage.md)zu übertragen.