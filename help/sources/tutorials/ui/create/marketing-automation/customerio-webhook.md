---
title: Erstellen einer Customer.io-Source-Verbindung und eines Datenflusses in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Customer.io-Quellverbindung erstellen.
badge: Beta
exl-id: 7655a34c-808a-46e3-94e3-022a433755a4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 20%

---

# Erstellen einer [!DNL Customer.io] Quellverbindung und eines Datenflusses in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL Customer.io]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../../../home.md#terms-and-conditions) „Quellen - Übersicht“.

In diesem Tutorial werden Schritte zum Erstellen einer [!DNL Customer.io] Quellverbindung und eines Datenflusses mithilfe der Adobe Experience Platform-Benutzeroberfläche beschrieben.

## Erste Schritte {#getting-started}

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Voraussetzungen {#prerequisites}

Im folgenden Abschnitt finden Sie Informationen zu Voraussetzungen, die erfüllt sein müssen, bevor Sie eine [!DNL Customer.io] Quellverbindung erstellen können.

### Beispiel-JSON zum Definieren des Quellschemas für [!DNL Customer.io] {#prerequisites-json-schema}

Bevor Sie eine [!DNL Customer.io] Quellverbindung erstellen, benötigen Sie ein Quellschema, das bereitgestellt werden muss. Sie können die folgende JSON-Datei verwenden.

```
{
  "event_id": "01E4C4CT6YDC7Y5M7FE1GWWPQJ",
  "object_type": "customer",
  "metric": "subscribed",
  "timestamp": 1613063089,
  "data": {
    "customer_id": "42",
    "email_address": "test@example.com",
    "identifiers": {
      "id": "42",
      "email": "test@example.com",
      "cio_id": "d9c106000001"
    }
  }
}
```

### Erstellen eines Experience Platform-Schemas für [!DNL Customer.io] {#create-platform-schema}

Sie müssen auch sicherstellen, dass Sie ein Experience Platform-Schema erstellen, das für Ihre Quelle verwendet werden soll. Eine ausführliche Anleitung zum Erstellen [ Schemas finden Sie ](../../../../../xdm/schema/composition.md) Tutorial zum Erstellen eines Experience Platform-Schemas .

Screenshot der ![Experience Platform-Benutzeroberfläche mit einem Beispielschema für Customer.io](../../../../images/tutorials/create/marketing-automation/customerio-webhook/schema.png)

## Verbinden Ihres [!DNL Customer.io]-Kontos {#connect-account}

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL linken Navigationsbereich die Option]** Quellen“ aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen und einen Quellkatalog anzuzeigen, der in Experience Platform verfügbar ist.

Verwenden Sie das Menü *[!UICONTROL Kategorien]*, um Quellen nach Kategorie zu filtern. Geben Sie alternativ einen Quellnamen in die Suchleiste ein, um eine bestimmte Quelle aus dem Katalog zu finden.

Gehen Sie zur Kategorie [!UICONTROL Marketing], um die [!DNL Customer.io] anzuzeigen. Wählen Sie zunächst **[!UICONTROL Daten hinzufügen]** aus.

![Screenshot der Experience Platform-Benutzeroberfläche für den Katalog mit der Karte Customer.io](../../../../images/tutorials/create/marketing-automation/customerio-webhook/catalog.png)

## Daten auswählen {#select-data}

Der Schritt **[!UICONTROL Daten auswählen]** wird angezeigt und bietet eine Schnittstelle zur Auswahl der Daten, die Sie an Experience Platform übermitteln möchten.

* Der linke Teil der Benutzeroberfläche ist ein Browser, mit dem Sie die verfügbaren Datenströme in Ihrem Konto anzeigen können.
* Im rechten Teil der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Datenzeilen aus einer JSON-Datei anzeigen.

