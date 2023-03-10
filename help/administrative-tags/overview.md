---
keywords: Experience Platform; Startseite; beliebte Themen; einheitliche Tags; Tags;
title: Übersicht über Unified Tags (Beta)
description: Dieses Dokument enthält Informationen zu einheitlichen Tags in Adobe Experience Platform
source-git-commit: de258d0e9fe8304b239633c6901a62e3d7b9e214
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---

# Übersicht über Unified Tags (Beta)

>[!IMPORTANT]
>
>Einheitliche Tags befinden sich in der Beta-Phase. Wenn Sie Feedback hinterlassen möchten, wählen Sie dazu die Schaltfläche oben auf der Tag-Admin-Seite aus.

Tags sind eine Funktion von Adobe Experience Platform, mit der Administratoren Metadaten-Taxonomien verwalten können, um Geschäftsobjekte zu klassifizieren und so die Erkennung und Kategorisierung zu erleichtern. Tags sind Metadaten, die als Suchbegriffe betrachtet werden können, die an ein Segment, einen Datensatz, ein Journey oder andere Objekte angehängt werden können, um Suchen nach diesem Objekt und verwandten Objekten zu ermöglichen. Tags sind in zwei Typen klassifiziert: kategorisiert und nicht kategorisiert.

Um mehr Kontext bereitzustellen und den Zweck eines Tags zu definieren, organisieren Kategorien Tags in nützlichen Sets. Ein Administrator definiert, welche kategorisierten Tags Benutzern zum Hinzufügen zu Objekten zur Verfügung stehen. Neue Tags, die keine Kategorien enthalten, können in Workflows, in denen Tags angewendet werden, auch inline erstellt werden. Diese Tags werden im nicht kategorisierten Abschnitt des Tag-Bestands angezeigt. Tags können von Administratoren und Benutzern gleichermaßen angewendet werden, unabhängig davon, wer sie erstellt hat. Bei der Zuweisung zu einem Objekt, bei der Suche oder beim Filtern stehen alle Arten von Tags zur Auswahl.

## Terminologie von Tags

Tagging umfasst die folgenden Komponenten:

| Terminologie | Definition |
| --- | --- |
| Archiviert | Ein Status für ein Tag, der aktuelle Verknüpfungen mit Objekten behält, das Tag jedoch daran hindert, auf weitere Objekte angewendet zu werden.  Archivierte Tags werden in der Tag-Auswahl ausgeblendet. |
| Objekt | Ein Experience Cloud -Element, auf das ein Tag angewendet werden kann.  Beispiele: Segment, Journey, Datensatz. |
| Tag | Tags sind Metadaten und können als Keywords betrachtet werden, die an ein Segment, einen Datensatz, ein Journey oder andere Objekte angehängt werden können, um Suchen zu ermöglichen, die nach diesem Objekt und verwandten Objekten suchen. |
| Tag-Kategorie | Tag-Kategorien gruppieren Tags in aussagekräftigen Sätzen, um einen größeren Kontext zu bieten oder den Zweck des Tags zu beschreiben.  Administratoren verwalten Tag-Kategorien und Tags innerhalb von Kategorien. |
| Nicht kategorisiertes Tag | Ein neues Tag, das inline erstellt wird, in dem Tags angewendet werden. Diese Tags können von jedem Benutzer erstellt und angewendet werden, sind jedoch nicht an eine Kategorie gebunden.  Administratoren können diese Tags in eine Kategorie verschieben, um sie an anderen ähnlichen Tags auszurichten. |

## Tag-Inventar

Tag-Kategorie und Tag-Management mit dem Tag-Inventar sind in der Experience Platform und der Journey Optimizer-Navigation verfügbar. Änderungen an Tags im Inventar werden in allen Objekten übernommen, die Tags unterstützen. Alle Benutzer können auf den Tag-Bestand zugreifen und ihn durchsuchen. Das Tag-Management ist jedoch auf System- und Produktadministratoren beschränkt.

Der Tag-Bestand verfügt über drei Hierarchieebenen, mit denen Benutzer Tag-Kategorien, Tags innerhalb einer Kategorie und einzelne Tags verwalten können. Beim Verwalten eines einzelnen Tags können Benutzer jedes Objekt anzeigen und zu ihm navigieren, auf das dieses Tag derzeit angewendet wird.

### Tagkategorien

Kategorien gruppieren Tags in aussagekräftigen Sätzen, um einen größeren Kontext zu bieten oder den Zweck des Tags zu beschreiben. Bei jedem Tag mit einer Kategorie steht der Kategoriename gefolgt von einem Doppelpunkt vor dem Tag-Namen.

Die folgenden Aktionen sind bei Verwendung von Tag-Kategorien möglich:

* [Tag-Kategorie erstellen](./ui/tags-categories.md#create-tag-category)
* [Tag-Kategorie bearbeiten](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [Tag-Kategorie löschen](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### Verwalten von Tags innerhalb einer Kategorie

>[!NOTE]
>
>Um Tags für Experience Cloud verwalten zu können, müssen Sie Systemadministrator oder Produktadministrator für Adobe Experience Platform für Ihr Unternehmen sein, das über ein Abonnement für Experience Cloud verfügt.

Innerhalb einer Kategorie (oder der Standardgruppe &quot;Nicht kategorisiert&quot;) können Sie Tags erstellen und verwalten. Die folgenden Aktionen sind beim Verwalten von Tags möglich:

* [Erstellen von Tags](./ui/managing-tags.md#create-a-tag-create-tag)
* [Tag bearbeiten](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [Tag zwischen Kategorien verschieben](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [Tag archivieren](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [Archiviertes Tag wiederherstellen](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [Löschen von Tags](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [Anzeigen von getaggten Objekten](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
