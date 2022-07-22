---
title: Dashboard "Kontoprofile"
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zu den B2B-Kontoprofilen Ihres Unternehmens anzeigen können.
source-git-commit: 4ff30c689808e0513245852625efc4a162ab2c0e
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 4%

---

# [!UICONTROL Kontoprofile] Dashboard

Die Adobe Experience Platform-Benutzeroberfläche bietet ein Dashboard, über das Sie wichtige Informationen zu Ihren Kontoprofilen anzeigen können, die in einer täglichen Momentaufnahme erfasst werden. In diesem Handbuch wird beschrieben, wie Sie auf die [!UICONTROL Kontoprofile] Dashboard in der Benutzeroberfläche und bietet weitere Informationen zu den im Dashboard angezeigten Visualisierungen.

Einen Überblick über alle Funktionen in der Benutzeroberfläche des Kontoprofils erhalten Sie im [Benutzeroberflächenleitfaden für Kontoprofile](../../rtcdp/accounts/account-profile-ui-guide.md).

## Erste Schritte

Sie müssen [Real-time Customer Data Platform B2B Edition](../../rtcdp/b2b-overview.md) für den Zugang zum B2B [!UICONTROL Kontoprofile] Dashboard.

## Kontoprofildaten

Die [!UICONTROL Kontoprofile] Dashboard zeigt eine Momentaufnahme der einheitlichen Kontoinformationen aus den verschiedenen Quellen in Ihren Marketing-Kanälen und den verschiedenen Systemen an, die Ihr Unternehmen derzeit zum Speichern von Kundenkontoinformationen verwendet.

Die Profildaten im Schnappschuss zeigen die Daten exakt so an, wie sie zu dem Zeitpunkt angezeigt werden, zu dem der Schnappschuss erstellt wurde. Mit anderen Worten, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten, und die [!UICONTROL Kontoprofile] Das Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme des Schnappschusses an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn der nächste Schnappschuss erstellt wurde.

## Die [!UICONTROL Kontoprofile] Dashboard

So navigieren Sie zum [!UICONTROL Kontoprofile] Dashboard in der Platform-Benutzeroberfläche auswählen **[!UICONTROL Profile]** under [!UICONTROL Konten] im linken Navigationsbereich.

![Die Platform-Benutzeroberfläche mit Kontoprofilen im linken Navigationsbereich wurde hervorgehoben und die Registerkarte Übersicht wurde angezeigt.](../images/account-profiles/account-profiles-dashboard.png)

