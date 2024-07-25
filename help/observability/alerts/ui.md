---
keywords: Experience Platform;Startseite;beliebte Themen;Datumsbereich
title: Handbuch zur Warnhinweis-Benutzeroberfläche
description: Hier erfahren Sie, wie Sie Warnhinweise in der Benutzeroberfläche von Experience Platform verwalten.
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 40%

---

# Handbuch zur Warnhinweis-Benutzeroberfläche

In der Adobe Experience Platform-Benutzeroberfläche können Sie einen Verlauf der empfangenen Warnungen anhand von Metriken anzeigen, die von Adobe Experience Platform Observability Insights bereitgestellt wurden. Über die Benutzeroberfläche können Sie auch verfügbare Warnhinweisregeln anzeigen, aktivieren, deaktivieren und abonnieren.

>[!NOTE]
>
>Eine Einführung in Warnhinweise in Experience Platform finden Sie unter [Warnhinweise – Übersicht](./overview.md).

Wählen Sie zunächst im linken Navigationsbereich **[!UICONTROL Warnhinweise]** aus.

![Warnt die Seite, die im linken Navigationsbereich [!UICONTROL Warnhinweise] markiert.](../images/alerts/ui/workspace.png)

## Verwalten von Warnhinweisregeln

Auf der Registerkarte **[!UICONTROL Durchsuchen]** werden die verfügbaren Regeln aufgelistet, die einen Warnhinweis auslösen können.

![Eine Liste der verfügbaren Warnhinweise wird auf der Registerkarte [!UICONTROL Durchsuchen] angezeigt.](../images/alerts/ui/rules.png)

Wählen Sie eine Regel aus der Liste aus, um ihre Beschreibung und ihre Konfigurationsparameter in der rechten Leiste anzuzeigen, einschließlich Schwellenwert und Schweregrad.

![Eine Warnregel wurde mit Details in der rechten Leiste hervorgehoben.](../images/alerts/ui/rule-details.png)

Wählen Sie auf die Auslassungspunkte (**...**) neben dem Namen einer Regel klicken, zeigt eine Dropdown-Liste die Steuerelemente zum Aktivieren oder Deaktivieren des Warnhinweises (je nach seinem aktuellen Status) und zum Abonnieren oder Abbestellen von E-Mail-Benachrichtigungen für den Warnhinweis.

![Die ausgewählten Ellipsen zeigen das Dropdown-Menü an.](../images/alerts/ui/disable-subscribe.png)

## Warnhinweis-Abonnierende verwalten

>[!NOTE]
>
> Um eine Warnung einer Adobe-Benutzer-ID, einer externen E-Mail-Adresse oder einer E-Mail-Gruppenliste zuzuweisen, müssen Sie Administrator sein.

Auf der Registerkarte **[!UICONTROL Durchsuchen]** werden die verfügbaren Regeln aufgelistet, die einen Warnhinweis auslösen können.

![Eine Liste der verfügbaren Warnungsregeln, die auf der Registerkarte [!UICONTROL Durchsuchen] angezeigt werden.](../images/alerts/ui/rules.png)

Wählen Sie die Auslassungszeichen (**...**) neben dem Namen einer Regel aus. Ein Dropdown-Menü zeigt Steuerelemente an. Wählen Sie **[!UICONTROL Warnhinweis-Abonnenten verwalten]** aus.

![Wählen Sie die Ellipsen aus, um das Dropdownmenü anzuzeigen. Die Option [!UICONTROL Abonnenten des Warnhinweises verwalten] ist hervorgehoben.](../images/alerts/ui/manage-alert-subscribers.png)

Die Seite [!UICONTROL Warnhinweis-Abonnenten verwalten] wird angezeigt. Um Benachrichtigungen bestimmten Benutzern zuzuweisen, geben Sie ihre Adobe-Benutzer-ID, ihre externe E-Mail-Adresse oder eine E-Mail-Gruppenliste ein und drücken Sie die Eingabetaste.

