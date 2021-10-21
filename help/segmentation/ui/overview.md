---
keywords: Experience Platform;Home;beliebte Themen;Segmentierungsservice;Segmentierung;Segmentierungsdienst;Benutzerhandbuch;Handbuch;Segmentierungsleitfaden;Segmentierungsleitfaden;Segmenterstellung;Segmentaufbau;realisiert;Bestehend;Exit;
solution: Experience Platform
title: Handbuch zur Segmentierungsservice-UI
topic-legacy: ui guide
description: Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche für das Erstellen und Verwalten von Segmentdefinitionen.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 8325ae6fd7d0013979e80d56eccd05b6ed6f5108
workflow-type: tm+mt
source-wordcount: '1691'
ht-degree: 20%

---

# Handbuch zur Segmentierungsservice-UI

[!DNL Adobe Experience Platform Segmentation Service] stellt eine Benutzeroberfläche zum Erstellen und Verwalten von Segmentdefinitionen bereit.

## Erste Schritte

Die Arbeit mit Segmentdefinitionen erfordert ein Verständnis der verschiedenen [!DNL Experience Platform] mit der Segmentierung verbundene Dienste. Bevor Sie dieses Benutzerhandbuch lesen, lesen Sie bitte die Dokumentation für folgende Dienste:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] allows you to divide data stored in [!DNL Experience Platform] that relates to individuals (such as customers, prospects, users, or organizations) into smaller groups.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Ermöglicht die Erstellung von Profilen von Kunden durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, die in [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profil und Ereignis gemäß der [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md).

Außerdem sollten Sie zwei Schlüsselbegriffe kennen, die in diesem Dokument verwendet werden, und den Unterschied zwischen ihnen verstehen:
- **Segmentdefinition**: Der Regelsatz, der zur Beschreibung wichtiger Merkmale oder Verhaltensweisen einer Zielgruppe verwendet wird.
- **Audience**: Der resultierende Satz von Profilen, die den Kriterien einer Segmentdefinition entsprechen.

## Übersicht

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Segmente]** in der linken Navigation, um die **[!UICONTROL Überblick]** Tabulator, der die [!UICONTROL Segmente] Dashboard.

>[!NOTE]
>
>Wenn Ihr Unternehmen neu bei Platform ist und noch keine aktiven Profil-DataSets oder Merge-Richtlinien erstellt wurden, [!UICONTROL Segmente] Dashboard ist nicht sichtbar. Stattdessen [!UICONTROL Überblick] zeigt Links und Dokumentation an, um Ihnen die ersten Schritte mit Segmenten zu erleichtern.

### [!UICONTROL Segmente] Dashboard {#segments-dashboard}

Die **[!UICONTROL Segmente]** In Dashboard werden Schlüsselmetriken zu den Segmentdaten Ihres Unternehmens umrissen.

Weitere Informationen finden Sie unter [Segment-Dashboard-Handbuch](../../dashboards/guides/segments.md).

![](../../dashboards/images/segments/dashboard-overview.png)

## Durchsuchen

Wählen Sie **[!UICONTROL Durchsuchen]** um eine Liste aller Segmentdefinitionen für Ihre IMS-Organisation anzuzeigen.

![](../images/ui/overview/segment-browse-all.png)

In dieser Ansicht werden Informationen zur Segmentdefinition Liste, einschließlich Aufschlüsselung, Ablage, Anzahl der Profil, Bewertungsmethode, Erstellungsdatum und Datum der letzten Änderung.

In der Aufschlüsselung wird ein Balkendiagramm angezeigt, in dem der prozentuale Anteil der Profil dargestellt wird, die zu jedem der folgenden Status gehören: [!UICONTROL Realisiert], [!UICONTROL Vorhanden]und [!UICONTROL Beenden]. Zusätzlich wird die Aufschlüsselung der [!UICONTROL Durchsuchen] tab ist die genaueste Aufschlüsselung des Segmentstatus. Wenn sich diese Zahl von der auf der [!UICONTROL Überblick] verwenden, sollten Sie die Zahlen auf der [!UICONTROL Durchsuchen] als korrekte Informationsquelle, da [!UICONTROL Überblick] Registernummern werden nur einmal pro Tag aktualisiert.

![](../images/ui/overview/segment-browse-breakdown.png)

