---
keywords: Experience Platform;Profil;Echtzeit-Kundendaten;Profil;Benutzeroberfläche;Anpassung;Profil;Details
title: Profil-Detailanpassung in der Benutzeroberfläche
description: 'Dieses Handbuch enthält schrittweise Anleitungen zum Anpassen der Art und Weise, wie Kundendaten in Echtzeit in der Adobe Experience Platform-Benutzeroberfläche angezeigt werden. '
topic-legacy: guide
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] Detail-Anpassung  {#profile-detail-customization}

Auf der Adobe Experience Platform-Benutzeroberfläche können Sie Daten in Form von Kundendaten Ansicht und Interaktion mit [!DNL Real-time Customer Profile]-Daten ausführen. Die in der Benutzeroberfläche angezeigten Informationen zum Profil wurden aus mehreren Profil-Fragmenten zusammengeführt, um eine Ansicht des jeweiligen Kunden zu bilden. Dazu gehören Details wie Basisattribute, verknüpfte Identitäten und Voreinstellungen für Kanal. Die in den Profilen angezeigten Standardfelder können auch auf organisatorischer Ebene geändert werden, um bevorzugte [!DNL Profile]-Attribute anzuzeigen. Dieses Handbuch enthält schrittweise Anleitungen zum Anpassen der Anzeige von [!DNL Profile]-Daten in der Plattform-Benutzeroberfläche.

Eine vollständige Anleitung zur Benutzeroberfläche für Profile finden Sie im Handbuch [Profil UI (UI-Handbuch](user-guide.md)).

## Karten neu anordnen und Größe ändern {#reorder-and-resize-cards}

Auf der Registerkarte **[!UICONTROL Detail]** des Profils können Sie **[!UICONTROL Dashboard]** ändern auswählen, um die Größe und Anordnung der vorhandenen Karten zu ändern.

![](../images/profile-customization/profiles-modify-dashboard.png)

Nachdem Sie das Dashboard geändert haben, können Sie die Reihenfolge der Karten ändern, indem Sie den Kartentitel auswählen und die Karten in die gewünschte Reihenfolge ziehen. Sie können die Größe einer Karte auch ändern, indem Sie das Winkelsymbol in der unteren rechten Ecke der Karte (`⌟`) auswählen und die Karte auf die gewünschte Größe ziehen. In diesem Beispiel wird die Größe der Karte **[!UICONTROL Grundlegende Attribute]** geändert.

![](../images/profile-customization/profiles-resize-cards.png)

Die ausgewählte Karte passt sich der gewünschten Größe an und die umliegenden Karten werden dynamisch neu positioniert. Dies kann dazu führen, dass einige Karten in zusätzliche Zeilen verschoben werden, sodass Sie nach unten blättern müssen, um alle Karten anzuzeigen. Wenn beispielsweise die Größe der Karte &quot;[!UICONTROL Grundlegende Attribute]&quot;geändert wird, ist die Karte &quot;[!UICONTROL Verknüpfte Identitäten]&quot;nicht mehr in der ersten Zeile sichtbar und erscheint nun in einer neuen zweiten Zeile im Profil (nicht angezeigt). Um die Karte &quot;[!UICONTROL Verknüpfte Identitäten]&quot;in die oberste Zeile zurückzugeben, können Sie sie per Drag &amp; Drop an die aktuelle Position der Karte &quot;[!UICONTROL Voreinstellungen für Kanal]&quot;verschieben.

![](../images/profile-customization/profiles-card-resized.png)

## Bearbeiten und Entfernen von Karten

Neben der Größenanpassung und Neuanordnung von Karten können Sie den Inhalt bestimmter Karten bearbeiten und einige Karten ganz aus dem Dashboard entfernen. Wählen Sie die Auslassungspunkte (`...`) in der oberen rechten Ecke der Karte aus, um sie zu bearbeiten oder zu entfernen. Dadurch wird ein Dropdown-Menü mit Optionen zum Bearbeiten oder Entfernen der Karte geöffnet, je nach den Eigenschaften der ausgewählten Karte.

>[!NOTE]
>
>Nicht alle Karten können bearbeitet oder entfernt werden. Dies liegt daran, dass einige Karten schreibgeschützte oder erforderliche Informationen enthalten. Wenn eine Karte keine Ellipsen in der oberen rechten Ecke enthält, enthält sie schreibgeschützte UND erforderliche Informationen und kann weder bearbeitet noch entfernt werden. Wenn eine Karte Ellipsen in der Ecke enthält und bei Auswahl dieser Option nur eine Option zum Entfernen der Karte angezeigt wird, sind die Karteninformationen schreibgeschützt und können nicht bearbeitet werden.

![](../images/profile-customization/profiles-edit-remove-resized.png)

Wählen Sie **[!UICONTROL Bearbeiten]** in der Dropdown-Liste, um den Arbeitsbereich **[!UICONTROL Widget bearbeiten]** zu öffnen. Dort können Sie den Kartentitel aktualisieren, die sichtbaren Attribute neu anordnen oder entfernen oder zusätzliche Attribute mithilfe der Schaltfläche **[!UICONTROL Hinzufügen Attribute]** hinzufügen.

![](../images/profile-customization/profiles-edit-widget-basic-attributes.png)

## hinzufügen Attribute {#add-attributes}

Wählen Sie im Bildschirm **[!UICONTROL Widget bearbeiten]** in der oberen rechten Ecke der Karte **[!UICONTROL Hinzufügen Attribute]** aus, um dieser Karte Attribute hinzuzufügen.

![](../images/profile-customization/profiles-edit-widget-basic-add-attributes.png)

Wenn das Dialogfeld **[!UICONTROL Schema Vereinigung auswählen]** geöffnet wird, wird auf der linken Seite des Dialogfelds das vollständige Schema [!UICONTROL XDM Individuelles Profil] Vereinigung angezeigt, dessen Felder darunter verschachtelt sind. Weitere Informationen zu Schemas der Vereinigung finden Sie im Abschnitt [Vereinigung Schemas des [!DNL Profile] Benutzerhandbuchs](user-guide.md#union-schema).

Im Abschnitt **[!UICONTROL Ausgewählte Attribute]** auf der rechten Seite des Dialogfelds werden die Attribute angezeigt, die aktuell in der Karte enthalten sind, die Sie bearbeiten. Sie können Attribute auch hier entfernen und neu anordnen. Die Gesamtzahl der ausgewählten Attribute sowie die maximale Anzahl der Attribute (20), die einer einzelnen Karte hinzugefügt werden können, werden angezeigt.

![](../images/profile-customization/profiles-select-field-before.png)

Sie können alle verfügbaren Schema-Felder für Vereinigungen auswählen, um die Attribute auf der zu bearbeitenden Karte anzupassen. Die ausgewählten Felder werden mit einem Häkchen neben ihnen angezeigt und automatisch zur Liste der ausgewählten Attribute hinzugefügt. Nachdem Sie alle Attribute hinzugefügt haben, die auf der Karte angezeigt werden sollen, wählen Sie **[!UICONTROL Wählen Sie]** aus, um zum Bildschirm **[!UICONTROL Widget bearbeiten]** zurückzukehren.

![](../images/profile-customization/profiles-select-field-after.png)

Wenn Sie zum Bildschirm **[!UICONTROL Widget bearbeiten]** zurückkehren, sollte die Liste der Attribute auf der Karte jetzt aktualisiert werden, um Ihre Auswahl widerzuspiegeln. Sie können die Kartenattribute trotzdem entfernen oder neu anordnen oder den Kartentitel nach Bedarf bearbeiten. Nachdem die Änderungen abgeschlossen sind, wählen Sie **[!UICONTROL Speichern]**, um die Änderungen zu speichern.

![](../images/profile-customization/profiles-edit-widget-new-attributes.png)

Nach dem Speichern werden Sie zum Register **[!UICONTROL Detail]** zurückgeleitet, wo die aktualisierte Karte und die aktualisierten Attribute angezeigt werden.

![](../images/profile-customization/profiles-resized-card-new-attributes.png)

## hinzufügen einer neuen Karte {#add-a-new-card}

Um das Aussehen von Profilen innerhalb der Experience Platform weiter anzupassen, können Sie neue Karten zum Dashboard hinzufügen und die Attribute auswählen, die auf diesen Karten angezeigt werden sollen. Wählen Sie zunächst **[!UICONTROL Dashboard]** auf der Registerkarte **[!UICONTROL Detail]** ändern.

![](../images/profile-customization/profiles-modify-dashboard.png)

Wählen Sie anschließend **[!UICONTROL Hinzufügen Widget]** in der oberen linken Ecke des Dashboards aus.

![](../images/profile-customization/profiles-add-widget.png)

Wenn Sie eine neue Karte hinzufügen möchten, wird der Bildschirm **[!UICONTROL Widget bearbeiten]** geöffnet, in dem Sie einen Titel für die neue Karte eingeben und die Attribute auswählen können, die auf der Karte angezeigt werden sollen. Um der Karte Attribute hinzuzufügen, wählen Sie **[!UICONTROL Hinzufügen Attribute]**.

![](../images/profile-customization/profiles-edit-new-widget.png)

Wenn das Dialogfeld **[!UICONTROL Schema Vereinigung auswählen]** geöffnet wird, zeigt die linke Seite des Dialogfelds das vollständige Schema [!UICONTROL XDM Individuelles Profil] Vereinigung und der Abschnitt **[!UICONTROL Ausgewählte Attribute]** auf der rechten Seite des Dialogfelds die Attribute an, die Sie für Ihre  auswählen. Weitere Informationen zum Hinzufügen von Attributen finden Sie im Abschnitt [zum Hinzufügen von Attributen](#add-attributes), der weiter oben in diesem Dokument angezeigt wird.

Die Gesamtzahl der ausgewählten Attribute sowie die maximale Anzahl der Attribute (20), die einer einzelnen Karte hinzugefügt werden können, werden angezeigt. Sie können die ausgewählten Attribute auch aus diesem Bildschirm entfernen und neu anordnen. Nachdem Sie alle Attribute hinzugefügt haben, die auf der Karte angezeigt werden sollen, wählen Sie **[!UICONTROL Wählen Sie]** aus, um zum Bildschirm **[!UICONTROL Widget bearbeiten]** zurückzukehren.

![](../images/profile-customization/profiles-add-fields-new-widget.png)

Wenn Sie zum Bildschirm **[!UICONTROL Widget bearbeiten]** zurückkehren, sollte die Liste der Attribute auf der Karte Ihre Auswahl aus dem vorherigen Bildschirm widerspiegeln. Sie können Kartenattribute auch nach Bedarf neu anordnen und entfernen.

Um Ihre neue Karte zu speichern, müssen Sie zunächst einen **[!UICONTROL Kartentitel]** angeben, dann können Sie **[!UICONTROL Speichern]** auswählen und den Vorgang zum Erstellen der Karte abschließen.

![](../images/profile-customization/profiles-edit-new-widget-with-fields.png)

Nach dem Speichern werden Sie zum Register **[!UICONTROL Detail]** zurückgeleitet, wo Ihre neue Karte und Ihre neuen Attribute sichtbar sind.

![](../images/profile-customization/profiles-detail-new-widget.png)

## Standardkarten wiederherstellen

Wenn Sie sich jederzeit entscheiden, dass Sie Standardkarten wiederherstellen möchten, die entfernt wurden, haben Sie die Möglichkeit, dies schnell und einfach zu tun. Wählen Sie zunächst **[!UICONTROL Dashboard]** ändern und dann **[!UICONTROL Standardkarten wiederherstellen]**. Sobald die Standardkarten sichtbar sind, können Sie **[!UICONTROL Speichern]** auswählen, um Ihre Änderungen zu speichern, oder **[!UICONTROL Abbrechen]** wählen, wenn Sie die Standardkarten nicht wiederherstellen möchten.

![](../images/profile-customization/profiles-restore-default.png)

## Nächste Schritte

Indem Sie diesem Dokument folgen, sollten Sie jetzt in der Lage sein, die Profil-Ansicht für Ihr Unternehmen zu aktualisieren, einschließlich Hinzufügen und Entfernen von Karten, Bearbeiten von Kartendetails und -attributen sowie Neuanordnen und Ändern der Kartengröße. Weitere Informationen zum Arbeiten mit [!DNL Profile]-Daten in der Benutzeroberfläche der Experience Platform finden Sie im [[!DNL Profile] Benutzerhandbuch](user-guide.md).
