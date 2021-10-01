---
solution: Experience Platform
title: Datentyp der Zustimmungszeichenfolge
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp "Consent String".
exl-id: 288ec79e-074a-4d72-9c5f-e9cd8485b804
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 5%

---

# [!UICONTROL Consent ] String-Datentyp

[!UICONTROL Einverständniszeichenfolge ] ist ein standardmäßiger XDM-Datentyp, der einen Zeichenfolgenwert beschreibt, der die Einwilligung eines Kunden darstellt. Sie enthält kontextbezogene Informationen wie den Standard für die Zustimmungszeichenfolge (z. B. das [IAB Transparency and Consent Framework (TCF) 2.0](../field-groups/profile/iab.md)).

![](../images/data-types/consent-string.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `consentStandard` | Zeichenfolge | Der Standard für die Zustimmungszeichenfolge. Dies hilft bei der Bestimmung des Formats der Zustimmungszeichenfolge, das von den Zustimmungsverwaltungsdiensten festgelegt wird. |
| `consentStandardVersion` | Zeichenfolge | Die Version des Zustimmungsstandards, die verwendet wird, um das Format der Zustimmungszeichenfolge genau zu definieren, das von den Zustimmungsverwaltungsdiensten festgelegt wurde. |
| `consentStringValue` | Zeichenfolge | Die vollständige Zustimmungszeichenfolge, die vom Zustimmungsverwaltungsdienst bereitgestellt wird. `consentStandard` und  `consentStandardVersion` helfen bei der Definition, wie diese Zeichenfolge analysiert wird. |
| `containsPersonalData` | Boolesch | Wenn dieses Feld wahr ist, bedeutet dies, dass diese Zustimmungszeichenfolge für die Durchsetzung der Zustimmung verarbeitet werden muss. |
| `gdprApplies` | Boolesch | Wenn dieses Feld zutrifft, bedeutet dies, dass die Einwilligung mit personenbezogenen Daten eingeht. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
