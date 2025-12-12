---
title: Bibliotheken
description: Machen Sie sich mit dem Konzept und der Funktionsweise von Tag-Bibliotheken in Adobe Experience Platform vertraut.
exl-id: 4d6f86e6-5684-4635-aaf1-87ba10cd7d94
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 97%

---

# Bibliotheken

Eine Bibliothek ist eine Reihe von Anweisungen, die spezifizieren, wie Erweiterungen, Datenelemente und Regeln nach deren Bereitstellung miteinander interagieren. Beim Erstellen einer Bibliothek geben Sie die Änderungen an, die Sie in Ihrer Bibliothek vornehmen möchten. Zum Zeitpunkt der Erstellung werden diese Änderungen mit allen Elementen kombiniert, die in früheren Bibliotheken übermittelt, genehmigt oder veröffentlicht wurden.

Bibliotheken beinhalten das Hinzufügen oder Entfernen von:

* Regeln
* Elementen
* Erweiterungskonfiguration

Bibliotheken müssen einer Umgebung zugewiesen werden, bevor sie in einen Build kompiliert werden können. Bibliotheken werden als Ganzes genehmigt oder abgelehnt. Sie können einzelne Elemente in einer Bibliothek nicht genehmigen oder ablehnen. Eine Bibliothek wechselt zwischen verschiedenen Umgebungen, während sie den Workflow zur Veröffentlichung durchläuft.

## eine Bibliothek erstellen {#create-a-library}

Um eine Bibliothek zu erstellen, führen Sie die folgenden Schritte aus.

1. Öffnen Sie die Registerkarte [!UICONTROL Publishing].

   Auf der Seite [!UICONTROL Publishing] werden die Entwicklungsbibliotheken aufgelistet und die Möglichkeiten bereitgestellt, sie zur Genehmigung einzureichen, zum Staging zu verschieben oder in der Produktion zu veröffentlichen.

1. Wählen Sie **[!UICONTROL Add New Library]** aus.

   ![](../../images/library-create.jpg)

1. Benennen Sie die Bibliothek.
1. Weisen Sie die Bibliothek einer Entwicklungsumgebung zu.
1. Fügen Sie der Bibliothek eine Änderung hinzu.
Klicken Sie zum Hinzufügen eines Elements auf **[!UICONTROL Add a Change]** und wählen Sie die Elemente aus, die Sie hinzufügen möchten. Jedes Element, das bearbeitet oder gelöscht wurde, kann der ausgewählten Bibliothek hinzugefügt werden.

   ![](../../images/library-add-change.jpg)

   Sie können Ihrer Bibliothek Folgendes hinzufügen:

   * Regeln
   * Datenelemente
   * Erweiterungskonfigurationen

1. Klicken Sie auf **[!UICONTROL Add All Changed Resources]**, um alle Ressourcen hinzuzufügen, die sich geändert haben.
1. Wählen Sie **[!UICONTROL Save]** oder **[!UICONTROL Save and Build for Development]** aus.

   Beim Bereitstellen wird ein Build kompiliert und in der zugewiesenen Umgebung bereitgestellt.

Wählen Sie nach Erstellung einer Bibliothek das Dropdown-Menü für diese Bibliothek aus, um eine der folgenden Optionen auszuwählen:

* **Bearbeiten**: Mit dieser Option können Sie die Bibliothekskonfiguration ändern.

* **Build für Entwicklung**: Mit dieser Option wird ein Build kompiliert und in der zugewiesenen Umgebung bereitgestellt.

* **Zur Genehmigung einreichen**: Mit dieser Option kann die Bibliothek von einem Genehmiger in den nächsten Schritt im Veröffentlichungsprozess verschoben werden.

* **Löschen**: Mit dieser Option wird die aktuell ausgewählte Bibliothek aus dem Veröffentlichungsprozess entfernt.

![](../../images/library-menu.png)

## Hinzufügen zu einer Bibliothek {#add-to-a-library}

Um eine Bibliothek hinzuzufügen, führen Sie die folgenden Schritte aus.

