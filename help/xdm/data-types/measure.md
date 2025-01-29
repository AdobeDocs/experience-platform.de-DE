---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Kennzahlen;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Kennzahldatentyp
description: Erfahren Sie mehr über den Datentyp Measure Experience Data Model (XDM).
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 5%

---

# [!UICONTROL Kennzahl] Datentyp

[!UICONTROL Measure] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der einen konkreten quantifizierbaren Datenpunkt einer bestimmten Metrik enthält. Eine Kennzahl besteht aus einer eindeutigen Kennung und einem Wert.

![Bild messen](../images/data-types/measure.PNG){width=500}

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `id` | Zeichenfolge | Die eindeutige Kennung dieser Kennzahl. Bei der Datenerfassung über verlustbehaftete Kommunikationskanäle, wie z. B. mobile Apps oder Websites mit Offline-Funktionalität, bei denen die Übertragung von Maßnahmen nicht sichergestellt werden kann, enthält diese Eigenschaft eine Client-generierte eindeutige ID der getroffenen Maßnahme. Es empfiehlt sich, dies so lange zu wählen, dass eine ausreichende Zufälligkeit gewährleistet ist. <br><br> Wenn Informationen wie Zeitstempel, Geräte-ID, IP-Adresse, MAC-Adresse oder andere potenziell benutzeridentifizierende Werte in die Generierung der `id` einbezogen werden, sollte das Ergebnis gehasht werden. Dadurch wird sichergestellt, dass keine personenbezogenen Daten im Wert codiert werden, da das Ziel nicht darin besteht, einen Benutzer oder ein Gerät zu identifizieren, sondern die spezifische Zeitmessung. |
| `value` | Double | Der quantifizierbare Wert dieser Maßnahme. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
