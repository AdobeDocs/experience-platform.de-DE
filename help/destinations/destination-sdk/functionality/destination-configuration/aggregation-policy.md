---
description: Erfahren Sie, wie Sie eine Aggregationsrichtlinie einrichten, um zu bestimmen, wie HTTP-Anfragen an Ihr Ziel gruppiert und in Batches eingesetzt werden sollen.
title: Aggregationsrichtlinie
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 96%

---


# Aggregationsrichtlinie

Um beim Export von Daten in Ihren API-Endpunkt maximale Effizienz zu gewährleisten, können Sie verschiedene Einstellungen verwenden, um etwa exportierte Profile in größere oder kleinere Batches zu aggregieren, sie nach Identität zu gruppieren, und andere Anwendungsfälle. Auf diese Weise können Sie Datenexporte auch auf nachgelagerte Einschränkungen Ihres API-Endpunkts anpassen (Ratenbegrenzung, Anzahl der Identitäten pro API-Aufruf usw.).

Verwenden Sie eine konfigurierbare Aggregation, um sich einen tiefen Einblick in die von Destination SDK bereitgestellten Einstellungen zu verschaffen, oder nutzen Sie die Aggregation nach bestem Bemühen, um Destination SDK anzuweisen, die API-Aufrufe so gut wie möglich zu bündeln.

Beim Erstellen eines Echtzeit-Ziels (Streaming) mit Destination SDK können Sie konfigurieren, wie die exportierten Profile in den resultierenden Exporten kombiniert werden sollen. Dieses Verhalten wird durch die Einstellungen der Aggregationsrichtlinie bestimmt.

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm in der Dokumentation zu [Konfigurationsoptionen](../configuration-options.md) oder im Handbuch zum [Verwenden von Destination SDK zum Konfigurieren eines Streaming-Ziels](../../guides/configure-destination-instructions.md#create-destination-configuration).

Sie können die Einstellungen der Aggregationsrichtlinie über den Endpunkt `/authoring/destinations` konfigurieren. Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aktualisieren einer Zielkonfiguration](../../authoring-api/destination-configuration/update-destination-configuration.md)

In diesem Artikel werden alle unterstützten Einstellungen für Aggregationsrichtlinien beschrieben, die Sie für Ihr Ziel verwenden können.

