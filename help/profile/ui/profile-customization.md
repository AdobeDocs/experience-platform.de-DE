---
keywords: Experience Platform;profile;real-time customer profile;user interface;UI;customization;profile details;details
title: Profil-Detailanpassung
description: 'Dieses Handbuch enthält schrittweise Anleitungen zum Anpassen der Art und Weise, wie Kundendaten in Echtzeit in der Adobe Experience Platform-Benutzeroberfläche angezeigt werden. '
topic: guide
translation-type: tm+mt
source-git-commit: d05884c87445ec16b0ad44f593cf782b8c80d646
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] Detail-Anpassung {#profile-detail-customization}

Auf der Adobe Experience Platform-Benutzeroberfläche können Sie Daten in Form von Kundendaten Ansicht und Interaktion mit [!DNL Real-time Customer Profile] Profilen durchführen. Die in der Benutzeroberfläche angezeigten Informationen zum Profil wurden aus mehreren Profil-Fragmenten zusammengeführt, um eine Ansicht des jeweiligen Kunden zu bilden. Dazu gehören Details wie Basisattribute, verknüpfte Identitäten und Voreinstellungen für Kanal. Die in den Profilen angezeigten Standardfelder können auch auf organisatorischer Ebene geändert werden, um bevorzugte [!DNL Profile] Attribute anzuzeigen. Dieses Handbuch enthält schrittweise Anleitungen zum Anpassen der Art und Weise, wie [!DNL Profile] Daten in der Plattform-Benutzeroberfläche angezeigt werden.

Eine vollständige Anleitung zur Benutzeroberfläche für Profile finden Sie im Handbuch [Profil-Benutzeroberfläche](user-guide.md).

## Karten neu anordnen und Größe ändern {#reorder-and-resize-cards}

Wählen Sie auf der Registerkarte &quot; **[!UICONTROL Details]** &quot;des Profils &quot;Kunden&quot;die Option &quot;Dashboard **** ändern&quot;aus, um die Größe der vorhandenen Karten zu ändern und neu anzuordnen.

![](../images/profile-customization/profiles-modify-dashboard.png)

Nachdem Sie das Dashboard geändert haben, können Sie die Reihenfolge der Karten ändern, indem Sie den Kartentitel auswählen und die Karten in die gewünschte Reihenfolge ziehen. Sie können die Größe einer Karte auch ändern, indem Sie das Winkelsymbol in der unteren rechten Ecke der Karte auswählen (`⌟`) und die Karte auf die gewünschte Größe ziehen. In diesem Beispiel wird die Größe der Karte &quot; **[!UICONTROL Grundlegende Attribute]** &quot;geändert.

![](../images/profile-customization/profiles-resize-cards.png)

Die ausgewählte Karte passt sich der gewünschten Größe an und die umliegenden Karten werden dynamisch neu positioniert. Dies kann dazu führen, dass einige Karten in zusätzliche Zeilen verschoben werden, sodass Sie nach unten blättern müssen, um alle Karten anzuzeigen. Wenn beispielsweise die Größe der Karte &quot;[!UICONTROL Grundlegende Attribute]&quot;geändert wird, ist die Karte &quot;[!UICONTROL Verlinkte Identitäten]&quot;nicht mehr in der oberen Zeile sichtbar und wird jetzt in einer neuen zweiten Zeile im Profil angezeigt (nicht angezeigt). Um die Karte &quot;[!UICONTROL Verlinkte Identitäten]&quot;an die oberste Zeile zurückzugeben, können Sie sie per Drag &amp; Drop an die aktuelle Position der Karte &quot;[!UICONTROL Kanal-Voreinstellungen]&quot;ziehen.

![](../images/profile-customization/profiles-card-resized.png)

## Bearbeiten und Entfernen von Karten

Neben der Größenanpassung und Neuanordnung von Karten können Sie den Inhalt bestimmter Karten bearbeiten und einige Karten ganz aus dem Dashboard entfernen. Wählen Sie die Ellipsen (`...`) in der oberen rechten Ecke der Karte aus, um sie zu bearbeiten oder zu entfernen. Dadurch wird ein Dropdown-Menü mit Optionen zum Bearbeiten oder Entfernen der Karte geöffnet, je nach den Eigenschaften der ausgewählten Karte.

>[!NOTE]
>
>Nicht alle Karten können bearbeitet oder entfernt werden. Dies liegt daran, dass einige Karten schreibgeschützte oder erforderliche Informationen enthalten. Wenn eine Karte keine Ellipsen in der oberen rechten Ecke enthält, enthält sie schreibgeschützte UND erforderliche Informationen und kann weder bearbeitet noch entfernt werden. Wenn eine Karte Ellipsen in der Ecke enthält und bei Auswahl dieser Option nur eine Option zum Entfernen der Karte angezeigt wird, sind die Karteninformationen schreibgeschützt und können nicht bearbeitet werden.

![](../images/profile-customization/profiles-edit-remove-resized.png)

Wählen Sie **[!UICONTROL Bearbeiten]** im Dropdown-Menü, um den Arbeitsbereich &quot;Widget **** bearbeiten&quot;zu öffnen. Dort können Sie den Kartentitel aktualisieren, die sichtbaren Attribute neu anordnen oder entfernen oder zusätzliche Attribute mithilfe der Schaltfläche &quot; **[!UICONTROL Hinzufügen Attribute]** &quot;hinzufügen.

![](../images/profile-customization/profiles-edit-widget-basic-attributes.png)

## hinzufügen {#add-attributes}

Wählen Sie im Bildschirm &quot;Widget **[!UICONTROL bearbeiten]** &quot;in der oberen rechten Ecke der Karte die **[!UICONTROL Hinzufügen Attribute]** aus, um dieser Karte Attribute hinzuzufügen.

![](../images/profile-customization/profiles-edit-widget-basic-add-attributes.png)

Wenn das Dialogfeld &quot;Vereinigung **[!UICONTROL auswählen&quot;]** geöffnet wird, wird auf der linken Seite des Dialogfelds das vollständige Schema zur Vereinigung des [!UICONTROL XDM-Profils] angezeigt, dessen Felder darunter verschachtelt sind. Weitere Informationen zu Schemas der Vereinigung finden Sie im Abschnitt zu Schemas der [Vereinigung im [!DNL Profile] Benutzerhandbuch](user-guide.md#union-schema).

Im Abschnitt &quot; **[!UICONTROL Ausgewählte Attribute]** &quot;auf der rechten Seite des Dialogfelds werden die Attribute angezeigt, die aktuell in der Karte enthalten sind, die Sie bearbeiten. Sie können Attribute auch hier entfernen und neu anordnen. Die Gesamtzahl der ausgewählten Attribute sowie die maximale Anzahl der Attribute (20), die einer einzelnen Karte hinzugefügt werden können, werden angezeigt.

![](../images/profile-customization/profiles-select-field-before.png)

Sie können alle verfügbaren Schema-Felder für Vereinigungen auswählen, um die Attribute auf der zu bearbeitenden Karte anzupassen. Die ausgewählten Felder werden mit einem Häkchen neben ihnen angezeigt und automatisch zur Liste der ausgewählten Attribute hinzugefügt. Nachdem Sie alle Attribute hinzugefügt haben, die auf der Karte angezeigt werden sollen, wählen Sie &quot; **[!UICONTROL Auswählen]** &quot;, um zum Bildschirm &quot;Widget **[!UICONTROL bearbeiten]** &quot;zurückzukehren.

![](../images/profile-customization/profiles-select-field-after.png)

Wenn Sie zum Bildschirm &quot;Widget **[!UICONTROL bearbeiten]** &quot;zurückkehren, sollte die Liste der Attribute auf der Karte jetzt aktualisiert werden, um Ihre Auswahl widerzuspiegeln. Sie können die Kartenattribute trotzdem entfernen oder neu anordnen oder den Kartentitel nach Bedarf bearbeiten. Nachdem die Änderungen abgeschlossen sind, wählen Sie **[!UICONTROL Speichern]** , um die Änderungen zu speichern.

![](../images/profile-customization/profiles-edit-widget-new-attributes.png)

Nach dem Speichern werden Sie zur Registerkarte &quot; **[!UICONTROL Details]** &quot;zurückgeleitet, auf der die aktualisierte Karte und die aktualisierten Attribute angezeigt werden.

![](../images/profile-customization/profiles-resized-card-new-attributes.png)

## Add a new card {#add-a-new-card}

Um das Aussehen von Profilen innerhalb der Experience Platform weiter anzupassen, können Sie neue Karten zum Dashboard hinzufügen und die Attribute auswählen, die auf diesen Karten angezeigt werden sollen. Wählen Sie zunächst auf der Registerkarte &quot; **[!UICONTROL Details&quot;die Option &quot;Dashboard]** **[!UICONTROL ändern&quot;]** .

![](../images/profile-customization/profiles-modify-dashboard.png)

Wählen Sie dann **[!UICONTROL Hinzufügen Widget]** in der oberen linken Ecke des Dashboards aus.

![](../images/profile-customization/profiles-add-widget.png)

Wenn Sie eine neue Karte hinzufügen möchten, wird der Bildschirm &quot;Widget **** bearbeiten&quot;geöffnet, in dem Sie einen Titel für die neue Karte eingeben und die Attribute auswählen können, die auf der Karte angezeigt werden sollen. Um der Karte Attribute hinzuzufügen, wählen Sie **[!UICONTROL Hinzufügen Attribute]**.

![](../images/profile-customization/profiles-edit-new-widget.png)

Wenn das Dialogfeld &quot;Schema **[!UICONTROL für Vereinigung]** auswählen&quot;geöffnet wird, wird auf der linken Seite des Dialogfelds das vollständige Schema für die Vereinigung des [!UICONTROL XDM-Profils] angezeigt. Die **[!UICONTROL ausgewählten Attribute]** auf der rechten Seite des Dialogfelds zeigen die von Ihnen ausgewählten  an. Weitere Informationen zum Hinzufügen von Attributen finden Sie im [Abschnitt zum Hinzufügen von Attributen](#add-attributes) , der weiter oben in diesem Dokument angezeigt wird.

Die Gesamtzahl der ausgewählten Attribute sowie die maximale Anzahl der Attribute (20), die einer einzelnen Karte hinzugefügt werden können, werden angezeigt. Sie können die ausgewählten Attribute auch aus diesem Bildschirm entfernen und neu anordnen. Nachdem Sie alle Attribute hinzugefügt haben, die auf der Karte angezeigt werden sollen, wählen Sie &quot; **[!UICONTROL Auswählen]** &quot;, um zum Bildschirm &quot;Widget **[!UICONTROL bearbeiten]** &quot;zurückzukehren.

![](../images/profile-customization/profiles-add-fields-new-widget.png)

Wenn Sie zum Bildschirm &quot;Widget **[!UICONTROL bearbeiten]** &quot;zurückkehren, sollte die Liste der Attribute auf der Karte Ihre Auswahl aus dem vorherigen Bildschirm widerspiegeln. Sie können Kartenattribute auch nach Bedarf neu anordnen und entfernen.

Um Ihre neue Karte zu speichern, müssen Sie zunächst einen **[!UICONTROL Kartentitel]** angeben, dann können Sie &quot; **[!UICONTROL Speichern]** &quot;wählen und den Kartenerstellungsprozess abschließen.

![](../images/profile-customization/profiles-edit-new-widget-with-fields.png)

Nach dem Speichern werden Sie zur Registerkarte &quot; **[!UICONTROL Details]** &quot;zurückgeleitet, auf der Ihre neue Karte und Ihre neuen Attribute angezeigt werden.

![](../images/profile-customization/profiles-detail-new-widget.png)

## Standardkarten wiederherstellen

Wenn Sie sich jederzeit entscheiden, dass Sie Standardkarten wiederherstellen möchten, die entfernt wurden, haben Sie die Möglichkeit, dies schnell und einfach zu tun. Wählen Sie zunächst &quot;Dashboard ****&#x200B;ändern&quot;und dann &quot;Standardkarten **[!UICONTROL wiederherstellen&quot;]**. Sobald die Standardkarten sichtbar sind, können Sie &quot; **[!UICONTROL Speichern]** &quot;auswählen, um die Änderungen zu speichern, oder auf &quot; **[!UICONTROL Abbrechen]** &quot;klicken, wenn Sie die Standardkarten nicht wiederherstellen möchten.

![](../images/profile-customization/profiles-restore-default.png)

## Nächste Schritte

Indem Sie diesem Dokument folgen, sollten Sie jetzt in der Lage sein, die Profil-Ansicht für Ihr Unternehmen zu aktualisieren, einschließlich Hinzufügen und Entfernen von Karten, Bearbeiten von Kartendetails und -attributen sowie Neuanordnen und Ändern der Kartengröße. Weitere Informationen zum Arbeiten mit [!DNL Profile] Daten in der Benutzeroberfläche der Experience Platform finden Sie im [[!DNL Profile] Benutzerhandbuch](user-guide.md).