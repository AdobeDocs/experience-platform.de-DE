---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Google Cloud-Datenspeicherung-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 799445eca080175e2bffc49c6714f0c812b9bbea
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 1%

---


# Erstellen eines Google Cloud-Datenspeicherung-Quellconnectors in der Benutzeroberfläche

Source Connectors in Adobe Experience Platform bieten die Möglichkeit, Daten aus externen Quellen planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Erstellen eines Google Cloud-Datenspeicherung-Quellconnectors (im Folgenden &quot;GCS&quot;) mithilfe der Plattform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung](../../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Profil](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine GCS-Basisverbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/batch/cloud-storage.md)fortfahren.

### Unterstützte Dateiformate

Experience Platform unterstützt die folgenden Dateiformate, die aus externen Datenspeicherung erfasst werden:

* Trennzeichen-getrennte Werte (DSV): Die Unterstützung für DSV-formatierte Datendateien ist derzeit auf kommagetrennte Werte beschränkt. Der Wert von Feldkopfzeilen in DSV-formatierten Dateien darf nur aus alphanumerischen Zeichen und Unterstrichen bestehen. Die Unterstützung für allgemeine DSV-Dateien wird in Zukunft bereitgestellt.
* JavaScript Object Notation (JSON): JSON-formatierte Datendateien müssen XDM-kompatibel sein.
* Apache Parquet: Parquet-formatierte Datendateien müssen XDM-konform sein.

### Erforderliche Berechtigungen erfassen

Um auf Ihre GCS-Daten auf der Plattform zugreifen zu können, müssen Sie eine gültige GCS- **Zugriffsschlüssel-ID** und **Geheimhaltung** angeben. Weitere Informationen zum Abrufen dieser Werte finden Sie im <a href="https://cloud.google.com/docs/authentication/production" target="_blank">Server-zu-Server-Authentifizierungshandbuch</a> für Google Cloud.

## Verbinden Sie Ihr GCS-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um eine neue eingehende Basisverbindung zu erstellen, um Ihr GCS-Konto mit der Plattform zu verknüpfen.

Melden Sie sich bei <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **Quellen** &quot;, um auf den *Quellenarbeitsbereich* zuzugreifen. Im Anzeigebereich &quot; *Katalog* &quot;werden eine Vielzahl von Quellen angezeigt, mit denen Sie eingehende Basisverbindungen erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Basisverbindungen an, die mit ihnen verbunden sind.

Wählen Sie unter der Kategorie *Cloud-Datenspeicherung* die Option **Google Cloud-Datenspeicherung** , um eine Informationsleiste auf der rechten Seite Ihres Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zum Herstellen einer Verbindung mit der Quelldokumentation oder zum Herstellen einer Verbindung mit der Ansicht. Um eine neue eingehende Basisverbindung zu erstellen, klicken Sie auf Quelle **verbinden**.

![](../../../../images/tutorials/create/google-cloud-storage/sources-catalog.png)

Das Dialogfeld &quot; _Verbindung mit Google Cloud-Datenspeicherung_ herstellen&quot;wird angezeigt. Geben Sie im Eingabedatum die Basisverbindung mit einem Namen, einer optionalen Beschreibung und Ihren GCS-Anmeldeinformationen ein. Klicken Sie abschließend auf **Verbinden** und lassen Sie dann etwas Zeit, bis die neue Basisverbindung hergestellt ist.

![](../../../../images/tutorials/create/google-cloud-storage/gcs-credentials.png)

Nachdem eine Basisverbindung hergestellt wurde, können Sie mit dem nächsten Abschnitt fortfahren und einen Datenflug konfigurieren, um Daten in die Plattform zu übertragen.

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Basisverbindung zu Ihrem GCS-Konto hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten in Plattform](../../dataflow/batch/cloud-storage.md)zu übertragen.