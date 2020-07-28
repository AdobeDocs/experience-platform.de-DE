---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Quell-Connectors für Azure Data Lake Storage Gen2 über die Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 17%

---


# Create an [!DNL Azure Data Lake Storage Gen2] source connector in the UI

Quellschnittstellen in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Authentifizieren eines [!DNL Azure Data Lake Storage Gen2] (im Folgenden &quot;ADLS Gen2&quot;) Quellconnectors über die [!DNL Platform] Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Experience-Datenmodell (XDM)-System](../../../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [Echtzeit-Kundenprofil](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine ADLS Gen2-Basisverbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Lernprogramm zur [Konfiguration eines Datenflusses](../../dataflow/batch/cloud-storage.md)fortfahren.

### Erforderliche Anmeldedaten sammeln

Um den ADLS Gen2-Quellanschluss zu authentifizieren, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `url` | Der Endpunkt für ADLS Gen2. |
| `servicePrincipalId` | Die Client-ID der Anwendung. |
| `servicePrincipalKey` | Der Schlüssel der Anwendung. |
| `tenant` | Die Mandanteninformationen, die Ihre Anwendung enthalten. |

Weitere Informationen zu diesen Werten finden Sie in [diesem ADLS Gen2-Dokument](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

## Schließen Sie Ihr ADLS Gen2-Konto an

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um eine neue eingehende Basisverbindung zu erstellen, mit der Sie Ihr ADLS Gen2-Konto verknüpfen [!DNL Platform].

Melden Sie sich bei <a href="https://platform.adobe.com" target="_blank">Adobe an [!DNL Experience Platform]</a> und wählen Sie dann in der linken Navigationsleiste **[!UICONTROL Quellen]** , um auf den *[!UICONTROL Quellarbeitsbereich]* zuzugreifen. Auf der Registerkarte &quot; *[!UICONTROL Katalog]* &quot;werden verschiedene Quellen angezeigt, für die eingehende Basisverbindungen erstellt werden können. Jede Quelle zeigt die Anzahl der vorhandenen Basisverbindungen an, die ihnen zugeordnet sind.

Wählen Sie unter der Kategorie *[!UICONTROL Cloud-Datenspeicherung]* die Option **[!UICONTROL Azurblauer Data Lake Gen2]** , um eine Informationsleiste auf der rechten Seite Ihres Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zum Herstellen einer Verbindung zur Quelldokumentation der Ansicht. Um eine neue eingehende Basisverbindung zu erstellen, klicken Sie auf Quelle **[!UICONTROL verbinden]**.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

Das Dialogfeld &quot; *[!UICONTROL Verbindung zu Azurblauer Data Lake Gen2]* &quot;wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im angezeigten Eingabedatum einen Namen, eine optionale Beschreibung und Ihre ADLS Gen2-Anmeldeinformationen für die Basisverbindung ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis die neue Basisverbindung hergestellt ist.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das ADLS Gen2-Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** , um fortzufahren.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Basisverbindung zu Ihrem ADLS Gen2-Konto hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in Platform](../../dataflow/batch/cloud-storage.md)zu übertragen.