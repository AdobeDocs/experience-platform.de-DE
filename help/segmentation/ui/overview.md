---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierungsdienst; Segmentierung; Segmentierungsdienst; Benutzerhandbuch; Benutzerhandbuch; Handbuch zur Segmentierung; Segmentierungs-UI; Segment Builder; Segment Builder; realisiert; vorhandene; Beenden;
solution: Experience Platform
title: Handbuch zur Benutzeroberfläche des Segmentierungsdienstes
topic-legacy: ui guide
description: Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche zum Erstellen und Verwalten von Segmentdefinitionen.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 998332007465c1f8457b5d8cf0e153d513505d39
workflow-type: tm+mt
source-wordcount: '1547'
ht-degree: 22%

---

# Handbuch zur Benutzeroberfläche des Segmentierungsdienstes

[!DNL Adobe Experience Platform Segmentation Service] bietet eine Benutzeroberfläche zum Erstellen und Verwalten von Segmentdefinitionen.

## Erste Schritte

Das Arbeiten mit Segmentdefinitionen erfordert ein Verständnis der verschiedenen [!DNL Experience Platform]-Dienste, die mit der Segmentierung verbunden sind. Bevor Sie dieses Benutzerhandbuch lesen, lesen Sie bitte die Dokumentation für folgende Dienste:

- [[!DNL Segmentation Service]](../home.md):  [!DNL Segmentation Service] ermöglicht es Ihnen, die in gespeicherten Daten,  [!DNL Experience Platform] die sich auf Einzelpersonen (wie Kunden, Interessenten, Benutzer oder Organisationen) beziehen, in kleinere Gruppen zu unterteilen.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Ermöglicht die Erstellung von Kundenprofilen durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, in die  [!DNL Platform]aufgenommen wird.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

Außerdem sollten Sie zwei Schlüsselbegriffe kennen, die in diesem Dokument verwendet werden, und den Unterschied zwischen ihnen verstehen:
- **Segmentdefinition**: Der Regelsatz, der zur Beschreibung wichtiger Merkmale oder Verhaltensweisen einer Zielgruppe verwendet wird.
- **Audience**: Der resultierende Satz von Profilen, die den Kriterien einer Segmentdefinition entsprechen.

## Übersicht

