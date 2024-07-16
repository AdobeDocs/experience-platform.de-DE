---
title: Erstellen einer Pendo Source-Verbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Pendo-Quellverbindung erstellen.
badge: Beta
exl-id: defdec30-42af-43c8-b2eb-7ce98f7871e3
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 20%

---

# Erstellen eines Datenflusses für die Quellverbindung mit [!DNL Pendo] in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL Pendo]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellenübersicht](../../../../home.md#terms-and-conditions) .

In diesem Tutorial werden Schritte zum Erstellen einer [!DNL Pendo]-Quellverbindung und eines Datenflusses mithilfe der Adobe Experience Platform-Benutzeroberfläche beschrieben.

## Erste Schritte {#getting-started}

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Voraussetzungen {#prerequisites}

Im folgenden Abschnitt finden Sie Informationen zu den Voraussetzungen, die erfüllt sein müssen, bevor Sie eine [!DNL Pendo]-Quellverbindung erstellen können.

### Beispiel-JSON zum Definieren des Quellschemas für [!DNL Pendo] {#prerequisites-json-schema}

Bevor Sie eine [!DNL Pendo]-Quellverbindung erstellen, müssen Sie ein Quellschema angeben. Sie können die JSON unten verwenden.

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

Weitere Informationen finden Sie im [[!DNL Pendo] Handbuch zu Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks).

### Erstellen eines Platform-Schemas für [!DNL Pendo] {#create-platform-schema}

Sie müssen außerdem sicherstellen, dass Sie zunächst ein Platform-Schema erstellen, das für Ihre Quelle verwendet werden soll. Umfassende Schritte zum Erstellen eines Schemas finden Sie im Tutorial zum Erstellen eines Platform-Schemas](../../../../../xdm/schema/composition.md) .[

![Platform-Benutzeroberfläche mit einem Beispielschema für Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/schema.png)

## Verbinden Ihres [!DNL Pendo]-Kontos {#connect-account}

Wählen Sie in der Platform-Benutzeroberfläche im linken Navigationsbereich die Option **[!UICONTROL Quellen]** aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen und einen Quellkatalog anzuzeigen, der unter Experience Platform verfügbar ist.

Verwenden Sie das Menü *[!UICONTROL Kategorien]* , um Quellen nach Kategorie zu filtern. Geben Sie alternativ einen Quellnamen in die Suchleiste ein, um eine bestimmte Quelle aus dem Katalog zu finden.

Wechseln Sie zur Kategorie [!UICONTROL Analytics] , um die Quellkarte [!DNL Pendo] anzuzeigen. Wählen Sie zunächst **[!UICONTROL Daten hinzufügen]** aus.

![Der Quellkatalog der Platform-Benutzeroberfläche mit der Pendo-Karte.](../../../../images/tutorials/create/analytics-pendo-webhook/catalog.png)

## Daten auswählen {#select-data}

Der Schritt **[!UICONTROL Daten auswählen]** wird angezeigt und bietet eine Oberfläche zur Auswahl der Daten, die Sie an Platform übermitteln möchten.

* Der linke Teil der Benutzeroberfläche ist ein Browser, mit dem Sie die verfügbaren Datenströme in Ihrem Konto anzeigen können.
* Im rechten Bereich der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Zeilen mit Daten aus einer JSON-Datei anzeigen.

Wählen Sie **[!UICONTROL Dateien hochladen]** aus, um eine JSON-Datei von Ihrem lokalen System hochzuladen. Alternativ können Sie die JSON-Datei, die Sie hochladen möchten, per Drag-and-Drop in den Bereich [!UICONTROL Dateien ziehen und ablegen] ziehen.

![Der Schritt zum Hinzufügen von Daten des Ursprungs-Workflows.](../../../../images/tutorials/create/analytics-pendo-webhook/add-data.png)

Nach dem Hochladen Ihrer Datei wird die Vorschau-Oberfläche aktualisiert, um eine Vorschau des hochgeladenen Schemas anzuzeigen. Über die Vorschau-Oberfläche können Sie den Inhalt und die Struktur einer Datei überprüfen. Sie können auch das Dienstprogramm [!UICONTROL Suchfeld] verwenden, um auf bestimmte Elemente innerhalb Ihres Schemas zuzugreifen.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Vorschauschritt des Ursprungs-Workflows.](../../../../images/tutorials/create/analytics-pendo-webhook/preview.png)

