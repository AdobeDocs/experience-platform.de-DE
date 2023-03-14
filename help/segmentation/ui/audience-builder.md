---
keywords: Experience Platform;Startseite;beliebte Themen;Segmentation Service;Segmentierung;segmentation service;Benutzerhandbuch;UI-Handbuch;Handbuch zur Zielgruppen-Benutzeroberfläche;Audience Builder;Zielgruppen;Zielgruppen;Handbuch zur Zielgruppen-Benutzeroberfläche;
solution: Experience Platform
title: Handbuch zur Zielgruppen-Benutzeroberfläche
description: Audience Builder in der Adobe Experience Platform-Benutzeroberfläche bietet einen umfassenden Arbeitsbereich, in dem Sie mit Profildatenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Zielgruppen für Ihre Organisation.
hide: true
hidefromtoc: true
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 100%

---

# Handbuch zur Benutzeroberfläche von Audience Builder

>[!IMPORTANT]
>
>Audience Builder befindet sich derzeit in der Beta-Phase und steht nicht allen Benutzenden zur Verfügung. Dokumentation und Funktionalitäten können sich ändern.

Audience Builder bietet einen Arbeitsbereich zum Erstellen und Bearbeiten von Zielgruppen mithilfe von Blöcken, die zur Darstellung verschiedener Aktionen verwendet werden.

![Die Audience Builder-Benutzeroberfläche.](../images/ui/audience-builder/audience-builder.png)

