---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Benutzerhandbuch zu Zusammenführungsrichtlinien
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 83%

---


# Benutzerhandbuch zu Zusammenführungsrichtlinien

Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen zusammenführen und kombinieren, um sich einen kompletten Überblick über einzelne Kunden zu verschaffen. When bringing this data together, merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be combined to create that unified view.

Über RESTful-APIs oder die Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihre Organisation einrichten. Dieses Handbuch enthält schrittweise Anleitungen zum Verwenden von Zusammenführungsrichtlinien mit der Benutzeroberfläche von Adobe Experience Platform.

If you would prefer to work with merge policies using the [!DNL Real-time Customer Profile] API, please follow the instructions outlined in the [merge policies API tutorial](../api/merge-policies.md).

## Erste Schritte

This guide requires a working understanding of the various [!DNL Experience Platform] services involved with merge policies. Bevor Sie mit dem Tutorial beginnen, lesen Sie bitte die Dokumentation für folgende Dienste:

* [!DNL Real-time Customer Profile](../home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [!DNL Identity Service](../../identity-service/home.md): Ermöglicht [!DNL Real-time Customer Profile] die Überbrückung von Identitäten aus unterschiedlichen Datenquellen, in die Daten eingehen [!DNL Platform].
* [!DNL Experience Data Model (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Platform] organisiert werden.

## Zusammenführungsrichtlinien anzeigen

Within the [!DNL Experience Platform] user interface, you can begin to work with merge policies and see a list of your organization&#39;s existing merge policies by clicking **[!UICONTROL Profile]** in the left-rail and then selecting the **[!UICONTROL Merge policies]** tab.

![Landingpage für Zusammenführungsrichtlinien](../images/merge-policies/landing.png)

Details zu einzelnen für Ihre Organisation verfügbaren Zusammenführungsrichtlinien finden Sie auf der Landingpage, einschließlich *[!UICONTROL Richtlinienname]*, *[!UICONTROL standardmäßiger Zusammenführungsrichtlinie]* und *[!UICONTROL Schema]*.

Um zu entscheiden, welche Details angezeigt werden sollen, oder um der Anzeige weitere Spalten hinzuzufügen, wählen Sie rechts das Spaltenauswahlsymbol und klicken Sie auf den Spaltennamen, um die gewünschte Spalte der Ansicht hinzuzufügen bzw. zu entfernen.

![](../images/merge-policies/adjust-view.png)

## Zusammenführungsrichtlinie erstellen

Um eine neue Zusammenführungsrichtlinie zu erstellen, klicken Sie oben rechts auf dem Tab **[!UICONTROL Zusammenführungsrichtlinien]** auf **[!UICONTROL Zusammenführungsrichtlinie erstellen]**.

![Landingpage für Zusammenführungsrichtlinien](../images/merge-policies/create-new.png)

Der Bildschirm **[!UICONTROL Zusammenführungsrichtlinie erstellen]** wird angezeigt, in dem Sie wichtige Daten für Ihre neue Zusammenführungsrichtlinie angeben können.

![](../images/merge-policies/create.png)

* **[!UICONTROL Name]**: Der Name Ihrer Zusammenführungsrichtlinie sollte beschreibend, aber kurz sein.
* **[!UICONTROL Schema]**: Das mit der Zusammenführungsrichtlinie verknüpfte Schema. Damit wird das XDM-Schema angegeben, für das die Zusammenführungsrichtlinie erstellt wird. Organisationen können mehrere Zusammenführungsrichtlinien pro Schema erstellen.
* **[!UICONTROL ID-Zusammenfügung]**: In diesem Feld wird definiert, wie die verwandten Identitäten eines Kunden ermittelt werden. Es gibt zwei mögliche Werte:
   * **[!UICONTROL Keine]**: Keine Identitätszusammenfügung durchführen.
   * **[!UICONTROL Privates Diagramm]**: Identitätszusammenfügung basierend auf Ihrem privaten Identitätsdiagramm durchführen.
* **[!UICONTROL Attributzusammenführung]**: Ein Profilfragment besteht aus den Profildaten für nur eine Identität aus der Liste an Identitäten, die für einen einzelnen Kunden bestehen. Wenn der Typ des Identitätsdiagramms Ergebnisse in mehr als einer Identität genutzt hat, können Profileigenschaftswerte kollidieren. Das heißt, dass eine Priorität angegeben werden muss. Mit der *Attributzusammenführung* können Sie festlegen, welche Datensatzprofilwerte bei einem Zusammenführungskonflikt priorisiert werden sollen. Es gibt zwei mögliche Werte:
   * **[!UICONTROL Zeitstempel mit Reihenfolge]**: Bei Konflikten ist das zuletzt aktualisierte Profil mit Priorität zu behandeln.
   * **[!UICONTROL Datensatzpriorität]**: Profilfragmente erhalten anhand des Datensatzes, aus dem sie stammen, Priorität. Bei Auswahl dieser Option müssen Sie die zugehörigen Datensätze und ihre Prioritätsreihenfolge auswählen. Weiterführende Informationen finden Sie unten in den Details zur [Datensatzpriorität](#dataset-precedence).
* **[!UICONTROL Standardmäßige Zusammenführungsrichtlinie]**: Eine Umschalter-Schaltfläche, mit der Sie festlegen können, ob diese Zusammenführungsrichtlinie der Standard für Ihre Organisation sein soll oder nicht. Wenn der Selektor aktiviert ist und Sie die neue Richtlinie speichern, wird Ihre vorherige Standardrichtlinie automatisch so aktualisiert, dass sie nicht mehr der Standard ist.

### Datensatzpriorität {#dataset-precedence}

Wenn Sie einen Wert für *[!UICONTROL Attributzusammenführung]* auswählen, können Sie die *[!UICONTROL Datensatzpriorität]* festlegen, um Profilfragmenten je nach dem Datensatz, aus dem sie stammen, Priorität einzuräumen.

Ein Beispiel bestünde darin, wenn es in Ihrer Organisation Daten in einem Datensatz gibt, die bevorzugt werden oder vertrauenswürdiger sind als Daten in einem anderen Datensatz.

Wenn Sie *[!UICONTROL Datensatzpriorität]* auswählen, wird ein separates Fenster geöffnet, in dem Sie aus *[!UICONTROL verfügbaren Datensätzen]* auswählen müssen (oder das Kontrollkästchen verwenden können, um alle auszuwählen). Dadurch legen Sie fest, welche Datensätze einbezogen werden sollen. Sie können die Datensätze dann per Drag &amp; Drop in das Bedienfeld *[!UICONTROL Ausgewählte Datensätze]* und dann in die richtige Prioritätsreihenfolge ziehen. Der oberste Datensatz erhält die höchste Priorität, der zweite Datensatz erhält die zweithöchste Priorität usw.

![](../images/merge-policies/dataset-precedence.png)

Nachdem Sie die Zusammenführungsrichtlinie erstellt haben, klicken Sie auf **[!UICONTROL Speichern]**, um zum Tab *[!UICONTROL Zusammenführungsrichtlinien]* zurückzukehren. Hier wird Ihre neue Zusammenführungsrichtlinie in der Liste der Richtlinien angezeigt.

## Zusammenführungsrichtlinie bearbeiten

Sie können eine vorhandene Zusammenführungsrichtlinie über den Tab *[!UICONTROL Zusammenführungsrichtlinien]* ändern, indem Sie auf den *[!UICONTROL Richtliniennamen]* für die zu bearbeitende Zusammenführungsrichtlinie klicken.

![Landingpage für Zusammenführungsrichtlinien](../images/merge-policies/select-edit.png)

Wenn der Bildschirm *[!UICONTROL Zusammenführungsrichtlinie bearbeiten]* angezeigt wird, können Sie Änderungen am *[!UICONTROL Namen]*, *[!UICONTROL Schema]*, *[!UICONTROL ID-Zusammenfügungstyp]* und *[!UICONTROL Attributzusammenführungstyp]* vornehmen und festlegen, ob die Richtlinie als *[!UICONTROL standardmäßige Zusammenführungsrichtlinie]* für Ihre Organisation dienen soll oder nicht.

>[!NHinweis]
>Sie können die Kennung der Zusammenführungsrichtlinie, die oben im Bearbeitungsbildschirm angezeigt wird, nicht bearbeiten. Es handelt sich dabei um eine schreibgeschützte, systemgenerierte Kennung, die sich nicht ändern lässt.

![](../images/merge-policies/edit-screen.png)

Nachdem Sie die erforderlichen Änderungen vorgenommen haben, klicken Sie auf **[!UICONTROL Speichern]**, um zum Tab *[!UICONTROL Zusammenführungsrichtlinien]* zurückzukehren. Hier werden die aktualisierten Daten zur Zusammenführungsrichtlinie jetzt angezeigt.

![](../images/merge-policies/edited.png)

## Verstöße gegen Data Governance-Richtlinien

Beim Erstellen oder Aktualisieren einer Zusammenführungsrichtlinie wird geprüft, ob die Zusammenführungsrichtlinie eine der von Ihrer Organisation definierten Datennutzungsrichtlinien verletzt. Data usage policies are part of Adobe Experience Platform [!DNL Data Governance] and are rules that describe the kinds of marketing actions that you are allowed to, or restricted from, performing on specific [!DNL Platform] data. Wenn zum Beispiel eine Zusammenführungsrichtlinie zum Erstellen eines Segments verwendet wurde, das für ein Drittanbieterziel aktiviert wurde, und Ihre Organisation eine Datennutzungsrichtlinie aufwiese, die den Export bestimmter Daten an Dritte verhinderte, würden Sie beim Versuch, Ihre Zusammenführungsrichtlinie zu speichern, eine Benachrichtigung erhalten, dass eine „Verletzung der Data Governance-Richtlinie entdeckt“ wurde.

Diese Benachrichtigung enthält eine Liste der Datennutzungsrichtlinien, die verletzt wurden, und ermöglicht Ihnen das Anzeigen von Details zur Verletzung, indem Sie eine Richtlinie aus der Liste auswählen. Bei Auswahl einer verletzten Richtlinie liefert der Tab *Ermittlung der Datenherkunft* den *Grund für die Verletzung* und die *betroffenen Aktivierungen*. So erhalten Sie genauere Details zur Verletzung der jeweiligen Datennutzungsrichtlinie.

Um mehr über Data Governance in Adobe Experience Platform zu erfahren, lesen Sie zunächst den [Überblick zu Data Governance](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Nächste Schritte

Nachdem Sie Zusammenführungsrichtlinien für Ihre IMS-Organisation erstellt und konfiguriert haben, können Sie diese nun verwenden, um Zielgruppensegmente aus Ihren Profildaten zu erstellen. See the [Segmentation overview](../../segmentation/home.md) for more information on how to create and work with segments using [!DNL Experience Platform].