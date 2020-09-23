---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: Benutzerhandbuch zu Zusammenführungsrichtlinien
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 36%

---


# Benutzerhandbuch zu Zusammenführungsrichtlinien

Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen zusammenführen und kombinieren, damit Sie sich einen kompletten Überblick über einzelne Kunden verschaffen können. When bringing this data together, merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be combined to create that unified view.

Über die RESTful APIs oder die Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen einrichten. Dieses Handbuch enthält schrittweise Anleitungen zum Verwenden von Zusammenführungsrichtlinien mit der Benutzeroberfläche von Adobe Experience Platform.

If you would prefer to work with merge policies using the [!DNL Real-time Customer Profile] API, please follow the instructions outlined in the [merge policies API tutorial](../api/merge-policies.md).

## Erste Schritte

This guide requires a working understanding of the various [!DNL Experience Platform] services involved with merge policies. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [[!DNL Echtzeit-Profil]](../home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL-Identitätsdienst]](../../identity-service/home.md): Ermöglicht [!DNL Real-time Customer Profile] die Überbrückung von Identitäten aus unterschiedlichen Datenquellen, in die Daten eingehen [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Platform] organisiert werden.

## Zusammenführungsrichtlinien anzeigen

Within the [!DNL Experience Platform] user interface, you can begin to work with merge policies and see a list of your organization&#39;s existing merge policies by selecting **[!UICONTROL Profiles]** in the left-rail and then selecting the **[!UICONTROL Merge policies]** tab.

![Landingpage für Zusammenführungsrichtlinien](../images/merge-policies/landing.png)

Details for each merge policy available to your organization are visible on the landing page, including the [!UICONTROL Policy Name], [!UICONTROL Default merge policy], and [!UICONTROL Schema].

Um auszuwählen, welche Details sichtbar sind, oder um der Anzeige weitere Spalten hinzuzufügen, wählen Sie das Symbol für die Spaltenauswahl aus und klicken Sie auf einen Spaltennamen, um diese der Ansicht hinzuzufügen oder zu entfernen.

![](../images/merge-policies/adjust-view.png)

## Zusammenführungsrichtlinie erstellen

Um eine neue Richtlinie zum Zusammenführen zu erstellen, wählen Sie &quot; **[!UICONTROL Richtlinie]** zum Zusammenführen erstellen&quot;.

![Landingpage für Zusammenführungsrichtlinien](../images/merge-policies/create-new.png)

Der Bildschirm **[!UICONTROL Zusammenführungsrichtlinie erstellen]** wird angezeigt, in dem Sie wichtige Daten für Ihre neue Zusammenführungsrichtlinie angeben können.

![](../images/merge-policies/create.png)

* **[!UICONTROL Name]**: Der Name Ihrer Zusammenführungsrichtlinie sollte beschreibend, aber kurz sein.
* **[!UICONTROL Schema]**: Das mit der Zusammenführungsrichtlinie verknüpfte Schema. Damit wird das XDM-Schema angegeben, für das die Zusammenführungsrichtlinie erstellt wird. Organisationen können mehrere Zusammenführungsrichtlinien pro Schema erstellen.
* **[!UICONTROL ID-Zusammenfügung]**: In diesem Feld wird definiert, wie die verwandten Identitäten eines Kunden ermittelt werden. Es gibt zwei mögliche Werte:
   * **[!UICONTROL Keine]**: Keine Identitätszusammenfügung durchführen.
   * **[!UICONTROL Privates Diagramm]**: Identitätszusammenfügung basierend auf Ihrem privaten Identitätsdiagramm durchführen.
