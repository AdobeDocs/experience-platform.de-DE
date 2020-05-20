---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Amazon Kinesis-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: dcd6293a71178fee14647f5b2c8b56d03d1ec7df
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---


# Erstellen eines Amazon Kinesis-Quellconnectors in der Benutzeroberfläche

>[!NOTE]
> Der Amazon Kinesis Connector befindet sich in der Betaphase. Die Funktionen und Dokumentation können sich ändern.

Source Connectors in Adobe Experience Platform bieten die Möglichkeit, Daten aus externen Quellen planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Authentifizieren eines Amazon Kinesis-Quellconnectors (im Folgenden &quot;Kinesis&quot;) mithilfe der Plattform-Benutzeroberfläche.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

- [Erlebnis-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   - [Grundlagen der Zusammensetzung](../../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   - [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [Echtzeit-Profil](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über ein Kinesis-Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/streaming/cloud-storage.md)fortfahren.

### Erforderliche Berechtigungen erfassen

Um den Kinesis-Quellanschluss zu authentifizieren, müssen Sie Werte für die folgenden Verbindungseigenschaften bereitstellen:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `accessKeyId` | Die Zugriffsschlüssel-ID für Ihr Kinesis-Konto. |
| `Secret access key` | Der geheime Zugriffsschlüssel für Ihr Kinesis-Konto. |
| `region` | Der Bereich Ihres AWS-Servers. |

Weitere Informationen zu diesen Werten finden Sie in [diesem Kinesis Dokument](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Verbinden Sie Ihr Kinesis-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr Kinesis-Konto mit der Plattform zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **Quellen** &quot;, um auf den *Quellenarbeitsbereich* zuzugreifen. Auf der Registerkarte &quot; *Katalog* &quot;werden verschiedene Quellen angezeigt, für die eine Verbindung zur Plattform möglich ist. Jede Quelle zeigt die Anzahl der vorhandenen Konten, die ihnen zugeordnet sind.

Wählen Sie unter der Kategorie *Cloud-Datenspeicherung* die Option **Amazon-Kinesis** und klicken Sie **auf das Pluszeichen (+)** , um einen neuen Kinesis-Connector zu erstellen.

![](../../../../images/tutorials/create/kinesis/catalog.png)

Das Dialogfeld &quot; *Verbindung mit Amazon-Kinesis* herstellen&quot;wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **Neues Konto**&quot;aus. Geben Sie im eingeblendeten Eingabefeld einen Namen, eine optionale Beschreibung und Ihre Kinesis-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie &quot; **Verbinden** &quot;und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![](../../../../images/tutorials/create/kinesis/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das Kinesis-Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **Weiter** , um fortzufahren.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Nächste Schritte

Durch Befolgen dieses Lernprogramms haben Sie eine Verbindung zu Ihrem Kinesis-Konto mit Platform hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in Platform](../../dataflow/streaming/cloud-storage.md)zu übertragen.