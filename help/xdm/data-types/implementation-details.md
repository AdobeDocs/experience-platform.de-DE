---
title: Datentyp "Implementierungsdetails"
description: Dieses Dokument bietet einen Überblick über die Implementierungsdetails zum Experience-Datenmodell (XDM)-Datentyp.
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 18%

---

# [!UICONTROL Implementierungsdetails] Datentyp

[!UICONTROL Implementierungsdetails] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der eine Technologieimplementierung wie eine API oder ein SDK beschreibt.

![Datentypstruktur](../images/data-types/implementation-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `environment` | Zeichenfolge | Die Umgebung der Implementierung. |
| `name` | Zeichenfolge | Die Kennung für das SDK oder den Endpunkt. Alle SDKs oder Endpunkte werden über einen URI identifiziert, einschließlich Erweiterungen. |
| `version` | Zeichenfolge | Die Version der API oder des SDK. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
