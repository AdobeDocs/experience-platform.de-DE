---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierungsdienst; Segmentierungsdienst; Segmentierungsdienst; Benutzerhandbuch; Handbuch zu Zielgruppen; Benutzerhandbuch; Audience Builder; Zielgruppe; Zielgruppen; Benutzerhandbuch; Handbuch zu Zielgruppen;
solution: Experience Platform
title: Handbuch zur Benutzeroberfläche von Zielgruppen
topic-legacy: ui guide
description: Der Audience Builder in der Adobe Experience Platform-Benutzeroberfläche bietet einen umfassenden Arbeitsbereich, in dem Sie mit Profildatenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Zielgruppen für Ihre Organisation.
hide: true
hidefromtoc: true
source-git-commit: f71d49b576059e687c337cbacd6dd3d525e97834
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 1%

---

# Handbuch zur Benutzeroberfläche von Audience Builder

>[!IMPORTANT]
>
>Audience Builder befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.

Audience Builder bietet einen Arbeitsbereich zum Erstellen und Bearbeiten von Zielgruppen mithilfe von Bausteinen, die zur Darstellung verschiedener Aktionen verwendet werden.

![Die Audience Builder-Benutzeroberfläche.](../images/ui/audience-builder/audience-builder.png)

Die Arbeitsfläche für die Zielgruppenzusammensetzung besteht aus fünf verschiedenen Baustypen: **[[!UICONTROL Zielgruppe]](#audience-block)**, **[[!UICONTROL Ausschließen]](#exclude-block)**, **[[!UICONTROL Mitglied werden]](#join-block)**, **[[!UICONTROL Rang]](#rank-block)** und **[[!UICONTROL Aufspaltung]](#split-block)**.

## [!UICONTROL Zielgruppe ] {#audience-block}

Die **[!UICONTROL Zielgruppe]** -Blocktyp können Sie die Unterzielgruppen hinzufügen, aus denen Sie Ihre neue größere Zielgruppe erstellen möchten. Standardmäßig wird ein **[!UICONTROL Zielgruppe]** -Block ist oben auf der Arbeitsfläche der Komposition enthalten.

Wenn Sie die **[!UICONTROL Zielgruppe]** -Block, zeigt die rechte Leiste Steuerelemente für die Beschriftung und das Hinzufügen von Zielgruppen zum Baustein an.

![Die Details des Zielgruppenblocks werden angezeigt.](../images/ui/audience-builder/select-audience.png)

Nach Auswahl **[!UICONTROL Zielgruppe hinzufügen]**, wird eine Liste von Zielgruppen angezeigt. Wählen Sie die Zielgruppen aus, die Sie einbeziehen möchten, gefolgt von **[!UICONTROL Hinzufügen]** , um sie an Ihren Audience-Block anzuhängen.

![Eine Liste der Zielgruppen wird angezeigt. In diesem Dialogfeld können Sie auswählen, welche Audience Sie hinzufügen möchten.](../images/ui/audience-builder/select-audience.png)

Ihre ausgewählten Zielgruppen werden jetzt in der rechten Leiste angezeigt, wenn die **[!UICONTROL Zielgruppe]** aktiviert ist. Von hier aus können Sie den Zusammenführungstyp der kombinierten Zielgruppen ändern.

![Die möglichen Zusammenführungstypen für die Zielgruppen werden hervorgehoben.](../images/ui/audience-builder/merge-types.png)

| Zusammenführungstyp | Beschreibung |
| ---------- | ----------- |
| [!UICONTROL Vereinigung] | Die Zielgruppen werden zu einer Zielgruppe zusammengefasst. Dies entspricht einem ODER-Vorgang. |
| [!UICONTROL Schnittmenge] | Die Zielgruppen werden mit den Zielgruppen kombiniert, die in freigegeben sind **all** hinzugefügt werden. Dies entspricht einem AND-Vorgang. |
| [!UICONTROL Überschneidung ausschließen] | Die Zielgruppen werden mit den Zielgruppen kombiniert, die in freigegeben sind **einer, aber nicht alle** hinzugefügt werden. Dies entspricht einem XOR-Vorgang. |

## [!UICONTROL Ausschließen] {#exclude-block}

Die **[!UICONTROL Ausschließen]** Mit dem Blocktyp können Sie bestimmte Unterzielgruppen oder Attribute aus Ihrer neuen größeren Zielgruppe ausschließen.

So fügen Sie eine **[!UICONTROL Ausschließen]** Block, wählen Sie die **+** Symbol, gefolgt von **[!UICONTROL Ausschließen]**.

![Die Option Ausschließen ist ausgewählt.](../images/ui/audience-builder/add-exclude-block.png)

Die **[!UICONTROL Ausschließen]** hinzugefügt. Wenn dieser Block ausgewählt ist, werden Details zum Ausschluss in der rechten Leiste angezeigt. Dazu gehören der Titel und der Ausschlusstyp des Blocks. Sie können [nach Zielgruppe](#exclude-audience) oder [nach Attribut](#exclude-attribute).

![den Block Ausschließen , in dem die beiden verfügbaren Ausschlusstypen hervorgehoben werden.](../images/ui/audience-builder/exclude.png)

### Nach Zielgruppe ausschließen {#exclude-audience}

Wenn Sie die Zielgruppe ausschließen, können Sie durch Auswahl von **[!UICONTROL Zielgruppe hinzufügen]**.

![Die Schaltfläche Audience hinzufügen ist ausgewählt, über die Sie auswählen können, welche Audience Sie ausschließen möchten.](../images/ui/audience-builder/add-excluded-audience.png)

Eine Liste der Zielgruppen wird angezeigt. Auswählen **[!UICONTROL Hinzufügen]** , um die Zielgruppen, die Sie ausschließen möchten, Ihrem Ausschlussblock hinzuzufügen.

![Eine Liste der Zielgruppen wird angezeigt. In diesem Dialogfeld können Sie auswählen, welche Audience Sie hinzufügen möchten.](../images/ui/audience-builder/select-audience.png)

### Nach Attribut ausschließen {#exclude-attribute}

Wenn Sie die Attribute nach Attribut ausschließen, können Sie durch Auswahl der ![filter](../images/ui/audience-builder/filter-attribute.png) innerhalb des **[!UICONTROL Ausschlussregel]** Abschnitt.

![Der Abschnitt &quot;Attribut&quot;wird hervorgehoben und zeigt an, wo das auszuschließende Attribut ausgewählt werden soll.](../images/ui/audience-builder/exclude-attribute.png)

Eine Liste der Profilattribute wird angezeigt. Wählen Sie den Attributtyp aus, den Sie ausschließen möchten, gefolgt von **[!UICONTROL Auswählen]** , um sie zu Ihrem Ausschlussblock hinzuzufügen.

![Eine Liste mit Attributen wird angezeigt.](../images/ui/audience-builder/select-attribute.png)

## [!UICONTROL Join] {#join-block}

Die **[!UICONTROL Mitglied werden]** Mit dem Blocktyp können Sie externe Zielgruppen aus Datensätzen hinzufügen, die noch nicht von Adobe Experience Platform verarbeitet wurden.

So fügen Sie eine **[!UICONTROL Mitglied werden]** Block, wählen Sie die **+** Symbol, gefolgt von **[!UICONTROL Mitglied werden]**.

![Die Option Join ist ausgewählt.](../images/ui/audience-builder/add-join-block.png)

Wenn Sie den Baustein auswählen, werden in der rechten Leiste Details zum Join angezeigt, einschließlich des Titels des Bausteins und der Option, Zielgruppen zum Anreicherungsdatensatz hinzuzufügen.

![Der Join-Block einschließlich Details zum Join-Block wird hervorgehoben.](../images/ui/audience-builder/join.png)

Nach Auswahl **[!UICONTROL Zielgruppe hinzufügen]**, wird eine Liste von Zielgruppen angezeigt. Wählen Sie die Zielgruppen aus, die Sie einbeziehen möchten, gefolgt von **[!UICONTROL Hinzufügen]** , um sie Ihrem Join-Block hinzuzufügen.

![Eine Liste der Zielgruppen wird angezeigt. In diesem Dialogfeld können Sie auswählen, welche Audience Sie hinzufügen möchten.](../images/ui/audience-builder/select-audience.png)

Ihre ausgewählten Zielgruppen werden jetzt in der rechten Leiste angezeigt, wenn die **[!UICONTROL Mitglied werden]** aktiviert ist.

![Die Zielgruppen, die als Teil des Joins hinzugefügt wurden, werden angezeigt.](../images/ui/audience-builder/selected-audiences.png)

## [!UICONTROL Rang] {#rank-block}

Die **[!UICONTROL Rang]** Mit dem Blocktyp können Sie die Zielgruppen vor der Veröffentlichung Ihrer neuen Zielgruppe nach Rang ordnen und sortieren.

So fügen Sie eine **[!UICONTROL Rang]** Block, wählen Sie die **+** Symbol, gefolgt von **[!UICONTROL Rang]**.

![Die Option Rang ist ausgewählt.](../images/ui/audience-builder/add-rank-block.png)

Bei der Auswahl des Bausteins werden Details zum Rang in der rechten Leiste angezeigt, einschließlich des Titels des Bausteins, des einzustufenden Attributs, der Rangreihenfolge und eines Umschalters zur Begrenzung der Anzahl der Profile auf den Rang.

![Der Rangblock sowie die Details des Rangblocks werden hervorgehoben.](../images/ui/audience-builder/rank.png)

Um festzulegen, nach welchem Attribut die Zielgruppen sortiert werden sollen, wählen Sie die ![filter](../images/ui/audience-builder/filter-attribute.png) Symbol.

![Das Filtersymbol wird hervorgehoben und zeigt an, welche Optionen für den Zugriff auf den Bildschirm zur Profilattributauswahl ausgewählt werden sollen.](../images/ui/audience-builder/select-rank-attribute.png)

Eine Liste der Profilattribute wird angezeigt. In diesem Popup-Fenster können Sie den Attributtyp auswählen, nach dem Sie Ihre Zielgruppe ordnen möchten. Auswählen **[!UICONTROL Auswählen]** , um ihn zu Ihrem Rangblock hinzuzufügen. Beachten Sie, dass das ausgewählte Attribut **only** vom Typ `int`.

![Eine Liste mit Attributen wird angezeigt.](../images/ui/audience-builder/select-attribute.png)

Nach Auswahl des Attributs können Sie die Reihenfolge auswählen, nach der es sortiert werden soll. Dies geschieht entweder in aufsteigender (von niedrigster zu höchster) oder in absteigender (von höchster zu niedrigster) Reihenfolge.

Darüber hinaus können Sie die Anzahl der zurückgegebenen Zielgruppen einschränken, indem Sie die **[!UICONTROL Profilbegrenzung hinzufügen]** umschalten. Wenn dieser Umschalter aktiviert ist, können Sie die maximale Anzahl von Zielgruppen festlegen, die innerhalb der **[!UICONTROL Enthaltene Profile]** -Feld.

![Der Umschalter Profilbeschränkung hinzufügen ist hervorgehoben, sodass Sie die Anzahl der zurückgegebenen Zielgruppen einschränken können.](../images/ui/audience-builder/add-profile-limit.png)

## [!UICONTROL Teilen] {#split-block}

Die **[!UICONTROL Aufspaltung]** -Blocktyp ermöglicht es Ihnen, Ihre neue Zielgruppe in verschiedene Unterzielgruppen zu unterteilen. Sie können diese Zielgruppe entweder nach Prozentsatz oder Attribut aufteilen.

So fügen Sie eine **[!UICONTROL Aufspaltung]** Block, wählen Sie die **+** Symbol, gefolgt von **[!UICONTROL Aufspaltung]**.

![Die Option Aufspaltung ist ausgewählt.](../images/ui/audience-builder/add-split-block.png)

### Aufspaltung nach Prozentsatz {#split-percentage}

Bei der Aufteilung nach Prozentsatz werden die Zielgruppen nach dem Zufallsprinzip auf der Grundlage der Anzahl der bereitgestellten Pfade und Prozentsätze aufgeteilt.

Sie könnten beispielsweise drei Pfade mit jeweils unterschiedlichem Prozentsatz an Profilen haben.

![Die Aufschlüsselung der Anzahl gespeicherter Zielgruppen und Prozentsätze wird angezeigt.](../images/ui/audience-builder/percentages.png)

Darüber hinaus können Sie eine der aufgeteilten Zielgruppen zur Kontrollgruppe markieren.

![Der Umschalter für Kontrollgruppen ist aktiviert. Auf diese Weise können Sie eine der aufgeteilten Zielgruppen als Kontrollgruppe markieren.](../images/ui/audience-builder/control-group.png)

### Aufspaltung nach Attribut {#split-attribute}

Bei der Aufteilung nach Attribut werden die Zielgruppen anhand der bereitgestellten Attribute aufgeteilt. Um das Attribut auszuwählen, nach dem aufgeteilt werden soll, wählen Sie die **[!UICONTROL Aufspaltung]** Block, gefolgt von der ![filter](../images/ui/audience-builder/filter-attribute.png) Symbol.

![Die Filterschaltfläche ist ausgewählt und zeigt an, wie nach Attribut gefiltert werden kann.](../images/ui/audience-builder/select-attribute-split.png)

Eine Liste der Profilattribute wird angezeigt. Wählen Sie den Attributtyp gefolgt von **[!UICONTROL Auswählen]** , um ihn zu Ihrem Baustein hinzuzufügen.

![Eine Liste mit Attributen wird angezeigt.](../images/ui/audience-builder/select-attribute.png)

Nach Auswahl des Attributs können Sie auswählen, welche Profile zu welcher Unterzielgruppe gehören, indem Sie die Werte in der **[!UICONTROL Werte]** -Feld.

![Die Werte, nach denen die Attribute aufgeteilt werden sollen, werden hinzugefügt.](../images/ui/audience-builder/attribute-split-values.png)

Darüber hinaus können Sie die **[!UICONTROL Andere Profile]** Umschalten auf die Erstellung einer Unter-Audience, die aus allen nicht ausgewählten Profilen besteht.

![Der Umschalter Andere Profile wird hervorgehoben.](../images/ui/audience-builder/attribute-split-other-profiles.png)

## Veröffentlichen der Audience

Nachdem Sie Ihre Audience erstellt haben, können Sie sie speichern und veröffentlichen, indem Sie **[!UICONTROL Veröffentlichen]**.

![Die Schaltfläche Veröffentlichen ist hervorgehoben und zeigt, wie Sie Ihre Audience speichern und veröffentlichen können.](../images/ui/audience-builder/publish-audience.png)

Wenn bei der Erstellung der Audience Fehler auftreten, wird ein Warnhinweis angezeigt, in dem Sie erfahren, wie Sie das Problem beheben können.

![Die Schaltfläche Veröffentlichen ist hervorgehoben und zeigt, wie Sie Ihre Audience speichern und veröffentlichen können.](../images/ui/audience-builder/audience-alert.png)

## Nächste Schritte

Der Audience Builder bietet einen umfassenden Workflow, mit dem Sie Audiences der verschiedenen Blocktypen erstellen können. Weitere Informationen zu anderen Teilen der Segmentation Service-Benutzeroberfläche finden Sie in der [Benutzerhandbuch zum Segmentierungsdienst](./overview.md).