---
title: Datentyp "Implementierungsdetails"
description: Erfahren Sie mehr über die Implementierungsdetails zum Experience-Datenmodell (XDM)-Datentyp.
exl-id: d3d16bae-196b-489d-8590-fd22150eedf1
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 7%

---

# [!UICONTROL Implementierungsdetails] Datentyp

[!UICONTROL Implementierungsdetails] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der eine Technologieimplementierung wie eine API oder ein SDK beschreibt.

![Datentypstruktur](../images/data-types/implementation-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `environment` | Zeichenfolge | Die Umgebung der Implementierung. |
| `name` | Zeichenfolge | Die Kennung für das SDK oder den Endpunkt. Alle SDKs oder Endpunkte werden über einen URI identifiziert, einschließlich Erweiterungen. |
| `version` | Zeichenfolge | Die Version der API oder des SDK. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
