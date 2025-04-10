---
title: Benutzerhandbuch für Benutzeroberfläche zu Zusammenführungsrichtlinien
type: Documentation
description: Erfahren Sie, wie Sie mithilfe der Benutzeroberfläche von Adobe Experience Platform mit Zusammenführungsrichtlinien arbeiten.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 77%

---


# Benutzerhandbuch für Benutzeroberfläche zu Zusammenführungsrichtlinien

Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen zusammenführen und kombinieren, damit Sie sich eine vollständige Ansicht über jeden einzelnen Ihrer Kunden verschaffen können. Beim Zusammenführen dieser Daten dienen Zusammenführungsrichtlinien als jene Regeln, [!DNL Experience Platform] mit denen bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden sollen, um eine Übersicht zu schaffen.

Über die RESTful APIs oder die Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen einrichten. Dieses Handbuch enthält schrittweise Anleitungen zum Verwenden von Zusammenführungsrichtlinien mit der Benutzeroberfläche von Adobe Experience Platform.

Um mehr über Zusammenführungsrichtlinien und ihre Rolle in der Experience Platform zu erfahren, lesen Sie zunächst die [Übersicht über Zusammenführungsrichtlinien](overview.md).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis mehrerer wichtiger [!DNL Experience Platform] Funktionen voraus. Bevor Sie dieses Benutzerhandbuch lesen, lesen Sie bitte die Dokumentation für folgende Dienste:

