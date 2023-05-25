---
keywords: Experience Platform;Startseite;beliebte Themen;Segmentierungs-Service;Segmentierung;Segmentierungs-Dienst;Benutzerhandbuch;UI-Handbuch;Handbuch zur Segmentierungs-Benutzeroberfläche;segment builder;Segment Builder;realisiert;vorhanden;Beenden;
solution: Experience Platform
title: Handbuch zur Benutzeroberfläche des Segmentierungs-Service
description: Der Segmentierungs-Service von Adobe Experience Platform bietet eine Benutzeroberfläche zum Erstellen und Verwalten von Segmentdefinitionen.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 207cddae6b632866d564729de49d28fc5c29ef7f
workflow-type: tm+mt
source-wordcount: '2646'
ht-degree: 97%

---

# Handbuch zur Benutzeroberfläche des Segmentierungs-Service

[!DNL Adobe Experience Platform Segmentation Service] bietet eine Benutzeroberfläche zum Erstellen und Verwalten von Segmentdefinitionen.

## Erste Schritte

Das Verwenden von Segmentdefinitionen setzt ein Verständnis der verschiedenen [!DNL Experience Platform]-Services voraus, die mit der Segmentierung verbunden sind. Bevor Sie dieses Benutzerhandbuch lesen, lesen Sie bitte die Dokumentation für folgende Services:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] ermöglicht die Aufteilung der in [!DNL Experience Platform] gespeicherten Daten, die sich auf Einzelanwender (wie Kunden, Interessenten, Benutzer oder Organisationen) beziehen, in kleinere Gruppen.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Ermöglicht die Erstellung von Kundenprofilen durch das Zusammenführen von Identitäten aus unterschiedlichen Datenquellen, die in [!DNL Platform] aufgenommen werden.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten durch [!DNL Platform] organisiert werden. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profile und Ereignisse gemäß den [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md) aufgenommen werden.

Außerdem sollten Sie zwei Schlüsselbegriffe kennen, die in diesem Dokument verwendet werden, und den Unterschied zwischen ihnen verstehen:
- **Segmentdefinition**: Der Regelsatz, der zur Beschreibung wichtiger Merkmale oder Verhaltensweisen einer Zielgruppe verwendet wird.
- **Zielgruppe**: Der resultierende Satz von Profilen, die den Kriterien einer Segmentdefinition entsprechen. Dieser kann entweder über Adobe Experience Platform (Platform-generierte Zielgruppe) oder aus einer externen Quelle (extern generierte Zielgruppe) erstellt werden.

## Übersicht

Wählen Sie in der Benutzeroberfläche von Experience Platform im linken Navigationsbereich die Option **[!UICONTROL Segmente]** aus, um die Registerkarte **[!UICONTROL Überblick]** mit dem Dashboard [!UICONTROL Segmente] zu öffnen.

>[!NOTE]
>
>Wenn Ihre Organisation erst seit kurzem Platform nutzt und noch keine aktiven Profildatensätze oder Zusammenführungsrichtlinien erstellt hat, ist das [!UICONTROL Segmente]-Dashboard nicht sichtbar. Stattdessen werden auf der Registerkarte [!UICONTROL Überblick] Links und Dokumentation angezeigt, die Ihnen bei den ersten Schritten im Zusammenhang mit Segmenten helfen können.

### [!UICONTROL Segmente]-Dashboard {#segments-dashboard}

Im **[!UICONTROL Segmente]**-Dashboard werden Schlüsselmetriken im Zusammenhang mit den Segmentdaten Ihres Unternehmens beschrieben.

Weitere Informationen finden Sie im [Handbuch für das Segment-Dashboard](../../dashboards/guides/segments.md).

![Das Segment-Dashboard wird angezeigt. Darin werden verschiedene Widgets angezeigt, darunter die Zielgruppengröße, Profile nach Identität, Identitätsüberlagerung und der Änderungs-Trend der Zielgruppengröße.](../../dashboards/images/segments/dashboard-overview.png)

