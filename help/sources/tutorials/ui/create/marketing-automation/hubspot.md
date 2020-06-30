---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines HubSpot-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---


# Erstellen eines [!DNL HubSpot] Quellconnectors in der Benutzeroberfläche

> [!NOTE]
> Der [!DNL HubSpot] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Quellschnittstellen in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Erstellen eines [!DNL HubSpot] Quell-Connectors mithilfe der [!DNL Platform] Benutzeroberfläche.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Zusammensetzung](../../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Profil](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine [!DNL HubSpot] Basisverbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses zur Marketingautomatisierung fortfahren](../../dataflow/marketing-automation.md).

### Erforderliche Berechtigungen erfassen

Um auf Ihr [!DNL HubSpot] Konto zugreifen zu können, müssen Sie die folgenden Werte angeben [!DNL Platform]:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `clientId` | Die mit Ihrer [!DNL HubSpot] Anwendung verknüpfte Client-ID. |
| `clientSecret` | Das mit Ihrer [!DNL HubSpot] Anwendung verknüpfte Clientgeheimnis. |
| `accessToken` | Das Zugriffstoken, das beim erstmaligen Authentifizieren der OAuth-Integration erhalten wurde. |
| `refreshToken` | Das Aktualisierungstoken, das beim erstmaligen Authentifizieren der OAuth-Integration erhalten wurde. |

Weitere Informationen zum Einstieg finden Sie in diesem [HubSpot-Dokument](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

## Verbinden Sie Ihr [!DNL HubSpot] Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um eine neue eingehende Basisverbindung zu erstellen, mit der Sie Ihr [!DNL HubSpot] Konto verknüpfen [!DNL Platform].

Melden Sie sich bei <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> an und wählen Sie dann in der linken Navigationsleiste **[!UICONTROL Quellen]** , um auf den *[!UICONTROL Quellarbeitsbereich]* zuzugreifen. Im Anzeigebereich &quot; *[!UICONTROL Katalog]* &quot;werden eine Vielzahl von Quellen angezeigt, mit denen Sie eingehende Basisverbindungen erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Basisverbindungen an, die mit ihnen verbunden sind.

Wählen Sie unter der Kategorie *[!UICONTROL Marketing Automation]* die Option **[!UICONTROL HubSpot]** , um eine Informationsleiste auf der rechten Seite Ihres Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zum Herstellen einer Verbindung zur Quelle oder Ansicht der zugehörigen Dokumentation. Um eine neue eingehende Basisverbindung zu erstellen, wählen Sie &quot; **[!UICONTROL Connect source]**&quot;aus.

![Katalog](../../../../images/tutorials/create/hubspot/catalog.png)

Die Seite &quot; *[!UICONTROL Verbindung mit HubSpot]* herstellen&quot;wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im eingeblendeten Eingabebild einen Namen, eine optionale Beschreibung und Ihre [!DNL HubSpot] Anmeldeinformationen für die Basisverbindung ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis die neue Basisverbindung hergestellt ist.

![connect](../../../../images/tutorials/create/hubspot/connect.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL HubSpot] Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** , um fortzufahren.

![existing](../../../../images/tutorials/create/hubspot/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Basisverbindung zu Ihrem [!DNL HubSpot] Konto aufgebaut. Sie können nun mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um die Daten des Marketingautomatisierungssystems in die Platform](../../dataflow/marketing-automation.md)zu bringen.