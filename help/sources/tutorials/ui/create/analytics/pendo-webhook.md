---
title: Erstellen einer Pendo-Quellverbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Pendo-Quellverbindung erstellen.
badge: Beta
exl-id: defdec30-42af-43c8-b2eb-7ce98f7871e3
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 21%

---

# Erstellen Sie eine [!DNL Pendo] Datenfluss der Quellverbindung und in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL Pendo]-Quelle befindet sich in der Beta-Phase. Bitte lesen Sie die [Quellen - Übersicht](../../../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Pendo] Quellverbindung und Datenfluss über die Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte {#getting-started}

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Voraussetzungen {#prerequisites}

Im folgenden Abschnitt finden Sie Informationen zu Voraussetzungen, die erfüllt sein müssen, bevor Sie eine [!DNL Pendo] Quellverbindung.

### JSON-Beispieldatei zum Definieren des Quellschemas für [!DNL Pendo] {#prerequisites-json-schema}

Vor der Erstellung [!DNL Pendo] Quellverbindung verwenden, müssen Sie ein Quellschema angeben. Sie können die JSON unten verwenden.

```
{
  "accountId": "58f79ee324d3f",
  "timestamp": 1673372516,
  "visitorId": "test@test.com",
  "uniqueId": "166e50cdf40930fe1367e4d44795c9c74d88b83a",
  "properties": {
    "guideProperties": {
  "name": "Guide Conversion Test"
  }
}
}
```

Weitere Informationen finden Sie im Abschnitt [[!DNL Pendo] Handbuch zu Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks).

### Erstellen eines Platform-Schemas für [!DNL Pendo] {#create-platform-schema}

Sie müssen außerdem sicherstellen, dass Sie zunächst ein Platform-Schema erstellen, das für Ihre Quelle verwendet werden soll. Siehe Tutorial zu [Erstellen eines Platform-Schemas](../../../../../xdm/schema/composition.md) für umfassende Schritte zum Erstellen eines Schemas.

![Platform-Benutzeroberfläche mit einem Beispielschema für Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/schema.png)

## Verbinden Ihres [!DNL Pendo]-Kontos {#connect-account}

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** über die linke Navigationsleiste auf [!UICONTROL Quellen] Arbeitsbereich und sehen Sie sich einen Quellkatalog an, der unter Experience Platform verfügbar ist.

Verwenden Sie die *[!UICONTROL Kategorien]* Menü zum Filtern von Quellen nach Kategorie. Geben Sie alternativ einen Quellnamen in die Suchleiste ein, um eine bestimmte Quelle aus dem Katalog zu finden.

Navigieren Sie zu [!UICONTROL Analytics] -Kategorie, um die [!DNL Pendo] Quellkarte. Wählen Sie zunächst **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog der Platform-Benutzeroberfläche mit der Pendo-Karte.](../../../../images/tutorials/create/analytics-pendo-webhook/catalog.png)

## Daten auswählen {#select-data}

Die **[!UICONTROL Daten auswählen]** angezeigt, um eine Oberfläche zur Auswahl der Daten bereitzustellen, die Sie an Platform übermitteln möchten.

* Der linke Teil der Benutzeroberfläche ist ein Browser, mit dem Sie die verfügbaren Datenströme in Ihrem Konto anzeigen können.
* Im rechten Bereich der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Zeilen mit Daten aus einer JSON-Datei anzeigen.

Auswählen **[!UICONTROL Dateien hochladen]** , um eine JSON-Datei von Ihrem lokalen System hochzuladen. Alternativ können Sie die hochzuladende JSON-Datei per Drag-and-Drop in die [!UICONTROL Dateien per Drag &amp; Drop verschieben] Bedienfeld.

![Der Schritt Daten hinzufügen des Ursprungs-Workflows.](../../../../images/tutorials/create/analytics-pendo-webhook/add-data.png)

