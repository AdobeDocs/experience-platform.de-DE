---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: PayPal-Quellanschluss in der Benutzeroberfläche erstellen
topic: overview
translation-type: tm+mt
source-git-commit: 7328226b8349ffcdddadbd27b74fc54328b78dc5
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---


# PayPal-Quellanschluss in der Benutzeroberfläche erstellen

> [!NOTE]
> Der PayPal-Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Quellschnittstellen in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. In diesem Lernprogramm werden die Schritte zum Erstellen eines PayPal-Quell-Connectors mithilfe der Benutzeroberfläche &quot;Platform&quot;beschrieben.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung](../../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Profil](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine PayPal-Basisverbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses fortfahren](../../dataflow/payments.md)

### Erforderliche Berechtigungen erfassen

Um auf Ihre PayPal-Platform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Die URL der PayPal-Instanz. |
| `clientID` | Die mit Ihrer PayPal-Anwendung verknüpfte Client-ID. |
| `clientSecret` | Das mit Ihrer PayPal-Anwendung verknüpfte Client-Geheimnis. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [PayPal-Dokument](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Verbinden Sie Ihr PayPal-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um eine neue eingehende Basisverbindung zu erstellen, um Ihr PayPal-Konto mit der Platform zu verknüpfen.

Melden Sie sich bei <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> an und wählen Sie dann in der linken Navigationsleiste **Quellen** , um auf den *Quellarbeitsbereich* zuzugreifen. Im Anzeigebereich &quot; *Katalog* &quot;werden eine Vielzahl von Quellen angezeigt, mit denen Sie eingehende Basisverbindungen erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Basisverbindungen an, die mit ihnen verbunden sind.

Wählen Sie unter der *CRM* -Kategorie **PayPal** , um eine Informationsleiste auf der rechten Seite Ihres Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zum Herstellen einer Verbindung zur Quelle oder Ansicht der zugehörigen Dokumentation. Um eine neue eingehende Basisverbindung zu erstellen, wählen Sie &quot; **Connect source**&quot;aus.

![Katalog](../../../../images/tutorials/create/paypal/catalog.png)

Die Seite *Verbindung zu PayPal* herstellen wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **Neues Konto**&quot;aus. Geben Sie im eingeblendeten Eingabebild einen Namen, eine optionale Beschreibung und Ihre PayPal-Anmeldeinformationen für die Basisverbindung ein. Wenn Sie fertig sind, wählen Sie &quot; **Verbinden** &quot;und lassen Sie dann etwas Zeit, bis die neue Basisverbindung hergestellt ist.

![connect](../../../../images/tutorials/create/paypal/connect.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das PayPal-Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **Weiter** , um fortzufahren.

![existing](../../../../images/tutorials/create/paypal/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Basisverbindung zu Ihrem PayPal-Konto hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um CRM-Daten in die Platform](../../dataflow/payments.md)zu bringen.