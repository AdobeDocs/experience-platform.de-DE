---
keywords: Experience Platform; Startseite; beliebte Themen; Kantensegmentierung; Segmentierung; Segmentierungsdienst; Segmentierungsdienst; Benutzerhandbuch; Streaming-Edge;
solution: Experience Platform
title: UI-Anleitung zur Edge-Segmentierung
topic-legacy: ui guide
description: Bei der Edge-Segmentierung können Segmente in Platform sofort am Rand ausgewertet werden, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 8375d5a35ef652335c60b4b8b4571bf42ec1924a
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 5%

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
| Frequenzabfrage | Jede Segmentdefinition, die auf ein Ereignis verweist, das mindestens eine bestimmte Anzahl von Malen stattfindet. |  |
| Frequenzabfrage, die sich auf ein Profil bezieht | Jede Segmentdefinition, die auf ein Ereignis verweist, das mindestens eine bestimmte Anzahl von Malen stattfindet und mindestens ein Profilattribut aufweist. |  |

Wenn die Abfrage mit einem der oben genannten Abfragetypen übereinstimmt, wird sie automatisch mithilfe der Kantensegmentierung ausgewertet.

Die folgenden Abfragetypen werden derzeit für die Kantensegmentierung **nicht** unterstützt:

| Abfragetyp | Details |
| ---------- | ------- |
| Relatives Zeitfenster | Wenn sich eine Abfrage auf ein Zeitfenster bezieht, kann sie nicht mithilfe der Kantensegmentierung ausgewertet werden. |
| Negation | Wenn eine Abfrage eine Negation oder ein `not` -Ereignis enthält, kann sie nicht mithilfe der Kantensegmentierung ausgewertet werden. |
| Mehrere Ereignisse | Wenn eine Abfrage mehr als ein Ereignis enthält, kann sie nicht mithilfe der Kantensegmentierung ausgewertet werden. |

## Nächste Schritte

In diesem Benutzerhandbuch wird erläutert, wie Sie Segmente mit Kantensegmentierung in Adobe Experience Platform auswerten können.

Weitere Informationen zur Verwendung der Adobe Experience Platform-Benutzeroberfläche finden Sie im [Benutzerhandbuch zur Segmentierung](./overview.md). Weitere Informationen zum Ausführen ähnlicher Aktionen und zum Arbeiten mit Segmenten mithilfe der Adobe Experience Platform-Benutzeroberfläche finden Sie im [Handbuch zur Edge-Segmentierungs-API](../api/edge-segmentation.md).
