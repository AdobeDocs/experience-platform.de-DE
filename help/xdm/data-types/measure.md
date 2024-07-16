---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; messen; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp messen
description: Erfahren Sie mehr über den Datentyp Erlebnis-Datenmodell messen (XDM) .
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 5%

---

# Datentyp [!UICONTROL Messung]

[!UICONTROL Maßnahme] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der einen konkreten quantifizierbaren Datenpunkt einer bestimmten Metrik enthält. Eine Kennzahl besteht aus einer eindeutigen Kennung und einem Wert.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `id` | Zeichenfolge | Die eindeutige Kennung dieser Kennzahl. Bei der Datenerfassung über verlustreiche Kommunikationskanäle wie mobile Apps oder Websites mit Offline-Funktionalität, bei denen die Übermittlung von Kennzahlen nicht sichergestellt werden kann, enthält diese Eigenschaft eine clientgenerierte, eindeutige ID der getroffenen Maßnahme. Es ist Best Practice, dies so lange zu machen, dass eine ausreichende Zufallsrate gewährleistet ist. <br><br> Wenn Informationen wie Zeitstempel, Geräte-ID, IP, MAC-Adresse oder andere mögliche Benutzeridentifizierungswerte in die Generierung von `id` einbezogen werden, sollte das Ergebnis gehasht werden. Dadurch wird sichergestellt, dass keine PII im Wert kodiert ist, da das Ziel nicht darin besteht, einen Benutzer oder ein Gerät zu identifizieren, sondern die spezifische Kennzahl rechtzeitig. |
| `value` | Double | Der quantifizierbare Wert dieser Maßnahme. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
