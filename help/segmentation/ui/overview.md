---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierungsdienst; Segmentierung; Segmentierungsdienst; Benutzerhandbuch; Benutzerhandbuch; Handbuch zur Segmentierung; Segmentierungs-UI; Segment Builder; Segment Builder; realisiert; vorhandene; Beenden;
solution: Experience Platform
title: Handbuch zur Benutzeroberfläche des Segmentierungsdienstes
topic-legacy: ui guide
description: Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche zum Erstellen und Verwalten von Segmentdefinitionen.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 71741a18c99a003e6401bc324822d50a266350b3
workflow-type: tm+mt
source-wordcount: '1746'
ht-degree: 19%

---

# Handbuch zur Benutzeroberfläche des Segmentierungsdienstes

[!DNL Adobe Experience Platform Segmentation Service] bietet eine Benutzeroberfläche zum Erstellen und Verwalten von Segmentdefinitionen.

## Erste Schritte

Die Arbeit mit Segmentdefinitionen erfordert ein Verständnis der verschiedenen [!DNL Experience Platform] Dienste, die mit der Segmentierung verbunden sind. Bevor Sie dieses Benutzerhandbuch lesen, lesen Sie bitte die Dokumentation für folgende Dienste:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] ermöglicht die Aufteilung der in [!DNL Experience Platform] die sich auf Einzelanwender (wie Kunden, Interessenten, Benutzer oder Organisationen) in kleinere Gruppen bezieht.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Ermöglicht die Erstellung von Kundenprofilen durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, in die erfasst wird [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Platform] organisiert werden. Um die Segmentierung optimal zu nutzen, stellen Sie bitte sicher, dass Ihre Daten als Profile und Ereignisse gemäß dem [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md).

Außerdem sollten Sie zwei Schlüsselbegriffe kennen, die in diesem Dokument verwendet werden, und den Unterschied zwischen ihnen verstehen:
- **Segmentdefinition**: Der Regelsatz, der zur Beschreibung wichtiger Merkmale oder Verhaltensweisen einer Zielgruppe verwendet wird.
- **Audience**: Der resultierende Satz von Profilen, die den Kriterien einer Segmentdefinition entsprechen.

## Übersicht

Wählen Sie in der Benutzeroberfläche &quot;Experience Platform&quot;die Option **[!UICONTROL Segmente]** im linken Navigationsbereich, um die **[!UICONTROL Übersicht]** Registerkarte mit den [!UICONTROL Segmente] Dashboard.

>[!NOTE]
>
>Wenn Ihr Unternehmen neu bei Platform ist und noch keine aktiven Profildatensätze oder Zusammenführungsrichtlinien erstellt wurden, wird die [!UICONTROL Segmente] Das Dashboard ist nicht sichtbar. Stattdessen wird die [!UICONTROL Übersicht] enthält Links und Dokumentation, die Ihnen bei den ersten Schritten mit Segmenten helfen.

### [!UICONTROL Segment-Dashboard] {#segments-dashboard}

Die **[!UICONTROL Segmente]** Im Dashboard werden Schlüsselmetriken im Zusammenhang mit den Segmentdaten Ihres Unternehmens beschrieben.

Weitere Informationen finden Sie unter [Segment-Dashboard-Handbuch](../../dashboards/guides/segments.md).

![](../../dashboards/images/segments/dashboard-overview.png)

## Durchsuchen {#browse}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_churncolumnname"
>title="Abwanderung"
>abstract="Die Abwanderung stellt den Prozentsatz der Profile dar, die sich innerhalb einer Segmentdefinition ändern, verglichen mit dem letzten Ausführen des Segmentauftrags."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_evaluationmethodcolumnname"
>title="Auswertungsmethode"
>abstract="Zu den Auswertungsmethoden für Segmente gehören Batch, Streaming und Edge."

Wählen Sie die **[!UICONTROL Durchsuchen]** um eine Liste aller Segmentdefinitionen für Ihre IMS-Organisation anzuzeigen.

![](../images/ui/overview/segment-browse-all.png)

Diese Ansicht listet Informationen zur Segmentdefinition auf, einschließlich Aufschlüsselung, Abwanderung, Anzahl der Profile, Auswertungsmethode, Erstellungsdatum und Datum der letzten Änderung.

Die Aufschlüsselung zeigt ein Balkendiagramm, in dem der Prozentsatz der Profile, die zu den folgenden Status gehören, dargestellt wird: [!UICONTROL Realisiert], [!UICONTROL Bestehend]und [!UICONTROL Beenden]. Außerdem wird die Aufschlüsselung auf der Seite [!UICONTROL Durchsuchen] -Tab ist die genaueste Aufschlüsselung des Segmentstatus. Wenn sich diese Zahl von der auf der [!UICONTROL Übersicht] verwenden, sollten Sie die Zahlen im [!UICONTROL Durchsuchen] als richtige Informationsquelle angeben, da die Variable [!UICONTROL Übersicht] Die Tabulatornummern werden nur einmal pro Tag aktualisiert.

