---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Benutzeroberfläche; Benutzeroberfläche; Anpassung; Profildetails; Details
title: Anpassung der Profildetails in der Benutzeroberfläche
description: Dieses Handbuch enthält schrittweise Anweisungen zum Anpassen der Art und Weise, wie Echtzeit-Kundenprofildaten in der Benutzeroberfläche von Adobe Experience Platform angezeigt werden.
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
source-git-commit: 69ac6d3f98675df11183082ecbbb49d18ddb57af
workflow-type: tm+mt
source-wordcount: '1394'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile]-Detailanpassung {#profile-detail-customization}

In der Benutzeroberfläche von Adobe Experience Platform können Sie [!DNL Real-Time Customer Profile] -Daten in Form von Kundenprofilen anzeigen und damit interagieren. Die in der Benutzeroberfläche angezeigten Profilinformationen wurden aus mehreren Profilfragmenten zusammengeführt, um für jeden einzelnen Kunden eine einzige Ansicht zu erstellen. Dazu gehören Details wie grundlegende Attribute, verknüpfte Identitäten und Kanalvoreinstellungen. Die in Profilen angezeigten Standardfelder können auch auf Organisationsebene geändert werden, um die bevorzugten [!DNL Profile] Attribute anzuzeigen. Dieses Handbuch enthält schrittweise Anweisungen zum Anpassen der Anzeige von [!DNL Profile]-Daten in der Platform-Benutzeroberfläche.

Eine vollständige Anleitung zur Benutzeroberfläche &quot;Profile&quot;finden Sie im [Handbuch zur Benutzeroberfläche des Profils](user-guide.md).

## Karten neu anordnen und Größe ändern {#reorder-and-resize-cards}

Auf der Registerkarte **[!UICONTROL Detail]** des Kundenprofils können Sie **[!UICONTROL Profildetails anpassen]** auswählen, um die Größe vorhandener Karten zu ändern und neu anzuordnen.

![Die Schaltfläche Profildetails anpassen wird im Profil-Dashboard hervorgehoben.](../images/profile-customization/customize-profile-details.png)

Nachdem Sie sich entschieden haben, das Dashboard zu ändern, können Sie die Karten neu anordnen, indem Sie den Kartentitel auswählen und die Karten in die gewünschte Reihenfolge ziehen. Sie können die Größe einer Karte auch ändern, indem Sie das Winkelsymbol in der rechten unteren Ecke der Karte (`⌟`) auswählen und die Karte auf die gewünschte Größe ziehen. In diesem Beispiel wird die Größe der Karte **[!UICONTROL Grundlegende Attribute]** geändert.

![Die Schaltfläche zum Ändern der Größe wird auf der Karte Grundlegende Attribute hervorgehoben.](../images/profile-customization/resize.png)

Die ausgewählte Karte passt sich der gewünschten Größe an und die umliegenden Karten werden dynamisch neu positioniert. Dies kann dazu führen, dass einige Karten in zusätzliche Zeilen verschoben werden, sodass Sie nach unten scrollen müssen, um alle Karten zu sehen. Wenn beispielsweise die Größe der Karte &quot;[!UICONTROL Grundlegende Attribute]&quot; geändert wird, ist die Karte &quot;[!UICONTROL Verknüpfte Identitäten]&quot; nicht mehr in der obersten Zeile sichtbar und wird nun in einer neuen zweiten Zeile im Profil angezeigt (nicht angezeigt). Um die Karte &quot;[!UICONTROL Verknüpfte Identitäten]&quot; in die oberste Zeile zurückzugeben, können Sie sie per Drag-and-Drop an die aktuelle Position der Karte &quot;[!UICONTROL Kanalvoreinstellungen]&quot; ziehen.

![Eine Karte mit einer neuen Größe wird hervorgehoben.](../images/profile-customization/resized.png)

## Bearbeiten und Entfernen von Karten

Neben der Größenanpassung und Neuordnung von Karten können Sie den Inhalt bestimmter Karten bearbeiten und einige Karten vollständig aus dem Dashboard entfernen. Wählen Sie die Auslassungszeichen (`...`) in der oberen rechten Ecke der Karte aus, um sie zu bearbeiten oder zu entfernen. Dadurch wird ein Dropdown-Menü mit Optionen zum Bearbeiten oder Entfernen der Karte geöffnet, je nach den Eigenschaften der ausgewählten Karte.

>[!NOTE]
>
>Nicht alle Karten können bearbeitet oder entfernt werden. Dies liegt daran, dass einige Karten schreibgeschützte oder erforderliche Informationen enthalten. Wenn eine Karte keine Auslassungspunkte in der oberen rechten Ecke aufweist, enthält sie schreibgeschützte UND erforderliche Informationen und kann weder bearbeitet noch entfernt werden. Wenn eine Karte in der Ecke Ellipsen enthält und bei Auswahl nur eine Option zum Entfernen der Karte angezeigt wird, sind die Karteninformationen schreibgeschützt und können nicht bearbeitet werden.

![Das Dropdown-Menü &quot;Bearbeitungskarte&quot;wird hervorgehoben. Dazu gehören Optionen zum Bearbeiten oder Entfernen der Karte.](../images/profile-customization/edit-card.png)

Wählen Sie im Dropdown-Menü **[!UICONTROL Bearbeiten]** aus, um den Arbeitsbereich **[!UICONTROL Widget bearbeiten]** zu öffnen. Dort können Sie den Kartentitel aktualisieren, die sichtbaren Attribute neu anordnen oder entfernen oder zusätzliche Attribute mithilfe der Schaltfläche **[!UICONTROL Attribute hinzufügen]** hinzufügen.

![Die Karte &quot;Grundlegende Attribute&quot;wird angezeigt.](../images/profile-customization/basic-attributes.png)

## Attribute hinzufügen {#add-attributes}

Wählen Sie im Bildschirm **[!UICONTROL Widget bearbeiten]** oben rechts auf der Karte die Option **[!UICONTROL Attribute hinzufügen]** aus, um dieser Karte Attribute hinzuzufügen.

![Die Schaltfläche &quot;Attribute hinzufügen&quot;auf der Karte &quot;Grundlegende Attribute&quot;ist hervorgehoben.](../images/profile-customization/add-attributes.png)

Wenn das Dialogfeld **[!UICONTROL Vereinigungsschema-Feld auswählen]** geöffnet wird, wird auf der linken Seite des Dialogfelds das vollständige Vereinigungsschema [!UICONTROL XDM Individual Profile] mit unter dem Feld verschachtelten Feldern angezeigt. Weiterführende Informationen zu Vereinigungsschemata finden Sie im Abschnitt [Vereinigungsschemas des [!DNL Profile] Benutzerhandbuchs](user-guide.md#union-schema).

Im Abschnitt **[!UICONTROL Ausgewählte Attribute]** auf der rechten Seite des Dialogfelds werden die Attribute angezeigt, die derzeit in der Karte enthalten sind, die Sie bearbeiten. Sie können Attribute auch hier entfernen und neu anordnen. Es werden die Gesamtzahl der ausgewählten Attribute sowie die maximale Anzahl der Attribute (20) angezeigt, die einer einzelnen Karte hinzugefügt werden können.

![Die Attribute, aus denen sich derzeit die Attribute auf der Karte zusammensetzen, werden hervorgehoben.](../images/profile-customization/select-before.png)

Sie können eines der verfügbaren Vereinigungsschemafelder auswählen, um die Attribute auf der Karte anzupassen, die Sie bearbeiten. Bei der Auswahl der Felder können Sie entweder den Dateinamen oder den Anzeigenamen anzeigen. Um zwischen diesen beiden Anzeigen zu wechseln, wählen Sie den Umschalter **[!UICONTROL Anzeigenamen anzeigen]** aus.

![Der Umschalter [!UICONTROL Anzeigenamen anzeigen] wird auf der Seite mit den Profildetails hervorgehoben.](../images/profile-customization/show-display-names.png)

Ausgewählte Felder werden mit einem Häkchen neben ihnen angezeigt und automatisch zur Liste der ausgewählten Attribute hinzugefügt. Nachdem Sie alle Attribute hinzugefügt haben, die Sie auf der Karte angezeigt haben möchten, wählen Sie **[!UICONTROL Auswählen]** aus, um zum Bildschirm **[!UICONTROL Widget bearbeiten]** zurückzukehren.

![Die neu hinzugefügten Attribute werden hervorgehoben.](../images/profile-customization/select-after.png)

Wenn Sie zum Bildschirm **[!UICONTROL Widget bearbeiten]** zurückkehren, sollte die Liste der Attribute auf der Karte jetzt aktualisiert werden, um Ihre Auswahl widerzuspiegeln. Sie können die Kartenattribute dennoch entfernen oder neu anordnen oder den Kartentitel nach Bedarf bearbeiten. Nachdem die Änderungen abgeschlossen sind, wählen Sie **[!UICONTROL Speichern]** aus, um Ihre Änderungen zu speichern.

![Die neu hinzugefügten Attribute werden auf der bearbeiteten Karte angezeigt.](../images/profile-customization/new-attributes.png)

Nach dem Speichern kehren Sie zur Registerkarte **[!UICONTROL Detail]** zurück, auf der die aktualisierte Karte und Attribute sichtbar sind.

![Die neu hinzugefügten Attribute werden auf der Karte im Profil-Dashboard angezeigt.](../images/profile-customization/added-attributes.png)

## Neue Karte hinzufügen {#add-a-new-card}

Um das Erscheinungsbild von Profilen innerhalb von Experience Platform weiter anzupassen, können Sie neue Karten zum Dashboard hinzufügen und die Attribute auswählen, die auf diesen Karten angezeigt werden sollen. Wählen Sie zunächst **[!UICONTROL Dashboard ändern]** auf der Registerkarte **[!UICONTROL Detail]** aus.

![Die Schaltfläche Profildetails anpassen ist hervorgehoben.](../images/profile-customization/customize-profile-details.png)

Wählen Sie dann **[!UICONTROL Widget hinzufügen]** in der oberen linken Ecke des Dashboards aus.

![Die Schaltfläche Widget hinzufügen ist hervorgehoben.](../images/profile-customization/add-widget.png)

Wenn Sie eine neue Karte hinzufügen, wird der Bildschirm **[!UICONTROL Widget bearbeiten]** geöffnet. Hier können Sie einen Titel für die neue Karte angeben und die Attribute auswählen, die die Karte anzeigen soll. Um der Karte Attribute hinzuzufügen, wählen Sie **[!UICONTROL Attribute hinzufügen]** aus.

![Im Bildschirm &quot;Widget bearbeiten&quot;wird eine leere neue Widget-Karte angezeigt.](../images/profile-customization/edit-widget.png)

Wenn das Dialogfeld **[!UICONTROL Vereinigungsschema-Feld auswählen]** geöffnet wird, zeigt die linke Seite des Dialogfelds das vollständige Vereinigungsschema [!UICONTROL XDM Individual Profile] und der Abschnitt **[!UICONTROL Ausgewählte Attribute]** auf der rechten Seite des Dialogfelds zeigt die Attribute an, die Sie für Ihre Karte auswählen. Weitere Informationen zum Hinzufügen von Attributen finden Sie im Abschnitt [über das Hinzufügen von Attributen](#add-attributes), der zuvor in diesem Dokument angezeigt wird.

Es werden die Gesamtzahl der ausgewählten Attribute sowie die maximale Anzahl der Attribute (20) angezeigt, die einer einzelnen Karte hinzugefügt werden können. Sie können die ausgewählten Attribute auch aus diesem Bildschirm entfernen und neu anordnen. Nachdem Sie alle Attribute hinzugefügt haben, die auf der Karte angezeigt werden sollen, wählen Sie **[!UICONTROL Auswählen]** aus, um zum Bildschirm **[!UICONTROL Widget bearbeiten]** zurückzukehren.

![Die Felder, die Sie der Karte hinzufügen, werden hervorgehoben.](../images/profile-customization/add-widget-attributes.png)

Wenn Sie zum Bildschirm **[!UICONTROL Widget bearbeiten]** zurückkehren, sollte die Liste der Attribute auf der Karte Ihre Optionen aus dem vorherigen Bildschirm widerspiegeln. Sie können Kartenattribute nach Bedarf auch neu anordnen und entfernen.

Um Ihre neue Karte zu speichern, müssen Sie zunächst einen **[!UICONTROL Kartentitel]** angeben, dann können Sie **[!UICONTROL Speichern]** auswählen und den Kartenerstellungsprozess abschließen.

![Das neue Widget wird im Bildschirm &quot;Widget bearbeiten&quot;in der Vorschau angezeigt.](../images/profile-customization/new-widget.png)

Nach dem Speichern kehren Sie zur Registerkarte **[!UICONTROL Detail]** zurück, auf der Ihre neue Karte und Attribute sichtbar sind.

![Das neue Widget wird dem Profil-Dashboard hinzugefügt.](../images/profile-customization/added-widget.png)

## Standardkarten wiederherstellen

Wenn Sie sich entscheiden, Standardkarten wiederherzustellen, die inzwischen entfernt wurden, können Sie dies schnell und einfach tun. Wählen Sie zunächst **[!UICONTROL Dashboard ändern]** und dann **[!UICONTROL Standardkarten wiederherstellen]** aus. Sobald die Standardkarten sichtbar sind, können Sie **[!UICONTROL Speichern]** auswählen, um Ihre Änderungen zu speichern, oder **[!UICONTROL Abbrechen]** auswählen, wenn Sie die Standardkarten nicht wiederherstellen möchten.

![Die Schaltfläche Standardkarten wiederherstellen wird im Profil-Dashboard hervorgehoben.](../images/profile-customization/restore-default.png)

## Nächste Schritte

Durch Befolgen dieses Dokuments sollten Sie jetzt in der Lage sein, die Profilansicht für Ihr Unternehmen zu aktualisieren, einschließlich Hinzufügen und Entfernen von Karten, Bearbeiten von Kartendetails und -attributen sowie Neuanordnen und Größenanpassung von Karten. Weitere Informationen zum Arbeiten mit [!DNL Profile] Daten in der Experience Platform-Benutzeroberfläche finden Sie im [[!DNL Profile] Benutzerhandbuch](user-guide.md).
