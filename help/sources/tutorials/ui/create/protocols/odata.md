---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines generischen OData-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 598b29f681ac930a4e1781f7f298608c8344d807
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 15%

---


# Create a [!DNL Generic OData] source connector in the UI

>[!NOTE]
> Der [!DNL Generic OData] Anschluss befindet sich in der Betaphase. See the [Sources overview](../../../../home.md#terms-and-conditions) for more information on using beta-labelled connectors.

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Erstellen eines Generischen Open Data Protocol (im Folgenden &quot;OData&quot;)-Quellconnectors über die [!DNL Platform] Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)-System](../../../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Kundenprofil](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige OData-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Protokolldataset-Flusses fortfahren](../../dataflow/protocols.md)

### Erforderliche Anmeldedaten sammeln

In order to access your [!DNL OData] account in [!DNL Platform], you must provide the following values:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `url` | Die Stamm-URL des [!DNL OData] Dienstes. |

Weitere Informationen zum Einstieg finden Sie in [diesem OData-Dokument](https://www.odata.org/getting-started/basic-tutorial/).

## Connect your [!DNL OData] account

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues [!DNL OData] Konto für die Verbindung zu erstellen [!DNL Platform].

Log in to [Adobe Experience Platform](https://platform.adobe.com) and then select **[!UICONTROL Sources]** from the left navigation bar to access the *[!UICONTROL Sources]* workspace. Im Anzeigebereich &quot; *[!UICONTROL Katalog]* &quot;werden eine Reihe von Quellen angezeigt, für die Sie ein eingehendes Konto erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse, die ihnen zugeordnet sind.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie *[!UICONTROL Protokolle]* die Option **[!UICONTROL Generische OData]** , um eine Informationsleiste auf der rechten Seite des Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zum Herstellen einer Verbindung zur Quelle oder Ansicht der zugehörigen Dokumentation. Um eine neue eingehende Verbindung zu erstellen, wählen Sie **[!UICONTROL Hinzufügen Daten]**.

![Katalog](../../../../images/tutorials/create/odata/catalog.png)

Die Seite &quot; *[!UICONTROL Verbindung zu generischen OData]* herstellen&quot;wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im angezeigten Eingabedatum einen Namen, eine optionale Beschreibung und Ihre [!DNL OData] Anmeldeinformationen für die Verbindung ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis das neue Konto eingerichtet ist.

![connect](../../../../images/tutorials/create/odata/connect.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL OData] Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** , um fortzufahren.

![existing](../../../../images/tutorials/create/odata/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL OData] Konto hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Dataset-Fluss [konfigurieren, um Protokolldaten in Plattform](../../dataflow/protocols.md)zu importieren.