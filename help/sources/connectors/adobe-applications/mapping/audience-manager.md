---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zuordnungsfeld für Audience Manager
topic: overview
translation-type: tm+mt
source-git-commit: 53fb7ea201ed9361584d24c8bd2ad10edd9f3975
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# Zuordnungsfelder für Audience Manager

Die folgenden Tabellen enthalten die Zuordnungen zwischen den Feldern in Adobe Audience Manager-Daten (Echtzeit-, Onboarded- und Profil-Daten) und den zugehörigen XDM-Feldern.

Weitere Informationen zu den einzelnen XDM-Feldern finden Sie im [XDM-Feldwörterbuch](../../../../xdm/schema/field-dictionary.md) .

## Echtzeitdaten

Typ: Echtzeitdaten

| Echtzeit-Datenfeld | XDM-Feld |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *Nur für Namensraum, die in endUserIds vorhanden sind, und nur für den ersten Wert.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *Nur für Namensraum, die in endUserIds vorhanden sind, und nur für den ersten Wert.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType → type</li><li>Hersteller → Hersteller</li><li>marketingName → model</li><li>modelNumber → model</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateProvince</li><li>d_city → city</li><li>d_postal → postCode</li><li>d_lat → Breitengrad</li><li>d_Längengrad → Längengrad</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → os_name </li><li>d_os_version → os_version</li></ul> |
| `Signals` | ExperienceEvent.signals |

## Inbound-Daten **(nicht mehr unterstützt)**

Typ: ExperienceEvent

| Inbound-Feld | XDM-Feld |
| --- | --- |
| `uuid` | `ExperienceEvent.identityMap[<ID Type>]` |
| `deviceIds` | `ExperienceEvent.identityMap["CORE"] And calculated ECIDs  ExperienceEvent.identityMap["ECID"]` |
| `signals` | `ExperienceEvent.signals` |
| `b_time` | `ExperienceEvent.timeStamp` |
| `overwrite` | `overwriteTraits` |

>[!NOTE] Eingehende Felder werden in einer zukünftigen Version als veraltet geplant.

## Profil

Typ: Profil XDM

| Profil | XDM-Feld |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