Aus dem [!UICONTROL Kontoprofile] Dashboard können Sie [die in Ihrer Organisation erfassten Kontoprofile durchsuchen](#browse-account-profiles)oder [Zeigen Sie die Gesamtheit Ihrer Kontoprofildaten mithilfe von Widgets auf einen Blick an.](#standard-widgets) , die Aspekte der Daten visualisieren.

## Durchsuchen von Account-Profilen {#browse-account-profiles}

Die [!UICONTROL Durchsuchen] -Tab können Sie die in Ihrem Unternehmen erfassten schreibgeschützten Kontoprofile mithilfe einer Konto-ID aus einer verbundenen Unternehmensquelle suchen und anzeigen oder Quelldetails direkt eingeben. Von hier aus können Sie wichtige Informationen aus dem Kontoprofil sehen, einschließlich Name, Branche, Umsatz und Segment.

Wählen Sie die [!UICONTROL Profil-ID] aus den auf der [!UICONTROL Durchsuchen] Registerkarte zum Öffnen [!UICONTROL Details] für das Kontoprofil.

![Auf der Registerkarte &quot;Kontoprofile&quot;werden die Ergebnisse angezeigt und die Profil-ID hervorgehoben.](../images/account-profiles/account-profiles-browse-tab.png) —>

Die Kontoprofilinformationen werden auf der Seite [!UICONTROL Details] wurde aus mehreren Profilfragmenten zusammengeführt, um eine Ansicht des einzelnen Kontos zu bilden. Weitere Informationen finden Sie in der Dokumentation unter [Durchsuchen von Kontoprofilen in Real-time Customer Data Platform](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) , um mehr über die Anzeigefunktionen von Kontoprofilen in der Platform-Benutzeroberfläche zu erfahren.

## Die [!UICONTROL Kontoprofile] [!UICONTROL Übersicht] {#overview}

Die [!UICONTROL Übersicht] -Registerkarte besteht aus Widgets, die schreibgeschützte Metriken bereitstellen, um wichtige Informationen zu Ihren Kontoprofilen zu vermitteln. Auswählen **[!UICONTROL Dashboard ändern]** , um das Erscheinungsbild der [!UICONTROL Übersicht] durch Verschieben und Ändern der Größe von Widgets.

![Auf der Registerkarte Übersicht über Kontoprofile wurde das Dashboard Ändern hervorgehoben.](../images/account-profiles/modify-dashboard.png)

Weitere Informationen finden Sie im Dokument unter [Ändern von Dashboards](../customize/modify.md) und [Übersicht über die Widget-Bibliothek](../customize/widget-library.md) , um mehr zu erfahren.

## Standard-Widgets {#standard-widgets}

Adobe bietet Standard-Widgets, mit denen Sie verschiedene Metriken im Zusammenhang mit Ihren Kontoprofilen visualisieren können.

Um mehr über die einzelnen verfügbaren Standard-Widgets zu erfahren, wählen Sie den Namen eines Widgets aus der folgenden Liste aus:

* [Rechnungsabschlüsse nach Wirtschaftszweigen insgesamt](#total-accounts-by-industry)
* [Kontoprofile hinzugefügt](#account-profiles-added)

### Rechnungsabschlüsse nach Wirtschaftszweigen insgesamt {#total-accounts-by-industry}

Dieses Widget zeigt die Gesamtanzahl der Konten in einer einzelnen Metrik und verwendet ein Ringdiagramm, um die proportionalen Zählergrößen für die Branchen zu veranschaulichen, aus denen die Gesamtanzahl besteht. Der Schlüssel bietet Informationen zur Farbcodierung für die verschiedenen Branchen, aus denen das Ringdiagramm besteht.

Einzelne Zahlen für die verschiedenen Branchen werden in einem Dialogfeld angezeigt, wenn der Cursor über den entsprechenden Abschnitt des Ringdiagramms bewegt wird.

![Die Gesamtkonten nach Branchen-Widget.](../images/account-profiles/total-accounts-by-industry-widget.png)

### Kontoprofile hinzugefügt {#account-profiles-added}

Dieses Widget verwendet ein farbkodiertes Balkendiagramm, um die Anzahl der Profile, die einem Konto über einen bestimmten Zeitraum hinzugefügt wurden, und den Anteil der verschiedenen Branchen, aus denen diese hinzugefügten Profile bestehen, zu veranschaulichen. Die Branchen sind farbcodiert, und ein Schlüssel liefert Informationen zur Farbcodierung für die verschiedenen Branchen, aus denen das Balkendiagramm besteht. Der Analysezeitraum wird aus dem Widget-Dropdown-Menü ausgewählt. Das Balkendiagramm kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden.

>[!NOTE]
>
>Da Profile nur zu einem Konto hinzugefügt und nie entfernt werden, ist die niedrigstmögliche Anzahl von Profilen, die über einen Zeitraum hinzugefügt werden, null.

![Das Widget Kontoprofile hinzugefügt.](../images/account-profiles/accounts-profiles-added-widget.png)

## Nächste Schritte

Durch Befolgen dieses Dokuments sollten Sie jetzt in der Lage sein, die [!UICONTROL Kontoprofile] Dashboard. Sie sollten auch die Metriken verstehen, die in den verfügbaren Widgets angezeigt werden. Weiterführende Informationen zum Arbeiten mit Kontoprofilen als Teil Ihrer B2B-Daten in der Experience Platform-Benutzeroberfläche finden Sie im Abschnitt [Übersicht über Kontoprofile](../../rtcdp/accounts/account-profile-overview.md) für Adobe Real-Time CDP, B2B Edition.
