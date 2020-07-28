---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Audience Manager-Mapping-Feld
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 97%

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
| `Signals` | ExperienceEvent.signals |

## Eingehende Daten **(nicht mehr unterstützt)**

Typ: ExperienceEvent

| Eingehendes Feld | XDM-Feld |
| --- | --- |
| `uuid` | `ExperienceEvent.identityMap[<ID Type>]` |
| `deviceIds` | `ExperienceEvent.identityMap["CORE"] And calculated ECIDs  ExperienceEvent.identityMap["ECID"]` |
| `signals` | `ExperienceEvent.signals` |
| `b_time` | `ExperienceEvent.timeStamp` |
| `overwrite` | `overwriteTraits` |

>[!NOTE]
>
>Eingehende Felder werden in einer zukünftigen Version nicht mehr unterstützt.

## Profildaten

Typ: Profil

| Profilfeld | XDM-Feld |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
