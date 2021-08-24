---
keywords: Experience Platform; Startseite; beliebte Themen; Kantensegmentierung; Segmentierung; Segmentierungsdienst; Segmentierungsdienst; Benutzerhandbuch; Streaming-Edge;
solution: Experience Platform
title: UI-Anleitung zur Edge-Segmentierung
topic-legacy: ui guide
description: Bei der Edge-Segmentierung können Segmente in Platform sofort am Rand ausgewertet werden, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 8f2540902cdcff99627393429424dbfe1de2d3da
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 4%

---

# Handbuch zur Edge-Segmentierungs-UI (Beta)

>[!NOTE]
>
>Die Edge-Segmentierung befindet sich derzeit in der Betaphase. Die Dokumentation und Funktionalität können sich ändern.

Bei der Edge-Segmentierung können Segmente in Adobe Experience Platform sofort am Rand ausgewertet werden, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.

## Kantensegmentierungs-Abfragetypen

Eine Abfrage kann mit Kantensegmentierung ausgewertet werden, wenn sie eines der folgenden Kriterien erfüllt:

| Abfragetyp | Details | Beispiel |
| ---------- | ------- | ------- |
| Eingehender Treffer | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| Eingehender Treffer, der sich auf ein Profil bezieht | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung und ein oder mehrere Profilattribute verweist. | ![](../images/ui/edge-segmentation/profile-hit.png) |
| Eingehender Treffer mit einem Zeitfenster von 24 Stunden | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis innerhalb von 24 Stunden verweist |  |
| Eingehender Treffer, der sich auf ein Profil mit einem Zeitfenster von 24 Stunden bezieht | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis innerhalb von 24 Stunden und ein oder mehrere Profilattribute verweist. |  |

Wenn die Abfrage mit einem der oben genannten Abfragetypen übereinstimmt, wird sie automatisch mithilfe der Kantensegmentierung ausgewertet.

Die folgenden Abfragetypen werden derzeit für die Kantensegmentierung **nicht** unterstützt:

| Abfragetyp | Details |
| ---------- | ------- |
| Mehrere Ereignisse | Wenn eine Abfrage mehr als ein Ereignis enthält, kann sie nicht mithilfe der Kantensegmentierung ausgewertet werden. |
| Frequenzabfrage | Jede Segmentdefinition, die auf ein Ereignis verweist, das mindestens eine bestimmte Anzahl von Malen stattfindet. |  |
| Frequenzabfrage, die sich auf ein Profil bezieht | Jede Segmentdefinition, die auf ein Ereignis verweist, das mindestens eine bestimmte Anzahl von Malen stattfindet und mindestens ein Profilattribut aufweist. |  |

## Nächste Schritte

In diesem Benutzerhandbuch wird erläutert, wie Sie Segmente mit Kantensegmentierung in Adobe Experience Platform auswerten können.

Weitere Informationen zur Verwendung der Adobe Experience Platform-Benutzeroberfläche finden Sie im [Benutzerhandbuch zur Segmentierung](./overview.md). Weitere Informationen zum Ausführen ähnlicher Aktionen und zum Arbeiten mit Segmenten mithilfe der Adobe Experience Platform-Benutzeroberfläche finden Sie im [Handbuch zur Edge-Segmentierungs-API](../api/edge-segmentation.md).
