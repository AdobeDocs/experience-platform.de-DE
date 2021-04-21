---
keywords: Experience Platform;Startseite;beliebte Themen;Segmentierungsdienst;Segmentierungsdienst;Segmentierungsdienst;Benutzerhandbuch;Segmentierungsleitfaden;Segmentaufbau;Segmentaufbau;Realisierung;Bestehend;Ausstieg;
solution: Experience Platform
title: Handbuch zur Benutzeroberfläche des Segmentdienstes
topic-legacy: ui guide
description: Der Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche zum Erstellen und Verwalten von Segmentdefinitionen.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 22%

---

# Handbuch zur Benutzeroberfläche des Segmentdienstes

[!DNL Adobe Experience Platform Segmentation Service] stellt eine Benutzeroberfläche zum Erstellen und Verwalten von Segmentdefinitionen bereit.

## Erste Schritte

Das Arbeiten mit Segmentdefinitionen erfordert ein Verständnis der verschiedenen [!DNL Experience Platform]-Dienste, die mit der Segmentierung verbunden sind. Bevor Sie dieses Benutzerhandbuch lesen, lesen Sie bitte die Dokumentation für folgende Dienste:

- [[!DNL Segmentation Service]](../home.md):  [!DNL Segmentation Service] ermöglicht es Ihnen, Daten,  [!DNL Experience Platform] die in Bezug auf Einzelpersonen (z. B. Kunden, Potenzieller Kunde, Benutzer oder Organisationen) gespeichert sind, in kleinere Gruppen zu unterteilen.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Ermöglicht die Erstellung von Profilen von Kunden durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, in die  [!DNL Platform]eingegriffen wird.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

Außerdem sollten Sie zwei Schlüsselbegriffe kennen, die in diesem Dokument verwendet werden, und den Unterschied zwischen ihnen verstehen:
- **Segmentdefinition**: Der Regelsatz, der zur Beschreibung wichtiger Merkmale oder Verhaltensweisen einer Zielgruppe verwendet wird.
- **Audience**: Der resultierende Satz von Profilen, die den Kriterien einer Segmentdefinition entsprechen.

## Übersicht

