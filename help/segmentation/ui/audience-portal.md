---
title: Zielgruppen-Portal - Übersicht
description: Erfahren Sie, wie Sie mit Audience Portal Zielgruppen in Adobe Experience Platform anzeigen, verwalten und erstellen können.
exl-id: 505ac22e-05f3-423a-a9a0-7f3470af8945
source-git-commit: f02c76c646bb9966b345940e30e37ac52e636cfa
workflow-type: tm+mt
source-wordcount: '4421'
ht-degree: 54%

---

# Zielgruppen-Portal - Übersicht

Audience Portal ist ein zentraler Knotenpunkt in Adobe Experience Platform, über den Sie Zielgruppen anzeigen, verwalten und erstellen können.

In Audience Portal können Sie die folgenden Aufgaben ausführen:

>[!BEGINSHADEBOX]

- [Anzeigen einer Liste Ihrer Zielgruppen](#list)
   - [Verwenden von Schnellaktionen für Audiences](#quick-actions)
   - [Anpassen der in der Liste der Zielgruppen angezeigten Eigenschaften](#customize)
   - [Verwenden von Filtern, Ordnern und Tags zum Organisieren von Audiences](#manage-audiences)
- [Details zu Ihrer Audience anzeigen](#audience-details)
   - [Eine Zusammenfassung Ihrer Audience anzeigen](#audience-summary)
- [Zielgruppen für geplante Segmentierung aktivieren](#scheduled-segmentation)
- [Erstellen einer Zielgruppe](#create-audience)
   - [Verwenden von Segment Builder zum Erstellen einer Zielgruppe](#segment-builder)
   - [Verwenden der Audience-Komposition zum Erstellen einer Audience](#audience-composition)
   - [Verwenden Sie die Federated Audience-Komposition, um eine Audience mit Daten aus Ihrem vorhandenen Data Warehouse zu erstellen](#fac)
   - [Verwenden von Data Distiller zum Erstellen einer Zielgruppe](#data-distiller)
- [Extern generierte Zielgruppen importieren](#import-audience)

>[!ENDSHADEBOX]

Um das Audience Portal zu öffnen, wählen Sie **[!UICONTROL Abschnitt Segmentierung]** Registerkarte Durchsuchen aus.

## Zielgruppenliste {#list}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_churncolumnname"
>title="Abwanderung"
>abstract="Die Fluktuation stellt den Prozentsatz der Profile dar, die sich innerhalb einer Zielgruppendefinition ändern, verglichen mit der letzten Ausführung des Zielgruppenvorgangs."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_evaluationmethodcolumnname"
>title="Auswertungsmethode"
>abstract="Zu den Auswertungsmethoden für Zielgruppen gehören Batch, Streaming und Edge."

Standardmäßig zeigt Zielgruppenportal eine Liste aller Zielgruppen in Ihrer Organisation und Sandbox an, einschließlich Profilanzahl, Herkunft, Erstellungsdatum, Datum der letzten Änderung, Tags und Aufschlüsselung.

![Der Bildschirm zum Durchsuchen wird angezeigt. Eine Liste aller Zielgruppen, die zur Organisation gehören, wird angezeigt.](../images/ui/audience-portal/audience-browse.png)

### Schnellaktionen {#quick-actions}

Neben jeder Zielgruppe befindet sich ein Symbol mit Auslassungspunkten. Wenn Sie diese auswählen, wird eine Liste der verfügbaren Schnellaktionen für die Zielgruppe angezeigt. Diese Aktionsliste unterscheidet sich je nach Ursprung der Zielgruppe.

![Die Liste der Schnellaktionen wird für Zielgruppen mit dem Ursprung [!UICONTROL Zielgruppenkomposition] angezeigt.](../images/ui/audience-portal/browse-audience-composition-details.png)

| Aktion | Ursprünge | Beschreibung |
| ------ | ------- | ----------- |
| [!UICONTROL Vorlage] | Segmentierungs-Service | Öffnet Segment Builder zur Bearbeitung Ihrer Audience. Beachten Sie, dass Sie Ihre Zielgruppe, die über die API erstellt wurde **mit** Segment Builder bearbeiten können. Weitere Informationen zur Verwendung von Segment Builder finden Sie im [Handbuch zur Benutzeroberfläche von Segment Builder](./segment-builder.md). |
| [!UICONTROL Komposition öffnen] | Zielgruppenkomposition | Öffnet die Audience-Komposition, um Ihre Audience anzuzeigen. Weitere Informationen zur Komposition von Zielgruppen finden Sie im [Handbuch zur Benutzeroberfläche der Zielgruppenkomposition](./audience-composition.md). |
| [!UICONTROL Für Ziel aktivieren] | Segmentierungs-Service | Aktiviert die Zielgruppe für ein Ziel. Ausführlichere Informationen zur Aktivierung einer Zielgruppe für ein Ziel finden Sie in der [Übersicht zur Aktivierung](../../destinations/ui/activation-overview.md). |
| [!UICONTROL Für Partner freigeben] | Zielgruppen-Komposition, Benutzerdefinierter Upload, Segmentierungs-Service | Gibt Ihre Zielgruppe für andere Experience Platform-Benutzer frei. Weitere Informationen zu dieser Funktion finden Sie in der [Übersicht zu Segmentübereinstimmungen](./segment-match/overview.md). |
| [!UICONTROL Tags verwalten] | Zielgruppen-Komposition, Benutzerdefinierter Upload, Segmentierungs-Service | Verwaltet die benutzerdefinierten Tags, die zur Audience gehören. Weitere Informationen zu dieser Funktion finden Sie im Abschnitt zum [Filtern und Tagging](#manage-audiences). |
| [!UICONTROL In Ordner verschieben] | Zielgruppen-Komposition, Benutzerdefinierter Upload, Segmentierungs-Service | Verwaltet, zu welchem Ordner die Zielgruppe gehört. Weitere Informationen zu dieser Funktion finden Sie im Abschnitt zum [Filtern und Tagging](#manage-audiences). |
| [!UICONTROL Kopieren] | Segmentierungs-Service | Dupliziert die ausgewählte Zielgruppe. Weitere Informationen zu dieser Funktion finden Sie in den [Häufig gestellte Fragen zur Segmentierung](../faq.md#copy). |
| [!UICONTROL Zugriffsbeschriftungen anwenden] | Zielgruppen-Komposition, Benutzerdefinierter Upload, Segmentierungs-Service | Verwaltet die Zugriffsbeschriftungen für die Zielgruppe. Weitere Informationen zu Zugriffsbeschriftungen finden Sie in der Dokumentation zum [Verwalten von Beschriftungen](../../access-control/abac/ui/labels.md). |
| [!UICONTROL Veröffentlichen] | Benutzerdefinierter Upload, Segmentierungs-Service | Veröffentlicht die ausgewählte Zielgruppe. Weitere Informationen zur Verwaltung des Lebenszyklusstatus finden Sie im Abschnitt [Lebenszyklusstatus“ der häufig gestellten Fragen zur Segmentierung](../faq.md#lifecycle-states). |
| [!UICONTROL Deaktivieren] | Benutzerdefinierter Upload, Segmentierungs-Service | Deaktiviert die ausgewählte Zielgruppe. Um eine Zielgruppe zu deaktivieren, kann sie **nicht** in **beliebigen** Zielen (einschließlich Nicht-Experience Platform-Zielen) aktiviert werden oder Teil **beliebigen** anderen Zielgruppen sein. Weitere Informationen zur Verwaltung des Lebenszyklusstatus finden Sie im Abschnitt [Lebenszyklusstatus“ der häufig gestellten Fragen zur Segmentierung](../faq.md#lifecycle-states). |
| [!UICONTROL Löschen] | Zielgruppen-Komposition, Benutzerdefinierter Upload, Segmentierungs-Service | Löscht die ausgewählte Zielgruppe. Zielgruppen, die in nachgelagerten Zielen verwendet werden oder von anderen Zielgruppen abhängen **können** nicht gelöscht werden. Weitere Informationen zum Löschen von Audiences finden Sie unter [Häufig gestellte Fragen zur Segmentierung](../faq.md#lifecycle-states). |
| [!UICONTROL Zu Paket hinzufügen] | Zielgruppen-Komposition, Benutzerdefinierter Upload, Segmentierungs-Service | Verschiebt die Zielgruppe zwischen Sandboxes. Weitere Informationen zu dieser Funktion finden Sie im [Sandbox-Tool-Handbuch](../../sandboxes/ui/sandbox-tooling.md). |

>[!IMPORTANT]
>
>Stellen Sie vor dem Löschen Ihrer Zielgruppe sicher, dass die Zielgruppe **nicht** als Komponente in einer kontobasierten Zielgruppe oder in Adobe Journey Optimizer verwendet wird.

Oben auf der Seite finden Sie Optionen zum Hinzufügen aller Zielgruppen zu einem Zeitplan, zum Importieren einer Zielgruppe, zum Erstellen einer neuen Zielgruppe und zum Anzeigen einer Zusammenfassung der Zielgruppenauswertung.

Durch Umschalten auf **[!UICONTROL Alle Zielgruppen planen]** wird die geplante Segmentierung aktiviert. Weitere Informationen zur geplanten Segmentierung finden Sie im [Abschnitt „Geplante Segmentierung“ in diesem Benutzerhandbuch](#scheduled-segmentation).

Wenn Sie **[!UICONTROL Zielgruppe importieren]** auswählen, können Sie eine extern generierte Zielgruppe importieren. Weitere Informationen zum Importieren von Zielgruppen finden Sie im Abschnitt [Importieren einer Zielgruppe“ im Benutzerhandbuch](#import-audience).

Durch Auswahl von **[!UICONTROL Zielgruppe erstellen]** können Sie eine Zielgruppe erstellen. Um mehr über das Erstellen von Zielgruppen zu erfahren, lesen Sie den Abschnitt [Erstellen einer Zielgruppe](#create-audience) im Benutzerhandbuch.

![Die obere Navigationsleiste auf der Seite zum Durchsuchen von Zielgruppen ist hervorgehoben. Diese Leiste enthält eine Schaltfläche zum Erstellen einer Zielgruppe und eine Schaltfläche zum Importieren einer Zielgruppe.](../images/ui/audience-portal/browse-audiences-top.png)

Sie können auf **[!UICONTROL Auswertungszusammenfassung]** klicken, um ein Tortendiagramm anzuzeigen, das eine Zusammenfassung der Zielgruppenbewertungen anzeigt.

![Die Schaltfläche „Bewertungszusammenfassung“ ist hervorgehoben.](../images/ui/audience-portal/browse-audience-evaluation-summary.png)

Das Tortendiagramm wird angezeigt, in dem die Zielgruppen nach Zielgruppenbewertung aufgeschlüsselt sind. Das Diagramm zeigt die Gesamtzahl der Zielgruppen in der Mitte und unten die tägliche Batch-Auswertungszeit in UTC an. Wenn Sie den Mauszeiger über die verschiedenen Teile der Zielgruppe bewegen, wird die Anzahl der Zielgruppen angezeigt, die zu jedem Aktualisierungshäufigkeitstyp gehören.

![Das Tortendiagramm für die Zielgruppenbewertung ist hervorgehoben, wobei die Auswertungszeit für die Batch-Segmentierung ebenfalls angezeigt wird.](../images/ui/audience-portal/evaluation-summary.png)

### Anpassen {#customize}

Sie können zusätzliche Felder zu Audience Portal hinzufügen, indem Sie ![das Filterattribut-Symbol](/help/images/icons/column-settings.png) auswählen. Diese zusätzlichen Felder umfassen: Lebenszyklusstatus, Aktualisierungshäufigkeit, Zuletzt aktualisiert von, Beschreibung, Erstellt von und Zugriffsbeschriftungen.

| Feld | Beschreibung |
| ----- | ----------- |
| [!UICONTROL Name] | Der Name der Zielgruppe. |
| [!UICONTROL Anzahl der Profile] | Die Gesamtzahl der Profile, die für die Zielgruppe qualifiziert sind. |
| [!UICONTROL Herkunft] | Die Herkunft der Zielgruppe. Hier wird angegeben, woher die Zielgruppe stammt. Mögliche Werte sind [Segmentierungs-Service](#segment-builder), [Benutzerdefinierter Upload](#import-audience), [Zielgruppenkomposition](#audience-composition), [Audience Manager](https://experienceleague.adobe.com/de/docs/audience-manager/user-guide/aam-home), [Lookalike-Zielgruppe](../types/lookalike-audiences.md), [Federated Zielgruppenkomposition](#fac), [Customer Journey Analytics](https://experienceleague.adobe.com/de/docs/analytics-platform/using/cja-overview/cja-overview), [Data Distiller](#data-distiller), [AJO B2B](https://experienceleague.adobe.com/de/docs/journey-optimizer-b2b/user/guide-overview) und [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/destinations/experience-platform#audience-portal). |
| [!UICONTROL Lebenszyklus-Status] | Der Status der Zielgruppe. Mögliche Werte für dieses Feld sind `Draft`, `Inactive` und `Published`. Weitere Informationen zum Lebenszyklusstatus, einschließlich der Bedeutung der verschiedenen Status und der Verlagerung von Zielgruppen in verschiedene Lebenszyklusstatus, finden [ im Abschnitt „Lebenszyklusstatus“ der häufig gestellten Fragen zur Segmentierung](../faq.md#lifecycle-status). |
| [!UICONTROL Aktualisierungshäufigkeit] | Ein Wert, der angibt, wie oft die Daten der Zielgruppe aktualisiert werden. Mögliche Werte für dieses Feld sind [!UICONTROL Batch], [!UICONTROL Streaming], [!UICONTROL Edge] und [!UICONTROL Nicht geplant]. |
| [!UICONTROL Zuletzt aktualisiert von] | Der Name der Person, die die Zielgruppe zuletzt aktualisiert hat. |
| [!UICONTROL Erstellt] | Datum und Uhrzeit der Erstellung der Zielgruppe in UTC. |
| [!UICONTROL Zuletzt aktualisiert] | Datum und Uhrzeit der letzten Aktualisierung der Zielgruppe in UTC. |
| [!UICONTROL Tags] | Die benutzerdefinierten Tags, die zur Zielgruppe gehören. Weitere Informationen zu diesen Tags finden Sie im [Abschnitt zu Tags](#tags). |
| [!UICONTROL Beschreibung] | Die Beschreibung der Zielgruppe. |
| [!UICONTROL Erstellt von] | Der Name der Person, die die Zielgruppe erstellt hat. |
| [!UICONTROL Zugriffsbeschriftungen] | Die Zugriffsbeschriftungen für die Zielgruppe. Mit Zugriffsbeschriftungen können Sie Datensätze und Felder entsprechend den für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Diese Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Weitere Informationen zu Zugriffsbeschriftungen finden Sie in der Dokumentation unter [Verwalten von Beschriftungen](../../access-control/abac/ui/labels.md). |
| [!UICONTROL Aufschlüsselung] | Die Aufschlüsselung des Profilstatus für die Zielgruppe. Eine detailliertere Beschreibung dieser Aufschlüsselung des Profilstatus finden Sie unten. |

Wenn die Aufschlüsselung ausgewählt ist, wird ein Balkendiagramm angezeigt, das den prozentualen Anteil der Profile in jedem der folgenden berechneten Profilstatus anzeigt: [!UICONTROL Realisiert], [!UICONTROL Bestehend] und [!UICONTROL Verlassen]. Außerdem ist die auf der Registerkarte [!UICONTROL Durchsuchen] angezeigte Aufschlüsselung die genaueste Aufschlüsselung des Status der Segmentdefinition. Wenn diese Zahl von den Angaben auf der Registerkarte [!UICONTROL Übersicht] abweicht, sollten Sie als korrekte Informationsquelle die Zahlen auf der Registerkarte [!UICONTROL Durchsuchen] verwenden, da die Zahlen auf der Registerkarte [!UICONTROL Übersicht] nur einmal pro Tag aktualisiert werden.

| Status | Beschreibung |
| ------ | ----------- |
| [!UICONTROL Realisiert] | Die Anzahl der Profile **die sich in** letzten 24 Stunden seit der Ausführung des letzten Batch-Segmentauftrags für die Zielgruppe qualifiziert haben. |
| [!UICONTROL Bestehend] | Die Anzahl der Profile, **in** letzten 24 Stunden seit der Ausführung des letzten Batch-Segmentauftrags in der Zielgruppe verblieben sind. Dieses Feld ist **berechnet** und wird im [`segmentMembership` nicht ](../../xdm/field-groups/profile/segmentation.md). |
| [!UICONTROL Verlassen] | Die Anzahl der Profile, **die** in den letzten 24 Stunden seit der Ausführung des letzten Batch-Segmentauftrags verlassen haben. |

Nachdem Sie die Felder ausgewählt haben, die angezeigt werden sollen, können Sie auch die Breite der angezeigten Spalten ändern. Sie können dies tun, indem Sie den Bereich zwischen die Spalten ziehen oder indem Sie das ![Pfeilsymbol](/help/images/icons/chevron-down.png) der Spalte auswählen, deren Größe Sie ändern möchten, gefolgt von **[!UICONTROL Spaltengröße ändern]**.

![Die Schaltfläche „Spaltengröße ändern“ ist hervorgehoben.](../images/ui/audience-portal/browse-audience-resize-column.png)

### Filterung, Ordner und Tagging {#manage-audiences}

Um Ihre Arbeitseffizienz zu verbessern, können Sie nach vorhandenen Zielgruppen suchen, benutzerdefinierte Tags zu Zielgruppen hinzufügen, Zielgruppen in Ordnern ablegen und die angezeigten Zielgruppen filtern.

#### Suche {#search}

Mit [!DNL Unified Search] können Sie Ihre bestehenden Zielgruppen in bis zu 9 verschiedenen Sprachen suchen.

Um [!DNL Unified Search] zu verwenden, fügen Sie den gewünschten Suchbegriff in die hervorgehobene Suchleiste ein.

![Die Suchleiste ist hervorgehoben.](../images/ui/audience-portal/browse-audience-search.png)

Für weitere Informationen über [!DNL Unified Search], einschließlich der unterstützten Funktionen, lesen Sie die [Dokumentation zur einheitlichen Suche](https://experienceleague.adobe.com/docs/core-services/interface/services/search-experience-cloud.html?lang=de).

#### Tags {#tags}

Sie können benutzerdefinierte Tags hinzufügen, um Ihre Zielgruppen besser zu beschreiben, zu finden und zu verwalten.

Um ein Tag hinzuzufügen, wählen Sie **[!UICONTROL Tags verwalten]** für die Zielgruppe, die Sie markieren möchten.

![Die Schaltfläche [!UICONTROL Tags verwalten] ist für eine bestimmte Zielgruppe ausgewählt.](../images/ui/audience-portal/browse-manage-tags.png)

Das Popup-Fenster **[!UICONTROL Tags verwalten]** wird angezeigt. In diesem Popup-Fenster können Sie entweder ein kategorisiertes Tag oder ein nicht kategorisiertes Tag auswählen.

| Tag-Typ | Beschreibung |
| -------- | ----------- |
| Kategorisiert | Ein Tag, das von den Admins Ihrer Organisation erstellt und verwaltet wird. |
| Nicht kategorisiert | Ein Tag, das innerhalb des Popup-Fensters [!UICONTROL Tags verwalten] erstellt wird. Jeder kann diese Arten von Tags erstellen oder verwalten. |

![Das Popup-Fenster [!UICONTROL Tags verwalten] wird angezeigt. Die Optionen zur Auswahl einer kategorisierten oder nicht kategorisierten Auswahl sind hervorgehoben.](../images/ui/audience-portal/create-tag.png)

Nachdem Sie alle Tags hinzugefügt haben, die Sie an die Zielgruppe anhängen möchten, wählen Sie **[!UICONTROL Speichern]**.

![Im Popup-Fenster [!UICONTROL Tags verwalten] sind die hinzugefügten Tags hervorgehoben.](../images/ui/audience-portal/created-tags.png)

Weitere Informationen zum Erstellen und Verwalten von Tags finden Sie im [Handbuch zum Verwalten von Tags](../../administrative-tags/ui/managing-tags.md).

#### Ordner {#folders}

Für ein besseres Zielgruppen-Management können Sie Zielgruppen in Ordnern platzieren.

Um einen Ordner für Ihre Zielgruppen zu erstellen, wählen Sie **[!UICONTROL Ordner erstellen]** aus.

![Die Schaltfläche „Ordner erstellen“ ist hervorgehoben.](../images/ui/audience-portal/create-folder.png)

>[!NOTE]
>
>Sie können einen Ordner nur erstellen, wenn Sie sich in einem anderen Ordner befinden. Das bedeutet **dass Sie** Ordner nicht erstellen können, wenn **[!UICONTROL Alle Zielgruppen]** in der linken Navigationsleiste ausgewählt ist.

Ein Pop-up wird angezeigt, in dem Sie den neu erstellten Ordner benennen können. Wählen Sie **[!UICONTROL Speichern]** nach dem Benennen Ihres Ordners aus, um die Erstellung des Ordners abzuschließen. Beachten Sie, dass **Namen** übergeordneten Ordner eindeutig sein müssen.

![Die Schaltfläche „Speichern“ im Dialogfeld „Ordner erstellen“ ist hervorgehoben.](../images/ui/audience-portal/create-folder-dialog.png)

Um eine Zielgruppe in einen Ordner zu verschieben, wählen Sie **[!UICONTROL In Ordner verschieben]** für die Zielgruppe, die Sie verschieben möchten.

![Die Schaltfläche [!UICONTROL In Ordner verschieben] ist für eine bestimmte Zielgruppe ausgewählt.](../images/ui/audience-portal/browse-move-to-folder.png)

Das Popup-Fenster **Zielgruppe in Ordner verschieben** erscheint. Wählen Sie den Ordner aus, in den Sie die Zielgruppe verschieben möchten, und wählen Sie dann **[!UICONTROL Speichern]**.

![Das Popup-Fenster zum Verschieben der Zielgruppe in einen Ordner wird angezeigt. Der Ordner, in den die Zielgruppe verschoben wird, ist hervorgehoben.](../images/ui/audience-portal/move-to-folder.png)

Sobald sich die Zielgruppe in einem Ordner befindet, können Sie festlegen, dass nur Zielgruppen angezeigt werden, die zu einem bestimmten Ordner gehören.

![Zielgruppen, die zu einem bestimmten Ordner gehören, werden angezeigt.](../images/ui/audience-portal/browse-folders.png)

#### Filter {#filter}

Sie können Ihre Zielgruppen auch nach verschiedenen Einstellungen filtern.

Um die verfügbaren Zielgruppen zu filtern, wählen Sie das ![Filtersymbol](/help/images/icons/filter.png).

![Die Seite „Zielgruppen durchsuchen“ wird angezeigt, wobei das Filtersymbol hervorgehoben ist.](../images/ui/audience-portal/browse-select-filter.png)

Die Liste der verfügbaren Filter wird angezeigt.

| Filter | Beschreibung |
| ------ | ----------- |
| [!UICONTROL Herkunft] | Ermöglicht die Filterung nach der Herkunft der Zielgruppe. Mögliche Werte sind [Segmentierungs-Service](#segment-builder), [Benutzerdefinierter Upload](#import-audience), [Zielgruppenkomposition](#audience-composition), [Audience Manager](https://experienceleague.adobe.com/de/docs/audience-manager/user-guide/aam-home), [Lookalike-Zielgruppe](../types/lookalike-audiences.md), [Federated Zielgruppenkomposition](#fac), [Customer Journey Analytics](https://experienceleague.adobe.com/de/docs/analytics-platform/using/cja-overview/cja-overview), [Data Distiller](#data-distiller), [AJO B2B](https://experienceleague.adobe.com/de/docs/journey-optimizer-b2b/user/guide-overview) und [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/destinations/experience-platform#audience-portal). |
| [!UICONTROL Hat ein beliebiges Tag] | Filtert nach Tags. Sie können zwischen **[!UICONTROL Hat ein beliebiges Tag]** und **[!UICONTROL Hat alle Tags]** wählen. Wenn **[!UICONTROL Hat ein beliebiges Tag]** ausgewählt ist, enthalten die gefilterten Zielgruppen **jedes** der Tags, die Sie hinzugefügt haben. Wenn **[!UICONTROL Hat alle Tags]** ausgewählt ist, müssen die gefilterten Zielgruppen **alle** der von Ihnen hinzugefügten Tags enthalten. |
| [!UICONTROL Lebenszyklusstatus] | Ermöglicht die Filterung nach dem Lebenszyklusstatus der Zielgruppe. Zu den verfügbaren Optionen gehören [!UICONTROL Gelöscht], [!UICONTROL Entwurf], [!UICONTROL Inaktiv] und [!UICONTROL Veröffentlicht]. |
| [!UICONTROL Aktualisierungshäufigkeit] | Ermöglicht das Filtern nach der Aktualisierungshäufigkeit der Zielgruppe (Auswertungsmethode). Zu den verfügbaren Optionen [!UICONTROL Batch], [!UICONTROL Streaming] und [!UICONTROL Edge] |
| [!UICONTROL Erstellt von] | Ermöglicht die Filterung nach der Person, die die Zielgruppe erstellt hat. |
| [!UICONTROL Erstellungsdatum] | Ermöglicht die Filterung nach dem Erstellungsdatum der Zielgruppe. Sie können einen Datumsbereich auswählen, um danach zu filtern, wann die Zielgruppe erstellt wurde. |
| [!UICONTROL Änderungsdatum] | Damit können Sie nach dem letzten Änderungsdatum der Zielgruppe filtern. Sie können einen Datumsbereich auswählen, um danach zu filtern, wann die Zielgruppe zuletzt geändert wurde. |

![Die verfügbaren Filter werden auf der Seite „Zielgruppen durchsuchen“ angezeigt und hervorgehoben.](../images/ui/audience-portal/filter-audiences.png)

### Massenaktionen {#bulk-actions}

Darüber hinaus können Sie bis zu 25 verschiedene Zielgruppen auswählen und verschiedene Aktionen für diese Zielgruppen durchführen. Zu diesen Aktionen gehören [Verschieben in einen Ordner](#folders) [Bearbeiten oder Anwenden eines Tags](#tags), [Auswerten von Zielgruppen](#flexible-audience-evaluation) [Anwenden von Zugriffskennzeichnungen](../../access-control/abac/ui/labels.md) und [Löschen](#browse).

![Die verfügbaren Optionen für Massenaktionen werden angezeigt.](../images/ui/audience-portal/bulk-actions.png)

Wenn Sie Massenaktionen auf Zielgruppen anwenden, gelten die folgenden Bedingungen:

- Sie **Zielgruppen** verschiedenen Seiten auswählen.
- Eine Zielgruppe **die in einer Zielaktivierung verwendet wird, kann** nicht gelöscht werden.
- Wenn Sie einen Filter auswählen, werden die ausgewählten Zielgruppen **zurückgesetzt**.

#### Flexible Zielgruppenauswertung {#flexible-audience-evaluation}

Mit der flexiblen Zielgruppenauswertung können Sie bei Bedarf einen Segmentierungsauftrag ausführen. Weitere Informationen zur flexiblen Zielgruppenauswertung finden Sie im [Handbuch zur flexiblen Zielgruppenauswertung](../methods/flexible-audience-evaluation.md).

## Zielgruppendetails {#audience-details}

Um weitere Details zu einer bestimmten Zielgruppe anzuzeigen, wählen Sie den Namen der Zielgruppe auf der Registerkarte **[!UICONTROL Zielgruppen]** aus.

Die Seite mit den Details zur Zielgruppe wird angezeigt. Oben finden Sie eine Zusammenfassung der Zielgruppe, Informationen zur Größe der qualifizierten Zielgruppe sowie Ziele, für die das Segment aktiviert wurde.

![Die Detailseite für die Zielgruppe wird angezeigt. Die Karten für Zielgruppenzusammenfassung, Gesamtanzahl der Zielgruppen und aktivierte Ziele sind hervorgehoben.](../images/ui/audience-portal/audience-details-summary.png)

### Zielgruppenzusammenfassung {#audience-summary}

Der Abschnitt **[!UICONTROL Zielgruppenzusammenfassung]** enthält Informationen wie die ID, den Namen, die Beschreibung und Details der Attribute.

Darüber hinaus haben Sie die Möglichkeit, die Zielgruppe für ein Ziel zu aktivieren, Zugriffsbeschriftungen anzuwenden oder die Zielgruppe zu bearbeiten/zu aktualisieren.

Wenn Sie **[!UICONTROL Für Ziel aktivieren]** auswählen, können Sie die Zielgruppe für ein Ziel aktivieren. Detaillierte Informationen zum Aktivieren einer Zielgruppe für ein Ziel finden Sie in der [Übersicht zur Aktivierung](../../destinations/ui/activation-overview.md).

![Die Schaltfläche „Für Ziel aktivieren“ ist hervorgehoben.](../images/ui/audience-portal/audience-details-activate.png)

Wenn Sie **[!UICONTROL Zugriffsbeschriftungen anwenden]** auswählen, können Sie die Zugriffsbeschriftungen verwalten, die zur Zielgruppe gehören. Weitere Informationen zu Zugriffsbeschriftungen finden Sie in der Dokumentation zum [Verwalten von Beschriftungen](../../access-control/abac/ui/labels.md).

![Die Schaltfläche „Zugriffsbeschriftungen anwenden“ ist hervorgehoben.](../images/ui/audience-portal/audience-details-access-labels.png)

>[!BEGINTABS]

>[!TAB Zielgruppenkomposition]

![Die Seite mit den Zielgruppendetails mit hervorgehobener Schaltfläche [!UICONTROL Offene Komposition].](../images/ui/audience-portal/audience-details-open-composition.png)

Wenn Sie **[!UICONTROL Offene Komposition]** auswählen, können Sie Ihre Zielgruppe in der Zielgruppenkomposition anzeigen. Weitere Informationen zur Zielgruppenkomposition finden Sie im [Handbuch zur Benutzeroberfläche der Zielgruppenkomposition](./audience-composition.md).

>[!TAB Benutzerdefinierter Upload]

![Die Seite mit den Zielgruppendetails mit hervorgehobener Schaltfläche [!UICONTROL Zielgruppe aktualisieren].](../images/ui/audience-portal/audience-details-update-audience.png)

Wenn Sie **[!UICONTROL Zielgruppe aktualisieren]** auswählen, können Sie eine extern generierten Zielgruppe erneut hochladen. Weiterführende Informationen zum Import einer extern generierten Zielgruppe finden Sie im Abschnitt zum [Importieren einer Zielgruppe](#import-audience).

>[!TAB Segmentierungs-Service]

![Die Seite mit den Zielgruppendetails mit hervorgehobener Schaltfläche [!UICONTROL Zielgruppe bearbeiten].](../images/ui/audience-portal/audience-details-edit-audience.png)

Wenn Sie **[!UICONTROL Zielgruppe bearbeiten]** auswählen, können Sie Ihre Zielgruppe im Segment Builder bearbeiten. Detaillierte Informationen zur Verwendung des Arbeitsbereichs von [!DNL Segment Builder] finden Sie im [[!DNL Segment Builder] Benutzerhandbuch](./segment-builder.md).

>[!ENDTABS]

Wenn Sie **[!UICONTROL Eigenschaften bearbeiten]** auswählen, können Sie die grundlegenden Details der Zielgruppe bearbeiten, z. B. den Namen, die Beschreibung und die Tags.

![Die Schaltfläche „Eigenschaften bearbeiten“ ist auf der Seite mit den Zielgruppendetails hervorgehoben.](../images/ui/audience-portal/audience-details-edit-properties.png)

### Zielgruppe insgesamt {#audience-total}

Für von Experience Platform generierte Zielgruppen und Kompositionen wird im Abschnitt **[!UICONTROL Zielgruppe insgesamt]** die Gesamtzahl der Profile angezeigt, die für die Zielgruppe qualifiziert sind.

>[!NOTE]
>
>Es kann bis zu 30 Minuten dauern, bis die Gesamtanzahl der Zielgruppe nach Abschluss des Exportvorgangs aktualisiert ist.

Die Schätzungen werden anhand einer Stichprobengröße aus den Daten des jeweiligen Tages generiert. Wenn sich in Ihrem Profilspeicher weniger als 1 Million Entitäten befinden, wird der vollständige Datensatz verwendet. Bei zwischen 1 und 20 Millionen Entitäten werden 1 Million Entitäten verwendet, und bei mehr als 20 Millionen Entitäten werden 5 % der gesamten Entitäten verwendet. Weiterführende Informationen zum Generieren von Schätzungen finden Sie im Tutorial zur Zielgruppenerstellung im Abschnitt [Generieren von Schätzungen](../tutorials/create-a-segment.md#estimate-and-preview-an-audience).

### Aufnahmedetails {#ingestion-details}

Bei Zielgruppen mit dem Ursprung **[!UICONTROL Benutzerdefinierter Upload]** werden im Abschnitt **[!UICONTROL Aufnahmedetails]** sowohl die Profilsumme als auch Details zum Datensatz angezeigt, in den die extern generierte Zielgruppe aufgenommen wurde.

>[!NOTE]
>
>Es kann bis zu 30 Minuten nach dem Exportvorgang dauern, bis die Profilanzahl der Zielgruppe vollständig aktualisiert ist.

![Der Abschnitt „Aufnahmedetails“ für die Seite mit Zielgruppendetails wird angezeigt.](../images/ui/audience-portal/audience-details-ingestion-details.png)

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| Anzahl der Profile | Die Gesamtzahl der Profile, die für die Zielgruppe qualifiziert sind. |
| Datensatzname | Der Name des Datensatzes, in den die Zielgruppe aufgenommen wurde. Sie können den Datensatznamen auswählen, um weitere Informationen zum Datensatz zu erhalten. Weitere Informationen zu Datensätzen finden Sie im [Handbuch zur Datensatz-Benutzeroberfläche](../../catalog/datasets/user-guide.md). |
| Datensatz-Batch | Die ID des Datensatzes, in den die Zielgruppe aufgenommen wurde. Sie können die ID des Stapels auswählen, um weitere Informationen über den Stapel zu erhalten. Weitere Informationen zu Batches finden Sie im [Handbuch zur Datenaufnahme bei der Überwachung](../../ingestion/quality/monitor-data-ingestion.md#viewing-batches). |
| Profil-Batch | Die ID des Batches, der die Profile in Experience Platform erstellt hat. Sie können die ID des Stapels auswählen, um weitere Informationen über den Stapel zu erhalten. Weitere Informationen zu Batches finden Sie im [Handbuch zur Datenaufnahme bei der Überwachung](../../ingestion/quality/monitor-data-ingestion.md#viewing-batches). |
| Schema | Der Name des Schemas, zu dem die Zielgruppe gehört. Sie können den Namen des Schemas auswählen, um Informationen zur Struktur des Schemas anzuzeigen und Datennutzungskennzeichnungen anzuwenden. Weitere Informationen finden Sie im [Handbuch zum Verwalten von Datennutzungsbeschriftungen für ein Schema](../../xdm/tutorials/labels.md). |
| Aufgenommene Einträge | Die Anzahl der in den Datensatz aufgenommenen Datensätze. |
| Fehlgeschlagene Einträge | Die Anzahl der Datensätze, die nicht in den Datensatz aufgenommen werden konnten. |
| Neue Profilfragmente | Die Anzahl der neu erstellten Profile. |
| Vorhandene Profilfragmente | Die Anzahl der vorhandenen Profile, die aktualisiert wurden. |

>[!NOTE]
>
>Es empfiehlt sich, Datennutzungskennzeichnungen auf das Schema anzuwenden. Sie **können** eine Datennutzungskennzeichnung direkt auf die Zielgruppe anwenden.

### Aktivierte Ziele {#activated-destinations}

Der Abschnitt **[!UICONTROL Aktivierte Ziele]** zeigt die Ziele, für die diese Zielgruppe aktiviert ist.

>[!NOTE]
>
> Ziele sind eine Funktion, die mit [!DNL Adobe Real-Time Customer Data Platform] verfügbar ist und es Ihnen ermöglicht, Daten auf externe Plattformen zu exportieren. Weitere Informationen zu Zielen finden Sie unter [Ziele – Übersicht](../../destinations/home.md). Informationen zum Aktivieren eines Segments für ein Ziel finden Sie unter [Aktivierung – Übersicht](../../destinations/ui/activation-overview.md).

### Beispielprofile {#profile-samples}

Unten finden Sie eine Auswahl von Profilen, die für das Segment qualifiziert sind, mit detaillierten Informationen, einschließlich [!DNL Profile]-ID, Vorname, Nachname und persönlicher E-Mail-Adresse.

Die Methode, mit der das Daten-Sampling ausgelöst wird, hängt von der Art der Aufnahme ab.

Bei der Batch-Aufnahme wird der Profilspeicher automatisch alle fünfzehn Minuten gescannt, um festzustellen, ob seit dem letzten Sampling-Auftrag ein neuer Batch erfolgreich aufgenommen wurde. Wenn dies der Fall ist, wird der Profilspeicher anschließend überprüft, um festzustellen, ob sich die Anzahl der Datensätze um mindestens 5 % geändert hat. Wenn diese Bedingungen erfüllt sind, wird ein neuer Sampling-Auftrag ausgelöst.

Bei der Streaming-Aufnahme wird der Profilspeicher automatisch jede Stunde überprüft, um festzustellen, ob sich die Anzahl der Datensätze um mindestens 5 % geändert hat. Wenn diese Bedingung erfüllt ist, wird ein neuer Sampling-Auftrag ausgelöst.

Die Stichprobengröße der Überprüfung hängt von der Gesamtzahl der Entitäten in Ihrem Profilspeicher ab. Diese Stichprobengrößen sind in der folgenden Tabelle dargestellt:

| Entitäten im Profilspeicher | Stichprobengröße |
| ------------------------- | ----------- |
| Weniger als 1 Million | Vollständiger Datensatz |
| 1 bis 20 Millionen | 1 Million |
| Über 20 Millionen | 5 % der Gesamtgröße |

Ausführlichere Informationen zu jedem [!DNL Profile] erhalten Sie, wenn Sie auf die [!DNL Profile]-ID klicken. Um mehr über die Details eines Profils zu erfahren, lesen Sie bitte das [[!DNL Real-Time Customer Profile] Benutzerhandbuch](../../profile/ui/user-guide.md#profile-detail).

![Die Beispielprofile für die Zielgruppe sind hervorgehoben. Zu den Beispielprofilinformationen gehören die Profil-ID, der Vorname, der Nachname und die E-Mail-Adresse der Person.](../images/ui/audience-portal/audience-details-profiles.png)

## Geplante Segmentierung {#scheduled-segmentation}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_addallsegmentstoschedule"
>title="Alle Zielgruppen zum Zeitplan hinzufügen"
>abstract="Aktivieren Sie diese Option, um alle Zielgruppen einzubeziehen, die mit der Batch-Segmentierung in der täglich geplanten Aktualisierung ausgewertet wurden. Deaktivieren Sie sie, um alle Zielgruppen aus der geplanten Aktualisierung zu entfernen."

Nachdem Sie Zielgruppen erstellt haben, können Sie diese durch eine bedarfsgesteuerte oder geplante (kontinuierliche) Auswertung auswerten. Auswertung bedeutet, dass [!DNL Real-Time Customer Profile]-Daten durch Segmentaufträge bewegt werden, um entsprechende Zielgruppen zu produzieren. Nach der Erstellung werden die Zielgruppen gespeichert und aufbewahrt, sodass sie über die APIs von [!DNL Experience Platform] exportiert werden können.

Bei der bedarfsgesteuerten Auswertung wird die API zur Durchführung von Auswertungen und zum Aufbau von Zielgruppen nach Bedarf verwendet. Bei der geplanten Auswertung (auch „geplante Segmentierung“ genannt) können Sie hingegen einen wiederkehrenden Zeitplan erstellen, um die Zielgruppen zu einem bestimmten Zeitpunkt (maximal einmal täglich) auszuwerten.

### Aktivieren der geplanten Segmentierung {#enable-scheduled-segmentation}

Die Aktivierung Ihrer Zielgruppen für eine geplante Auswertung kann über die Benutzeroberfläche oder die API erfolgen. Kehren Sie in der Benutzeroberfläche zur Registerkarte **[!UICONTROL Durchsuchen]** in **[!UICONTROL Zielgruppen]** zurück und schalten Sie **[!UICONTROL Geplante Auswertung aller Zielgruppen]** ein. Dadurch werden alle Zielgruppen anhand des von Ihrer Organisation festgelegten Zeitplans ausgewertet.

>[!NOTE]
>
>Die geplante Auswertung kann für Sandboxes mit maximal fünf (5) Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] aktiviert werden. Wenn Ihre Organisation in einer Sandbox-Umgebung über mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] verfügt, können Sie keine geplante Auswertung verwenden.

Zeitpläne können derzeit nur mit der API erstellt werden. Ausführliche Anweisungen zum Erstellen, Bearbeiten und Verwenden von Zeitplänen mithilfe der API finden Sie im Tutorial zum Auswerten und Aufrufen von Segmentergebnissen, insbesondere im Abschnitt zur [geplanten Auswertung mithilfe der API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![Der Umschalter zum Planen aller Zielgruppen ist im Zielgruppenportal hervorgehoben.](../images/ui/audience-portal/browse-audiences-scheduled.png)

## Erstellen einer Zielgruppe {#create-audience}

Sie können **[!UICONTROL Zielgruppe erstellen]** auswählen, um eine Zielgruppe zu erstellen.

![Auf der Seite zum Durchsuchen von Zielgruppen ist die Schaltfläche „Zielgruppe erstellen“ hervorgehoben.](../images/ui/audience-portal/browse-create-audience.png)

Es wird ein Pop-up angezeigt, in dem Sie auswählen können, ob Sie eine Zielgruppe oder Regeln erstellen möchten.

![Ein Pop-up, das die beiden Arten von Zielgruppen anzeigt, die Sie erstellen können.](../images/ui/audience-portal/create-audience-type.png)

### Zielgruppenkomposition {#audience-composition}

Durch Auswählen von **[!UICONTROL Zielgruppen erstellen]** gelangen Sie zur Zielgruppenkomposition. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Zielgruppen, z. B. Drag-and-Drop-Kacheln, die verschiedenen Aktionen entsprechen. Weitere Informationen zum Erstellen von Zielgruppen finden Sie im [Handbuch zur Zielgruppenkomposition](./audience-composition.md).

![Der Arbeitsbereich „Zielgruppenkomposition“ wird angezeigt.](../images/ui/audience-portal/audience-composition.png)

### Segment Builder {#segment-builder}

Wenn Sie **[!UICONTROL Regel erstellen]** auswählen, gelangen Sie zum Segment Builder. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Segmentdefinitionen, z. B. Drag-and-Drop-Kacheln, die Dateneigenschaften entsprechen. Weitere Informationen zum Erstellen von Segmentdefinitionen finden Sie im [Segment Builder-Handbuch](./segment-builder.md)

![Der Segment Builder-Arbeitsbereich wird angezeigt.](../images/ui/audience-portal/segment-builder.png)

### Komposition föderierter Zielgruppen {#fac}

Sie können die Federated-Audience-Komposition von Adobe verwenden, um neue Zielgruppen aus Unternehmensdatensätzen zu erstellen, ohne die zugrunde liegenden Daten zu kopieren, und diese Zielgruppen in Adobe Experience Platform Audience Portal zu speichern.

Sie können auch bestehende Zielgruppen in Adobe Experience Platform anreichern, indem Sie zusammengestellte Zielgruppendaten verwenden, die aus dem Enterprise Data Warehouse zusammengeführt wurden. Lesen Sie das Handbuch zu [Komposition föderierter Zielgruppen](https://experienceleague.adobe.com/de/docs/federated-audience-composition/using/home).

![Eine Liste von Zielgruppen, die in der Federated-Audience-Komposition für Ihre Organisation erstellt wurden.](../images/ui/overview/federated-audience-composition.png)

### Data Distiller {#data-distiller}

Sie können die SQL-Erweiterung von Data Distiller verwenden, um Zielgruppen aus dem Data Lake zu erstellen. Diese Daten enthalten vorhandene Dimensionsentitäten wie Kundenattribute oder Produktinformationen.

Weitere Informationen zu Data Distiller finden Sie im Handbuch [Erstellen von Zielgruppen mithilfe von SQL](../../query-service/data-distiller-audiences/overview.md).

## Importieren einer Zielgruppe {#import-audience}

>[!IMPORTANT]
>
>Um eine extern generierte Zielgruppe zu importieren, **müssen** über die folgenden Berechtigungen verfügen: [!UICONTROL Segmente anzeigen], [!UICONTROL Segmente verwalten] und [!UICONTROL Zielgruppe importieren]. Weitere Informationen zu diesen Berechtigungen finden Sie unter [Zugriffssteuerung - Übersicht](../../access-control/home.md#permissions).

Sie können **[!UICONTROL Zielgruppe importieren]** auswählen, um eine extern generierte Zielgruppe zu importieren.

![Auf der Seite „Zielgruppen durchsuchen“ ist die Schaltfläche „Zielgruppe importieren“ hervorgehoben.](../images/ui/audience-portal/browse-import-audience.png)

Der Workflow **[!UICONTROL Zielgruppen-CSV importieren]** wird angezeigt. Sie können eine CSV-Datei auswählen, die als extern generierte Zielgruppe importiert werden soll.

![Im Workflow [!UICONTROL Zielgruppen-CSV importieren] ist das Kontrollkästchen [!UICONTROL Dateien per Drag-and-Drop verschieben] hervorgehoben und zeigt an, wo Sie Ihre extern generierten Zielgruppen hochladen können.](../images/ui/audience-portal/import-audience-csv.png)

>[!NOTE]
>
>Die extern generierte Zielgruppe **muss** im CSV-Format vorliegen, darf **maximal** 25 Spalten enthalten und muss kleiner als 1 GB sein.
>
>Darüber hinaus **Sie** Leerzeichen oder Gedankenstriche in der ersten Zeile oder den zugehörigen Spalten der CSV-Datei nicht verwenden.
>
>Der Wert der ersten Zeile kann beispielsweise „FirstName“ oder „First_Name“ sein, er darf jedoch nicht „First Name“ oder „First-Name“ lauten.

Nach Auswahl der zu importierenden CSV-Datei wird eine Liste mit Beispieldaten für diese extern generierte Zielgruppe angezeigt. Nachdem Sie die Richtigkeit der Beispieldaten bestätigt haben, wählen Sie **[!UICONTROL Weiter]** aus.

![Beispieldaten für die extern generierte Zielgruppe werden angezeigt.](../images/ui/audience-portal/import-audience-sample-data.png)

Die Seite **[!UICONTROL Zielgruppendetails]** erscheint. Sie können Informationen über Ihre Zielgruppe hinzufügen, einschließlich Name, Beschreibung, primäre Identität und Identity-Namespace-Wert.

Beim Importieren der extern generierten Zielgruppe müssen Sie eine der Spalten als primäres Identitätsfeld auswählen und den Namespace-Wert angeben. Beachten Sie, dass alle verbleibenden Felder als &quot;**&quot;** werden. Diese Attribute gelten als **nicht beständig** da sie nur zur Personalisierung mit dieser Zielgruppe verknüpft sind und **nicht** mit dem Profil verbunden sind.

![Die Seite [!UICONTROL Zielgruppendetails] wird angezeigt.](../images/ui/audience-portal/import-audience-audience-details.png)

Sie können Ihrer extern generierten Zielgruppe optional auch einige zusätzliche Details hinzufügen, z. B. eine ID zuweisen, ihre Zusammenführungsrichtlinie definieren oder ihren Spaltendatentyp bearbeiten.

>[!NOTE]
>
>Wenn Sie eine benutzerdefinierte externe Zielgruppen-ID verwenden, müssen Sie die folgenden Richtlinien einhalten:
>
> - Sie **muss** mit einem Buchstaben (a-z oder A-Z), einem Unterstrich (_) oder einem Dollarzeichen ($) beginnen.
> - Alle nachfolgenden Zeichen können alphanumerisch (a-z, A-Z, 0-9), Unterstriche (_) oder Dollarzeichen ($) sein.

Nachdem Sie die Zielgruppendetails ausgefüllt haben, wählen Sie **[!UICONTROL Weiter]** aus.

![Die Schaltfläche [!UICONTROL Weiter] ist auf der Seite [!UICONTROL Zielgruppendetails] hervorgehoben.](../images/ui/audience-portal/import-audience-filled-details.png)

Die Seite **[!UICONTROL Überprüfen]** wird angezeigt. Sie können die Details Ihrer neu importierten, extern generierten Zielgruppe überprüfen.

![Die Seite [!UICONTROL Überprüfen] wird angezeigt und gibt Details zu Ihren neu importierten, extern generierten Zielgruppen an.](../images/ui/audience-portal/import-audience-review-details.png)

Nachdem Sie bestätigt haben, dass die Details korrekt sind, wählen Sie **[!UICONTROL Beenden]** aus, um Ihre extern generierte Zielgruppe in Adobe Experience Platform zu importieren.

>[!IMPORTANT]
>
>Standardmäßig laufen die Daten extern generierter Zielgruppen 30 Tage ab. Der Ablauf der Daten wird zurückgesetzt, wenn die Zielgruppe in irgendeiner Weise aktualisiert oder geändert wird.
>
>Wenn Ihre extern generierte Zielgruppe außerdem sensible und/oder gesundheitsbezogene Informationen enthält, **müssen** die erforderlichen Datennutzungskennzeichnungen vor der Aktivierung auf ein beliebiges Ziel anwenden. Da Variablen von extern generierten Zielgruppen im Data Lake und nicht im Echtzeit-Kundenprofil gespeichert werden, sollten **nicht** Einverständnisdaten in Ihre CSV-Datei einschließen.
>
>Weitere Informationen zum Anwenden von Datennutzungskennzeichnungen finden Sie in der Dokumentation unter [ von Kennzeichnungen](../../access-control/abac/ui/labels.md). Um mehr über Datennutzungskennzeichnungen in Experience Platform im Allgemeinen zu erfahren, lesen Sie [Datennutzungskennzeichnungen - Übersicht](../../data-governance/labels/overview.md). Informationen zur Funktionsweise des Einverständnisses in extern generierten Zielgruppen finden Sie in den [Häufig gestellte Fragen zu Zielgruppen](../faq.md#consent).

## Nächste Schritte

Nach dem Lesen dieser Übersicht sollten Sie in der Lage sein, Zielgruppenportal zu verwenden, um Zielgruppen effektiv zu verwalten, zu erstellen und in Adobe Experience Platform zu importieren.

Für weitere Informationen zur Verwendung der Segmentierungsdienst-Benutzeroberfläche lesen Sie bitte den [Überblick über die Segmentierungs-Service-Benutzeroberfläche](./overview.md).

Häufig gestellte Fragen zu Audience Portal finden Sie unter [Häufig gestellte Fragen](../faq.md).