## Datenflussdetails {#dataflow-detail}

Der Schritt **Datenfluss-Detail** wird angezeigt und bietet Ihnen Optionen zur Verwendung eines vorhandenen Datensatzes oder zur Einrichtung eines neuen Datensatzes für Ihren Datenfluss sowie die Möglichkeit, einen Namen und eine Beschreibung für Ihren Datenfluss anzugeben. In diesem Schritt können Sie auch Einstellungen für die Profilerfassung, Fehlerdiagnose, partielle Erfassung und Warnhinweise konfigurieren.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Schritt &quot;Datenfluss-Detail&quot;des Ursprungs-Workflows.](../../../../images/tutorials/create/analytics-pendo-webhook/dataflow-detail.png)

## Zuordnung {#mapping}

Es erfolgt der Schritt der [!UICONTROL Zuordnung], in dem Ihnen eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden XDM-Zielfeldern im Zielschema bereitgestellt wird.

Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Umfassende Schritte zur Verwendung der Zuordnungsoberfläche und der berechneten Felder finden Sie im Handbuch [Data Prep UI guide](../../../../../data-prep/ui/mapping.md).

Die unten aufgeführten Zuordnungen sind obligatorisch und sollten eingerichtet werden, bevor Sie mit der Phase [!UICONTROL Überprüfen] fortfahren.

| Zielfeld | Beschreibung |
| --- | --- |
| `uniqueId` | Die [!DNL Pendo]-Kennung für das Ereignis. |

Nachdem die Quelldaten erfolgreich zugeordnet wurden, wählen Sie **[!UICONTROL Weiter]** aus.

![Der Zuordnungsschritt des Ursprungs-Workflows.](../../../../images/tutorials/create/analytics-pendo-webhook/mapping.png)

## Überprüfung {#review}

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten innerhalb dieser Quelldatei an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![Der Überprüfungsschritt des Ursprungs-Workflows.](../../../../images/tutorials/create/analytics-pendo-webhook/review.png)

## Abrufen der Streaming-Endpunkt-URL {#get-streaming-endpoint-url}

Mit dem erstellten Streaming-Datenfluss können Sie jetzt Ihre Streaming-Endpunkt-URL abrufen. Dieser Endpunkt wird zum Abonnieren Ihres Webhooks verwendet, sodass Ihre Streaming-Quelle mit Experience Platform kommunizieren kann.

Um die URL zu erstellen, die zum Konfigurieren des Webhooks auf [!DNL Pendo] verwendet wird, müssen Sie Folgendes abrufen:

* **[!UICONTROL Datenfluss-ID]**
* **[!UICONTROL Streaming-Endpunkt]**

Um Ihre **[!UICONTROL Datenfluss-ID]** und Ihren **[!UICONTROL Streaming-Endpunkt]** abzurufen, rufen Sie die Seite [!UICONTROL Datenfluss-Aktivität] des soeben erstellten Datenflusses auf und kopieren Sie die Details aus dem unteren Bereich des Bereichs [!UICONTROL Eigenschaften] .

![ Der Streaming-Endpunkt in der Datenflug-Aktivität.](../../../../images/tutorials/create/analytics-pendo-webhook/endpoint-test.png)

Nachdem Sie Ihren Streaming-Endpunkt und Ihre Datenfluss-ID abgerufen haben, erstellen Sie eine URL basierend auf dem folgenden Muster: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Beispielsweise könnte eine konstruierte Webhook-URL wie folgt aussehen: ```https://dcs.adobedc.net/collection/0c61859cc71939a0caf01123f91b2fc52589018800ad46b6c76c2dff3595ee95```

