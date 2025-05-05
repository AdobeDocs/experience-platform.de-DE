---
title: Erstellen einer Chatlio Source-Verbindung über die Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Chatlio-Quellverbindung erstellen.
badge: Beta
exl-id: 55c10bcb-0332-45ff-970b-272d375b591d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 21%

---

# Erstellen eines Quell-Connectors für [!DNL Chatlio] in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL Chatlio]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../../../home.md#terms-and-conditions) „Quellen - Übersicht“.

In diesem Tutorial finden Sie die Schritte zum Erstellen einer [!DNL Chatlio]-Quellverbindung mithilfe der Benutzeroberfläche von Adobe Experience Platform.

## Erste Schritte {#getting-started}

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Voraussetzungen {#prerequisites}

Im folgenden Abschnitt finden Sie Informationen zu Voraussetzungen, die erfüllt sein müssen, bevor Sie eine [!DNL Chatlio] Quellverbindung erstellen können.

### Beispiel-JSON zum Definieren des Quellschemas für [!DNL Chatlio] {#prerequisites-json-schema}

Bevor Sie eine [!DNL Chatlio] Quellverbindung erstellen, benötigen Sie ein Quellschema, das bereitgestellt werden muss. Sie können die folgende JSON verwenden.

```
{
  "visitor": {
    "email": "test@example.com",
    "UUID": "2d3f4260-2235-903b-0a82-a23d326cc257"
  },
   "message": "Hi",
  "channelId": "C04J7M7LCMQ",
  "slackChannelName": "aep",
  "slackChannelId": "C04JVR71WKS"
}
```

### Erstellen eines Experience Platform-Schemas für [!DNL Chatlio] {#create-platform-schema}

Sie müssen auch sicherstellen, dass Sie ein Experience Platform-Schema erstellen, das für Ihre Quelle verwendet werden soll. Eine ausführliche Anleitung zum Erstellen [ Schemas finden Sie im Tutorial ](../../../../../xdm/schema/composition.md) Erstellen eines Experience Platform-Schemas .

![Die Experience Platform-Benutzeroberfläche mit einem Beispielschema für Chatlio](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/schema.png)

## Verbinden Ihres [!DNL Chatlio]-Kontos {#connect-account}

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL linken Navigationsbereich die Option]** Quellen“ aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen und einen Quellkatalog anzuzeigen, der in Experience Platform verfügbar ist.

Verwenden Sie das Menü *[!UICONTROL Kategorien]*, um Quellen nach Kategorie zu filtern. Geben Sie alternativ einen Quellnamen in die Suchleiste ein, um eine bestimmte Quelle aus dem Katalog zu finden.

Gehen Sie zur Kategorie [!UICONTROL Marketing], um die [!DNL Chatlio] anzuzeigen. Wählen Sie zunächst **[!UICONTROL Daten hinzufügen]** aus.

![Der Experience Platform UI-Katalog mit Chatlio-Karte](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/catalog.png)

## Daten auswählen {#select-data}

Der Schritt **[!UICONTROL Daten auswählen]** wird angezeigt und bietet eine Schnittstelle zur Auswahl der Daten, die Sie an Experience Platform übermitteln möchten.

* Der linke Teil der Benutzeroberfläche ist ein Browser, mit dem Sie die verfügbaren Datenströme in Ihrem Konto anzeigen können.
* Im rechten Teil der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Datenzeilen aus einer JSON-Datei anzeigen.

Wählen Sie **[!UICONTROL Dateien hochladen]** aus, um eine JSON-Datei von Ihrem lokalen System hochzuladen. Alternativ können Sie die JSON-Datei, die Sie hochladen möchten, per Drag-and-Drop in das Bedienfeld [!UICONTROL Dateien per Drag-and-Drop &#x200B;].

![Der Schritt „Daten hinzufügen“ des Quell-Workflows.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/add-data.png)

Nachdem Ihre Datei hochgeladen wurde, wird die Vorschau-Oberfläche aktualisiert, um eine Vorschau des hochgeladenen Schemas anzuzeigen. In der Vorschauoberfläche können Sie den Inhalt und die Struktur einer Datei überprüfen. Sie können auch das Dienstprogramm [!UICONTROL Suchfeld] verwenden, um innerhalb Ihres Schemas auf bestimmte Elemente zuzugreifen.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Vorschauschritt des Quell-Workflows.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/preview.png)

## Datenflussdetails {#dataflow-detail}

Der Schritt **Datenflussdetails** wird angezeigt und bietet Ihnen Optionen zum Verwenden eines vorhandenen Datensatzes oder zum Einrichten eines neuen Datensatzes für Ihren Datenfluss sowie die Möglichkeit, einen Namen und eine Beschreibung für Ihren Datenfluss anzugeben. In diesem Schritt können Sie auch Einstellungen für die Profilaufnahme, Fehlerdiagnose, partielle Aufnahme und Warnhinweise konfigurieren.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Schritt „Datenflussdetails“ des Quell-Workflows.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/dataflow-detail.png)

## Zuordnung {#mapping}

Es erfolgt der Schritt der [!UICONTROL Zuordnung], in dem Ihnen eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden XDM-Zielfeldern im Zielschema bereitgestellt wird.

Experience Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Eine ausführliche Anleitung zur Verwendung der Zuordnungsschnittstelle und berechneter Felder finden Sie im [Handbuch zur Datenvorbereitungs-Benutzeroberfläche](../../../../../data-prep/ui/mapping.md).

Die unten aufgeführten Zuordnungen sind obligatorisch und sollten eingerichtet werden, bevor Sie mit der Phase [!UICONTROL Überprüfung] fortfahren.