* [Echtzeit-Kundenprofil](../home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Ermöglicht es Echtzeit-Kundenprofil, Identitäten aus unterschiedlichen Datenquellen zu verbinden, die in [!DNL Experience Platform] aufgenommen werden.
* [Experience-Datenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.

## Zusammenführungsrichtlinien anzeigen {#view-merge-policies}

>[!CONTEXTUALHELP]
>id="platform_errors_uplib_101221_404"
>title="Zusammenführungsrichtlinie nicht gefunden"
>abstract="Das bedeutet, dass die angeforderte Zusammenführungsrichtlinie von Experience Platform nicht gefunden wurde. Versuchen Sie eine der folgenden Lösungen, um diesen Fehler zu beheben:<ul><li>Stellen Sie sicher, dass die richtige Zusammenführungsrichtlinien-ID in der URL aufgeführt ist.</li><li>Stellen Sie sicher, dass Sie über die richtige Kombination aus Organisation und Sandbox für die Zusammenführungsrichtlinie verfügen, auf die Sie zugreifen möchten.</li></ul>"

In der [!DNL Experience Platform] Benutzeroberfläche können Sie mit Zusammenführungsrichtlinien beginnen, indem Sie im linken Navigationsbereich **[!UICONTROL Profile]** auswählen und dann die Registerkarte **[!UICONTROL Zusammenführungsrichtlinien]** auswählen.

Diese Registerkarte enthält eine Liste aller vorhandenen Zusammenführungsrichtlinien für Ihre Organisation sowie Details für jede Zusammenführungsrichtlinie, einschließlich des Richtliniennamen, ob die Zusammenführungsrichtlinie die standardmäßige Zusammenführungsrichtlinie ist oder nicht, sowie die Schemaklasse, auf die sich die Zusammenführungsrichtlinie bezieht.

![Die Seite zum Durchsuchen von Zusammenführungsrichtlinien wird angezeigt.](../images/merge-policies/landing.png)

Um zu entscheiden, welche Details angezeigt werden sollen, oder um der Anzeige weitere Spalten hinzuzufügen, wählen Sie ![das Symbol Spalteneinstellungen ](../../images/icons/column-settings.png) und wählen Sie einen Spaltennamen aus, um ihn der Ansicht hinzuzufügen oder daraus zu entfernen.

![Die verfügbaren Optionen zum Anpassen der Seite zum Durchsuchen von Zusammenführungsrichtlinien werden angezeigt.](../images/merge-policies/adjust-view.png)

## Zusammenführungsrichtlinie erstellen {#create-a-merge-policy}

Um eine neue Zusammenführungsrichtlinie zu erstellen, wählen Sie auf der Registerkarte „Zusammenführungsrichtlinien“ die Option **[!UICONTROL Zusammenführungsrichtlinie erstellen]** aus, um den neuen Workflow für Zusammenführungsrichtlinien einzugeben.

![Landingpage für Zusammenführungsrichtlinien mit hervorgehobener Schaltfläche „Erstellen“.](../images/merge-policies/create-new.png)

Für den Workflow **[!UICONTROL Neue Zusammenführungsrichtlinie]** müssen Sie mithilfe einer Reihe von geführten Schritten wichtige Informationen für Ihre neue Zusammenführungsrichtlinie angeben. Diese Schritte werden in den folgenden Abschnitten beschrieben.

![Der neue Workflow für Zusammenführungsrichtlinien.](../images/merge-policies/create.png)

## [!UICONTROL Konfigurieren] {#configure}

Im ersten Schritt des Workflows können Sie Ihre Zusammenführungsrichtlinie konfigurieren, indem Sie grundlegende Informationen angeben. Zu diesen Informationen gehören:

* **[!UICONTROL Name]**: Der Name Ihrer Zusammenführungsrichtlinie sollte beschreibend, aber kurz sein.
* **[!UICONTROL Schema class]**: Die XDM-Schemaklasse, die der Zusammenführungsrichtlinie zugeordnet ist. Damit wird das Schemaklasse angegeben, für das die Zusammenführungsrichtlinie erstellt wird. Organisationen können mehrere Zusammenführungsrichtlinien pro Schemaklasse erstellen. Derzeit ist in der Benutzeroberfläche nur die Klasse [!UICONTROL XDM Individual Profile] verfügbar. Sie können eine Vorschau des Vereinigungsschemas für die Schemaklasse anzeigen, indem Sie **[!UICONTROL Vereinigungsschema anzeigen]** auswählen. Weitere Informationen finden Sie im folgenden Abschnitt [Anzeigen des Vereinigungsschemas](#view-union-schema).
* **[!UICONTROL ID-Zusammenfügung]**: In diesem Feld wird definiert, wie die verwandten Identitäten eines Kunden ermittelt werden. Es gibt zwei mögliche Werte für die Identitätszuordnung. Es ist wichtig zu verstehen, wie sich die von Ihnen ausgewählte Art der Identitätszuordnung auf Ihre Daten auswirkt. Weitere Informationen finden Sie unter [Übersicht über Zusammenführungsrichtlinien](overview.md).
   * **[!UICONTROL Keine]**: Keine Identitätszusammenfügung durchführen.
   * **[!UICONTROL Privates Diagramm]**: Identitätszusammenfügung basierend auf Ihrem privaten Identitätsdiagramm durchführen.
* **[!UICONTROL Standardmäßige Zusammenführungsrichtlinie]**: Eine Umschalter-Schaltfläche, mit der Sie festlegen können, ob diese Zusammenführungsrichtlinie der Standard für Ihre Organisation sein soll oder nicht. Wenn die Auswahl aktiviert ist, werden Sie in einer Warnung aufgefordert zu bestätigen, dass Sie die standardmäßige Zusammenführungsrichtlinie Ihrer Organisation ändern möchten. Weitere Informationen zu standardmäßigen Zusammenführungsrichtlinien finden Sie unter [Übersicht über Zusammenführungsrichtlinien](overview.md).
  ![Ein Pop-up, in dem erläutert wird, was passiert, wenn die Zusammenführungsrichtlinie als standardmäßige Zusammenführungsrichtlinie festgelegt ist.](../images/merge-policies/create-make-default.png)
* **[!UICONTROL Zusammenführungsrichtlinie „Active-On-Edge“]**: Ein Umschalt-Button, mit dem Sie festlegen können, ob diese Zusammenführungsrichtlinie in den Randbereichen aktiv sein soll oder nicht. Um sicherzustellen, dass alle Profilnutzer in den Randbereichen mit derselben Ansicht arbeiten, können Zusammenführungsrichtlinien als am Rand aktiv markiert werden. Damit eine Zielgruppe in Edge aktiviert (als Edge-Zielgruppe markiert) werden kann, muss sie an eine Zusammenführungsrichtlinie gebunden sein, die als in Edge aktiv markiert ist. Wenn eine Zielgruppe **nicht** mit einer Zusammenführungsrichtlinie verknüpft ist, die als im Randbereich aktiv markiert ist, wird die Zielgruppe nicht als im Randbereich aktiv, sondern als Streaming-Zielgruppe markiert. Darüber hinaus kann jede Sandbox in einer Organisation nur über **eine** Zusammenführungsrichtlinie verfügen, die im Randbereich aktiv ist.

Nachdem die erforderlichen Felder ausgefüllt wurden, können Sie **[!UICONTROL Weiter]** auswählen, um mit dem Workflow fortzufahren.

![Ein abgeschlossener Bildschirm Konfigurieren mit hervorgehobener Schaltfläche Weiter.](../images/merge-policies/create-complete.png)

## [!UICONTROL Vereinigungsschema anzeigen] {#view-union-schema}

Beim Erstellen oder Bearbeiten einer Zusammenführungsrichtlinie können Sie das Vereinigungsschema für die ausgewählte Schemaklasse durch die Auswahl von **[!UICONTROL Vereinigungsschema anzeigen]** anzeigen.

![Die Schaltfläche „Vereinigungsschema anzeigen“ ist im Workflow „Neue Zusammenführungsrichtlinie“ hervorgehoben.](../images/merge-policies/view-union-schema.png)

Dadurch wird das Dialogfeld [!UICONTROL Vereinigungsschema anzeigen] geöffnet, in dem alle beitragenden Schemata, Identitäten und Beziehungen angezeigt werden, die mit dem Vereinigungsschema verknüpft sind. Sie können das Dialogfeld verwenden, um das Vereinigungsschema auf die gleiche Weise zu untersuchen, wie Sie dies tun, indem Sie auf die Registerkarte [!UICONTROL Vereinigungsschema] im Abschnitt [!UICONTROL Profile] der Experience Platform-Benutzeroberfläche zugreifen.

Detaillierte Informationen zu Vereinigungsschemata, einschließlich der Interaktion mit ihnen im [!UICONTROL Vereinigungsschema]-Tab oder im Dialogfeld [!UICONTROL Vereinigungsschema anzeigen], das im Workflow für Zusammenführungsrichtlinien angezeigt wird, finden Sie im Handbuch [Vereinigungs-Schema-Benutzeroberfläche](../ui/union-schema.md).

![Das Dialogfeld Vereinigungsschema anzeigen.](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL Profil-Datensätze auswählen] {#select-profile-datasets}

Wählen Sie im Bildschirm **[!UICONTROL Profil-Datensätze]** die **[!UICONTROL Zusammenführungsmethode]** aus, die Sie für Ihre Zusammenführungsrichtlinie verwenden möchten. Auf dem Bildschirm wird auch die Gesamtzahl der [!UICONTROL Profil-Datensätze] in Ihrer Organisation angezeigt, die sich auf die Schemaklasse beziehen, die im vorherigen Bildschirm ausgewählt wurde.

Abhängig von der gewählten Zusammenführungsmethode werden alle Profildatensätze mit der Reihenfolge zusammengeführt, in der sie zuletzt aktualisiert wurden (Zeitstempel sortiert). Andernfalls müssen Sie auswählen, welche Profildatensätze in die Zusammenführungsrichtlinie aufgenommen werden sollen und in welcher Reihenfolge sie zusammengeführt werden sollen (Datensatzpriorität).

Weiterführende Informationen zu Zusammenführungsmethoden finden Sie in der [Übersicht über Zusammenführungsrichtlinien](overview.md).

>[!BEGINTABS]

>[!TAB Zeitstempel geordnet]

Wenn Sie **[!UICONTROL Zeitstempel ordered]** als Zusammenführungsmethode auswählen, haben Attribute aus den zuletzt aktualisierten Datensätzen Vorrang. Dies gilt für alle Profildatensätze.

>[!NOTE]
>
>Die Zahl in Klammern neben **[!UICONTROL Profildatensätze]** (z. B. `(37)` in der Abbildung) zeigt die Gesamtanzahl der einzuschließenden Profildatensätze an.

![Ein Bild, das die ausgewählte Zusammenführungsmethode Zeitstempel geordnet anzeigt.](../images/merge-policies/timestamp-ordered.png)

>[!TAB Datensatzpriorität]

Wenn Sie **[!UICONTROL Datensatzpriorität]** als Zusammenführungsmethode auswählen, müssen Sie Profildatensätze auswählen und diese manuell priorisieren. Jeder aufgelistete Datensatz enthält auch den Status des zuletzt erfassten Batches oder zeigt an, dass keine Batches in diesen Datensatz aufgenommen wurden.

Sie können bis zu 50 Datensätze aus der Datensatzliste auswählen, die in die Zusammenführungsrichtlinie aufgenommen werden sollen.

>[!NOTE]
>
>Die Zahl in eckigen Klammern neben **[!UICONTROL Profildatensätze]** (z. B. `(37)` in der Abbildung) zeigt die Gesamtanzahl der zur Auswahl verfügbaren Profildatensätze an.

Wenn Datensätze ausgewählt sind, werden sie zum Abschnitt **[!UICONTROL Datensätze auswählen]** hinzugefügt, sodass Sie die Datensätze per Drag-and-Drop verschieben und entsprechend Ihrer gewünschten Priorität sortieren können. Da die Datensätze in der Liste angepasst werden, wird die Ordinalzahl (1, 2, 3 usw.) neben dem Datensatz aktualisiert und zeigt die Priorität an (1 erhält die höchste Priorität, 2 und höher).

Bei Auswahl eines Datensatzes wird auch der Abschnitt **[!UICONTROL Vereinigungsschema]** aktualisiert und die Felder im Vereinigungsschema angezeigt, zu denen jeder Datensatz Daten beiträgt. Weitere Informationen zu Vereinigungsschemata, einschließlich der Interaktion mit Visualisierungen in der Benutzeroberfläche, finden Sie im [UI-Handbuch für Vereinigungsschemas](../ui/union-schema.md)

![Ein Bild, das die ausgewählte Datensatzpriorität zusammen mit den entsprechenden Einstellungen anzeigt, die Sie auswählen müssen, wenn diese Option aktiviert ist.](../images/merge-policies/dataset-precedence.png)

>[!ENDTABS]

## [!UICONTROL ExperienceEvent-Datensätze auswählen] {#select-experienceevent-datasets}

Für den nächsten Schritt im Workflow müssen Sie ExperienceEvent-Datensätze auswählen. Dieser Bildschirm wird von der Zusammenführungsmethode beeinflusst, die Sie auf dem Bildschirm [[!UICONTROL Profil-Datensätze auswählen]](#select-profile-datasets) ausgewählt haben.

>[!BEGINTABS]

>[!TAB Zeitstempel geordnet]

Wenn Sie **[!UICONTROL Zeitstempel ordered]** als Zusammenführungsmethode für Profildatensätze ausgewählt haben, haben auch hier die Attribute aus den zuletzt aktualisierten ExperienceEvent-Datensätzen Vorrang.

>[!NOTE]
>
>Die Zahl in eckigen Klammern neben **[!UICONTROL ExperienceEvent-Datensätze]** (z. B. `(1)` in der Abbildung) zeigt die Gesamtzahl der von Ihrem Unternehmen erstellten ExperienceEvent-Datensätze, die sich auf die Schemaklasse beziehen, die Sie im Konfigurationsbildschirm für Zusammenführungsrichtlinien ausgewählt haben.

![Die Gesamtzahl der ExperienceEvent-Datensätze, die sich auf die Schemaklasse beziehen können, wird angezeigt.](../images/merge-policies/timestamp-experienceevent.png)

>[!TAB Datensatzpriorität]

Wenn Sie **[!UICONTROL Datensatzpriorität]** als Zusammenführungsmethode für Profildatensätze ausgewählt haben, müssen Sie ExperienceEvent-Datensätze auswählen, die einbezogen werden sollen. Sie können bis zu 50 ExperienceEvent-Datensätze aus der Datensatzliste auswählen.

>[!NOTE]
>
>Die Zahl in eckigen Klammern neben **[!UICONTROL ExperienceEvent-Datensätze]** (z. B. `(1)` in der Abbildung) zeigt die Gesamtzahl der von Ihrem Unternehmen erstellten ExperienceEvent-Datensätze, die sich auf die Schemaklasse beziehen, die Sie im Konfigurationsbildschirm für Zusammenführungsrichtlinien ausgewählt haben.

Wenn Datensätze ausgewählt sind, werden sie im Abschnitt [!UICONTROL Datensätze auswählen] angezeigt.

ExperienceEvent-Datensätze können nicht manuell sortiert werden. Stattdessen werden die Attribute in den ExperienceEvent-Datensätzen an die Profil-Datensätze angehängt, wenn sie Teil desselben Profilfragments sind.

Ähnlich wie bei der Auswahl von Profildatensätzen wird durch die Auswahl eines ExperienceEvent-Datensatzes auch der Abschnitt **[!UICONTROL Vereinigungsschema]** aktualisiert und die Felder im Vereinigungsschema angezeigt, zu denen jeder Datensatz Daten beiträgt. Weitere Informationen zu Vereinigungsschemata, einschließlich der Interaktion mit Visualisierungen in der Benutzeroberfläche, finden Sie im [Handbuch zur Benutzeroberfläche des Vereinigungsschemas](../ui/union-schema.md).

![Die auswählbaren ExperienceEvent-Datensätze werden angezeigt.](../images/merge-policies/dataset-precedence-experienceevent.png)

>[!ENDTABS]

## [!UICONTROL Überprüfung] {#review}

Der letzte Schritt im Workflow besteht darin, Ihre Zusammenführungsrichtlinie zu überprüfen. Der Bildschirm **[!UICONTROL Überprüfung]** enthält Informationen zu Ihrer Zusammenführungsrichtlinie, einschließlich der ausgewählten ID-Zuordnungsmethode, der ausgewählten Zusammenführungsmethode und der eingeschlossenen Datensätze. (Um alle enthaltenen Profile- oder ExperienceEvent-Datensätze anzuzeigen, wählen Sie die Anzahl der Datensätze aus, um die Dropdown-Liste zu erweitern.)

Auf dem Überprüfungsbildschirm finden Sie auch die Tabelle **[!UICONTROL Daten in der Vorschau]**, die Beispieldatensätze von Profilen mit Ihrer Zusammenführungsrichtlinie anzeigt. Auf diese Weise können Sie vor dem Speichern Ihrer Zusammenführungsrichtlinie eine Vorschau des Kundenprofils anzeigen.

Stellen Sie sicher, dass Sie die Konfiguration Ihrer Zusammenführungsrichtlinien sorgfältig überprüfen und Daten in der Vorschau anzeigen, bevor Sie **[!UICONTROL Beenden]** auswählen, um den Erstellungsarbeitsablauf abzuschließen.

>[!BEGINTABS]

>[!TAB Zeitstempel geordnet]

Wenn Sie **[!UICONTROL Zeitstempel ordered]** als Zusammenführungsmethode für Ihre Zusammenführungsrichtlinie ausgewählt haben, enthält die Liste der Profildatensätze alle Datensätze, die von Ihrer Organisation im Zusammenhang mit der Schemaklasse erstellt wurden, in der Reihenfolge des Zeitstempels. Die Liste der ExperienceEvent-Datensätze enthält alle Datensätze, die Ihr Unternehmen für die ausgewählte Schemaklasse erstellt hat, und wird an die Profil-Datensätze angehängt.

Die Tabelle **[!UICONTROL Vorschau der Daten]** zeigt Beispielprofildatensätze basierend auf einer Zeitstempelreihenfolge der Datensätze an. Auf diese Weise können Sie vor dem Speichern Ihrer Zusammenführungsrichtlinie eine Vorschau des Kundenprofils anzeigen.

Wählen Sie **[!UICONTROL Beenden]** aus, um Ihre neue Zusammenführungsrichtlinie zu erstellen.

![Die Überprüfungsseite wird angezeigt. Auf dieser Seite können Sie die Details Ihrer neu erstellten Zusammenführungsrichtlinie überprüfen.](../images/merge-policies/timestamp-review.png)

>[!TAB Datensatzpriorität]

Wenn Sie **[!UICONTROL Datensatzpriorität]** als Zusammenführungsmethode für Ihre Zusammenführungsrichtlinie ausgewählt haben, enthalten die Listen der Profile- und ExperienceEvent-Datensätze nur die Profil- und ExperienceEvent-Datensätze, die Sie während des Erstellungsarbeitsablaufs ausgewählt haben. Die Reihenfolge der Profildatensätze sollte mit der Priorität übereinstimmen, die Sie bei der Erstellung angegeben haben. Ist dies nicht der Fall, verwenden Sie die Schaltfläche [!UICONTROL Zurück], um zu den vorherigen Workflow-Schritten zurückzukehren und die Priorität anzupassen.

Die Tabelle **[!UICONTROL Datenvorschau]** zeigt Beispieldatensätze mit Profildatensätzen unter Verwendung der ausgewählten Datensätze an. Auf diese Weise können Sie vor dem Speichern Ihrer Zusammenführungsrichtlinie eine Vorschau des Kundenprofils anzeigen.

Wählen Sie **[!UICONTROL Beenden]** aus, um Ihre neue Zusammenführungsrichtlinie zu erstellen.

![Die Überprüfungsseite wird angezeigt. Auf dieser Seite können Sie die Details Ihrer neu erstellten Zusammenführungsrichtlinie überprüfen.](../images/merge-policies/dataset-precedence-review.png)

>[!ENDTABS]

## Zusammenführungsrichtlinie bearbeiten {#edit}

Auf der Registerkarte [!UICONTROL Zusammenführungsrichtlinien] können Sie eine vorhandene Zusammenführungsrichtlinie ändern, die für die Klasse [!DNL XDM Individual Profile] erstellt wurde, indem Sie **[!UICONTROL Richtlinienname]** für die Zusammenführungsrichtlinie auswählen, die Sie bearbeiten möchten.

Wenn der Bildschirm **[!UICONTROL Zusammenführungsrichtlinie bearbeiten]** angezeigt wird, können Sie Änderungen am Namen [!UICONTROL ID-Zusammenfügungstyp] und Attributzusammenführungstyp vornehmen und festlegen, ob die Richtlinie als standardmäßige Zusammenführungsrichtlinie für Ihre Organisation dienen soll oder nicht.

Wählen Sie **[!UICONTROL Weiter]** aus, um den Arbeitsablauf für Zusammenführungsrichtlinien zu durchlaufen und die in der Zusammenführungsrichtlinie enthaltene Zusammenführungsmethode und Datensätze zu aktualisieren.

![Der Workflow Zusammenführungsrichtlinie bearbeiten wird angezeigt.](../images/merge-policies/edit-screen.png)

Nachdem Sie die erforderlichen Änderungen vorgenommen haben, überprüfen Sie Ihre Zusammenführungsrichtlinie und wählen Sie **[!UICONTROL Beenden]** aus, um Ihre Änderungen zu speichern und zur Registerkarte [!UICONTROL Zusammenführungsrichtlinien] zurückzukehren.

>[!WARNING]
>
>Das Ändern einer Zusammenführungsrichtlinie kann sich auf die Segmentierung und die Profilergebnisse auswirken, da dadurch die Art und Weise verändert wird, wie Datenkonflikte gelöst werden. Prüfen Sie die Änderungen an Ihren Zusammenführungsrichtlinien sorgfältig, bevor Sie sie speichern.

![Die Überprüfungsseite für den Workflow „Richtlinie bearbeiten“ wird angezeigt.](../images/merge-policies/edit-review.png)

## Verstöße gegen Data Governance-Richtlinien

Beim Erstellen oder Aktualisieren einer Zusammenführungsrichtlinie wird geprüft, ob die Zusammenführungsrichtlinie eine der von Ihrer Organisation definierten Datennutzungsrichtlinien verletzt. Datennutzungsrichtlinien sind Teil von Adobe Experience Platform Data Governance und stellen Regeln dar, die die Arten von Marketing-Aktionen beschreiben, die Sie für bestimmte [!DNL Experience Platform] ausführen dürfen oder nicht.

Wenn zum Beispiel eine Zusammenführungsrichtlinie zum Erstellen einer Zielgruppe verwendet wurde, die für ein Drittanbieterziel aktiviert wurde, und Ihre Organisation eine Datennutzungsrichtlinie aufwiese, die den Export bestimmter Daten an Dritte verhinderte, würden Sie beim Versuch, Ihre Zusammenführungsrichtlinie zu speichern, eine **[!UICONTROL Verletzung der Data Governance]** Richtlinie erkannt) erhalten.

Diese Benachrichtigung enthält eine Liste der Datennutzungsrichtlinien, die verletzt wurden, und ermöglicht Ihnen das Anzeigen von Details zur Verletzung, indem Sie eine Richtlinie aus der Liste auswählen. Bei Auswahl einer verletzten Richtlinie liefert der Tab **[!UICONTROL Datenverlaufskontrolle]** den Grund für die Verletzung und die betroffenen Aktivierungen. So erhalten Sie genauere Details zur Verletzung der jeweiligen Datennutzungsrichtlinie.

Um mehr über Data Governance in Adobe Experience Platform zu erfahren, lesen Sie zunächst den [Überblick zu Data Governance](../../data-governance/home.md).

## Nächste Schritte

Nachdem Sie Zusammenführungsrichtlinien für Ihr Unternehmen erstellt und konfiguriert haben, können Sie sie verwenden, um die Ansicht von Kundenprofilen in Experience Platform anzupassen und aus Ihren Profildaten Zielgruppen zu erstellen. Weitere Informationen [ Erstellen und Verwenden von Audiences mithilfe der [!DNL Experience Platform]-Benutzeroberfläche und von APIs finden Sie in der ](../../segmentation/home.md)Segmentierungsübersicht) .