## Durchsuchen {#browse}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_churncolumnname"
>title="Abwanderung"
>abstract="Die Abwanderung stellt den Prozentsatz der Profile dar, die sich innerhalb einer Segmentdefinition ändern, verglichen mit der letzten Ausführung des Segmentvorgangs."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_evaluationmethodcolumnname"
>title="Auswertungsmethode"
>abstract="Zu den Auswertungsmethoden für Segmente gehören Batch, Streaming und Edge."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_addallsegmentstoschedule"
>title="Alle Segmente zum Zeitplan hinzufügen"
>abstract="Aktivieren Sie diese Option, um alle Batch-Auswertungssegmente in die tägliche geplante Aktualisierung einzuschließen. Deaktivieren Sie sie, um alle Segmente aus der geplanten Aktualisierung zu entfernen."

Wählen Sie die Registerkarte **[!UICONTROL Durchsuchen]**, um eine Liste aller Segmentdefinitionen für Ihre Organisation anzuzeigen.

![Der Bildschirm zum Durchsuchen von Segmenten wird angezeigt. Eine Liste aller Segmente, die zur Organisation gehören, wird angezeigt.](../images/ui/overview/segment-browse-all.png)

Diese Ansicht listet Daten zur Segmentdefinition auf, einschließlich der Profilanzahl, des Erstellungsdatums und des Datums der letzten Änderung.

Sie können dieser Anzeige zusätzliche Felder hinzufügen, indem Sie das ![Filterattribut-Symbol](../images/ui/overview/filter-attribute.png) auswählen. Zu diesen zusätzlichen Feldern gehören Aufschlüsselung, Auswertungsmethode und Auftrags-ID.

Wenn die Aufschlüsselung ausgewählt ist, wird ein Balkendiagramm angezeigt, das den prozentualen Anteil der Profile in jedem der folgenden berechneten Profilstatus anzeigt: [!UICONTROL Realisiert], [!UICONTROL Bestehend] und [!UICONTROL Verlassen]. Außerdem ist die auf der Registerkarte [!UICONTROL Durchsuchen] angezeigte Aufschlüsselung die genaueste Aufschlüsselung des Segmentstatus. Wenn diese Zahl von den Angaben auf der Registerkarte [!UICONTROL Übersicht] abweicht, sollten Sie als korrekte Informationsquelle die Zahlen auf der Registerkarte [!UICONTROL Durchsuchen] verwenden, da die Zahlen auf der Registerkarte [!UICONTROL Übersicht] nur einmal pro Tag aktualisiert werden.

| Status | Beschreibung |
| ------ | ----------- |
| [!UICONTROL Realisiert] | Die Anzahl der Profile, die **qualifiziert** für das Segment in den letzten 24 Stunden seit der Ausführung des letzten Batch-Segmentauftrags. |
| [!UICONTROL Bestehend] | Die Anzahl der Profile, die **verbleiben** in dem Segment in den letzten 24 Stunden seit der Ausführung des letzten Batch-Segmentauftrags. |
| [!UICONTROL Verlassen] | Die Anzahl der Profile, die **beendet** das Segment in den letzten 24 Stunden seit Ausführung des letzten Batch-Segmentauftrags. |

Die Auswertungsmethode kann entweder Streaming, Batch oder Edge sein. Streaming-Segmente werden konstant ausgewertet, sobald Daten in das System strömen. Batch-Segmente werden gemäß einem festgelegten Zeitplan ausgewertet. Edge-Segmente werden in Echtzeit ausgewertet, was die Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.

![Die Segmente auf der Seite zum Durchsuchen von Segmenten sind hervorgehoben.](../images/ui/overview/segment-browse-segments.png)

Oben auf der Seite finden Sie Optionen zum Hinzufügen aller Segmente zu einem Zeitplan und zum Erstellen eines neuen Segments.

