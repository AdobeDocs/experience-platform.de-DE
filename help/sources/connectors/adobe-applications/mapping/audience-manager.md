---
keywords: Experience Platform;Startseite;beliebte Themen;Zuordnung von Audience Managern;Zuordnung von Audiencen-Managern
solution: Experience Platform
title: Audience Manager-Mapping-Feld
topic: overview
description: Die folgenden Tabellen enthalten die Mappings zwischen den Feldern in Adobe Audience Manager-Daten (Echtzeit-, integrierte und Profil-Daten) und den zugehörigen XDM-Feldern.
translation-type: tm+mt
source-git-commit: 6934bfeee84f542558894bbd4ba5759891cd17f3
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 90%

---


# Zuordnungsfelder für Audience Manager

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

## Profildaten

Typ: Profil

| Profilfeld | XDM-Feld |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
