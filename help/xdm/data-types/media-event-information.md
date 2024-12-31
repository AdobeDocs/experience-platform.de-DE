---
title: Datentyp der Medienereignis-Informationen
description: Erfahren Sie mehr über den Datentyp Medienereignis-Experience-Datenmodell (XDM).
exl-id: 91bb7f28-b629-4044-b687-768c545ac8a2
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 5%

---

# [!UICONTROL Medienereignis-Informationen] Datentyp

[!UICONTROL Medienereignisinformationen] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Mediendetailinformationen im Zusammenhang mit dem Erlebnisereignis beschreibt.

![Ein Diagramm zum Datentyp „Medienereignisinformationen“.](../images/data-types/media-event-information.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `mediaCollection` | [!UICONTROL mediaDetails] | Informationen zu Mediendetails im Zusammenhang mit dem Erlebnisereignis. Dieser Datentyp wird sowohl für die [Mediendaten-Erfassung](./media-collection-details.md) als auch für [Mediendatenberichte](./media-reporting-details.md) verwendet. |
| `mediaEventTimestamp` | [!UICONTROL String] | Der Zeitpunkt, zu dem ein Medienereignis aufgetreten ist. |
| `mediaEventType` | [!UICONTROL String] | Der Medienereignistyp. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)
