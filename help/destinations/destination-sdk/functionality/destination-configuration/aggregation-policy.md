---
description: Erfahren Sie, wie Sie eine Aggregationsrichtlinie einrichten, um zu bestimmen, wie HTTP-Anfragen an Ihr Ziel gruppiert und in Batches eingesetzt werden sollen.
title: Aggregationsrichtlinie
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 14%

---


# Aggregationsrichtlinie

Um beim Export von Daten in Ihren API-Endpunkt maximale Effizienz zu gewährleisten, können Sie verschiedene Einstellungen verwenden, um exportierte Profile in größere oder kleinere Batches zu aggregieren, sie nach Identität und anderen Anwendungsfällen zu gruppieren. Auf diese Weise können Sie Datenexporte auch auf nachgelagerte Einschränkungen Ihres API-Endpunkts anpassen (Ratenbegrenzung, Anzahl der Identitäten pro API-Aufruf usw.).

Verwenden Sie eine konfigurierbare Aggregation, um sich einen tiefen Einblick in die von Destination SDK bereitgestellten Einstellungen zu verschaffen, oder nutzen Sie die Aggregation nach bestem Wissen, um Destination SDK anzuweisen, die API-Aufrufe so zusammenzuführen, wie es möglich ist.

Beim Erstellen eines Echtzeit-Ziels (Streaming) mit Destination SDK können Sie konfigurieren, wie die exportierten Profile in den resultierenden Exporten kombiniert werden sollen. Dieses Verhalten wird durch die Einstellungen der Aggregationsrichtlinie bestimmt.

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm im [Konfigurationsoptionen](../configuration-options.md) Dokumentation oder lesen Sie das Handbuch zu [Verwenden von Destination SDK zum Konfigurieren eines Streaming-Ziels](../../guides/configure-destination-instructions.md#create-destination-configuration).

Sie können die Einstellungen der Aggregationsrichtlinie über die `/authoring/destinations` -Endpunkt. Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Zielkonfiguration aktualisieren](../../authoring-api/destination-configuration/update-destination-configuration.md)

In diesem Artikel werden alle unterstützten Einstellungen für Aggregationsrichtlinien beschrieben, die Sie für Ihr Ziel verwenden können.

