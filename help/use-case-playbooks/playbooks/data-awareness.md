---
solution: Experience Platform
title: Übersicht über das Datenbewusstsein in "Anwendungsfallbüchern"
description: Erfahren Sie, wie Sie die Wertschöpfungszeit beschleunigen können, indem Sie die in der zugrunde liegenden inspirierenden Sandbox erstellten Assets in andere Sandboxes kopieren.
role: Developer
exl-id: 537eff13-f5fe-4cc9-9769-ab47b3cecda7
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# Publish-Playbook-generierte Assets in andere Sandboxes {#publish-to-other-sandboxes}

Anwendungsbeispiele sind Marketing-Vorlagen, mit denen Assets wie Zielgruppen, Schemata oder Journey für gängige Marketing-Anwendungsfälle generiert werden. Sie können die von Playbooks erstellten Assets in der inspirierenden Sandbox testen. Sobald Sie bereit sind, können Sie die Assets in andere Entwicklungs-Sandboxes importieren, um sie mit den in diesen Sandboxes verfügbaren Daten weiter zu testen. Wenn Sie mit dem Test zufrieden sind, können Sie die Assets dann aus Entwicklungs-Sandboxes in Produktions-Sandboxes verschieben.

In bestimmten Fällen haben Sie jedoch möglicherweise bereits Ihre eigenen Schemas, Felder und Feldergruppen in anderen Entwicklungs-Sandboxes eingerichtet. Dadurch können einige der von den Anwendungsfallvorlagen generierten Assets, z. B. Journey, mit Ihren Daten inkompatibel werden. In diesem Tutorial erfahren Sie, wie Sie mithilfe der Datenerfassungsfunktion die generierten Assets besser an Ihre vorhandenen Assets anpassen und ergänzen können.

## Voraussetzungen {#prerequisites}

