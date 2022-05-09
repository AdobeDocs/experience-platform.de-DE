---
keywords: Experience Platform;Startseite;beliebte Themen;Datumsbereich
title: Handbuch zur Warnhinweis-Benutzeroberfläche
description: Hier erfahren Sie, wie Sie Warnhinweise in der Benutzeroberfläche von Experience Platform verwalten.
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: ed18ecea98497e0c20d44617436a013bf83b69d2
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 69%

---

# Handbuch zur Warnhinweis-Benutzeroberfläche

In der Adobe Experience Platform-Benutzeroberfläche können Sie einen Verlauf der empfangenen Warnungen anhand von Metriken anzeigen, die von Adobe Experience Platform Observability Insights bereitgestellt wurden. Über die Benutzeroberfläche können Sie auch verfügbare Warnhinweisregeln anzeigen, aktivieren, deaktivieren und abonnieren.

>[!NOTE]
>
>Eine Einführung in Warnhinweise in Experience Platform finden Sie unter [Warnhinweise – Übersicht](./overview.md).

Wählen Sie zunächst im linken Navigationsbereich **[!UICONTROL Warnhinweise]** aus.

![](../images/alerts/ui/workspace.png)

## Verwalten von Warnhinweisregeln

Auf der Registerkarte **[!UICONTROL Durchsuchen]** werden die verfügbaren Regeln aufgelistet, die einen Warnhinweis auslösen können.

![](../images/alerts/ui/rules.png)

Wählen Sie eine Regel aus der Liste aus, um ihre Beschreibung und ihre Konfigurationsparameter in der rechten Leiste anzuzeigen, einschließlich Schwellenwert und Schweregrad.

![](../images/alerts/ui/rule-details.png)

Wählen Sie auf die Auslassungspunkte (**...**) neben dem Namen einer Regel klicken, zeigt eine Dropdown-Liste die Steuerelemente zum Aktivieren oder Deaktivieren des Warnhinweises (je nach seinem aktuellen Status) und zum Abonnieren oder Abbestellen von E-Mail-Benachrichtigungen für den Warnhinweis.

![](../images/alerts/ui/disable-subscribe.png)

## Aktivieren von E-Mail-Warnungen

Warnhinweise können direkt an Ihre E-Mail gesendet werden.

Wählen Sie das Glockensymbol (![Glockensymbol](../images/alerts/ui/bell-icon.png)) im oberen Band auf der rechten Seite, um Benachrichtigungen und Mitteilungen anzuzeigen. Wählen Sie im angezeigten Dropdown-Menü das Zahnradsymbol (![Zahnradsymbol](../images/alerts/ui/cog-icon.png)), um auf die Seite mit den Experience Cloud-Voreinstellungen zuzugreifen.

![](../images/alerts/ui/edit-preferences.png)

Die **Profil** angezeigt. Wählen Sie die **[!UICONTROL Benachrichtigungen]** im linken Navigationsbereich, um auf die Voreinstellungen für E-Mail-Warnungen zuzugreifen.

![](../images/alerts/ui/profile.png)

Scrollen Sie zum **E-Mails** im unteren Bereich der Seite und wählen Sie **[!UICONTROL Sofortige Benachrichtigungen]**

![](../images/alerts/ui/notifications.png)

Alle Warnungen, die Sie abonniert haben, werden jetzt an die E-Mail-Adresse gesendet, die mit Ihrem Adobe ID-Konto verbunden ist.

## Anzeigen des Warnhinweisverlaufs

Die Registerkarte **[!UICONTROL Verlauf]** zeigt den Verlauf der empfangenen Warnhinweise für Ihre Organisation, einschließlich der Regel, die den jeweiligen Warnhinweis ausgelöst hat, des Auslösedatums und ggf. des Auflösungsdatums.

![](../images/alerts/ui/history.png)

Wenn Sie einen aufgelisteten Warnhinweis auswählen, werden weitere Details in der rechten Leiste angezeigt, einschließlich einer kurzen Zusammenfassung des Ereignisses, das den Warnhinweis ausgelöst hat.

![](../images/alerts/ui/history-details.png)

## Nächste Schritte

Dieses Dokument bietet eine Übersicht darüber, wie Warnhinweise in der Platform-Benutzeroberfläche angezeigt und verwaltet werden. Weitere Informationen zu den Funktionen dieses Services finden Sie in der Übersicht zu [Observability Insights](../home.md).
