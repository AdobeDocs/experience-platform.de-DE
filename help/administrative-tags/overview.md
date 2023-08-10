---
keywords: Experience Platform;Startseite;beliebte Themen;einheitliche Tags;Tags
title: Übersicht über Unified Tags
description: Dieses Dokument enthält Informationen zu einheitlichen Tags in Adobe Experience Platform
exl-id: a19e37c3-697a-4000-9cb8-d67478b47dc6
source-git-commit: 6977438d57dc8e1390812e58bf039ebc60cb830d
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 98%

---

# Übersicht über Unified Tags

Tags sind eine Funktion von Adobe Experience Platform, mit der Administrierende Metadaten-Taxonomien verwalten können, um Geschäftsobjekte zu klassifizieren und so die Erkennung und Kategorisierung zu erleichtern. Tags sind Metadaten, die als Suchbegriffe betrachtet werden können, die an ein Segment, einen Datensatz, eine Journey oder andere Objekte angehängt werden können, um Suchen nach diesem Objekt und verwandten Objekten zu ermöglichen. Tags werden in zwei Typen klassifiziert: kategorisiert und nicht kategorisiert.

Um mehr Kontext bereitzustellen und den Zweck eines Tags zu definieren, organisieren Kategorien Tags in nützlichen Sätzen. Administrierende definieren, welche kategorisierten Tags Benutzende zum Hinzufügen zu Objekten zur Verfügung stehen. Neue Tags, die keine Kategorien enthalten, können in Workflows, in denen Tags angewendet werden, auch inline erstellt werden. Diese Tags werden im nicht kategorisierten Abschnitt des Tag-Bestands angezeigt. Tags können von Administrierenden und Benutzenden gleichermaßen angewendet werden, unabhängig davon, wer sie erstellt hat. Bei der Zuweisung zu einem Objekt, bei der Suche oder beim Filtern stehen alle Arten von Tags zur Auswahl.

## Terminologie von Tags

Tagging umfasst die folgenden Komponenten:

| Terminologie | Definition |
| --- | --- |
| Archiviert | Ein Status für ein Tag, der aktuelle Verknüpfungen mit Objekten behält, aber die Anwendung des Tags auf weitere Objekte einschränkt.  Archivierte Tags werden in der Tag-Auswahl ausgeblendet. |
| Objekt | Ein Experience Cloud-Element, auf das ein Tag angewendet werden kann.  Beispiele: Segment, Journey, Datensatz. |
| Tag | Tags sind Metadaten und können als Keywords betrachtet werden, die an ein Segment, einen Datensatz, eine Journey oder andere Objekte angehängt werden können, um Suchen zu ermöglichen, die nach diesem Objekt und verwandten Objekten suchen. |
| Tag-Kategorie | Tag-Kategorien gruppieren Tags in aussagekräftigen Sätzen, um einen größeren Kontext zu bieten oder den Zweck des Tags zu beschreiben.  Administrierende verwalten Tag-Kategorien und Tags innerhalb von Kategorien. |
| Nicht kategorisiertes Tag | Ein neues Tag, das inline erstellt wird, in dem Tags angewendet werden. Diese Tags können von allen Benutzenden erstellt und angewendet werden, sind jedoch nicht an eine Kategorie gebunden.  Administrierende können diese Tags in eine Kategorie verschieben, um sie an anderen ähnlichen Tags auszurichten. |

## Tag-Inventar

Tag-Kategorie und Tag-Management mit dem Tag-Inventar sind in der Experience Platform und der Journey Optimizer-Navigation verfügbar. Änderungen an Tags im Inventar werden in allen Objekten übernommen, die Tags unterstützen. Alle Benutzenden können auf das Tag-Inventar zugreifen und es durchsuchen. Das Tag-Management ist jedoch auf System- und Produktadministrierende beschränkt.

Der Tag-Bestand verfügt über drei Hierarchieebenen, mit denen Benutzende Tag-Kategorien, Tags innerhalb einer Kategorie und einzelne Tags verwalten können. Beim Verwalten eines einzelnen Tags können Benutzende jedes Objekt anzeigen und zu ihm navigieren, auf das dieses Tag derzeit angewendet wird.

### Tag-Kategorien

Kategorien gruppieren Tags in aussagekräftigen Sätzen, um einen größeren Kontext zu bieten oder den Zweck des Tags zu beschreiben. Bei jedem Tag mit einer Kategorie steht der Kategoriename gefolgt von einem Doppelpunkt vor dem Tag-Namen.

Die folgenden Aktionen sind bei Verwendung von Tag-Kategorien möglich:

* [Erstellen von Tag-Kategorien](./ui/tags-categories.md#create-tag-category)
* [Bearbeiten von Tag-Kategorien](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [Löschen von Tag-Kategorien](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### Verwalten von Tags innerhalb einer Kategorie

>[!NOTE]
>
>Um Tags für Experience Cloud verwalten zu können, müssen Sie System- oder Produktadministratorrechte für Adobe Experience Platform für Ihr Unternehmen haben, das über ein Abonnement für Experience Cloud verfügt.

Innerhalb einer Kategorie (oder der Standardgruppe „Nicht kategorisiert“) können Sie Tags erstellen und verwalten. Die folgenden Aktionen sind beim Verwalten von Tags möglich:

* [Erstellen von Tags](./ui/managing-tags.md#create-a-tag-create-tag)
* [Bearbeiten eines Tags](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [Verschieben eines Tags zwischen Kategorien](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [Archivieren eines Tags](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [Wiederherstellen eines archivierten Tags](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [Löschen von Tags](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [Anzeigen von getaggten Objekten](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
