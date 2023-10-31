---
solution: Experience Platform
title: Erstellen, Freigeben und Wiederverwenden von Playbook-Instanzen
description: Erfahren Sie, wie Sie für Ihren Marketing-Anwendungsfall Playbook-Instanzen erstellen, freigeben und wiederverwenden können.
badgeBeta: label="Beta" type="Informative"
exl-id: b06d8186-c41f-4150-bac4-69c616151ef9
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 100%

---

# (Beta) Erstellen, Freigeben und Wiederverwenden von Playbook-Instanzen

>[!AVAILABILITY]
>
>Diese Funktion befinden sich derzeit in der Betaphase und steht nicht allen Benutzenden zur Verfügung. Dokumentation und Funktionalitäten können sich ändern.

Um ein Playbook zu verwenden, navigieren Sie zu **[!UICONTROL Playbooks für Anwendungsfälle] > [!UICONTROL Playbooks]**. Durchsuchen und verwenden Sie die verschiedenen Such- und Filteroptionen auf der Seite, um ein bestimmtes Playbook auszuwählen und die ersten Schritte damit auszuführen.

## Erstellen einer Playbook-Instanz {#create-playbook-instance}

Bevor Sie eine Playbook-Instanz erstellen, sollten Sie die verfügbaren Playbooks erkunden, um das [richtige Playbook für sich zu finden](/help/use-case-playbooks/playbooks/discover.md). Wenn Sie bereit sind, mit einem Playbook fortzufahren und eine Instanz zu erstellen, wählen Sie **[!UICONTROL Instanz erstellen]** aus, um mit dem Playbook fortzufahren und technische Assets zu generieren.

![Erstellen einer Playbook-Instanz.](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

Diese Aktion generiert mehrere Assets, die Sie für den im Playbook beschriebenen Anwendungsfall verwenden können.

![Playbook-Ansicht der generierten Assets nach der Aktivierung.](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### Bearbeiten von Instanznamen und -beschreibungen mithilfe von Konfigurationssteuerelementen {#edit-instance-metadata}

Nachdem Sie eine Instanz basierend auf einem Playbook erstellt haben, können Sie sie personalisieren, um sie von anderen Instanzen zu unterscheiden, die anhand desselben Playbooks erstellt wurden. Wählen Sie das Konfigurationssteuerelement aus, wie unten gezeigt. Bearbeiten Sie den Namen, die Beschreibung und die Notizen und wählen Sie **[!UICONTROL Speichern]** aus, wenn Sie fertig sind.

![Bearbeiten des Namens und der Beschreibung einer Instanz.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### Grundlegendes zu generierten Assets {#understand-assets}

>[!IMPORTANT]
>
>Keine Sorge! Hier können Sie sicher experimentieren. Es kann nichts kaputtgehen. Mit den von Ihnen erstellten Assets sind noch keine Daten verknüpft. Sie müssen zunächst Daten aufnehmen, um Anwendungsfälle zu erhalten.

Es ist wichtig zu verstehen, dass die generierten Assets je nach aktiviertem Anwendungsfall unterschiedlich sind:

* Für verschiedene Arten von Playbooks werden verschiedene Assets generiert. Diese Assets werden speziell für den auf dem Playbook basierenden Anwendungsfall erstellt. Ein Playbook generiert beispielsweise ein Schema, ein Segment, eine Journey und Nachrichten. Ein anderes Playbook generiert ein Schema, ein Segment und ein Ziel, für das Daten aktiviert werden sollen.
* Die Assets selbst unterscheiden sich zwischen den Playbooks. Für das Playbook **[!UICONTROL Geburtstagsnachricht an Gäste senden]** gilt für die erstellte Zielgruppe etwa die Regel `birthday=today AND year=any`.

Beispiel: Für das Playbook **[!UICONTROL Abgebrochener Warenkorb: Artikel]** können Sie sehen, dass eine bestimmte Journey erstellt wurde, die die für diesen Anwendungsfall erstellten Nachrichten enthält.

![Mit der Option „Playbooks für Anwendungsfälle“ erstellte Journey.](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### Verwenden und Bearbeiten generierter Assets {#use-and-edit-assets}

Wenn Sie die Assets erkunden, die nach dem Erstellen einer Playbook-Instanz generiert werden, können Sie alle erstellten Assets bearbeiten.

Wenn Sie oder ein Team-Mitglied eine andere Instanz des Playbooks erstellen, werden die bearbeiteten Assets beibehalten und neue Assets für die neue Instanz des Playbooks erstellt.

Das oben beschriebene Verhalten gilt für alle Assets, die erstellt werden, mit Ausnahme von Schemata. Bei Schemata werden neue Schemata nicht erstellt, wenn eine neue Instanz eines Playbooks erstellt wird. Daher verwenden Sie das bearbeitete Schema einer anderen Instanz des Playbooks in der neu erstellten Instanz.

>[!TIP]
>
>Testen Sie in der Entwicklungs-Sandbox und wechseln Sie zur Produktion, wenn Sie dazu bereit sind.
>
>Nachdem Objekte generiert wurden, können Sie sie in den Entwicklungs-Sandboxes weiter testen, indem Sie Daten hinzufügen. Sie können die Assets so lange Sie möchten in der Entwicklungs-Sandbox testen, und Sie können die Asset-Logik (Segmentdefinitionen, Journeys, Schemata) in der Produktions-Sandbox replizieren, wenn Sie dazu bereit sind.

## Wiederverwenden von Playbooks {#reuse-playbooks}

Wenn Sie mehrere Instanzen desselben Playbooks erstellen, können Sie denselben Anwendungsfall später implementieren, ohne die Details Ihrer vorherigen Implementierung des Anwendungsfalls zu ändern.

## Geben Sie das Playbook und die generierten Assets für andere Team-Mitglieder frei {#share-playbook}

Sie können die generierte Instanz und erstellten Assets für andere Team-Mitglieder freigeben. Kopieren Sie dazu den URL-Link aus dem Browser und geben Sie ihn an Ihr Team weiter, damit es einen Überblick über die generierten Assets erhält.

![In einer Ansicht „Playbooks für Anwendungsfälle“ hervorgehobene URL.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Nächste Schritte {#next-steps}

Durch Lesen dieses Handbuchs und des Leitfadens zum Finden des richtigen Playbooks wissen Sie jetzt, wie Sie die verschiedenen Abschnitte eines Playbooks interpretieren und wie Sie die Assets verwenden, die generiert werden, nachdem Sie eine Playbook-Instanz erstellt haben.

Als Nächstes können Sie den Playbook-Katalog durchsuchen, um das richtige Playbook für Ihren Anwendungsfall zu finden. Sollten Probleme auftreten, finden Sie weitere Informationen im [Handbuch zur Fehlerbehebung](/help/use-case-playbooks/playbooks/troubleshooting.md).
