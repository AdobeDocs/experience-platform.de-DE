---
description: Erfahren Sie mehr über die historischen Profilqualifikationen, die von mit Destination SDK erstellten Zielen unterstützt werden.
title: Historische Profilqualifikationen
source-git-commit: 65a658208b48a50184e55a6d64cdf7ad6de0f04f
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 10%

---


# Historische Profilqualifikationen

Alle Ziele, die über Destination SDK erstellt wurden, unterstützen standardmäßig historische Profilqualifikationen. Das bedeutet, dass der erste Export, wenn Benutzer einen Aktivierungsdatenfluss zu Ihren Zielen einrichten, alle Mitglieder des Segments enthält, die sich für dieses Segment qualifiziert haben.

Dieses Verhalten wird durch die Variable `"backfillHistoricalProfileData":true` in der Zielkonfiguration.

>[!IMPORTANT]
>
>Historische Profilqualifikationen sind für alle Ziele aktiviert, die durch die Destination SDK erstellt wurden, und die `backfillHistoricalProfileData` -Parameter kann nicht vom Benutzer konfiguriert werden.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Ja |
| Dateibasierte (Batch-)Integrationen | Ja |



<!-- 
|Parameter | Type | Description|
|---------|----------|------|
|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when segments are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the segment before the segment is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the segment after the segment is activated. </li></ul> |

{style="table-layout:auto"} -->


## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie wissen, dass die Experience Platform automatisch eine historische Population aller Profile exportiert, die sich je für ein aktiviertes Segment qualifiziert haben, wenn das Segment zum ersten Mal an das Ziel exportiert wird. Diese Option kann nicht in Destination SDK oder in der Experience Platform-Benutzeroberfläche konfiguriert werden.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Kundenauthentifizierung](customer-authentication.md)
* [OAuth 2-Authentifizierung](oauth2-authentication.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Benutzeroberflächenattribute](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Identitäts-Namespace-Konfiguration](identity-namespace-configuration.md)
* [Unterstützte Zuordnungskonfigurationen](supported-mapping-configurations.md)
* [Zielbereitstellung](destination-delivery.md)
* [Konfiguration von Zielgruppen-Metadaten](audience-metadata-configuration.md)
* [Aggregationsrichtlinie](aggregation-policy.md)
* [Batch-Konfiguration](batch-configuration.md)