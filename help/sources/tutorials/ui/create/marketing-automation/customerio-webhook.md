---
title: Erstellen einer Customer.io-Source-Verbindung und eines Datenflusses in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung von Customer.io erstellen.
badge: Beta
exl-id: 7655a34c-808a-46e3-94e3-022a433755a4
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 20%

---

# Erstellen einer [!DNL Customer.io]-Quellverbindung und eines Datenflusses in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL Customer.io]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellenübersicht](../../../../home.md#terms-and-conditions) .

In diesem Tutorial werden Schritte zum Erstellen einer [!DNL Customer.io]-Quellverbindung und eines Datenflusses mithilfe der Adobe Experience Platform-Benutzeroberfläche beschrieben.

## Erste Schritte {#getting-started}

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Voraussetzungen {#prerequisites}

Im folgenden Abschnitt finden Sie Informationen zu den Voraussetzungen, die erfüllt sein müssen, bevor Sie eine [!DNL Customer.io]-Quellverbindung erstellen können.

### Beispiel-JSON zum Definieren des Quellschemas für [!DNL Customer.io] {#prerequisites-json-schema}

Bevor Sie eine [!DNL Customer.io]-Quellverbindung erstellen, müssen Sie ein Quellschema angeben. Sie können die folgende JSON-Datei verwenden.

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

### Erstellen eines Platform-Schemas für [!DNL Customer.io] {#create-platform-schema}

Sie müssen außerdem sicherstellen, dass Sie ein Platform-Schema erstellen, das für Ihre Quelle verwendet werden soll. Umfassende Schritte zum Erstellen eines Schemas finden Sie im Tutorial zum Erstellen eines Platform-Schemas](../../../../../xdm/schema/composition.md) .[

![Screenshot der Platform-Benutzeroberfläche mit einem Beispielschema für Customer.io](../../../../images/tutorials/create/marketing-automation/customerio-webhook/schema.png)

## Verbinden Ihres [!DNL Customer.io]-Kontos {#connect-account}

Wählen Sie in der Platform-Benutzeroberfläche im linken Navigationsbereich die Option **[!UICONTROL Quellen]** aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen und einen Quellkatalog anzuzeigen, der unter Experience Platform verfügbar ist.

Verwenden Sie das Menü *[!UICONTROL Kategorien]* , um Quellen nach Kategorie zu filtern. Geben Sie alternativ einen Quellnamen in die Suchleiste ein, um eine bestimmte Quelle aus dem Katalog zu finden.

Wechseln Sie zur Kategorie [!UICONTROL Marketing-Automatisierung] , um die Quellkarte [!DNL Customer.io] anzuzeigen. Wählen Sie zunächst **[!UICONTROL Daten hinzufügen]** aus.

![Screenshot der Platform-Benutzeroberfläche für Katalog mit Customer.io-Karte](../../../../images/tutorials/create/marketing-automation/customerio-webhook/catalog.png)

## Daten auswählen {#select-data}

Der Schritt **[!UICONTROL Daten auswählen]** wird angezeigt und bietet eine Oberfläche zur Auswahl der Daten, die Sie an Platform übermitteln möchten.

* Der linke Teil der Benutzeroberfläche ist ein Browser, mit dem Sie die verfügbaren Datenströme in Ihrem Konto anzeigen können.
* Im rechten Bereich der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Zeilen mit Daten aus einer JSON-Datei anzeigen.

Wählen Sie **[!UICONTROL Dateien hochladen]** aus, um eine JSON-Datei von Ihrem lokalen System hochzuladen. Alternativ können Sie die JSON-Datei, die Sie hochladen möchten, per Drag-and-Drop in den Bereich [!UICONTROL Dateien ziehen und ablegen] ziehen.

![Der Schritt zum Hinzufügen von Daten des Ursprungs-Workflows.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//add-data.png)

Nach dem Hochladen Ihrer Datei wird die Vorschau-Oberfläche aktualisiert, um eine Vorschau des hochgeladenen Schemas anzuzeigen. Über die Vorschau-Oberfläche können Sie den Inhalt und die Struktur einer Datei überprüfen. Sie können auch das Dienstprogramm [!UICONTROL Suchfeld] verwenden, um auf bestimmte Elemente innerhalb Ihres Schemas zuzugreifen.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Vorschauschritt des Ursprungs-Workflows.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//preview.png)

## Datenflussdetails {#dataflow-detail}

Der Schritt **Datenfluss-Detail** wird angezeigt und bietet Ihnen Optionen zur Verwendung eines vorhandenen Datensatzes oder zur Einrichtung eines neuen Datensatzes für Ihren Datenfluss sowie die Möglichkeit, einen Namen und eine Beschreibung für Ihren Datenfluss anzugeben. In diesem Schritt können Sie auch Einstellungen für die Profilerfassung, Fehlerdiagnose, partielle Erfassung und Warnhinweise konfigurieren.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Schritt &quot;Datenfluss-Detail&quot;des Ursprungs-Workflows.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//dataflow-detail.png)

## Zuordnung {#mapping}

Es erfolgt der Schritt der [!UICONTROL Zuordnung], in dem Ihnen eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden XDM-Zielfeldern im Zielschema bereitgestellt wird.

Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Umfassende Schritte zur Verwendung der Zuordnungsoberfläche und der berechneten Felder finden Sie im Handbuch [Data Prep UI guide](../../../../../data-prep/ui/mapping.md).

Alle unten aufgeführten Zuordnungen sind obligatorisch und sollten eingerichtet werden, bevor Sie mit der Phase [!UICONTROL Überprüfen] fortfahren.

| Zielfeld | Beschreibung |
| --- | --- |
| `object_type` | Die unterstützten Typen werden in der Dokumentation [!DNL Customer.io] [events](https://customer.io/docs/webhooks/#events) beschrieben. |
| `id` | Die Kennung des Objekts. |
| `email` | Die mit dem Objekt verknüpfte E-Mail-Adresse. |
| `event_id` | Die eindeutige Kennung des Ereignisses. |
| `cio_id` | Die [!DNL Customer.io]-Kennung für das Ereignis. |
| `metric` | Der Ereignistyp. Weitere Informationen zu unterstützten Typen finden Sie in der Dokumentation zu [!DNL Customer.io] [events](https://customer.io/docs/webhooks/#events) . |
| `timestamp` | Der Zeitstempel, zu dem das Ereignis aufgetreten ist. |

>[!IMPORTANT]
>
>Mappen Sie beim Ausführen von [!DNL Customer.io] Webhook in der `test mode` nicht `cio_id`, da keine zugehörigen Felder von [!DNL Customer.io] gesendet werden.

Nachdem die Quelldaten erfolgreich zugeordnet wurden, wählen Sie **[!UICONTROL Weiter]** aus.

![Der Zuordnungsschritt des Ursprungs-Workflows.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/mapping.png)

## Überprüfung {#review}

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten innerhalb dieser Quelldatei an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![Der Überprüfungsschritt des Ursprungs-Workflows.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/review.png)

## Abrufen der Streaming-Endpunkt-URL {#get-streaming-endpoint}

Mit dem erstellten Streaming-Datenfluss können Sie jetzt Ihre Streaming-Endpunkt-URL abrufen. Dieser Endpunkt wird zum Abonnieren Ihres Webhooks verwendet, sodass Ihre Streaming-Quelle mit Experience Platform kommunizieren kann.

Um die URL zu erstellen, die zum Konfigurieren des Webhooks auf [!DNL Customer.io] verwendet wird, müssen Sie Folgendes abrufen:

* **[!UICONTROL Datenfluss-ID]**
* **[!UICONTROL Streaming-Endpunkt]**

Um Ihre **[!UICONTROL Datenfluss-ID]** und Ihren **[!UICONTROL Streaming-Endpunkt]** abzurufen, rufen Sie die Seite [!UICONTROL Datenfluss-Aktivität] des soeben erstellten Datenflusses auf und kopieren Sie die Details aus dem unteren Bereich des Bereichs [!UICONTROL Eigenschaften] .

![ Der Streaming-Endpunkt in der Datenflug-Aktivität.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/endpoint-test.png)

Nachdem Sie Ihren Streaming-Endpunkt und Ihre Datenfluss-ID abgerufen haben, erstellen Sie eine URL basierend auf dem folgenden Muster: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Beispielsweise könnte eine konstruierte Webhook-URL wie folgt aussehen: ``https://dcs.adobedc.net/collection/febc116d22ba0ea2868e9c93b199375302afb8a589617700991bb8f3f0341ad7?x-adobe-flow-id=439b3fc4-3042-4a3a-b5e0-a494898d3fb0``

## Einrichten des Berichts-Webhooks in [!DNL Customer.io] {#set-up-webhook}

Nachdem Sie Ihre Webhook-URL erstellt haben, können Sie jetzt Ihren Berichterstellungs-Webhook mithilfe der [!DNL Customer.io] -Benutzeroberfläche einrichten. Anweisungen zum Einrichten von Reporting-Webhooks finden Sie im [[!DNL Customer.io] Handbuch](https://customer.io/docs/webhooks/#setup) zum Einrichten von Webhooks.

Geben Sie in der Benutzeroberfläche von [!DNL Customer.io] Ihre [Webhook-URL](#get-streaming-endpoint-url) in das Feld [!DNL WEBHOOK ENDPOINT] ein.

![Die Benutzeroberfläche von Customer.io, die das Webhook-Endpunktfeld anzeigt](../../../../images/tutorials/create/marketing-automation/customerio-webhook/webhook.png)

>[!TIP]
>
>Sie können für Ihren Berichterstellungs-Webhook eine Vielzahl verschiedener Ereignisse abonnieren. Die Nachricht jedes Ereignisses wird in Platform erfasst, wenn die Kriterien für den Trigger eines Aktionsereignisses vom Typ [!DNL Customer.io] erfüllt sind. Weiterführende Informationen zu den verschiedenen Ereignissen finden Sie in der Dokumentation zu [[!DNL Customer.io] Ereignissen](https://customer.io/docs/webhooks/#events).

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie erfolgreich einen Streaming-Datenfluss konfiguriert, um Ihre [!DNL Customer.io] -Daten an Experience Platform zu übertragen. Informationen zum Überwachen der erfassten Daten finden Sie im Handbuch zum [Überwachen von Streaming-Datenflüssen mithilfe der Platform-Benutzeroberfläche](../../monitor-streaming.md).

## Zusätzliche Ressourcen {#additional-resources}

Die folgenden Abschnitte enthalten zusätzliche Ressourcen, auf die Sie bei Verwendung der [!DNL Customer.io]-Quelle verweisen können.

### Leitplanken {#guardrails}

Informationen zu Limits finden Sie auf der Seite [[!DNL Customer.io] Timeouts und Fehler](https://customer.io/docs/webhooks/#timeouts-and-failures).

### Validierung {#validation}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie die Quelle korrekt eingerichtet haben und [!DNL Customer.io] Nachrichten erfasst werden:

* Sie können die Seite [!DNL Customer.io] **[!UICONTROL Aktivitätsprotokolle]** überprüfen, um die von [!DNL Customer.io] erfassten Ereignisse zu identifizieren.

![UI-Screenshot des Kunden.io mit Aktivitätsprotokollen](../../../../images/tutorials/create/marketing-automation/customerio-webhook/activity-logs.png)

* Wählen Sie in der Platform-Benutzeroberfläche im Quellkatalog neben dem Kartenmenü [!DNL Customer.io] die Option **[!UICONTROL Datenflüsse anzeigen]** aus. Wählen Sie als Nächstes **[!UICONTROL Vorschau des Datensatzes anzeigen]** aus, um die Daten zu überprüfen, die für die Ereignisse erfasst wurden, die Sie in [!DNL Customer.io] ausgewählt haben.

![Screenshot der Platform-Benutzeroberfläche mit aufgenommenen Ereignissen](../../../../images/tutorials/create/marketing-automation/customerio-webhook/platform-dataset.png)