![](../images/ui/overview/segment-browse-breakdown.png)

| Status | Beschreibung |
| ------ | ----------- |
| Realisiert | Ein neues Profil innerhalb des Segments. |
| Bestehend | Ein vorhandenes Profil, das innerhalb des Segments verbleibt. |
| Beenden | Ein vorhandenes Profil, das das Segment verlässt. |

Die Abwanderung stellt den Prozentsatz der Profile dar, die sich innerhalb einer Segmentdefinition ändern, im Vergleich zum letzten Ausführen des Segmentauftrags, während die Profilanzahl die Gesamtanzahl der Profile darstellt, die sich für das Segment qualifizieren.

Die Auswertungsmethode kann entweder Streaming, Batch oder Edge sein. Streaming-Segmente werden konstant ausgewertet, sobald Daten in das System strömen. Batch-Segmente werden gemäß einem festgelegten Zeitplan ausgewertet. Edge-Segmente werden in Echtzeit ausgewertet, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.

![](../images/ui/overview/segment-browse-segments.png)

Am oberen Rand der Seite finden Sie Optionen zum Hinzufügen aller Segmente zu einem Zeitplan und zum Erstellen eines neuen Segments.

Umschalten **[!UICONTROL Alle Segmente zur Planung hinzufügen]** aktiviert die geplante Segmentierung. Weitere Informationen zur geplanten Segmentierung finden Sie im Abschnitt [Abschnitt zur geplanten Segmentierung dieses Benutzerhandbuchs](#scheduled-segmentation).

Auswählen **[!UICONTROL Segment erstellen]** gelangen Sie zum Segment Builder. Weitere Informationen zum Erstellen von Segmenten finden Sie im Abschnitt unter [Erstellen eines Segments im Benutzerhandbuch](#create-segment).

![](../images/ui/overview/segment-browse-top.png)

Die rechte Seitenleiste enthält Informationen zu allen Segmenten innerhalb der IMS-Organisation, listet die Gesamtanzahl der Segmente, das letzte Auswertungsdatum, das nächste Auswertungsdatum sowie eine Aufschlüsselung der Segmente nach Bewertungsmethode auf.

![](../images/ui/overview/segment-browse-segment-info.png)

Die Auswahl der Zeile der Segmentdefinition bietet eine Zusammenfassung der Segmentdefinition, einschließlich Optionen zum Bearbeiten oder Löschen des Segments, zum Aktivieren des Segments für ein Ziel, der qualifizierten Zielgruppe für das Segment, der Gesamtgröße der Zielgruppe, zusätzlich zum Namen, der Beschreibung, der Auswertungsmethode, dem erstellten Datum und dem Datum der letzten Änderung.

>[!NOTE]
>
> Sie werden **not** ein Segment löschen können, das in einer Zielaktivierung verwendet wird.

![](../images/ui/overview/segment-browse-details.png)

## Details zur Segmentdefinition {#segment-details}

Um weitere Details zu einer bestimmten Segmentdefinition anzuzeigen, wählen Sie den Namen eines Segments in der **[!UICONTROL Durchsuchen]** Registerkarte.

Die Seite mit den Segmentdetails wird angezeigt. Oben finden Sie eine Zusammenfassung der Segmentdefinition, Informationen zur qualifizierten Zielgruppengröße sowie Ziele, für die das Segment aktiviert wird.

![](../images/ui/overview/segment-details-summary.png)

### Segmentzusammenfassung

Die **[!UICONTROL Segmentzusammenfassung]** enthält Informationen wie die ID, den Namen, die Beschreibung und Details der Attribute.

Darüber hinaus haben Sie die Möglichkeit, das Segment entweder für ein Ziel zu aktivieren oder es zu bearbeiten. Auswählen **[!UICONTROL Auf Ziel aktivieren]** können Sie das Segment für ein Ziel aktivieren. Detaillierte Informationen zum Aktivieren eines Segments für ein Ziel finden Sie im Abschnitt [Aktivierungsübersicht](../../destinations/ui/activation-overview.md).

![](../images/ui/overview/segment-details-activate.png)

Auswählen **[!UICONTROL Segment bearbeiten]** bringen Sie zum [!DNL Segment Builder]. Detaillierte Informationen zur Verwendung der [!DNL Segment Builder] Arbeitsbereich, lesen Sie bitte die [[!DNL Segment Builder] Benutzerhandbuch](./segment-builder.md).

![](../images/ui/overview/segment-details-edit-segment.png)

### Gesamtzielgruppe im Segment

Die **[!UICONTROL Gesamtzielgruppe im Segment]** zeigt die Gesamtzahl der Profile an, die für das Segment qualifiziert sind.

Schätzungen werden anhand einer Stichprobengröße der Beispieldaten dieses Tages erstellt. Wenn sich in Ihrem Profilspeicher weniger als 1 Million Entitäten befinden, wird der vollständige Datensatz verwendet. Bei zwischen 1 und 20 Millionen Entitäten werden 1 Million Entitäten verwendet; bei mehr als 20 Millionen Entitäten werden 5 % der Gesamtentitäten genutzt. Weiterführende Informationen zum Generieren von Segmentschätzungen finden Sie in der Anleitung zur Segmenterstellung im Abschnitt zum [Generieren von Schätzungen](../tutorials/create-a-segment.md#estimate-and-preview-an-audience).

### Aktivierte Ziele

Die **[!UICONTROL Aktivierte Ziele]** zeigt die Ziele an, für die dieses Segment aktiviert ist.

>[!NOTE]
>
> Ziele sind eine Funktion, die mit [!DNL Real-time Customer Data Platform]und ermöglichen Ihnen den Export von Daten in externe Plattformen. Weitere Informationen zu Zielen finden Sie im Abschnitt [Ziele - Übersicht](../../destinations/home.md). Informationen zum Aktivieren eines Segments für ein Ziel finden Sie unter [Aktivierungsübersicht](../../destinations/ui/activation-overview.md).

### Profilbeispiele

Darunter finden Sie eine Auswahl von Profilen, die für das Segment qualifiziert sind, mit detaillierten Informationen, einschließlich der [!DNL Profile] ID, Vorname, Nachname und persönliche E-Mail-Adresse.

Die Art und Weise, wie das Sampling von Daten ausgelöst wird, hängt von der Erfassungsmethode ab.

Für die Batch-Erfassung wird der Profilspeicher automatisch alle fünfzehn Minuten überprüft, um festzustellen, ob ein neuer Batch seit der letzten Sampling-Ausführung erfolgreich erfasst wurde. Ist dies der Fall, wird der Profilspeicher daraufhin überprüft, um festzustellen, ob sich die Anzahl der Datensätze um mindestens 5 % geändert hat. Wenn diese Bedingungen erfüllt sind, wird ein neuer Sampling-Auftrag ausgelöst.

Für die Streaming-Erfassung wird der Profilspeicher automatisch stündlich gescannt, um festzustellen, ob sich die Anzahl der Datensätze um mindestens 5 % geändert hat. Wenn diese Bedingung erfüllt ist, wird ein neuer Sampling-Auftrag ausgelöst.

Die Stichprobengröße der Prüfung hängt von der Gesamtanzahl der Entitäten in Ihrem Profilspeicher ab. Diese Stichprobengrößen werden in der folgenden Tabelle dargestellt:

| Entitäten im Profilspeicher | Stichprobengröße |
| ------------------------- | ----------- |
| Weniger als 1 Million | Vollständiger Datensatz |
| 1 bis 20 Mio. | 1 Mio. |
| Über 20 Millionen | 5 % des Gesamtbetrags |

Detailliertere Informationen zu den einzelnen [!DNL Profile] angezeigt werden, indem Sie die [!DNL Profile] Kennung. Weitere Informationen zu Profildetails finden Sie im [[!DNL Real-time Customer Profile] Benutzerhandbuch](../../profile/ui/user-guide.md#profile-detail).

![](../images/ui/overview/segment-details-profiles.png)

## Erstellen eines Segments {#create-segment}

Auswählen **[!UICONTROL Segment erstellen]** in der oberen rechten Ecke öffnet sich das [!DNL Segment Builder] Arbeitsbereich, in dem Sie mit der Erstellung einer Segmentdefinition beginnen können.

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] Arbeitsbereich

[!DNL Segment Builder] bietet einen umfassenden Arbeitsbereich, in dem Sie mit [!DNL Profile] Datenelemente. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag-and-Drop-Kacheln, die zur Darstellung von Dateneigenschaften dienen.

Detaillierte Informationen zur Verwendung der [!DNL Segment Builder] Arbeitsbereich, lesen Sie bitte die [[!DNL Segment Builder] Benutzerhandbuch](./segment-builder.md).

![](../images/ui/overview/segment-builder.png)

## Geplante Segmentierung {#scheduled-segmentation}

Nachdem Sie Segmentdefinitionen erstellt haben, können Sie diese durch eine On-Demand- oder geplante (kontinuierliche) Auswertung auswerten. Auswertung bedeutet Verschieben [!DNL Real-time Customer Profile] Daten durch Segmentdefinitionen verwenden, um entsprechende Zielgruppen zu erstellen. Nach der Erstellung werden die Audiences gespeichert, sodass sie exportiert werden können mit [!DNL Experience Platform] APIs.

Bei der On-Demand-Auswertung wird die API zur Durchführung von Auswertungen und zum Aufbau von Zielgruppen nach Bedarf verwendet. Bei der geplanten Auswertung (auch „geplante Segmentierung“ genannt) können Sie hingegen einen Zeitplan erstellen, um die Segmentdefinitionen zu einem bestimmten Zeitpunkt (maximal einmal täglich) auszuwerten.

### Geplante Segmentierung aktivieren {#enable-scheduled-segmentation}

Die Aktivierung Ihrer Segmentdefinitionen für eine geplante Auswertung kann über die Benutzeroberfläche oder die API erfolgen. Kehren Sie in der Benutzeroberfläche zum **[!UICONTROL Durchsuchen]** Registerkarte innerhalb **[!UICONTROL Segmente]** und aktivieren **[!UICONTROL Alle Segmente zur Planung hinzufügen]**. Dadurch werden alle Segmente anhand des von Ihrer Organisation festgelegten Zeitplans evaluiert.

>[!NOTE]
>
>Die geplante Auswertung kann für Sandboxes mit maximal fünf (5) Zusammenführungsrichtlinien für [!DNL XDM Individual Profile]. Wenn Ihr Unternehmen mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] in einer Sandbox-Umgebung können Sie keine geplante Auswertung verwenden.

Zeitpläne können derzeit nur mit der API erstellt werden. Ausführliche Anweisungen zum Erstellen, Bearbeiten und Verwenden von Zeitplänen mithilfe der API finden Sie im Tutorial zum Auswerten und Aufrufen von Segmentergebnissen, insbesondere im Abschnitt zur [geplanten Auswertung mithilfe der API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## Streaming-Segmentierung  {#streaming-segmentation}

Streaming-Segmentierung ist die Möglichkeit, die Segmentierung für [!DNL Platform] nahezu in Echtzeit, wobei der Schwerpunkt auf Datenreichweite liegt. Mit Streaming-Segmentierung erfolgt die Segmentqualifizierung jetzt, wenn Daten eingehen in [!DNL Platform], wodurch Segmentierungsaufträge einfacher geplant und ausgeführt werden müssen.

Weitere Informationen zur Streaming-Segmentierung finden Sie im Abschnitt [Benutzerhandbuch zur Streaming-Segmentierung](./streaming-segmentation.md).

>[!NOTE]
>
>Damit Streaming-Segmentierung funktioniert, müssen Sie die geplante Segmentierung für die Organisation aktivieren. Weitere Informationen zur Aktivierung der geplanten Segmentierung finden Sie unter [den Abschnitt zur Streaming-Segmentierung in diesem Benutzerhandbuch](#scheduled-segmentation).

## Edge-Segmentierung {#edge-segmentation}

Bei der Edge-Segmentierung können Segmente in Platform sofort am Rand ausgewertet werden, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.

Weitere Informationen zur Kantensegmentierung finden Sie im Abschnitt [Handbuch zur Edge-Segmentierungsbenutzeroberfläche](./edge-segmentation.md)

## Richtlinienverletzungen

>[!NOTE]
>
>Richtlinienverletzungen gelten nur, wenn Sie ein Segment erstellen, das einem Ziel zugewiesen wurde.

Nachdem Sie Ihr Segment erstellt haben, wird das Segment von Adobe Experience Platform Data Governance analysiert, um sicherzustellen, dass keine Richtlinienverletzungen innerhalb des Segments auftreten. Siehe [Data Governance - Übersicht](../../data-governance/home.md) für weitere Informationen.

![](../images/ui/overview/segment-dule-policy-violations.png)

## Nächste Schritte und zusätzliche Ressourcen {#next-steps}

Die [!DNL Segmentation Service] Die Benutzeroberfläche bietet einen umfassenden Workflow, mit dem Sie marktfähige Zielgruppen isolieren können von [!DNL Real-time Customer Profile] Daten.

Weitere Informationen finden Sie unter [!DNL Segmentation Service], lesen Sie bitte die Dokumentation weiter. Erfahren Sie, wie Sie die [!DNL Segmentation Service] API, lesen Sie bitte die [[!DNL Segmentation Service] Entwicklerhandbuch](../api/overview.md).
