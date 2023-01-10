---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segment Builder; Segment Builder
solution: Experience Platform
title: Anleitung zur überarbeiteten Segmentierungszeitbegrenzung
description: Segment Builder bietet eine umfangreiche Arbeitsfläche, über die Sie mit Profildatenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag-and-Drop-Kacheln, die zur Darstellung von Dateneigenschaften dienen.
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 11%

---

# Umkehrung von Zeitbeschränkungen

In der Version vom Oktober 2020 für Adobe Experience Platform wurden Leistungsänderungen am Adobe Experience Platform Segmentation Service eingeführt, die neue Einschränkungen für die Verwendung der logischen Operatoren &quot;OR&quot;und &quot;AND&quot;enthielten. Diese Änderungen wirken sich auf neu erstellte oder bearbeitete Segmente aus, die über die Benutzeroberfläche von Segment Builder vorgenommen werden. In diesem Handbuch wird erläutert, wie Sie diese Änderungen beheben können.

Vor der Version vom Oktober 2020 bezogen sich alle Zeitbeschränkungen auf Regelebene, Gruppenebene und Ereignisebene redundant auf denselben Zeitstempel. Um die Verwendung von Zeitbeschränkungen zu verdeutlichen, wurden Zeitbeschränkungen auf Regelebene und Gruppenebene entfernt. Um diese Änderung zu berücksichtigen, müssen alle Zeitbeschränkungen als Zeitbeschränkungen auf Ereignisebene neu geschrieben werden.

Zuvor konnten an ein einzelnes Ereignis mehrere Zeitbegrenzungsregeln angehängt werden.

![Der frühere Stil von Zeitbeschränkungen wird im Segment Builder hervorgehoben.](../images/ui/segment-refactoring/former-time-constraint.png)

Wie Sie sehen können, weist dieses Segment auf der Regelebene zwei Begrenzungen auf: Eins für &quot;[!UICONTROL Heute]&quot; und der andere für &quot;[!UICONTROL Gestern]&quot;.

Das vorherige Segment entspricht dem folgenden Segment - beide Zeitbeschränkungen auf Ereignisebene wurden über einen UND -Operator verbunden. Die erste Zeitbeschränkung auf Ereignisebene verweist auf ein Klickereignis, dessen Name &quot;Training&quot;entspricht und heute stattfindet, während die zweite Zeitbegrenzung auf Ereignisebene auf ein Klickereignis verweist, dessen Name &quot;Haustiere&quot;entspricht und gestern stattgefunden hat.

![Der neue Stil von Zeitbeschränkungen wird im Segment Builder hervorgehoben.](../images/ui/segment-refactoring/time-constraint-1.png) ![Der neue Stil von Zeitbeschränkungen wird im Segment Builder hervorgehoben.](../images/ui/segment-refactoring/time-constraint-2.png)

Diese Umgestaltung von Zeitbeschränkungen wirkt sich auch auf Zeitbeschränkungen aus, die über einen ODER-Operator verbunden werden.
