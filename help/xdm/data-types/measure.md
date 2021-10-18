---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; messen; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp messen
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den Datentyp "Experience-Datenmodell (XDM) messen".
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 6%

---

#  Messdatentyp

 Measurement ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der einen konkreten quantifizierbaren Datenpunkt einer bestimmten Metrik enthält. Eine Kennzahl besteht aus einer eindeutigen Kennung und einem Wert.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `id` | Zeichenfolge | Die eindeutige Kennung dieser Kennzahl. Bei der Datenerfassung über verlustreiche Kommunikationskanäle wie mobile Apps oder Websites mit Offline-Funktionalität, bei denen die Übermittlung von Kennzahlen nicht sichergestellt werden kann, enthält diese Eigenschaft eine clientgenerierte, eindeutige ID der getroffenen Maßnahme. Es ist Best Practice, dies so lange zu machen, dass eine ausreichende Zufallsrate gewährleistet ist. <br><br> Wenn Informationen wie Zeitstempel, Geräte-ID, IP, MAC-Adresse oder andere potenziell identifizierbare Benutzerwerte in die Generierung der integriert sind, sollte  `id`das Ergebnis gehasht werden. Dadurch wird sichergestellt, dass keine PII im Wert kodiert ist, da das Ziel nicht darin besteht, einen Benutzer oder ein Gerät zu identifizieren, sondern die spezifische Kennzahl rechtzeitig. |
| `value` | Double | Der quantifizierbare Wert dieser Maßnahme. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
