---
keywords: Experience Platform;profile;real-time customer profile;user interface;UI;customization;profile dashboard;dashboard
title: Profil-Dashboard
description: 'In diesem Handbuch wird das Echtzeit-Dashboard für Kundendaten in der Adobe Experience Platform-Benutzeroberfläche beschrieben. '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 983b357f2f17aad273f0465dc9250240a062dcd2
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 1%

---


# (Alpha) [!DNL Real-time Customer Profile] Dashboard {#profile-dashboard}

>[!IMPORTANT]
>
>Die in diesem Dokument beschriebene Dashboard-Funktion ist derzeit alphanumerisch und steht nicht allen Benutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.

Die Adobe Experience Platform-Benutzeroberfläche (UI) bietet ein Dashboard, mit dem Sie wichtige Informationen zu Ihren [!DNL Real-time Customer Profile] Daten, wie sie in einem täglichen Schnappschuss erfasst werden, Ansicht haben. In diesem Handbuch wird beschrieben, wie Sie auf das [!DNL Profile] Dashboard in der Benutzeroberfläche zugreifen und mit ihm arbeiten, und es werden weitere Informationen zu den im Dashboard angezeigten Metriken bereitgestellt.

Einen Überblick über alle Profil-Funktionen in der Benutzeroberfläche der Experience Platform finden Sie im Handbuch für die Benutzeroberfläche des [Echtzeit-Profils](user-guide.md).

## Profil-Dashboard-Daten

Das Profil-Dashboard zeigt eine Momentaufnahme der Attributdaten (Datensatzdaten) an, die Ihr Unternehmen im Profil-Store in der Experience Platform hat. Der Schnappschuss enthält keine Ereignis- (Zeitreihendaten).

Die Attributdaten im Schnappschuss zeigen die Daten exakt so an, wie sie zu dem Zeitpunkt angezeigt werden, zu dem der Schnappschuss erstellt wurde. Das heißt, der Schnappschuss ist keine Näherung oder Stichprobe der Daten, und das Profil-Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Erstellung des Schnappschusses an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn der nächste Schnappschuss erstellt wurde.

Die im Profil-Dashboard angezeigten Metriken basieren auf der standardmäßigen Zusammenführungsrichtlinie für Ihr Unternehmen. Weitere Informationen zu Zusammenführungsrichtlinien und dazu, wie Sie Ihre standardmäßige Zusammenführungsrichtlinie auswählen oder ändern können, finden Sie im UI-Handbuch zu [Zusammenführungsrichtlinien](merge-policies.md).

## Profil-Dashboard

Um zum Profil-Dashboard in der Plattform-Benutzeroberfläche zu navigieren, wählen Sie in der linken Leiste die Option &quot; **[!UICONTROL Profil]** &quot;und wählen Sie dann die Registerkarte &quot; **[!UICONTROL Übersicht]** &quot;aus, um das Dashboard anzuzeigen.

![](../images/profile-dashboard/dashboard-overview.png)

### Widgets und Metriken

Das Dashboard besteht aus Widgets, die schreibgeschützte Metriken sind und wichtige Informationen zu Ihren Profil-Daten enthalten. Das Datum und die Uhrzeit der letzten Aktualisierung im Widget werden angezeigt, wenn der letzte Schnappschuss der Daten aufgenommen wurde.

![](../images/profile-dashboard/dashboard-timestamp.png)

## Verfügbare Widgets

Experience Platform bietet mehrere Widgets, mit denen Sie verschiedene Metriken zu Ihren Profil-Daten visualisieren können. Wählen Sie unten den Namen eines Widget aus, um weitere Informationen zu erhalten:

* [[!UICONTROL Audience]](#audience-size)
* [[!UICONTROL Profile nach Namensraum]](#profiles-by-namespace)

### [!UICONTROL Audience] {#audience-size}

Das Widget zur Größe **[!UICONTROL der]** Audience zeigt die Gesamtzahl der zusammengeführten Profil im Profil-Datenspeicher zum Zeitpunkt des Snapshots an. Diese Nummer ist das Ergebnis der Anwendung der standardmäßigen Zusammenführungsrichtlinie Ihres Unternehmens auf Ihre Profil-Daten, um Profil-Fragmente zu einem einzelnen Profil zusammenzuführen.

Weitere Informationen zu Fragmenten und zusammengeführten Profilen finden Sie im Abschnitt [Profil-Fragmente und zusammengeführte Profile](../home.md#profile-fragments-vs-merged-profiles) in der Übersicht über das [Profil](../home.md).

![](../images/profile-dashboard/audience-size.png)

### [!UICONTROL Profile nach Namensraum] {#profiles-by-namespace}

Das Widget &quot; **[!UICONTROL Profil nach Namensraum]** &quot;zeigt die Aufschlüsselung der Namensraum für alle zusammengeführten Profil in Ihrem Profil-Store an. Die Gesamtanzahl der Profil nach [!UICONTROL ID-Namensraum] (d. h. das Addieren der für jeden Namensraum angezeigten Werte) ist immer höher als die Gesamtanzahl der zusammengeführten Profil, da ein Profil mehrere Namensraum mit diesem verknüpft sein könnte. Wenn ein Kunde beispielsweise auf mehr als einem Kanal mit Ihrer Marke interagiert, werden mehrere Namensraum mit diesem Kunden verknüpft.

Weitere Informationen zu Identitäts-Namensräumen finden Sie in der Dokumentation zum [Adobe Experience Platform-Identitätsdienst](../../identity-service/home.md).

![](../images/profile-dashboard/profiles-by-namespace.png)

## Zusätzliche Dashboards

Die Plattform-Benutzeroberfläche bietet zusätzliche Dashboards zum Anzeigen von Momentaufnahmen Ihrer Daten in der Experience Platform. Zu diesen Dashboards gehören die Segmentierung und die Lizenznutzung. Weitere Informationen zu diesen zusätzlichen Dashboards finden Sie unter den folgenden Links:

* [Segment-Dashboard](../../segmentation/ui/segment-dashboard.md)
* [Dashboard zur Lizenzverwendung](../../landing/license-usage-dashboard.md)

## Nächste Schritte

Indem Sie diesem Dokument folgen, sollten Sie jetzt in der Lage sein, das Profil-Dashboard zu finden und die Metriken zu verstehen, die in den verfügbaren Widgets angezeigt werden. Weitere Informationen zum Arbeiten mit [!DNL Profile] Daten in der Benutzeroberfläche der Experience Platform finden Sie im [[!DNL Profile] UI-Handbuch](user-guide.md).