---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Google AdWords-Quell-Connectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 14%

---


# Create a [!DNL Google AdWords] source connector in the UI

>[!NOTE]
>Der [!DNL Google AdWords] Anschluss befindet sich in der Betaphase. See the [Sources overview](../../../../home.md#terms-and-conditions) for more information on using beta-labelled connectors.

Source connectors in Adobe Experience Platform provide the ability to ingest externally sourced data on a scheduled basis. This tutorial provides steps for creating a [!DNL Google AdWords] source connector using the [!DNL Platform] user interface.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)-System](../../../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Kundenprofil](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine [!DNL Google AdWords] Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses fortfahren.](../../dataflow/payments.md)

### Erforderliche Anmeldedaten sammeln

Um auf Ihr [!DNL Google AdWords] Konto zugreifen zu können, [!DNL Platform]müssen Sie die folgenden Werte angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `clientCustomerId` | Die Kunden-ID des AdWords-Kontos. |
| `developerToken` | Das mit dem Managerkonto verknüpfte Entwicklertoken. |
| `refreshToken` | Das Aktualisierungstoken, das Sie [!DNL Google] zur Autorisierung des Zugriffs auf AdWords erhalten haben. |
| `clientId` | Die Client-ID der [!DNL Google] Anwendung, mit der das Aktualisierungstoken erfasst wird. |
| `clientSecret` | Das Clientgeheimnis der [!DNL Google] Anwendung, die zum Abrufen des Aktualisierungstokens verwendet wird. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [Google AdWords-Dokument](https://developers.google.com/adwords/api/docs/guides/authentication).

## Verbinden Sie Ihr [!DNL Google AdWords] Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um eine neue eingehende Basisverbindung zu erstellen, mit der Sie Ihr [!DNL Google AdWords] Konto verknüpfen [!DNL Platform].

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den *[!UICONTROL Quellarbeitsbereich]* zuzugreifen. Im Anzeigebereich &quot; *[!UICONTROL Katalog]* &quot;werden eine Vielzahl von Quellen angezeigt, mit denen Sie eingehende Basisverbindungen erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Basisverbindungen an, die mit ihnen verbunden sind.

Wählen Sie unter der Kategorie *[!UICONTROL Werbung]* die Option **[!UICONTROL Google AdWords]** , um eine Informationsleiste auf der rechten Seite Ihres Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zum Herstellen einer Verbindung zur Quelle oder Ansicht der zugehörigen Dokumentation. Um eine neue eingehende Basisverbindung zu erstellen, wählen Sie **[!UICONTROL Hinzufügen Daten]**.

![Katalog](../../../../images/tutorials/create/ads/catalog.png)

The *[!UICONTROL Connect to Google AdWords]* page appears. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. On the input form that appears, provide the base connection with a name, an optional description, and your [!DNL Google AdWords] credentials. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis die neue Basisverbindung hergestellt ist.

![connect](../../../../images/tutorials/create/ads/connect.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Google AdWords] Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** , um fortzufahren.

![existing](../../../../images/tutorials/create/ads/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Basisverbindung zu Ihrem [!DNL Google AdWords] Konto aufgebaut. You can now continue on to the next tutorial and [configure a dataflow to bring advertising data into Platform](../../dataflow/advertising.md).