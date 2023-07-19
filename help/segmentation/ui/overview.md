---
solution: Experience Platform
title: Handbuch zur Benutzeroberfläche des Segmentierungs-Service
description: Erfahren Sie, wie Sie in der Adobe Experience Platform-Benutzeroberfläche Zielgruppen und Segmentdefinitionen erstellen und verwalten.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 04c0b19bf4ffbc0719a89f710570cc667ca5e482
workflow-type: tm+mt
source-wordcount: '3606'
ht-degree: 30%

---

# Handbuch zur Benutzeroberfläche des Segmentierungs-Service

[!DNL Adobe Experience Platform Segmentation Service] bietet eine Benutzeroberfläche zum Erstellen und Verwalten von Zielgruppen und Segmentdefinitionen.

## Erste Schritte

Die Arbeit mit Zielgruppen und Segmentdefinitionen erfordert ein Verständnis der verschiedenen [!DNL Experience Platform] Dienste, die mit der Segmentierung verbunden sind. Bevor Sie dieses Benutzerhandbuch lesen, lesen Sie bitte die Dokumentation für folgende Services:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] ermöglicht Ihnen das Segmentieren von Daten, die in gespeichert sind. [!DNL Experience Platform] die sich auf Einzelanwender (wie Kunden, Interessenten, Benutzer oder Organisationen) in kleinere Gruppen bezieht.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Ermöglicht die Erstellung von Kundenprofilen durch das Zusammenführen von Identitäten aus unterschiedlichen Datenquellen, die in [!DNL Platform] aufgenommen werden.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten durch [!DNL Platform] organisiert werden. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profile und Ereignisse gemäß den [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md) aufgenommen werden.

Sie sollten auch zwei Schlüsselbegriffe verstehen, die in diesem Dokument verwendet werden, und den Unterschied zwischen ihnen verstehen:

- **Zielgruppe**: Eine Gruppe von Personen, die ähnliche Verhaltensweisen und/oder Merkmale aufweisen. Diese Personensammlung kann entweder von Adobe Experience Platform mithilfe von Segmentdefinitionen oder der Zielgruppenzusammensetzung (plattformgenerierte Zielgruppe) oder aus externen Quellen wie benutzerdefinierten Uploads (extern generierte Zielgruppe) erstellt werden.
- **Segmentdefinition**: Die Regeln, die Adobe Experience Platform verwendet, um die wichtigsten Merkmale oder das Verhalten einer Zielgruppe zu beschreiben.
- **Segment**: Die Trennung von Profilen in Audiences.

## Übersicht

Wählen Sie in der Benutzeroberfläche &quot;Experience Platform&quot;die Option **[!UICONTROL Zielgruppen]** im linken Navigationsbereich, um die **[!UICONTROL Übersicht]** Registerkarte mit den [!UICONTROL Zielgruppen] Dashboard.

>[!NOTE]
>
>Wenn Ihr Unternehmen neu bei Platform ist und noch keine aktiven Profildatensätze oder Zusammenführungsrichtlinien erstellt wurden, wird die [!UICONTROL Zielgruppen] Das Dashboard ist nicht sichtbar. Stattdessen wird die [!UICONTROL Übersicht] enthält Links und Dokumentation, die Ihnen bei den ersten Schritten mit Zielgruppen helfen.

### [!UICONTROL Zielgruppen] Dashboard {#segments-dashboard}

Die **[!UICONTROL Zielgruppen]** Im Dashboard werden Schlüsselmetriken im Zusammenhang mit den Zielgruppendaten Ihres Unternehmens beschrieben.

Weitere Informationen finden Sie unter [Dashboard-Handbuch für Zielgruppen](../../dashboards/guides/audiences.md).

![Das Zielgruppen-Dashboard wird angezeigt. Es werden verschiedene Widgets angezeigt, darunter die Zielgruppengröße, Profile nach Identität, Identitätsüberschneidungen und der Trend zur Änderung der Zielgruppengröße.](../../dashboards/images/segments/dashboard-overview.png)

## Durchsuchen {#browse}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_churncolumnname"
>title="Abwanderung"
>abstract="Die Fluktuation stellt den Prozentsatz der Profile dar, die sich innerhalb einer Zielgruppendefinition ändern, verglichen mit der letzten Ausführung des Zielgruppenvorgangs."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_evaluationmethodcolumnname"
>title="Auswertungsmethode"
>abstract="Zu den Auswertungsmethoden für Zielgruppen gehören Batch, Streaming und Edge."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_addallsegmentstoschedule"
>title="Alle Zielgruppen zum Zeitplan hinzufügen"
>abstract="Aktivieren Sie diese Option, um alle Zielgruppen einzubeziehen, die mit der Batch-Segmentierung in der täglich geplanten Aktualisierung ausgewertet wurden. Deaktivieren Sie sie, um alle Zielgruppen aus der geplanten Aktualisierung zu entfernen."

Wählen Sie die **[!UICONTROL Durchsuchen]** um eine Liste aller Zielgruppen für Ihre Organisation anzuzeigen.