Durch Aktivieren der Option **[!UICONTROL Alle Segmente zum Zeitplan hinzufügen]** wird die geplante Segmentierung aktiviert. Weitere Informationen zur geplanten Segmentierung finden Sie im [Abschnitt „Geplante Segmentierung“ in diesem Benutzerhandbuch](#scheduled-segmentation).

Wenn Sie **[!UICONTROL Segment erstellen]** wählen, gelangen Sie zum Segment Builder. Um mehr über die Erstellung von Segmenten zu erfahren, lesen Sie bitte den Abschnitt zum [Erstellen eines Segments im Benutzerhandbuch](#create-segment).

![Die obere Navigationsleiste auf der Seite zum Durchsuchen von Segmenten ist hervorgehoben. Diese Leiste enthält einen Umschalter zum Hinzufügen aller Segmente zu einem Zeitplan und einen Button zum Erstellen eines Segments.](../images/ui/overview/segment-browse-top.png)

Die rechte Seitenleiste enthält Informationen über alle Segmente innerhalb der Organisation, die Gesamtzahl der Segmente, das letzte Bewertungsdatum, das nächste Bewertungsdatum sowie eine Aufschlüsselung der Segmente nach Bewertungsmethode.

![Die rechte Seitenleiste auf der Seite zum Durchsuchen von Segmenten ist hervorgehoben. Es werden Informationen zu den Segmenten in der Organisation angezeigt. Dazu gehören Informationen wie die Gesamtanzahl der Segmente, die letzte ausgewertete Zeit, die nächste ausgewertete Zeit sowie eine Aufschlüsselung der verschiedenen Segmenttypen.](../images/ui/overview/segment-browse-segment-info.png)

Wenn Sie die Zeile der Segmentdefinition auswählen, erhalten Sie eine Zusammenfassung der Segmentdefinition, einschließlich der Optionen zum Bearbeiten oder Löschen des Segments, zum Aktivieren des Segments für ein Ziel, zur qualifizierten Zielgruppe für das Segment, zur Gesamtgröße der Zielgruppe sowie zum Namen des Segments, zur Beschreibung, zur Bewertungsmethode, zum Erstellungsdatum und zum Datum der letzten Änderung.

>[!NOTE]
>
> Sie können ein Segment, das in einer Zielaktivierung verwendet wird, **nicht** löschen.

![Es werden Details zum ausgewählten Segment angezeigt. Dies umfasst Details zur Anzahl der qualifizierten Profile, zur prozentualen Verteilung der qualifizierten Profile im Vergleich zu den Gesamtprofilen sowie zum letzten Auswertungsdatum.](../images/ui/overview/segment-browse-details.png)

## Details zur Segmentdefinition {#segment-details}

Um weitere Details zu einer bestimmten Segmentdefinition anzusehen, wählen Sie in der Registerkarte **[!UICONTROL Durchsuchen]** den Namen eines Segments aus.

Die Seite mit den Segmentdetails wird angezeigt. Oben finden Sie eine Zusammenfassung der Segmentdefinition, Informationen zur Größe der qualifizierten Zielgruppe sowie Ziele, für die das Segment aktiviert wurde.

![Die Seite mit Details zur Segmentdefinition wird angezeigt. Die Segmentzusammenfassung, die Gesamt-Zielgruppe im Segment und die aktivierten Zielkarten sind hervorgehoben.](../images/ui/overview/segment-details-summary.png)

### Segmentzusammenfassung {#segment-summary}

Die **[!UICONTROL Segmentzusammenfassung]** enthält Informationen wie die ID, den Namen, die Beschreibung und Details der Attribute.

Darüber hinaus haben Sie die Option, das Segment entweder für ein Ziel zu aktivieren oder es zu bearbeiten. Wenn Sie **[!UICONTROL Für Ziel aktivieren]** auswählen, können Sie das Segment für ein Ziel aktivieren. Detaillierte Informationen zum Aktivieren eines Segments für ein Ziel finden Sie unter [Aktivierung – Übersicht](../../destinations/ui/activation-overview.md).

![Der Button „Für Ziel aktivieren“ ist hervorgehoben.](../images/ui/overview/segment-details-activate.png)

Wenn Sie **[!UICONTROL Segment bearbeiten]** auswählen, werden Sie zum [!DNL Segment Builder] weitergeleitet. Detaillierte Informationen zur Verwendung des Arbeitsbereichs von [!DNL Segment Builder] finden Sie im [[!DNL Segment Builder] Benutzerhandbuch](./segment-builder.md).

![](../images/ui/overview/segment-details-edit-segment.png)

### Gesamtzielgruppe im Segment

Im Abschnitt **[!UICONTROL Gesamtzielgruppe im Segment]** wird die Gesamtzahl der Profile angezeigt, die für das Segment qualifiziert sind.

Die Schätzungen werden anhand einer Stichprobengröße aus den Daten des jeweiligen Tages generiert. Wenn sich in Ihrem Profilspeicher weniger als 1 Million Entitäten befinden, wird der vollständige Datensatz verwendet. Bei zwischen 1 und 20 Millionen Entitäten werden 1 Million Entitäten verwendet; bei mehr als 20 Millionen Entitäten werden 5 % der Gesamtentitäten genutzt. Weiterführende Informationen zum Generieren von Segmentschätzungen finden Sie in der Anleitung zur Segmenterstellung im Abschnitt zum [Generieren von Schätzungen](../tutorials/create-a-segment.md#estimate-and-preview-an-audience).

### Aktivierte Ziele

Der Abschnitt **[!UICONTROL Aktivierte Ziele]** zeigt die Ziele, für die dieses Segment aktiviert ist.

>[!NOTE]
>
> Ziele sind eine Funktion, die mit [!DNL Adobe Real-Time Customer Data Platform] verfügbar ist und es Ihnen ermöglicht, Daten auf externe Plattformen zu exportieren. Weitere Informationen zu Zielen finden Sie unter [Ziele – Übersicht](../../destinations/home.md). Informationen zum Aktivieren eines Segments für ein Ziel finden Sie unter [Aktivierung – Übersicht](../../destinations/ui/activation-overview.md).

### Beispielprofile

Unten finden Sie eine Auswahl von Profilen, die für das Segment qualifiziert sind, mit detaillierten Informationen, einschließlich [!DNL Profile]-ID, Vorname, Nachname und persönlicher E-Mail-Adresse.

Die Methode, mit der das Daten-Sampling ausgelöst wird, hängt von der Art der Aufnahme ab.

Bei der Batch-Aufnahme wird der Profilspeicher automatisch alle fünfzehn Minuten gescannt, um festzustellen, ob seit dem letzten Sampling-Auftrag ein neuer Batch erfolgreich aufgenommen wurde. Wenn dies der Fall ist, wird der Profilspeicher anschließend daraufhin überprüft, ob sich die Anzahl der Datensätze um mindestens 5 % geändert hat. Wenn diese Bedingungen erfüllt sind, wird ein neuer Sampling-Auftrag ausgelöst.

Bei der Streaming-Aufnahme wird der Profilspeicher automatisch jede Stunde überprüft, um festzustellen, ob sich die Anzahl der Datensätze um mindestens 5 % geändert hat. Wenn diese Bedingung erfüllt ist, wird ein neuer Sampling-Auftrag ausgelöst.

Die Stichprobengröße der Überprüfung hängt von der Gesamtzahl der Entitäten in Ihrem Profilspeicher ab. Diese Stichprobengrößen sind in der folgenden Tabelle dargestellt:

| Entitäten im Profilspeicher | Stichprobengröße |
| ------------------------- | ----------- |
| Weniger als 1 Million | Vollständiger Datensatz |
| 1 bis 20 Millionen | 1 Million |
| Über 20 Millionen | 5 % der Gesamtgröße |

Ausführlichere Informationen zu jedem [!DNL Profile] erhalten Sie, wenn Sie auf die [!DNL Profile]-ID klicken. Um mehr über die Details eines Profils zu erfahren, lesen Sie bitte das [[!DNL Real-Time Customer Profile] Benutzerhandbuch](../../profile/ui/user-guide.md#profile-detail).

![Die Beispielprofile für die Segmentdefinition sind hervorgehoben. Zu den Beispielprofilinformationen gehören die Profil-ID, der Vorname, der Nachname und die E-Mail-Adresse der Person.](../images/ui/overview/segment-details-profiles.png)

## Erstellen eines Segments {#create-segment}

Wenn Sie in der rechten oberen Ecke auf **[!UICONTROL Erstellen eines Segments]** klicken, öffnet sich der [!DNL Segment Builder]-Arbeitsbereich, in dem Sie mit der Erstellung einer Segmentdefinition beginnen können.

![Auf der Seite zum Durchsuchen von Segmenten ist der Button „Segment erstellen“ hervorgehoben.](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder]-Arbeitsbereich

[!DNL Segment Builder] bietet einen umfangreichen Arbeitsbereich, in dem Sie mit [!DNL Profile]-Datenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag-and-Drop-Kacheln, die Dateneigenschaften entsprechen.

Detaillierte Informationen zur Verwendung des Arbeitsbereichs [!DNL Segment Builder] finden Sie im [[!DNL Segment Builder] Benutzerhandbuch](./segment-builder.md).

![Der Segment Builder-Arbeitsbereich wird angezeigt.](../images/ui/overview/segment-builder.png)

## Geplante Segmentierung {#scheduled-segmentation}

Nachdem Sie Segmentdefinitionen erstellt haben, können Sie diese durch eine On-Demand- oder geplante (kontinuierliche) Auswertung auswerten. Auswertung bedeutet, dass [!DNL Real-Time Customer Profile]-Daten durch Segmentdefinitionen bewegt werden, um entsprechende Zielgruppen zu erreichen. Nach der Erstellung werden die Zielgruppen gespeichert und aufbewahrt, sodass sie über die APIs von [!DNL Experience Platform] exportiert werden können.

Bei der On-Demand-Auswertung wird die API zur Durchführung von Auswertungen und zum Aufbau von Zielgruppen nach Bedarf verwendet. Bei der geplanten Auswertung (auch „geplante Segmentierung“ genannt) können Sie hingegen einen Zeitplan erstellen, um die Segmentdefinitionen zu einem bestimmten Zeitpunkt (maximal einmal täglich) auszuwerten.

### Aktivieren der geplanten Segmentierung {#enable-scheduled-segmentation}

Die Aktivierung Ihrer Segmentdefinitionen für eine geplante Auswertung kann über die Benutzeroberfläche oder die API erfolgen. Kehren Sie in der Benutzeroberfläche unter **[!UICONTROL Segmente]** zur Registerkarte **[!UICONTROL Durchsuchen]** zurück und legen Sie den Umschalter auf **[!UICONTROL Alle Segmente zum Zeitplan hinzufügen]** fest. Dadurch werden alle Segmente anhand des von Ihrer Organisation festgelegten Zeitplans ausgewertet.

>[!NOTE]
>
>Die geplante Auswertung kann für Sandboxes mit maximal fünf (5) Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] aktiviert werden. Wenn Ihre Organisation in einer Sandbox-Umgebung über mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] verfügt, können Sie keine geplante Auswertung verwenden.

Zeitpläne können derzeit nur mit der API erstellt werden. Ausführliche Anweisungen zum Erstellen, Bearbeiten und Verwenden von Zeitplänen mithilfe der API finden Sie im Tutorial zum Auswerten und Aufrufen von Segmentergebnissen, insbesondere im Abschnitt zur [geplanten Auswertung mithilfe der API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![Der Umschalter zum Hinzufügen aller Segmente zu einem Zeitplan ist auf der Seite zum Durchsuchen von Segmenten hervorgehoben.](../images/ui/overview/segment-browse-scheduled.png)

## Zielgruppen {#audiences}

>[!IMPORTANT]
>
>Die Zielgruppen-Funktionalität befindet sich derzeit in einer begrenzten Beta-Phase und ist nicht für alle Benutzenden verfügbar. Dokumentation und Funktionalitäten können sich ändern.

Wählen Sie die Registerkarte **[!UICONTROL Zielgruppen]** aus, um eine Liste aller Zielgruppen für Ihre Organisation anzuzeigen.

![Eine Liste von Zielgruppen für Ihre Organisation.](../images/ui/overview/list-audiences.png)

Standardmäßig enthält diese Ansicht Informationen zu den Zielgruppen, einschließlich Name, Profilanzahl, Ursprung, Erstellungsdatum und Datum der letzten Änderung.

Sie können das Symbol ![Tabelle anpassen](../images/ui/overview/customize-table.png) auswählen, um zu ändern, welche Felder angezeigt werden.

![Die Schaltfläche „Tabelle anpassen“ ist hervorgehoben. Durch Auswahl dieser Schaltfläche können Sie die Felder anpassen, die auf der Seite zum Durchsuchen von Zielgruppen angezeigt werden.](../images/ui/overview/select-customize-table.png)

Es wird ein Pop-up mit allen Feldern angezeigt, die in der Tabelle angezeigt werden können.

![Die Attribute, die für den Abschnitt „Zielgruppen durchsuchen“ angezeigt werden können.](../images/ui/overview/customize-table-attributes.png)

| Feld | Beschreibung |
| ----- | ----------- | 
| [!UICONTROL Name] | Der Name der Zielgruppe. |
| [!UICONTROL Anzahl der Profile] | Die Gesamtzahl der Profile, die für die Zielgruppe qualifiziert sind. |
| [!UICONTROL Herkunft] | Die Herkunft der Zielgruppe. Wenn diese Zielgruppe von Platform generiert wurde, ist ihr Ursprung der Segmentierungs-Service. |
| [!UICONTROL Lebenszyklus-Status] | Der Status der Zielgruppe. Mögliche Werte für dieses Feld sind `Draft`, `Published` und `Archived`. |
| [!UICONTROL Aktualisierungshäufigkeit] | Ein Wert, der angibt, wie oft die Daten der Zielgruppe aktualisiert werden. Mögliche Werte für dieses Feld sind `On Demand`, `Scheduled` und `Continuous`. |
| [!UICONTROL Zuletzt aktualisiert von] | Der Name der Person, die die Zielgruppe zuletzt aktualisiert hat. |
| [!UICONTROL Erstellt] | Datum und Uhrzeit der Erstellung der Zielgruppe. |
| [!UICONTROL Zuletzt aktualisiert] | Datum und Uhrzeit der letzten Aktualisierung der Zielgruppe. |
| [!UICONTROL Zugriffsbeschriftungen] | Die Zugriffsbeschriftungen für die Zielgruppe. Mit Zugriffsbeschriftungen können Sie Datensätze und Felder entsprechend den für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Diese Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Weitere Informationen zu Zugriffsbeschriftungen finden Sie in der Dokumentation unter [Verwalten von Beschriftungen](../../access-control/abac/ui/labels.md). |

Sie können **[!UICONTROL Zielgruppe erstellen]** auswählen, um eine Zielgruppe zu erstellen.

![Die Schaltfläche „Zielgruppe erstellen“ ist hervorgehoben und zeigt an, wo Sie eine Zielgruppe erstellen können.](../images/ui/overview/create-audience.png)

Es wird ein Pop-up angezeigt, in dem Sie auswählen können, ob Sie eine Zielgruppe oder Regeln erstellen möchten.

![Ein Pop-up, das die beiden Arten von Zielgruppen anzeigt, die Sie erstellen können.](../images/ui/overview/create-audience-type.png)

Durch Auswählen von **[!UICONTROL Zielgruppen erstellen]** gelangen Sie zum Audience Builder. Weitere Informationen zum Erstellen von Zielgruppen finden Sie im [Audience Builder-Handbuch](./audience-builder.md).

Wenn Sie **[!UICONTROL Regel erstellen]** wählen, gelangen Sie zum Segment Builder. Weitere Informationen zum Erstellen von Segmenten finden Sie im [Segment Builder-Handbuch](./segment-builder.md)

## Zielgruppendetails {#audience-details}

Um weitere Details zu einer bestimmten Zielgruppe anzuzeigen, wählen Sie den Namen der Zielgruppe auf der Registerkarte [!UICONTROL Zielgruppen] aus.

Die Seite mit den Details zur Zielgruppe wird angezeigt. Diese Seite unterscheidet sich in einigen Details, je nachdem, ob die Zielgruppe mit Adobe Experience Platform oder aus einer externen Quelle wie der Zielgruppenorchestrierung generiert wurde.

### Platform-generierte Zielgruppe

Weitere Informationen über Platform-generierte Zielgruppen finden Sie im [Abschnitt zur Segmentzusammenfassung](#segment-summary).

### Extern generierte Zielgruppe

Oben auf der Seite mit den Zielgruppendetails finden Sie eine Zusammenfassung der Zielgruppe und Details zu dem Datensatz, in dem die Zielgruppe gespeichert ist.

![Die bereitgestellten Details für eine extern generierte Zielgruppe.](../images/ui/overview/externally-generated-audience.png)

Der Abschnitt **[!UICONTROL Zielgruppenzusammenfassung]** enthält Informationen wie die ID, den Namen, die Beschreibung und Details der Attribute.

Der Abschnitt **[!UICONTROL Datensatzdetails]** enthält Informationen wie den Namen, die Beschreibung, den Tabellennamen, die Quelle und das Schema. Sie können auf **[!UICONTROL Datensatz anzeigen]** klicken, um weitere Informationen zum Datensatz anzuzeigen.

| Feld | Beschreibung |
| ----- | ----------- |
| [!UICONTROL Name] | Der Name des Datensatzes. |
| [!UICONTROL Beschreibung] | Die Beschreibung des Datensatzes. |
| [!UICONTROL Tabellenname] | Der Tabellenname des Datensatzes. |
| [!UICONTROL Quelle] | Die Quelle des Datensatzes. Für extern generierte Zielgruppen wird dieser Wert **Schema**. |
| [!UICONTROL Schema] | Der Typ des XDM-Schemas, dem der Datensatz entspricht. |

Weitere Informationen zu Datensätzen finden Sie in der [Datensatz-Übersicht](../../catalog/datasets/overview.md).

## Streaming-Segmentierung  {#streaming-segmentation}

Streaming-Segmentierung bedeutet, dass Sie auf [!DNL Platform] nahezu in Echtzeit segmentieren und sich dabei auf den Datenreichtum konzentrieren können. Mit der Streaming-Segmentierung erfolgt die Segmentqualifizierung jetzt direkt beim Eintreffen der Daten in [!DNL Platform]. Damit entfällt die Notwendigkeit, Segmentierungsaufträge zu planen und auszuführen.

Weitere Informationen zur Streaming-Segmentierung finden Sie im [Benutzerhandbuch zur Streaming-Segmentierung](./streaming-segmentation.md).

>[!NOTE]
>
>Damit die Streaming-Segmentierung funktioniert, müssen Sie die geplante Segmentierung für die Organisation aktivieren. Einzelheiten zur Aktivierung der geplanten Segmentierung finden Sie [im Abschnitt zur Streaming-Segmentierung in diesem Benutzerhandbuch](#scheduled-segmentation).

## Edge-Segmentierung {#edge-segmentation}

Bei der Edge-Segmentierung werden Segmente in Platform sofort am Edge ausgewertet, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.

Weitere Informationen zur Edge-Segmentierung finden Sie in der [Handbuch zur Benutzeroberfläche der Edge-Segmentierung](./edge-segmentation.md)

## Richtlinienverstöße

>[!NOTE]
>
>Richtlinienverstöße können nur dann auftreten, wenn Sie ein Segment erstellen, das einem Ziel zugewiesen wurde.

Sobald Sie Ihr Segment erstellt haben, wird das Segment von der Data Governance in Adobe Experience Platform analysiert, um sicherzustellen, dass es keine Richtlinienverstöße innerhalb des Segments gibt. Weitere Informationen finden Sie in der [Übersicht zu Data Governance](../../data-governance/home.md).

![Die Richtlinienverletzungen für das Segment werden angezeigt.](../images/ui/overview/segment-dule-policy-violations.png)

## Nächste Schritte und zusätzliche Ressourcen {#next-steps}

Die [!DNL Segmentation Service]-Benutzeroberfläche bietet einen umfangreichen Workflow, der es Ihnen ermöglicht, vermarktbare Zielgruppen aus [!DNL Real-Time Customer Profile]-Daten zu isolieren.

Um mehr über den [!DNL Segmentation Service] zu erfahren, lesen Sie bitte die Dokumentation weiter. Um zu erfahren, wie Sie die [!DNL Segmentation Service]-API verwenden können, lesen Sie bitte das [[!DNL Segmentation Service] Entwicklerhandbuch](../api/overview.md).
