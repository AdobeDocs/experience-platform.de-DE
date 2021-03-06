---
keywords: Experience Platform; Ziel-API; Ad-hoc-Aktivierung; Ad-hoc-Aktivierung von Segmenten aktivieren
solution: Experience Platform
title: Aktivieren von Zielgruppensegmenten für Batch-Ziele über die Ad-hoc-Aktivierungs-API
description: Dieser Artikel veranschaulicht den End-to-End-Workflow zum Aktivieren von Zielgruppensegmenten über die Ad-hoc-Aktivierungs-API, einschließlich der Segmentierungsaufträge, die vor der Aktivierung ausgeführt werden.
topic-legacy: tutorial
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: 9e191d52d8385d716ed312725f72bd85c1e4b72d
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 14%

---

# Aktivieren von Zielgruppensegmenten bei Bedarf für Batch-Ziele über die Ad-hoc-Aktivierungs-API

>[!IMPORTANT]
>
>Nach Abschluss der Beta-Phase wird die [!DNL ad-hoc activation API] ist jetzt allgemein für alle Experience Platform-Kunden verfügbar (GA). In der GA-Version wurde die API auf Version 2 aktualisiert. Schritt 4 ([Abrufen der neuesten Segmentexportauftrag-ID](#segment-export-id)) ist nicht mehr erforderlich, da die API die Export-ID nicht mehr benötigt.
>
>Siehe [Ausführen des Ad-hoc-Aktivierungsauftrags](#activation-job) Weitere Informationen finden Sie weiter unten in diesem Tutorial .

## Übersicht {#overview}

Mit der Ad-hoc-Aktivierungs-API können Marketing-Experten Zielgruppensegmente schnell und effizient für Situationen aktivieren, in denen eine sofortige Aktivierung erforderlich ist.

Das folgende Diagramm zeigt den End-to-End-Workflow zum Aktivieren von Segmenten über die Ad-hoc-Aktivierungs-API, einschließlich der Segmentierungsaufträge, die alle 24 Stunden in Platform stattfinden.

![Ad-hoc-Aktivierung](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

>[!NOTE]
>
>Die Ad-hoc-Zielgruppenaktivierung wird nur von [Batch-dateibasierte Ziele](../destination-types.md#file-based).

## Anwendungsfälle {#use-cases}

### Flash-Verkäufe oder -Promotions

Ein Online-Händler bereitet einen begrenzten Flash-Verkauf vor und möchte Kunden kurzfristig benachrichtigen. Über die Ad-hoc-Aktivierungs-API der Experience Platform kann das Marketing-Team bei Bedarf Segmente exportieren und Werbe-E-Mails schnell an den Kundenstamm senden.

### Aktuelle Veranstaltungen oder aktuelle Nachrichten

Ein Hotel erwartet ein schlechtes Wetter an den folgenden Tagen, und das Team möchte die ankommenden Gäste schnell informieren, damit sie entsprechend planen können. Das Marketing-Team kann die Ad-hoc-Aktivierungs-API der Experience Platform verwenden, um Segmente bei Bedarf zu exportieren und die Gäste zu benachrichtigen.

### Integrationstests

IT-Manager können die Ad-hoc-Aktivierungs-API der Experience Platform verwenden, um Segmente bei Bedarf zu exportieren, sodass sie ihre benutzerdefinierte Integration mit Adobe Experience Platform testen und sicherstellen können, dass alles ordnungsgemäß funktioniert.

## Limits {#guardrails}

Beachten Sie bei der Verwendung der Ad-hoc-Aktivierungs-API die folgenden Limits.

* Derzeit kann jeder Ad-hoc-Aktivierungsauftrag bis zu 80 Segmente aktivieren. Der Versuch, mehr als 80 Segmente pro Auftrag zu aktivieren, führt dazu, dass der Auftrag fehlschlägt. Dieses Verhalten kann sich in zukünftigen Versionen ändern.
* Ad-hoc-Aktivierungsvorgänge können nicht parallel zu geplanten Aktivitäten ausgeführt werden [Segmentexportaufträge](../../segmentation/api/export-jobs.md). Bevor Sie einen Ad-hoc-Aktivierungsauftrag ausführen, stellen Sie sicher, dass der geplante Segmentexportauftrag abgeschlossen ist. Siehe [Ziel-Datenfluss-Überwachung](../../dataflows/ui/monitor-destinations.md) Informationen zur Überwachung des Status der Aktivierungsflüsse. Wenn Ihr Aktivierungsdataflow beispielsweise eine **[!UICONTROL Verarbeitung]** -Status, warten Sie, bis sie abgeschlossen ist, bevor Sie den Ad-hoc-Aktivierungsauftrag ausführen.
* Führen Sie nicht mehr als einen gleichzeitigen Ad-hoc-Aktivierungsauftrag pro Segment aus.

## Überlegungen zur Segmentierung {#segmentation-considerations}

Adobe Experience Platform führt geplante Segmentierungsaufträge einmal alle 24 Stunden aus. Die Ad-hoc-Aktivierungs-API wird basierend auf den neuesten Segmentierungsergebnissen ausgeführt.

## Schritt 1: Voraussetzungen {#prerequisites}

Bevor Sie die Adobe Experience Platform-APIs aufrufen können, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

* Sie verfügen über ein IMS-Organisationskonto mit Zugriff auf Adobe Experience Platform.
* Ihr Experience Platform-Konto verfügt über die `developer` und `user` Rollen, die für das Adobe Experience Platform API-Produktprofil aktiviert sind. Wenden Sie sich an [Admin Console](../../access-control/home.md) Administrator, um diese Rollen für Ihr Konto zu aktivieren.
* Du hast einen Adobe ID. Wenn Sie keine Adobe ID haben, navigieren Sie zum [Adobe Developer-Konsole](https://developer.adobe.com/console) und erstellen Sie ein neues Konto.

## Schritt 2: Sammeln von Anmeldeinformationen {#credentials}

Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Ressourcen in Experience Platform lassen sich in spezifischen virtuellen Sandboxes isolieren. Bei Anfragen an Platform-APIs können Sie den Namen und die Kennung der Sandbox angeben, in der der Vorgang ausgeführt werden soll. Dies sind optionale Parameter.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in Experience Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* Content-Type: `application/json`

## Schritt 3: Erstellen eines Aktivierungsflusses in der Platform-Benutzeroberfläche {#activation-flow}

Bevor Sie Segmente über die Ad-hoc-Aktivierungs-API aktivieren können, muss zunächst ein Aktivierungsfluss in der Platform-Benutzeroberfläche für das ausgewählte Ziel konfiguriert werden.

Dazu gehören der Einstieg in den Aktivierungs-Workflow, die Auswahl Ihrer Segmente, die Konfiguration eines Zeitplans und die Aktivierung dieser Segmente. Sie können die Benutzeroberfläche oder API verwenden, um einen Aktivierungsfluss zu erstellen:

* [Verwenden Sie die Platform-Benutzeroberfläche, um einen Aktivierungsfluss zu Batch-Profil-Exportzielen zu erstellen](../ui/activate-batch-profile-destinations.md)
* [Verwenden Sie die Flow Service-API, um eine Verbindung zu Batch-Profil-Exportzielen herzustellen und Daten zu aktivieren.](../api/connect-activate-batch-destinations.md)

## Schritt 4: Abrufen der neuesten Segmentexportauftrag-ID (in v2 nicht erforderlich) {#segment-export-id}

>[!IMPORTANT]
>
>In v2 der Ad-hoc-Aktivierungs-API müssen Sie nicht die neueste Segmentexportauftrag-ID abrufen. Sie können diesen Schritt überspringen und mit dem nächsten fortfahren.

Nachdem Sie einen Aktivierungsfluss für Ihr Batch-Ziel konfiguriert haben, werden geplante Segmentierungsaufträge automatisch alle 24 Stunden ausgeführt.

Bevor Sie den Ad-hoc-Aktivierungsauftrag ausführen können, müssen Sie die ID des aktuellen Segmentexportauftrags abrufen. Sie müssen diese ID in der Ad-hoc-Aktivierungsanfrage übergeben.

Befolgen Sie die beschriebenen Anweisungen. [here](../../segmentation/api/export-jobs.md#retrieve-list) , um eine Liste aller Segmentexportaufträge abzurufen.

Suchen Sie in der Antwort nach dem ersten Datensatz, der die unten stehende Schemaeigenschaft enthält.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

Die Segmentexportauftrag-ID befindet sich im `id` -Eigenschaft, wie unten dargestellt.

![Segmentexportauftrag-ID](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## Schritt 5: Ausführen des Ad-hoc-Aktivierungsauftrags {#activation-job}

Adobe Experience Platform führt geplante Segmentierungsaufträge einmal alle 24 Stunden aus. Die Ad-hoc-Aktivierungs-API wird basierend auf den neuesten Segmentierungsergebnissen ausgeführt.

Bevor Sie einen Ad-hoc-Aktivierungsauftrag ausführen, stellen Sie sicher, dass der geplante Segmentexportauftrag für Ihre Segmente abgeschlossen ist. Siehe [Ziel-Datenfluss-Überwachung](../../dataflows/ui/monitor-destinations.md) Informationen zur Überwachung des Status der Aktivierungsflüsse. Wenn Ihr Aktivierungsdataflow beispielsweise eine **[!UICONTROL Verarbeitung]** -Status, warten Sie, bis sie abgeschlossen ist, bevor Sie den Ad-hoc-Aktivierungsauftrag ausführen.

Nach Abschluss des Segmentexportauftrags können Sie die Aktivierung Trigger haben.

>[!NOTE]
>
>Derzeit kann jeder Ad-hoc-Aktivierungsauftrag bis zu 80 Segmente aktivieren. Der Versuch, mehr als 80 Segmente pro Auftrag zu aktivieren, führt dazu, dass der Auftrag fehlschlägt. Dieses Verhalten kann sich in zukünftigen Versionen ändern.

### Anfrage {#request}

>[!IMPORTANT]
>
>Es ist obligatorisch, die `Accept: application/vnd.adobe.adhoc.activation+json; version=2` -Kopfzeile in Ihrer Anfrage verwenden, um v2 der Ad-hoc-Aktivierungs-API zu verwenden.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun' \
--header 'x-gw-ims-org-id: 5555467B5D8013E50A494220@AdobeOrg' \
--header 'Authorization: Bearer {{token}}' \
--header 'x-sandbox-id: 6ef74723-3ee7-46a4-b747-233ee7a6a41a' \
--header 'x-sandbox-name: {sandbox-id}' \
--header 'Accept: application/vnd.adobe.adhoc.activation+json; version=2' \
--header 'Content-Type: application/json' \
--data-raw '{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   }
}'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Die IDs der Zielinstanzen, für die Sie Segmente aktivieren möchten. Sie können diese IDs über die Platform-Benutzeroberfläche abrufen, indem Sie zu **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** und auf die gewünschte Zielzeile klicken, um die Ziel-ID in der rechten Leiste anzuzeigen. Weitere Informationen finden Sie im Abschnitt [Dokumentation zum Zielarbeitsbereich](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | Die IDs der Segmente, die Sie für das ausgewählte Ziel aktivieren möchten. |

{style=&quot;table-layout:auto&quot;}

### Anfrage mit Export-IDs (nicht mehr unterstützt) {#request-deprecated}

>[!IMPORTANT]
>
>**Veralteter Anforderungstyp**. Dieser Beispieltyp beschreibt den Anfragetyp für die API-Version 1. In v2 der Ad-hoc-Aktivierungs-API müssen Sie nicht die neueste ID des Segmentexportauftrags angeben.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -d '
{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   },
   "exportIds":[
      "exportId1"
   ]
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Die IDs der Zielinstanzen, für die Sie Segmente aktivieren möchten. Sie können diese IDs über die Platform-Benutzeroberfläche abrufen, indem Sie zu **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** und auf die gewünschte Zielzeile klicken, um die Ziel-ID in der rechten Leiste anzuzeigen. Weitere Informationen finden Sie im Abschnitt [Dokumentation zum Zielarbeitsbereich](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | Die IDs der Segmente, die Sie für das ausgewählte Ziel aktivieren möchten. |
| <ul><li>`exportId1`</li></ul> | Die in der Antwort der [Segmentexport](../../segmentation/api/export-jobs.md#retrieve-list) Auftrag. Siehe [Schritt 4: Abrufen der neuesten Segmentexportauftrag-ID](#segment-export-id) für Anweisungen zum Auffinden dieser ID. |

{style=&quot;table-layout:auto&quot;}

### Antwort {#response}

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zurück.

```shell
{
   "order":[
      {
         "segment":"db8961e9-d52f-45bc-b3fb-76d0382a6851",
         "order":"ef2dcbd6-36fc-49a3-afed-d7b8e8f724eb",
         "statusURL":"https://platform.adobe.io/data/foundation/flowservice/runs/88d6da63-dc97-460e-b781-fc795a7386d9"
      }
   ]
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `segment` | Die ID des aktivierten Segments. |
| `order` | Die ID des Ziels, für das das Segment aktiviert wurde. |
| `statusURL` | Die Status-URL des Aktivierungsflusses. Sie können den Flussfortschritt mithilfe der [Flussdienst-API](../../sources/tutorials/api/monitor.md). |

{style=&quot;table-layout:auto&quot;}

## Umgang mit API-Fehlern {#api-error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

### API-Fehlercodes und -nachrichten, die für die Ad-hoc-Aktivierungs-API spezifisch sind {#specific-error-messages}

Bei Verwendung der Ad-hoc-Aktivierungs-API können Fehlermeldungen auftreten, die speziell für diesen API-Endpunkt gelten. Überprüfen Sie die Tabelle, um zu verstehen, wie Sie sie bearbeiten können, wenn sie angezeigt werden.

| Fehlermeldung | Auflösung |
|---------|----------|
| Bereits für ein Segment ausführen `segment ID` für die Bestellung `dataflow ID` mit Run-ID `flow run ID` | Diese Fehlermeldung weist darauf hin, dass derzeit ein Ad-hoc-Aktivierungsfluss für ein Segment ausgeführt wird. Warten Sie, bis der Auftrag abgeschlossen ist, bevor Sie den Aktivierungsauftrag erneut auslösen. |
| Segmente `<segment name>` sind nicht Teil dieses Datenflusses oder außerhalb des Zeitplanbereichs! | Diese Fehlermeldung weist darauf hin, dass die von Ihnen ausgewählten Segmente nicht dem Datenfluss zugeordnet sind oder dass der für die Segmente eingerichtete Aktivierungsplan entweder abgelaufen ist oder noch nicht gestartet wurde. Überprüfen Sie, ob das Segment tatsächlich dem Datenfluss zugeordnet ist, und stellen Sie sicher, dass sich der Zeitplan für die Segmentaktivierung mit dem aktuellen Datum überschneidet. |

## Verwandte Informationen {#related-information}

* [Verbinden mit Batch-Zielen und Aktivieren von Daten mit der Flow Service-API](/help/destinations/api/connect-activate-batch-destinations.md)