![Der Suchbildschirm wird angezeigt. Eine Liste aller Zielgruppen der Organisation wird angezeigt.](../images/ui/overview/audience-browse.png)

Diese Ansicht listet Informationen zu den Zielgruppen auf, einschließlich Profilanzahl, Ursprung, Erstellungsdatum, Datum der letzten Änderung, Tags und Aufschlüsselung.

Sie können dieser Anzeige zusätzliche Felder hinzufügen, indem Sie das ![Filterattribut-Symbol](../images/ui/overview/filter-attribute.png) auswählen. Diese zusätzlichen Felder umfassen Lebenszyklusstatus, Aktualisierungshäufigkeit, Letzte Aktualisierung durch, Beschreibung, erstellt von und Zugriffsbeschriftungen.

| Feld | Beschreibung |
| ----- | ----------- |
| [!UICONTROL Name] | Der Name der Zielgruppe. |
| [!UICONTROL Anzahl der Profile] | Die Gesamtzahl der Profile, die für die Zielgruppe qualifiziert sind. |
| [!UICONTROL Herkunft] | Die Herkunft der Zielgruppe. Hier wird angegeben, woher die Zielgruppe stammt. Mögliche Werte sind Segmentierungsdienst, benutzerdefinierter Upload, Zielgruppenzusammensetzung und Audience Manager. |
| [!UICONTROL Erstellt] | Datum und Uhrzeit der Erstellung der Audience in UTC. |
| [!UICONTROL Zuletzt aktualisiert] | Datum und Uhrzeit der letzten Aktualisierung der Audience in UTC. |
| [!UICONTROL Tags] | Die benutzerdefinierten Tags, die zur Zielgruppe gehören. Weitere Informationen zu diesen Tags finden Sie im [Abschnitt zu Tags](#tags). |
| [!UICONTROL Aufschlüsselung] | Die Aufschlüsselung des Profilstatus für die Zielgruppe. Eine detailliertere Beschreibung dieser Aufschlüsselung des Profilstatus finden Sie unten. |
| [!UICONTROL Lebenszyklus-Status] | Der Status der Zielgruppe. Mögliche Werte für dieses Feld sind `Draft`, `Published` und `Archived`. |
| [!UICONTROL Aktualisierungshäufigkeit] | Ein Wert, der angibt, wie oft die Daten der Zielgruppe aktualisiert werden. Mögliche Werte für dieses Feld sind `On Demand`, `Scheduled` und `Continuous`. |
| [!UICONTROL Zuletzt aktualisiert von] | Der Name der Person, die die Zielgruppe zuletzt aktualisiert hat. |
| [!UICONTROL Beschreibung] | Die Beschreibung der Zielgruppe. |
| [!UICONTROL Erstellt von] | Der Name der Person, die die Zielgruppe erstellt hat. |
| [!UICONTROL Zugriffsbeschriftungen] | Die Zugriffsbeschriftungen für die Zielgruppe. Mit Zugriffsbeschriftungen können Sie Datensätze und Felder entsprechend den für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Diese Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Weitere Informationen zu Zugriffsbeschriftungen finden Sie in der Dokumentation unter [Verwalten von Beschriftungen](../../access-control/abac/ui/labels.md). |

Wenn die Aufschlüsselung ausgewählt ist, wird ein Balkendiagramm angezeigt, das den prozentualen Anteil der Profile in jedem der folgenden berechneten Profilstatus anzeigt: [!UICONTROL Realisiert], [!UICONTROL Bestehend] und [!UICONTROL Verlassen]. Außerdem wird die Aufschlüsselung auf der Seite [!UICONTROL Durchsuchen] -Tab ist die genaueste Aufschlüsselung des Segmentdefinitionsstatus. Wenn diese Zahl von den Angaben auf der Registerkarte [!UICONTROL Übersicht] abweicht, sollten Sie als korrekte Informationsquelle die Zahlen auf der Registerkarte [!UICONTROL Durchsuchen] verwenden, da die Zahlen auf der Registerkarte [!UICONTROL Übersicht] nur einmal pro Tag aktualisiert werden.

| Status | Beschreibung |
| ------ | ----------- |
| [!UICONTROL Realisiert] | Die Anzahl der Profile, die **qualifiziert** für das Segment in den letzten 24 Stunden seit der Ausführung des letzten Batch-Segmentauftrags. |
| [!UICONTROL Bestehend] | Die Anzahl der Profile, die **verbleiben** in dem Segment in den letzten 24 Stunden seit der Ausführung des letzten Batch-Segmentauftrags. |
| [!UICONTROL Verlassen] | Die Anzahl der Profile, die **beendet** das Segment in den letzten 24 Stunden seit Ausführung des letzten Batch-Segmentauftrags. |

Neben jeder Zielgruppe befindet sich ein Auslassungssymbol. Wenn Sie diese Option auswählen, wird eine Liste der verfügbaren Schnellaktionen für die Zielgruppe angezeigt. Diese Aktionsliste unterscheidet sich je nach Ursprung der Zielgruppe.

![Die Liste der Schnellaktionen wird für Zielgruppen mit dem Ursprung von [!UICONTROL Zielgruppenzusammensetzung].](../images/ui/overview/browse-audience-composition-details.png)

| Aktion | Ursprung | Beschreibung |
| ------ | ------- | ----------- |
| Bearbeiten | Segmentierungs-Service | Ermöglicht Ihnen das Öffnen von Segment Builder zum Bearbeiten Ihrer Zielgruppe. Weitere Informationen zur Verwendung von Segment Builder finden Sie im Abschnitt [Handbuch zur Benutzeroberfläche von Segment Builder](./segment-builder.md). |
| Offene Komposition | Zielgruppenzusammensetzung | Ermöglicht Ihnen das Öffnen der Audience-Komposition , um Ihre Zielgruppe anzuzeigen. Weitere Informationen zur Komposition von Zielgruppen finden Sie im [Handbuch zur Benutzeroberfläche der Zielgruppenzusammensetzung](./audience-composition.md). |
| Auf Ziel aktivieren | Segmentierungs-Service | Ermöglicht die Aktivierung der Zielgruppe für ein Ziel. Detaillierte Informationen zum Aktivieren einer Zielgruppe für ein Ziel finden Sie im Abschnitt [Aktivierungsübersicht](../../destinations/ui/activation-overview.md). |
| Mit Partnern teilen | Zielgruppenzusammensetzung, benutzerdefinierter Upload, Segmentierungsdienst | Ermöglicht die Freigabe Ihrer Zielgruppe für andere Platform-Benutzer. Weitere Informationen zu dieser Funktion finden Sie im Abschnitt [Übersicht über Segmentübereinstimmungen](./segment-match/overview.md). |
| Verwalten von Tags | Zielgruppenzusammensetzung, benutzerdefinierter Upload, Segmentierungsdienst | Ermöglicht die Verwaltung der benutzerdefinierten Tags, die zur Zielgruppe gehören. Weitere Informationen zu dieser Funktion finden Sie im Abschnitt unter [Filtern und Tagging](#manage-audiences). |
| In Ordner verschieben | Zielgruppenzusammensetzung, benutzerdefinierter Upload, Segmentierungsdienst | Hiermit können Sie verwalten, zu welchem Ordner die Zielgruppe gehört. Weitere Informationen zu dieser Funktion finden Sie im Abschnitt unter [Filtern und Tagging](#manage-audiences). |
| Kopieren | Zielgruppenzusammensetzung, benutzerdefinierter Upload, Segmentierungsdienst | Dupliziert die ausgewählte Zielgruppe. |
| Zugriffsbeschriftungen anwenden | Zielgruppenzusammensetzung, benutzerdefinierter Upload, Segmentierungsdienst | Ermöglicht die Verwaltung der Zugriffsbeschriftungen, die zur Zielgruppe gehören. Weitere Informationen zu Zugriffsbeschriftungen finden Sie in der Dokumentation unter [Verwalten von Beschriftungen](../../access-control/abac/ui/labels.md). |
| Archivieren | Benutzerdefinierter Upload | Archiviert die ausgewählte Zielgruppe. |
| Löschen | Zielgruppenzusammensetzung, benutzerdefinierter Upload, Segmentierungsdienst | Löscht die ausgewählte Zielgruppe. |

Oben auf der Seite finden Sie Optionen zum Hinzufügen aller Zielgruppen zu einem Zeitplan, zum Importieren einer Zielgruppe und zum Erstellen einer neuen Zielgruppe.

Umschalten **[!UICONTROL Alle Zielgruppen planen]** aktiviert die geplante Segmentierung. Weitere Informationen zur geplanten Segmentierung finden Sie im [Abschnitt „Geplante Segmentierung“ in diesem Benutzerhandbuch](#scheduled-segmentation).

Auswählen **[!UICONTROL Audience importieren]** können Sie eine extern generierte Zielgruppe importieren. Weiterführende Informationen zum Zielgruppenimport finden Sie im Abschnitt [Importieren einer Zielgruppe im Benutzerhandbuch](#import-audience).

Auswählen **[!UICONTROL Zielgruppe erstellen]** ermöglicht Ihnen die Erstellung einer Audience. Weiterführende Informationen zur Erstellung von Zielgruppen finden Sie im Abschnitt [Erstellen einer Zielgruppe im Benutzerhandbuch](#create-audience).

![Die obere Navigationsleiste auf der Seite zum Durchsuchen von Zielgruppen wird hervorgehoben. Diese Leiste enthält eine Schaltfläche zum Erstellen einer Audience und eine Schaltfläche zum Importieren einer Audience.](../images/ui/overview/browse-audiences-top.png)

>[!NOTE]
>
> Sie werden **not** in der Lage sein, eine Zielgruppe zu löschen, die in einer Zielaktivierung verwendet wird.

### Filtern und Taggen {#manage-audiences}

Um Ihre Arbeitseffizienz zu verbessern, können Sie nach vorhandenen Zielgruppen suchen, benutzerdefinierte Tags zu Zielgruppen hinzufügen, Zielgruppen in Ordner setzen und die angezeigten Zielgruppen filtern.

**Durchsuchen** {#search}

Sie können Ihre vorhandenen Zielgruppen in bis zu 9 verschiedenen Sprachen durchsuchen mit [!DNL Unified Search].

Verwendung [!DNL Unified Search], fügen Sie den zu suchenden Begriff in der hervorgehobenen Suchleiste hinzu.

![Die Suchleiste wird hervorgehoben.](../images/ui/overview/browse-audience-search.png)

Weitere Informationen finden Sie unter [!DNL Unified Search], einschließlich der unterstützten Funktionen, lesen Sie bitte den Abschnitt [Dokumentation zur einheitlichen Suche](https://experienceleague.adobe.com/docs/core-services/interface/services/search-experience-cloud.html).

**Tags** {#tags}

Sie können benutzerdefinierte Tags hinzufügen, um Ihre Zielgruppen besser zu beschreiben, zu finden und zu verwalten.

Um ein Tag hinzuzufügen, wählen Sie **[!UICONTROL Tags verwalten]** auf der Zielgruppe, die Sie taggen möchten.

![Die [!UICONTROL Tags verwalten] für eine bestimmte Zielgruppe ausgewählt ist.](../images/ui/overview/browse-manage-tags.png)

Die **[!UICONTROL Tags verwalten]** Popup angezeigt. In diesem Popup können Sie entweder ein kategorisiertes Tag oder ein nicht kategorisiertes Tag auswählen.

| Tag-Typ | Beschreibung |
| -------- | ----------- |
| kategorisiert | Ein Tag, das von den Administratoren Ihres Unternehmens erstellt und verwaltet wird. |
| Nicht kategorisiert | Ein Tag, das innerhalb der [!UICONTROL Tags verwalten] Popover. Jeder kann diese Arten von Tags erstellen oder verwalten. |

![Die [!UICONTROL Tags verwalten] Popover angezeigt. Die Optionen zur Auswahl einer kategorisierten oder nicht kategorisierten Auswahl werden hervorgehoben.](../images/ui/overview/create-tag.png)

Nachdem Sie alle Tags hinzugefügt haben, die Sie an die Audience anhängen möchten, wählen Sie **[!UICONTROL Speichern]**.

![Im [!UICONTROL Tags verwalten] Popover angezeigt werden, werden die hinzugefügten Tags hervorgehoben.](../images/ui/overview/created-tags.png)

Weitere Informationen zum Erstellen und Verwalten von Tags finden Sie im Abschnitt [Verwalten von Tags-Handbuch](../../administrative-tags/ui/managing-tags.md).

**Ordner** {#folders}

Für ein besseres Zielgruppen-Management können Sie Zielgruppen in Ordnern platzieren.

Um eine Zielgruppe in einen Ordner zu verschieben, wählen Sie **[!UICONTROL In Ordner verschieben]** auf der Zielgruppe, die Sie verschieben möchten.

![Die [!UICONTROL In Ordner verschieben] für eine bestimmte Zielgruppe ausgewählt ist.](../images/ui/overview/browse-move-to-folder.png)

Die **Zielgruppe in Ordner verschieben** Popup angezeigt. Wählen Sie den Ordner aus, in den Sie die Zielgruppe verschieben möchten, und wählen Sie dann **[!UICONTROL Speichern]**.

![Das Popover Zielgruppe in Ordner verschieben wird angezeigt. Der Ordner, in den die Zielgruppe verschoben wird, wird hervorgehoben.](../images/ui/overview/move-to-folder.png)

Sobald sich die Zielgruppe in einem Ordner befindet, können Sie festlegen, dass nur Zielgruppen angezeigt werden, die zu einem bestimmten Ordner gehören.

![Zielgruppen, die zu einem bestimmten Ordner gehören, werden angezeigt.](../images/ui/overview/browse-folders.png)

**Filter** {#filter}

Sie können Ihre Zielgruppen auch nach verschiedenen Einstellungen filtern.

Um die verfügbaren Zielgruppen zu filtern, wählen Sie die ![Filtersymbol](../images/ui/overview/filter-icon.png).

![Die Seite Zielgruppen durchsuchen wird angezeigt, wobei das Filtersymbol hervorgehoben ist.](../images/ui/overview/browse-select-filter.png)

Die Liste der verfügbaren Filter wird angezeigt.

| Filter | Beschreibung |
| ------ | ----------- |
| [!UICONTROL Herkunft] | Ermöglicht die Filterung nach der Herkunft der Audience. Zu den verfügbaren Optionen gehören Segmentierungsdienst, benutzerdefinierter Upload, Zielgruppenzusammensetzung und Audience Manager. |
| [!UICONTROL Hat ein Tag] | Filtert nach Tags. Sie können zwischen **[!UICONTROL Hat ein Tag]** und **[!UICONTROL Enthält alle Tags]**. Wann **[!UICONTROL Hat ein Tag]** ausgewählt ist, enthalten die gefilterten Zielgruppen **any** der Tags, die Sie hinzugefügt haben. Wann **[!UICONTROL Enthält alle Tags]** ausgewählt ist, müssen die gefilterten Zielgruppen **all** der Tags, die Sie hinzugefügt haben. |
| [!UICONTROL Lebenszyklus-Status] | Ermöglicht die Filterung nach dem Lebenszyklusstatus der Zielgruppe. Verfügbare Optionen umfassen [!UICONTROL Aktiv], [!UICONTROL Archiviert], [!UICONTROL Gelöscht], [!UICONTROL Entwurf], [!UICONTROL Inaktiv]und [!UICONTROL Veröffentlicht]. |
| [!UICONTROL Aktualisierungshäufigkeit] | Ermöglicht die Filterung nach der Aktualisierungshäufigkeit der Audience. Verfügbare Optionen umfassen [!UICONTROL Geplant], [!UICONTROL Kontinuierlich]und [!UICONTROL On Demand]. |
| [!UICONTROL Erstellt von] | Ermöglicht die Filterung nach der Person, die die Zielgruppe erstellt hat. |
| [!UICONTROL Erstellungsdatum] | Ermöglicht die Filterung nach dem Erstellungsdatum der Audience. Sie können einen Datumsbereich auswählen, nach dem der Zeitpunkt der Erstellung der Audience gefiltert werden soll. |
| [!UICONTROL Änderungsdatum] | Filtert die Daten nach dem Datum der letzten Änderung der Audience. Sie können einen Datumsbereich auswählen, nach dem gefiltert werden soll, wann die Zielgruppe zuletzt geändert wurde. |

![Die verfügbaren Filter werden auf der Seite Zielgruppen durchsuchen angezeigt und hervorgehoben.](../images/ui/overview/filter-audiences.png)

### Zielgruppendetails {#audience-details}

Um weitere Details zu einer bestimmten Zielgruppe anzuzeigen, wählen Sie den Namen einer Zielgruppe im **[!UICONTROL Durchsuchen]** Registerkarte.

Die Seite mit den Details zur Zielgruppe wird angezeigt. Oben finden Sie eine Zusammenfassung der Zielgruppe, Informationen zur qualifizierten Zielgruppengröße sowie Ziele, für die das Segment aktiviert wird.

![Die Seite mit den Zielgruppendetails wird angezeigt. Die Karten für Zielgruppenzusammenfassung, Gesamtanzahl der Zielgruppen und aktivierte Ziele werden hervorgehoben.](../images/ui/overview/audience-details-summary.png)

**Zielgruppenzusammenfassung** {#segment-summary}

Die **[!UICONTROL Zielgruppenzusammenfassung]** enthält Informationen wie die ID, den Namen, die Beschreibung, den Ursprung und die Details der Attribute.

Darüber hinaus haben Sie die Möglichkeit, die Zielgruppe für ein Ziel zu aktivieren, Zugriffsbeschriftungen anzuwenden oder die Zielgruppe zu bearbeiten/zu aktualisieren.

Auswählen **[!UICONTROL Auf Ziel aktivieren]** ermöglicht die Aktivierung der Audience für ein Ziel. Detaillierte Informationen zum Aktivieren einer Zielgruppe für ein Ziel finden Sie im Abschnitt [Aktivierungsübersicht](../../destinations/ui/activation-overview.md).

![Der Button „Für Ziel aktivieren“ ist hervorgehoben.](../images/ui/overview/audience-details-activate.png)

Auswählen **[!UICONTROL Zugriffsbeschriftungen anwenden]** ermöglicht die Verwaltung der Zugriffsbeschriftungen, die zur Zielgruppe gehören. Weitere Informationen zu Zugriffsbeschriftungen finden Sie in der Dokumentation unter [Verwalten von Beschriftungen](../../access-control/abac/ui/labels.md).

![Die Schaltfläche Zugriffsbeschriftungen anwenden ist hervorgehoben.](../images/ui/overview/audience-details-access-labels.png)

>[!BEGINTABS]

>[!TAB Zielgruppenzusammensetzung]

![Die Seite mit den Zielgruppendetails wird mit dem [!UICONTROL Offene Komposition] hervorgehoben.](../images/ui/overview/audience-details-open-composition.png)

Auswählen **[!UICONTROL Offene Komposition]** ermöglicht Ihnen, Ihre Zielgruppe in Zielgruppenkomposition anzuzeigen. Weitere Informationen zur Zielgruppenkomposition finden Sie im [Handbuch zur Benutzeroberfläche für Zielgruppenkomposition](./audience-composition.md).

>[!TAB Benutzerdefinierter Upload]

![Die Seite mit den Zielgruppendetails wird mit dem [!UICONTROL Audience aktualisieren] hervorgehoben.](../images/ui/overview/audience-details-update-audience.png)

Auswählen **[!UICONTROL Audience aktualisieren]** ermöglicht das erneute Hochladen einer extern generierten Zielgruppe. Weiterführende Informationen zum Import einer extern generierten Zielgruppe finden Sie im Abschnitt unter [Audience importieren](#import-audience).

>[!TAB Segmentierungsdienst]

![Die Seite mit den Zielgruppendetails wird mit dem [!UICONTROL Audience bearbeiten] hervorgehoben.](../images/ui/overview/audience-details-edit-audience.png)

Auswählen **[!UICONTROL Audience bearbeiten]** ermöglicht die Bearbeitung Ihrer Audience im Segment Builder. Detaillierte Informationen zur Verwendung des Arbeitsbereichs von [!DNL Segment Builder] finden Sie im [[!DNL Segment Builder] Benutzerhandbuch](./segment-builder.md).

>[!ENDTABS]

Auswählen **[!UICONTROL Eigenschaften bearbeiten]** können Sie die grundlegenden Details der Zielgruppe bearbeiten, z. B. den Namen, die Beschreibung und die Tags.

![](../images/ui/overview/audience-details-edit-properties.png)

**Zielgruppe insgesamt** {#audience-total}

Die **[!UICONTROL Zielgruppe insgesamt]** zeigt die Gesamtzahl der Profile an, die für die Zielgruppe geeignet sind.

Die Schätzungen werden anhand einer Stichprobengröße aus den Daten des jeweiligen Tages generiert. Wenn sich in Ihrem Profilspeicher weniger als 1 Million Entitäten befinden, wird der vollständige Datensatz verwendet. Bei zwischen 1 und 20 Millionen Entitäten werden 1 Million Entitäten verwendet; bei mehr als 20 Millionen Entitäten werden 5 % der Gesamtentitäten genutzt. Weitere Informationen zum Generieren von Schätzungen finden Sie im [Schätzung des Generierungsabschnitts](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) des Tutorials zur Zielgruppenerstellung.

**Aktivierte Ziele** {#activated-destinations}

Die **[!UICONTROL Aktivierte Ziele]** zeigt die Ziele an, für die diese Zielgruppe aktiviert ist.

>[!NOTE]
>
> Ziele sind eine Funktion, die mit [!DNL Adobe Real-Time Customer Data Platform] verfügbar ist und es Ihnen ermöglicht, Daten auf externe Plattformen zu exportieren. Weitere Informationen zu Zielen finden Sie unter [Ziele – Übersicht](../../destinations/home.md). Informationen zum Aktivieren eines Segments für ein Ziel finden Sie unter [Aktivierung – Übersicht](../../destinations/ui/activation-overview.md).

**Beispielprofile** {#profile-samples}

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

![Die Beispielprofile für die Audience werden hervorgehoben. Zu den Beispielprofilinformationen gehören die Profil-ID, der Vorname, der Nachname und die E-Mail-Adresse der Person.](../images/ui/overview/audience-details-profiles.png)

### Audience erstellen {#create-audience}

Sie können **[!UICONTROL Zielgruppe erstellen]** , um eine Audience zu erstellen.

![Auf der Seite Zielgruppendurchsuchen wird die Schaltfläche Zielgruppe erstellen hervorgehoben.](../images/ui/overview/browse-create-audience.png)

Es wird ein Pop-up angezeigt, in dem Sie auswählen können, ob Sie eine Zielgruppe oder Regeln erstellen möchten.

![Ein Pop-up, das die beiden Arten von Zielgruppen anzeigt, die Sie erstellen können.](../images/ui/overview/create-audience-type.png)

**Zielgruppenkomposition** {#audience-composition}

Auswählen **[!UICONTROL Erstellen von Zielgruppen]** Sie gelangen zur Zielgruppenkomposition. Dieser Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Zielgruppen, z. B. Drag &amp; Drop-Kacheln, die zur Darstellung verschiedener Aktionen verwendet werden. Weitere Informationen zum Erstellen von Zielgruppen finden Sie in der [Handbuch zur Zielgruppenkomposition](./audience-composition.md).

![Der Arbeitsbereich Zielgruppenkomposition wird angezeigt.](../images/ui/overview/audience-composition.png)

**Segment Builder** {#segment-builder}

Auswählen **[!UICONTROL Regel erstellen]** führt Sie zum Segment Builder. Dieser Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Segmentdefinitionen, z. B. Drag &amp; Drop-Kacheln, die zur Darstellung von Dateneigenschaften verwendet werden. Weitere Informationen zum Erstellen von Segmentdefinitionen finden Sie im Abschnitt [Segment Builder-Handbuch](./segment-builder.md)

![Der Segment Builder-Arbeitsbereich wird angezeigt.](../images/ui/overview/segment-builder.png)

### Audience importieren {#import-audience}

Sie können **[!UICONTROL Audience importieren]** um eine extern generierte Zielgruppe zu importieren.

![Auf der Seite Zielgruppendurchsuchen wird die Schaltfläche Zielgruppe importieren hervorgehoben.](../images/ui/overview/browse-import-audience.png)

Die **[!UICONTROL Audience-CSV importieren]** Workflow angezeigt. Sie können eine CSV-Datei auswählen, die als extern generierte Zielgruppe importiert werden soll.

![Im [!UICONTROL Audience-CSV importieren] Workflow, der [!UICONTROL Dateien per Drag &amp; Drop verschieben] hervorgehoben wird, wo Sie Ihre extern generierte Zielgruppe hochladen können.](../images/ui/overview/import-audience-csv.png)

>[!NOTE]
>
>Die von außen generierte Zielgruppe **must** im CSV-Format vorliegen, haben eine **maximum** 11 Spalten und kleiner als 1 GB sein.

Nach Auswahl der zu importierenden CSV-Datei wird eine Liste mit Beispieldaten für diese extern generierte Zielgruppe angezeigt. Nachdem Sie die Richtigkeit der Beispieldaten bestätigt haben, wählen Sie **[!UICONTROL Nächste]**.

![Beispieldaten für die extern generierte Zielgruppe werden angezeigt.](../images/ui/overview/import-audience-sample-data.png)

Die **[!UICONTROL Zielgruppendetails]** angezeigt. Sie können Informationen über Ihre Zielgruppe hinzufügen, einschließlich Name, Beschreibung, primäre Identität und Identitäts-Namespace-Wert.

![Die [!UICONTROL Zielgruppendetails] angezeigt.](../images/ui/overview/import-audience-audience-details.png)

Nachdem Sie die Zielgruppendetails ausgefüllt haben, wählen Sie **[!UICONTROL Nächste]**.

![Die [!UICONTROL Nächste] -Schaltfläche wird auf der [!UICONTROL Zielgruppendetails] Seite.](../images/ui/overview/import-audience-filled-details.png)

Die **[!UICONTROL Überprüfen]** angezeigt. Sie können die Details Ihrer neu importierten, extern generierten Zielgruppe überprüfen.

![Die [!UICONTROL Überprüfen] wird angezeigt, auf der Details Ihrer neu importierten, extern generierten Zielgruppe angezeigt werden.](../images/ui/overview/import-audience-review-details.png)

Nachdem Sie bestätigt haben, dass die Details korrekt sind, wählen Sie **[!UICONTROL Beenden]** , um Ihre extern generierte Zielgruppe in Adobe Experience Platform zu importieren.

## Geplante Segmentierung {#scheduled-segmentation}

Nach der Erstellung von Zielgruppen können Sie diese dann durch On-Demand- oder geplante (kontinuierliche) Auswertung bewerten. Auswertung bedeutet Verschieben [!DNL Real-Time Customer Profile] Daten über Segmentaufträge, um entsprechende Zielgruppen zu erstellen. Nach der Erstellung werden die Zielgruppen gespeichert und aufbewahrt, sodass sie über die APIs von [!DNL Experience Platform] exportiert werden können.

Die On-Demand-Auswertung beinhaltet die Verwendung der API zur Durchführung von Auswertungen und zur Erstellung von Zielgruppen nach Bedarf, während die geplante Auswertung (auch als &quot;geplante Segmentierung&quot;bezeichnet) es Ihnen ermöglicht, einen wiederkehrenden Zeitplan zur Auswertung von Zielgruppen zu einem bestimmten Zeitpunkt (maximal einmal täglich) zu erstellen.

### Aktivieren der geplanten Segmentierung {#enable-scheduled-segmentation}

Die Aktivierung Ihrer Zielgruppen für eine geplante Auswertung kann über die Benutzeroberfläche oder die API erfolgen. Kehren Sie in der Benutzeroberfläche zum **[!UICONTROL Durchsuchen]** Registerkarte innerhalb **[!UICONTROL Zielgruppen]** und aktivieren **[!UICONTROL Alle Zielgruppen planen]**. Dadurch werden alle Zielgruppen basierend auf dem von Ihrer Organisation festgelegten Zeitplan bewertet.

>[!NOTE]
>
>Die geplante Auswertung kann für Sandboxes mit maximal fünf (5) Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] aktiviert werden. Wenn Ihre Organisation in einer Sandbox-Umgebung über mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] verfügt, können Sie keine geplante Auswertung verwenden.

Zeitpläne können derzeit nur mit der API erstellt werden. Ausführliche Anweisungen zum Erstellen, Bearbeiten und Verwenden von Zeitplänen mithilfe der API finden Sie im Tutorial zum Auswerten und Aufrufen von Segmentierungsergebnissen, insbesondere im Abschnitt zu [Geplante Auswertung mit der API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![Der Umschalter zum Planen aller Zielgruppen wird auf der Seite Durchsuchen von Zielgruppen hervorgehoben.](../images/ui/overview/browse-audiences-scheduled.png)

## Kompositionen {#compositions}

Wählen Sie die **[!UICONTROL Kompositionen]** um eine Liste aller Zielgruppen anzuzeigen, die durch die Zielgruppenkomposition für Ihre Organisation generiert wurden.

![Eine Liste der Zielgruppen, die in Zielgruppenkomposition für Ihre Organisation erstellt wurden.](../images/ui/overview/compositions.png)

Standardmäßig enthält diese Ansicht Informationen zu den Zielgruppen, einschließlich Name, Status, Erstellungsdatum, Erstellungsdatum, Datum der letzten Aktualisierung und Datum der letzten Aktualisierung.

Sie können das Symbol ![Tabelle anpassen](../images/ui/overview/customize-table.png) auswählen, um zu ändern, welche Felder angezeigt werden.

![Die Schaltfläche „Tabelle anpassen“ ist hervorgehoben. Durch Auswahl dieser Schaltfläche können Sie die auf der Seite Zielgruppen-Kompositionen angezeigten Felder anpassen.](../images/ui/overview/compositions-select-customize-table.png)

Es wird ein Pop-up mit allen Feldern angezeigt, die in der Tabelle angezeigt werden können.

![Die Attribute, die für den Abschnitt Komposition angezeigt werden können.](../images/ui/overview/compositions-customize-table.png)

| Feld | Beschreibung |
| ----- | ----------- | 
| [!UICONTROL Name] | Der Name der Zielgruppe. |
| [!UICONTROL Status] | Der Status der Zielgruppe. Mögliche Werte für dieses Feld sind `Draft`, `Published` und `Archived`. |
| [!UICONTROL Erstellt] | Datum und Uhrzeit der Erstellung der Zielgruppe. |
| [!UICONTROL Erstellt von] | Der Name der Person, die die Zielgruppe erstellt hat. |
| [!UICONTROL Aktualisierung von  ] | Datum und Uhrzeit der letzten Aktualisierung der Audience. |
| [!UICONTROL Aktualisiert von] | Der Name der Person, die die Zielgruppe zuletzt aktualisiert hat. |

Um zu sehen, wie die Zielgruppe erstellt wurde, wählen Sie den Namen einer Zielgruppe im [!UICONTROL Zielgruppen] Registerkarte.

Die Seite Zielgruppenkomposition wird mit den Bausteinen angezeigt, aus denen sich Ihre Zielgruppe zusammensetzt. Weitere Informationen zur Verwendung der Zielgruppenkomposition finden Sie unter [Handbuch zur Benutzeroberfläche für Zielgruppenkomposition](./audience-composition.md).

## Streaming-Segmentierung  {#streaming-segmentation}

Streaming-Segmentierung bedeutet, dass Sie auf [!DNL Platform] nahezu in Echtzeit segmentieren und sich dabei auf den Datenreichtum konzentrieren können. Mit Streaming-Segmentierung wird die Segmentierung jetzt qualifiziert, wenn Daten in [!DNL Platform], wodurch Segmentierungsaufträge einfacher geplant und ausgeführt werden müssen.

Weitere Informationen zur Streaming-Segmentierung finden Sie im [Benutzerhandbuch zur Streaming-Segmentierung](./streaming-segmentation.md).

>[!NOTE]
>
>Damit die Streaming-Segmentierung funktioniert, müssen Sie die geplante Segmentierung für die Organisation aktivieren. Einzelheiten zur Aktivierung der geplanten Segmentierung finden Sie [im Abschnitt zur Streaming-Segmentierung in diesem Benutzerhandbuch](#scheduled-segmentation).

## Edge-Segmentierung {#edge-segmentation}

Bei der Edge-Segmentierung können Zielgruppen in Platform sofort am Rand ausgewertet werden, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.

Weitere Informationen zur Edge-Segmentierung finden Sie in der [Handbuch zur Benutzeroberfläche der Edge-Segmentierung](./edge-segmentation.md)

## Richtlinienverstöße

>[!NOTE]
>
>Richtlinienverletzungen gelten nur, wenn Sie eine Zielgruppe erstellen, die einem Ziel zugewiesen wurde.

Nachdem Sie die Erstellung Ihrer Zielgruppe abgeschlossen haben, wird die Zielgruppe von Adobe Experience Platform Data Governance analysiert, um sicherzustellen, dass keine Richtlinienverletzungen innerhalb der Zielgruppe auftreten. Weitere Informationen finden Sie in der [Übersicht zu Data Governance](../../data-governance/home.md).

![Die Richtlinienverletzungen für die Zielgruppe werden angezeigt.](../images/ui/overview/audience-dule-policy-violations.png)

## Nächste Schritte und zusätzliche Ressourcen {#next-steps}

Die [!DNL Segmentation Service] Die Benutzeroberfläche bietet einen umfassenden Workflow, mit dem Sie vermarktbare Zielgruppen aus [!DNL Real-Time Customer Profile] Daten.

Um mehr über den [!DNL Segmentation Service] zu erfahren, lesen Sie bitte die Dokumentation weiter. Um zu erfahren, wie Sie die [!DNL Segmentation Service]-API verwenden können, lesen Sie bitte das [[!DNL Segmentation Service] Entwicklerhandbuch](../api/overview.md).