Lesen Sie nach diesem Dokument den Abschnitt über die [Verwendung von Vorlagen](../../functionality/destination-server/message-format.md#using-templating) und die [wichtigsten Aggregations-Beispiele](../../functionality/destination-server/message-format.md#template-aggregation-key), um zu verstehen, wie Sie die Aggregationsrichtlinie basierend auf Ihrer ausgewählten Aggregationsrichtlinie in Ihre Nachrichtenumwandlungsvorlage einschließen.

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Ja |
| Dateibasierte (Batch-)Integrationen | Nein |

## Aggregation nach bestem Bemühen (Best-Effort-Aggregation) {#best-effort-aggregation}

Die Aggregation nach bestem Bemühen eignet sich am besten für Ziele, die weniger Profile pro Anfrage bevorzugen und lieber mehr Anfragen mit weniger Daten als weniger Anfragen mit mehr Daten hätten.

Die folgende Beispielkonfiguration zeigt eine Konfiguration einer Aggregation nach bestem Bemühen. Ein Beispiel für eine konfigurierbare Aggregation finden Sie im Abschnitt [konfigurierbare Aggregation](#configurable-aggregation). Die Parameter für die Aggregation nach bestem Bemühen sind in der folgenden Tabelle beschrieben.

```json
"aggregation":{
   "aggregationType":"BEST_EFFORT",
   "bestEffortAggregation":{
      "maxUsersPerRequest":10,
      "splitUserById":false
   }
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `aggregationType` | Zeichenfolge | Gibt den Typ der Aggregationsrichtlinie an, die Ihr Ziel verwenden soll. Unterstützte Aggregationstypen: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | Ganzzahl | Experience Platform kann mehrere exportierte Profile in einem einzigen HTTP-Aufruf aggregieren. <br><br>Geben Sie hier die maximale Anzahl von Profilen an, die Ihr Endpunkt in einem einzelnen HTTP-Aufruf erhalten soll. Beachten Sie, dass dies eine bestmögliche Aggregation ist. Wenn Sie beispielsweise den Wert 100 angeben, kann Platform eine beliebige Anzahl von Profilen senden, solange es weniger als 100 sind. <br><br> Wenn Ihr Server nicht mehrere Benutzerinnen oder Benutzer pro Anfrage akzeptiert, setzen Sie diesen Wert auf `1`. |
| `bestEffortAggregation.splitUserById` | Boolesch | Verwenden Sie dieses Flag, wenn der Aufruf an das Ziel nach Identität aufgeteilt werden soll. Setzen Sie dieses Flag auf `true`, wenn Ihr Server für einen gegebenen Namespace nur eine Identität pro Aufruf akzeptiert. |

{style="table-layout:auto"}

>[!TIP]
>
>Verwenden Sie die Aggregation nach bestem Bemühen, wenn Ihr API-Endpunkt weniger als 100 Profile pro API-Aufruf akzeptiert.

## Konfigurierbare Aggregation {#configurable-aggregation}

Die konfigurierbare Aggregation eignet sich am besten, wenn Sie im selben Aufruf große Batches mit Tausenden Profilen verwenden möchten. Mit dieser Option können Sie die exportierten Profile auch anhand komplexer Aggregationsregeln aggregieren.

Die folgende Beispielkonfiguration zeigt eine konfigurierbare Aggregationskonfiguration. Ein Beispiel für die Aggregation nach bestem Bemühen finden Sie im Abschnitt [Aggregation nach bestem Bemühen](#best-effort-aggregation). Die Parameter für die konfigurierbare Aggregation sind in der folgenden Tabelle beschrieben.

```json
"aggregation":{
   "aggregationType":"CONFIGURABLE_AGGREGATION",
   "configurableAggregation":{
      "splitUserById":true,
      "maxBatchAgeInSecs":2400,
      "maxNumEventsInBatch":5000,
      "aggregationKey":{
         "includeSegmentId":true,
         "includeSegmentStatus":true,
         "includeIdentity":true,
         "oneIdentityPerGroup":true,
         "groups":[
            {
               "namespaces":[
                  "IDFA",
                  "GAID"
               ]
            },
            {
               "namespaces":[
                  "EMAIL"
               ]
            }
         ]
      }
   }
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `aggregationType` | Zeichenfolge | Gibt den Typ der Aggregationsrichtlinie an, die Ihr Ziel verwenden soll. Unterstützte Aggregationstypen: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `configurableAggregation.splitUserById` | Boolesch | Verwenden Sie dieses Flag, wenn der Aufruf an das Ziel nach Identität aufgeteilt werden soll. Setzen Sie dieses Flag auf `true`, wenn Ihr Server für einen gegebenen Namespace nur eine Identität pro Aufruf akzeptiert. |
| `configurableAggregation.maxBatchAgeInSecs` | Ganzzahl | Zusammen mit `maxNumEventsInBatch` bestimmt dieser Parameter, wie lange Experience Platform warten soll, bis ein API-Aufruf an Ihren Endpunkt gesendet wird. <ul><li>Mindestwert (Sekunden): 1800</li><li>Höchstwert (Sekunden): 3600</li></ul> Wenn Sie beispielsweise den Maximalwert für beide Parameter verwenden, wartet Experience Platform entweder 3.600 Sekunden ODER, bis 10000 qualifizierte Profile vorhanden sind, bevor der API-Aufruf erfolgt (je nachdem, was früher eintritt). |
| `configurableAggregation.maxNumEventsInBatch` | Ganzzahl | Zusammen mit `maxBatchAgeInSecs` bestimmt dieser Parameter, wie viele qualifizierte Profile in einem API-Aufruf aggregiert werden sollen. <ul><li>Mindestwert: 1000</li><li>Höchstwert: 10.000</li></ul> Wenn Sie beispielsweise den Maximalwert für beide Parameter verwenden, wartet Experience Platform entweder 3.600 Sekunden ODER, bis 10000 qualifizierte Profile vorhanden sind, bevor der API-Aufruf erfolgt (je nachdem, was früher eintritt). |
| `configurableAggregation.aggregationKey` | – | Ermöglicht die Aggregation der dem Ziel zugeordneten exportierten Profile anhand der folgenden Parameter. |
| `configurableAggregation.aggregationKey.includeSegmentId` | Boolesch | Legen Sie diesen Parameter auf `true` , wenn Sie Profile gruppieren möchten, die nach Zielgruppen-ID in Ihr Ziel exportiert wurden. |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | Boolesch | Legen Sie sowohl diesen Parameter als auch fest. `includeSegmentId` nach `true`, wenn Sie Profile gruppieren möchten, die nach Zielgruppen-ID und Zielgruppenstatus in Ihr Ziel exportiert wurden. |
| `configurableAggregation.aggregationKey.includeIdentity` | Boolesch | Legen Sie diesen Parameter auf `true` fest, wenn Sie Profile gruppieren möchten, die nach Identity-Namespace zu Ihrem Ziel exportiert wurden. |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | Boolesch | Legen Sie diesen Parameter auf `true` fest, um anzugeben, ob die exportierten Profile in Gruppen einer einzigen Identität zusammengefasst werden sollen (GAID, IDFA, Telefonnummern, E-Mail usw.). |
| `configurableAggregation.aggregationKey.groups` | Array | Erstellen Sie Listen mit Identitätsgruppen, wenn Sie Profile gruppieren möchten, die nach Gruppen von Identity-Namespaces in Ihr Ziel exportiert wurden. Beispielsweise können Sie Profile, die die Kennungen IDFA und GAID für Mobilgeräte enthalten, mithilfe der im obigen Beispiel beschriebenen Konfiguration zu einem Aufruf an Ihr Ziel und E-Mails an ein anderes kombinieren. |

{style="table-layout:auto"}

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie besser verstehen, wie Sie Aggregationsrichtlinien für Ihr Ziel konfigurieren können.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Konfiguration der Kundenauthentifizierung](customer-authentication.md)
* [OAuth 2-Authentifizierung](oauth2-authentication.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Benutzeroberflächenattribute](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration von Identity-Namespaces](identity-namespace-configuration.md)
* [Unterstützte Zuordnungskonfigurationen](supported-mapping-configurations.md)
* [Zielbereitstellung](destination-delivery.md)
* [Konfiguration von Zielgruppen-Metadaten](audience-metadata-configuration.md)
* [Batch-Konfiguration](batch-configuration.md)
* [Historische Profilqualifikationen](historical-profile-qualifications.md)