---
title: Verbesserungen bei der Zielgruppenkomposition
description: Erfahren Sie mehr über die Verbesserungen bei der Audience-Komposition mit Zielgruppenanreicherung und schnellerer Aktivierung.
hide: true
hidefromtoc: true
source-git-commit: 065990790307124e0992731139abe9641a742a1b
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# Verbesserungen der Zielgruppenkomposition

Sie haben jetzt Zugriff auf **2** Verbesserungen bei der Zielgruppenkomposition:

- [Zielgruppen-Anreicherung](#audience-enrichment)
- [Schnellere Aktivierung](#faster-activation)

## Zielgruppen-Anreicherung {#audience-enrichment}

Mit der Zielgruppenanreicherung können Sie das Array von Werten ausgeben, mit denen Ihre Profile für die von Ihnen erstellte Zielgruppe qualifiziert werden.

Um Zielgruppenanreicherungen zu Ihrer Komposition hinzuzufügen, wählen Sie den obersten **[!UICONTROL Audience]** auf der Arbeitsfläche aus. Nachdem Sie der Zielgruppe einen Namen gegeben haben, wählen Sie **[!UICONTROL Build rule]** aus, um die Arbeitsfläche des Regel-Builders zu öffnen.

![Der Block „Zielgruppe“ sowie die Schaltfläche „Regel erstellen“ sind hervorgehoben.](/help/segmentation/images/ui/composition-enhancements/select-build-rule.png)

Die Arbeitsfläche des Regel-Builders wird angezeigt. Jetzt können Filterkriterien für die Anreicherung Ihrer Audience erstellt werden. Dieses Filterkriterium **muss** ein Attribut enthalten, das sich in einem Array befindet. Das Attribut, das ein Array ist, hängt von der Schemastruktur Ihrer Organisation ab. Nachdem Sie Ihre Filterkriterien erstellt haben, wählen Sie im rechten Bedienfeld **[!UICONTROL Delivery]** aus.

![Die Arbeitsfläche des Regel-Builders zeigt ein Beispiel für eine Zielgruppe, die über Anreicherungen verfügen kann. Die Schaltfläche „Versand“ ist ebenfalls hervorgehoben.](/help/segmentation/images/ui/composition-enhancements/view-delivery.png)

Wählen Sie in der Liste im linken Bereich das Objekt-Array aus, das Sie für die Anreicherung verwenden möchten. Wenn im Profil nur ein Array vorhanden ist, wird das Array automatisch für Sie ausgewählt. Wählen Sie **[!UICONTROL Save]** aus, um zur Audience-Komposition zurückzukehren.

<!-- , as well as the fields you want to be used in the enrichment. -->

![Die Schemastruktur für die Anreicherungsstruktur wird angezeigt.](/help/segmentation/images/ui/composition-enhancements/view-schema-tree.png)

Innerhalb der Zielgruppenkomposition ist Ihr [!UICONTROL Audience] jetzt vom Typ &quot;[!UICONTROL Rule builder with enhancement]&quot;. Wählen Sie **[!UICONTROL Publish]** aus, um Ihre Audience für den nächsten täglichen Batch zu aktivieren.

![Der Zielgruppen-Block ist hervorgehoben und zeigt an, dass eine Zielgruppe mit einer Anreicherung hinzugefügt wird.](/help/segmentation/images/ui/composition-enhancements/rule-builder-with-enrichment.png)

### Verhaltensdetails und Leitlinien

Beachten Sie bei der Verwendung der Zielgruppenanreicherung die folgenden Details und Leitplanken:

- Sie können die Zielgruppenanreicherung nur in Zielgruppen verwenden, die in der Zielgruppenkomposition erstellt wurden
- Der erste innerhalb der Komposition verwendete Block **muss** eine regelbasierte Zielgruppe sein.
- Sie **keine** Vorgänge innerhalb der Komposition verwenden.
- Nach der Veröffentlichung **Sie die Komposition** der regelbasierten Zielgruppe nicht mehr bearbeiten.

   - Sie ** die Komposition in einen Entwurf kopieren und den Entwurf bearbeiten, wenn Sie Änderungen an der Basiskomposition oder der regelbasierten Zielgruppe vornehmen möchten.

- Es **nur** Objekt-Array verwendet werden, um die Anreicherungs-Payload innerhalb einer einzigen Zielgruppe zu generieren

   - Das Payload-Array kann in einem Objekt verschachtelt sein (bis zu sieben Ebenen innerhalb des Profilschemas), **kann** in einem anderen Array enthalten sein.
   - Das Payload-Array **muss** 50 oder weniger Zeilen enthalten.
   - Alle in der Payload ausgegebenen Spalten **müssen** ein primitiver Typ sein.
   - Nur die ersten **20** Spalten des Arrays werden ausgegeben.

- Derzeit **nur 10** Zielgruppenkompositionen zur Verwendung verfügbar

## Schnellere Aktivierung {#faster-activation}

Durch eine schnellere Aktivierung können Sie Ihre Audience sofort nach der Auswertung der Komposition für ein nachgelagertes Ziel aktivieren. Wenn Ihr Ziel so eingestellt ist, dass es nach der Segmentauswertung aktiviert wird, müssen Sie nicht mehr 24 Stunden warten, bis der Auswertungsauftrag abgeschlossen ist.

Weitere Informationen finden Sie im Handbuch [Aktivieren von Zielgruppen für Batch-Profil-Ziele](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files).
