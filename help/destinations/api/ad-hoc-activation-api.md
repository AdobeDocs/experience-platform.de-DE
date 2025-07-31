---
keywords: Experience Platform;Ziel-API;Ad-hoc-Aktivierung;Zielgruppen-Ad-hoc aktivieren
solution: Experience Platform
title: Aktivieren von Zielgruppen für Batch-Ziele über die Ad-hoc-Aktivierungs-API
description: Dieser Artikel veranschaulicht den End-to-End-Workflow für die Aktivierung von Zielgruppen über die Ad-hoc-Aktivierungs-API, einschließlich der Segmentierungsaufträge, die vor der Aktivierung stattfinden.
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 8%

---

# Aktivieren von Zielgruppen bei Bedarf für Batch-Ziele über die Ad-hoc-Aktivierungs-API

>[!IMPORTANT]
>
>Nach Abschluss der Beta-Phase ist die [!DNL ad-hoc activation API] jetzt allgemein für alle Experience Platform-Kunden verfügbar (GA). In der GA-Version wurde die API auf Version 2 aktualisiert. Schritt 4 ([Abrufen der neuesten Zielgruppenexportvorgangs-](#segment-export-id)) ist nicht mehr erforderlich, da die API die Export-ID nicht mehr benötigt.
>
>Weitere Informationen finden [ in diesem Tutorial unter „Ausführen ](#activation-job) Ad-hoc-Aktivierungsauftrags“ weiter unten.

## Überblick {#overview}

Mit der Ad-hoc-Aktivierungs-API können Marketing-Experten Zielgruppen programmgesteuert und schnell für Ziele aktivieren, wenn eine sofortige Aktivierung erforderlich ist.

Verwenden Sie die Ad-hoc-Aktivierungs-API, um vollständige Dateien in Ihr gewünschtes Dateiempfangssystem zu exportieren. Die Ad-hoc-Zielgruppenaktivierung wird nur von [Batch-dateibasierten Zielen](../destination-types.md#file-based) unterstützt.

Die folgende Abbildung zeigt den kompletten Workflow zum Aktivieren von Zielgruppen über die Ad-hoc-Aktivierungs-API, einschließlich der Segmentierungsaufträge, die alle 24 Stunden in Experience Platform stattfinden.

![Ad-hoc-Aktivierung](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

## Anwendungsfälle {#use-cases}

### Flash-Verkäufe oder -Promotions

Ein Online-retailer bereitet einen begrenzten Flash-Verkauf vor und möchte die Kunden kurzfristig benachrichtigen. Über die Ad-hoc-Aktivierungs-API von Experience Platform kann das Marketing-Team Zielgruppen bei Bedarf exportieren und schnell Werbe-E-Mails an den Kundenstamm senden.

### Aktuelle Ereignisse oder aktuelle Nachrichten

Ein Hotel erwartet in den nächsten Tagen ungünstiges Wetter und das Team möchte die ankommenden Gäste schnell informieren, damit sie entsprechend planen können. Das Marketing-Team kann die Ad-hoc-Aktivierungs-API von Experience Platform verwenden, um Zielgruppen bei Bedarf zu exportieren und die Gäste zu benachrichtigen.

### Integrationstests

IT-Manager können die Ad-hoc-Aktivierungs-API von Experience Platform verwenden, um Zielgruppen bei Bedarf zu exportieren, sodass sie ihre benutzerdefinierte Integration mit Adobe Experience Platform testen und sicherstellen können, dass alles ordnungsgemäß funktioniert.

## Leitlinien {#guardrails}

Beachten Sie die folgenden Leitplanken bei der Verwendung der Ad-hoc-Aktivierungs-API.

* Derzeit kann jeder Ad-hoc-Aktivierungsauftrag bis zu 80 Zielgruppen aktivieren. Der Versuch, mehr als 80 Zielgruppen pro Auftrag zu aktivieren, führt zum Fehlschlagen des Auftrags. Dieses Verhalten kann sich in zukünftigen Versionen ändern.
* Ad-hoc-Aktivierungsaufträge können nicht parallel zu geplanten [Zielgruppen-Exportvorgängen](../../segmentation/api/export-jobs.md) ausgeführt werden. Stellen Sie vor dem Ausführen eines Ad-hoc-Aktivierungsauftrags sicher, dass der geplante Zielgruppen-Exportauftrag abgeschlossen wurde. Informationen [ Überwachen des Status ](../../dataflows/ui/monitor-destinations.md) Aktivierungsflüsse finden Sie unter „Ziel-Datenflussüberwachung“. Wenn Ihr Aktivierungsdatenfluss beispielsweise den Status **[!UICONTROL Verarbeitung läuft]** aufweist, warten Sie, bis er abgeschlossen ist, bevor Sie den Ad-hoc-Aktivierungsauftrag ausführen.
* Führen Sie nicht mehr als einen gleichzeitigen Ad-hoc-Aktivierungsauftrag pro Zielgruppe aus.

## Überlegungen zur Segmentierung {#segmentation-considerations}

Adobe Experience Platform führt geplante Segmentierungsaufträge alle 24 Stunden aus. Die Ad-hoc-Aktivierungs-API wird auf der Grundlage der neuesten Segmentierungsergebnisse ausgeführt.

## Schritt 1: Voraussetzungen {#prerequisites}

Bevor Sie die Adobe Experience Platform-APIs aufrufen können, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

* Sie haben ein Organisationskonto mit Zugriff auf Adobe Experience Platform.
* Für Ihr Experience Platform-Konto sind die Rollen `developer` und `user` für das Adobe Experience Platform-API-Produktprofil aktiviert. Wenden Sie sich an Ihren [Admin Console](../../access-control/home.md)-Administrator, um diese Rollen für Ihr Konto zu aktivieren.
* Sie haben eine Adobe ID. Wenn Sie keine Adobe ID haben, gehen Sie zur [Adobe Developer Console](https://developer.adobe.com/console) und erstellen Sie ein neues Konto.

## Schritt 2: Sammeln von Anmeldeinformationen {#credentials}

Um Experience Platform-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Ressourcen in Experience Platform lassen sich in spezifischen virtuellen Sandboxes isolieren. Bei Anfragen an Experience Platform-APIs können Sie den Namen und die ID der Sandbox angeben, in der der Vorgang ausgeführt werden soll. Dies sind optionale Parameter.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in Experience Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* Content-Type: `application/json`

## Schritt 3: Erstellen eines Aktivierungsflusses in der Experience Platform-Benutzeroberfläche {#activation-flow}

Bevor Sie Zielgruppen über die Ad-hoc-Aktivierungs-API aktivieren können, muss zunächst in der Experience Platform-Benutzeroberfläche ein Aktivierungsfluss für das ausgewählte Ziel konfiguriert worden sein.

Dazu gehören der Einstieg in den Aktivierungs-Workflow, die Auswahl Ihrer Zielgruppen, die Konfiguration eines Zeitplans und die Aktivierung. Sie können die Benutzeroberfläche oder API verwenden, um einen Aktivierungsfluss zu erstellen:

* [Verwenden der Experience Platform-Benutzeroberfläche zum Erstellen eines Aktivierungsflusses zu Batch-Profil-Exportzielen](../ui/activate-batch-profile-destinations.md)
* [Verwenden Sie die Flow Service-API, um eine Verbindung zu Batch-Profil-Exportzielen herzustellen und Daten zu aktivieren](../api/connect-activate-batch-destinations.md)

## Schritt 4: Abrufen der neuesten Zielgruppen-Exportvorgangs-ID (in Version 2 nicht erforderlich) {#segment-export-id}

>[!IMPORTANT]
>
>In der v2 der Ad-hoc-Aktivierungs-API müssen Sie nicht die neueste Zielgruppen-Exportvorgangs-ID abrufen. Sie können diesen Schritt überspringen und mit dem nächsten fortfahren.

Nachdem Sie einen Aktivierungsfluss für Ihr Batch-Ziel konfiguriert haben, werden geplante Segmentierungsaufträge automatisch alle 24 Stunden ausgeführt.

Bevor Sie den Ad-hoc-Aktivierungsauftrag ausführen können, müssen Sie die ID des neuesten Zielgruppen-Exportauftrags abrufen. Sie müssen diese ID in der Ad-hoc-Aktivierungsanfrage übergeben.

Befolgen Sie die [hier](../../segmentation/api/export-jobs.md#retrieve-list) beschriebenen Anweisungen, um eine Liste aller Zielgruppenexportvorgänge abzurufen.

Suchen Sie in der Antwort nach dem ersten Datensatz, der die folgende Schemaeigenschaft enthält.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

Die Auftrags-ID des Zielgruppenexports befindet sich in der `id`-Eigenschaft, wie unten dargestellt.

![Zielgruppenexportvorgangs-ID](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## Schritt 5: Ad-hoc-Aktivierungsauftrag ausführen {#activation-job}

Adobe Experience Platform führt geplante Segmentierungsaufträge alle 24 Stunden aus. Die Ad-hoc-Aktivierungs-API wird auf der Grundlage der neuesten Segmentierungsergebnisse ausgeführt.

>[!IMPORTANT]
>
>Beachten Sie die folgende einmalige Einschränkung: Stellen Sie vor der Ausführung eines Ad-hoc-Aktivierungsauftrags sicher, dass seit dem Zeitpunkt, zu dem die Zielgruppe zum ersten Mal gemäß dem Zeitplan aktiviert wurde, mindestens eine Stunde vergangen ist ([ 3. Schritt - Aktivierungsfluss erstellen in der Experience Platform-Benutzeroberfläche](#activation-flow).

Stellen Sie vor der Ausführung eines Ad-hoc-Aktivierungsauftrags sicher, dass der geplante Zielgruppenexportauftrag für Ihre Zielgruppen abgeschlossen ist. Informationen [ Überwachen des Status ](../../dataflows/ui/monitor-destinations.md) Aktivierungsflüsse finden Sie unter „Ziel-Datenflussüberwachung“. Wenn Ihr Aktivierungsdatenfluss beispielsweise den Status **[!UICONTROL Verarbeitung läuft]** aufweist, warten Sie, bis er abgeschlossen ist, bevor Sie den Ad-hoc-Aktivierungsauftrag ausführen, um eine vollständige Datei zu exportieren.

Nachdem der Zielgruppenexport abgeschlossen ist, können Sie einen Trigger für die Aktivierung erstellen.

>[!NOTE]
>
>Derzeit kann jeder Ad-hoc-Aktivierungsauftrag bis zu 80 Zielgruppen aktivieren. Der Versuch, mehr als 80 Zielgruppen pro Auftrag zu aktivieren, führt zum Fehlschlagen des Auftrags. Dieses Verhalten kann sich in zukünftigen Versionen ändern.

### Anfrage {#request}

>[!IMPORTANT]
>
>Um v2 der Ad-hoc-Aktivierungs-API verwenden zu können, müssen Sie in Ihrer Anfrage den `Accept: application/vnd.adobe.adhoc.activation+json; version=2`-Header einfügen.

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Die IDs der Zielinstanzen, für die Sie Zielgruppen aktivieren möchten. Sie können diese IDs über die Experience Platform-Benutzeroberfläche abrufen, indem Sie zur Registerkarte **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** navigieren und auf die gewünschte Zielzeile klicken, um die Ziel-ID in der rechten Leiste aufzurufen. Weitere Informationen finden Sie in der [Dokumentation zum Arbeitsbereich „Ziele](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | Die IDs der Zielgruppen, die Sie für das ausgewählte Ziel aktivieren möchten. Mit der Ad-hoc-API können Sie Experience Platform-generierte Zielgruppen sowie externe (benutzerdefinierte Upload-)Zielgruppen exportieren. Verwenden Sie beim Aktivieren externer Zielgruppen die systemgenerierte ID anstelle der Zielgruppen-ID. Die systemgenerierte ID finden Sie in der Ansicht „Zielgruppenzusammenfassung“ in der Benutzeroberfläche „Zielgruppen“. <br> ![Ansicht der Zielgruppen-ID, die nicht ausgewählt werden soll.](/help/destinations/assets/api/ad-hoc-activation/audience-id-do-not-use.png "Ansicht der Zielgruppen-ID, die nicht ausgewählt werden soll."){width="100" zoomable="yes"} <br> ![Ansicht der systemgenerierten Zielgruppen-ID, die verwendet werden soll.](/help/destinations/assets/api/ad-hoc-activation/system-generated-id-to-use.png "Ansicht der systemgenerierten Zielgruppen-ID, die verwendet werden soll."){width="100" zoomable="yes"} |

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Die IDs der Zielinstanzen, für die Sie Zielgruppen aktivieren möchten. Sie können diese IDs über die Experience Platform-Benutzeroberfläche abrufen, indem Sie zur Registerkarte **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** navigieren und auf die gewünschte Zielzeile klicken, um die Ziel-ID in der rechten Leiste aufzurufen. Weitere Informationen finden Sie in der [Dokumentation zum Arbeitsbereich „Ziele](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | Die IDs der Zielgruppen, die Sie für das ausgewählte Ziel aktivieren möchten. |
| <ul><li>`exportId1`</li></ul> | Die ID, die in der Antwort des [Zielgruppenexport“-](../../segmentation/api/export-jobs.md#retrieve-list) zurückgegeben wird. Unter [Schritt 4: Abrufen der neuesten Zielgruppen-Exportvorgangs-](#segment-export-id)) finden Sie Anweisungen, wie Sie diese ID finden. |

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
| `segment` | Die ID der aktivierten Zielgruppe. |
| `order` | Die ID des Ziels, für das die Zielgruppe aktiviert wurde. |
| `statusURL` | Die Status-URL des Aktivierungsflusses. Sie können den Flussfortschritt mithilfe der [Flow Service-API) ](../../sources/tutorials/api/monitor.md). |

{style="table-layout:auto"}

## Umgang mit API-Fehlern {#api-error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status](../../landing/troubleshooting.md#api-status-codes)Codes und [Fehler in der Anfragekopfzeile](../../landing/troubleshooting.md#request-header-errors) im Handbuch zur Fehlerbehebung bei Experience Platform.

### API-Fehler-Codes und Meldungen, die spezifisch für die Ad-hoc-Aktivierungs-API sind {#specific-error-messages}

Bei Verwendung der Ad-hoc-Aktivierungs-API können Sie auf Fehlermeldungen stoßen, die für diesen API-Endpunkt spezifisch sind. Überprüfen Sie die Tabelle, um zu verstehen, wie Sie darauf reagieren, wenn sie angezeigt werden.

| Fehlermeldung | Auflösung |
|---------|----------|
| Ausführung läuft bereits für Zielgruppen-`segment ID` für `dataflow ID` mit Ausführungs-ID `flow run ID` | Diese Fehlermeldung weist darauf hin, dass derzeit ein Ad-hoc-Aktivierungsfluss für eine Zielgruppe läuft. Warten Sie, bis der Vorgang abgeschlossen ist, bevor Sie den Aktivierungsvorgang erneut auslösen. |
| Segmente `<segment name>` sind nicht Teil dieses Datenflusses oder außerhalb des Zeitplanbereichs! | Diese Fehlermeldung zeigt an, dass die Zielgruppen, die Sie aktivieren möchten, nicht dem Datenfluss zugeordnet sind oder dass der für die Zielgruppen eingerichtete Aktivierungsplan entweder abgelaufen oder noch nicht gestartet wurde. Überprüfen Sie, ob die Zielgruppe tatsächlich dem Datenfluss zugeordnet ist, und stellen Sie sicher, dass sich der Zeitplan für die Zielgruppenaktivierung mit dem aktuellen Datum überschneidet. |

## Verwandte Informationen {#related-information}

* [Verbinden mit Batch-Zielen und Aktivieren von Daten mit der Flow Service-API](/help/destinations/api/connect-activate-batch-destinations.md)
* [(Beta) Exportieren von Dateien nach Bedarf in Batch-Ziele mithilfe der Experience Platform-Benutzeroberfläche](/help/destinations/ui/export-file-now.md)