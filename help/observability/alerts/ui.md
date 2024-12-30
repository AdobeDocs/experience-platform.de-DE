---
keywords: Experience Platform;Startseite;beliebte Themen;Datumsbereich
title: Handbuch zur Warnhinweis-Benutzeroberfläche
description: Hier erfahren Sie, wie Sie Warnhinweise in der Benutzeroberfläche von Experience Platform verwalten.
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: 2e0fc17fee9b1586b4c2b44c326e2c305c127fad
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 36%

---

# Handbuch zur Warnhinweis-Benutzeroberfläche

In der Adobe Experience Platform-Benutzeroberfläche können Sie einen Verlauf der empfangenen Warnungen anhand von Metriken anzeigen, die von Adobe Experience Platform Observability Insights bereitgestellt wurden. Über die Benutzeroberfläche können Sie auch verfügbare Warnhinweisregeln anzeigen, aktivieren, deaktivieren und abonnieren.

>[!NOTE]
>
>Eine Einführung in Warnhinweise in Experience Platform finden Sie unter [Warnhinweise – Übersicht](./overview.md).

Wählen Sie zunächst im linken Navigationsbereich **[!UICONTROL Warnhinweise]** aus.

![Warnhinweisseite mit hervorgehobener [!UICONTROL Warnhinweise] im linken Navigationsbereich.](../images/alerts/ui/workspace.png)

## Verwalten von Warnhinweisregeln {#manage-rules}

Auf der Registerkarte **[!UICONTROL Durchsuchen]** werden die verfügbaren Regeln aufgelistet, die einen Warnhinweis auslösen können.

![Eine Liste der verfügbaren Warnhinweise wird auf der Registerkarte [!UICONTROL Durchsuchen] angezeigt.](../images/alerts/ui/rules.png)

Wählen Sie eine Regel aus der Liste aus, um ihre Beschreibung und ihre Konfigurationsparameter in der rechten Leiste anzuzeigen, einschließlich Schwellenwert und Schweregrad.

![Eine hervorgehobene Warnregel mit Details in der rechten Leiste.](../images/alerts/ui/rule-details.png)

Wählen Sie auf die Auslassungspunkte (**...**) neben dem Namen einer Regel klicken, zeigt eine Dropdown-Liste die Steuerelemente zum Aktivieren oder Deaktivieren des Warnhinweises (je nach seinem aktuellen Status) und zum Abonnieren oder Abbestellen von E-Mail-Benachrichtigungen für den Warnhinweis.

![Die ausgewählten Auslassungszeichen zeigen das Dropdown-Menü an.](../images/alerts/ui/disable-subscribe.png)

## Warnhinweis-Abonnierende verwalten {#manage-subscribers}

>[!NOTE]
>
> Um einen Warnhinweis einer Adobe-Benutzer-ID, einer externen E-Mail-Adresse oder einer E-Mail-Gruppenliste zuzuweisen, müssen Sie Administrator sein.

Auf der Registerkarte **[!UICONTROL Durchsuchen]** werden die verfügbaren Regeln aufgelistet, die einen Warnhinweis auslösen können.

![Eine Liste der verfügbaren Warnhinweisregeln, die auf der Registerkarte [!UICONTROL Durchsuchen] angezeigt wird.](../images/alerts/ui/rules.png)

Klicken Sie auf die Auslassungszeichen (**…**) neben dem Namen einer Regel. In einem Dropdown-Menü werden dann Steuerelemente angezeigt. Wählen **[!UICONTROL Warnhinweis-Abonnenten verwalten]** aus.

![Wählen Sie die Auslassungszeichen aus, um das Dropdown-Menü anzuzeigen. Die [!UICONTROL Option „Warnhinweis-Abonnenten verwalten] ist hervorgehoben.](../images/alerts/ui/manage-alert-subscribers.png)

Die [!UICONTROL Warnhinweis-Abonnenten verwalten] wird angezeigt. Um Benachrichtigungen bestimmten Benutzern zuzuweisen, geben Sie deren Adobe-Benutzer-ID, externe E-Mail-Adresse oder eine E-Mail-Gruppenliste ein und drücken Sie dann die Eingabetaste.

>[!NOTE]
>
>Um diese Benachrichtigung an mehrere Benutzer gleichzeitig zu senden, geben Sie eine Liste der Benutzer-IDs oder E-Mail-Adressen an, die durch Kommas getrennt sind.

![Die Seite „Warnhinweis-Abonnenten verwalten“ mit den eingegebenen E-Mail-Adressen.](../images/alerts/ui/manage-alert-add-email.png)

Die E-Mail-Adressen werden in der Liste der aktuellen Abonnenten angezeigt. Wählen Sie **[!UICONTROL Aktualisieren]** aus.

![Die Seite „Warnhinweis-Abonnenten verwalten“ mit Hervorhebung von Abonnentinnen und Abonnenten und [!UICONTROL Aktualisieren].](../images/alerts/ui/manage-alert-subscribers-added-email.png)

Sie haben Benutzer erfolgreich zu Ihrer Benachrichtigungsliste für Warnhinweise hinzugefügt. Die gesendeten Benutzer erhalten jetzt E-Mail-Benachrichtigungen für diesen Warnhinweis, wie in der Abbildung unten dargestellt.

