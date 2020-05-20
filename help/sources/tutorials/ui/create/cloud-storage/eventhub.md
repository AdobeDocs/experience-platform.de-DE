---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Azurblauen Ereignis-Hubs-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 75581529ede3772606bc18fea683da5d396996c5
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---


# Erstellen eines Azurblauen Ereignis-Hubs-Quellconnectors in der Benutzeroberfläche

>[!NOTE]
> Der Azurblauer Ereignis Hubs Stecker ist in Beta. Die Funktionen und Dokumentation können sich ändern.

Source Connectors in Adobe Experience Platform bieten die Möglichkeit, Daten aus externen Quellen planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Authentifizieren eines Azurblauen Ereignis-Hubs (im Folgenden &quot;Ereignis Hubs&quot; genannt) mithilfe der Plattform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

- [Erlebnis-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   - [Grundlagen der Zusammensetzung](../../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   - [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [Echtzeit-Profil](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über ein Ereignis-Hubs-Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/streaming/cloud-storage.md)fortfahren.

### Erforderliche Berechtigungen erfassen

Um den Ereignis-Hubs-Quellanschluss zu authentifizieren, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `sasKeyName` | Der Name der Autorisierungsregel, der auch als SAS-Schlüsselname bezeichnet wird. |
| `sasKey` | Die generierte Unterschrift für den gemeinsamen Zugriff. |
| `namespace` | Der Namensraum der Ereignis-Hubs, auf die Sie zugreifen. |

Weitere Informationen zu diesen Werten finden Sie in [diesem Ereignis-Hubs-Dokument](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Verbinden Sie Ihr Ereignis-Hubs-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr Ereignis-Hubs-Konto mit der Plattform zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **Quellen** &quot;, um auf den *Quellenarbeitsbereich* zuzugreifen. Auf der Registerkarte &quot; *Katalog* &quot;werden verschiedene Quellen angezeigt, für die eine Verbindung zur Plattform möglich ist. Jede Quelle zeigt die Anzahl der vorhandenen Konten, die ihnen zugeordnet sind.

Wählen Sie unter der Kategorie *Cloud-Datenspeicherung* die Option **Azurblauer Ereignis-Hubs** und klicken Sie **auf das Pluszeichen (+)** , um einen neuen Ereignis-Hubs-Connector zu erstellen.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Der Dialog *Verbindung zu Azurblauer Ereignis Hubs* wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **Neues Konto**&quot;aus. Geben Sie im angezeigten Eingabedatum einen Namen, eine optionale Beschreibung und Ihre Ereignis-Hubs-Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie &quot; **Verbinden** &quot;und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![](../../../../images/tutorials/create/eventhub/new.png)

### Vorhandenes Konto

Um ein bestehendes Konto zu verknüpfen, wählen Sie das Ereignis-Hubs-Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **Weiter** , um fortzufahren.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Nächste Schritte

Indem Sie diesem Tutorial folgen, haben Sie Ihr Ereignis-Hubs-Konto mit Platform verbunden. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in Platform](../../dataflow/streaming/cloud-storage.md)zu übertragen.