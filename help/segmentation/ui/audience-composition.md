---
solution: Experience Platform
title: Handbuch zur Zielgruppen-Benutzeroberfläche
description: Die Zielgruppenkomposition in der Adobe Experience Platform-Benutzeroberfläche bietet einen umfassenden Arbeitsbereich, in dem Sie mit Profildatenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Zielgruppen für Ihre Organisation.
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 56d9d3ec5565960438540ffec867ed528b52eaf1
workflow-type: tm+mt
source-wordcount: '1767'
ht-degree: 54%

---

# Handbuch zur Benutzeroberfläche für Zielgruppenkomposition

>[!NOTE]
>
>In diesem Handbuch wird beschrieben, wie Sie Zielgruppen mithilfe der Zielgruppenkomposition erstellen. Informationen zum Erstellen von Zielgruppen mithilfe von Segmentdefinitionen mithilfe von Segment Builder finden Sie im Abschnitt [Handbuch zur Benutzeroberfläche von Segment Builder](./segment-builder.md).

Zielgruppenkomposition bietet einen Arbeitsbereich zum Erstellen und Bearbeiten von Zielgruppen mithilfe von Bausteinen, die zur Darstellung verschiedener Aktionen verwendet werden.

![Die Benutzeroberfläche für die Zielgruppenkomposition .](../images/ui/audience-composition/audience-composition.png)

Um die Details der Komposition, einschließlich Titel und Beschreibung, zu ändern, wählen Sie die ![Regler](../images/ui/audience-composition/sliders.png) Schaltfläche.

Die **[!UICONTROL Kompositionseigenschaften]** Popover angezeigt. Sie können Details zu Ihrer Komposition einfügen, einschließlich Titel und Beschreibung hier.

![Das Popover Kompositionseigenschaften wird angezeigt.](../images/ui/audience-composition/composition-properties.png)

>[!NOTE]
>
>Wenn Sie **not** Geben Sie Ihrer Komposition einen Titel, sie hat einen Titel &quot;Komposition&quot;, gefolgt von dem Erstellungsdatum und der Erstellungszeit standardmäßig.

Nachdem Sie die Details Ihrer Komposition aktualisiert haben, wählen Sie **[!UICONTROL Speichern]** um diese Aktualisierungen zu bestätigen. Die Arbeitsfläche für die Zielgruppenzusammensetzung wird erneut angezeigt.