Nach dem Hochladen Ihrer Datei wird die Vorschau-Oberfläche aktualisiert, um eine Vorschau des hochgeladenen Schemas anzuzeigen. Über die Vorschau-Oberfläche können Sie den Inhalt und die Struktur einer Datei überprüfen. Sie können auch die [!UICONTROL Suchfeld] -Dienstprogramm zum Zugreifen auf bestimmte Elemente aus Ihrem Schema.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Vorschauschritt des Ursprungs-Workflows.](../../../../images/tutorials/create/analytics-pendo-webhook/preview.png)

## Datenflussdetails {#dataflow-detail}

Die **Datenflussdetails** -Schritt angezeigt, der Ihnen Optionen zur Verwendung eines vorhandenen Datensatzes oder zur Einrichtung eines neuen Datensatzes für Ihren Datenfluss sowie die Möglichkeit bietet, einen Namen und eine Beschreibung für Ihren Datenfluss bereitzustellen. In diesem Schritt können Sie auch Einstellungen für die Profilerfassung, Fehlerdiagnose, partielle Erfassung und Warnhinweise konfigurieren.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Schritt dataflow-detail des Ursprungs-Workflows.](../../../../images/tutorials/create/analytics-pendo-webhook/dataflow-detail.png)

## Zuordnung {#mapping}

Es erfolgt der Schritt der [!UICONTROL Zuordnung], in dem Ihnen eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden XDM-Zielfeldern im Zielschema bereitgestellt wird.

Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Umfassende Schritte zur Verwendung der Mapper-Oberfläche und der berechneten Felder finden Sie im Abschnitt [Handbuch zur Datenvorbereitung-Benutzeroberfläche](../../../../../data-prep/ui/mapping.md).

Die unten aufgeführten Zuordnungen sind obligatorisch und sollten eingerichtet werden, bevor Sie mit dem [!UICONTROL Überprüfen] Bühne.

| Zielfeld | Beschreibung |
| --- | --- |
| `uniqueId` | Die [!DNL Pendo] Kennung für das Ereignis. |

Nachdem die Quelldaten erfolgreich zugeordnet wurden, wählen Sie **[!UICONTROL Nächste]**.

![Der Zuordnungsschritt des Ursprungs-Workflows.](../../../../images/tutorials/create/analytics-pendo-webhook/mapping.png)

## Überprüfung {#review}

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten innerhalb dieser Quelldatei an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![Der Überprüfungsschritt des Ursprungs-Workflows.](../../../../images/tutorials/create/analytics-pendo-webhook/review.png)

## Abrufen der Streaming-Endpunkt-URL {#get-streaming-endpoint-url}

Mit dem erstellten Streaming-Datenfluss können Sie jetzt Ihre Streaming-Endpunkt-URL abrufen. Dieser Endpunkt wird zum Abonnieren Ihres Webhooks verwendet, sodass Ihre Streaming-Quelle mit Experience Platform kommunizieren kann.

Um die URL zu erstellen, mit der der Webhook konfiguriert wird [!DNL Pendo] Sie müssen Folgendes abrufen:

* **[!UICONTROL Dataflow-ID]**
* **[!UICONTROL Streaming-Endpunkt]**

So rufen Sie Ihre **[!UICONTROL Dataflow-ID]** und **[!UICONTROL Streaming-Endpunkt]**, navigieren Sie zu [!UICONTROL Datenfluss-Aktivität] Seite des soeben erstellten Datenflusses und kopieren Sie die Details vom unteren Rand des [!UICONTROL Eigenschaften] Bedienfeld.

![Der Streaming-Endpunkt in der Datenfluss-Aktivität.](../../../../images/tutorials/create/analytics-pendo-webhook/endpoint-test.png)

