---
solution: Experience Platform
title: Datentyp der Einverständniszeichenfolge
description: Erfahren Sie mehr über den XDM-Datentyp der Einverständniszeichenfolge.
exl-id: 288ec79e-074a-4d72-9c5f-e9cd8485b804
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 13%

---

# [!UICONTROL Einverständniszeichenfolge] Datentyp

[!UICONTROL Einverständniszeichenfolge] ist ein standardmäßiger XDM-Datentyp, der einen Zeichenfolgenwert beschreibt, der das Einverständnis eines Kunden darstellt. Sie enthält kontextuelle Informationen wie den Standard für die Einverständniszeichenfolge (z. B. das [IAB Transparency and Consent Framework (TCF) 2.0](../field-groups/profile/iab.md)).

![](../images/data-types/consent-string.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `consentStandard` | Zeichenfolge | Der Standard für die Einverständniszeichenfolge. Dies hilft bei der Bestimmung des Formats der Einverständniszeichenfolge, wie es von den Services der Einverständnisverwaltung festgelegt wird. |
| `consentStandardVersion` | String | Die Version des Einverständnisstandards, die verwendet wird, um das Format der Einverständniszeichenfolge genau zu definieren, wie es von den Services der Einverständnisverwaltung festgelegt wird. |
| `consentStringValue` | String | Die vollständige Einverständniszeichenfolge, wie vom Einverständnisverwaltungs-Service bereitgestellt. `consentStandard` und `consentStandardVersion` helfen zu definieren, wie diese Zeichenfolge analysiert werden soll. |
| `containsPersonalData` | Boolesch | Wenn dieses Feld „true“ ist, bedeutet dies, dass diese Einverständniszeichenfolge zur Durchsetzung des Einverständnisses verarbeitet werden muss. |
| `gdprApplies` | Boolesch | Wenn dieses Feld wahr ist, bedeutet dies, dass die Einwilligung mit personenbezogenen Daten erfolgt. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