| Status | Beschreibung |
| ------ | ----------- |
| Realisiert | Ein neues Profil innerhalb des Segments. |
| Vorhanden | An existing profile which has remained within the segment. |
| Beenden | Ein bestehendes Profil, das das Segment verlässt. |

Die Abwanderung stellt den Prozentsatz der Profil dar, die sich innerhalb einer Segmentdefinition im Vergleich zum letzten Segmentauftrag ändern, während die Segmentanzahl die Gesamtanzahl der Profil darstellt, die für das Profil infrage kommen.

Die Auswertungsmethode kann entweder Streaming oder Batch sein. Streaming-Segmente werden konstant ausgewertet, sobald Daten in das System strömen. Batch-Segmente werden gemäß einem festgelegten Zeitplan ausgewertet.

![](../images/ui/overview/segment-browse-segments.png)

Am oberen Rand der Seite finden Sie Optionen zum Hinzufügen aller Segmente zu einem Zeitplan und zum Erstellen eines neuen Segments.

Umschalten **[!UICONTROL Alle Segmente planen Hinzufügen]** aktiviert die geplante Segmentierung. Weitere Informationen zur geplanten Segmentierung finden Sie im [geplanten Segmentierungsabschnitt dieses Benutzerhandbuchs](#scheduled-segmentation).

Auswählen **[!UICONTROL Segment erstellen]** bringt Sie zum Segmentaufbau. Weitere Informationen zum Erstellen von Segmenten finden Sie im Abschnitt [Erstellen eines Segments im Benutzerhandbuch](#create-segment).

![](../images/ui/overview/segment-browse-top.png)

Die rechte Sidebar enthält Informationen über alle Segmente innerhalb der IMS-Organisation, listet die Gesamtanzahl der Segmente, das letzte Bewertungsdatum, das nächste Bewertungsdatum sowie eine Aufschlüsselung der Segmente nach Bewertungsmethode auf.

![](../images/ui/overview/segment-browse-segment-info.png)

Die Auswahl der Segmentdefinitionszeile bietet eine Übersicht über die Segmentdefinition, einschließlich der Optionen zum Bearbeiten oder Löschen des Segments, zum Aktivieren des Segments an einem Ziel, der qualifizierten Audience für das Segment, der Gesamtgröße der Audience zusätzlich zu Segmentname, -beschreibung, -bewertungsmethode, Erstellungsdatum und Datum der letzten Änderung.

>[!NOTE]
>
> Sie werden **nicht** kann ein Segment löschen, das in einer Ziel-Aktivierung verwendet wird.

![](../images/ui/overview/segment-browse-details.png)

## Details zur Segmentdefinition {#segment-details}

Um weitere Details über eine bestimmte Segmentdefinition anzuzeigen, wählen Sie den Segmentnamen in der **[!UICONTROL Durchsuchen]** Tabulator.

Die Segmentdetailseite wird angezeigt. Oben finden Sie eine Übersicht über die Segmentdefinition, Informationen über die Größe der qualifizierten Audience sowie über Ziele, für die das Segment aktiviert ist.

![](../images/ui/overview/segment-details-summary.png)

### Segmentübersicht

Die **[!UICONTROL Segmentübersicht]** -Abschnitt enthält Informationen wie ID, Name, Beschreibung und Details der Attribute.

Außerdem haben Sie die Möglichkeit, das Segment entweder an einem Ziel zu aktivieren oder das Segment zu bearbeiten. Auswählen **[!UICONTROL Am Ziel aktivieren]** aktiviert das Segment an ein Ziel. Weitere Informationen zum Aktivieren eines Segments für ein Ziel finden Sie im [Aktivierung - Übersicht](../../destinations/ui/activation-overview.md).

![](../images/ui/overview/segment-details-activate.png)

Auswählen **[!UICONTROL Segment bearbeiten]** bringt Sie zu [!DNL Segment Builder]. Weitere Informationen zur Verwendung der [!DNL Segment Builder] Arbeitsbereich, bitte lesen Sie die [[!DNL Segment Builder] Benutzerhandbuch](./segment-builder.md).

![](../images/ui/overview/segment-details-edit-segment.png)

### Audience insgesamt im Segment

Die **[!UICONTROL Audience insgesamt im Segment]** zeigt die Gesamtanzahl der Profil an, die für das Segment infrage kommen.

Die Schätzungen werden anhand einer Stichprobengröße der Beispieldaten dieses Tages erstellt. Wenn sich in Ihrem Profilspeicher weniger als 1 Million Entitäten befinden, wird der vollständige Datensatz verwendet. Bei zwischen 1 und 20 Millionen Entitäten werden 1 Million Entitäten verwendet; bei mehr als 20 Millionen Entitäten werden 5 % der Gesamtentitäten genutzt. Weiterführende Informationen zum Generieren von Segmentschätzungen finden Sie in der Anleitung zur Segmenterstellung im Abschnitt zum [Generieren von Schätzungen](../tutorials/create-a-segment.md#estimate-and-preview-an-audience).

### Aktivierte Ziele

Die **[!UICONTROL Aktivierte Ziele]** zeigt die Ziele an, für die dieses Segment aktiviert ist.

>[!NOTE]
>
> Ziele sind eine Funktion, die verfügbar ist mit [!DNL Real-time Customer Data Platform], und erlauben Sie Ihnen, Daten auf externe Plattformen zu exportieren. Weitere Informationen zu Reisezielen finden Sie im [Zielgruppenübersicht](../../destinations/home.md). Informationen zur Aktivierung eines Segments für ein Ziel finden Sie unter [Aktivierung - Übersicht](../../destinations/ui/activation-overview.md).

### Profil-Beispiele

Darunter finden Sie eine Stichprobe der Profil, die für das Segment infrage kommen, mit detaillierten Informationen einschließlich der [!DNL Profile] ID, Vorname, Nachname und persönliche E-Mail-Adresse.

Die Art und Weise, in der die Datenerfassung ausgelöst wird, hängt von der Art der Aufnahme ab.

Bei der Stapelverarbeitung wird der Profil-Store alle fünfzehn Minuten automatisch gescannt, um festzustellen, ob ein neuer Stapel seit dem letzten Stichprobenauftrag erfolgreich erfasst wurde. Wenn das der Fall ist, wird der Profil-Store daraufhin gescannt, um zu sehen, ob sich die Anzahl der Datensätze um mindestens 5 % geändert hat. Wenn diese Bedingungen erfüllt sind, wird ein neuer Probenahmeauftrag ausgelöst.

For streaming ingestion, the profile store is automatically scanned every hour to see if there&#39;s been at least a 5% change in the number of records. Wenn diese Bedingung erfüllt ist, wird ein neuer Stichprobenauftrag ausgelöst.

The sample size of the scan depends on the overall number of entities in your profile store. These sample sizes are represented in the following table:

| Einrichtungen im Profil-Store | Stichprobengröße |
| ------------------------- | ----------- |
| Weniger als 1 Million | Vollständiger Datensatz |
| 1 bis 20 Millionen | 1 Million |
| über 20 Millionen | 5 % der Gesamtmittel |

Detailliertere Informationen zu den einzelnen [!DNL Profile] kann angezeigt werden, indem Sie die [!DNL Profile] ID. Weitere Informationen zu den Einzelheiten eines Profils finden Sie im [[!DNL Real-time Customer Profile] Benutzerhandbuch](../../profile/ui/user-guide.md#profile-detail).

![](../images/ui/overview/segment-details-profiles.png)

## Erstellen eines Segments {#create-segment}

Auswählen **[!UICONTROL Segment erstellen]** in der rechten oberen Ecke öffnet sich die [!DNL Segment Builder] Arbeitsbereich, in dem Sie mit der Erstellung einer Segmentdefinition beginnen können.

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] Arbeitsbereich

[!DNL Segment Builder] bietet einen umfangreichen Arbeitsbereich, mit dem Sie interagieren können [!DNL Profile] Datenelemente. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag-and-Drop-Kacheln, die zur Darstellung von Dateneigenschaften dienen.

Weitere Informationen zur Verwendung der [!DNL Segment Builder] Arbeitsbereich, bitte lesen Sie die [[!DNL Segment Builder] Benutzerhandbuch](./segment-builder.md).

![](../images/ui/overview/segment-builder.png)

## Geplante Segmentierung {#scheduled-segmentation}

Nachdem Sie Segmentdefinitionen erstellt haben, können Sie diese durch eine On-Demand- oder geplante (kontinuierliche) Auswertung auswerten. Bewertung bedeutet Bewegung [!DNL Real-time Customer Profile] Daten durch Segmentdefinitionen zur Erstellung entsprechender Audiencen. Nach der Erstellung werden die Audiencen gespeichert und gespeichert, damit sie exportiert werden können mit [!DNL Experience Platform] APIs.

Bei der On-Demand-Auswertung wird die API zur Durchführung von Auswertungen und zum Aufbau von Zielgruppen nach Bedarf verwendet. Bei der geplanten Auswertung (auch „geplante Segmentierung“ genannt) können Sie hingegen einen Zeitplan erstellen, um die Segmentdefinitionen zu einem bestimmten Zeitpunkt (maximal einmal täglich) auszuwerten.

### Geplante Segmentierung aktivieren {#enable-scheduled-segmentation}

Die Aktivierung Ihrer Segmentdefinitionen für eine geplante Auswertung kann über die Benutzeroberfläche oder die API erfolgen. In the UI, return to the **[!UICONTROL Browse]** tab within **[!UICONTROL Segments]** and toggle on **[!UICONTROL Add all segments to schedule]**. Dadurch werden alle Segmente anhand des von Ihrer Organisation festgelegten Zeitplans evaluiert.

>[!NOTE]
>
>Die geplante Evaluierung kann für Sandboxen mit maximal fünf (5) Zusammenführungsrichtlinien aktiviert werden für [!DNL XDM Individual Profile]. Wenn Ihr Unternehmen mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] innerhalb einer einzigen Sandbox-Umgebung können Sie keine geplante Evaluierung verwenden.

Zeitpläne können derzeit nur mit der API erstellt werden. Ausführliche Anweisungen zum Erstellen, Bearbeiten und Verwenden von Zeitplänen mithilfe der API finden Sie im Tutorial zum Auswerten und Aufrufen von Segmentergebnissen, insbesondere im Abschnitt zur [geplanten Auswertung mithilfe der API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## Streaming-Segmentierung {#streaming-segmentation}

Streaming-Segmentierung ist die Fähigkeit zur Segmentierung auf [!DNL Platform] in Echtzeit, wobei der Schwerpunkt auf Datenreichweite liegt. Mit der Streaming-Segmentierung erfolgt die Segmentqualifizierung nun, da Daten landen in [!DNL Platform], um die Notwendigkeit zu verringern, Segmentierungsaufträge zu planen und auszuführen.

Weitere Informationen zur Streaming-Segmentierung finden Sie im [Benutzerhandbuch für Streaming-Segmentierung](./streaming-segmentation.md).

>[!NOTE]
>
>Damit die Streaming-Segmentierung funktioniert, müssen Sie die geplante Segmentierung für das Unternehmen aktivieren. Weitere Informationen zum Aktivieren der geplanten Segmentierung finden Sie unter [den Abschnitt zur Streaming-Segmentierung in diesem Benutzerhandbuch](#scheduled-segmentation).

## Kantensegmentierung {#edge-segmentation}

Mit der Edge-Segmentierung können Segmente in der Plattform unmittelbar am Rand ausgewertet werden, sodass dieselben Anwendungsfälle für die Personalisierung der Seite und der nächsten Seite aktiviert werden.

Weitere Informationen zur Segmentierung der Kante finden Sie im [Hilfslinie für die Benutzeroberfläche für Kantensegmentierung](./edge-segmentation.md)

## Politische Verstöße

>[!NOTE]
>
>Richtlinienverletzungen gelten nur, wenn Sie ein Segment erstellen, das einem Ziel zugewiesen wurde.

Once you are done creating your segment, the segment will be analyzed by Adobe Experience Platform Data Governance to ensure there are no policy violations within the segment. Weitere Informationen finden Sie in der [[!DNL Data Governance] Übersicht über](../../data-governance/home.md).

![](../images/ui/overview/segment-dule-policy-violations.png)

## Nächste Schritte und zusätzliche Ressourcen {#next-steps}

Die [!DNL Segmentation Service] Die Benutzeroberfläche bietet einen umfangreichen Workflow, in dem Sie marktfähige Audiencen isolieren können von [!DNL Real-time Customer Profile] Daten.

Weitere Informationen [!DNL Segmentation Service], lesen Sie bitte die Dokumentation weiter. So verwenden Sie die [!DNL Segmentation Service] API, bitte lesen Sie die [[!DNL Segmentation Service] Entwicklerleitfaden](../api/overview.md).