Wählen Sie in der [[!DNL Experience Platform] UI](https://platform.adobe.com/) **[!UICONTROL Segmente]** im linken Navigationsbereich aus, um die Registerkarte **[!UICONTROL Übersicht]** zu öffnen. Auf dieser Registerkarte finden Sie Links zu Dokumentationen und Videos, die Ihnen helfen, Segmente zu verstehen und mit ihnen zu arbeiten.

![](../images/ui/overview/segment-overview.png)

### Segmente-Dashboard

Für einige Benutzer bietet die Auswahl von **[!UICONTROL Segmenten]** im linken Navigationsbereich und das Öffnen des Tabs **[!UICONTROL Übersicht]** ein Dashboard, in dem die Schlüsselmetriken für Ihre Segmentdaten dargestellt werden.

Weitere Informationen finden Sie im Handbuch [Segment-Dashboard](segment-dashboard.md).

## Durchsuchen

Wählen Sie die Registerkarte **[!UICONTROL Durchsuchen]** aus, um eine Liste aller Segmentdefinitionen für Ihre IMS-Organisation anzuzeigen.

![](../images/ui/overview/segment-browse-all.png)

Diese Ansicht listet Informationen zur Segmentdefinition auf, einschließlich Aufschlüsselung, Abwanderung, Anzahl der Profile, Auswertungsmethode, Erstellungsdatum und Datum der letzten Änderung.

Die Aufschlüsselung zeigt ein Balkendiagramm, in dem der Prozentsatz der Profile, die zu den folgenden Status gehören, dargestellt wird: [!UICONTROL Realized], [!UICONTROL Existing] und [!UICONTROL Exiting].

![](../images/ui/overview/segment-browse-breakdown.png)

| Status | Beschreibung |
| ------ | ----------- |
| Realisiert | Ein neues Profil innerhalb des Segments. |
| Bestehend | Ein vorhandenes Profil, das innerhalb des Segments verbleibt. |
| Beenden | Ein vorhandenes Profil, das das Segment verlässt. |

Die Abwanderung stellt den Prozentsatz der Profile dar, die sich innerhalb einer Segmentdefinition ändern, im Vergleich zum letzten Ausführen des Segmentauftrags, während die Profilanzahl die Gesamtanzahl der Profile darstellt, die sich für das Segment qualifizieren.

Die Auswertungsmethode kann entweder Streaming oder Batch sein. Streaming-Segmente werden konstant ausgewertet, sobald Daten in das System strömen. Batch-Segmente werden gemäß einem festgelegten Zeitplan ausgewertet.

![](../images/ui/overview/segment-browse-segments.png)

Am oberen Rand der Seite finden Sie Optionen zum Hinzufügen aller Segmente zu einem Zeitplan und zum Erstellen eines neuen Segments.

Durch das Umschalten von **[!UICONTROL Alle Segmente zur Planung]** wird die geplante Segmentierung aktiviert. Weitere Informationen zur geplanten Segmentierung finden Sie im Abschnitt [Geplante Segmentierung dieses Benutzerhandbuchs](#scheduled-segmentation).

Wenn Sie **[!UICONTROL Segment]** erstellen, gelangen Sie zum Segment Builder. Weitere Informationen zum Erstellen von Segmenten finden Sie im Abschnitt zum Erstellen eines Segments im Benutzerhandbuch](#create-segment).[

![](../images/ui/overview/segment-browse-top.png)

Die rechte Seitenleiste enthält Informationen zu allen Segmenten innerhalb der IMS-Organisation, listet die Gesamtanzahl der Segmente, das letzte Auswertungsdatum, das nächste Auswertungsdatum sowie eine Aufschlüsselung der Segmente nach Bewertungsmethode auf.

![](../images/ui/overview/segment-browse-segment-info.png)

Die Auswahl der Zeile der Segmentdefinition bietet eine Zusammenfassung der Segmentdefinition, einschließlich Optionen zum Bearbeiten oder Löschen des Segments, der qualifizierten Zielgruppe für das Segment, der Gesamtgröße der Zielgruppe, zusätzlich zum Namen, der Beschreibung, der Auswertungsmethode, dem erstellten Datum und dem Datum der letzten Änderung.

![](../images/ui/overview/segment-browse-details.png)

## Details zur Segmentdefinition {#segment-details}

Um weitere Details zu einer bestimmten Segmentdefinition anzuzeigen, wählen Sie den Namen eines Segments auf der Registerkarte **[!UICONTROL Durchsuchen]** aus.

Die Seite mit den Segmentdetails wird angezeigt. Oben finden Sie eine Zusammenfassung der Segmentdefinition, Informationen zur qualifizierten Zielgruppengröße sowie Ziele, für die das Segment aktiviert wird.

![](../images/ui/overview/segment-details-summary.png)

### Segmentzusammenfassung

Der Abschnitt **[!UICONTROL Segmentzusammenfassung]** enthält Informationen wie die ID, den Namen, die Beschreibung und Details der Attribute.

Darüber hinaus haben Sie die Möglichkeit, das Segment zu bearbeiten. Wenn Sie **[!UICONTROL Segment bearbeiten]** auswählen, gelangen Sie zum [!DNL Segment Builder]. Weitere Informationen zur Verwendung des Arbeitsbereichs [!DNL Segment Builder] finden Sie im [[!DNL Segment Builder] Benutzerhandbuch](./segment-builder.md).

### Gesamtzielgruppe im Segment

Im Abschnitt **[!UICONTROL Gesamtanzahl der Zielgruppen im Segment]** wird die Gesamtanzahl der Profile angezeigt, die für das Segment qualifiziert sind.

Schätzungen werden anhand einer Stichprobengröße der Beispieldaten dieses Tages erstellt. Wenn sich in Ihrem Profilspeicher weniger als 1 Million Entitäten befinden, wird der vollständige Datensatz verwendet. Bei zwischen 1 und 20 Millionen Entitäten werden 1 Million Entitäten verwendet; bei mehr als 20 Millionen Entitäten werden 5 % der Gesamtentitäten genutzt. Weiterführende Informationen zum Generieren von Segmentschätzungen finden Sie in der Anleitung zur Segmenterstellung im Abschnitt zum [Generieren von Schätzungen](../tutorials/create-a-segment.md#estimate-and-preview-an-audience).

### Aktivierte Ziele

Im Abschnitt **[!UICONTROL Aktivierte Ziele]** werden die Ziele angezeigt, für die dieses Segment aktiviert ist.

>[!NOTE]
>
> Ziele sind eine Funktion, die mit [!DNL Real-time Customer Data Platform] verfügbar ist und mit der Sie Daten auf externe Plattformen exportieren können. Weitere Informationen zu Zielen finden Sie in der [Zielübersicht](../../destinations/home.md). Informationen zum Aktivieren eines Segments für ein Ziel finden Sie in der [Anleitung zum Aktivieren von Segmenten für ein Ziel](../../destinations/ui/activate-destinations.md).

### Profilbeispiele

Darunter finden Sie eine Auswahl an Profilen, die für das Segment qualifiziert sind, mit detaillierten Informationen, einschließlich der [!DNL Profile]-ID, des Vornamens, des Nachnamens und der persönlichen E-Mail-Adresse.

Die Art und Weise, wie das Sampling von Daten ausgelöst wird, hängt von der Erfassungsmethode ab.

Für die Batch-Erfassung wird der Profilspeicher automatisch alle fünfzehn Minuten überprüft, um festzustellen, ob ein neuer Batch seit der letzten Sampling-Ausführung erfolgreich erfasst wurde. Ist dies der Fall, wird der Profilspeicher daraufhin überprüft, um festzustellen, ob sich die Anzahl der Datensätze um mindestens 5 % geändert hat. Wenn diese Bedingungen erfüllt sind, wird ein neuer Sampling-Auftrag ausgelöst.

Für die Streaming-Erfassung wird der Profilspeicher automatisch stündlich gescannt, um festzustellen, ob sich die Anzahl der Datensätze um mindestens 5 % geändert hat. Wenn diese Bedingung erfüllt ist, wird ein neuer Sampling-Auftrag ausgelöst.

Die Stichprobengröße der Prüfung hängt von der Gesamtanzahl der Entitäten in Ihrem Profilspeicher ab. Diese Stichprobengrößen werden in der folgenden Tabelle dargestellt:

| Entitäten im Profilspeicher | Stichprobengröße |
| ------------------------- | ----------- |
| Weniger als 1 Million | Vollständiger Datensatz |
| 1 bis 20 Mio. | 1 Mio. |
| Über 20 Millionen | 5 % des Gesamtbetrags |

Detailliertere Informationen zu den einzelnen [!DNL Profile]-IDs erhalten Sie durch Auswahl der ID [!DNL Profile] . Weitere Informationen zu Profildetails finden Sie im [[!DNL Real-time Customer Profile] Benutzerhandbuch](../../profile/ui/user-guide.md#profile-detail).

![](../images/ui/overview/segment-details-profiles.png)

## Erstellen eines Segments {#create-segment}

Wenn Sie in der oberen rechten Ecke **[!UICONTROL Segment]** erstellen auswählen, wird der Arbeitsbereich [!DNL Segment Builder] geöffnet, in dem Sie mit der Erstellung einer Segmentdefinition beginnen können.

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] Arbeitsbereich

[!DNL Segment Builder] bietet einen umfassenden Arbeitsbereich, in dem Sie mit  [!DNL Profile] Datenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag-and-Drop-Kacheln, die zur Darstellung von Dateneigenschaften dienen.

Weitere Informationen zur Verwendung des Arbeitsbereichs [!DNL Segment Builder] finden Sie im [[!DNL Segment Builder] Benutzerhandbuch](./segment-builder.md).

![](../images/ui/overview/segment-builder.png)

## Geplante Segmentierung {#scheduled-segmentation}

Nachdem Sie Segmentdefinitionen erstellt haben, können Sie diese durch eine On-Demand- oder geplante (kontinuierliche) Auswertung auswerten. Auswertung bedeutet, [!DNL Real-time Customer Profile]-Daten durch Segmentdefinitionen zu verschieben, um entsprechende Zielgruppen zu erstellen. Nach der Erstellung werden die Zielgruppen gespeichert und so exportiert, dass sie mit [!DNL Experience Platform]-APIs exportiert werden können.

Bei der On-Demand-Auswertung wird die API zur Durchführung von Auswertungen und zum Aufbau von Zielgruppen nach Bedarf verwendet. Bei der geplanten Auswertung (auch „geplante Segmentierung“ genannt) können Sie hingegen einen Zeitplan erstellen, um die Segmentdefinitionen zu einem bestimmten Zeitpunkt (maximal einmal täglich) auszuwerten.

### Geplante Segmentierung aktivieren {#enable-scheduled-segmentation}

Die Aktivierung Ihrer Segmentdefinitionen für eine geplante Auswertung kann über die Benutzeroberfläche oder die API erfolgen. Kehren Sie in der Benutzeroberfläche zur Registerkarte **[!UICONTROL Durchsuchen]** innerhalb von **[!UICONTROL Segmente]** zurück und schalten Sie **[!UICONTROL Alle Segmente zur Planung hinzufügen]** ein. Dadurch werden alle Segmente anhand des von Ihrer Organisation festgelegten Zeitplans evaluiert.

>[!NOTE]
>
>Geplante Auswertung kann für Sandboxes mit maximal fünf (5) Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] aktiviert werden. Wenn Ihr Unternehmen innerhalb einer Sandbox-Umgebung über mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] verfügt, können Sie keine geplante Auswertung verwenden.

Zeitpläne können derzeit nur mit der API erstellt werden. Ausführliche Anweisungen zum Erstellen, Bearbeiten und Verwenden von Zeitplänen mithilfe der API finden Sie im Tutorial zum Auswerten und Aufrufen von Segmentergebnissen, insbesondere im Abschnitt zur [geplanten Auswertung mithilfe der API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## Streaming-Segmentierung {#streaming-segmentation}

Streaming-Segmentierung ist die Möglichkeit, die Segmentierung für [!DNL Platform] nahezu in Echtzeit durchzuführen, während der Schwerpunkt auf Datenreichweite liegt. Mit Streaming-Segmentierung erfolgt die Segmentqualifizierung jetzt, wenn Daten in [!DNL Platform] landen. So wird die Notwendigkeit verringert, Segmentierungsaufträge zu planen und auszuführen.

Weitere Informationen zur Streaming-Segmentierung finden Sie im [Benutzerhandbuch zur Streaming-Segmentierung](./streaming-segmentation.md).

>[!NOTE]
>
>Damit Streaming-Segmentierung funktioniert, müssen Sie die geplante Segmentierung für die Organisation aktivieren. Weitere Informationen zum Aktivieren der geplanten Segmentierung finden Sie im Abschnitt [Streaming-Segmentierung in diesem Benutzerhandbuch](#scheduled-segmentation).

## Edge-Segmentierung {#edge-segmentation}

Bei der Edge-Segmentierung können Segmente in Platform sofort am Rand ausgewertet werden, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.

Weitere Informationen zur Kantensegmentierung finden Sie im [UI-Handbuch zur Kantensegmentierung](./edge-segmentation.md)

## Richtlinienverletzungen

>[!NOTE]
>
>Richtlinienverletzungen gelten nur, wenn Sie ein Segment erstellen, das einem Ziel zugewiesen wurde.

Nachdem Sie Ihr Segment erstellt haben, wird das Segment von Adobe Experience Platform Data Governance analysiert, um sicherzustellen, dass keine Richtlinienverletzungen innerhalb des Segments auftreten. Weitere Informationen finden Sie in der [[!DNL Data Governance] Übersicht über ](../../data-governance/home.md).

![](../images/ui/overview/segment-dule-policy-violations.png)

## Nächste Schritte und zusätzliche Ressourcen {#next-steps}

Die Benutzeroberfläche von [!DNL Segmentation Service] bietet einen umfassenden Workflow, mit dem Sie vermarktbare Zielgruppen von [!DNL Real-time Customer Profile]-Daten isolieren können.

Um mehr über [!DNL Segmentation Service] zu erfahren, lesen Sie bitte die Dokumentation weiter. Informationen zur Verwendung der [!DNL Segmentation Service]-API finden Sie im [[!DNL Segmentation Service] Entwicklerhandbuch](../api/overview.md).
