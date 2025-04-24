---
title: Datenerfassung – Übersicht
description: In diesem Dokument werden die drei Hauptwege für die Aufnahme von Daten in Experience Platform mit Links zu den jeweiligen Übersichtsdokumenten vorgestellt, in denen Sie weitere Informationen finden.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: 0e484dffa38d454561f9d67c6bea92f426d3515d
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 14%

---

# Datenerfassung – Übersicht

In Adobe Experience Platform bezeichnet Datenaufnahme den Transport von Daten aus verschiedenen Quellen zu einem Speichermedium, auf das Unternehmen zugreifen und die Daten dort verwenden sowie analysieren können. Die Datenaufnahme in Experience Platform kann in zwei Hauptkategorien unterteilt werden: **Streaming-Aufnahme** und **Batch-Aufnahme**.

Unter Streaming und Batch-Aufnahme gibt es eine Reihe verschiedener Methoden, mit denen Sie Ihre Daten in Experience Platform aufnehmen können. Zu diesen Methoden gehören die Verwendung einer Vielzahl von **Quellen** und das Herstellen einer Verbindung zu diesen Quellen, um dann Daten in Experience Platform zu importieren.

In diesem Dokument erhalten Sie einen Überblick über die vielen verschiedenen Möglichkeiten, wie Daten in Experience Platform aufgenommen werden können.

<!-- Adobe Experience Platform brings data from multiple sources together in order to help marketers better understand the behavior of their customers. Adobe Experience Platform Data Ingestion represents the multiple methods by which Experience Platform ingests data from these sources, as well as how that data is persisted within the Data Lake for use by downstream Experience Platform services. -->

## Streaming-Aufnahme {#streaming}

Sie können die Streaming-Aufnahme verwenden, um Daten von Client- und Server-seitigen Geräten in Echtzeit an Experience Platform zu senden. Experience Platform unterstützt die Verwendung von Daten-Inlets zum Streamen eingehender Erlebnisdaten, die in Streaming-fähigen Datensätzen im Data Lake beibehalten werden. Daten-Inlets können so konfiguriert werden, dass die von ihnen erfassten Daten automatisch authentifiziert werden, sodass sichergestellt ist, dass die Daten von einer vertrauenswürdigen Quelle stammen.

Weitere Informationen finden Sie unter [Streaming-Aufnahme - Übersicht](./streaming-ingestion/overview.md).

## Batch-Erfassung {#batch}

In Experience Platform ist ein Batch ein Satz von Daten, die über einen bestimmten Zeitraum gesammelt und als eine Einheit verarbeitet werden. Datensätze bestehen aus Batches. Sie können die Batch-Aufnahme verwenden, um Daten als Batch-Dateien in Experience Platform aufzunehmen. Nach der Erfassung stellen Batches Metadaten bereit, die die Anzahl der erfolgreich erfassten Datensätze sowie alle fehlgeschlagenen Datensätze und zugehörigen Fehlermeldungen beschreiben.

Manuell hochgeladene Datendateien wie CSV-Flatfiles (die XDM-Schemata zugeordnet sind) und Parquet-Dateien müssen mit dieser Methode aufgenommen werden.

Weitere Informationen finden Sie unter [Übersicht über die Batch-Aufnahme](./batch-ingestion/overview.md).

## Quellen {#sources}

Sie können auch Daten aufnehmen, indem Sie eine Verbindung zu Experience Platform-Quellen herstellen. Experience Platform verwaltet einen Katalog mit einer Vielzahl verschiedener Datenquellen, mit denen Sie eine Verbindung herstellen und aus denen Sie Daten aufnehmen können. Bei diesen Quellen kann es sich um native Adobe-Programme wie die Adobe Analytics- oder die Marketo Engage-Quelle handeln. Sie können auch eine Verbindung zu Quellen von Drittanbietern herstellen, z. B. zur [!DNL Amazon S3] und zur [!DNL Google Cloud Storage].

Quellen sind in verschiedene Kategorien wie Cloud-Speicher, Datenbanken und CRM-Systeme unterteilt. Eine bestimmte Quelle unterstützt möglicherweise die Batch- oder Streaming-Aufnahme.

