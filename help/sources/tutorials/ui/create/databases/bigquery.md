---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Google Big Abfrage-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---


# Erstellen eines [!DNL Google Big Query] Quellconnectors in der Benutzeroberfläche

> [!NOTE]
> Der [!DNL Google BigQuery] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Quellschnittstellen in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Erstellen eines [!DNL Google Big Query] (im Folgenden &quot;GBQ&quot;) Quell-Connectors mithilfe der [!DNL Platform] Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Zusammensetzung](../../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Profil](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine GBQ-Basisverbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/databases.md)fortfahren.

### Erforderliche Berechtigungen erfassen

Um auf Ihr GBQ-Konto zugreifen zu [!DNL Platform]können, müssen Sie die folgenden Werte angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `project` | Die Projekt-ID des [!DNL BigQuery] Standardprojekts, gegen das Abfrage werden soll. |
| `clientID` | Der ID-Wert, mit dem das Aktualisierungstoken generiert wird. |
| `clientSecret` | Der zum Generieren des Aktualisierungstokens verwendete geheime Wert. |
| `refreshToken` | Das Aktualisierungstoken, das aus [!DNL Google] der Autorisierung des Zugriffs auf [!DNL BigQuery]. |

Weitere Informationen zu diesen Werten finden Sie in [diesem GBQ-Dokument](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## Verbinden Sie Ihr GBQ-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um eine neue eingehende Basisverbindung zu erstellen, mit der Sie Ihr GBQ-Konto verknüpfen [!DNL Platform]können.

Melden Sie sich bei <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> an und wählen Sie dann in der linken Navigationsleiste **[!UICONTROL Quellen]** , um auf den *[!UICONTROL Quellarbeitsbereich]* zuzugreifen. Im Anzeigebereich &quot; *[!UICONTROL Katalog]* &quot;werden eine Vielzahl von Quellen angezeigt, mit denen Sie eingehende Basisverbindungen erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Basisverbindungen an, die mit ihnen verbunden sind.

Wählen Sie unter der Kategorie &quot; *[!UICONTROL Datenbanken]* &quot;die Option &quot; **[!UICONTROL Google Big-Abfrage]** &quot;, um eine Informationsleiste auf der rechten Seite Ihres Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zum Herstellen einer Verbindung zur Quelle oder Ansicht der zugehörigen Dokumentation. Um eine neue eingehende Basisverbindung zu erstellen, wählen Sie &quot; **[!UICONTROL Connect source]**&quot;aus.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

Die Seite &quot; *[!UICONTROL Verbindung zu Google Big-Abfrage]* herstellen&quot;wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im angezeigten Eingabedatum die Basisverbindung mit einem Namen, einer optionalen Beschreibung und Ihren GBQ-Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis die neue Basisverbindung hergestellt ist.

![](../../../../images/tutorials/create/google-big-query/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das GBQ-Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** , um fortzufahren.

![](../../../../images/tutorials/create/google-big-query/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Basisverbindung zu Ihrem GBQ-Konto aufgebaut. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten in die Platform](../../dataflow/databases.md)zu bringen.