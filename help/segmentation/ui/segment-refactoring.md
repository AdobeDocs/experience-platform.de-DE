---
keywords: Experience Platform;Startseite;beliebte Themen;Segmentierung;segmentierung;Segment Builder;segment builder
solution: Experience Platform
title: Handbuch zur umgestalteten Benutzeroberfläche für Segmentierungszeitbeschränkungen
description: Segment Builder bietet eine umfangreiche Arbeitsfläche, über die Sie mit Profildatenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag-and-Drop-Kacheln, die zur Darstellung von Dateneigenschaften dienen.
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 100%

---

# Umgestaltung der Zeitbeschränkungen

In der Adobe Experience Platform-Version vom Oktober 2020 wurden Leistungsänderungen für Adobe Experience Platform Segmentation Service eingeführt, die neue Einschränkungen bei Verwendung der logischen Operatoren „OR“ und „AND“ umfassen. Diese Änderungen wirken sich auf über die Benutzeroberfläche von Segment Builder neu erstellte oder bearbeitete Segmente aus. In diesem Handbuch wird erläutert, wie Sie diesen Änderungen entgegenwirken.

Vor der Version vom Oktober 2020 bezogen sich alle Zeitbeschränkungen auf Regel-, Gruppen- und Ereignisebene redundant auf denselben Zeitstempel. Um die Verwendung von Zeitbeschränkungen klarzustellen, wurden Zeitbeschränkungen auf Regel- und Gruppenebene entfernt. Um dieser Änderung Rechnung zu tragen, müssen alle Zeitbeschränkungen neu als Zeitbeschränkungen auf Ereignisebene geschrieben werden.

Zuvor konnten einem einzelnen Ereignis mehrere Zeitbeschränkungsregeln beigefügt werden.

![Der frühere Stil von Zeitbeschränkungen ist in Segment Builder hervorgehoben.](../images/ui/segment-refactoring/former-time-constraint.png)

Wie zu sehen ist, weist dieses Segment auf der Regelebene zwei Beschränkungen auf: eine für „[!UICONTROL Heute]“ und die andere für „[!UICONTROL Gestern]“.

Das vorherige Segment entspricht dem folgenden Segment – beide Zeitbeschränkungen auf Ereignisebene wurden über einen AND-Operator verbunden. Die erste Zeitbeschränkung auf Ereignisebene verweist auf ein Klickereignis, dessen Name „Training“ lautet und heute stattfindet, während die zweite Zeitbeschränkung auf Ereignisebene auf ein Klickereignis verweist, dessen Name „Haustiere“ lautet und gestern stattgefunden hat.

![Der neue Stil von Zeitbeschränkungen ist in Segment Builder hervorgehoben.](../images/ui/segment-refactoring/time-constraint-1.png) ![Der neue Stil von Zeitbeschränkungen ist in Segment Builder hervorgehoben.](../images/ui/segment-refactoring/time-constraint-2.png)

Diese Umgestaltung der Zeitbeschränkungen wirkt sich auch auf Zeitbeschränkungen aus, die über einen OR-Operator verbunden werden.
