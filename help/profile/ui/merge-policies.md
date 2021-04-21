---
keywords: Experience Platform;Profil;Echtzeit-Profil von Kunden;Zusammenführungsrichtlinien;Benutzeroberfläche;Benutzeroberfläche;Zeitstempel geordnet;Datensatzpräferenz
title: Leitfaden zur Benutzeroberfläche "Richtlinien zusammenführen"
topic-legacy: guide
type: Documentation
description: Mit Adobe Experience Platform können Sie Datenfragmente aus mehreren Quellen zusammenführen und kombinieren, um eine vollständige Ansicht Ihrer einzelnen Kunden zu erhalten. Beim Zusammenführen dieser Daten sind Zusammenführungsrichtlinien die Regeln, die Plattform verwendet, um zu bestimmen, wie Daten priorisiert werden und welche Daten kombiniert werden, um eine einheitliche Ansicht zu erstellen.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '3017'
ht-degree: 8%

---

# Leitfaden zur Benutzeroberfläche &quot;Richtlinien zusammenführen&quot;

Mit Adobe Experience Platform können Sie Datenfragmente aus mehreren Quellen zusammenführen und kombinieren, um eine vollständige Ansicht Ihrer einzelnen Kunden zu erhalten. Beim Zusammenführen dieser Daten sind Zusammenführungsrichtlinien die Regeln, die [!DNL Platform] verwenden, um zu bestimmen, wie Daten priorisiert werden und welche Daten kombiniert werden, um eine einheitliche Ansicht zu erstellen.

Wenn ein Kunde beispielsweise über mehrere Kanal mit Ihrer Marke interagiert, enthält Ihr Unternehmen mehrere Profil-Fragmente, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen angezeigt werden. Wenn diese Fragmente in eine Plattform integriert werden, werden sie zusammengeführt, um ein einzelnes Profil für diesen Kunden zu erstellen. Wenn die Daten aus mehreren Quellen in Konflikt geraten (z. B. ein Fragment als &quot;Single&quot;, während die anderen Listen als &quot;verheiratet&quot;Liste werden), bestimmt die Richtlinie zum Zusammenführen, welche Informationen in das Profil für die betreffende Person aufgenommen werden sollen.

Über die RESTful APIs oder die Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen einrichten. Dieses Handbuch enthält schrittweise Anleitungen zum Arbeiten mit Zusammenführungsrichtlinien über die Adobe Experience Platform-Benutzeroberfläche.

Wenn Sie lieber mit der API [!DNL Real-time Customer Profile] zusammenführen möchten, befolgen Sie die Anweisungen, die im Handbuch [Richtlinien-API zusammenführen](../api/merge-policies.md) beschrieben sind.

## Erste Schritte

