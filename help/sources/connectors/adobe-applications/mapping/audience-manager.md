---
keywords: Experience Platform; Startseite; beliebte Themen; Audience Manager-Mapping; Zielgruppen-Manager-Mapping
solution: Experience Platform
title: Zuordnen von Feldern für den Adobe Audience Manager Source Connector
description: Erfahren Sie, wie Sie Adobe Audience Manager-Daten (Echtzeit-, integrierte und Profildaten) den entsprechenden Experience-Datenmodell (XDM)-Feldern für den Audience Manager-Quell-Connector zuordnen.
exl-id: b800ba43-c308-4334-adce-3d554d50cefb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 73%

---

# Audience Manager-Feldzuordnungen

Die folgenden Tabellen enthalten die Mappings zwischen den Feldern in Adobe Audience Manager-Daten (Echtzeit-, integrierte und Profil-Daten) und den zugehörigen XDM-Feldern.

Weiterführende Informationen zu den einzelnen XDM-Feldern finden Sie im [Wörterbuch für XDM-Felder](../../../../xdm/schema/field-dictionary.md).

## Echtzeitdaten

Typ: Echtzeitdaten

| Echtzeitdatenfeld | XDM-Feld |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *Nur für Namespaces, die in endUserIds vorhanden sind, und nur der erste Wert.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *Nur für Namespaces, die in endUserIds vorhanden sind, und nur der erste Wert.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType → type</li><li>manufacturer → manufacturer</li><li>marketingName → model</li><li>modelNumber → model</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateProvince</li><li>d_city → city</li><li>d_postal → postalCode</li><li>d_lat → latitude</li><li>d_longitude → longitude</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → os name </li><li>d_os_version → os_version</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Profildaten

Typ: Profil

| Profilfeld | XDM-Feld |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |

{style=&quot;table-layout:auto&quot;}