Wählen Sie **[!UICONTROL Dateien hochladen]** aus, um eine JSON-Datei von Ihrem lokalen System hochzuladen. Alternativ können Sie die JSON-Datei, die Sie hochladen möchten, per Drag-and-Drop in das Bedienfeld [!UICONTROL Dateien per Drag-and-Drop &#x200B;].

![Der Schritt „Daten hinzufügen“ des Quell-Workflows.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//add-data.png)

Nachdem Ihre Datei hochgeladen wurde, wird die Vorschau-Oberfläche aktualisiert, um eine Vorschau des hochgeladenen Schemas anzuzeigen. In der Vorschauoberfläche können Sie den Inhalt und die Struktur einer Datei überprüfen. Sie können auch das Dienstprogramm [!UICONTROL Suchfeld] verwenden, um innerhalb Ihres Schemas auf bestimmte Elemente zuzugreifen.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Vorschauschritt des Quell-Workflows.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//preview.png)

## Datenflussdetails {#dataflow-detail}

Der Schritt **Datenflussdetails** wird angezeigt und bietet Ihnen Optionen zum Verwenden eines vorhandenen Datensatzes oder zum Einrichten eines neuen Datensatzes für Ihren Datenfluss sowie die Möglichkeit, einen Namen und eine Beschreibung für Ihren Datenfluss anzugeben. In diesem Schritt können Sie auch Einstellungen für die Profilaufnahme, Fehlerdiagnose, partielle Aufnahme und Warnhinweise konfigurieren.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Schritt „Datenflussdetails“ des Quell-Workflows.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//dataflow-detail.png)

## Zuordnung {#mapping}

Es erfolgt der Schritt der [!UICONTROL Zuordnung], in dem Ihnen eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden XDM-Zielfeldern im Zielschema bereitgestellt wird.

Experience Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Eine ausführliche Anleitung zur Verwendung der Zuordnungsschnittstelle und berechneter Felder finden Sie im [Handbuch zur Datenvorbereitungs-Benutzeroberfläche](../../../../../data-prep/ui/mapping.md).

Alle unten aufgeführten Zuordnungen sind obligatorisch und sollten eingerichtet werden, bevor Sie mit der Phase [!UICONTROL Überprüfung] fortfahren.

| Zielfeld | Beschreibung |
| --- | --- |
| `object_type` | Informationen zum Objekttyp finden Sie in der [!DNL Customer.io] [Ereignisse](https://customer.io/docs/webhooks/#events) Dokumentation zu den unterstützten Typen. |
| `id` | Die Kennung des Objekts. |
| `email` | Die mit dem Objekt verknüpfte E-Mail-Adresse. |
| `event_id` | Die eindeutige Kennung des Ereignisses. |
| `cio_id` | Die [!DNL Customer.io] Kennung für das Ereignis. |
| `metric` | Der Ereignistyp. Weitere Informationen zu unterstützten Typen finden Sie in der [!DNL Customer.io] [Ereignisse](https://customer.io/docs/webhooks/#events)-Dokumentation. |
| `timestamp` | Der Zeitstempel, wann das Ereignis aufgetreten ist. |

>[!IMPORTANT]
>
>Ordnen Sie beim Ausführen [!DNL Customer.io] Webhooks in der `test mode` keine `cio_id` zu, da keine zugehörigen Felder von [!DNL Customer.io] gesendet werden.

Nachdem Ihre Quelldaten erfolgreich zugeordnet wurden, klicken Sie auf **[!UICONTROL Weiter]**.

![Der Zuordnungsschritt des Quell-Workflows.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/mapping.png)

## Überprüfung {#review}

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten innerhalb dieser Quelldatei an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![Der Überprüfungsschritt des Quell-Workflows.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/review.png)

## Abrufen der Streaming-Endpunkt-URL {#get-streaming-endpoint}

Nachdem Sie Ihren Streaming-Datenfluss erstellt haben, können Sie jetzt Ihre Streaming-Endpunkt-URL abrufen. Dieser Endpunkt wird verwendet, um Ihren Webhook zu abonnieren, sodass Ihre Streaming-Quelle mit Experience Platform kommunizieren kann.

Um die URL zu erstellen, die zum Konfigurieren des Webhooks in [!DNL Customer.io] verwendet wird, müssen Sie Folgendes abrufen:

* **[!UICONTROL Datenfluss-ID]**
* **[!UICONTROL Streaming-Endpunkt]**

Um Ihre **[!UICONTROL Datenfluss-ID]** und den **[!UICONTROL Streaming-Endpunkt]** abzurufen, gehen Sie zur Seite [!UICONTROL Datenflussaktivität] des soeben erstellten Datenflusses und kopieren Sie die Details am unteren Rand des Bedienfelds [!UICONTROL Eigenschaften].

![Der Streaming-Endpunkt in der Datenflussaktivität.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/endpoint-test.png)

Nachdem Sie Ihren Streaming-Endpunkt und Ihre Datenfluss-ID abgerufen haben, erstellen Sie eine URL nach dem folgenden Muster: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Eine erstellte Webhook-URL kann beispielsweise wie folgt aussehen: ``https://dcs.adobedc.net/collection/febc116d22ba0ea2868e9c93b199375302afb8a589617700991bb8f3f0341ad7?x-adobe-flow-id=439b3fc4-3042-4a3a-b5e0-a494898d3fb0``

## Reporting-Webhook in [!DNL Customer.io] einrichten {#set-up-webhook}

Nachdem Sie Ihre Webhook-URL erstellt haben, können Sie jetzt Ihren Reporting-Webhook über die [!DNL Customer.io]-Benutzeroberfläche einrichten. Anweisungen zum Einrichten von Reporting-Webhooks finden Sie im [[!DNL Customer.io] Handbuch](https://customer.io/docs/webhooks/#setup) zum Einrichten von Webhooks.

Geben Sie in der [!DNL Customer.io]-Benutzeroberfläche Ihre [Webhook-URL](#get-streaming-endpoint-url) in das Feld [!DNL WEBHOOK ENDPOINT] ein.

![Die Benutzeroberfläche „Customer.io“, die das Feld „Webhook-Endpunkt“ anzeigt](../../../../images/tutorials/create/marketing-automation/customerio-webhook/webhook.png)

>[!TIP]
>
>Sie können eine Vielzahl verschiedener Ereignisse für Ihren Reporting-Webhook abonnieren. Die Nachricht jedes Ereignisses wird in Experience Platform aufgenommen, wenn die Kriterien für den Trigger eines [!DNL Customer.io] Aktionsereignisses erfüllt sind. Weitere Informationen zu den verschiedenen Ereignissen finden Sie in der [[!DNL Customer.io] Ereignisdokumentation](https://customer.io/docs/webhooks/#events).

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie erfolgreich einen Streaming-Datenfluss konfiguriert, um Ihre [!DNL Customer.io]-Daten in Experience Platform zu übertragen. Informationen zum Überwachen der aufgenommenen Daten finden Sie im Handbuch unter [Überwachen von Streaming-Datenflüssen mithilfe der Experience Platform-Benutzeroberfläche](../../monitor-streaming.md).

## Zusätzliche Ressourcen {#additional-resources}

Die folgenden Abschnitte enthalten zusätzliche Ressourcen, auf die Sie bei Verwendung der [!DNL Customer.io] verweisen können.

### Leitlinien {#guardrails}

Informationen zu Leitplanken finden Sie auf der Seite [[!DNL Customer.io] Zeitüberschreitungen und Fehler](https://customer.io/docs/webhooks/#timeouts-and-failures).

### Validierung {#validation}

Um zu überprüfen, ob Sie die Quelle richtig eingerichtet haben und [!DNL Customer.io] Nachrichten aufgenommen werden, führen Sie die folgenden Schritte aus:

* Sie können die Seite [!DNL Customer.io]&#x200B;**[!UICONTROL Aktivitätsprotokolle]** überprüfen, um die von [!DNL Customer.io] erfassten Ereignisse zu identifizieren.

![Screenshot der Benutzeroberfläche von Customer.io mit Aktivitätsprotokollen](../../../../images/tutorials/create/marketing-automation/customerio-webhook/activity-logs.png)

* Wählen Sie in der Benutzeroberfläche von Experience Platform **[!UICONTROL Datenflüsse anzeigen]** neben dem [!DNL Customer.io] im Quellkatalog aus. Wählen Sie als Nächstes **[!UICONTROL Vorschau des Datensatzes]** aus, um die Daten zu überprüfen, die für die Ereignisse aufgenommen wurden, die Sie in [!DNL Customer.io] ausgewählt haben.

Screenshot der ![Experience Platform-Benutzeroberfläche mit aufgenommenen Ereignissen](../../../../images/tutorials/create/marketing-automation/customerio-webhook/platform-dataset.png)