1. Installieren Sie die [Erweiterungen](../managing-resources/extensions/overview.md), die Sie hinzufügen möchten.
1. Erstellen Sie die [Datenelemente](../managing-resources/data-elements.md) und Regeln, die Sie hinzufügen möchten.
1. Öffnen Sie die Registerkarte **[!UICONTROL Publishing]**.
1. Wählen Sie die zu ändernde [Bibliothek](libraries.md) aus und klicken Sie auf **[!UICONTROL Edit]**.
1. Verwenden Sie die Schaltflächen „Regeln“, „Datenelemente“ und „Erweiterungen“, um die Elemente auszuwählen, die Sie der Bibliothek hinzufügen möchten.
1. Speichern Sie die Änderungen.

Änderungen an der Bibliothek werden im Änderungsprotokoll der Bibliotheksinhalte angezeigt.

>[!NOTE]
>
>Datenelemente können von Erweiterungen abhängig sein. Regeln können von Datenelementen und Erweiterungen abhängig sein. Wenn Sie nicht alle erforderlichen Komponenten in Ihre Bibliothek aufnehmen, schlägt der Build zum Zeitpunkt der Erstellung fehl, und Sie müssen die erforderlichen Komponenten hinzufügen, bevor Sie einen erfolgreichen Build abschließen. In einer künftigen Version werden Abhängigkeiten überprüft, wenn Sie Änderungen an einer Bibliothek vornehmen.

## Entfernen aus einer Bibliothek

Um etwas aus einer Bibliothek zu entfernen, müssen Sie es deaktivieren und dann den deaktivierten Status veröffentlichen.

1. Deaktivieren Sie die zu entfernenden Erweiterungen sowie die Datenelemente und Regeln, die von diesen Erweiterungen abhängig sind.
1. Deaktivieren Sie die zu entfernenden Datenelemente und Regeln.
1. Öffnen Sie die Registerkarte **[!UICONTROL Publishing]**.
1. Wählen Sie die Bibliothek aus, die Sie ändern möchten.
1. Verwenden Sie die Schaltflächen „Regeln“, „Datenelemente“ und „Erweiterungen“, um die deaktivierten Elemente auszuwählen, die Sie aus der Bibliothek entfernen möchten.
1. Speichern Sie die Änderungen.

## Verwalten von Bibliotheksänderungen

Um Bibliotheksoptionen zu bearbeiten, führen Sie die folgenden Schritte aus.

1. Wählen Sie eine Bibliothek aus und klicken Sie auf **[!UICONTROL Edit]**, um Änderungen der Bibliothek anzuzeigen. Alle Änderungen werden in der [!UICONTROL Library Contents]-Liste angezeigt.

   ![](../../images/library-contents.jpg)

1. Klicken Sie auf die Änderung, die Sie anzeigen möchten, und wählen Sie eine Revision aus.

   ![](../../images/library-contents-revision.jpg)

1. Wählen Sie aus, ob **alle** oder **geänderte** Artikel angezeigt werden sollen.
1. Wählen Sie die Revision aus und klicken Sie auf **[!UICONTROL Select Revision]**.
1. Klicken Sie entweder auf **[!UICONTROL Add a Change]** oder auf **[!UICONTROL Add All Changed Resources]**.

## Aktive Bibliothek {#active-library}

Bibliotheken enthalten eine Reihe von Änderungen, die Sie an Ihrem bereitgestellten Code vornehmen möchten. Die aktive Bibliothek erleichtert dies, sodass Sie Änderungen schnell durchsuchen und sich die Auswirkungen ansehen können.

Erweiterungen, Regeln und Datenelemente können jetzt direkt in der Bibliothek gespeichert werden, an der Sie gerade arbeiten. Bei Bedarf kann aus der Dropdown-Liste [!UICONTROL Active Library] auch ein neuer Build oder sogar eine neue Bibliothek erstellt werden.

Die folgende Liste enthält weitere Informationen zum Verwalten einer aktiven Bibliothek.

1. [Erstellen Sie eine neue Bibliothek](libraries.md#create-a-library).
1. Navigieren Sie zu [Regeln](../managing-resources/rules.md), [Datenelemente](../managing-resources/data-elements.md) oder [Erweiterungen](../managing-resources/extensions/overview.md).
1. Wählen Sie Ihre aktive Bibliothek aus.
1. Nehmen Sie Ihre Änderungen vor, speichern Sie und erstellen Sie die Bibliothek.
1. Testen Sie Ihre Änderungen und wiederholen Sie diese Schritte nach Bedarf.