>[!NOTE]
>
>Um diese Benachrichtigung gleichzeitig an mehrere Benutzer zu senden, geben Sie eine Liste mit Benutzer-IDs oder E-Mail-Adressen getrennt durch Kommas an.

![Die Seite zum Verwalten von Abonnenten von Warnhinweisen mit den eingegebenen E-Mail-Adressen.](../images/alerts/ui/manage-alert-add-email.png)

Die E-Mail-Adressen werden in der Liste der aktuellen Abonnenten angezeigt. Wählen Sie **[!UICONTROL Aktualisieren]** aus.

![Die Seite zum Verwalten von Warnhinweis-Abonnenten, auf der Abonnenten und [!UICONTROL Aktualisieren] hervorgehoben werden.](../images/alerts/ui/manage-alert-subscribers-added-email.png)

Sie haben Ihrer Benachrichtigungsliste erfolgreich Benutzer hinzugefügt. Die gesendeten Benutzer erhalten jetzt E-Mail-Benachrichtigungen zu diesem Warnhinweis, wie in der Abbildung unten dargestellt.

![Ein E-Mail-Beispiel für die erhaltene Warnhinweis-Benachrichtigung.](../images/alerts/ui/manage-alert-subscribers-email.png)

## Aktivieren von E-Mail-Warnungen

Warnhinweise können direkt an Ihre E-Mail gesendet werden.

Wählen Sie das Glockensymbol (![Glockensymbol](/help/images/icons/bell.png)) im oberen Band rechts aus, um Benachrichtigungen und Mitteilungen anzuzeigen. Wählen Sie im angezeigten Dropdown-Menü das Zahnradsymbol (![Zahnradsymbol](/help/images/icons/settings.png)) aus, um auf die Seite mit den Experience Cloud-Voreinstellungen zuzugreifen.

![Eine Liste von Warnhinweisen, die das Glockensymbol und das Zahnradsymbol hervorheben.](../images/alerts/ui/edit-preferences.png)

Die Seite **Profil** wird angezeigt. Wählen Sie im linken Navigationsbereich **[!UICONTROL Benachrichtigungen]** aus, um auf die Voreinstellungen für E-Mail-Warnungen zuzugreifen.

![Die Profilseite, die im linken Navigationsbereich [!UICONTROL Benachrichtigungen] hervorhebt.](../images/alerts/ui/profile.png)

Scrollen Sie zum Abschnitt **E-Mails** am unteren Rand der Seite und wählen Sie **[!UICONTROL Instant notifications]** aus.

![Der auf der Profilseite hervorgehobene Abschnitt &quot;E-Mails&quot;.](../images/alerts/ui/notifications.png)

Alle Warnungen, die Sie abonniert haben, werden jetzt an die E-Mail-Adresse gesendet, die mit Ihrem Adobe ID-Konto verbunden ist.

## Anzeigen des Warnhinweisverlaufs

Die Registerkarte **[!UICONTROL Verlauf]** zeigt den Verlauf der empfangenen Warnhinweise für Ihre Organisation, einschließlich der Regel, die den jeweiligen Warnhinweis ausgelöst hat, des Auslösedatums und ggf. des Auflösungsdatums.

![Eine Liste der empfangenen Warnungen wird auf der Registerkarte [!UICONTROL Verlauf] angezeigt.](../images/alerts/ui/history.png)

Wenn Sie einen aufgelisteten Warnhinweis auswählen, werden weitere Details in der rechten Leiste angezeigt, einschließlich einer kurzen Zusammenfassung des Ereignisses, das den Warnhinweis ausgelöst hat.

![Ein Warnhinweis, der Details in der rechten Leiste anzeigt.](../images/alerts/ui/history-details.png)

## Nächste Schritte

Dieses Dokument bietet eine Übersicht darüber, wie Warnhinweise in der Platform-Benutzeroberfläche angezeigt und verwaltet werden. Weitere Informationen zu den Funktionen dieses Services finden Sie in der Übersicht zu [Observability Insights](../home.md).