Die Arbeitsfläche für die Zielgruppenzusammensetzung besteht aus vier verschiedenen Baustypen: **[[!UICONTROL Zielgruppe]](#audience-block)**, **[[!UICONTROL Ausschließen]](#exclude-block)**, **[[!UICONTROL Rang]](#rank-block)**, und **[[!UICONTROL Aufspaltung]](#split-block)**.

## [!UICONTROL Zielgruppe] {#audience-block}

Mit dem Block **[!UICONTROL Zielgruppe]** können Sie die Unterzielgruppen hinzufügen, aus denen Sie Ihre neue größere Zielgruppe erstellen möchten. Standardmäßig ist ein **[!UICONTROL Zielgruppen]**-Block oben auf der Arbeitsfläche für die Komposition enthalten.

Wenn Sie die **[!UICONTROL Zielgruppe]** -Baustein, zeigt die rechte Leiste Steuerelemente für die Kennzeichnung der Zielgruppe, das Hinzufügen von Zielgruppen zum Baustein sowie das Erstellen benutzerdefinierter Regeln für den Zielgruppenblock an.

>[!NOTE]
>
>Sie können entweder Zielgruppen hinzufügen **oder** eine benutzerspezifische Regel erstellen. Diese beiden Funktionen **cannot** zusammen verwendet werden.

![Details zum Zielgruppen-Block werden angezeigt.](../images/ui/audience-composition/audience-block.png)

### [!UICONTROL Audience hinzufügen] {#add-audience}

So fügen Sie Zielgruppen zum Audience -Block hinzu. select **[!UICONTROL Zielgruppe hinzufügen]**.

![Die Schaltfläche Audience hinzufügen ist hervorgehoben.](../images/ui/audience-composition/add-audience.png)

Eine Liste von Zielgruppen wird angezeigt. Wählen Sie die Zielgruppe aus, die Sie einbeziehen möchten, und dann **[!UICONTROL Hinzufügen]**, um sie an Ihren Zielgruppen-Block anzuhängen.

![Eine Liste von Zielgruppen wird angezeigt. In diesem Dialogfeld können Sie auswählen, welche Zielgruppe Sie hinzufügen möchten.](../images/ui/audience-composition/select-audience.png)

Ihre ausgewählten Zielgruppen werden jetzt in der rechten Leiste angezeigt, wenn der Block **[!UICONTROL Zielgruppe]** aktiviert ist. Von hier aus können Sie den Zusammenführungstyp der kombinierten Zielgruppen ändern.

![Die möglichen Zusammenführungstypen für die Zielgruppen sind hervorgehoben.](../images/ui/audience-composition/merge-types.png)

| Zusammenführungstyp | Beschreibung |
| ---------- | ----------- |
| [!UICONTROL Vereinigung] | Die Zielgruppen werden zu einer Zielgruppe zusammengefasst. Dies entspricht einem OR-Vorgang. |
| [!UICONTROL Schnittmenge] | Die Zielgruppen werden nur mit den Zielgruppen kombiniert, die in **allen** freigegeben sind und hinzugefügt werden. Dies entspricht einem AND-Vorgang. |
| [!UICONTROL Ausschließen von Überschneidungen] | Die Zielgruppen werden kombiniert, wobei nur die Zielgruppen hinzugefügt werden, die zu genau **einer, aber nicht zu allen** gehören. Dies entspricht einem XOR-Vorgang. |

### [!UICONTROL Regel erstellen] {#build-rule}

Um eine benutzerdefinierte Regel zum Audience-Block hinzuzufügen, wählen Sie **[!UICONTROL Regel erstellen]**.

![Die Schaltfläche Regel erstellen ist hervorgehoben.](../images/ui/audience-composition/build-rule.png)

Segment Builder wird angezeigt. Sie können den Segment Builder verwenden, um eine benutzerdefinierte Regel für die Zielgruppe zu erstellen. Weitere Informationen zur Verwendung von Segment Builder finden Sie im Abschnitt [Segment Builder-Handbuch](./segment-builder.md).

![Die Benutzeroberfläche von Segment Builder wird angezeigt.](../images/ui/audience-composition/segment-builder.png)

Nachdem Sie eine benutzerdefinierte Regel hinzugefügt haben, wählen Sie **[!UICONTROL Speichern]** , um die Regel Ihrer Zielgruppe hinzuzufügen.

![](../images/ui/audience-composition/custom-rule.png)

## [!UICONTROL Ausschließen] {#exclude-block}

Mit dem Blocktyp **[!UICONTROL Ausschließen]** können Sie bestimmte Unterzielgruppen oder Attribute aus Ihrer neuen größeren Zielgruppe ausschließen.

Um einen Block **[!UICONTROL Ausschließen]** hinzuzufügen, wählen Sie das Symbol **+** und dann **[!UICONTROL Ausschließen]** aus.

![Die Option „Ausschließen“ ist ausgewählt.](../images/ui/audience-composition/add-exclude-block.png)

Der Block **[!UICONTROL Ausschließen]** wird hinzugefügt. Wenn dieser Block ausgewählt ist, werden Details zum Ausschluss in der rechten Leiste angezeigt. Dazu gehören die Kennzeichnung und der Ausschlusstyp des Blocks. Sie können [nach Zielgruppe](#exclude-audience) oder [nach Attribut](#exclude-attribute) ausschließen.

![Der Block „Ausschließen“, in dem die beiden verfügbaren Ausschlusstypen hervorgehoben sind.](../images/ui/audience-composition/exclude.png)

### Ausschließen nach Zielgruppe {#exclude-audience}

Wenn Sie nach Zielgruppe ausschließen, können Sie durch Auswahl von **[!UICONTROL Zielgruppe hinzufügen]** auswählen, welche Zielgruppen ausgeschlossen werden sollen.

![Die Schaltfläche „Zielgruppe hinzufügen“ ist ausgewählt, über die Sie auswählen können, welche Zielgruppe Sie ausschließen möchten.](../images/ui/audience-composition/add-excluded-audience.png)

Eine Liste von Zielgruppen wird angezeigt. Wählen Sie **[!UICONTROL Hinzufügen]** aus, um die Zielgruppen, die ausgeschlossen werden sollen, Ihrem Ausschlussblock hinzuzufügen.

![Eine Liste von Zielgruppen wird angezeigt. In diesem Dialogfeld können Sie auswählen, welche Zielgruppe Sie hinzufügen möchten.](../images/ui/audience-composition/select-audience.png)

### Ausschließen nach Attribut {#exclude-attribute}

Wenn Sie nach Attribut ausschließen, können Sie durch Auswahl des Symbols ![Filtern](../images/ui/audience-composition/filter-attribute.png) innerhalb des Abschnitts **[!UICONTROL Ausschlussregel]** festlegen, welche Attribute ausgeschlossen werden sollen.

![Der Abschnitt „Attribut“ wird hervorgehoben und zeigt an, wo das auszuschließende Attribut ausgewählt werden soll.](../images/ui/audience-composition/exclude-attribute.png)

Eine Liste der Profilattribute wird angezeigt. Wählen Sie den Attributtyp aus, den Sie ausschließen möchten, und dann **[!UICONTROL Auswählen]**, um diese Attribute zu Ihrem Ausschlussblock hinzuzufügen.

![Eine Liste mit Attributen wird angezeigt.](../images/ui/audience-composition/select-attribute-exclude.png)

## [!UICONTROL Anreichern] {#enrich-block}

>[!IMPORTANT]
>
>Zu diesem Zeitpunkt können Anreicherungsattribute **only** in nachgelagerten Adobe Journey Optimizer-Szenarien verwendet werden.

Die **[!UICONTROL Anreichern]** Mit dem Blocktyp können Sie Ihre Zielgruppe mit zusätzlichen Attributen aus einem Datensatz anreichern. Sie können diese Attribute in Anwendungsfällen der Personalisierung verwenden.

So fügen Sie eine **[!UICONTROL Anreichern]** -Block, wählen Sie die **+** Symbol, gefolgt von **[!UICONTROL Anreichern]**.

![Die [!UICONTROL Anreichern] ausgewählt ist.](../images/ui/audience-composition/add-enrich-block.png)

Die **[!UICONTROL Anreichern]** hinzugefügt. Wenn dieser Block ausgewählt ist, werden Details zur Anreicherung in der rechten Leiste angezeigt. Dazu gehören der Titel des Blocks und der Anreicherungsdatensatz.

Um den Datensatz zur Anreicherung der Audience auszuwählen, wählen Sie die ![filter](../images/ui/audience-composition/filter-attribute.png) Symbol.

![Die Filterschaltfläche ist hervorgehoben. Wenn Sie dies auswählen, gelangen Sie zum [!UICONTROL Datensatz auswählen] Popover.](../images/ui/audience-composition/enrich-select-dataset.png)

Die **[!UICONTROL Datensatz auswählen]** Popover angezeigt. Wählen Sie den Datensatz aus, den Sie zur Anreicherung hinzufügen möchten, gefolgt von **[!UICONTROL Auswählen]** , um den Datensatz zur Anreicherung hinzuzufügen.

![Der ausgewählte Datensatz wird ausgewählt.](../images/ui/audience-composition/enrich-dataset-selected.png)

>[!IMPORTANT]
>
>Der ausgewählte Datensatz **must** die folgenden Kriterien erfüllen:
>
>- Der Datensatz **must** von Datensatztyp sein.
>   - Der Datensatz **cannot** vom Ereignistyp sein, systemgeneriert oder für Profil markiert sein.
>- Der Datensatz **must** 1 GB oder kleiner sein.

Die **[!UICONTROL Anreicherungskriterien]** wird nun in der rechten Leiste angezeigt. In diesem Abschnitt können Sie die **[!UICONTROL Quellenverbindungsschlüssel]** und **[!UICONTROL Join-Schlüssel für Anreicherungsdatensatz]**, mit dem Sie den Anreicherungsdatensatz mit der Zielgruppe verknüpfen können, die Sie erstellen möchten.

![Die [!UICONTROL Anreicherungskriterien] -Bereich markiert ist.](../images/ui/audience-composition/enrichment-criteria.png)

So wählen Sie die **[!UICONTROL Quellenverbindungsschlüssel]**, wählen Sie die ![filter](../images/ui/audience-composition/filter-attribute.png) Symbol.

![Das Filtersymbol für [!UICONTROL Quellenverbindungsschlüssel] hervorgehoben ist.](../images/ui/audience-composition/enrich-select-source-join-key.png)

Die **[!UICONTROL Profilattribut auswählen]** Popover angezeigt. Wählen Sie das Profilattribut aus, das Sie als Quell-Join-Schlüssel verwenden möchten, gefolgt von **[!UICONTROL Auswählen]** um dieses Attribut als Quell-Join-Schlüssel auszuwählen.

![Das Attribut, das Sie als Quell-Join-Schlüssel verwenden möchten, wird hervorgehoben.](../images/ui/audience-composition/enrich-select-profile-attribute.png)

So wählen Sie die **[!UICONTROL Join-Schlüssel für Anreicherungsdatensatz]**, wählen Sie die ![filter](../images/ui/audience-composition/filter-attribute.png) Symbol.

![Das Filtersymbol für [!UICONTROL Join-Schlüssel für Anreicherungsdatensatz] hervorgehoben ist.](../images/ui/audience-composition/enrich-select-enrichment-dataset-join-key.png)

Die **[!UICONTROL Anreicherungsattribute]** Popover angezeigt. Wählen Sie das Attribut aus, das Sie als Join-Schlüssel für den Anreicherungsdatensatz verwenden möchten, gefolgt von **[!UICONTROL Auswählen]** , um dieses Attribut als Join-Schlüssel für Ihren Anreicherungsdatensatz auszuwählen.

![Das Attribut, das Sie als Join-Schlüssel für den Anreicherungsdatensatz verwenden möchten, wird hervorgehoben.](../images/ui/audience-composition/enrich-select-enrichment-dataset-attribute.png)

Nachdem Sie nun beide Join-Schlüssel hinzugefügt haben, wird die **[!UICONTROL Anreicherungsattribute]** angezeigt. Jetzt können Sie das Attribut hinzufügen, mit dem Sie Ihre Zielgruppe erweitern möchten. Um diese Attribute hinzuzufügen, wählen Sie **[!UICONTROL Attribut hinzufügen]**.

![Die [!UICONTROL Attribut hinzufügen] -Schaltfläche markiert ist.](../images/ui/audience-composition/enrich-select-add-attribute.png)

Die **[!UICONTROL Anreicherungsattribute]** Popover angezeigt. Sie können die Attribute aus dem Datensatz auswählen, um Ihre Zielgruppe mit **[!UICONTROL Auswählen]** , um die Attribute Ihrer Audience hinzuzufügen.

![Die Anreicherungsattribute, die Sie hinzufügen möchten, werden hervorgehoben.](../images/ui/audience-composition/enrich-add-enrichment-attributes.png)

<!-- ## [!UICONTROL Join] {#join-block}

The **[!UICONTROL Join]** block type allows you to add in external audiences from datasets that have not yet been processed by Adobe Experience Platform.

To add a **[!UICONTROL Join]** block, select the **+** icon, followed by **[!UICONTROL Join]**.

![The Join option is selected.](../images/ui/audience-composition/add-join-block.png)

When you select the block, details about the join are shown in the right rail, including the block's label and the option to add audiences to the enrichment dataset.

![The join block is highlighted, including details about the join block.](../images/ui/audience-composition/join.png)

After selecting **[!UICONTROL Add Audience]**, a list of audiences appears. Select the audiences you want to include, followed by **[!UICONTROL Add]** to add them to your join block.

![A list of audiences appears. You can select which audience you want to add from this dialog.](../images/ui/audience-composition/select-audience.png)

Your selected audiences now appear within the right rail when the **[!UICONTROL Join]** block is selected. 

![The audiences that were added as part of the Join are shown.](../images/ui/audience-composition/selected-audiences.png) -->

## [!UICONTROL Rang] {#rank-block}

Die **[!UICONTROL Rang]** Mit dem Blocktyp können Sie Profile nach einem bestimmten Attribut sortieren und sortieren und diese bewerteten Profile in Ihre Komposition aufnehmen.

Um einen Block **[!UICONTROL Rang]** hinzuzufügen, wählen Sie das Symbol **+** und dann **[!UICONTROL Rang]** aus.

![Die Option „Rang“ ist ausgewählt.](../images/ui/audience-composition/add-rank-block.png)

Bei der Auswahl des Blocks werden Details zum Rang in der rechten Leiste angezeigt, einschließlich der Kennzeichnung des Blocks, des nach Rang zu ordnenden Attributs, der Rangreihenfolge und eines Umschalters zur Begrenzung der Anzahl der nach Rang zu ordnenden Profile.

![Der Block „Rang“ ist mit zugehörigen Details hervorgehoben.](../images/ui/audience-composition/rank.png)

Um festzulegen, nach welchem Attribut die Zielgruppen geordnet werden sollen, wählen Sie das Symbol ![Filtern](../images/ui/audience-composition/filter-attribute.png) aus.

![Das Filtersymbol ist hervorgehoben und zeigt an, welche Optionen für den Zugriff auf den Bildschirm zur Profilattributauswahl ausgewählt werden sollen.](../images/ui/audience-composition/select-rank-attribute.png)

Eine Liste der Profilattribute wird angezeigt. In diesem Popup können Sie den Attributtyp auswählen, nach dem Sie Ihre Zielgruppe ordnen möchten. Wählen Sie **[!UICONTROL Auswählen]** aus, um ihn Ihrem Block „Rang“ hinzuzufügen. Beachten Sie, dass das ausgewählte Attribut **only** sind Zahlen.

![Eine Liste mit Attributen wird angezeigt.](../images/ui/audience-composition/select-attribute-rank.png)

Nach Auswahl des Attributs können Sie die Reihenfolge auswählen, nach der geordnet werden soll. Dies geschieht entweder in aufsteigender (von niedrigster zu höchster) oder in absteigender (von höchster zu niedrigster) Reihenfolge.

Darüber hinaus können Sie die Anzahl der zurückgegebenen Zielgruppen einschränken, indem Sie den Umschalter **[!UICONTROL Profil-Limit hinzufügen]** aktivieren. Wenn dieser Umschalter aktiviert ist, können Sie die maximale Anzahl von Zielgruppen festlegen, die innerhalb des Felds **[!UICONTROL Enthaltene Profile]** zurückgegeben wird.

![Der Umschalter „Profil-Limit hinzufügen“ ist hervorgehoben, sodass Sie die Anzahl der zurückgegebenen Zielgruppen einschränken können.](../images/ui/audience-composition/add-profile-limit.png)

## [!UICONTROL Aufspaltung] {#split-block}

Mit dem Blocktyp **[!UICONTROL Aufspaltung]** können Sie Ihre neue Zielgruppe in verschiedene Unterzielgruppen unterteilen. Sie können diese Zielgruppe entweder nach Prozentsatz oder nach einem Attribut aufteilen.

Um einen Block **[!UICONTROL Aufspaltung]** hinzuzufügen, wählen Sie das Symbol **+** und dann **[!UICONTROL Aufspaltung]** aus.

![Die Option „Aufspaltung“ ist ausgewählt.](../images/ui/audience-composition/add-split-block.png)

Bei der Aufspaltung der Audience können Sie sie entweder nach Prozentsatz aufteilen oder nach Attribut aufteilen.

### Aufspaltung nach Prozentsatz {#split-percentage}

Bei der Aufteilung nach Prozentsatz werden die Zielgruppen nach dem Zufallsprinzip auf Grundlage der Anzahl der angegebenen Pfade und Prozentsätze aufgeteilt.

Beispielsweise wären drei Pfade mit jeweils unterschiedlichen Prozentsätzen an Profilen möglich.

![Die Aufschlüsselung der Anzahl gespeicherter Zielgruppen und Prozentsätze wird angezeigt.](../images/ui/audience-composition/percentages.png)

### Aufspaltung nach Attribut {#split-attribute}

Bei der Aufteilung nach Attribut werden die Zielgruppen anhand der bereitgestellten Attribute aufgeteilt. Um das Attribut auszuwählen, nach dem aufgeteilt werden soll, wählen Sie den Block **[!UICONTROL Aufspaltung]** und dann das Symbol ![Filtern](../images/ui/audience-composition/filter-attribute.png) aus.

![Die Filterschaltfläche ist ausgewählt und zeigt an, wie nach Attribut gefiltert werden kann.](../images/ui/audience-composition/select-split-attribute.png)

Eine Liste der Profilattribute wird angezeigt. Wählen Sie den Attributtyp und dann **[!UICONTROL Auswählen]** aus, um ihn zu Ihrem Block hinzuzufügen.

![Eine Liste mit Attributen wird angezeigt.](../images/ui/audience-composition/select-attribute-exclude.png)

Nach Auswahl des Attributs können Sie festlegen, welche Profile zu welcher Unterzielgruppe gehören werden, indem Sie die Werte im Feld **[!UICONTROL Werte]** hinzufügen.

![Die Werte, nach denen die Attribute aufgeteilt werden sollen, werden hinzugefügt.](../images/ui/audience-composition/attribute-split-values.png)

Darüber hinaus können Sie den Umschalter **[!UICONTROL Andere Profile]** aktivieren, um eine Unterzielgruppe, die aus allen nicht ausgewählten Profilen besteht, zu erstellen.

![Der Umschalter „Andere Profile“ ist hervorgehoben.](../images/ui/audience-composition/split-other-profiles.png)

## Veröffentlichen der Zielgruppe

Nachdem Sie Ihre Zielgruppe erstellt haben, können Sie sie speichern und veröffentlichen, indem Sie **[!UICONTROL Veröffentlichen]** auswählen.

![Die Schaltfläche „Veröffentlichen“ ist hervorgehoben und zeigt, wie Sie Ihre Zielgruppe speichern und veröffentlichen.](../images/ui/audience-composition/publish.png)

Wenn bei der Erstellung der Zielgruppe Fehler auftreten, wird ein Warnhinweis angezeigt, über den Sie erfahren, wie Sie das Problem beheben können.

![Die Schaltfläche „Veröffentlichen“ ist hervorgehoben und zeigt, wie Sie Ihre Zielgruppe speichern und veröffentlichen.](../images/ui/audience-composition/audience-alert.png)

## Nächste Schritte

Zielgruppenkomposition bietet einen umfassenden Workflow, mit dem Sie Zielgruppen aus den verschiedenen Blocktypen erstellen können. Weitere Informationen zu anderen Teilen der Segmentierungs-Service-Benutzeroberfläche finden Sie im [Segmentierungs-Service-Benutzerhandbuch](./overview.md).