Dieser Leitfaden erfordert ein funktionierendes Verständnis einiger wichtiger [!DNL Experience Platform] Funktionen. Bevor Sie diesem Handbuch folgen oder Profil-APIs verwenden, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [Echtzeit-Kundenprofil](../home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Adobe Experience Platform-Identitätsdienst](../../identity-service/home.md): Ermöglicht Kunden-Profil in Echtzeit durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, in die Daten eingehen  [!DNL Platform].
* [Experience-Datenmodell (XDM)](../../xdm/home.md)[!DNL Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.

## Methoden zusammenführen {#merge-methods}

Jedes Profil-Fragment enthält Informationen zu nur einer Identität aus der Gesamtanzahl der Identitäten, die für eine Einzelperson vorhanden sein könnten. Beim Zusammenführen dieser Daten zu einem Profil eines Kunden besteht die Möglichkeit, dass diese Informationen kollidieren und eine Priorität angegeben werden muss. Wenn Sie eine Zusammenführungsmethode wählen, können Sie angeben, welche Datensatzattribute priorisiert werden sollen, wenn ein Zusammenführungskonflikt zwischen Datensätzen auftritt.

Für Zusammenführungsrichtlinien stehen zwei mögliche Zusammenführungsmethoden zur Verfügung. Jede dieser Methoden wird nachfolgend mit zusätzlichen Details in den folgenden Abschnitten zusammengefasst:

* **[!UICONTROL Zeitstempel angeordnet]:** Im Ereignis eines Konflikts wird dem Profil-Fragment, das zuletzt aktualisiert wurde, Priorität eingeräumt.
   * **Benutzerdefinierte Zeitstempel:** [!UICONTROL Zeitstempel ] werden auch von benutzerdefinierten Zeitstempeln unterstützt, die beim Zusammenführen von Daten innerhalb desselben Datensatzes (mehrere Identitäten) oder über Datasets hinweg Vorrang vor Systemzeitstempeln haben. Weitere Informationen finden Sie im Abschnitt [mit benutzerdefinierten Zeitstempeln](#custom-timestamps).
* **[!UICONTROL Priorität] des Datensatzes: Geben Sie** im Ereignis eines Konflikts den Fragmenten des Profils Priorität, basierend auf dem Datensatz, aus dem sie stammten. Bei Auswahl dieser Option müssen Sie die zugehörigen Datensätze und deren Reihenfolge der Priorität auswählen.

### Zeitstempel bestellt {#timestamp-ordered}

Während Profil-Datensätze in die Experience Platform aufgenommen werden, wird zum Zeitpunkt der Erfassung ein Systemzeitstempel abgerufen und dem Datensatz hinzugefügt. Wenn als Zusammenführungsmethode für eine Zusammenführungsrichtlinie **[!UICONTROL Zeitstempel sortiert]** ausgewählt ist, werden Profil basierend auf dem Systemzeitstempel zusammengeführt. Das heißt, das Zusammenführen erfolgt auf der Grundlage des Zeitstempels für den Zeitpunkt, zu dem der Datensatz in die Plattform aufgenommen wurde.

#### Verwenden benutzerdefinierter Zeitstempel {#custom-timestamps}

Gelegentlich kann es zu Anwendungsfällen kommen, bei denen ein benutzerdefinierter Zeitstempel bereitgestellt werden muss und bei denen die Richtlinie zum Zusammenführen den benutzerdefinierten Zeitstempel und nicht den Systemzeitstempel berücksichtigen muss. Dazu gehören beispielsweise das Aufstocken von Daten oder das Sicherstellen der richtigen Reihenfolge von Ereignissen, wenn die Datensätze nicht mehr in der richtigen Reihenfolge angezeigt werden.

Um einen benutzerdefinierten Zeitstempel zu verwenden, muss das **[!UICONTROL Externe Quellsystem-Audit-Details-Mixin]** Ihrem Profil-Schema hinzugefügt werden. Nach dem Hinzufügen kann der benutzerdefinierte Zeitstempel mithilfe des Felds `lastUpdatedDate` ausgefüllt werden. Wenn ein Datensatz mit dem ausgefüllten Feld `lastUpdatedDate` erfasst wird, verwendet die Experience Platform dieses Feld, um Datensätze über Datensätze hinweg zusammenzuführen. Wenn `lastUpdatedDate` nicht vorhanden oder nicht gefüllt ist, verwendet die Plattform weiterhin den Systemzeitstempel.

>[!NOTE]
>
>Sie müssen sicherstellen, dass der Zeitstempel `lastUpdatedDate` aufgefüllt wird, wenn ein Update für denselben Datensatz vorgenommen wird.

Im folgenden Screenshot werden die Felder im [!UICONTROL Externe Quellsystem-Prüfdetails-Mixin] angezeigt. Eine schrittweise Anleitung zum Arbeiten mit Schemas in der Plattform-Benutzeroberfläche, einschließlich des Hinzufügens von Mixins zu Schemas, finden Sie im [Lernprogramm zum Erstellen eines Schemas mit der Benutzeroberfläche](../../xdm/tutorials/create-schema-ui.md).

![](../images/merge-policies/custom-timestamp-mixin.png)

Informationen zum Arbeiten mit benutzerdefinierten Zeitstempeln mithilfe der API finden Sie im Abschnitt [Richtlinie-Endpunkt zusammenführen zu benutzerdefinierten Zeitstempeln](../api/merge-policies.md#custom-timestamps).

### Datensatzpriorität {#dataset-precedence}

Wenn **[!UICONTROL Datensatzpriorität]** als Zusammenführungsmethode für eine Zusammenführungsrichtlinie ausgewählt ist, können Sie Profil-Fragmenten anhand des Datensatzes, aus dem sie stammen, Priorität einräumen. Ein Beispiel bestünde darin, wenn es in Ihrer Organisation Daten in einem Datensatz gibt, die bevorzugt werden oder vertrauenswürdiger sind als Daten in einem anderen Datensatz.

Um eine Richtlinie zum Zusammenführen mit **[!UICONTROL Datensatzpriorität]** zu erstellen, müssen Sie die eingeschlossenen Profil- und ExperienceEvent-Datensätze auswählen und dann die Profil-Datensätze manuell nach Priorität sortieren. Sobald die Datensätze ausgewählt und sortiert wurden, erhält der oberste Datensatz die höchste Priorität, der zweite Datensatz die zweithöchste usw.

## [!UICONTROL ID-Stiftung] {#id-stitching}

Identitätszuordnung ([!UICONTROL ID-Zuführung]) ist der Vorgang, bei dem Datenfragmente identifiziert und zu einem vollständigen Profil zusammengefasst werden. Um die unterschiedlichen Stilverhalten zu veranschaulichen, sollten Sie einen einzelnen Kunden in Betracht ziehen, der mit einer Marke über zwei verschiedene E-Mail-Adressen interagiert.

* **[!UICONTROL Keine]:** Wenn diese Option aktiviert ist, werden IDs nicht zusammengeführt. Bei einer Segmentierung werden Identitäten, die zu derselben Person gehören, nicht zusammengeführt, und bei der Segmentierung werden die Attribute, die jeder einzelnen ID zugeordnet sind, nur berücksichtigt, wenn festgestellt wird, ob ein Kunde für eine Segmentmitgliedschaft infrage kommt. Dies könnte dazu führen, dass ein Kunde mehrere Profil hat und jedes Profil für verschiedene Segmente qualifiziert ist, sodass mehrere Marketingmeldungen an denselben Kunden gesendet werden.
* **[!UICONTROL Privates Diagramm]:** Wenn das private Diagramm ausgewählt ist, werden mehrere Identitäten, die sich auf dieselbe Person beziehen, miteinander verknüpft. Dies führt dazu, dass der Kunde über ein einzelnes Profil verfügt, und ermöglicht es der Segmentierung, mehrere Attribute aus mehreren verwandten Identitäten bei der Bestimmung der Segmentqualifikation zu berücksichtigen. In diesem Szenario verfügt der Kunde wahrscheinlich über ein einzelnes Profil, qualifiziert sich für ein Segment, das auf der Kombination von Attributen über Identitäten hinweg basiert, und erhält nur eine Marketing-Nachricht.

Wenn Sie mehr über Identitäten und deren Rolle bei der Generierung von Profilen und Segmenten erfahren möchten, lesen Sie zunächst die [Übersicht über den Identitätsdienst](../../identity-service/home.md).

## Standardrichtlinie für die Zusammenführung {#default-merge-policy}

Ein Unternehmen kann eine Standardrichtlinie für die Zusammenführung von Profil-Fragmenten für sein Unternehmen erstellen. Auf diese Weise können Benutzer bei Aktionen in der Experience Platform, wie dem Anzeigen von Profilen oder dem Erstellen von Segmenten, ganz einfach die Standardrichtlinie auswählen. In den meisten Fällen wird die standardmäßige Zusammenführungsrichtlinie verwendet, sofern keine andere Richtlinie angegeben wurde.

Jedes Unternehmen kann mehrere Zusammenführungsrichtlinien für eine einzelne XDM-Schema-Klasse erstellen. Es kann jedoch nur eine Standardzusammenführungsrichtlinie für jede Klasse deklariert werden. Ihre Organisation könnte beispielsweise über eine Standardrichtlinie zum Zusammenführen für die [!DNL XDM Individual Profile]-Klasse und eine andere Standardrichtlinie zum Zusammenführen für eine benutzerdefinierte Produktinventarklasse verfügen.

Wenn Sie eine neue Richtlinie für die Zusammenführung erstellen und diese als Standard festlegen, wird die vorherige Standardrichtlinie für die Zusammenführung automatisch vom System aktualisiert, sodass sie nicht mehr standardmäßig verwendet wird.

>[!WARNING]
>
>Profil-Zähler und Segmente mit einer vorhandenen, verknüpften Standardzusammenführungsrichtlinie können betroffen sein. Jedes Segment, für das eine Standardzusammenführungsrichtlinie angewendet wurde, wird auf die neue Standardrichtlinie für die Zusammenführung aktualisiert.

## Zusammenführungsrichtlinien anzeigen {#view-merge-policies}

In der Benutzeroberfläche [!DNL Experience Platform] können Sie mit der Arbeit mit Zusammenführungsrichtlinien beginnen, indem Sie **[!UICONTROL Profil]** in der linken Navigation auswählen und dann die Registerkarte **[!UICONTROL Richtlinien zusammenführen]** auswählen. Auf dieser Registerkarte finden Sie eine Liste aller für Ihr Unternehmen geltenden Zusammenführungsrichtlinien sowie Details zu den einzelnen Zusammenführungsrichtlinien, einschließlich des Richtliniennamen, ob die Zusammenführungsrichtlinie die standardmäßige Zusammenführungsrichtlinie ist oder nicht, und die Schema-Klasse, auf die sich die Zusammenführungsrichtlinie bezieht.

![Landingpage für Zusammenführungsrichtlinien](../images/merge-policies/landing.png)

Um auszuwählen, welche Details sichtbar sind, oder um der Anzeige weitere Spalten hinzuzufügen, wählen Sie **[!UICONTROL Spalten konfigurieren]** und klicken Sie auf einen Spaltennamen, um sie hinzuzufügen oder aus der Ansicht zu entfernen.

![](../images/merge-policies/adjust-view.png)

## Zusammenführungsrichtlinie erstellen {#create-a-merge-policy}

Um eine neue Richtlinie für die Zusammenführung zu erstellen, wählen Sie auf der Registerkarte &quot;Zusammenführungsrichtlinien&quot;die Option **[!UICONTROL Richtlinie für die Zusammenführung erstellen]**.

![Landingpage der Richtlinien mit hervorgehobener Schaltfläche &quot;Erstellen&quot;zusammenführen.](../images/merge-policies/create-new.png)

Im Bildschirm **[!UICONTROL Neue Mergerichtlinie]** für den Workflow können Sie wichtige Informationen für Ihre neue Mergerichtlinie in einer Reihe von Anleitungen bereitstellen.

![Der neue Arbeitsablauf für die Zusammenführungsrichtlinie.](../images/merge-policies/create.png)

### [!UICONTROL Konfigurieren von] {#configure}

Der erste Schritt im Arbeitsablauf ermöglicht es Ihnen, Ihre Zusammenführungsrichtlinie zu konfigurieren, indem Sie grundlegende Informationen bereitstellen. Zu diesen Informationen gehören:

* **[!UICONTROL Name]**: Der Name Ihrer Zusammenführungsrichtlinie sollte beschreibend, aber kurz sein.
* **[!UICONTROL Schema-Klasse]**: Die XDM-Schema-Klasse, die der Mergerichtlinie zugeordnet ist. Dies gibt die Schema-Klasse an, für die diese Zusammenführungsrichtlinie erstellt wird. Organisationen können mehrere Zusammenführungsrichtlinien pro Schema-Klasse erstellen. In der Benutzeroberfläche ist derzeit nur die Klasse [!UICONTROL XDM Individuelles Profil] verfügbar. Sie können das Vereinigung-Schema für die Schema-Klasse durch Auswahl von **[!UICONTROL Ansicht Vereinigung-Schema]** Vorschau. Weitere Informationen finden Sie im folgenden Abschnitt zum Schema [Vereinigung](#view-union-schema).
* **[!UICONTROL ID-Zusammenfügung]**: In diesem Feld wird definiert, wie die verwandten Identitäten eines Kunden ermittelt werden. Weitere Informationen finden Sie im Abschnitt zu [ID-Heften](#id-stitching) weiter oben in diesem Handbuch. Es gibt zwei mögliche Werte:
   * **[!UICONTROL Keine]**: Keine Identitätszusammenfügung durchführen.
   * **[!UICONTROL Privates Diagramm]**: Identitätszusammenfügung basierend auf Ihrem privaten Identitätsdiagramm durchführen.
* **[!UICONTROL Standardmäßige Zusammenführungsrichtlinie]**: Eine Umschalter-Schaltfläche, mit der Sie festlegen können, ob diese Zusammenführungsrichtlinie der Standard für Ihre Organisation sein soll oder nicht. Wenn der Selektor aktiviert ist, werden Sie in einer Warnmeldung aufgefordert, zu bestätigen, dass Sie die standardmäßige Fusionsrichtlinie Ihres Unternehmens ändern möchten. Weitere Informationen finden Sie im Abschnitt zu [Richtlinien für die standardmäßige Zusammenführung](#default-merge-policy) weiter oben in diesem Handbuch.
   ![](../images/merge-policies/create-make-default.png)

Nachdem die erforderlichen Felder ausgefüllt wurden, können Sie **[!UICONTROL Weiter]** auswählen, um den Workflow fortzusetzen.

![Ein kompletter Bildschirm &quot;Konfigurieren&quot;mit hervorgehobener Schaltfläche Weiter.](../images/merge-policies/create-complete.png)

#### [!UICONTROL Ansicht Vereinigung Schema] {#view-union-schema}

Beim Erstellen oder Bearbeiten einer Zusammenführungsrichtlinie können Sie das Schema Vereinigung für die ausgewählte Schema-Klasse durch Auswahl von **[!UICONTROL Ansicht Vereinigung Schema]** Ansicht.

![](../images/merge-policies/view-union-schema.png)

Dadurch wird das Dialogfeld [!UICONTROL Ansicht Vereinigung Schema] geöffnet, in dem alle beitragenden Schema, Identitäten und Beziehungen angezeigt werden, die mit dem Vereinigung-Schema verbunden sind. Mit dem Dialogfeld können Sie das Schema &quot;Vereinigung&quot;auf dieselbe Weise wie mit dem Register [!UICONTROL Vereinigung Schema] im Bereich [!UICONTROL Profil] der Plattform-Benutzeroberfläche erkunden.

Ausführliche Informationen zu Schemas der Vereinigung, einschließlich der Interaktion mit ihnen im Dialogfeld [!UICONTROL Vereinigung Schema] oder [!UICONTROL Ansicht Vereinigung Schema], das im Arbeitsablauf der Zusammenführungsrichtlinien angezeigt wird, finden Sie im Handbuch [Vereinigung Schema UI guide](union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)


### [!UICONTROL Profil-Datensätze auswählen] {#select-profile-datasets}

Wählen Sie im Bildschirm **[!UICONTROL Profil-Datensätze auswählen]** die **[!UICONTROL Zusammenführungsmethode]** aus, die Sie für Ihre Zusammenführungsrichtlinie verwenden möchten. Außerdem wird auf dem Bildschirm die Gesamtzahl der [!UICONTROL Profil-Datensätze] in Ihrem Unternehmen angezeigt, die sich auf die im vorherigen Bildschirm ausgewählte Schema-Klasse beziehen.

Je nach der gewählten Zusammenführungsmethode werden alle Profil-Datensätze in der Reihenfolge zusammengeführt, in der sie zuletzt aktualisiert wurden (Zeitstempel sortiert). Andernfalls müssen Sie festlegen, welche Profil-Datensätze in die Zusammenführungsrichtlinie aufgenommen werden sollen und in welcher Reihenfolge sie zusammengeführt werden sollen (Datensatzpriorität). Weitere Informationen zu Zusammenführungsmethoden finden Sie im Abschnitt [Zusammenführungsmethoden](#merge-methods), der weiter oben in diesem Dokument bereitgestellt wurde.

#### Zeitstempel bestellt {#timestamp-ordered-profile}

Wenn Sie **[!UICONTROL Zeitstempel sortiert]** als Zusammenführungsmethode auswählen, haben Attribute aus den zuletzt aktualisierten Datensätzen Vorrang. Dies gilt für alle Profil-Datensätze.

![](../images/merge-policies/timestamp-ordered.png)

#### Datensatzpriorität {#dataset-precedence-profile}

Wenn Sie **[!UICONTROL Datensatzpriorität]** als Zusammenführungsmethode auswählen, müssen Sie Profil-Datensätze auswählen und sie manuell priorisieren. Jeder aufgelistete Datensatz enthält auch den Status des zuletzt erfassten Stapels oder zeigt einen Hinweis an, dass keine Stapel in diesen Datensatz aufgenommen wurden.

Sie können bis zu 50 Datensätze aus der DataSet-Liste auswählen, die in die Zusammenführungsrichtlinie aufgenommen werden sollen. Bei Auswahl der Datensätze werden sie dem Abschnitt **[!UICONTROL Datensatz auswählen]** hinzugefügt, sodass Sie die Datensätze per Drag &amp; Drop verschieben und entsprechend Ihrer gewünschten Priorität sortieren können. Da die Datensätze in der Liste angepasst werden, wird die Ordinalform (1, 2, 3 usw.) neben dem Datensatz aktualisiert und zeigt die Priorität an (1 erhält die höchste Priorität, dann 2 und höher).

Durch Auswahl eines Datensatzes wird auch das Schema **[!UICONTROL Vereinigung]** aktualisiert und die Felder im Schema Vereinigung angezeigt, zu denen jeder Datensatz Daten beiträgt. Weitere Informationen zu Schemas der Vereinigung, einschließlich der Interaktion mit Visualisierungen in der Benutzeroberfläche, finden Sie im Handbuch [Vereinigung Schema UI (UI-Handbuch)](union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

### [!UICONTROL ExperienceEvent-Datensätze auswählen] {#select-experienceevent-datasets}

Im nächsten Schritt im Workflow müssen Sie ExperienceEvent-Datensätze auswählen. Dieser Bildschirm wird durch die Zusammenführungsmethode beeinflusst, die Sie im Bildschirm [[!UICONTROL Profil-Datensätze auswählen]](#select-profile-datasets) ausgewählt haben.

In diesem Bildschirm wird auch die Gesamtanzahl der von Ihrem Unternehmen erstellten **[!UICONTROL ExperienceEvent-Datensätze]** angezeigt, die sich auf die Schema-Klasse beziehen, die Sie im Bildschirm &quot;Konfiguration der Zusammenführungsrichtlinie&quot;ausgewählt haben.

#### Zeitstempel bestellt {#timestamp-ordered-experienceevent}

Wenn Sie **[!UICONTROL Zeitstempel sortiert]** als Zusammenführungsmethode für Profil-Datasets ausgewählt haben, haben auch die Attribute der zuletzt aktualisierten ExperienceEvent-Datasets Vorrang.

![](../images/merge-policies/timestamp-experienceevent.png)

#### Datensatzpriorität {#dataset-precedence-experienceevent}

Wenn Sie **[!UICONTROL Datensatzpriorität]** als Zusammenführungsmethode für Profil-Datensätze ausgewählt haben, müssen Sie ExperienceEvent-Datensätze auswählen, die einbezogen werden sollen. Sie können bis zu 50 ExperienceEvent-Datensätze aus der DataSet-Liste auswählen. Wenn Datensätze ausgewählt sind, werden sie im Abschnitt [!UICONTROL Datensatz auswählen] angezeigt.

ExperienceEvent-Datensätze können nicht manuell angeordnet werden. Stattdessen werden die Attribute in den ExperienceEvent-Datensätzen an die Profil-Datensätze angehängt, wenn sie zum selben Profil-Fragment gehören.

Ähnlich wie bei der Auswahl von Profil-Datensätzen wird bei Auswahl eines ExperienceEvent-Datensatzes auch der Abschnitt **[!UICONTROL Vereinigung-Schema]** aktualisiert und die Felder im Schema Vereinigung angezeigt, zu denen jeder Datensatz Daten beiträgt. Weitere Informationen zu Schemas der Vereinigung, einschließlich der Interaktion mit Visualisierungen in der Benutzeroberfläche, finden Sie im Handbuch [Vereinigung Schema UI (UI-Handbuch)](union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

### [!UICONTROL Review] {#review}

Der letzte Schritt im Arbeitsablauf besteht darin, Ihre Zusammenführungsrichtlinie zu überprüfen. Der Bildschirm **[!UICONTROL Überprüfen]** zeigt den Namen Ihrer neuen Zusammenführungsrichtlinie, die Schema-Klasse, auf der sie basiert, die [!UICONTROL ID-Suche]-Option sowie die Zusammenführungsmethode und die in der Zusammenführungsrichtlinie enthaltenen Datensätze an. Um alle enthaltenen Profil- oder ExperienceEvent-Datensätze Ansicht, wählen Sie die Anzahl der Datensätze aus, um die Dropdown-Liste zu erweitern.

Bitte überprüfen Sie Ihre Merge-Richtlinie sorgfältig, bevor Sie **[!UICONTROL Finish]** auswählen, um den Erstellungsarbeitsablauf abzuschließen.

#### Zeitstempel bestellt {#timestamp-ordered-review}

Wenn Sie **[!UICONTROL Zeitstempel sortiert]** als Zusammenführungsmethode für Ihre Zusammenführungsrichtlinie ausgewählt haben, enthält die Liste der Profil-Datensätze alle Datensätze, die von Ihrem Unternehmen im Zusammenhang mit der Schema-Klasse erstellt wurden, in der Reihenfolge des Zeitstempels. Die Liste der ExperienceEvent-Datensätze umfasst alle Datensätze, die Ihr Unternehmen für die ausgewählte Schema-Klasse erstellt hat, und wird an die Profil-Datensätze angehängt.

![](../images/merge-policies/timestamp-review.png)

#### Datensatzpriorität {#dataset-precedence-review}

Wenn Sie **[!UICONTROL Datensatzpriorität]** als Zusammenführungsmethode für Ihre Zusammenführungsrichtlinie ausgewählt haben, enthalten die Listen von Profil- und ExperienceEvent-Datensätzen nur die Profil- und ExperienceEvent-Datensätze, die Sie während des Erstellungsarbeitsablaufs ausgewählt haben. Die Reihenfolge der Profil-Datensätze sollte mit der Priorität übereinstimmen, die Sie bei der Erstellung angegeben haben. Ist dies nicht der Fall, verwenden Sie die Schaltfläche [!UICONTROL Zurück], um zu den vorherigen Workflow-Schritten zurückzukehren und die Priorität anzupassen.

![](../images/merge-policies/dataset-precedence-review.png)

### Aktualisierte Liste der Zusammenführungsrichtlinien {#updated-list}

Nach Abschluss des Workflows zum Erstellen einer neuen Richtlinie zum Zusammenführen kehren Sie zur Registerkarte **[!UICONTROL Richtlinien zusammenführen]** zurück. Die Liste der Zusammenführungsrichtlinien für Ihr Unternehmen sollte nun die von Ihnen soeben erstellte Zusammenführungsrichtlinie enthalten.

![](../images/merge-policies/new-merge-policy-created.png)

## Zusammenführungsrichtlinie bearbeiten

Auf der Registerkarte [!UICONTROL Richtlinien zusammenführen] können Sie eine vorhandene, für die [!DNL XDM Individual Profile]-Klasse erstellte Merge-Richtlinie ändern, indem Sie für die zu bearbeitende Mergerichtlinie **[!UICONTROL den Richtliniennamen]** auswählen.

![Landingpage für Zusammenführungsrichtlinien](../images/merge-policies/select-edit.png)

Wenn der Bildschirm **[!UICONTROL Richtlinie zum Bearbeiten der Zusammenführung]** angezeigt wird, können Sie Änderungen am Namen und an der [!UICONTROL ID-Zuordnung] vornehmen und ändern, ob diese Richtlinie die Standardrichtlinie für die Zusammenführung in Ihrem Unternehmen ist.

Wählen Sie **[!UICONTROL Weiter]**, um den Arbeitsablauf für die Zusammenführungsrichtlinie zu durchlaufen und die in der Zusammenführungsrichtlinie enthaltene Zusammenführungsmethode und die darin enthaltenen Datensätze zu aktualisieren.

![](../images/merge-policies/edit-screen.png)

Nachdem Sie die erforderlichen Änderungen vorgenommen haben, überprüfen Sie Ihre Zusammenführungsrichtlinie und wählen Sie **[!UICONTROL Fertig stellen]**, um zur Registerkarte **[!UICONTROL Richtlinien zusammenführen]** zurückzukehren.

>[!WARNING]
>
>Eine Änderung der Richtlinie zum Zusammenführen kann sich auf die Segmentierung und die Ergebnisse von Profilen auswirken, da sich dadurch die Art und Weise, wie Datenkonflikte gelöst werden, ändert.

![](../images/merge-policies/edit-review.png)

## Verstöße gegen Data Governance-Richtlinien

Beim Erstellen oder Aktualisieren einer Zusammenführungsrichtlinie wird geprüft, ob die Zusammenführungsrichtlinie eine der von Ihrer Organisation definierten Datennutzungsrichtlinien verletzt. Datenverwendungs-Richtlinien gehören zu Adobe Experience Platform [!DNL Data Governance] und sind Regeln, die die Arten von Marketingaktionen beschreiben, von denen Sie für bestimmte [!DNL Platform]-Daten berechtigt oder eingeschränkt sind. Wenn zum Beispiel eine Richtlinie zum Zusammenführen verwendet wurde, um ein Segment zu erstellen, das an ein Drittanbieterziel aktiviert wurde, und Ihr Unternehmen über eine Datenverwendungsrichtlinie verfügte, die den Export bestimmter Daten an Dritte verhinderte, erhalten Sie beim Versuch, Ihre Fusionsrichtlinie zu speichern, eine **[!UICONTROL Benachrichtigung zur Datenschutzrichtlinien, die]** erkannt wurde.

Diese Benachrichtigung enthält eine Liste der Datennutzungsrichtlinien, die verletzt wurden, und ermöglicht Ihnen das Anzeigen von Details zur Verletzung, indem Sie eine Richtlinie aus der Liste auswählen. Bei der Auswahl einer verletzten Richtlinie liefert die Registerkarte **[!UICONTROL Datenlinie]** den Grund für die Verletzung und die betroffenen Aktivierungen, die jeweils detailliertere Informationen darüber liefern, wie die Datenverwendungsrichtlinie verletzt wurde.

Um mehr über Data Governance in Adobe Experience Platform zu erfahren, lesen Sie zunächst den [Überblick zu Data Governance](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Nächste Schritte

Nachdem Sie für Ihr Unternehmen Zusammenführungsrichtlinien erstellt und konfiguriert haben, können Sie diese verwenden, um die Ansicht von Profilen innerhalb der Plattform anzupassen und Audiencen aus Ihren Profil-Daten zu erstellen. Weitere Informationen zum Erstellen und Arbeiten mit Segmenten mithilfe der [!DNL Experience Platform]-Benutzeroberfläche und -APIs finden Sie unter [Segmentierungsübersicht](../../segmentation/home.md).
