---
solution: Experience Platform
title: Erstellen, Freigeben und Wiederverwenden von Playbook-Instanzen
description: Erfahren Sie, wie Sie für Ihren Marketing-Anwendungsfall Playbook-Instanzen erstellen, freigeben und wiederverwenden können.
role: User, Developer
exl-id: b06d8186-c41f-4150-bac4-69c616151ef9
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 71%

---

# Erstellen, Freigeben und Wiederverwenden von Playbook-Instanzen

Um ein Playbook zu verwenden, navigieren Sie zu **[!UICONTROL Use Case Playbooks]>[!UICONTROL Playbooks]**. Durchsuchen und verwenden Sie die verschiedenen Such- und Filteroptionen auf der Seite, um ein bestimmtes Playbook auszuwählen und die ersten Schritte damit auszuführen.

## Erstellen einer Playbook-Instanz {#create-playbook-instance}

>[!CONTEXTUALHELP]
>id="platform_playbooks_create"
>title="Erstellen einer Instanz"
>abstract="Erstellen Sie eine Liste mit Assets wie Journeys, Zielgruppen, Schemata oder Zielen, die für Journeys oder Aktivierungsszenarien verwendet werden können."

Bevor Sie eine Playbook-Instanz erstellen, erkunden Sie die verfügbaren Playbooks, um [das richtige Playbook auszuwählen](/help/use-case-playbooks/playbooks/choose.md). Wenn Sie bereit sind, mit einem Playbook fortzufahren und eine Instanz zu erstellen, wählen Sie **[!UICONTROL Create Instance]** aus, um mit dem Playbook fortzufahren und technische Assets zu generieren.

![Erstellen einer Playbook-Instanz.](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

Diese Aktion generiert mehrere Assets, die Sie für den im Playbook beschriebenen Anwendungsfall verwenden können.

![Playbook-Ansicht der generierten Assets nach der Aktivierung.](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### Bearbeiten von Instanznamen und -beschreibungen mithilfe von Konfigurationssteuerelementen {#edit-instance-metadata}

Nachdem Sie eine Instanz basierend auf einem Playbook erstellt haben, können Sie sie personalisieren, um sie von anderen Instanzen zu unterscheiden, die anhand desselben Playbooks erstellt wurden. Wählen Sie das Konfigurationssteuerelement aus, wie unten gezeigt. Bearbeiten Sie den Namen, die Beschreibung und die Notizen und wählen Sie **[!UICONTROL Save]** aus, wenn Sie fertig sind.

![Bearbeiten des Namens und der Beschreibung einer Instanz.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### Grundlegendes zu generierten Assets {#understand-assets}

>[!IMPORTANT]
>
>Keine Sorge! Hier können Sie sicher experimentieren. Es kann nichts kaputtgehen. Mit den von Ihnen erstellten Assets sind noch keine Daten verknüpft. Sie müssen zunächst Daten aufnehmen, um Anwendungsfälle zu erhalten.

Es ist wichtig zu verstehen, dass die generierten Assets je nach aktiviertem Anwendungsfall unterschiedlich sind:

* Für verschiedene Arten von Playbooks werden verschiedene Assets generiert. Diese Assets werden speziell für den auf dem Playbook basierenden Anwendungsfall erstellt. Beispielsweise generiert ein Playbook ein Schema, eine Zielgruppe, eine Journey und Nachrichten. Ein anderes Playbook generiert ein Schema, eine Zielgruppe und ein Ziel, für das Daten aktiviert werden können.
* Die Assets selbst unterscheiden sich zwischen den Playbooks. Für das Playbook &quot;**[!UICONTROL Send A Birthday Message To Guests]**&quot; hat beispielsweise die erstellte Zielgruppe die `birthday=today AND year=any`.

Um ein Beispiel zu veranschaulichen, können Sie für das **[!UICONTROL Abandoned Cart: Merchandise]** Playbook sehen, dass eine bestimmte Journey erstellt wird, die die für diesen Anwendungsfall erstellten Nachrichten enthält.

![Mit der Option „Playbooks für Anwendungsfälle“ erstellte Journey.](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### Verwenden und Bearbeiten generierter Assets {#use-and-edit-assets}

Wenn Sie die Assets erkunden, die nach dem Erstellen einer Playbook-Instanz generiert werden, können Sie alle erstellten Assets bearbeiten.

Wenn Sie oder ein Team-Mitglied eine andere Instanz des Playbooks erstellen, werden die bearbeiteten Assets beibehalten und neue Assets für die neue Instanz des Playbooks erstellt.

Das oben beschriebene Verhalten gilt für alle Assets, die erstellt werden, mit Ausnahme von Schemata. Bei Schemata werden neue Schemata nicht erstellt, wenn eine neue Instanz eines Playbooks erstellt wird. Daher verwenden Sie das bearbeitete Schema einer anderen Instanz des Playbooks in der neu erstellten Instanz.

>[!TIP]
>
>Testen Sie in der Entwicklungs-Sandbox und wechseln Sie zur Produktion, wenn Sie dazu bereit sind.
>
>Nachdem Objekte generiert wurden, können Sie sie in den Entwicklungs-Sandboxes weiter testen, indem Sie Daten hinzufügen. Sie können die Assets in der Entwicklungs-Sandbox so lange testen, wie Sie möchten, und Sie können die Asset-Logik (Zielgruppendefinitionen, Journey, Schemata usw.) in der Produktions-Sandbox replizieren, wenn Sie bereit sind. Sie können zur Entwicklungs-Sandbox und dann zur Produktions-Sandbox wechseln, indem Sie die Funktion [Datenerkennung](/help/use-case-playbooks/playbooks/data-awareness.md) verwenden.

## Wiederverwenden von Playbooks {#reuse-playbooks}

Wenn Sie mehrere Instanzen desselben Playbooks erstellen, können Sie denselben Anwendungsfall später implementieren, ohne die Details Ihrer vorherigen Implementierung des Anwendungsfalls zu ändern.

## Geben Sie das Playbook und die generierten Assets für andere Team-Mitglieder frei {#share-playbook}

Sie können die generierte Instanz und erstellten Assets für andere Team-Mitglieder freigeben. Kopieren Sie dazu den URL-Link aus dem Browser und geben Sie ihn an Ihr Team weiter, damit es einen Überblick über die generierten Assets erhält.

![In einer Ansicht „Playbooks für Anwendungsfälle“ hervorgehobene URL.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Videoeinführung des End-to-End-Playbook-Prozesses

Sehen Sie sich dieses Video an, um zu erfahren, wie Sie Instanzen eines Anwendungsfall-Playbooks von Anfang bis Ende entdecken, erstellen, veröffentlichen und beheben sowie die vom Playbook generierten Assets in andere in Ihrer Organisation eingerichtete Sandboxes kopieren können.

>[!VIDEO](https://video.tv.adobe.com/v/3427058/?learn=on)

## Nächste Schritte {#next-steps}

Durch Lesen dieses Handbuchs und des Leitfadens zum Finden des richtigen Playbooks wissen Sie jetzt, wie Sie die verschiedenen Abschnitte eines Playbooks interpretieren und wie Sie die Assets verwenden, die generiert werden, nachdem Sie eine Playbook-Instanz erstellt haben.

Als Nächstes können Sie den Playbook-Katalog durchsuchen, um das richtige Playbook für Ihren Anwendungsfall zu finden. Sollten Probleme auftreten, finden Sie weitere Informationen im [Handbuch zur Fehlerbehebung](/help/use-case-playbooks/playbooks/troubleshooting.md).
