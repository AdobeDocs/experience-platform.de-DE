---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines FTP- oder SFTP-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 799445eca080175e2bffc49c6714f0c812b9bbea
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 1%

---


# Erstellen eines FTP- oder SFTP-Quellconnectors in der Benutzeroberfläche

Source Connectors in Adobe Experience Platform bieten die Möglichkeit, Daten aus externen Quellen planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Erstellen eines FTP- oder SFTP-Quellconnectors über die Plattform-Benutzeroberfläche.

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

Um auf Ihren FTP- oder SFTP-Server auf der Plattform zugreifen zu können, müssen Sie den **Hostnamen** des Servers, einen **Benutzernamen** und ein **Kennwort** angeben.

## Verbindung zum Server herstellen

Wenn die Anmeldeinformationen Ihres Servers bereit sind, können Sie die folgenden Schritte ausführen, um eine neue eingehende Basisverbindung zu erstellen, um Ihren FTP- oder SFTP-Server mit der Plattform zu verknüpfen.

Melden Sie sich bei <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> an und wählen Sie dann in der linken Navigationsleiste **Quellen** , um auf den Quellarbeitsbereich zuzugreifen. Im Anzeigebereich &quot; *Katalog* &quot;werden eine Vielzahl von Quellen angezeigt, mit denen Sie eingehende Basisverbindungen erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Basisverbindungen an, die mit ihnen verbunden sind.

Wählen Sie unter der Kategorie *Cloud-Datenspeicherung* entweder **FTP** oder **SFTP** , um eine Informationsleiste auf der rechten Seite des Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zur Ansicht der Dokumentation oder zur Verbindung mit der Quelle. Um eine neue eingehende Basisverbindung zu erstellen, klicken Sie auf Quelle **verbinden**.

![](../../../../images/tutorials/create/sftp/sftp_sources_catalog.png)

Geben Sie im Eingabefeld einen Namen, eine optionale Beschreibung und Ihre FTP- oder SFTP-Anmeldeinformationen für die Basisverbindung ein. Klicken Sie schließlich auf **Verbinden** und lassen Sie dann etwas Zeit, bis die neue Basisverbindung hergestellt ist.

![](../../../../images/tutorials/create/sftp/sftp_credentials.png)

Sobald eine Basisverbindung mit Ihrem FTP- oder SFTP-Server hergestellt wurde, können Sie mit dem nächsten Abschnitt fortfahren und einen Datendurchlauf konfigurieren, um Daten in die Plattform zu übertragen.

## Nächste Schritte

In diesem Lernprogramm haben Sie eine Verbindung zu Ihrem FTP- oder SFTP-Server hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten in Plattform](../../dataflow/batch/cloud-storage.md)zu übertragen.
