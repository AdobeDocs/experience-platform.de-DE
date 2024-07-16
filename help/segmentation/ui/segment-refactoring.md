---
solution: Experience Platform
title: Handbuch zur umgestalteten Benutzeroberfläche für Segmentierungszeitbeschränkungen
description: Segment Builder bietet eine umfangreiche Arbeitsfläche, über die Sie mit Profildatenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag-and-Drop-Kacheln, die zur Darstellung von Dateneigenschaften dienen.
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: 665bbd1904e857336a4fb677230389d7977f6b60
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 26%

---

# Umgestaltung der Zeitbeschränkungen {#refactorization}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_constraints"
>title="Umgestaltung der Zeitbeschränkungen"
>abstract="Zeitbeschränkungen auf Regelebene und Gruppenebene wurden entfernt, um die Verwendung von Zeitbeschränkungen klarer zu gestalten. Bitte schreiben Sie Ihre Beschränkung als Zeitbegrenzung auf Arbeitsebene oder Kartenebene neu."

In der Version vom Januar 2024 für Adobe Experience Platform wurden Änderungen am Adobe Experience Platform Segmentation Service eingeführt, die neue Einschränkungen hinzufügen, für die Zeitbeschränkungen definiert werden können. Diese Änderungen wirken sich auf neu erstellte oder bearbeitete Segmente aus, die über die Benutzeroberfläche von Segment Builder vorgenommen werden. In diesem Handbuch wird erläutert, wie Sie diesen Änderungen entgegenwirken.

Vor der Version vom Januar 2024 bezogen sich alle Zeitbeschränkungen auf Regelebene, Gruppenebene und Arbeitsfläche Redundant auf denselben Zeitstempel. Um die Verwendung von Zeitbeschränkungen klarzustellen, wurden Zeitbeschränkungen auf Regel- und Gruppenebene entfernt. Um diese Änderung zu berücksichtigen, müssen alle Zeitbeschränkungen **** in Zeitbeschränkungen auf **Arbeitsflächenebene** oder **Kartenebene** umgeschrieben werden.

Zuvor konnten an ein einzelnes Ereignis mehrere Zeitbegrenzungsregeln angehängt werden. Mit dieser kürzlich erfolgten Aktualisierung führt der Versuch, einer Regel eine Zeitbeschränkung hinzuzufügen, jetzt zu einem **Fehler**.

![Die Zeitbegrenzung auf Regelebene wird hervorgehoben. Der Fehler, der anschließend auftritt, wird ebenfalls hervorgehoben. ](../images/ui/segment-refactoring/rule-time-constraint.png)

Zeitbeschränkungen können jetzt nur noch auf Arbeitsflächenebene oder auf Kartenebene angewendet werden.

Beim Anwenden einer Zeitbegrenzung auf die Arbeitsfläche können Sie weiterhin alle verfügbaren Zeitbeschränkungen auswählen.

>[!NOTE]
>
>Wenn sich auf der Arbeitsfläche nur die Karte **1} befindet, ist die Anwendung der Zeitbegrenzung auf die Karte** entspricht **, um die Zeitbegrenzung auf die Arbeitsfläche anzuwenden.**
>
>Wenn sich **mehrere** Karten auf der Arbeitsfläche befinden, wird diese Zeitbegrenzung durch Anwendung der Zeitbegrenzung auf die Arbeitsflächenebene auf **alle** Karten auf der Arbeitsfläche angewendet.

![Die Zeitbegrenzung auf Leinwandebene wird hervorgehoben.](../images/ui/segment-refactoring/canvas-time-constraint.png)

Um eine Zeitbegrenzung auf Kartenebene anzuwenden, wählen Sie die spezifische Karte aus, auf die Sie die Zeitbegrenzung anwenden möchten. Der Container **[!UICONTROL Ereignisregeln]** wird angezeigt. Sie können jetzt die Zeitbegrenzung auswählen, die Sie auf die Karte anwenden möchten.

![Die Zeitbegrenzung auf Kartenebene wird hervorgehoben.](../images/ui/segment-refactoring/card-time-constraint.png)
