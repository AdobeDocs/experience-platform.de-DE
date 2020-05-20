---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Google Ads-Quell-Connectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 3b5821d641d35e1190ea9fecfd4def5beced6ecc
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---


# Erstellen eines Google Ads-Quell-Connectors in der Benutzeroberfläche

Source Connectors in Adobe Experience Platform bieten die Möglichkeit, Daten aus externen Quellen planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Erstellen eines Google Ads-Quell-Connectors mithilfe der Plattform-Benutzeroberfläche.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung](../../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Profil](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine Google Ads-Basisverbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses fortfahren](../../dataflow/payments.md)

### Erforderliche Berechtigungen erfassen

Um auf Ihre Google Ads-Kontoplattform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `clientCustomerId` | Die Kunden-ID des Ads-Kontos. |
| `developerToken` | Das mit dem Managerkonto verknüpfte Entwicklertoken. |
| `refreshToken` | Das Aktualisierungstoken, das von Google für die Autorisierung des Zugriffs auf Anzeigen erhalten wurde. |
| `clientId` | Die Client-ID der Google-Anwendung, mit der das Aktualisierungstoken erfasst wurde. |
| `clientSecret` | Das Clientgeheimnis der Google-Anwendung, das zum Abrufen des Aktualisierungstokens verwendet wurde. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [Google Ads-Dokument](https://developers.google.com/adwords/api/docs/guides/authentication).

## Google Ads-Konto verbinden

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um eine neue eingehende Basisverbindung zu erstellen, um Ihr Google Ads-Konto mit der Plattform zu verknüpfen.

Melden Sie sich bei <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **Quellen** &quot;, um auf den *Quellenarbeitsbereich* zuzugreifen. Im Anzeigebereich &quot; *Katalog* &quot;werden eine Vielzahl von Quellen angezeigt, mit denen Sie eingehende Basisverbindungen erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Basisverbindungen an, die mit ihnen verbunden sind.

Wählen Sie unter der *Kategorie &quot;Werbung* &quot;die Option &quot; **Google-Anzeigen** &quot;, um eine Informationsleiste auf der rechten Seite Ihres Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zum Herstellen einer Verbindung zur Quelle oder Ansicht der zugehörigen Dokumentation. Um eine neue eingehende Basisverbindung zu erstellen, wählen Sie &quot; **Connect source**&quot;aus.

![Katalog](../../../../images/tutorials/create/ads/catalog.png)

Die Seite *Verbindung mit Google Ads* herstellen wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **Neues Konto**&quot;aus. Geben Sie im eingeblendeten Eingabebild einen Namen, eine optionale Beschreibung und Ihre Google Ads-Anmeldedaten für die Basisverbindung ein. Wenn Sie fertig sind, wählen Sie &quot; **Verbinden** &quot;und lassen Sie dann etwas Zeit, bis die neue Basisverbindung hergestellt ist.

![connect](../../../../images/tutorials/create/ads/connect.png)

### Vorhandenes Konto

Um ein bestehendes Konto zu verbinden, wählen Sie das Google Ads-Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **Weiter** , um fortzufahren.

![existing](../../../../images/tutorials/create/ads/existing.png)

## Nächste Schritte

Indem Sie diesem Tutorial folgen, haben Sie eine Basisverbindung zu Ihrem Google Ads-Konto hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und einen Datenbogen [konfigurieren, um Werbedaten in Plattform](../../dataflow/advertising.md)zu übertragen.