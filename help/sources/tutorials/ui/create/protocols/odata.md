---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines generischen OData-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---


# Erstellen eines [!DNL Generic OData] Quellconnectors in der Benutzeroberfläche

> [!NOTE]
> Der [!DNL Generic OData] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Quellschnittstellen in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Erstellen eines Generischen Open Data Protocol (im Folgenden &quot;OData&quot;)-Quellconnectors über die [!DNL Platform] Benutzeroberfläche.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Zusammensetzung](../../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Profil](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige OData-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Protokolldataset-Flusses fortfahren](../../dataflow/protocols.md)

### Erforderliche Berechtigungen erfassen

Für den Zugriff auf Ihr [!DNL OData] Konto in müssen Sie die folgenden Werte angeben [!DNL Platform]:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `url` | Die Stamm-URL des [!DNL OData] Dienstes. |

Weitere Informationen zum Einstieg finden Sie in [diesem OData-Dokument](https://www.odata.org/getting-started/basic-tutorial/).

## Verbinden Sie Ihr [!DNL OData] Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues [!DNL OData] Konto für die Verbindung zu erstellen [!DNL Platform].

Melden Sie sich bei <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> an und wählen Sie dann in der linken Navigationsleiste **[!UICONTROL Quellen]** , um auf den *[!UICONTROL Quellarbeitsbereich]* zuzugreifen. Im Anzeigebereich &quot; *[!UICONTROL Katalog]* &quot;werden eine Reihe von Quellen angezeigt, für die Sie ein eingehendes Konto erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse, die ihnen zugeordnet sind.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie *[!UICONTROL Protokolle]* die Option **[!UICONTROL Generische OData]** , um eine Informationsleiste auf der rechten Seite des Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zum Herstellen einer Verbindung zur Quelle oder Ansicht der zugehörigen Dokumentation. Um eine neue eingehende Verbindung zu erstellen, wählen Sie Quelle **[!UICONTROL verbinden]**.

![Katalog](../../../../images/tutorials/create/odata/catalog.png)

Die Seite &quot; *[!UICONTROL Verbindung zu generischen OData]* herstellen&quot;wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im angezeigten Eingabedatum einen Namen, eine optionale Beschreibung und Ihre [!DNL OData] Anmeldeinformationen für die Verbindung ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis das neue Konto eingerichtet ist.

![connect](../../../../images/tutorials/create/odata/connect.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL OData] Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** , um fortzufahren.

![existing](../../../../images/tutorials/create/odata/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL OData] Konto hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und einen Datenfluss [konfigurieren, um Protokolldaten in die Platform](../../dataflow/protocols.md)zu bringen.