Lesen Sie nach dem Lesen dieses Dokuments das Handbuch unter [mit Vorlage](../../functionality/destination-server/message-format.md#using-templating) und [Beispiele für Aggregationsschlüssel](../../functionality/destination-server/message-format.md#template-aggregation-key) um zu verstehen, wie Sie die Aggregationsrichtlinie basierend auf Ihrer ausgewählten Aggregationsrichtlinie in Ihre Nachrichtenumwandlungsvorlage aufnehmen.

>[!IMPORTANT]
>
>Alle von Destination SDK unterstützten Parameternamen und Werte sind **Groß-/Kleinschreibung**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Ja |
| Dateibasierte (Batch-)Integrationen | Nein |

## Best-Effort-Aggregation {#best-effort-aggregation}

Die optimale Aggregation eignet sich am besten für Ziele, die weniger Profile pro Anforderung bevorzugen und stattdessen mehr Anforderungen mit weniger Daten als weniger Anforderungen mit mehr Daten aufnehmen möchten.

Die folgende Beispielkonfiguration zeigt eine Konfiguration der Aggregation mit dem besten Aufwand. Ein Beispiel für eine konfigurierbare Aggregation finden Sie unter [konfigurierbare Aggregation](#configurable-aggregation) Abschnitt. Die Parameter für die Aggregation des besten Aufwands sind in der folgenden Tabelle beschrieben.

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
| `aggregationType` | Zeichenfolge | Gibt den Typ der Aggregationsrichtlinie an, die Ihr Ziel verwenden soll. Unterstützte Aggregattypen: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | Ganzzahl | Experience Platform kann mehrere exportierte Profile in einem einzigen HTTP-Aufruf aggregieren. <br><br>Dieser Wert gibt die maximale Anzahl von Profilen an, die Ihr Endpunkt in einem einzelnen HTTP-Aufruf erhalten soll. Beachten Sie, dass dies eine bestmögliche Aggregation ist. Wenn Sie beispielsweise den Wert 100 angeben, kann Platform eine beliebige Anzahl von Profilen senden, solange es weniger als 100 sind. <br><br> Wenn Ihr Server mehrere Benutzer pro Anforderung nicht akzeptiert, setzen Sie diesen Wert auf `1`. |
| `bestEffortAggregation.splitUserById` | Boolesch | Verwenden Sie dieses Flag, wenn der Aufruf an das Ziel nach Identität aufgeteilt werden soll. Setzen Sie dieses Flag auf `true` Wenn Ihr Server nur eine Identität pro Aufruf akzeptiert, für einen bestimmten Identitäts-Namespace. |

{style="table-layout:auto"}

>[!TIP]
>
>Verwenden Sie die optimale Aggregation, wenn Ihr API-Endpunkt weniger als 100 Profile pro API-Aufruf akzeptiert.

## Konfigurierbare Aggregation {#configurable-aggregation}

Die konfigurierbare Aggregation funktioniert am besten, wenn Sie große Batches mit Tausenden von Profilen im selben Aufruf einsetzen möchten. Mit dieser Option können Sie die exportierten Profile auch anhand komplexer Aggregationsregeln aggregieren.

Die folgende Beispielkonfiguration zeigt eine konfigurierbare Aggregationskonfiguration. Ein Beispiel für die Aggregation des besten Aufwands finden Sie unter [Aggregation des besten Aufwands](#best-effort-aggregation) Abschnitt. Die Parameter für die konfigurierbare Aggregation sind in der folgenden Tabelle beschrieben.

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
| `aggregationType` | Zeichenfolge | Gibt den Typ der Aggregationsrichtlinie an, die Ihr Ziel verwenden soll. Unterstützte Aggregattypen: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `configurableAggregation.splitUserById` | Boolesch | Verwenden Sie dieses Flag, wenn der Aufruf an das Ziel nach Identität aufgeteilt werden soll. Setzen Sie dieses Flag auf `true` Wenn Ihr Server nur eine Identität pro Aufruf akzeptiert, für einen bestimmten Identitäts-Namespace. |
| `configurableAggregation.maxBatchAgeInSecs` | Ganzzahl | Wird in Verbindung mit `maxNumEventsInBatch`festgelegt ist, bestimmt dieser Parameter, wie lange die Experience Platform warten soll, bis ein API-Aufruf an Ihren -Endpunkt gesendet wird. <ul><li>Mindestwert (Sekunden): 1800</li><li>Höchstwert (Sekunden): 3600</li></ul> Wenn Sie beispielsweise den Maximalwert für beide Parameter verwenden, wartet die Experience Platform entweder 3600 Sekunden ODER, bis 10000 qualifizierte Profile vorhanden sind, bevor der API-Aufruf erfolgt (je nachdem, was früher eintritt). |
| `configurableAggregation.maxNumEventsInBatch` | Ganzzahl | Wird zusammen mit `maxBatchAgeInSecs`festgelegt ist, bestimmt dieser Parameter, wie viele qualifizierte Profile in einem API-Aufruf aggregiert werden sollen. <ul><li>Mindestwert: 1000</li><li>Höchstwert: 10.000</li></ul> Wenn Sie beispielsweise den Maximalwert für beide Parameter verwenden, wartet die Experience Platform entweder 3600 Sekunden ODER, bis 10000 qualifizierte Profile vorhanden sind, bevor der API-Aufruf erfolgt (je nachdem, was früher eintritt). |
| `configurableAggregation.aggregationKey` | – | Ermöglicht die Aggregation der dem Ziel zugeordneten exportierten Profile anhand der unten beschriebenen Parameter. |
| `configurableAggregation.aggregationKey.includeSegmentId` | Boolesch | Legen Sie diesen Parameter auf `true` , wenn Sie Profile gruppieren möchten, die nach Segment-ID in Ihr Ziel exportiert wurden. |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | Boolesch | Legen Sie sowohl diesen Parameter als auch fest. `includeSegmentId` nach `true`, wenn Sie Profile gruppieren möchten, die nach Segment-ID und Segmentstatus in Ihr Ziel exportiert wurden. |
| `configurableAggregation.aggregationKey.includeIdentity` | Boolesch | Legen Sie diesen Parameter auf `true` , wenn Sie Profile gruppieren möchten, die nach Ihrem Ziel nach Identitäts-Namespace exportiert wurden. |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | Boolesch | Setzen Sie diesen Parameter auf `true` wenn die exportierten Profile basierend auf einer einzigen Identität in Gruppen zusammengefasst werden sollen (GAID, IDFA, Telefonnummern, E-Mail usw.). |
| `configurableAggregation.aggregationKey.groups` | Array | Erstellen Sie Listen mit Identitätsgruppen, wenn Sie Profile gruppieren möchten, die nach Gruppen von Identitäts-Namespaces an Ihr Ziel exportiert wurden. Beispielsweise können Sie Profile, die die Kennung des IDFA- und des GAID-Handys enthalten, mithilfe der oben gezeigten Konfiguration zu einem Aufruf an Ihr Ziel und zu E-Mails zu einem anderen kombinieren. |

{style="table-layout:auto"}

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie besser verstehen, wie Sie Aggregationsrichtlinien für Ihr Ziel konfigurieren können.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Konfiguration der Kundenauthentifizierung](customer-authentication.md)
* [OAuth 2-Authentifizierung](oauth2-authentication.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Benutzeroberflächenattribute](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Identitäts-Namespace-Konfiguration](identity-namespace-configuration.md)
* [Unterstützte Zuordnungskonfigurationen](supported-mapping-configurations.md)
* [Zielbereitstellung](destination-delivery.md)
* [Konfiguration von Zielgruppen-Metadaten](audience-metadata-configuration.md)
* [Batch-Konfiguration](batch-configuration.md)
* [Historische Profilqualifikationen](historical-profile-qualifications.md)