Bevor Sie dieses Tutorial lesen, durchsuchen Sie die [verfügbaren Anwendungsfallenspielbuchvorlagen](/help/use-case-playbooks/playbooks/choose.md#search-and-filter) und [erstellen Sie eine Instanz](/help/use-case-playbooks/playbooks/create-share-reuse.md) eines bevorzugten Playbooks.

Beim Erstellen einer Instanz wird ein Satz von Assets wie Journey, Segmenten, Schemata und Nachrichten in der inspirierenden Sandbox generiert. Lesen Sie weiter, um zu erfahren, wie Sie diese Assets in andere Sandboxes kopieren können.

### Erstellen und Veröffentlichen eines Pakets {#create-publish-package}

>[!NOTE]
>
> Sie können Pakete nur in andere Entwicklungs-Sandboxes importieren. Sobald Sie alle erforderlichen Änderungen oder Aktualisierungen vorgenommen haben, können Sie die Assets oder Pakete aus diesen Entwicklungs-Sandboxes in die Produktion importieren. Sie können nicht direkt aus den Sandboxes &quot;Anwendungsfall-Playbooks&quot;in die Produktion importieren.

1. Um Objekte aus der inspirierenden Sandbox in eine andere Sandbox zu importieren, navigieren Sie zu einer gewünschten Instanz eines Anwendungsfall-Playbooks und wählen Sie **[!UICONTROL Publish in eine andere Sandbox]** aus, um die Artefakte als Paket zu exportieren.

   ![GIF mit den verschiedenen Anwendungsfallinstanzen](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. Nachdem Sie die Schaltfläche **[!UICONTROL Publish in eine andere Sandbox]** ausgewählt haben, wird ein Modal angezeigt. Geben Sie den Namen und die optionale Beschreibung ein und wählen Sie **[!UICONTROL Erstellen]** aus. In diesem Schritt werden die generierten Assets in einem Paket gebündelt, das in eine andere Sandbox importiert werden kann.

   ![Ein Modal zum Erstellen eines Pakets](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. Navigieren Sie zur Seite **Sandboxes** im linken Navigationsbereich und wählen Sie die Registerkarte **Pakete** aus, suchen Sie Ihr Paket und veröffentlichen Sie es. Um ein Paket zu veröffentlichen, das sich im Entwurfsstatus befindet, führen Sie die Schritte im Dokument [Sandbox-Tool](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish) aus.

   ![Verpacken im Entwurfsstatus oder unveröffentlicht](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![Veröffentlichen des Pakets](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. Nachdem die Veröffentlichung erfolgreich war, sollte auf der Seite zum Durchsuchen von Paketen neben dem Namen eine Schaltfläche &quot;**+**&quot; aktiviert werden.

   Registerkarte ![Pakete auf der Seite &quot;Sandboxes&quot;](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > Das Paket kann nicht importiert werden, solange es sich noch im Entwurfsmodus befindet. Öffnen Sie daher die Seite mit den Paketdetails und veröffentlichen Sie das Paket.

5. Wählen Sie das Steuerelement **+** aus und starten Sie den Workflow, um die vom Anwendungsfall-Playbook generierten Assets in die Sandbox **[!UICONTROL Ziel]** zu importieren. Wählen Sie eine Ziel-Sandbox aus und bestätigen Sie mithilfe des Dropdown-Menüs den Paketnamen, den Sie importieren möchten. Fügen Sie die Auftragsdetails wie Auftragsname und Auftragsbeschreibung hinzu, bevor Sie mit dem nächsten Schritt fortfahren.

   ![Import-Workflow starten, Ziel auswählen, Paket bestätigen, Auftragsdetails hinzufügen.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

6. Im Schritt **[!UICONTROL Abhängigkeiten anzeigen]** können Sie Schemas zuordnen und andere Assets aus der inspirierenden Sandbox in die Ziel-Sandbox kopieren. Die Schaltfläche **[!UICONTROL Beenden]** ist deaktiviert, bis Sie jedes Schema zuordnen.

   ![Ordnen Sie Schemas im Schritt &quot;Abhängigkeiten anzeigen&quot;zu, indem Sie die Schaltfläche &quot;Fertigstellen&quot;aktivieren.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### Schemata zuordnen {#map-schemas}

1. Zuordnen des ersten Schemas Im Dialogfeld für die Schemazuordnung wird eine Dropdown-Liste zur Auswahl des Zielschemas angezeigt. Wenn das Quellschema ein Profilschema ist, gibt es neben dem [individuellen Vereinigungsprofilschema](/help/xdm/classes/individual-profile.md) keine weiteren Zielschemaoptionen. Sie sehen automatisch generierte Zuordnungsempfehlungen zwischen Source-Daten und Zielfeldern, wenn die Seite zum ersten Mal angezeigt wird. Sie können die Zuordnungen bearbeiten, indem Sie das Zielfeld auswählen und dann ein neues Feld auswählen. Wenn Sie die vorgeschlagenen Zuordnungen ändern, verwenden Sie die Schaltfläche **Validieren** , um die neuen Zuordnungen zu validieren und Fehler anzuzeigen, die mit den neuen Zuordnungen verknüpft sein können. Wählen Sie **Speichern** aus, sobald die Zuordnung abgeschlossen ist.

   ![Dialogfeld für die Schemazuordnung mit einer Dropdown-Liste zur Auswahl eines Zielschemas.](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. Fahren Sie mit der Zuordnung aller Felder in den Schemas fort. Wenn das Schema ein [Ereignisschema](/help/xdm/classes/experienceevent.md) ist, wird im Dialogfeld eine Dropdown-Liste angezeigt, in der Sie alle Ereignisschemata in der Ziel-Sandbox anzeigen können.

   ![Wählen Sie ein Zielschema aus dem Dropdown-Menü aus](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. Wählen Sie ein Schema aus den verfügbaren Schemas in der **Ziel-Sandbox** aus.

   ![Schema auswählen](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. Schließen Sie die Zuordnung ab und wählen Sie **Speichern** aus.

   ![Zuordnung speichern](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. Nachdem Sie die Zuordnung aller Felder in den Schemas abgeschlossen haben, wählen Sie **Beenden** aus, um den Import-Workflow abzuschließen.

   ![Beenden Sie den Fluss](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > Sie können keine Assets mit Ausnahme der Schemas ändern, da es sich um eine inspirierende Sandbox handelt, sie jedoch als Abhängigkeiten des Pakets angezeigt werden.

### Importstatus {#import-status}

1. Sie werden automatisch zur Seite [**Importe**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details) weitergeleitet, auf der Sie den Fortschritt Ihres Imports sehen können.

   ![Seite mit dem Importfortschritt](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. Während das Paket importiert wird, werden die Assets des Pakets in der Ziel-Sandbox erstellt. Nach Abschluss referenzieren sie die Felder, die Sie während des Importvorgangs zugeordnet haben. Der Prozess ist jetzt abgeschlossen und die Assets aus der inspirierenden Sandbox sind jetzt auch in Ihrer Ziel-Sandbox vorhanden, damit Sie sie testen können.

   ![ Generierte Assets in der Ziel-Sandbox](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## Nächste Schritte

Nach dem Lesen dieses Handbuchs haben Sie jetzt ein besseres Verständnis dafür, wie Sie Anwendungsfallbücher zusammen mit dem [Sandbox-Tool](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details) nutzen können, um ausführbare Journey zu erstellen, die auf Ihre Schemas verweisen. Erfahren Sie mehr über die gängigen [Real-Time CDP-Anwendungsfälle](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md).