Nachdem Sie Ihren Streaming-Endpunkt und Ihre Datenfluss-ID abgerufen haben, erstellen Sie eine URL basierend auf dem folgenden Muster: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Beispielsweise könnte eine konstruierte Webhook-URL wie folgt aussehen: ```https://dcs.adobedc.net/collection/0c61859cc71939a0caf01123f91b2fc52589018800ad46b6c76c2dff3595ee95```

## Einrichten von Webhook in [!DNL Pendo] {#set-up-webhook}

Melden Sie sich als Nächstes bei Ihrem Konto an bei [[!DNL Pendo]](https://pendo.io/) und erstellen Sie einen Webhook. Anweisungen zum Erstellen eines Webhooks mit dem [!DNL Pendo] Die Benutzeroberfläche, siehe [[!DNL Pendo] Handbuch zum Erstellen von Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

Nachdem Ihr Webhook erstellt wurde, navigieren Sie zur Einstellungsseite Ihrer [!DNL Pendo] Webhook erstellen und Ihre Webhook-URL in [!DNL URL] -Feld.

![Der Screenshot der Pendo-Benutzeroberfläche mit dem Webhook-Endpunktfeld](../../../../images/tutorials/create/analytics-pendo-webhook/webhook.png)

>[!TIP]
>
>Sie können verschiedene Ereigniskategorien abonnieren, um die Art der Ereignisse zu bestimmen, die Sie von Ihrer [!DNL Pendo] -Instanz in Platform. Weitere Informationen zu den verschiedenen Veranstaltungen finden Sie im Abschnitt [[!DNL Pendo] Dokumentation](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie erfolgreich einen Streaming-Datenfluss konfiguriert, um Ihre [!DNL Pendo] Daten an Experience Platform. Informationen zum Überwachen der erfassten Daten finden Sie im Handbuch unter [Überwachen von Streaming-Datenflüssen mithilfe der Platform-Benutzeroberfläche](../../monitor-streaming.md).

## Zusätzliche Ressourcen {#additional-resources}

Die folgenden Abschnitte enthalten zusätzliche Ressourcen, auf die Sie bei der Verwendung der Variablen [!DNL Pendo] -Quelle.

### Validierung {#validation}

Überprüfen, ob Sie die Quelle richtig eingerichtet haben und [!DNL Pendo] -Nachrichten werden erfasst, führen Sie die folgenden Schritte aus:

* Sie können die [!DNL Pendo] **[!UICONTROL Berichte]** > **[!UICONTROL Chat-Verlauf]** Seite, um die Ereignisse zu identifizieren, von denen [!DNL Pendo].

![Screenshot der Pendo-Benutzeroberfläche mit Chat-Verlauf](../../../../images/tutorials/create/analytics-pendo-webhook/pendo-events.png)

* Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Datenflüsse anzeigen]** neben dem [!DNL Pendo] Kartenmenü im Quellkatalog. Wählen Sie als Nächstes **[!UICONTROL Datensatz-Vorschau]** , um die Daten zu überprüfen, die für die Webhooks erfasst wurden, die Sie in [!DNL Pendo].

![Screenshot der Platform-Benutzeroberfläche mit aufgenommenen Ereignissen](../../../../images/tutorials/create/analytics-pendo-webhook/platform-dataset.png)

### Fehler und Fehlerbehebung {#errors-and-troubleshooting}

Beim Überprüfen eines Datenfluss-Ablaufs wird möglicherweise die folgende Fehlermeldung angezeigt: `The message can't be validated ... uniqueID:expected minLength:1, actual 0].`

![Screenshot der Platform-Benutzeroberfläche mit Fehlermeldung.](../../../../images/tutorials/create/analytics-pendo-webhook/error.png)

Um diesen Fehler zu beheben, müssen Sie sicherstellen, dass die Variable *uniqueID* -Mapping eingerichtet wurde. Weitere Hinweise finden Sie im Abschnitt [Mapping](#mapping) Abschnitt.

Weitere Informationen finden Sie unter [[!DNL Pendo] Hilfe-Center](https://www.pendo.io/help-center/).