Mit -Quellen können Sie Daten aus einer Reihe verschiedener Datenquellen und von verschiedenen Anwendungsfallkategorien aufnehmen. Darüber hinaus bietet Ihnen die Datenaufnahme über eine Quelle die Möglichkeit, sich bei der externen Datenquelle zu authentifizieren, einen Aufnahmezeitplan zu konfigurieren und den Aufnahmedurchsatz zu verwalten.

Weitere Informationen finden Sie im Abschnitt [Quellen - Übersicht](../sources/home.md).

### ML-unterstützte Schemaerstellung {#ml-assisted-schema-creation}

Um neue Datenquellen schnell zu integrieren, können Sie jetzt maschinelle Lernalgorithmen verwenden, um ein Schema aus Beispieldaten zu generieren. Diese Automatisierung vereinfacht die Erstellung genauer Schemata, reduziert Fehler und beschleunigt den Prozess von der Datenerfassung bis hin zur Analyse und Erkenntnissen.

Weitere Informationen zu [ Workflow finden Sie ](../xdm/ui/ml-assisted-schema-creation.md) Handbuch zur Erstellung XML-unterstützter Schemata .

## Datenvorbereitung {#data-prep}

Die Datenvorbereitung ist zwar keine Methode zur Aufnahme, aber sie ist ein wichtiger Teil des Datenerfassungsprozesses. Verwenden Sie Datenvorbereitungsfunktionen, um Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren, bevor Sie einen Datenfluss erstellen, um Ihre Daten in Experience Platform aufzunehmen. Die Datenvorbereitung wird während der Datenaufnahme in der Benutzeroberfläche von Experience Platform als Schritt „Zuordnung“ angezeigt.

Weitere Informationen finden Sie unter [Datenvorbereitung - Übersicht](../data-prep/home.md).

## Streaming-Erfassungsmethoden {#streaming-ingestion-methods}

In der folgenden Tabelle sind die verschiedenen Methoden aufgeführt, mit denen Sie Streaming-Daten in Experience Platform aufnehmen können.

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1123px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:31px; vertical-align:top; width:1123px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">Streaming-Quellen</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Methode</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:401px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Häufige Anwendungsfälle</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Protokolle</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:282px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Zu beachten</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=de" style="color:#0563c1; text-decoration:underline">Adobe Web/Mobile SDK</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Datenerfassung von Websites und mobilen Apps.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Bevorzugte Methode für Client-seitige Erfassung.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, HTTP, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Implementieren Sie mithilfe einer einzigen SDK mehrere Adobe-Anwendungen.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/streaming/http" style="color:#0563c1; text-decoration:underline">HTTP-API-Connector</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Erfassung aus Streaming-Quellen, Transaktionen, relevanten Kundenereignissen und Signalen.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, REST-API, JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Rohe oder XDM-Daten werden direkt an den Hub gestreamt, ohne Echtzeit-Edge-Segmentierung oder Ereignisweiterleitung.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/data-collection/interactive-data-collection.html?lang=en" style="color:#0563c1; text-decoration:underline">[!DNL Edge Network] API</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Erfassung aus Streaming-Quellen, Transaktionen, relevanten Kundenereignissen und Signalen der global verteilten [!DNL Edge Network].</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, REST-API, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Daten werden über die [!DNL Edge Network] gestreamt. Unterstützung für die Echtzeit-Segmentierung und Ereignisweiterleitung auf der Edge. </span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en" style="color:#0563c1; text-decoration:underline">Adobe-Anwendungen</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Datenaufnahme aus Programmen wie Adobe Analytics, Marketo Engage, Adobe Campaign Managed Services, Adobe Target, Adobe Audience Manager</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, Source-Connectoren und API</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Es wird empfohlen, zum Web/Mobile SDK zu migrieren, anstatt herkömmliche Anwendungs-SDKs zu verwenden.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=en" style="color:#0563c1; text-decoration:underline">Streaming-Quellen</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Aufnahme eines Unternehmens-Ereignis-Streams, der normalerweise zum Freigeben von Unternehmensdaten an mehrere nachgelagerte Anwendungen verwendet wird. </span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, REST-API, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Daten werden im JSON-Format gestreamt und können dem XDM-Schema zugeordnet werden.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/en/docs/experience-platform/sources/sdk/streaming-sdk/getting-started" style="color:#0563c1; text-decoration:underline">Streaming-Quellen - SDK</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Verwenden Sie die Self-Service-Funktionen von Self-Service Sources Streaming SDK , um Ihre eigene Datenquelle in den Experience Platform-Quellkatalog zu integrieren.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, HTTP-API, JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Beispiele für Partner-integrierte Streaming-Quellen sind: Braze, Pendo und RainFocus.</span></span></span></li>
</ul>
</td>
</tr>
</tbody>
</table>