Wählen Sie in der linken Navigation [[!DNL Experience Platform] UI](http://platform.adobe.com/) **[!UICONTROL Segmente]** aus, um die Registerkarte **[!UICONTROL Übersicht]** zu öffnen. Diese Registerkarte enthält Links zu Dokumentation und Videos, die Ihnen helfen, Segmente zu verstehen und mit ihnen zu arbeiten.

![](../images/ui/overview/segment-overview.png)

## Durchsuchen

Wählen Sie die Registerkarte **[!UICONTROL Durchsuchen]**, um eine Liste aller Segmentdefinitionen für Ihre IMS-Organisation anzuzeigen.

![](../images/ui/overview/segment-browse-all.png)

Diese Ansicht Liste Informationen zur Segmentdefinition, einschließlich Aufschlüsselung, Ruhephase, Profil-Anzahl, Bewertungsmethode, erstelltes Datum und Datum der letzten Änderung.

Die Aufschlüsselung zeigt ein Balkendiagramm mit dem Prozentwert der Profil, die zu den folgenden Statuswerten gehören: [!UICONTROL Eingegeben], [!UICONTROL Realisiert] und [!UICONTROL Ausstieg].

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

Wenn Sie **[!UICONTROL Hinzufügen alle Segmente umschalten, um]** einzuplanen, wird die geplante Segmentierung aktiviert. Weitere Informationen zur geplanten Segmentierung finden Sie im Abschnitt [Geplante Segmentierung dieses Benutzerhandbuchs](#scheduled-segmentation).

Wenn Sie **[!UICONTROL Segment]** erstellen auswählen, gelangen Sie zum Segmentaufbau. Weitere Informationen zum Erstellen von Segmenten finden Sie im Abschnitt [Erstellen eines Segments im Benutzerhandbuch](#create-segment).

![](../images/ui/overview/segment-browse-top.png)

Die rechte Seitenleiste enthält Informationen zu allen Segmenten innerhalb der IMS-Organisation, listet die Gesamtzahl der Segmente, das letzte Bewertungsdatum, das nächste Bewertungsdatum sowie eine Aufschlüsselung der Segmente nach Bewertungsmethode auf.

![](../images/ui/overview/segment-browse-segment-info.png)

Durch Auswahl der Segmentdefinitionszeile erhalten Sie eine Übersicht über die Segmentdefinition, einschließlich Optionen zum Bearbeiten oder Löschen des Segments, der qualifizierten Audience für das Segment, der Gesamtgröße der Audience zusätzlich zu Segmentname, -beschreibung, -bewertungsverfahren, Erstellungsdatum und Datum der letzten Änderung.

![](../images/ui/overview/segment-browse-details.png)

## Details zur Segmentdefinition {#segment-details}

Um weitere Details zu einer bestimmten Segmentdefinition anzuzeigen, wählen Sie den Namen eines Segments auf der Registerkarte **[!UICONTROL Durchsuchen]** aus.

Die Seite mit den Segmentdetails wird angezeigt. Oben finden Sie eine Zusammenfassung der Segmentdefinition, Informationen zur Größe der qualifizierten Audience sowie zu Zielen, für die das Segment aktiviert wird.

![](../images/ui/overview/segment-details-summary.png)

### Segmentzusammenfassung

Der Abschnitt **[!UICONTROL Segmentzusammenfassung]** enthält Informationen wie ID, Name, Beschreibung und Details der Attribute.

Außerdem haben Sie die Möglichkeit, das Segment zu bearbeiten. Wenn Sie **[!UICONTROL Segment bearbeiten]** auswählen, gelangen Sie zum [!DNL Segment Builder]. Weitere Informationen zur Verwendung des Arbeitsbereichs [!DNL Segment Builder] finden Sie im [[!DNL Segment Builder] Benutzerhandbuch](./segment-builder.md).

### Audience insgesamt im Segment

Der Abschnitt **[!UICONTROL Audience insgesamt in segment]** zeigt die Gesamtanzahl der Profil an, die für das Segment qualifiziert sind.

Schätzungen werden anhand einer Stichprobengröße der Musterdaten dieses Tages erstellt. Wenn sich in Ihrem Profilspeicher weniger als 1 Million Entitäten befinden, wird der vollständige Datensatz verwendet. Bei zwischen 1 und 20 Millionen Entitäten werden 1 Million Entitäten verwendet; bei mehr als 20 Millionen Entitäten werden 5 % der Gesamtentitäten genutzt. Weiterführende Informationen zum Generieren von Segmentschätzungen finden Sie in der Anleitung zur Segmenterstellung im Abschnitt zum [Generieren von Schätzungen](../tutorials/create-a-segment.md#estimate-and-preview-an-audience).

### Aktivierte Ziele

Der Abschnitt **[!UICONTROL Aktivierte Ziele]** zeigt die Ziele an, für die dieses Segment aktiviert ist.

>[!NOTE]
>
> Ziele sind eine Funktion, die mit [!DNL Real-time Customer Data Platform] verfügbar ist und mit der Sie Daten auf externe Plattformen exportieren können. Weitere Informationen zu Zielen finden Sie im [Überblick über Ziele](../../destinations/home.md). Um zu erfahren, wie Sie ein Segment zu einem Ziel aktivieren, lesen Sie bitte das Handbuch [zur Aktivierung von Segmenten zu einem Ziel](../../destinations/ui/activate-destinations.md).

### Profil-Beispiele

Darunter finden Sie eine Auswahl an Profilen, die für das Segment infrage kommen, mit detaillierten Informationen wie der [!DNL Profile]-ID, dem Vornamen, dem Nachnamen und der persönlichen E-Mail-Adresse.

Die Art und Weise, wie die Datenerfassung ausgelöst wird, hängt von der Erfassungsmethode ab.

Zur Stapelverarbeitung wird der Profil-Store alle 15 Minuten automatisch überprüft, um festzustellen, ob ein neuer Stapel seit Ausführung des letzten Stichprobenauftrags erfolgreich aufgenommen wurde. Ist dies der Fall, wird der Profil-Store anschließend gescannt, um festzustellen, ob sich die Anzahl der Datensätze um mindestens 5 % verändert hat. Wenn diese Bedingungen erfüllt sind, wird ein neuer Stichprobenauftrag ausgelöst.

Zur Streaming-Erfassung wird der Profil-Store stündlich automatisch überprüft, um festzustellen, ob sich die Anzahl der Datensätze um mindestens 5 % verändert hat. Wenn diese Bedingung erfüllt ist, wird ein neuer Stichprobenauftrag ausgelöst.

Die Stichprobengröße der Überprüfung hängt von der Gesamtanzahl der Entitäten in Ihrem Profil-Store ab. Diese Stichprobengrößen sind in der folgenden Tabelle dargestellt:

| Entitäten im Profil Store | Stichprobengröße |
| ------------------------- | ----------- |
| Weniger als 1 Million | Vollständiger Datensatz |
| 1 bis 20 Mio. | 1 Mio. |
| Über 20 Mio. | 5 % des Gesamtbetrags |

Detailliertere Informationen zu jedem [!DNL Profile] können Sie durch Auswahl der [!DNL Profile]-ID sehen. Weitere Informationen zu den Details eines Profils finden Sie im [[!DNL Real-time Customer Profile] Benutzerhandbuch](../../profile/ui/user-guide.md#profile-detail).

![](../images/ui/overview/segment-details-profiles.png)

## Erstellen eines Segments {#create-segment}

Wenn Sie in der oberen rechten Ecke **[!UICONTROL Segment erstellen]** auswählen, wird der Arbeitsbereich [!DNL Segment Builder] geöffnet, in dem Sie mit der Erstellung einer Segmentdefinition beginnen können.

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] Arbeitsbereich

[!DNL Segment Builder] bietet einen Rich-Workspace, mit dem Sie mit  [!DNL Profile] Datenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag-and-Drop-Kacheln, die zur Darstellung von Dateneigenschaften dienen.

Weitere Informationen zur Verwendung des Arbeitsbereichs [!DNL Segment Builder] finden Sie im [[!DNL Segment Builder] Benutzerhandbuch](./segment-builder.md).

![](../images/ui/overview/segment-builder.png)

## Geplante Segmentierung {#scheduled-segmentation}

Nachdem Sie Segmentdefinitionen erstellt haben, können Sie diese durch eine On-Demand- oder geplante (kontinuierliche) Auswertung auswerten. Bewertung bedeutet, dass [!DNL Real-time Customer Profile]-Daten durch Segmentdefinitionen verschoben werden, um entsprechende Audiencen zu erhalten. Nach der Erstellung werden die Audiencen gespeichert und gespeichert, damit sie mit [!DNL Experience Platform]-APIs exportiert werden können.

Bei der On-Demand-Auswertung wird die API zur Durchführung von Auswertungen und zum Aufbau von Zielgruppen nach Bedarf verwendet. Bei der geplanten Auswertung (auch „geplante Segmentierung“ genannt) können Sie hingegen einen Zeitplan erstellen, um die Segmentdefinitionen zu einem bestimmten Zeitpunkt (maximal einmal täglich) auszuwerten.

### Geplante Segmentierung aktivieren {#enable-scheduled-segmentation}

Die Aktivierung Ihrer Segmentdefinitionen für eine geplante Auswertung kann über die Benutzeroberfläche oder die API erfolgen. Kehren Sie in der Benutzeroberfläche zum Register **[!UICONTROL Durchsuchen]** innerhalb von **[!UICONTROL Segmente]** zurück und schalten Sie **[!UICONTROL Hinzufügen alle Segmente ein, um]** einzuplanen. Dadurch werden alle Segmente anhand des von Ihrer Organisation festgelegten Zeitplans evaluiert.

>[!NOTE]
>
>Geplante Evaluierung kann für Sandboxen mit maximal fünf (5) Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] aktiviert werden. Wenn Ihr Unternehmen über mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] in einer einzelnen Sandbox-Umgebung verfügt, können Sie keine geplante Auswertung verwenden.

Zeitpläne können derzeit nur mit der API erstellt werden. Ausführliche Anweisungen zum Erstellen, Bearbeiten und Verwenden von Zeitplänen mithilfe der API finden Sie im Tutorial zum Auswerten und Aufrufen von Segmentergebnissen, insbesondere im Abschnitt zur [geplanten Auswertung mithilfe der API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## Streaming-Segmentierung {#streaming-segmentation}

Streaming-Segmentierung ist die Fähigkeit, eine Segmentierung für [!DNL Platform] in nahezu Echtzeit durchzuführen, während der Schwerpunkt auf Datenreichweite liegt. Mit der Streaming-Segmentierung erfolgt die Segmentqualifizierung jetzt, wenn Daten nach [!DNL Platform] gelangen, was die Notwendigkeit verringert, Segmentierungsaufträge zu planen und auszuführen.

Weitere Informationen zur Streaming-Segmentierung finden Sie im Benutzerhandbuch [Streaming-Segmentierung](./streaming-segmentation.md).

>[!NOTE]
>
>Damit Streaming-Segmentierung funktioniert, müssen Sie die geplante Segmentierung für das Unternehmen aktivieren. Weitere Informationen zum Aktivieren der geplanten Segmentierung finden Sie im Abschnitt [Streaming-Segmentierung in diesem Benutzerhandbuch](#scheduled-segmentation).

## Kantensegmentierung {#edge-segmentation}

Bei der Edge-Segmentierung können Segmente direkt am Rand in der Plattform ausgewertet werden, sodass dieselben Anwendungsfälle für die Personalisierung der Seite und der nächsten Seite möglich sind.

Weitere Informationen zur Segmentierung der Edge finden Sie im [UI-Handbuch zur Segmentierung der Kante](./edge-segmentation.md)

## Rechtsverletzungen

>[!NOTE]
>
>Richtlinienverletzungen gelten nur, wenn Sie ein Segment erstellen, das einem Ziel zugewiesen wurde.

Nachdem Sie Ihr Segment erstellt haben, wird das Segment von Adobe Experience Platform Data Governance analysiert, um sicherzustellen, dass es keine Richtlinienverletzungen innerhalb des Segments gibt. Weitere Informationen finden Sie in der [[!DNL Data Governance] Übersicht über ](../../data-governance/home.md).

![](../images/ui/overview/segment-dule-policy-violations.png)

## Nächste Schritte und zusätzliche Ressourcen {#next-steps}

Die Benutzeroberfläche [!DNL Segmentation Service] bietet einen umfassenden Arbeitsablauf, mit dem Sie markierbare Audiencen aus [!DNL Real-time Customer Profile]-Daten isolieren können.

Um mehr über [!DNL Segmentation Service] zu erfahren, lesen Sie bitte die Dokumentation weiter. Weitere Informationen zur Verwendung der [!DNL Segmentation Service]-API finden Sie im [[!DNL Segmentation Service] Entwicklerhandbuch](../api/overview.md).
