---
solution: Experience Platform
title: Handbuch zur Benutzeroberfläche von Playbooks
description: Erfahren Sie, wie Sie mit der Experience Platform-Benutzeroberfläche Bücher anzeigen und aktivieren können.
badgeBeta: label="Beta" type="Informative"
source-git-commit: 63ea852ca9f9a45d1c071fd1033cbd44cbb427c6
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 2%

---


# (Beta) Aktivierung und Wiederverwendung eines Playbooks

>[!AVAILABILITY]
>
>Diese Funktion ist derzeit als Betaversion verfügbar und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalitäten können sich ändern.

Um ein Playbook zu verwenden, navigieren Sie zu **[!UICONTROL Anwendungsbeispiele für Playbooks] > [!UICONTROL Playbooks]**. Durchsuchen und verwenden Sie die verschiedenen Such- und Filteroptionen auf der Seite, um ein bestimmtes Playbook auszuwählen und zu beginnen.

## Suchen und filtern {#search-and-filter}

Verwenden Sie das Suchfenster und die auf der Seite verfügbaren Filter, um das richtige Playbook für Ihren Anwendungsfall zu finden.

Sie können beispielsweise Playbooks filtern, die Sie verwenden können, basierend auf der Phase im Marketing-Trichter, auf die Sie abzielen möchten - Konversion, Interaktion oder Bindung. Sie können die angezeigten Playbooks auch nach der Branche filtern, in der Sie sich befinden, oder nach der Produktberechtigungen, auf die Sie Zugriff haben - Adobe Journey Optimizer oder Echtzeit-Kundendatenplattform.

![Filtern von Playbooks nach Marketing-Trichter, Branche oder Produkt](/help/use-case-playbooks/assets/playbooks/ui-guide/filter-by-funnel-industry-product.gif)

Sie können auch die Suchfunktion verwenden, um das richtige Playbook für Sie zu finden. Unten finden Sie ein Beispiel dafür, wie Sie ein Playbook finden, das Ihnen dabei hilft, mit Benutzern in Kontakt zu treten, die möglicherweise ihren Warenkorb abgebrochen haben.

![Wenden Sie sich an Benutzer, die möglicherweise ihren Warenkorb abgebrochen haben.](/help/use-case-playbooks/assets/playbooks/ui-guide/engage-abandoned-cart.gif)

Alternativ können Sie die verfügbaren Playbooks nach den Kanälen filtern, die Sie zum Erreichen Ihrer Kunden verwenden möchten, wie unten dargestellt:

![Nach Kanal filtern](/help/use-case-playbooks/assets/playbooks/ui-guide/channel-select-filter.gif)

Experimentieren Sie mit den Filtern und suchen Sie nach der richtigen Playbook für Sie.

## Anzeigen von Playbook und Generieren von Assets {#view-playbook-generate-assets}

Bevor Sie sich auf ein Playbook setzen und Instanzen davon erstellen, sollten Sie es überprüfen, um sicherzustellen, dass es Ihren Anforderungen entspricht. Damit Sie die Anwendungsfälle besser verstehen können, die sie abdecken, enthalten alle Bücher die folgenden Abschnitte. Wenn Sie bereit sind, fortzufahren und Assets zu generieren, wählen Sie **[!UICONTROL Instanz erstellen]**.

### Mindmap {#mindmap}

Verwenden Sie den Abschnitt zur Übersicht in einem Playbook, um die Schritte des Workflows zu verstehen, die das Playbook Ihnen bei der Lösung unterstützen kann. Visualisieren Sie den Fluss, wie alle generierten Objekte dazu beitragen können, den Anwendungsfall zu erreichen, aus der Perspektive der im Anwendungsfall angesprochenen Persona.

Die Mindmap beginnt mit einer Definition, wer auf der Journey erreicht wird, und beschreibt bei jedem Schritt, ob etwas von Adobe bereitgestellt wird, z. B. eine neue Nachricht oder eine Erinnerung, oder ob es etwas ist, was die Zielperson getan hat, dass die nächste Nachricht oder das nächste Ereignis Trigger.

![Playbook-Mindmap hervorgehoben.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-mindmap.png)


### Zusammenfassung  {#summary}

