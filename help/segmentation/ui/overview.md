---
keywords: Experience Platform;home;popular topics;Segmentation Service;segmentation;segmentation service;user guide;ui guide;segmentation ui guide;segment builder;Segment builder;realized;existing;exiting;
solution: Experience Platform
title: Benutzerhandbuch zum Segmentdienst
topic: ui guide
description: Der Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche zum Erstellen und Verwalten von Segmentdefinitionen.
translation-type: tm+mt
source-git-commit: 3e83215cc24b32b7fe9486c6faf455f247b6c922
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 23%

---


# Handbuch zur Benutzeroberfläche des Segmentdienstes

[!DNL Adobe Experience Platform Segmentation Service] stellt eine Benutzeroberfläche zum Erstellen und Verwalten von Segmentdefinitionen bereit.

## Erste Schritte

Working with segment definitions requires an understanding of the various [!DNL Experience Platform] services involved with segmentation. Bevor Sie dieses Benutzerhandbuch lesen, lesen Sie bitte die Dokumentation für folgende Dienste:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] ermöglicht es Ihnen, Daten, die in Bezug auf Einzelpersonen gespeichert sind (z. B. Kunden, Potenzieller Kunde, Benutzer oder Organisationen), in kleinere Gruppen zu unterteilen. [!DNL Experience Platform]
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Ermöglicht die Erstellung von Profilen von Kunden durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, in die [!DNL Platform]eingegriffen wird.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

Außerdem sollten Sie zwei Schlüsselbegriffe kennen, die in diesem Dokument verwendet werden, und den Unterschied zwischen ihnen verstehen:
- **Segmentdefinition**: Der Regelsatz, der zur Beschreibung wichtiger Merkmale oder Verhaltensweisen einer Zielgruppe verwendet wird.
- **Audience**: Der resultierende Satz von Profilen, die den Kriterien einer Segmentdefinition entsprechen.

## Übersicht