![Ein E-Mail-Beispiel für die empfangene Warnbenachrichtigung.](../images/alerts/ui/manage-alert-subscribers-email.png)

## E-Mail-Warnhinweise aktivieren {#enable-email}

Warnhinweise können direkt an Ihre E-Mail gesendet werden.

Wählen Sie das Glockensymbol (![Glockensymbol](/help/images/icons/bell.png)) im oberen Menüband auf der rechten Seite aus, um Benachrichtigungen und Ankündigungen anzuzeigen. Wählen Sie im angezeigten Dropdown-Menü das Zahnradsymbol (![Zahnradsymbol](/help/images/icons/settings.png)) aus, um die Seite mit den Experience Cloud-Voreinstellungen aufzurufen.

![Eine Liste von Warnhinweisen, die das Glockensymbol und das Zahnradsymbol hervorheben.](../images/alerts/ui/edit-preferences.png)

Die **&quot;**&quot; wird angezeigt. Wählen Sie **[!UICONTROL linken Navigationsbereich die Option]** Benachrichtigungen“ aus, um auf die E-Mail-Warnhinweiseinstellungen zuzugreifen.

![Die Profilseite mit hervorgehobener [!UICONTROL  &quot;]&quot; im linken Navigationsbereich.](../images/alerts/ui/profile.png)

Scrollen Sie zum Abschnitt **E** unten auf der Seite und wählen Sie **[!UICONTROL Sofortige Benachrichtigungen]**

![Der Abschnitt „E-Mails“, der auf der Profilseite hervorgehoben ist.](../images/alerts/ui/notifications.png)

Alle Warnhinweise, die Sie abonniert haben, werden jetzt an die E-Mail-Adresse gesendet, die mit Ihrem Adobe ID-Konto verbunden ist.

## Warnschwelle anpassen {#alert-threshold}

Warnschwellenwerte können für die folgenden Warnhinweistypen angepasst werden:

| Warnhinweistyp | Benutzerdefinierter Parameter |
|---|---|
| Verzögerung bei Segmentvorgängen | Verzögerungsschwellenwert |
| Verzögerung beim Segmentexport | Verzögerungsschwellenwert |
| Verzögerung bei der Ausführung des Zielflusses | Verzögerungsschwellenwert |
| Verzögerung bei der Ausführung des Identity Service-Flusses | Verzögerungsschwellenwert |
| Verzögerung bei der Ausführung eines Profilflusses | Verzögerungsschwellenwert |
| Verzögerung bei Flussausführung an der Quelle | Verzögerungsschwellenwert |
| Verzögerung der Abfrageausführung | Verzögerungsschwellenwert |
| Aktivierungsüberspringrate überschritten | Fehlerschwellenwert |
| Fehlerrate bei der Quellaufnahme überschritten | Fehlerschwellenwert |

Klicken Sie auf die Auslassungszeichen (**…**) neben dem Namen einer Regel. In einem Dropdown-Menü werden dann Steuerelemente angezeigt. Wählen Sie **[!UICONTROL Bearbeiten]** aus.

![Die Option [!UICONTROL Bearbeiten] für die ausgewählte Regel ist hervorgehoben.](../images/alerts/ui/threshold-edit.png)

Die **[!UICONTROL Warnhinweis anpassen]** wird angezeigt. Aktualisieren Sie den Schwellenwert auf die gewünschten Minuten und klicken Sie dann auf **[!UICONTROL Bestätigen]**.

![Die Warnhinweisseite mit Hervorhebung der Optionen [!UICONTROL Schwellenwert] und [!UICONTROL Bestätigen].](../images/alerts/ui/threshold-update.png)

Sie kehren zur Seite &quot;**[!UICONTROL &quot;]**. Um die Schwellenwerteinstellungen für den Warnhinweis anzuzeigen, wählen Sie die Regel aus der Liste aus. Sie können die Schwellenwerteinstellungen für den Warnhinweis in der rechten Leiste sehen, einschließlich Details wie Status und Schweregrad.

![Ein hervorgehobener Warnhinweis mit Details in der rechten Leiste und Hervorhebung [!UICONTROL Schwellenwert].](../images/alerts/ui/threshold-view.png)

## Anzeigen des Warnhinweisverlaufs {#alert-history}

Die Registerkarte **[!UICONTROL Verlauf]** zeigt den Verlauf der empfangenen Warnhinweise für Ihre Organisation, einschließlich der Regel, die den jeweiligen Warnhinweis ausgelöst hat, des Auslösedatums und ggf. des Auflösungsdatums.

![Eine Liste der empfangenen Warnhinweise wird auf der Registerkarte [!UICONTROL Verlauf] angezeigt.](../images/alerts/ui/history.png)

Wenn Sie einen aufgelisteten Warnhinweis auswählen, werden weitere Details in der rechten Leiste angezeigt, einschließlich einer kurzen Zusammenfassung des Ereignisses, das den Warnhinweis ausgelöst hat.

![Ein hervorgehobener Warnhinweis mit Details in der rechten Leiste.](../images/alerts/ui/history-details.png)

## Nächste Schritte

Dieses Dokument bietet eine Übersicht darüber, wie Warnhinweise in der Platform-Benutzeroberfläche angezeigt und verwaltet werden. Weitere Informationen zu den Funktionen dieses Services finden Sie in der Übersicht zu [Observability Insights](../home.md).
