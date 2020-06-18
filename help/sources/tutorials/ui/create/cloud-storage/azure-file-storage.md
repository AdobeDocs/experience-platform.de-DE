---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Azurblase-Datenspeicherung-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: ced839f64bea48703c530c83d8592f3842c17e53
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---


# Erstellen eines Azurblase-Datenspeicherung-Quellconnectors in der Benutzeroberfläche

>[!NOTE]
>Der Azurblase File Datenspeicherung Stecker ist in Beta. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Quellschnittstellen in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Authentifizieren eines Azurblauen File Datenspeicherung-Quellconnectors mithilfe der Platform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

- [Erlebnis-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   - [Grundlagen der Zusammensetzung](../../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   - [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [Echtzeit-Profil](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine Dateiverbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/batch/cloud-storage.md)fortfahren.

### Erforderliche Berechtigungen erfassen

Um den Quellanschluss für die Datenspeicherung der Azurblase-Datei zu authentifizieren, müssen Sie Werte für die folgenden Verbindungseigenschaften bereitstellen:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Der Endpunkt der Azurblauen Dateiinstanz, auf die Sie zugreifen. |
| `userId` | Der Benutzer hat ausreichend Zugriff auf den Datenspeicherung-Endpunkt der Azurblauen Datei. |
| `password` | Die Azurblase-Datenspeicherung-Zugriffsschlüssel. |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem Dokument](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)der Azurblauen Datei-Datenspeicherung.

## Schließen Sie Ihr Azur File Datenspeicherung-Konto an

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues Azurblase File Datenspeicherung-Konto zu erstellen, um eine Verbindung zur Platform herzustellen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste **[!UICONTROL Quellen]** , um auf den *[!UICONTROL Quellarbeitsbereich]* zuzugreifen. Im Anzeigebereich &quot; *[!UICONTROL Katalog]* &quot;werden verschiedene Quellen angezeigt, mit denen Sie ein eingehendes Konto erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse an, die mit ihnen verbunden sind.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie &quot; *[!UICONTROL Datenbanken]* &quot;die Option &quot; **[!UICONTROL Azurblaue Dateidatei-Datenspeicherung]** &quot;aus und klicken Sie **auf das Pluszeichen (+)** , um einen neuen Azurblase-Datenspeicherung-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/azure-file-storage/catalog.png)

Die Seite &quot; *[!UICONTROL Verbindung mit der Datenspeicherung]* der leeren Datei herstellen&quot;wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im eingeblendeten Eingabebild einen Namen, eine optionale Beschreibung und Ihre Anmeldeinformationen für die Datenspeicherung ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis das neue Konto eingerichtet ist.

![connect](../../../../images/tutorials/create/azure-file-storage/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das Azurblase-Dateikonto aus, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** , um fortzufahren.

![existing](../../../../images/tutorials/create/azure-file-storage/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem Datenspeicherung-Konto von &quot;Blaue Datei&quot; hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in die Platform](../../dataflow/batch/cloud-storage.md)zu bringen.