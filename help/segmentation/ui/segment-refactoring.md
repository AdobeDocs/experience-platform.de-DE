---
keywords: Experience Platform;Startseite;beliebte Themen;Segmentierung;Segmentierung;Segmentaufbau;Segmentaufbau
solution: Experience Platform
title: Handbuch zu Einschränkungen der Segmentierungszeit in der Benutzeroberfläche
topic-legacy: ui guide
description: Segment Builder bietet eine umfangreiche Arbeitsfläche, über die Sie mit Profildatenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag-and-Drop-Kacheln, die zur Darstellung von Dateneigenschaften dienen.
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 13%

---

# Umkehrung von Zeitbeschränkungen

Die Version von Oktober 2020 für Adobe Experience Platform hat Leistungsänderungen am Adobe Experience Platform Segmentation Service eingeführt, die neue Einschränkungen für die Verwendung der logischen Operatoren &quot;OR&quot;und &quot;AND&quot;enthalten. Diese Änderungen wirken sich auf neu erstellte oder bearbeitete Segmente aus, die mithilfe der Segment Builder-Benutzeroberfläche vorgenommen werden. In diesem Handbuch wird erläutert, wie diese Änderungen eingedämmt werden können.

Vor der Version vom Oktober 2020 bezogen sich alle Zeitbeschränkungen auf Regelebene, Gruppenebene und Ereignis Redundant auf denselben Zeitstempel. Um die Verwendung von Zeitbeschränkungen zu klären, wurden Zeitbeschränkungen auf Regelebene und Gruppenebene entfernt. Um dieser Änderung Rechnung zu tragen, müssen alle Zeitbeschränkungen als Zeitbeschränkungen auf Ereignis-Ebene umgeschrieben werden.

Zuvor wurden an ein einzelnes Ereignis mehrere Zeitbeschränkungsregeln angehängt.

![](../images/ui/segment-refactoring/former-time-constraint.png)

Wie Sie sehen können, unterliegt dieses Segment auf Regelebene zwei Einschränkungen: Eine für &quot;[!UICONTROL Today]&quot;und die andere für &quot;[!UICONTROL Gestern]&quot;.

Das vorherige Segment entspricht dem folgenden Segment — Beide Zeitbeschränkungen auf Ereignis-Ebene wurden mit einem UND-Operator verbunden. Die erste Zeitbeschränkung auf Ereignis-Ebene verweist auf ein click-Ereignis, dessen Name gleich &quot;Schulung&quot;ist und das heute stattfindet, während die zweite Zeitbeschränkung auf Ereignis-Ebene auf ein click-Ereignis verweist, dessen Name &quot;Haustiere&quot;entspricht und gestern stattgefunden hat.

![](../images/ui/segment-refactoring/time-constraint-1.png) ![](../images/ui/segment-refactoring/time-constraint-2.png)

Diese Umgestaltung von Zeitbeschränkungen wirkt sich auch auf Zeitbeschränkungen aus, die mit einem ODER-Operator verbunden werden.
