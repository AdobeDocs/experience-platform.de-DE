---
title: Datentyp für Medienereignisinformationen
description: Erfahren Sie mehr über den Datentyp "Experience-Datenmodell (XDM) für Medienereignisse".
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 6%

---

# [!UICONTROL Informationen zu Medienereignissen] Datentyp

[!UICONTROL Medien-Ereignisinformationen] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Informationen zu Mediendetails im Zusammenhang mit dem Erlebnisereignis beschreibt.

![Ein Diagramm des Datentyps Media Event Information .](../images/data-types/media-event-information.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `mediaCollection` | [[!UICONTROL mediaDetails]](./media-details-information.md) | Mediendetailinformationen zum Erlebnisereignis. |
| `mediaEventTimestamp` | [!UICONTROL String] | Der Zeitpunkt, zu dem ein Medienereignis aufgetreten ist. |
| `mediaEventType` | [!UICONTROL String] | Der Medien-Ereignistyp. |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)
