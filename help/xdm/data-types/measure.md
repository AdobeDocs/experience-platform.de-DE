---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schema;Maß;Datentyp;Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp messen
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den Datentyp "Measure Experience Data Model (XDM)".
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 5%

---

#  Messdatentyp

 Measurement ist ein Standard-Experience Data Model (XDM)-Datentyp, der einen konkreten quantifizierbaren Datenpunkt einer bestimmten Metrik enthält. Eine Maßeinheit besteht aus einem eindeutigen Bezeichner und einem Wert.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `id` | Zeichenfolge | Der eindeutige Bezeichner dieser Maßnahme. Bei der Datenerfassung mit verlustbehafteten Kommunikations-Kanälen wie mobilen Apps oder Websites mit Offlinefunktion, bei denen die Übertragung von Messwerten nicht sichergestellt werden kann, enthält diese Eigenschaft eine vom Kunden generierte eindeutige ID der durchgeführten Maßnahme. Es empfiehlt sich, dies so lange zu machen, dass eine ausreichende Zufälligkeit gewährleistet ist. <br><br> Wenn Informationen wie Zeitstempel, Geräte-ID, IP, MAC-Adresse oder andere potenziell benutzerspezifische Werte in die Generierung der Datei einbezogen werden,  `id`sollte das Ergebnis mit Hashing versehen werden. Dadurch wird sichergestellt, dass keine PII-Datei im Wert kodiert ist, da das Ziel nicht darin besteht, einen Benutzer oder ein Gerät zu identifizieren, sondern die spezifische Messung rechtzeitig. |
| `value` | Double | Der quantifizierbare Wert dieser Maßnahme. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