| Zielfeld | Beschreibung |
| --- | --- |
| `UUID` | Die [!DNL Chatlio] Kennung für das Ereignis. |

Nachdem Ihre Quelldaten erfolgreich zugeordnet wurden, klicken Sie auf **[!UICONTROL Weiter]**.

![Der Zuordnungsschritt des Quell-Workflows.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/mapping.png)

## Überprüfung {#review}

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten innerhalb dieser Quelldatei an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![Der Überprüfungsschritt des Quell-Workflows.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/review.png)

## Abrufen der Streaming-Endpunkt-URL {#get-streaming-endpoint-url}

Nachdem Sie Ihren Streaming-Datenfluss erstellt haben, können Sie jetzt Ihre Streaming-Endpunkt-URL abrufen. Dieser Endpunkt wird verwendet, um Ihren Webhook zu abonnieren, sodass Ihre Streaming-Quelle mit Experience Platform kommunizieren kann.

Um die URL zu erstellen, die zum Konfigurieren des Webhooks in [!DNL Chatlio] verwendet wird, müssen Sie Folgendes abrufen:

* **[!UICONTROL Datenfluss-ID]**
* **[!UICONTROL Streaming-Endpunkt]**

Um Ihre **[!UICONTROL Datenfluss-ID]** und den **[!UICONTROL Streaming-Endpunkt]** abzurufen, gehen Sie zur Seite [!UICONTROL Datenflussaktivität] des soeben erstellten Datenflusses und kopieren Sie die Details am unteren Rand des Bedienfelds [!UICONTROL Eigenschaften].

![Der Streaming-Endpunkt in der Datenflussaktivität.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/endpoint-test.png)

Nachdem Sie Ihren Streaming-Endpunkt und Ihre Datenfluss-ID abgerufen haben, erstellen Sie eine URL nach dem folgenden Muster: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Eine erstellte Webhook-URL kann beispielsweise wie folgt aussehen: ``https://dcs.adobedc.net/collection/d56b47ee3985104beaf724efcd78a3e1a863d720471a482bebac0acc1ab95983``

## Webhook in [!DNL Chatlio] einrichten {#set-up-webhook}

Nachdem Sie Ihre Webhook-URL erstellt haben, können Sie Ihren Webhook jetzt über die [!DNL Chatlio]-Benutzeroberfläche einrichten.

Melden Sie sich bei Ihrem [[!DNL Chatlio]](https://chatlio.com/)-Konto an und befolgen Sie [Anleitung zur Einrichtung und Installation](https://chatlio.com/docs/setup/) um ein Widget zu erstellen.

Nachdem ein Widget erstellt wurde, navigieren Sie zur Seite „Einstellungen“ des Widgets, um Ihre Webhook-URL zu diesem Widget hinzuzufügen.

![Die Webhook-Einstellungsseite auf Chatlio.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/widget-settings.png)

Wählen Sie als Nächstes die Registerkarte **[!DNL Behavior]** aus und fügen Sie Ihre Webhook-URL zum Feld *[!DNL Webhook when a new conversation starts]* und zu allen anderen Webhook-Ereignissen hinzu, die Sie abonnieren möchten.

![Die Chatlio-Benutzeroberfläche mit dem Webhook-Endpunktfeld.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/webhook.png)

>[!TIP]
>
>Sie können eine Vielzahl verschiedener Ereignisse für Ihren [!DNL Chatlio] Webhook abonnieren. Weitere Informationen zu den verschiedenen Ereignissen finden Sie in der [[!DNL Chatlio] Ereignisdokumentation](https://chatlio.com/docs/webhooks/).

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie erfolgreich einen Streaming-Datenfluss konfiguriert, um Ihre [!DNL Chatlio]-Daten in Experience Platform zu übertragen. Informationen zum Überwachen der aufgenommenen Daten finden Sie im Handbuch unter [Überwachen von Streaming-Datenflüssen mithilfe der Experience Platform-Benutzeroberfläche](../../monitor-streaming.md).

## Zusätzliche Ressourcen {#additional-resources}

Die folgenden Abschnitte enthalten zusätzliche Ressourcen, auf die Sie bei Verwendung der [!DNL Chatlio] verweisen können.

### Validierung {#validation}

Um zu überprüfen, ob Sie die Quelle richtig eingerichtet haben und [!DNL Chatlio] Nachrichten aufgenommen werden, führen Sie die folgenden Schritte aus:

* Sie können die Seite [!DNL Chatlio] **[!UICONTROL Berichte]** > **[!UICONTROL Chat-]** überprüfen, um die von [!DNL Chatlio] erfassten Ereignisse zu identifizieren.

![Screenshot der Chatlio-Benutzeroberfläche mit dem Chatverlauf](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/chatlio-chat-history.png)

* Wählen Sie in der Benutzeroberfläche von Experience Platform **[!UICONTROL Datenflüsse anzeigen]** neben dem [!DNL Chatlio] im Quellkatalog aus. Wählen Sie als Nächstes **[!UICONTROL Vorschau des Datensatzes]** aus, um die Daten zu überprüfen, die für die Webhooks aufgenommen wurden, die Sie in [!DNL Chatlio] konfiguriert haben.

Screenshot der ![Experience Platform-Benutzeroberfläche mit aufgenommenen Ereignissen](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/platform-dataset.png)

Weitere Informationen zu [!DNL Chatlio] finden Sie in der [[!DNL Chatlio] Dokumentation](https://chatlio.com/docs/) und [FAQ](https://chatlio.com/pricing/#FAQ).