* **[!UICONTROL Attributzusammenführung]**: Ein Profil-Fragment enthält Informationen zu nur einer Identität aus der Liste von Identitäten, die für einen einzelnen Kunden vorhanden sind. Wenn der verwendete Identitätsdiagrammtyp zu mehr als einer Identität führt, besteht die Möglichkeit kollidierender Profil-Attribute, und die Priorität muss angegeben werden. Using [!UICONTROL Attribute merge] allows you to specify which dataset profile values to prioritize if a merge conflict occurs between key-value (record data) type datasets. Es gibt zwei mögliche Werte:
   * **[!UICONTROL Zeitstempel bestellt]**: Im Ereignis eines Konflikts wird dem zuletzt aktualisierten Profil Vorrang eingeräumt. [!UICONTROL Der bestellte] Zeitstempel unterstützt auch benutzerdefinierte Zeitstempel, die beim Zusammenführen von Daten innerhalb desselben Datensatzes (mehrere Identitäten) oder über Datasets hinweg Vorrang vor Systemzeitstempeln haben. Weitere Informationen finden Sie im folgenden Abschnitt mit dem [Zeitstempel](#timestamp-ordered) .
   * **[!UICONTROL Datensatzpriorität]** : Geben Sie im Ereignis eines Konflikts den Fragmenten des Profils Priorität, die auf dem Datensatz basieren, aus dem sie stammen. Bei Auswahl dieser Option müssen Sie die zugehörigen Datensätze und deren Reihenfolge der Priorität auswählen. Weiterführende Informationen finden Sie unten in den Details zur [Datensatzpriorität](#dataset-precedence).
* **[!UICONTROL Standardmäßige Zusammenführungsrichtlinie]**: Eine Umschalter-Schaltfläche, mit der Sie festlegen können, ob diese Zusammenführungsrichtlinie der Standard für Ihre Organisation sein soll oder nicht. Wenn der Selektor aktiviert ist und Sie die neue Richtlinie speichern, wird Ihre vorherige Standardrichtlinie automatisch so aktualisiert, dass sie nicht mehr der Standard ist.

### Zeitstempel sortiert {#timestamp-ordered}

Während Profil-Datensätze in die Experience Platform aufgenommen werden, wird zum Zeitpunkt der Erfassung ein Systemzeitstempel abgerufen und dem Datensatz hinzugefügt. Wenn als [!UICONTROL Attributzusammenführungstyp für eine Zusammenführungsrichtlinie der sortierte] [!UICONTROL Zeitstempel] ausgewählt ist, werden die Profil basierend auf dem Systemzeitstempel zusammengeführt. Das heißt, das Zusammenführen erfolgt auf der Grundlage des Zeitstempels für den Zeitpunkt, zu dem der Datensatz in die Plattform aufgenommen wurde.

Gelegentlich kann es zu Anwendungsfällen kommen, bei denen ein benutzerdefinierter Zeitstempel bereitgestellt werden muss und bei denen die Richtlinie zum Zusammenführen den benutzerdefinierten Zeitstempel und nicht den Systemzeitstempel berücksichtigen muss. Dazu gehören beispielsweise das Aufstocken von Daten oder das Sicherstellen der richtigen Reihenfolge von Ereignissen, wenn die Datensätze nicht mehr in der richtigen Reihenfolge angezeigt werden.

>[!NOTE]
>
>Diese Funktion steht nur zur Erfassung über Datensätze hinweg zur Verfügung. Wenn die Datensätze mit demselben Datensatz erfasst werden, tritt das standardmäßige Austauschverhalten auf.

### Verwenden benutzerdefinierter Zeitstempel {#custom-timestamps}

Um einen benutzerdefinierten Zeitstempel zu verwenden, muss das [!UICONTROL externe Quellsystem-Audit-Details-Mixin] Ihrem Profil-Schema hinzugefügt werden. Nach dem Hinzufügen kann der benutzerdefinierte Zeitstempel mithilfe des `lastUpdatedDate` Felds ausgefüllt werden.

Wenn ein Datensatz mit dem ausgefüllten `lastUpdatedDate` Feld erfasst wird, verwendet die Experience Platform dieses Feld, um Datensätze über Datensätze hinweg zusammenzuführen. Wenn `lastUpdatedDate` kein oder kein Ausfüllen erfolgt, verwendet Platform weiterhin den Systemzeitstempel.

>[!NOTE]
>
>Sie müssen sicherstellen, dass der `lastUpdatedDate` Zeitstempel aufgefüllt wird, wenn Sie eine Aktualisierung für denselben Datensatz vornehmen.

Im folgenden Screenshot werden die Felder im [!UICONTROL Audit-Details des externen Quellsystems angezeigt]. Eine schrittweise Anleitung zum Arbeiten mit Schemas in der Benutzeroberfläche, einschließlich dem Hinzufügen von Mixins zu Schemas, finden Sie im [Lernprogramm zum Erstellen eines Schemas mit der Benutzeroberfläche](../../xdm/tutorials/create-schema-ui.md).

![](../images/merge-policies/custom-timestamp-mixin.png)

Informationen zum Arbeiten mit benutzerdefinierten Zeitstempeln mithilfe der API finden Sie im Anhang des Endpunktanzeigers [für](../api/merge-policies.md) Zusammenführungsrichtlinien und im Abschnitt zur [Verwendung benutzerdefinierter Zeitstempel](../api/merge-policies.md#custom-timestamps).

### Datensatzpriorität {#dataset-precedence}

Wenn Sie einen Wert für [!UICONTROL Attributzusammenführung] auswählen, können Sie die [!UICONTROL Datensatzpriorität] festlegen, um Profilfragmenten je nach dem Datensatz, aus dem sie stammen, Priorität einzuräumen.

Ein Beispiel bestünde darin, wenn es in Ihrer Organisation Daten in einem Datensatz gibt, die bevorzugt werden oder vertrauenswürdiger sind als Daten in einem anderen Datensatz.

Wenn Sie die [!UICONTROL Datensatzpriorität]auswählen, wird ein separates Fenster geöffnet, in dem Sie aus den [!UICONTROL verfügbaren Datensätzen] auswählen müssen, welche Datensätze einbezogen werden (oder das Kontrollkästchen verwenden, um alle auszuwählen). Sie können die Datensätze dann per Drag &amp; Drop in das Bedienfeld [!UICONTROL Ausgewählte Datensätze] und dann in die richtige Prioritätsreihenfolge ziehen. Der oberste Datensatz erhält die höchste Priorität, der zweite Datensatz wird die zweithöchste sein usw.

![](../images/merge-policies/dataset-precedence.png)

Once you have finished creating the merge policy, select **[!UICONTROL Save]** to return to the [!UICONTROL Merge policies] tab where your new merge policy now appears in the list of policies.

## Zusammenführungsrichtlinie bearbeiten

You can modify an existing merge policy through the [!UICONTROL Merge policies] tab by selecting the **[!UICONTROL Policy name]** for the merge policy you wish to edit.

![Landingpage für Zusammenführungsrichtlinien](../images/merge-policies/select-edit.png)

Wenn der Bildschirm **[!UICONTROL Zusammenführungsrichtlinie bearbeiten]** angezeigt wird, können Sie Änderungen am [!UICONTROL Namen], [!UICONTROL Schema], [!UICONTROL ID-Zusammenfügungstyp] und [!UICONTROL Attributzusammenführungstyp] vornehmen und festlegen, ob die Richtlinie als [!UICONTROL standardmäßige Zusammenführungsrichtlinie] für Ihre Organisation dienen soll oder nicht.

>[!NOTE]
>
>Sie können die Kennung der Zusammenführungsrichtlinie, die oben im Bearbeitungsbildschirm angezeigt wird, nicht bearbeiten. Es handelt sich dabei um eine schreibgeschützte, systemgenerierte Kennung, die sich nicht ändern lässt.

![](../images/merge-policies/edit-screen.png)

Once you have made the necessary changes, select **[!UICONTROL Save]** to return to the [!UICONTROL Merge policies] tab where the updated merge policy information is now visible.

![](../images/merge-policies/edited.png)

## Verstöße gegen Data Governance-Richtlinien

Beim Erstellen oder Aktualisieren einer Zusammenführungsrichtlinie wird geprüft, ob die Zusammenführungsrichtlinie eine der von Ihrer Organisation definierten Datennutzungsrichtlinien verletzt. Data usage policies are part of Adobe Experience Platform [!DNL Data Governance] and are rules that describe the kinds of marketing actions that you are allowed to, or restricted from, performing on specific [!DNL Platform] data. For example, if a merge policy was used to create a segment that activated to a third-party destination, and your organization had a data usage policy preventing the export of specific data to third parties, you would receive a &quot;[!UICONTROL Data governance policy violation detected]&quot; notification when attempting to save your merge policy.

Diese Benachrichtigung enthält eine Liste der Datennutzungsrichtlinien, die verletzt wurden, und ermöglicht Ihnen das Anzeigen von Details zur Verletzung, indem Sie eine Richtlinie aus der Liste auswählen. Upon selecting a violated policy, the [!UICONTROL Data lineage] tab provides the reason for the violation and the [!UICONTROL Affected activations], each providing more detail into how the data usage policy has been violated.

Um mehr über Data Governance in Adobe Experience Platform zu erfahren, lesen Sie zunächst den [Überblick zu Data Governance](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Nächste Schritte

Nachdem Sie Zusammenführungsrichtlinien für Ihre IMS-Organisation erstellt und konfiguriert haben, können Sie diese nun verwenden, um Zielgruppensegmente aus Ihren Profildaten zu erstellen. See the [Segmentation overview](../../segmentation/home.md) for more information on how to create and work with segments using [!DNL Experience Platform].