Inspect Sie den Übersichtsabschnitt , um zu verstehen, welche Assets generiert werden, sobald Sie Instanzen aus dem Playbook erstellen. Die Assets, die für jedes Playbook generiert werden, sind auf den Anwendungsfall zugeschnitten, den das Playbook aktiviert. Weitere Informationen zu allen Elementen im Zusammenfassungsabschnitt erhalten Sie unten.

| Element | Beschreibung |
---------|----------|
| **[!UICONTROL Zielgruppe]** | Beschreibt die Rollen, die Sie über dieses Anwendungsbeispiel-Playbook erreichen möchten. |
| **[!UICONTROL Marketing-Kanäle]** | Beschreibt die Kanäle, die zum Erreichen der im Playbook ausgewählten Personas verwendet werden. |
| **[!UICONTROL Technische Assets]** | Eine Liste der technischen Assets, die generiert werden, nachdem Sie Instanzen des Playbooks erstellt haben. Die generierten Assets unterscheiden sich je nach Anwendungsfall von der Wiedergabeliste. Einige Playbooks generieren möglicherweise Schemas, Segmente und Journey. Andere können Ziele generieren. Siehe Abschnitt [Grundlegendes zu den generierten Assets](#understand-assets) weiter unten finden Sie weitere Informationen dazu, wie Sie die generierten Assets verwenden und wiederverwenden können. |

{style="table-layout:auto"}

![Playbook-Zusammenfassung hervorgehoben](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-summary.png)

### Instanzen {#instances}

Scrollen Sie nach unten zum Abschnitt Instanzen , um einen Überblick über die Instanzen dieses Playbooks zu erhalten, die Sie oder Mitglieder Ihres Teams bereits erstellt haben. Sie können verschiedene Steuerelemente verwenden, um die angezeigten Instanzen zu sortieren und zu filtern, um beispielsweise nur die von Ihnen erstellten Instanzen anzuzeigen. Sie können auch verschiedene Informationen zu den einzelnen Instanzen sehen, wie unten aufgeführt.

| Element | Beschreibung |
|---------|----------|
| **[!UICONTROL Name]** | Der Name der Instanz basierend auf dem Playbook. Sie können den Namen und die Beschreibung einer Instanz anpassen. Lesen Sie den folgenden Abschnitt unter [Bearbeiten von Instanzmetadaten](#edit-instance-metadata) für weitere Informationen. |
| **[!UICONTROL Status]** | Gibt den Status der Instanz an. A **[!UICONTROL Gesendet]** -Instanz kann verwendet werden. |
| **[!UICONTROL Erstellt]** | Gibt an, wann die Instanz erstellt wurde. |
| **[!UICONTROL Erstellt von]** | Gibt an, wer die Instanz erstellt hat. |
| **[!UICONTROL Zuletzt geändert]** | Gibt an, wann die Instanz zuletzt geändert wurde. |

{style="table-layout:auto"}

![Playbook-Instanz hervorgehoben.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-instances.png)

## Playbook aktivieren {#enable-playbook}

Wenn Sie bereit sind, mit einem Playbook fortzufahren und eine Instanz zu erstellen, wählen Sie **[!UICONTROL Instanz erstellen]** , um mit der Wiedergabe fortzufahren und technische Assets zu generieren.

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

### Spielbücher wiederverwenden {#reuse-playbooks}

Wenn Sie mehrere Instanzen desselben Playbooks erstellen, können Sie denselben Anwendungsfall später implementieren, ohne die Details Ihrer vorherigen Implementierung des Anwendungsfalls zu ändern.

### Geben Sie das Playbook und die generierten Assets für andere Team-Mitglieder frei. {#share-playbook}

Sie können die generierte Instanz und die Assets für andere Team-Mitglieder freigeben. Kopieren Sie dazu den URL-Link aus dem Browser und geben Sie ihn für Ihr Team frei, damit Sie einen Überblick über die generierten Assets erhalten.

![URL, die in einer Anwendungs-Playbook-Ansicht hervorgehoben ist.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Nächste Schritte {#next-steps}

Durch Lesen dieses Benutzerhandbuchs wissen Sie jetzt, wie Sie die verschiedenen Abschnitte eines Playbooks interpretieren und wie Sie die Assets verwenden, die generiert werden, nachdem Sie eine Instanz eines Playbooks erstellt haben. Als Nächstes können Sie den Playbook-Katalog durchsuchen, um das richtige Playbook für Ihren Anwendungsfall zu finden, und die Anleitung zur Fehlerbehebung lesen, wenn Fehler auftreten.