## Webhook in [!DNL Pendo] einrichten {#set-up-webhook}

Melden Sie sich als Nächstes bei Ihrem Konto bei [[!DNL Pendo]](https://pendo.io/) an und erstellen Sie einen Webhook. Anweisungen zum Erstellen eines Webhooks mithilfe der Benutzeroberfläche von [!DNL Pendo] finden Sie im [[!DNL Pendo] Handbuch zum Erstellen von Webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

Nachdem Ihr Webhook erstellt wurde, navigieren Sie zur Einstellungsseite Ihres [!DNL Pendo]-Webhooks und geben Sie Ihre Webhook-URL in das Feld [!DNL URL] ein.

![Der Screenshot der Pendo-Benutzeroberfläche mit dem Webhook-Endpunktfeld](../../../../images/tutorials/create/analytics-pendo-webhook/webhook.png)

>[!TIP]
>
>Sie können eine Vielzahl verschiedener Ereigniskategorien abonnieren, um die Art der Ereignisse zu bestimmen, die Sie von Ihrer [!DNL Pendo] -Instanz an Platform senden möchten. Weitere Informationen zu den verschiedenen Ereignissen finden Sie in der [[!DNL Pendo] Dokumentation](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie erfolgreich einen Streaming-Datenfluss konfiguriert, um Ihre [!DNL Pendo] -Daten an Experience Platform zu übertragen. Informationen zum Überwachen der erfassten Daten finden Sie im Handbuch zum [Überwachen von Streaming-Datenflüssen mithilfe der Platform-Benutzeroberfläche](../../monitor-streaming.md).

## Zusätzliche Ressourcen {#additional-resources}

Die folgenden Abschnitte enthalten zusätzliche Ressourcen, auf die Sie bei Verwendung der [!DNL Pendo]-Quelle verweisen können.

### Validierung {#validation}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie die Quelle korrekt eingerichtet haben und [!DNL Pendo] Nachrichten erfasst werden:

* Sie können die Seite [!DNL Pendo] **[!UICONTROL Berichte]** > **[!UICONTROL Chat-Verlauf]** überprüfen, um die von [!DNL Pendo] erfassten Ereignisse zu identifizieren.

![Pendo UI-Screenshot mit dem Chat-Verlauf](../../../../images/tutorials/create/analytics-pendo-webhook/pendo-events.png)

* Wählen Sie in der Platform-Benutzeroberfläche im Quellkatalog neben dem Kartenmenü [!DNL Pendo] die Option **[!UICONTROL Datenflüsse anzeigen]** aus. Wählen Sie als Nächstes **[!UICONTROL Vorschau des Datensatzes anzeigen]** aus, um die Daten zu überprüfen, die für die Webhooks erfasst wurden, die Sie in [!DNL Pendo] konfiguriert haben.

![Screenshot der Platform-Benutzeroberfläche mit aufgenommenen Ereignissen](../../../../images/tutorials/create/analytics-pendo-webhook/platform-dataset.png)

### Fehler und Fehlerbehebung {#errors-and-troubleshooting}

Beim Überprüfen eines Datenfluss-Ablaufs wird möglicherweise die folgende Fehlermeldung ausgegeben: `The message can't be validated ... uniqueID:expected minLength:1, actual 0].`

![Screenshot der Platform-Benutzeroberfläche mit Fehler.](../../../../images/tutorials/create/analytics-pendo-webhook/error.png)

Um diesen Fehler zu beheben, müssen Sie sicherstellen, dass die *uniqueID* -Zuordnung eingerichtet wurde. Weitere Hinweise finden Sie im Abschnitt [Zuordnen](#mapping) .

Weitere Informationen finden Sie im [[!DNL Pendo] Hilfezentrum](https://www.pendo.io/help-center/).
