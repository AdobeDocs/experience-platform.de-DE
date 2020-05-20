---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Richtlinien zusammenführen - Benutzerhandbuch
topic: guide
translation-type: tm+mt
source-git-commit: 3669d740b22b650d4079d83026f122ffee42b9a0
workflow-type: tm+mt
source-wordcount: '1131'
ht-degree: 3%

---


# Richtlinien zusammenführen - Benutzerhandbuch

Mit der Adobe Experience Platform können Sie Daten aus mehreren Quellen zusammenführen und kombinieren, um eine vollständige Ansicht der einzelnen Kunden zu erhalten. Beim Zusammenführen dieser Daten dienen Zusammenführungsrichtlinien als jene Regeln, mit denen Platform bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden sollen, um eine Übersicht zu schaffen.

Mit RESTful-APIs oder der Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen festlegen. Dieses Handbuch enthält schrittweise Anleitungen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der Benutzeroberfläche von Adobe Experience Platform.

Wenn Sie es vorziehen, mit Mergerichtlinien mithilfe der Echtzeit-Customer Profil-API zu arbeiten, befolgen Sie die Anweisungen, die im Lernprogramm zur API- [Zusammenführung](../api/merge-policies.md)beschrieben sind.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der verschiedenen Experience Platform-Dienste, die mit Fusionsrichtlinien verknüpft sind. Bevor Sie mit diesem Lernprogramm beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [Echtzeit-Profil](../home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Identitätsdienst](../../identity-service/home.md): Ermöglicht Kunden-Profil in Echtzeit durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, die in Plattform integriert werden.
* [Erlebnisdatenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.

## Ansicht-Zusammenführungsrichtlinien

In der Benutzeroberfläche von Experience Platform können Sie mit der Arbeit mit Zusammenführungsrichtlinien beginnen und eine Liste der bestehenden Zusammenführungsrichtlinien Ihres Unternehmens anzeigen, indem Sie auf **Profil** in der linken Leiste klicken und dann die Registerkarte Richtlinien **zusammenführen** auswählen.

![Landingpage von Richtlinien zusammenführen](../images/merge-policies/landing.png)

Details zu den einzelnen für Ihr Unternehmen verfügbaren Mergerichtlinien sind auf der Landingpage sichtbar, einschließlich *Richtlinienname*, *Standardrichtlinie* für die Zusammenführung und *Schema*.

Um auszuwählen, welche Details sichtbar sind, oder um der Anzeige weitere Spalten hinzuzufügen, wählen Sie rechts das Spaltenauswahlsymbol aus und klicken Sie auf den Spaltennamen, um es der Ansicht hinzuzufügen oder zu entfernen.

![](../images/merge-policies/adjust-view.png)

## Eine Richtlinie zum Zusammenführen erstellen

Um eine neue Richtlinie für die Zusammenführung zu erstellen, klicken Sie oben rechts auf der Registerkarte &quot;Richtlinien **zusammenführen&quot;auf** Richtlinie **erstellen** .

![Landingpage von Richtlinien zusammenführen](../images/merge-policies/create-new.png)

Der Bildschirm &quot; **Richtlinie** zum Zusammenführen erstellen&quot;wird angezeigt, in dem Sie wichtige Informationen zu Ihrer neuen Richtlinie zum Zusammenführen bereitstellen können.

![](../images/merge-policies/create.png)

* **Name**: Der Name der Zusammenführungsrichtlinie sollte beschreibend, aber knapp sein.
* **Schema**: Das Schema, das mit der Zusammenführungsrichtlinie verknüpft ist. Dies gibt das XDM-Schema an, für das diese Zusammenführungsrichtlinie erstellt wird. Organisationen können mehrere Zusammenführungsrichtlinien pro Schema erstellen.
* **ID-Stich**: In diesem Feld wird definiert, wie die entsprechenden Identitäten eines Kunden ermittelt werden. Es gibt zwei mögliche Werte:
   * **Keine**: Keine Identitätszuordnung durchführen.
   * **Privates Diagramm**: Führen Sie Identitätszuordnungen basierend auf Ihrem privaten Identitätsdiagramm durch.
* **Attributzusammenführung**: Ein Profil-Fragment ist das Profil für nur eine Identität aus der Liste der Identitäten, die für einen einzelnen Kunden vorhanden sind. Wenn der verwendete Identitätsdiagrammtyp zu mehr als einer Identität führt, besteht die Möglichkeit kollidierender Profil-Eigenschaftswerte, und die Priorität muss angegeben werden. Mithilfe der *Attributzusammenführung* können Sie festlegen, welche DataSet-Profil-Werte im Falle eines Zusammenführungskonflikts priorisiert werden sollen. Es gibt zwei mögliche Werte:
   * **Zeitstempel bestellt**: Bei Konflikten ist das zuletzt aktualisierte Profil vorrangig zu behandeln.
   * **Datensatzpriorität** : Weisen Sie Fragmenten des Profils Priorität auf der Grundlage des Datensatzes zu, aus dem sie stammen. Bei Auswahl dieser Option müssen Sie die zugehörigen Datensätze und deren Reihenfolge auswählen. Weitere Informationen finden Sie in den unten stehenden Details zur [Priorität](#dataset-precedence) des Datensatzes.
* **Standardrichtlinie für** Zusammenführung: Eine Umschalter-Schaltfläche, mit der Sie festlegen können, ob diese Zusammenführungsrichtlinie für Ihr Unternehmen standardmäßig verwendet werden soll. Wenn der Selektor aktiviert und die neue Richtlinie gespeichert wird, wird Ihre vorherige Standardrichtlinie automatisch aktualisiert, sodass sie nicht mehr die Standardrichtlinie ist.

### Datensatzpriorität {#dataset-precedence}

Wenn Sie einen *Attributzusammenführungswert* auswählen, können Sie die *Dataset-Priorität* auswählen, damit Sie Profil-Fragmenten je nach dem Datensatz, aus dem sie stammen, Priorität einräumen können.

Ein Anwendungsfall wäre z. B. dann, wenn in Ihrem Unternehmen Informationen in einem Datensatz vorhanden sind, die bevorzugt oder vertrauenswürdig sind als Daten in einem anderen Datensatz.

Wenn Sie die *Datensatzpriorität* auswählen, wird ein separates Fenster geöffnet, in dem Sie aus den *verfügbaren Datensätzen* auswählen müssen (oder das Kontrollkästchen verwenden, um alle auszuwählen), welche Datensätze einbezogen werden. Sie können diese Datensätze dann per Drag &amp; Drop in das Bedienfeld &quot; *Ausgewählte Datensätze* &quot;ziehen und sie in die richtige Reihenfolge der Priorität ziehen. Der oberste Datensatz erhält höchste Priorität, der zweite Datensatz wird an zweiter Stelle stehen usw.

![](../images/merge-policies/dataset-precedence.png)

Nachdem Sie die Richtlinie zum Zusammenführen erstellt haben, klicken Sie auf **Speichern** , um zur Registerkarte &quot;Richtlinien ** zusammenführen&quot;zurückzukehren, auf der Ihre neue Richtlinie zum Zusammenführen in der Liste der Richtlinien angezeigt wird.

## Eine Richtlinie zum Zusammenführen bearbeiten

Sie können eine vorhandene Richtlinie zum Zusammenführen über die Registerkarte &quot;Richtlinien ** zusammenführen&quot;ändern, indem Sie auf den *Richtliniennamen* für die zu bearbeitende Richtlinie klicken.

![Landingpage von Richtlinien zusammenführen](../images/merge-policies/select-edit.png)

Wenn der Bildschirm &quot; *Edit merge policy* &quot;angezeigt wird, können Sie Änderungen am *Namens*-, *Schema*-, *ID-Heftungstyp* - und *Attributzusammenführungstyp* ** vornehmen und festlegen, ob diese Richtlinie für Ihr Unternehmen alsStandard-Zusammenführungsrichtlinie definiert werden soll oder nicht.

>[!Note]
>Sie können die Richtlinie-ID zum Zusammenführen nicht bearbeiten, die oben im Bearbeitungsbildschirm angezeigt wird. Dies ist eine schreibgeschützte, systemgenerierte ID, die nicht geändert werden kann.

![](../images/merge-policies/edit-screen.png)

Nachdem Sie die erforderlichen Änderungen vorgenommen haben, klicken Sie auf **Speichern** , um zur Registerkarte &quot;Richtlinien ** zusammenführen&quot;zurückzukehren, auf der die aktualisierten Informationen zu den Zusammenführungsrichtlinien jetzt angezeigt werden.

![](../images/merge-policies/edited.png)

## Verstöße gegen die Datenschutzpolitik

Beim Erstellen oder Aktualisieren einer Richtlinie zum Zusammenführen wird geprüft, ob die Richtlinie zum Zusammenführen eine der von Ihrem Unternehmen definierten Datenverwendungsrichtlinien verletzt. Datenverwendungsrichtlinien sind Teil der Datenverwaltung in Adobe Experience Platform und stellen Regeln dar, die die Arten von Marketingaktionen beschreiben, von denen Sie bestimmte Plattformdaten ausführen dürfen oder deren Ausführung eingeschränkt ist. Wenn zum Beispiel eine Richtlinie zum Zusammenführen verwendet wurde, um ein Segment zu erstellen, das an ein Drittanbieterziel aktiviert wurde, und Ihr Unternehmen über eine Datenverwendungsrichtlinie verfügte, die den Export bestimmter Daten an Dritte verhinderte, erhalten Sie beim Versuch, Ihre Fusionsrichtlinie zu speichern, eine Benachrichtigung über die Meldung &quot;Verletzung der Datenschutzrichtlinien erkannt&quot;.

Diese Benachrichtigung enthält eine Liste der Richtlinien zur Datenverwendung, die verletzt wurden, und ermöglicht Ihnen die Ansicht der Details der Verletzung durch Auswahl einer Richtlinie aus der Liste. Bei der Auswahl einer verletzten Richtlinie liefert die Registerkarte &quot; *Datenlinie* &quot;den *Grund für die Verletzung* und die *betroffenen Aktivierungen*, die jeweils detaillierter erläutern, wie die Datenverwendungsrichtlinie verletzt wurde.

Um mehr über die Leistung der Datenverwaltung in Adobe Experience Platform zu erfahren, lesen Sie zunächst den Überblick über die [Datenverwaltung](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Nächste Schritte

Nachdem Sie die Zusammenführungsrichtlinien für Ihre IMS-Organisation erstellt und konfiguriert haben, können Sie diese verwenden, um Audiencen aus Ihren Profil-Daten zu erstellen. Weitere Informationen zum Erstellen und Arbeiten mit Segmenten mit Experience Platform finden Sie in der Übersicht [zur](../../segmentation/home.md) Segmentierung.