---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines HubSpot-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Erstellen eines HubSpot-Quellconnectors in der Benutzeroberfläche

Source Connectors in Adobe Experience Platform bieten die Möglichkeit, Daten aus externen Quellen planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Erstellen eines HubSpot-Quell-Connectors mithilfe der Plattform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung](../../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Profil](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine HubSpot-Basisverbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses zur Marketingautomatisierung fortfahren](../../dataflow/marketing-automation.md).

### Erforderliche Berechtigungen erfassen

Um auf Ihr HubSpot-Konto auf Plattform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `clientId` | Die mit Ihrer HubSpot-Anwendung verknüpfte Client-ID. |
| `clientSecret` | Das mit Ihrer HubSpot-Anwendung verknüpfte Client-Geheimnis. |
| `accessToken` | Das Zugriffstoken, das beim erstmaligen Authentifizieren der OAuth-Integration erhalten wurde. |
| `refreshToken` | Das Aktualisierungstoken, das beim erstmaligen Authentifizieren der OAuth-Integration erhalten wurde. |

Weitere Informationen zum Einstieg finden Sie in diesem [HubSpot-Dokument](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

## Verbinden Sie Ihr HubSpot-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um eine neue eingehende Basisverbindung zu erstellen, um Ihr HubSpot-Konto mit der Plattform zu verknüpfen.

Melden Sie sich bei <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **Quellen** &quot;, um auf den *Quellenarbeitsbereich* zuzugreifen. Im Anzeigebereich &quot; *Katalog* &quot;werden eine Vielzahl von Quellen angezeigt, mit denen Sie eingehende Basisverbindungen erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Basisverbindungen an, die mit ihnen verbunden sind.

Wählen Sie unter der Kategorie *Marketing Automation* die Option **HubSpot** , um eine Informationsleiste auf der rechten Seite Ihres Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zum Herstellen einer Verbindung zur Quelle oder Ansicht der zugehörigen Dokumentation. Um eine neue eingehende Basisverbindung zu erstellen, wählen Sie &quot; **Connect source**&quot;aus.

![Katalog](../../../../images/tutorials/create/hubspot/catalog.png)

Die Seite &quot; *Verbindung mit HubSpot* herstellen&quot;wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **Neues Konto**&quot;aus. Geben Sie im eingeblendeten Eingabebild einen Namen, eine optionale Beschreibung und Ihre HubSpot-Anmeldedaten für die Basisverbindung ein. Wenn Sie fertig sind, wählen Sie &quot; **Verbinden** &quot;und lassen Sie dann etwas Zeit, bis die neue Basisverbindung hergestellt ist.

![connect](../../../../images/tutorials/create/hubspot/connect.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das HubSpot-Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **Weiter** , um fortzufahren.

![existing](../../../../images/tutorials/create/hubspot/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Basisverbindung zu Ihrem HubSpot-Konto aufgebaut. Sie können nun mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten aus Marketingautomatisierungssystemen in Platform](../../dataflow/marketing-automation.md)zu bringen.