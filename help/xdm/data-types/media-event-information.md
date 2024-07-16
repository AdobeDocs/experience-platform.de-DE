---
title: Datentyp für Medienereignisinformationen
description: Erfahren Sie mehr über den Datentyp "Experience-Datenmodell (XDM) für Medienereignisse".
exl-id: 91bb7f28-b629-4044-b687-768c545ac8a2
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 5%

---

# Datentyp [!UICONTROL Medien-Ereignisinformationen]

[!UICONTROL Medien-Ereignisinformationen] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Mediendetails im Zusammenhang mit dem Erlebnisereignis beschreibt.

![Ein Diagramm des Datentyps &quot;Media Event Information&quot;.](../images/data-types/media-event-information.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `mediaCollection` | [!UICONTROL mediaDetails] | Mediendetailinformationen zum Erlebnisereignis. Dieser Datentyp wird sowohl für die [Mediensammlung](./media-collection-details.md) als auch für die [Mediendatenberichterstellung](./media-reporting-details.md) verwendet. |
| `mediaEventTimestamp` | [!UICONTROL String] | Der Zeitpunkt, zu dem ein Medienereignis aufgetreten ist. |
| `mediaEventType` | [!UICONTROL String] | Der Medien-Ereignistyp. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)
