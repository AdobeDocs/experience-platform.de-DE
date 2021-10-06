---
keywords: Experience Platform; Startseite; beliebte Themen; Kantensegmentierung; Segmentierung; Segmentierungsdienst; Segmentierungsdienst; Benutzerhandbuch; Streaming-Edge;
solution: Experience Platform
title: UI-Anleitung zur Edge-Segmentierung
topic-legacy: ui guide
description: Bei der Edge-Segmentierung können Segmente in Platform sofort am Rand ausgewertet werden, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 6bb1f417b5856f153adebe4deaac4fab264ef3a8
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 4%

---

# Handbuch zur Edge-Segmentierungs-UI (Beta)

>[!IMPORTANT]
>
>Die Edge-Segmentierung befindet sich derzeit in der Betaphase. Die Dokumentation und Funktionalität können sich ändern.

Bei der Edge-Segmentierung können Segmente in Adobe Experience Platform sofort [am Rand](../../edge/home.md) ausgewertet werden, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.

## Kantensegmentierungs-Abfragetypen

Derzeit können nur ausgewählte Abfragetypen mit Kantensegmentierung ausgewertet werden. Die folgenden Abschnitte enthalten eine Liste von Abfragetypen, die mit der Kantensegmentierung ausgewertet werden können und die derzeit nicht unterstützt werden.

### Unterstützte Abfragetypen

Eine Abfrage kann mit Kantensegmentierung ausgewertet werden, wenn sie eines der in der folgenden Tabelle aufgeführten Kriterien erfüllt.

>[!NOTE]
>
>Wenn die Abfrage mit einem der Abfragetypen in der folgenden Tabelle übereinstimmt, wird sie automatisch mithilfe der Kantensegmentierung ausgewertet. Das System bestimmt diese Fähigkeit automatisch anhand des Abfrageausdrucks.

| Abfragetyp | Details | Beispiel |
| ---------- | ------- | ------- |
| Eingehender Treffer | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| Eingehender Treffer, der sich auf ein Profil bezieht | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung und ein oder mehrere Profilattribute verweist. | ![](../images/ui/edge-segmentation/profile-hit.png) |
| Eingehender Treffer mit einem Zeitfenster von 24 Stunden | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis innerhalb von 24 Stunden verweist |  |
| Eingehender Treffer, der sich auf ein Profil mit einem Zeitfenster von 24 Stunden bezieht | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis innerhalb von 24 Stunden und ein oder mehrere Profilattribute verweist. |  |

### Derzeit nicht unterstützte Abfragetypen

Die folgenden Abfragetypen werden derzeit für die Kantensegmentierung **nicht** unterstützt:

| Abfragetyp | Details |
| ---------- | ------- |
| Mehrere Ereignisse | Wenn eine Abfrage mehr als ein Ereignis enthält, kann sie nicht mithilfe der Kantensegmentierung ausgewertet werden. |
| Frequenzabfrage | Jede Segmentdefinition, die auf ein Ereignis verweist, das mindestens eine bestimmte Anzahl von Malen stattfindet. |  |
| Frequenzabfrage, die sich auf ein Profil bezieht | Jede Segmentdefinition, die auf ein Ereignis verweist, das mindestens eine bestimmte Anzahl von Malen stattfindet und mindestens ein Profilattribut aufweist. |  |

## Nächste Schritte

In diesem Handbuch wird erläutert, wie Segmente mit Kantensegmentierung in Adobe Experience Platform ausgewertet werden. Weitere Informationen zur Verwendung der Experience Platform-Benutzeroberfläche finden Sie im [Benutzerhandbuch zur Segmentierung](./overview.md). Weitere Informationen zum Ausführen ähnlicher Aktionen und zum Arbeiten mit Segmenten mithilfe von Experience Platform-APIs finden Sie im [Handbuch zur Edge-Segmentierungs-API](../api/edge-segmentation.md).
