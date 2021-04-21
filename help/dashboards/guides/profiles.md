---
keywords: Experience Platform;Profil;Echtzeit-Profil von Kunden;Benutzeroberfläche;Anpassung;Profil-Dashboard;Dashboard
title: Profils-Dashboard
description: Adobe Experience Platform bietet ein Dashboard, mit dem Sie wichtige Informationen zu den Echtzeit-Daten Ihres Customer Profils in Ihrer Organisation Ansicht erhalten.
topic-legacy: guide
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 0%

---

# (Beta) [!UICONTROL Profile] Dashboard

>[!IMPORTANT]
>
>Die in diesem Dokument beschriebene Dashboard-Funktion befindet sich derzeit in der Beta-Version und steht nicht allen Benutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.

Die Adobe Experience Platform-Benutzeroberfläche (UI) bietet ein Dashboard zur Ansicht wichtiger Informationen zu Ihren [!DNL Real-time Customer Profile]-Daten, wie sie während eines täglichen Schnappschusses erfasst werden. In diesem Handbuch wird beschrieben, wie Sie auf das Dashboard [!UICONTROL Profil] in der Benutzeroberfläche zugreifen und mit ihm arbeiten, und es werden Informationen zu den im Dashboard angezeigten Metriken bereitgestellt.

Einen Überblick über alle Profil-Funktionen in der Benutzeroberfläche der Experience Platform finden Sie im Handbuch [Benutzeroberflächen-Handbuch für Kunden-Profil in Echtzeit](../../profile/ui/user-guide.md).

## Profil-Dashboard-Daten

Das Dashboard [!UICONTROL Profil] zeigt eine Momentaufnahme der Attributdaten (Datensatzdaten) an, die Ihr Unternehmen im Profil-Store in der Experience Platform hat. Der Schnappschuss enthält keine Ereignis- (Zeitreihendaten).

Die Attributdaten im Schnappschuss zeigen die Daten exakt so an, wie sie zu dem Zeitpunkt angezeigt werden, zu dem der Schnappschuss erstellt wurde. Das heißt, der Schnappschuss ist keine Näherung oder Stichprobe der Daten, und das Profil-Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Erstellung des Schnappschusses an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn der nächste Schnappschuss erstellt wurde.

## Das Dashboard [!UICONTROL Profile]

Um zum Dashboard [!UICONTROL Profil] in der Plattform-Benutzeroberfläche zu navigieren, wählen Sie **[!UICONTROL Profil]** in der linken Leiste aus und klicken Sie dann auf die Registerkarte **[!UICONTROL Übersicht]**, um das Dashboard anzuzeigen.

![](../images/profiles/dashboard-overview.png)

### Auswählen von Zusammenführungsrichtlinien

Die Metriken, die im Dashboard [!UICONTROL Profil] angezeigt werden, basieren auf Zusammenführungsrichtlinien, die auf Ihre Echtzeit-Kundendaten angewendet werden. Wenn Daten aus mehreren Quellen zusammengeführt werden, ist es möglich, dass die Daten widersprüchliche Werte enthalten (z. B. kann ein Datensatz einen Kunden als &quot;einzeln&quot;Liste haben, während ein anderer Datensatz den Kunden als &quot;verheiratet&quot;Liste), und es ist die Aufgabe der Zusammenführungsrichtlinie, zu bestimmen, welche Daten priorisiert und im Rahmen des Profils angezeigt werden sollen.

Das Dashboard wählt automatisch eine anzuzeigende Richtlinie für die Zusammenführung aus, Sie können jedoch die über das Dropdown-Menü ausgewählte Richtlinie für die Zusammenführung ändern. Um eine andere Richtlinie für die Zusammenführung auszuwählen, wählen Sie die Dropdown-Liste neben dem Namen der Zusammenführungsrichtlinie aus und wählen Sie dann die Richtlinie für die Zusammenführung aus, die Ansicht werden soll.

>[!NOTE]
>
>Das Dropdown-Menü zeigt nur Zusammenführungsrichtlinien an, die mit der XDM Individual Profil Class zusammenhängen. Wenn Ihr Unternehmen jedoch mehrere Zusammenführungsrichtlinien erstellt hat, müssen Sie möglicherweise einen Bildlauf durchführen, um die vollständige Liste der verfügbaren Zusammenführungsrichtlinien Ansicht.

Weitere Informationen zu Zusammenführungsrichtlinien, einschließlich zum Erstellen, Bearbeiten und Deklarieren einer standardmäßigen Zusammenführungsrichtlinie für Ihr Unternehmen, finden Sie im Handbuch [Zusammenführungsrichtlinien](../../profile/ui/merge-policies.md).

![](../images/profiles/select-merge-policy.png)

### Widgets und Metriken

Das Dashboard besteht aus Widgets, die schreibgeschützte Metriken sind und wichtige Informationen zu Ihren Profil-Daten enthalten. Das Datum und die Uhrzeit der letzten Aktualisierung eines Widgets werden angezeigt, wenn der letzte Schnappschuss der Daten aufgenommen wurde.

![](../images/profiles/dashboard-timestamp.png)

## Verfügbare Widgets

Experience Platform bietet mehrere Widgets, mit denen Sie verschiedene Metriken zu Ihren Profil-Daten visualisieren können. Wählen Sie unten den Namen eines Widget aus, um weitere Informationen zu erhalten:

