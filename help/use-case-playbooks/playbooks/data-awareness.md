---
solution: Experience Platform
title: Übersicht über die Datenerkennung in Playbooks für Anwendungsfälle
description: Erfahren Sie, wie Sie die Wertschöpfungszeit beschleunigen können, indem Sie die in der inspirierenden End-Sandbox generierten Assets in andere Sandboxes kopieren.
role: Developer
exl-id: 537eff13-f5fe-4cc9-9769-ab47b3cecda7
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# Publish Playbook-generierte Assets in andere Sandboxes {#publish-to-other-sandboxes}

Anwendungsfall-Playbooks sind Marketing-Vorlagen, die zur Generierung von Assets wie Zielgruppen, Schemata oder Journey für gängige Marketing-Anwendungsfälle entwickelt wurden. Sie können die von Playbooks erstellten Assets in der inspirierenden Sandbox testen. Wenn Sie bereit sind, können Sie die Assets in andere Entwicklungs-Sandboxes importieren, um sie mit den Daten, die in diesen Sandboxes verfügbar sind, weiter zu testen. Wenn Sie mit den Tests zufrieden sind, können Sie die Assets aus Entwicklungs-Sandboxes in Produktions-Sandboxes verschieben.

In bestimmten Fällen haben Sie möglicherweise bereits Ihre eigenen Schemata, Felder und Feldergruppen in anderen Entwicklungs-Sandboxes eingerichtet. Dadurch können einige der durch die Anwendungsfallvorlagen generierten Assets, z. B. Journey, nicht mit Ihren Daten kompatibel sein. In diesem Tutorial erfahren Sie, wie Sie mit der Datenerkennungsfunktion die generierten Assets besser an Ihre vorhandenen Assets anpassen und ergänzen können.

## Voraussetzungen {#prerequisites}