Die Arbeitsfläche für die Zielgruppenkomposition besteht aus fünf verschiedenen Blocktypen: **[[!UICONTROL Zielgruppe]](#audience-block)**, **[[!UICONTROL Ausschließen]](#exclude-block)**, **[[!UICONTROL Zusammenführen]](#join-block)**, **[[!UICONTROL Rang]](#rank-block)** und **[[!UICONTROL Aufspaltung]](#split-block)**.

## [!UICONTROL Zielgruppe] {#audience-block}

Mit dem Block **[!UICONTROL Zielgruppe]** können Sie die Unterzielgruppen hinzufügen, aus denen Sie Ihre neue größere Zielgruppe erstellen möchten. Standardmäßig ist ein **[!UICONTROL Zielgruppen]**-Block oben auf der Arbeitsfläche für die Komposition enthalten.

Wenn Sie den **[!UICONTROL Zielgruppen]**-Block auswählen, werden in der rechten Leiste Steuerelemente zum Kennzeichnen und Hinzufügen von Zielgruppen zum Block angezeigt.

![Details zum Zielgruppen-Block werden angezeigt.](../images/ui/audience-builder/select-audience.png)

Nach Auswahl von **[!UICONTROL Zielgruppe hinzufügen]** wird eine Liste von Zielgruppen angezeigt. Wählen Sie die Zielgruppe aus, die Sie einbeziehen möchten, und dann **[!UICONTROL Hinzufügen]**, um sie an Ihren Zielgruppen-Block anzuhängen.

![Eine Liste von Zielgruppen wird angezeigt. In diesem Dialogfeld können Sie auswählen, welche Zielgruppe Sie hinzufügen möchten.](../images/ui/audience-builder/select-audience.png)

Ihre ausgewählten Zielgruppen werden jetzt in der rechten Leiste angezeigt, wenn der Block **[!UICONTROL Zielgruppe]** aktiviert ist. Von hier aus können Sie den Zusammenführungstyp der kombinierten Zielgruppen ändern.

![Die möglichen Zusammenführungstypen für die Zielgruppen sind hervorgehoben.](../images/ui/audience-builder/merge-types.png)

| Zusammenführungstyp | Beschreibung |
| ---------- | ----------- |
| [!UICONTROL Vereinigung] | Die Zielgruppen werden zu einer Zielgruppe zusammengefasst. Dies entspricht einem OR-Vorgang. |
| [!UICONTROL Schnittmenge] | Die Zielgruppen werden nur mit den Zielgruppen kombiniert, die in **allen** freigegeben sind und hinzugefügt werden. Dies entspricht einem AND-Vorgang. |
| [!UICONTROL Ausschließen von Überschneidungen] | Die Zielgruppen werden kombiniert, wobei nur die Zielgruppen hinzugefügt werden, die zu genau **einer, aber nicht zu allen** gehören. Dies entspricht einem XOR-Vorgang. |

## [!UICONTROL Ausschließen] {#exclude-block}

Mit dem Blocktyp **[!UICONTROL Ausschließen]** können Sie bestimmte Unterzielgruppen oder Attribute aus Ihrer neuen größeren Zielgruppe ausschließen.

Um einen Block **[!UICONTROL Ausschließen]** hinzuzufügen, wählen Sie das Symbol **+** und dann **[!UICONTROL Ausschließen]** aus.

![Die Option „Ausschließen“ ist ausgewählt.](../images/ui/audience-builder/add-exclude-block.png)

Der Block **[!UICONTROL Ausschließen]** wird hinzugefügt. Wenn dieser Block ausgewählt ist, werden Details zum Ausschluss in der rechten Leiste angezeigt. Dazu gehören die Kennzeichnung und der Ausschlusstyp des Blocks. Sie können [nach Zielgruppe](#exclude-audience) oder [nach Attribut](#exclude-attribute) ausschließen.

![Der Block „Ausschließen“, in dem die beiden verfügbaren Ausschlusstypen hervorgehoben sind.](../images/ui/audience-builder/exclude.png)

### Ausschließen nach Zielgruppe {#exclude-audience}

Wenn Sie nach Zielgruppe ausschließen, können Sie durch Auswahl von **[!UICONTROL Zielgruppe hinzufügen]** auswählen, welche Zielgruppen ausgeschlossen werden sollen.

![Die Schaltfläche „Zielgruppe hinzufügen“ ist ausgewählt, über die Sie auswählen können, welche Zielgruppe Sie ausschließen möchten.](../images/ui/audience-builder/add-excluded-audience.png)

Eine Liste von Zielgruppen wird angezeigt. Wählen Sie **[!UICONTROL Hinzufügen]** aus, um die Zielgruppen, die ausgeschlossen werden sollen, Ihrem Ausschlussblock hinzuzufügen.

![Eine Liste von Zielgruppen wird angezeigt. In diesem Dialogfeld können Sie auswählen, welche Zielgruppe Sie hinzufügen möchten.](../images/ui/audience-builder/select-audience.png)

### Ausschließen nach Attribut {#exclude-attribute}

Wenn Sie nach Attribut ausschließen, können Sie durch Auswahl des Symbols ![Filtern](../images/ui/audience-builder/filter-attribute.png) innerhalb des Abschnitts **[!UICONTROL Ausschlussregel]** festlegen, welche Attribute ausgeschlossen werden sollen.

![Der Abschnitt „Attribut“ wird hervorgehoben und zeigt an, wo das auszuschließende Attribut ausgewählt werden soll.](../images/ui/audience-builder/exclude-attribute.png)

Eine Liste der Profilattribute wird angezeigt. Wählen Sie den Attributtyp aus, den Sie ausschließen möchten, und dann **[!UICONTROL Auswählen]**, um diese Attribute zu Ihrem Ausschlussblock hinzuzufügen.

![Eine Liste mit Attributen wird angezeigt.](../images/ui/audience-builder/select-attribute.png)

## [!UICONTROL Zusammenführen] {#join-block}

Mit dem Blocktyp **[!UICONTROL Zusammenführen]** können Sie externe Zielgruppen aus Datensätzen hinzufügen, die noch nicht von Adobe Experience Platform verarbeitet wurden.

Um einen Block **[!UICONTROL Zusammenführen]** hinzuzufügen, wählen Sie das Symbol **+** und dann **[!UICONTROL Zusammenführen]** aus.

![Die Option „Zusammenführen“ ist ausgewählt.](../images/ui/audience-builder/add-join-block.png)

Wenn Sie den Block auswählen, werden in der rechten Leiste Details zur Zusammenführung angezeigt, einschließlich der Kennzeichnung des Blocks und der Option, Zielgruppen zum Anreicherungsdatensatz hinzuzufügen.

![Der Block „Zusammenführen“ ist hervorgehoben, einschließlich entsprechender Details.](../images/ui/audience-builder/join.png)

Nach Auswahl von **[!UICONTROL Zielgruppe hinzufügen]** wird eine Liste von Zielgruppen angezeigt. Wählen Sie die Zielgruppen aus, die Sie einbeziehen möchten, und dann **[!UICONTROL Hinzufügen]**, um sie zum Block „Zusammenführen“ hinzuzufügen.

![Eine Liste von Zielgruppen wird angezeigt. In diesem Dialogfeld können Sie auswählen, welche Zielgruppe Sie hinzufügen möchten.](../images/ui/audience-builder/select-audience.png)

Ihre ausgewählten Zielgruppen werden jetzt in der rechten Leiste angezeigt, wenn der Block **[!UICONTROL Zusammenführen]** aktiviert ist.

![Die Zielgruppen, die als Teil der Zusammenführung hinzugefügt wurden, werden angezeigt.](../images/ui/audience-builder/selected-audiences.png)

## [!UICONTROL Rang] {#rank-block}

Mit dem Blocktyp **[!UICONTROL Rang]** können Sie die Zielgruppen vor der Veröffentlichung Ihrer neuen Zielgruppe nach Rang ordnen und sortieren.

Um einen Block **[!UICONTROL Rang]** hinzuzufügen, wählen Sie das Symbol **+** und dann **[!UICONTROL Rang]** aus.

![Die Option „Rang“ ist ausgewählt.](../images/ui/audience-builder/add-rank-block.png)

Bei der Auswahl des Blocks werden Details zum Rang in der rechten Leiste angezeigt, einschließlich der Kennzeichnung des Blocks, des nach Rang zu ordnenden Attributs, der Rangreihenfolge und eines Umschalters zur Begrenzung der Anzahl der nach Rang zu ordnenden Profile.

![Der Block „Rang“ ist mit zugehörigen Details hervorgehoben.](../images/ui/audience-builder/rank.png)

Um festzulegen, nach welchem Attribut die Zielgruppen geordnet werden sollen, wählen Sie das Symbol ![Filtern](../images/ui/audience-builder/filter-attribute.png) aus.

![Das Filtersymbol ist hervorgehoben und zeigt an, welche Optionen für den Zugriff auf den Bildschirm zur Profilattributauswahl ausgewählt werden sollen.](../images/ui/audience-builder/select-rank-attribute.png)

Eine Liste der Profilattribute wird angezeigt. In diesem Popup können Sie den Attributtyp auswählen, nach dem Sie Ihre Zielgruppe ordnen möchten. Wählen Sie **[!UICONTROL Auswählen]** aus, um ihn Ihrem Block „Rang“ hinzuzufügen. Beachten Sie, dass das ausgewählte Attribut **nur** vom Typ `int` sein kann.

![Eine Liste mit Attributen wird angezeigt.](../images/ui/audience-builder/select-attribute.png)

Nach Auswahl des Attributs können Sie die Reihenfolge auswählen, nach der geordnet werden soll. Dies geschieht entweder in aufsteigender (von niedrigster zu höchster) oder in absteigender (von höchster zu niedrigster) Reihenfolge.

Darüber hinaus können Sie die Anzahl der zurückgegebenen Zielgruppen einschränken, indem Sie den Umschalter **[!UICONTROL Profil-Limit hinzufügen]** aktivieren. Wenn dieser Umschalter aktiviert ist, können Sie die maximale Anzahl von Zielgruppen festlegen, die innerhalb des Felds **[!UICONTROL Enthaltene Profile]** zurückgegeben wird.

![Der Umschalter „Profil-Limit hinzufügen“ ist hervorgehoben, sodass Sie die Anzahl der zurückgegebenen Zielgruppen einschränken können.](../images/ui/audience-builder/add-profile-limit.png)

## [!UICONTROL Aufspaltung] {#split-block}

Mit dem Blocktyp **[!UICONTROL Aufspaltung]** können Sie Ihre neue Zielgruppe in verschiedene Unterzielgruppen unterteilen. Sie können diese Zielgruppe entweder nach Prozentsatz oder nach einem Attribut aufteilen.

Um einen Block **[!UICONTROL Aufspaltung]** hinzuzufügen, wählen Sie das Symbol **+** und dann **[!UICONTROL Aufspaltung]** aus.

![Die Option „Aufspaltung“ ist ausgewählt.](../images/ui/audience-builder/add-split-block.png)

### Aufspaltung nach Prozentsatz {#split-percentage}

Bei der Aufteilung nach Prozentsatz werden die Zielgruppen nach dem Zufallsprinzip auf Grundlage der Anzahl der angegebenen Pfade und Prozentsätze aufgeteilt.

Beispielsweise wären drei Pfade mit jeweils unterschiedlichen Prozentsätzen an Profilen möglich.

![Die Aufschlüsselung der Anzahl gespeicherter Zielgruppen und Prozentsätze wird angezeigt.](../images/ui/audience-builder/percentages.png)

Darüber hinaus können Sie eine der aufgeteilten Zielgruppen als Kontrollgruppe markieren.

![Der Umschalter für Kontrollgruppen ist aktiviert. Auf diese Weise können Sie eine der aufgeteilten Zielgruppen als Kontrollgruppe markieren.](../images/ui/audience-builder/control-group.png)

### Aufspaltung nach Attribut {#split-attribute}

Bei der Aufteilung nach Attribut werden die Zielgruppen anhand der bereitgestellten Attribute aufgeteilt. Um das Attribut auszuwählen, nach dem aufgeteilt werden soll, wählen Sie den Block **[!UICONTROL Aufspaltung]** und dann das Symbol ![Filtern](../images/ui/audience-builder/filter-attribute.png) aus.

![Die Filterschaltfläche ist ausgewählt und zeigt an, wie nach Attribut gefiltert werden kann.](../images/ui/audience-builder/select-attribute-split.png)

Eine Liste der Profilattribute wird angezeigt. Wählen Sie den Attributtyp und dann **[!UICONTROL Auswählen]** aus, um ihn zu Ihrem Block hinzuzufügen.

![Eine Liste mit Attributen wird angezeigt.](../images/ui/audience-builder/select-attribute.png)

Nach Auswahl des Attributs können Sie festlegen, welche Profile zu welcher Unterzielgruppe gehören werden, indem Sie die Werte im Feld **[!UICONTROL Werte]** hinzufügen.

![Die Werte, nach denen die Attribute aufgeteilt werden sollen, werden hinzugefügt.](../images/ui/audience-builder/attribute-split-values.png)

Darüber hinaus können Sie den Umschalter **[!UICONTROL Andere Profile]** aktivieren, um eine Unterzielgruppe, die aus allen nicht ausgewählten Profilen besteht, zu erstellen.

![Der Umschalter „Andere Profile“ ist hervorgehoben.](../images/ui/audience-builder/attribute-split-other-profiles.png)

## Veröffentlichen der Zielgruppe

Nachdem Sie Ihre Zielgruppe erstellt haben, können Sie sie speichern und veröffentlichen, indem Sie **[!UICONTROL Veröffentlichen]** auswählen.

![Die Schaltfläche „Veröffentlichen“ ist hervorgehoben und zeigt, wie Sie Ihre Zielgruppe speichern und veröffentlichen.](../images/ui/audience-builder/publish-audience.png)

Wenn bei der Erstellung der Zielgruppe Fehler auftreten, wird ein Warnhinweis angezeigt, über den Sie erfahren, wie Sie das Problem beheben können.

![Die Schaltfläche „Veröffentlichen“ ist hervorgehoben und zeigt, wie Sie Ihre Zielgruppe speichern und veröffentlichen.](../images/ui/audience-builder/audience-alert.png)

## Nächste Schritte

Audience Builder bietet einen umfassenden Workflow, mit dem Sie Zielgruppen der verschiedenen Blocktypen erstellen können. Weitere Informationen zu anderen Teilen der Segmentierungs-Service-Benutzeroberfläche finden Sie im [Segmentierungs-Service-Benutzerhandbuch](./overview.md).