* [[!UICONTROL Audience]](#audience-size)
* [[!UICONTROL Profile hinzugefügt]](#profiles-added)
* [[!UICONTROL Im Zeitverlauf hinzugefügte Profil]](#profiles-added-over-time)
* [[!UICONTROL Profile nach Namensraum]](#profiles-by-namespace)
* [[!UICONTROL Überschneidung von Namensräumen]](#namespace-overlap)

### [!UICONTROL Audience] {#audience-size}

Das Widget **[!UICONTROL Audience size]** zeigt die Gesamtzahl der zusammengeführten Profil im Profil-Datenspeicher zum Zeitpunkt des Snapshots an. Diese Nummer ist das Ergebnis der Anwendung der Zusammenführungsrichtlinie auf Ihre Profil-Daten, um Profil-Fragmente zu einem einzigen Profil zusammenzuführen.

Weitere Informationen zu Fragmenten und zusammengeführten Profilen finden Sie im Abschnitt *Profil-Fragmente vs. zusammengeführte Profil* des [Kundenüberblickes ](../../profile/home.md)Echtzeit-Profils.

>[!NOTE]
>
>Die zur Berechnung dieser Metrik verwendete Mergerichtlinie ist nicht mit der systemgenerierten Mergerichtlinie identisch, die zur Berechnung von [!UICONTROL Addressable Audiencen] im [!UICONTROL License usage]-Dashboard verwendet wird. Daher ist es unwahrscheinlich, dass die Audience in den Dashboards [!UICONTROL Profil] und [!UICONTROL License usage] genau gleich ist.

![](../images/profiles/audience-size.png)

### [!UICONTROL Profile hinzugefügt] {#profiles-added}

Das Widget **[!UICONTROL Hinzugefügte Profil]** zeigt die Gesamtanzahl der zusammengeführten Profil an, die dem Profil-Datenspeicher seit der letzten Momentaufnahme hinzugefügt wurden. Diese Nummer ist das Ergebnis der Anwendung der Zusammenführungsrichtlinie auf Ihre Profil-Daten, um Profil-Fragmente zu einem einzigen Profil zusammenzuführen.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Im Zeitverlauf hinzugefügte Profil] {#profiles-added-over-time}

Das Widget **[!UICONTROL Profil, die im Laufe der Zeit hinzugefügt werden]** zeigt die Gesamtanzahl der zusammengeführten Profil an, die in den letzten 30 Tagen täglich zum Datenspeicher des Profils hinzugefügt wurden. Diese Nummer wird jeden Tag aktualisiert, an dem der Schnappschuss erstellt wird. Wenn Sie also Profil in die Plattform aufnehmen möchten, wird die Anzahl der Profil erst angezeigt, wenn der nächste Schnappschuss erstellt wurde.

Die Anzahl der hinzugefügten Profil ist das Ergebnis der Anwendung der jeweiligen Zusammenführungsrichtlinie auf Ihre Profil-Daten, um Profil-Fragmente zu einem einzelnen Profil zusammenzuführen.

![](../images/profiles/profiles-added-over-time.png)

### [!UICONTROL Profile nach Namensraum] {#profiles-by-namespace}

Das Widget **[!UICONTROL Profil nach Namensraum]** zeigt die Aufschlüsselung der Identitäts-Namensraum für alle zusammengeführten Profil in Ihrem Profil-Store an. Die Gesamtanzahl der Profil nach [!UICONTROL ID-Namensraum] (d. h. das Addieren der für jeden Namensraum angezeigten Werte) kann höher sein als die Gesamtanzahl der zusammengeführten Profil, da einem Profil mehrere Namensraum zugeordnet sein können. Wenn ein Kunde beispielsweise auf mehr als einem Kanal mit Ihrer Marke interagiert, werden mehrere Namensraum mit diesem Kunden verknüpft.

Weitere Informationen zu Identitäts-Namensräumen finden Sie in der [Adobe Experience Platform Identity Service-Dokumentation](../../identity-service/home.md).

![](../images/profiles/profiles-by-namespace.png)

### [!UICONTROL Überschneidung von Namensräumen] {#namespace-overlap}

Das Widget **[!UICONTROL Überschneidung von Namensräumen]** zeigt ein Venn-Diagramm oder ein Set-Diagramm an, das die Überschneidung von Profilen in Ihrem Profil-Store mit mehreren Identitäts-Namensräumen anzeigt.

Nachdem Sie die zu vergleichenden Identitäts-Namensraum mithilfe der Dropdown-Menüs im Widget ausgewählt haben, werden Kreise mit der relativen Größe der einzelnen Namensraum angezeigt, wobei die Anzahl der Profil, die beide Namensraum enthalten, durch die Größe der Überschneidung zwischen den Kreisen dargestellt wird.

Wenn ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden mehrere Namensraum mit diesem Kunden verknüpft. Daher ist es wahrscheinlich, dass Ihr Unternehmen über mehrere Profil mit Fragmenten aus mehr als einem Identitäts-Namensraum verfügt.

Weitere Informationen zu Identitäts-Namensräumen finden Sie in der [Adobe Experience Platform Identity Service-Dokumentation](../../identity-service/home.md).

![](../images/profiles/namespace-overlap.png)

## Nächste Schritte

Indem Sie diesem Dokument folgen, sollten Sie nun in der Lage sein, das Dashboard &quot;Profil&quot;zu finden und die Metriken zu verstehen, die in den verfügbaren Widgets angezeigt werden. Weitere Informationen zum Arbeiten mit [!DNL Profile]-Daten in der Benutzeroberfläche &quot;Experience Platform&quot;finden Sie im Handbuch [Benutzeroberflächen-Handbuch für Kunden-Profil in Echtzeit](../../profile/ui/user-guide.md).