Durchsuchen Sie vor dem Lesen dieses Tutorials die [verfügbaren Anwendungsfall-Playbook](/help/use-case-playbooks/playbooks/choose.md#search-and-filter)Vorlagen und [erstellen Sie eine Instanz](/help/use-case-playbooks/playbooks/create-share-reuse.md) eines bevorzugten Playbooks.

Das Erstellen einer -Instanz generiert einen Satz von Assets wie Journeys, Segmente, Schemata und Nachrichten in der inspirierenden Sandbox. Im Folgenden erfahren Sie, wie Sie diese Assets in andere Sandboxes kopieren können.

### Erstellen und Veröffentlichen eines Pakets {#create-publish-package}

>[!NOTE]
>
> Sie können Pakete nur in andere Entwicklungs-Sandboxes importieren. Nachdem Sie alle erforderlichen Änderungen oder Aktualisierungen vorgenommen haben, können Sie die Assets oder Pakete aus diesen Entwicklungs-Sandboxes in die Produktion importieren. Sie können nicht direkt aus den Playbooks für Anwendungsfälle in die Produktion importieren.

1. Um Objekte aus der inspirierenden Sandbox in eine andere Sandbox zu importieren, navigieren Sie zu der gewünschten Instanz eines Anwendungsfall-Playbooks und wählen Sie **[!UICONTROL Publish in eine andere Sandbox]** aus, um die Artefakte als Paket zu exportieren.

   ![GIF mit den verschiedenen Anwendungsfallinstanzen](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. Nachdem Sie die Schaltfläche **[!UICONTROL Publish in eine andere Sandbox]** ausgewählt haben, wird ein Modal angezeigt. Geben Sie den Namen und die optionale Beschreibung ein und wählen Sie **[!UICONTROL Erstellen]**. In diesem Schritt werden die generierten Assets in einem Paket gebündelt, das in eine andere Sandbox importiert werden kann.

   ![Ein Modal zum Erstellen eines Pakets](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. Navigieren Sie zur Seite **Sandboxes** im linken Navigationsbereich und wählen Sie die Registerkarte **Pakete** aus, suchen Sie Ihr Paket und veröffentlichen Sie es. Um ein Paket im Entwurfsstatus zu veröffentlichen, führen Sie die Schritte im Dokument [Sandbox-Tools](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish) aus.

   ![Paket mit dem Status „Entwurf“ oder „Unveröffentlicht“](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![Veröffentlichen des Pakets](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. Nachdem die Veröffentlichung erfolgreich war, sollte auf der Seite zum Durchsuchen von Paketen neben dem Namen eine **+**-Schaltfläche angezeigt werden.

   ![Registerkarte „Pakete“ auf der Seite „Sandboxes“](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > Das Paket kann nicht importiert werden, während es sich noch im Entwurfsmodus befindet. Öffnen Sie daher die Paketdetailseite und veröffentlichen Sie das Paket.

5. Wählen Sie das Steuerelement **+** aus und starten Sie den Workflow, um die vom Playbook für Anwendungsfälle generierten Assets in die **[!UICONTROL Ziel-Sandbox]** zu importieren. Wählen Sie eine Ziel-Sandbox aus und bestätigen Sie mithilfe der Dropdown-Liste den Paketnamen, den Sie importieren möchten. Fügen Sie die Auftragsdetails wie Auftragsname und Auftragsbeschreibung hinzu, bevor Sie mit dem nächsten Schritt fortfahren.

   ![Import-Workflow starten, Ziel auswählen, Paket bestätigen, Auftragsdetails hinzufügen.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

6. Im Schritt **[!UICONTROL Abhängigkeiten anzeigen]** können Sie Schemata zuordnen und andere Assets aus der inspirierenden Sandbox in die Ziel-Sandbox kopieren. Die Schaltfläche **[!UICONTROL Beenden]** ist deaktiviert, bis Sie jedes Schema zuordnen.

   ![Zuordnen von Schemata im Schritt „Abhängigkeiten anzeigen“, wodurch die Schaltfläche Beenden aktiviert wird.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### Zuordnen von Schemata {#map-schemas}

1. Ordnen Sie das erste Schema zu. Das Dialogfeld für die Schemazuordnung zeigt eine Dropdown-Liste zur Auswahl des Zielschemas an. Wenn das Quellschema ein Profilschema ist, gibt es keine anderen Zielschemaoptionen außer dem [individuellen Vereinigungsprofilschema](/help/xdm/classes/individual-profile.md). Sie können automatisch generierte Zuordnungsempfehlungen zwischen Source-Daten und Zielfeldern sehen, wenn die Seite zum ersten Mal angezeigt wird. Sie können die Zuordnungen bearbeiten, indem Sie das Zielfeld auswählen und dann ein neues Feld auswählen. Wenn Sie die vorgeschlagenen Zuordnungen ändern, verwenden Sie die Schaltfläche **Validieren** , um die neuen Zuordnungen zu validieren und alle Fehler anzuzeigen, die mit den neuen Zuordnungen verknüpft sein könnten. Wählen Sie **Speichern** aus, sobald die Zuordnung abgeschlossen ist.

   ![Dialogfeld „Schemazuordnung“ mit einem Dropdown-Menü zur Auswahl eines Zielschemas.](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. Ordnen Sie weiterhin alle Felder in den Schemata zu. Wenn das Schema ein [Ereignisschema](/help/xdm/classes/experienceevent.md) ist, wird im Dialogfeld ein Dropdown-Menü angezeigt, in dem Sie alle Ereignisschemata in der Ziel-Sandbox anzeigen können.

   ![Wählen Sie ein Zielschema aus dem Dropdown-Menü aus](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. Wählen Sie ein Schema aus den verfügbaren Schemata in der **Ziel-Sandbox** aus.

   ![Schema auswählen](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. Schließen Sie die Zuordnung ab und wählen Sie **Speichern**.

   ![Zuordnung speichern](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. Nachdem Sie die Zuordnung aller Felder in den Schemata abgeschlossen haben, klicken Sie auf **Beenden**, um den Import-Workflow abzuschließen.

   ![Fluss beenden](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > Sie können mit Ausnahme der Schemata keine Assets ändern, da dies eine inspirierende Sandbox ist, sie werden jedoch als Abhängigkeiten des Pakets angezeigt.

### Importstatus {#import-status}

1. Sie werden automatisch zur Seite [**Importe**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details) weitergeleitet, auf der Sie den Fortschritt Ihres Imports sehen können.

   ![Seite mit dem Importfortschritt](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. Beim Importieren des Pakets werden die Assets des Pakets in der Ziel-Sandbox erstellt. Anschließend verweisen sie auf die Felder, die Sie während des Importvorgangs zugeordnet haben. Der Prozess ist jetzt abgeschlossen und die Assets aus der inspirierenden Sandbox sind jetzt auch in Ihrer Ziel-Sandbox vorhanden, damit Sie sie testen können.

   ![Generierte Assets in der Ziel-Sandbox](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## Nächste Schritte

Nach dem Lesen dieses Handbuchs haben Sie jetzt ein besseres Verständnis davon, wie Sie Anwendungsfall-Playbooks zusammen mit [Sandbox-Tools](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details) nutzen können, um ausführbare Journey zu erstellen, die auf Ihre Schemata verweisen. Erfahren Sie mehr über die häufigsten [Real-Time CDP-Anwendungsfälle](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md).