## Batch-Erfassungsmethoden {#batch-ingestion-methods}

In der folgenden Tabelle sind die verschiedenen Methoden aufgeführt, mit denen Sie Batch-Daten in Experience Platform aufnehmen können.

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1105px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:37px; vertical-align:top; width:1105px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">Batch-Quellen</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Methode</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:397px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Häufige Anwendungsfälle</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Protokolle</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:277px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Zu beachten</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/batch/overview" style="color:#0563c1; text-decoration:underline">Batch-Aufnahme-API</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Aufnahme aus einer vom Unternehmen verwalteten Warteschlange. Verwenden Sie die Batch-Aufnahme, wenn Ihre Daten vor der Aufnahme vorbereitet und formatiert werden müssen.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, JSON oder Parquet</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Muss Batches und Dateien für die Aufnahme verwalten.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/en/docs/experience-platform/sources/home" style="color:#0563c1; text-decoration:underline">Batch-Quellen</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Gemeinsamer Ansatz für die Aufnahme von Daten aus Cloud-Speicher-, CRM- und Marketing-Automatisierungs-Anwendungen.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ideal für die Aufnahme großer Mengen historischer Daten.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Pull, CSV, JSON, Parquet</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Aufnahme in Source basierend auf vorkonfigurierten geplanten Intervallen.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/cloud-storage/data-landing-zone.html?lang=en" style="color:#0563c1; text-decoration:underline">Data Landing Zone</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Von Adobe bereitgestellte Cloud-basierte Dateispeicherung. Sie haben Zugriff auf einen Data Landing Zone-Container pro Sandbox.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Übertragen Sie Ihre Dateien in die Data Landing Zone zur späteren Aufnahme in Experience Platform.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, CSV, JSON, Parquet</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Experience Platform erzwingt eine strikte siebentägige Gültigkeitsdauer für alle Dateien und Ordner, die in einen Data Landing Zone-Container hochgeladen werden. Alle Dateien und Ordner werden nach sieben Tagen gelöscht.</span></span></span></li>
</ul>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/sdk/overview.html?lang=en" style="color:#0563c1; text-decoration:underline">Batch-Quellen - SDK</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Verwenden Sie die Self-Service-Funktionen von Batch-SDK für Selbstbedienungsquellen , um Ihre eigene Datenquelle in den Experience Platform-Quellkatalog zu integrieren.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ideal für Partner-Connectoren oder für ein maßgeschneidertes Workflow-Erlebnis beim Einrichten eines Unternehmens-Connectors.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Pull-, REST-API, CSV oder JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Beispiele für partnerintegrierte Batch-Quellen sind Mailchimp, OneTrust und Zendesk</span></span></span></li>
</ul>

<p> </p>
</td>
</tr>
</tbody>
</table>

## Nächste Schritte und zusätzliche Ressourcen

Dieses Dokument bietet eine kurze Einführung in die verschiedenen Aspekte von [!DNL Data Ingestion] in [!DNL Experience Platform]. Bitte lesen Sie darüber hinaus die Übersichtsdokumentation für jede Aufnahmemethode, um sich mit deren verschiedenen Funktionen, Anwendungsfällen und Best Practices vertraut zu machen. Sie können sich als Ergänzung zum Lernen auch das nachfolgende Video zur Aufnahme ansehen. Weitere Informationen dazu, wie [!DNL Experience Platform] die Metadaten nach erfassten Datensätzen verfolgt, finden Sie unter [Übersicht über den Katalog-Service](../catalog/home.md).

>[!WARNING]
>
>Der Begriff „Unified Profile“, der im folgenden Video verwendet wird, ist veraltet. Die Begriffe [!DNL "Profile"] oder [!DNL "Real-Time Customer Profile"] sind die korrekten Begriffe, die in der [!DNL Experience Platform]-Dokumentation verwendet werden. Die neuesten Funktionen finden Sie in der Dokumentation.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
