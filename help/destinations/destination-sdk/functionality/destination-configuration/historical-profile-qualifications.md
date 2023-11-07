---
description: Erfahren Sie mehr über die historischen Profilqualifikationen, die von mit Destination SDK erstellten Zielen unterstützt werden.
title: Historische Profilqualifikationen
exl-id: 8880cff9-865b-4d45-a24d-a78e77419670
source-git-commit: 8f430fa3949c19c22732ff941e8c9b07adb37e1f
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 100%

---

# Historische Profilqualifikationen

Alle Ziele, die über Destination SDK erstellt wurden, unterstützen standardmäßig historische Profilqualifikationen. Das bedeutet, dass, wenn Benutzerinnen oder Benutzer einen Aktivierungsdatenfluss zu Ihren Zielen einrichten, der erste Export alle Mitglieder der Zielgruppe enthält, die sich für dieses Segment qualifiziert haben.

Dieses Verhalten wird durch die Variable `"backfillHistoricalProfileData":true` in der Zielkonfiguration bestimmt.

>[!IMPORTANT]
>
>Historische Profilqualifikationen sind für alle Ziele aktiviert, die durch Destination SDK erstellt wurden, und der Parameter `backfillHistoricalProfileData` kann nicht von Benutzenden konfiguriert werden.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Ja |
| Dateibasierte (Batch-)Integrationen | Ja |



<!-- 
|Parameter | Type | Description|
|---------|----------|------|
|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when audiences are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the audience before the audience is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the audience after the audience is activated. </li></ul> |

{style="table-layout:auto"} -->


## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie wissen, dass Experience Platform automatisch eine historische Population aller Profile exportiert, die sich je für eine aktivierte Zielgruppe qualifiziert haben, wenn die Zielgruppe zum ersten Mal an das Ziel exportiert wird. Diese Option kann weder in Destination SDK noch in der Experience Platform-Benutzeroberfläche konfiguriert werden.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Kundenauthentifizierung](customer-authentication.md)
* [OAuth 2-Authentifizierung](oauth2-authorization.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Benutzeroberflächenattribute](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration von Identity-Namespaces](identity-namespace-configuration.md)
* [Unterstützte Zuordnungskonfigurationen](supported-mapping-configurations.md)
* [Zielbereitstellung](destination-delivery.md)
* [Konfiguration von Zielgruppen-Metadaten](audience-metadata-configuration.md)
* [Aggregationsrichtlinie](aggregation-policy.md)
* [Batch-Konfiguration](batch-configuration.md)