Wählen Sie in der [[!DNL Experience Platform] Benutzeroberfläche](http://platform.adobe.com/)im linken Navigationsbereich die Option &quot; **[!UICONTROL Segmente]** &quot;, um die Registerkarte &quot; **[!UICONTROL Übersicht]** &quot;zu öffnen. Diese Registerkarte enthält Links zu Dokumentation und Videos, die Ihnen helfen, Segmente zu verstehen und mit ihnen zu arbeiten.

![](../images/ui/overview/segment-overview.png)

## Durchsuchen

Wählen Sie die Registerkarte &quot; **[!UICONTROL Durchsuchen]** &quot;, um eine Liste aller Segmentdefinitionen für Ihre IMS-Organisation anzuzeigen.

![](../images/ui/overview/segment-browse-all.png)

Diese Ansicht Liste Informationen zur Segmentdefinition, einschließlich Aufschlüsselung, Ruhephase, Profil-Anzahl, Bewertungsmethode, erstelltes Datum und Datum der letzten Änderung.

Die Aufschlüsselung zeigt ein Balkendiagramm mit dem Prozentwert der Profil, die zu den folgenden Statuswerten gehören: [!UICONTROL Einstieg], [!UICONTROL realisiert]und [!UICONTROL Ausstieg].

![](../images/ui/overview/segment-browse-breakdown.png)

| Status | Beschreibung |
| ------ | ----------- |
| Eingestiegen | Ein neues Profil innerhalb des Segments. |
| Realisiert | Ein vorhandenes Profil, das innerhalb des Segments geblieben ist. |
| Beenden | Ein vorhandenes Profil, das das Segment verlässt. |

Die Umdrehung stellt den Prozentsatz der Profil dar, die sich innerhalb einer Segmentdefinition im Vergleich zum letzten Ausführen des Segmentauftrags ändern, während die Anzahl der Profil die Gesamtanzahl der Profil darstellt, die für das Segment qualifiziert sind.

Die Auswertungsmethode kann entweder Streaming oder Batch sein. Streaming-Segmente werden konstant ausgewertet, sobald Daten in das System strömen. Batch-Segmente werden gemäß einem festgelegten Zeitplan ausgewertet.

![](../images/ui/overview/segment-browse-segments.png)

Oben auf der Seite befinden sich Optionen zum Hinzufügen aller Segmente zu einem Zeitplan und zum Erstellen eines neuen Segments.

Durch Umschalten **[!UICONTROL Hinzufügen alle Segmente zu planen]** wird die geplante Segmentierung aktiviert. Weitere Informationen zur geplanten Segmentierung finden Sie im Abschnitt zur [geplanten Segmentierung dieses Benutzerhandbuchs](#scheduled-segmentation).

Wenn Sie Segment **** erstellen auswählen, gelangen Sie zum Segmentaufbau. Weitere Informationen zum Erstellen von Segmenten finden Sie im Abschnitt zum [Erstellen eines Segments im Benutzerhandbuch](#create-segment).

![](../images/ui/overview/segment-browse-top.png)

Die rechte Seitenleiste enthält Informationen zu allen Segmenten innerhalb der IMS-Organisation, listet die Gesamtzahl der Segmente, das letzte Bewertungsdatum, das nächste Bewertungsdatum sowie eine Aufschlüsselung der Segmente nach Bewertungsmethode auf.

![](../images/ui/overview/segment-browse-segment-info.png)

Durch Auswahl der Segmentdefinitionszeile erhalten Sie eine Übersicht über die Segmentdefinition, einschließlich Optionen zum Bearbeiten oder Löschen des Segments, der qualifizierten Audience für das Segment, der Gesamtgröße der Audience zusätzlich zu Segmentname, -beschreibung, -bewertungsverfahren, Erstellungsdatum und Datum der letzten Änderung.

![](../images/ui/overview/segment-browse-details.png)

## Details zur Segmentdefinition {#segment-details}

Um weitere Details zu einer bestimmten Segmentdefinition anzuzeigen, wählen Sie auf der Registerkarte &quot; **[!UICONTROL Durchsuchen]** &quot;den Segmentnamen aus.

Die Seite mit den Segmentdetails wird angezeigt. Oben finden Sie eine Zusammenfassung der Segmentdefinition, Informationen zur Größe der qualifizierten Audience sowie zu Zielen, für die das Segment aktiviert wird.

![](../images/ui/overview/segment-details-summary.png)

### Segmentzusammenfassung

Der Abschnitt **[!UICONTROL Segmentzusammenfassung]** enthält Informationen wie ID, Name, Beschreibung und Details der Attribute.

Außerdem haben Sie die Möglichkeit, das Segment zu bearbeiten. Wenn Sie Segment **** bearbeiten auswählen, gelangen Sie zum [!DNL Segment Builder]. Weitere Informationen zur Verwendung des [!DNL Segment Builder] Arbeitsbereichs finden Sie im [[!DNL Segment Builder] Benutzerhandbuch](./segment-builder.md).

### Audience insgesamt im Segment

Der Abschnitt **[!UICONTROL Gesamte Audience im Segment]** zeigt die Gesamtanzahl der Profil an, die für das Segment qualifiziert sind.

Schätzungen werden anhand einer Stichprobengröße der Musterdaten dieses Tages erstellt. Wenn sich in Ihrem Profilspeicher weniger als 1 Million Entitäten befinden, wird der vollständige Datensatz verwendet. Bei zwischen 1 und 20 Millionen Entitäten werden 1 Million Entitäten verwendet; bei mehr als 20 Millionen Entitäten werden 5 % der Gesamtentitäten genutzt. Weiterführende Informationen zum Generieren von Segmentschätzungen finden Sie in der Anleitung zur Segmenterstellung im Abschnitt zum [Generieren von Schätzungen](../tutorials/create-a-segment.md#estimate-and-preview-an-audience).

### Aktivierte Ziele

Der Abschnitt **[!UICONTROL Aktivierte Ziele]** zeigt die Ziele an, für die dieses Segment aktiviert ist.

>[!NOTE]
>
> Ziele sind eine Funktion mit [!DNL Real-time Customer Data Platform]der Sie Daten auf externe Plattformen exportieren können. For more information on destinations, please read the [destinations overview](../../destinations/home.md). Um zu erfahren, wie Sie ein Segment an ein Ziel aktivieren, lesen Sie bitte das [Handbuch zur Aktivierung von Segmenten an ein Ziel](../../destinations/ui/activate-destinations.md).

### Profil-Beispiele

Darunter finden Sie eine Auswahl an Profilen, die für das Segment infrage kommen, mit detaillierten Informationen wie [!DNL Profile] ID, Vorname, Nachname und persönliche E-Mail-Adresse.

Die Art und Weise, wie die Datenerfassung ausgelöst wird, hängt von der Erfassungsmethode ab.

Zur Stapelverarbeitung wird der Profil-Store alle 15 Minuten automatisch überprüft, um festzustellen, ob ein neuer Stapel seit Ausführung des letzten Stichprobenauftrags erfolgreich aufgenommen wurde. Ist dies der Fall, wird der Profil-Store anschließend gescannt, um festzustellen, ob sich die Anzahl der Datensätze um mindestens 5 % verändert hat. Wenn diese Bedingungen erfüllt sind, wird ein neuer Stichprobenauftrag ausgelöst.

Zur Streaming-Erfassung wird der Profil-Store stündlich automatisch überprüft, um festzustellen, ob sich die Anzahl der Datensätze um mindestens 5 % verändert hat. Wenn diese Bedingung erfüllt ist, wird ein neuer Stichprobenauftrag ausgelöst.

Die Stichprobengröße der Überprüfung hängt von der Gesamtanzahl der Entitäten in Ihrem Profil-Store ab. Diese Stichprobengrößen sind in der folgenden Tabelle dargestellt:

| Entitäten im Profil Store | Stichprobengröße |
| ------------------------- | ----------- |
| Weniger als 1 Million | Vollständiger Datensatz |
| 1 bis 20 Mio. | 1 Mio. |
| Über 20 Mio. | 5 % des Gesamtbetrags |

Detailliertere Informationen zu den einzelnen IDs [!DNL Profile] finden Sie bei Auswahl der [!DNL Profile] ID. Weitere Informationen zu den Details eines Profils finden Sie im [[!DNL Real-time Customer Profile] Benutzerhandbuch](../../profile/ui/user-guide.md#profile-detail).

![](../images/ui/overview/segment-details-profiles.png)

## Erstellen eines Segments {#create-segment}

Selecting **[!UICONTROL Create segment]** in the top-right corner opens the [!DNL Segment Builder] workspace, where you can begin creating a segment definition.

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] Arbeitsbereich

[!DNL Segment Builder] bietet einen Rich-Workspace, mit dem Sie mit [!DNL Profile] Datenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag-and-Drop-Kacheln, die zur Darstellung von Dateneigenschaften dienen.

Weitere Informationen zur Verwendung des [!DNL Segment Builder] Arbeitsbereichs finden Sie im [[!DNL Segment Builder] Benutzerhandbuch](./segment-builder.md).

![](../images/ui/overview/segment-builder.png)

## Geplante Segmentierung {#scheduled-segmentation}

Nachdem Sie Segmentdefinitionen erstellt haben, können Sie diese durch eine On-Demand- oder geplante (kontinuierliche) Auswertung auswerten. Evaluation means moving [!DNL Real-time Customer Profile] data through segment definitions in order to produce corresponding audiences. Once created, the audiences are saved and stored so that they can be exported using [!DNL Experience Platform] APIs.

Bei der On-Demand-Auswertung wird die API zur Durchführung von Auswertungen und zum Aufbau von Zielgruppen nach Bedarf verwendet. Bei der geplanten Auswertung (auch „geplante Segmentierung“ genannt) können Sie hingegen einen Zeitplan erstellen, um die Segmentdefinitionen zu einem bestimmten Zeitpunkt (maximal einmal täglich) auszuwerten.

### Geplante Segmentierung aktivieren {#enable-scheduled-segmentation}

Die Aktivierung Ihrer Segmentdefinitionen für eine geplante Auswertung kann über die Benutzeroberfläche oder die API erfolgen. In the UI, return to the **[!UICONTROL Browse]** tab within **[!UICONTROL Segments]** and toggle on **[!UICONTROL Add all segments to schedule]**. Dadurch werden alle Segmente anhand des von Ihrer Organisation festgelegten Zeitplans evaluiert.

>[!NOTE]
>
>Scheduled evaluation can be enabled for sandboxes with a maximum of five (5) merge policies for [!DNL XDM Individual Profile]. If your organization has more than five merge policies for [!DNL XDM Individual Profile] within a single sandbox environment, you will not be able to use scheduled evaluation.

Zeitpläne können derzeit nur mit der API erstellt werden. Ausführliche Anweisungen zum Erstellen, Bearbeiten und Verwenden von Zeitplänen mithilfe der API finden Sie im Tutorial zum Auswerten und Aufrufen von Segmentergebnissen, insbesondere im Abschnitt zur [geplanten Auswertung mithilfe der API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## Streaming-Segmentierung {#streaming-segmentation}

Streaming-Segmentierung ist die Fähigkeit, Segmentierungen in Echtzeit durchzuführen und dabei auf den Datenreichtum [!DNL Platform] zu konzentrieren. Mit der Streaming-Segmentierung erfolgt die Segmentqualifizierung jetzt, wenn Daten eingehen, [!DNL Platform]was die Planung und Ausführung von Segmentierungsaufträgen verringert.

Weitere Informationen zur Streaming-Segmentierung finden Sie im Benutzerhandbuch zur [Streaming-Segmentierung](./streaming-segmentation.md).

>[!NOTE]
>
>Damit Streaming-Segmentierung funktioniert, müssen Sie die geplante Segmentierung für das Unternehmen aktivieren. For details on enabling scheduled segmentation, please refer to [the streaming segmentation section in this user guide](#scheduled-segmentation).

## Rechtsverletzungen

>[!NOTE]
>
>Richtlinienverletzungen gelten nur, wenn Sie ein Segment erstellen, das einem Ziel zugewiesen wurde.

Nachdem Sie Ihr Segment erstellt haben, wird das Segment von Adobe Experience Platform Data Governance analysiert, um sicherzustellen, dass es keine Richtlinienverletzungen innerhalb des Segments gibt. Weitere Informationen finden Sie in der [[!DNL Data Governance] Übersicht über ](../../data-governance/home.md).

![](../images/ui/overview/segment-dule-policy-violations.png)

## Nächste Schritte und zusätzliche Ressourcen {#next-steps}

Die [!DNL Segmentation Service] Benutzeroberfläche bietet einen umfassenden Arbeitsablauf, mit dem Sie marktfähige Audiencen von [!DNL Real-time Customer Profile] Daten isolieren können.

Weitere Informationen erhalten Sie [!DNL Segmentation Service]in der Dokumentation. Weitere Informationen zur Verwendung der [!DNL Segmentation Service] API finden Sie im [[!DNL Segmentation Service] Entwicklerhandbuch](../api/overview.md).
