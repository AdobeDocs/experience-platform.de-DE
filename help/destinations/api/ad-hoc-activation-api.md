---
keywords: Experience Platform; Ziel-API; Ad-hoc-Aktivierung; Ad-hoc-Aktivierung von Zielgruppen aktivieren
solution: Experience Platform
title: Aktivieren von Zielgruppen für Batch-Ziele über die Ad-hoc-Aktivierungs-API
description: Dieser Artikel veranschaulicht den durchgängigen Arbeitsablauf zum Aktivieren von Zielgruppen über die Ad-hoc-Aktivierungs-API, einschließlich der Segmentierungsaufträge, die vor der Aktivierung ausgeführt werden.
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: deecaf0af269b64af507126dba0523d2b16a5721
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 12%

---

# Aktivieren von Zielgruppen bei Bedarf für Batch-Ziele über die Ad-hoc-Aktivierungs-API

>[!IMPORTANT]
>
>Nach Abschluss der Beta-Phase ist der [!DNL ad-hoc activation API] jetzt allgemein für alle Experience Platform-Kunden verfügbar (GA). In der GA-Version wurde die API auf Version 2 aktualisiert. Schritt 4 ([Abrufen der neuesten ID des Zielgruppenexportauftrags](#segment-export-id)) ist nicht mehr erforderlich, da die API die Export-ID nicht mehr benötigt.
>
>Weitere Informationen finden Sie unter [Ausführen des Ad-hoc-Aktivierungsauftrags](#activation-job) weiter unten in diesem Tutorial.

## Übersicht {#overview}

Mit der Ad-hoc-Aktivierungs-API können Marketing-Experten Zielgruppen für Ziele programmgesteuert schnell und effizient für Situationen aktivieren, in denen eine sofortige Aktivierung erforderlich ist.

Verwenden Sie die Ad-hoc-Aktivierungs-API, um vollständige Dateien in Ihr gewünschtes Dateiempfangssystem zu exportieren. Die Aktivierung der Ad-hoc-Zielgruppe wird nur von [dateibasierten Batch-Zielen](../destination-types.md#file-based) unterstützt.

Das folgende Diagramm zeigt den durchgängigen Arbeitsablauf zum Aktivieren von Zielgruppen über die Ad-hoc-Aktivierungs-API, einschließlich der Segmentierungsaufträge, die alle 24 Stunden in Platform stattfinden.

![Ad-hoc-Aktivierung](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)



## Anwendungsfälle {#use-cases}

### Flash Vertrieb oder Verkaufsförderung

Ein Online-Händler bereitet einen begrenzten Flash-Verkauf vor und möchte Kunden kurzfristig benachrichtigen. Über die Ad-hoc-Aktivierungs-API von Experience Platform kann das Marketing-Team Zielgruppen bei Bedarf exportieren und Werbe-E-Mails schnell an die Kundenbasis senden.

### Aktuelle Veranstaltungen oder aktuelle Nachrichten

Ein Hotel erwartet ein schlechtes Wetter an den folgenden Tagen, und das Team möchte die ankommenden Gäste schnell informieren, damit sie entsprechend planen können. Das Marketing-Team kann die Ad-hoc-Aktivierungs-API von Experience Platform verwenden, um Zielgruppen bei Bedarf zu exportieren und die Gäste zu benachrichtigen.

### Integrationstests

IT-Manager können die Experience Platform Ad-hoc-Aktivierungs-API verwenden, um Zielgruppen bei Bedarf zu exportieren, sodass sie ihre benutzerdefinierte Integration mit Adobe Experience Platform testen und sicherstellen können, dass alles ordnungsgemäß funktioniert.

## Leitplanken {#guardrails}

Beachten Sie bei der Verwendung der Ad-hoc-Aktivierungs-API die folgenden Limits.

* Derzeit kann jeder Ad-hoc-Aktivierungsauftrag bis zu 80 Zielgruppen aktivieren. Der Versuch, mehr als 80 Zielgruppen pro Auftrag zu aktivieren, führt dazu, dass der Auftrag fehlschlägt. Dieses Verhalten kann sich in zukünftigen Versionen ändern.
* Ad-hoc-Aktivierungsaufträge können nicht parallel zu geplanten [Zielgruppen-Exportaufträgen](../../segmentation/api/export-jobs.md) ausgeführt werden. Bevor Sie einen Ad-hoc-Aktivierungsauftrag ausführen, stellen Sie sicher, dass der geplante Zielgruppenexport-Auftrag abgeschlossen ist. Informationen zum Überwachen des Status von Aktivierungsflüssen finden Sie unter [Überwachung des Ziel-Datenflusses](../../dataflows/ui/monitor-destinations.md) . Wenn Ihr Aktivierungs-Datenfluss beispielsweise den Status **[!UICONTROL Verarbeitung]** aufweist, warten Sie, bis er abgeschlossen ist, bevor Sie den Ad-hoc-Aktivierungsauftrag ausführen.
* Führen Sie nicht mehr als einen gleichzeitigen Ad-hoc-Aktivierungsauftrag pro Zielgruppe aus.

## Überlegungen zur Segmentierung {#segmentation-considerations}

Adobe Experience Platform führt geplante Segmentierungsaufträge einmal alle 24 Stunden aus. Die Ad-hoc-Aktivierungs-API wird basierend auf den neuesten Segmentierungsergebnissen ausgeführt.

## Schritt 1: Voraussetzungen {#prerequisites}

Bevor Sie die Adobe Experience Platform-APIs aufrufen können, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

* Sie haben ein Organisationskonto mit Zugriff auf Adobe Experience Platform.
* Für Ihr Experience Platform-Konto sind die Rollen `developer` und `user` für das Adobe Experience Platform API-Produktprofil aktiviert. Wenden Sie sich an Ihren Administrator von [Admin Console](../../access-control/home.md) , um diese Rollen für Ihr Konto zu aktivieren.
* Du hast einen Adobe ID. Wenn Sie keine Adobe ID haben, wechseln Sie zum Ordner [Adobe Developer Console](https://developer.adobe.com/console) und erstellen Sie ein neues Konto.

## Schritt 2: Anmeldeinformationen sammeln {#credentials}

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

## Schritt 3: Aktivierungsfluss in der Platform-Benutzeroberfläche erstellen {#activation-flow}

Bevor Sie Zielgruppen über die Ad-hoc-Aktivierungs-API aktivieren können, muss zunächst ein Aktivierungsfluss in der Platform-Benutzeroberfläche für das ausgewählte Ziel konfiguriert werden.

Dazu gehören der Einstieg in den Aktivierungs-Workflow, die Auswahl Ihrer Zielgruppen, die Konfiguration eines Zeitplans und die Aktivierung dieser Zielgruppen. Sie können die Benutzeroberfläche oder API verwenden, um einen Aktivierungsfluss zu erstellen:

* [Verwenden Sie die Platform-Benutzeroberfläche, um einen Aktivierungsfluss zu Batch-Profil-Exportzielen zu erstellen](../ui/activate-batch-profile-destinations.md)
* [Verwenden Sie die Flow Service-API, um eine Verbindung zu Batch-Profil-Exportzielen herzustellen und Daten zu aktivieren](../api/connect-activate-batch-destinations.md)

## Schritt 4: Abrufen der neuesten Auftrags-ID für den Zielgruppenexport (in v2 nicht erforderlich) {#segment-export-id}

>[!IMPORTANT]
>
>In v2 der Ad-hoc-Aktivierungs-API müssen Sie nicht die neueste ID des Zielgruppenexportauftrags abrufen. Sie können diesen Schritt überspringen und mit dem nächsten fortfahren.

Nachdem Sie einen Aktivierungsfluss für Ihr Batch-Ziel konfiguriert haben, werden geplante Segmentierungsaufträge automatisch alle 24 Stunden ausgeführt.

Bevor Sie den Ad-hoc-Aktivierungsauftrag ausführen können, müssen Sie die Kennung des aktuellen Zielgruppenexportauftrags abrufen. Sie müssen diese ID in der Ad-hoc-Aktivierungsanfrage übergeben.

Befolgen Sie die Anweisungen, die [hier](../../segmentation/api/export-jobs.md#retrieve-list) beschrieben sind, um eine Liste aller Zielgruppenexport-Aufträge abzurufen.

Suchen Sie in der Antwort nach dem ersten Datensatz, der die unten stehende Schemaeigenschaft enthält.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

Die Auftrags-ID des Zielgruppenexports befindet sich in der Eigenschaft `id` , wie unten dargestellt.

![Kennung des Audience-Exportauftrags](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## Schritt 5: Ad-hoc-Aktivierungsauftrag ausführen {#activation-job}

Adobe Experience Platform führt geplante Segmentierungsaufträge einmal alle 24 Stunden aus. Die Ad-hoc-Aktivierungs-API wird basierend auf den neuesten Segmentierungsergebnissen ausgeführt.

>[!IMPORTANT]
>
>Beachten Sie die folgende einmalige Einschränkung: Bevor Sie einen Ad-hoc-Aktivierungsauftrag ausführen, stellen Sie sicher, dass mindestens 20 Minuten nach dem Zeitpunkt vergangen sind, zu dem die Zielgruppe erstmals gemäß dem Zeitplan aktiviert wurde, den Sie in [Schritt 3 - Erstellen des Aktivierungsflusses in der Platform-Benutzeroberfläche](#activation-flow) festgelegt haben.

Bevor Sie einen Ad-hoc-Aktivierungsauftrag ausführen, stellen Sie sicher, dass der geplante Zielgruppenexport-Auftrag für Ihre Zielgruppen abgeschlossen ist. Informationen zum Überwachen des Status von Aktivierungsflüssen finden Sie unter [Überwachung des Ziel-Datenflusses](../../dataflows/ui/monitor-destinations.md) . Wenn Ihr Aktivierungsdataflow beispielsweise den Status **[!UICONTROL Verarbeitung]** aufweist, warten Sie, bis er abgeschlossen ist, bevor Sie den Ad-hoc-Aktivierungsauftrag ausführen, um eine vollständige Datei zu exportieren.

Nach Abschluss des Zielgruppenexportvorgangs kann die Aktivierung Trigger werden.

>[!NOTE]
>
>Derzeit kann jeder Ad-hoc-Aktivierungsauftrag bis zu 80 Zielgruppen aktivieren. Der Versuch, mehr als 80 Zielgruppen pro Auftrag zu aktivieren, führt dazu, dass der Auftrag fehlschlägt. Dieses Verhalten kann sich in zukünftigen Versionen ändern.

### Anfrage {#request}

>[!IMPORTANT]
>
>Es ist erforderlich, die Kopfzeile `Accept: application/vnd.adobe.adhoc.activation+json; version=2` in Ihre Anfrage aufzunehmen, um v2 der Ad-hoc-Aktivierungs-API zu verwenden.

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Die IDs der Zielinstanzen, für die Sie Zielgruppen aktivieren möchten. Sie können diese IDs über die Platform-Benutzeroberfläche abrufen, indem Sie zur Registerkarte **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** navigieren und auf die gewünschte Zielzeile klicken, um die Ziel-ID in der rechten Leiste anzuzeigen. Weitere Informationen finden Sie in der Dokumentation zum Arbeitsbereich [Ziele](/help/destinations/ui/destinations-workspace.md#browse) . |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | Die IDs der Zielgruppen, die Sie für das ausgewählte Ziel aktivieren möchten. Sie können die Ad-hoc-API verwenden, um Platform-generierte Zielgruppen sowie externe (benutzerdefinierte Upload-Zielgruppen) zu exportieren. Verwenden Sie beim Aktivieren externer Zielgruppen die systemgenerierte ID anstelle der Zielgruppen-ID. Die systemgenerierte ID finden Sie in der Zusammenfassungsansicht der Zielgruppe in der Benutzeroberfläche für Zielgruppen <br> . ![Ansicht der Zielgruppen-ID, die nicht ausgewählt werden sollte.](/help/destinations/assets/api/ad-hoc-activation/audience-id-do-not-use.png "Ansicht der Zielgruppen-ID, die nicht ausgewählt werden soll."){width="100" zoomable="yes"} <br> ![Ansicht der systemgenerierten Zielgruppen-ID, die verwendet werden soll.](/help/destinations/assets/api/ad-hoc-activation/system-generated-id-to-use.png "Ansicht der systemgenerierten Zielgruppen-ID, die verwendet werden soll."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

### Anfrage mit Export-IDs {#request-export-ids}

<!--

>[!IMPORTANT]
>
>**Deprecated request type**. This example type describes the request type for the API version 1. In the v2 of the ad-hoc activation API, you do not need to include the latest audience export job ID.

-->

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Die IDs der Zielinstanzen, für die Sie Zielgruppen aktivieren möchten. Sie können diese IDs über die Platform-Benutzeroberfläche abrufen, indem Sie zur Registerkarte **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** navigieren und auf die gewünschte Zielzeile klicken, um die Ziel-ID in der rechten Leiste anzuzeigen. Weitere Informationen finden Sie in der Dokumentation zum Arbeitsbereich [Ziele](/help/destinations/ui/destinations-workspace.md#browse) . |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | Die IDs der Zielgruppen, die Sie für das ausgewählte Ziel aktivieren möchten. |
| <ul><li>`exportId1`</li></ul> | Die in der Antwort des [Audience export](../../segmentation/api/export-jobs.md#retrieve-list) -Auftrags zurückgegebene ID. Anweisungen zum Auffinden dieser ID finden Sie unter [Schritt 4: Abrufen der neuesten ID des Zielgruppenexportauftrags](#segment-export-id) . |

{style="table-layout:auto"}

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
| `segment` | Die ID der aktivierten Audience. |
| `order` | Die ID des Ziels, für das die Zielgruppe aktiviert wurde. |
| `statusURL` | Die Status-URL des Aktivierungsflusses. Sie können den Fluss-Fortschritt mithilfe der [Flow Service API](../../sources/tutorials/api/monitor.md) verfolgen. |

{style="table-layout:auto"}

## Umgang mit API-Fehlern {#api-error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

### API-Fehlercodes und -nachrichten, die für die Ad-hoc-Aktivierungs-API spezifisch sind {#specific-error-messages}

Bei Verwendung der Ad-hoc-Aktivierungs-API können Fehlermeldungen auftreten, die speziell für diesen API-Endpunkt gelten. Überprüfen Sie die Tabelle, um zu verstehen, wie Sie sie bearbeiten können, wenn sie angezeigt werden.

| Fehlermeldung | Auflösung |
|---------|----------|
| Führen Sie bereits für die Zielgruppe `segment ID` für die Bestellung `dataflow ID` mit der Ausführungskennung `flow run ID` aus. | Diese Fehlermeldung weist darauf hin, dass derzeit ein Ad-hoc-Aktivierungsfluss für eine Zielgruppe ausgeführt wird. Warten Sie, bis der Auftrag abgeschlossen ist, bevor Sie den Aktivierungsauftrag erneut auslösen. |
| Segmente `<segment name>` sind nicht Teil dieses Datenflusses oder außerhalb des Zeitplanbereichs! | Diese Fehlermeldung weist darauf hin, dass die von Ihnen ausgewählten Zielgruppen nicht dem Datenfluss zugeordnet sind oder dass der für die Zielgruppen eingerichtete Aktivierungsplan entweder abgelaufen ist oder noch nicht gestartet wurde. Überprüfen Sie, ob die Audience tatsächlich dem Datenfluss zugeordnet ist, und stellen Sie sicher, dass sich der Aktivierungszeitplan für die Zielgruppe mit dem aktuellen Datum überschneidet. |

## Verwandte Informationen {#related-information}

* [Verbinden mit Batch-Zielen und Aktivieren von Daten mit der Flow Service-API](/help/destinations/api/connect-activate-batch-destinations.md)
* [(Beta) Exportieren von Dateien nach Bedarf in Batch-Ziele mithilfe der Experience Platform-Benutzeroberfläche](/help/destinations/ui/export-file-now.md)