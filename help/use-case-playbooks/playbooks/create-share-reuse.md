---
solution: Experience Platform
title: Erstellen, Freigeben und Wiederverwenden von Playbook-Instanzen
description: Erfahren Sie, wie Sie Playbook-Instanzen erstellen, freigeben und wiederverwenden können, um Ihren Marketing-Anwendungsfall zu erreichen.
badgeBeta: label="Beta" type="Informative"
source-git-commit: e61e200b148e4d17041b3711bd63c796a44b05c8
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---


# (Beta) Erstellen, Freigeben und Wiederverwenden von Playbook-Instanzen

>[!AVAILABILITY]
>
>Diese Funktion ist derzeit als Betaversion verfügbar und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalitäten können sich ändern.

Um ein Playbook zu verwenden, navigieren Sie zu **[!UICONTROL Anwendungsbeispiele für Playbooks] > [!UICONTROL Playbooks]**. Durchsuchen und verwenden Sie die verschiedenen Such- und Filteroptionen auf der Seite, um ein bestimmtes Playbook auszuwählen und zu beginnen.

## Erstellen einer Playbook-Instanz {#create-playbook-instance}

Bevor Sie eine Playbook-Instanz erstellen, sollten Sie die verfügbaren Playbooks in [Entdecken Sie das richtige Playbook für Sie](/help/use-case-playbooks/playbooks/discover.md). Wenn Sie bereit sind, mit einem Playbook fortzufahren und eine Instanz zu erstellen, wählen Sie **[!UICONTROL Instanz erstellen]** , um mit der Wiedergabe fortzufahren und technische Assets zu generieren.

![Erstellen Sie eine Instanz eines Playbooks.](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

Diese Aktion generiert mehrere Assets, die Sie verwenden können, um den im Playbook beschriebenen Anwendungsfall zu erreichen.

![Wiedergabe der generierten Assets nach der Aktivierung.](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### Verwenden Sie die Konfigurationssteuerelemente, um Instanznamen und -beschreibungen zu bearbeiten {#edit-instance-metadata}

Nachdem Sie eine Instanz basierend auf einem Playbook erstellt haben, können Sie sie personalisieren, um sie von anderen Instanzen zu unterscheiden, die aus demselben Playbook erstellt wurden. Wählen Sie das Konfigurationssteuerelement wie unten dargestellt aus. Bearbeiten Sie den Namen, die Beschreibung und die Notizen und wählen Sie **[!UICONTROL Speichern]** wenn Sie fertig sind.

![Bearbeiten Sie den Namen und die Beschreibung einer Instanz.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### Grundlegendes zu den generierten Assets {#understand-assets}

>[!IMPORTANT]
>
>Keine Sorge! Das ist ein sicherer Raum zum Experimentieren und man kann nichts kaputt machen. Mit den von Ihnen erstellten Assets sind noch keine Daten verknüpft. Sie müssen zunächst Daten erfassen, um die Anwendungsfälle zu erreichen.

Es ist wichtig zu verstehen, dass die generierten Assets je nach dem Anwendungsfall, den Sie aktivieren, unterschiedlich sind:

* Für verschiedene Arten von Playbooks werden verschiedene Assets generiert. Diese Assets werden speziell für den Anwendungsfall erstellt, der über das Playbook erreicht wird. Ein Playbook generiert beispielsweise ein Schema, ein Segment, eine Journey und Nachrichten. Ein anderes Playbook generiert ein Schema, ein Segment und ein Ziel, für das Daten aktiviert werden sollen.
* Die Assets selbst unterscheiden sich zwischen den Playbooks. Beispiel: für die **[!UICONTROL Geburtstagsnachricht an Gäste senden]** Playbook festlegen, hat die erstellte Zielgruppe die Regel `birthday=today AND year=any`.

Beispiel: **[!UICONTROL Warenkorb abgebrochen: Merchandise]** playbook können Sie sehen, dass eine bestimmte Journey erstellt wurde, die die für diesen Anwendungsfall erstellten Nachrichten enthält.

![Journey erstellt aus dem Anwendungsfall-Playbook.](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### Verwenden und Bearbeiten der generierten Assets {#use-and-edit-assets}

Wenn Sie die Assets durchsuchen, die nach dem Erstellen einer Instanz eines Playbooks generiert werden, können Sie alle erstellten Assets bearbeiten.

Wenn Sie oder jemand in Ihrem Team eine andere Instanz des Playbooks erstellen, werden die bearbeiteten Assets beibehalten und neue Assets für die neue Instanz des Playbooks erstellt.

Das oben beschriebene Verhalten gilt für alle Assets, die erstellt werden, mit Ausnahme von Schemas. Bei Schemata werden neue Schemas nicht erstellt, wenn eine neue Instanz eines Playbooks erstellt wird. Daher verwenden Sie das bearbeitete Schema einer anderen Instanz des Playbooks in der neu erstellten Instanz.

>[!TIP]
>
>Testen Sie in der Entwicklungs-Sandbox und wechseln Sie zur Produktion, sobald sie bereit ist.
>
>Nachdem Objekte generiert wurden, können Sie sie in den Entwicklungs-Sandboxes weiter testen, indem Sie Daten hinzufügen. Sie können die Assets so lange testen, wie Sie es in der Entwicklungs-Sandbox wünschen, und Sie können die Asset-Logik (Segmentdefinitionen, Journey, Schemas usw.) in der Produktions-Sandbox replizieren, wenn Sie bereit sind.

## Spielbücher wiederverwenden {#reuse-playbooks}

Wenn Sie mehrere Instanzen desselben Playbooks erstellen, können Sie denselben Anwendungsfall später implementieren, ohne die Details Ihrer vorherigen Implementierung des Anwendungsfalls zu ändern.

## Geben Sie das Playbook und die generierten Assets für andere Team-Mitglieder frei. {#share-playbook}

Sie können die generierte Instanz und die Assets für andere Team-Mitglieder freigeben. Kopieren Sie dazu den URL-Link aus dem Browser und geben Sie ihn für Ihr Team frei, damit Sie einen Überblick über die generierten Assets erhalten.

![URL, die in einer Anwendungs-Playbook-Ansicht hervorgehoben ist.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Nächste Schritte {#next-steps}

Durch Lesen dieses Handbuchs und des Leitfadens zum Entdecken des richtigen Playbooks wissen Sie jetzt, wie Sie die verschiedenen Abschnitte eines Playbooks interpretieren und wie Sie die Assets verwenden, die generiert werden, nachdem Sie eine Instanz eines Playbooks erstellt haben.

Als Nächstes können Sie den Playbook-Katalog durchsuchen, um das richtige Playbook für Ihr Anwendungsbeispiel zu finden und die [Handbuch zur Fehlerbehebung](/help/use-case-playbooks/playbooks/troubleshooting.md) wenn Probleme auftreten.