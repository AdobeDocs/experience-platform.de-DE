---
keywords: Experience Platform; Startseite; beliebte Themen; Warnhinweise; Ziele
description: Sie können Warnhinweise abonnieren, wenn Sie einen Datenfluss erstellen, um Warnhinweise zum Status, Erfolg oder Misserfolg Ihres Datenflusses zu erhalten.
title: Abonnieren von kontextbezogenen Zielwarnhinweisen
exl-id: 134144a0-cdfe-49a8-bd8b-e36a4f053de5
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 17%

---

# Abonnieren von kontextbezogenen Zielwarnhinweisen

Mit Adobe Experience Platform können Sie ereignisbasierte Warnhinweise zu Adobe Experience Platform-Aktivitäten abonnieren. Warnhinweise verringern oder beseitigen die Notwendigkeit, die [[!DNL Observability Insights] API](../../observability/api/overview.md) abzufragen, um zu überprüfen, ob ein Auftrag abgeschlossen wurde, ob ein bestimmter Meilenstein innerhalb eines Arbeitsablaufs erreicht wurde oder ob Fehler aufgetreten sind.

Sie können Warnhinweise abonnieren, wenn Sie einen Datenfluss erstellen, um Warnhinweise zum Status, Erfolg oder Misserfolg Ihres Datenflusses zu erhalten.

In diesem Dokument erfahren Sie, wie Sie Warnhinweise für Ihren Ziel-Datenfluss abonnieren.

## Erste Schritte

Dieses Dokument setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Ziele](../home.md): Vordefinierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.
* [Observability](../../observability/home.md): [!DNL Observability Insights] ermöglicht es Ihnen, Platform-Aktivitäten mithilfe statistischer Metriken und Ereignisbenachrichtigungen zu überwachen.
   * [Warnhinweise](../../observability/alerts/overview.md): Wenn bestimmte Bedingungen in Ihren Platform-Vorgängen erreicht sind (z. B. ein potenzielles Problem, wenn das System einen Schwellenwert überschreitet), kann Platform Warnhinweise an alle Benutzer in Ihrer Organisation senden, die sich für diese Bedingungen angemeldet haben.

## Abonnieren von Warnhinweisen in der Benutzeroberfläche {#subscribe-destination-alerts}

>[!CONTEXTUALHELP]
>id="platform_destination_alerts_subscribe"
>title="Abonnieren von Warnhinweisen für Ziele"
>abstract="Mit Warnhinweisen erhalten Sie Benachrichtigungen zum Status Ihrer Ziel-Datenflüsse. Sie können die Warnhinweise so einrichten, dass Sie Aktualisierungen erhalten, wenn Ihr Datenfluss gestartet wurde, erfolgreich war, fehlgeschlagen ist oder keine Daten an Ihr Ziel gesendet hat."
>text="Learn more in documentation"

>[!IMPORTANT]
>
>Sie müssen sofortige Benachrichtigungen von E-Mails für Ihr Platform-Konto aktivieren, um E-Mail-basierte Warnhinweise für Ihre Datenflüsse zu erhalten.

Sie können Warnhinweise für Ihre Datenflüsse während des Schritts [!UICONTROL Neues Ziel konfigurieren] des Workflows [Zielverbindung](connect-destination.md) aktivieren.

![UI-Bild, das den Abschnitt mit den Zielwarnungen anzeigt.](../assets/ui/alerts/destination-alerts.png)

Wählen Sie die Warnhinweise aus, die Sie abonnieren möchten, und klicken Sie dann auf **[!UICONTROL Weiter]** , um Ihren Datenfluss zu überprüfen und abzuschließen.

Die für Ziel-Datenflüsse verfügbaren Warnhinweise sind in der folgenden Tabelle beschrieben.

* Für Streaming-Ziele ist nur der Warnhinweis [!DNL Activation Skipped Rate Exceeded] verfügbar.
* Bei dateibasierten Zielen sind alle Warnhinweise verfügbar.

| Warnhinweise | Beschreibung |
| --- | --- |
| Verzögerung bei der Ausführung des Zielflusses | Dieser Warnhinweis benachrichtigt Sie, wenn die Aktivierung einer Audience länger als 150 Minuten dauert, bis ein Zielfluss ausgeführt wird. |
| Fehler beim Ausführen des Zielflusses | Dieser Warnhinweis benachrichtigt Sie, wenn beim Aktivieren einer Zielgruppe ein Fehler auftritt. |
| Erfolgreiche Ausführung des Zielflusses | Dieser Warnhinweis benachrichtigt Sie, wenn eine Zielgruppe erfolgreich für ein Ziel aktiviert wurde. |
| Start der Ausführung des Zielflusses | Dieser Warnhinweis benachrichtigt Sie, wenn ein Zielflussablauf mit der Aktivierung einer Zielgruppe beginnt. |
| Aktivierungsübersprungene Rate überschritten | Dieser Warnhinweis benachrichtigt Sie, wenn die Übersprungrate der Aktivierung 1 % der gesamten Aktivierungen überschritten hat. Identitäten werden während der Aktivierung übersprungen, wenn sie fehlende Attribute oder Zustimmungsverletzungen aufweisen. |

## Warnungen erhalten {#receiving-alerts}

Sobald Ihr Ziel-Datenfluss ausgeführt wird, können Sie Warnhinweise über die Benutzeroberfläche oder per E-Mail erhalten.

### Warnungen in der Benutzeroberfläche empfangen {#receiving-alerts-in-ui}

Warnhinweise werden in der Benutzeroberfläche durch ein Benachrichtigungssymbol in der oberen Kopfzeile der Platform-Benutzeroberfläche dargestellt. Wählen Sie das Benachrichtigungssymbol aus, um Warnhinweise zu Ihren Datenflüssen anzuzeigen.

![UI-Bild mit dem Benachrichtigungssymbol in Experience Platform](../assets/ui/alerts/notification.png)

Das Fenster &quot;Benachrichtigungen&quot;wird mit einer Liste von Statusaktualisierungen für den von Ihnen erstellten Datenfluss angezeigt.

![UI-Bild mit dem Benachrichtigungsbereich](../assets/ui/alerts/alert-window.png)

Sie können den Mauszeiger auf eine Warnmeldung bewegen, um sie als gelesen zu kennzeichnen, oder Sie können das Uhrensymbol auswählen, um zukünftige Erinnerungen zum Status Ihres Datenflusses festzulegen.

![UI-Bild, das die Benachrichtigungserinnerungsoptionen anzeigt](../assets/ui/alerts/remind-me.png)

Wählen Sie die Warnmeldung aus, um spezifische Informationen zu Ihrem Datenfluss anzuzeigen.

![UI-Bild, das zeigt, wie eine Benachrichtigung ausgewählt wird](../assets/ui/alerts/select-alert-message.png)

Die Seite [!UICONTROL Datenfluss-Ausführungsdetails] wird angezeigt. In der oberen Hälfte des Bildschirms wird ein Überblick über Ihren Datenfluss angezeigt, einschließlich Informationen zu seinen Attributen, der zugehörigen Datenfluss-Ausführungskennung und einer allgemeinen Fehlerzusammenfassung.

![UI-Bild, das die Seite mit den Ausführungsdetails des Datenflusses anzeigt.](../assets/ui/alerts/dataflow-overview.png)

In der unteren Hälfte der Seite werden alle [!UICONTROL Datenfluss-Ausführungsfehler] angezeigt, die während der Datenfluss-Ausführungsphase aufgetreten sind. Von hier aus können Sie eine Vorschau der Fehlerdiagnose anzeigen oder die [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) verwenden, um die Fehlerdiagnose oder das Dateimanifest herunterzuladen, das Ihrem Datenfluss entspricht.

![UI-Bild, das die Seite mit Details zur Ausführung des Datenflusses mit einer Hervorhebung im Abschnitt &quot;Fehler&quot;anzeigt.](../assets/ui/alerts/dataflow-run-error.png)

Weitere Informationen zum Umgang mit Datenflussfehlern finden Sie im Handbuch zum [Überwachen von Zieldataflows in der Benutzeroberfläche](../../dataflows/ui/monitor-destinations.md).

### Warnungen per E-Mail erhalten {#receiving-alerts-by-email}

Warnhinweise für Ihre Datenflüsse werden Ihnen auch per E-Mail zugestellt. Wählen Sie den Namen des Datenflusses im E-Mail-Textkörper aus, um weitere Informationen zu Ihrem Datenfluss anzuzeigen.

![Screenshot einer Warnhinweis-E-Mail](../assets/ui/alerts/email.png)

Ähnlich wie beim UI-Warnhinweis wird die Seite [!UICONTROL Übersicht über den Datenfluss] angezeigt, auf der Sie eine Oberfläche zur Untersuchung aller Fehler erhalten, die mit Ihrem Datenfluss verbunden sind.

![dataflow-overview](../assets/ui/alerts/dataflow-overview.png)

## Warnungen abonnieren und abmelden {#subscribe-and-unsubscribe}

Sie können weitere Warnhinweise abonnieren oder sich von etablierten Warnhinweisen für einen vorhandenen Ziel-Datenfluss auf der Seite Ziele [!UICONTROL Durchsuchen] abmelden.

![UI-Bild, das die Seite &quot;Ziele durchsuchen&quot;anzeigt](../assets/ui/alerts/destination-list.png)

Suchen Sie die Zielverbindung, für die Sie Warnhinweise erhalten möchten, und wählen Sie die Auslassungspunkte (`...`) aus, um ein Dropdown-Menü mit Optionen anzuzeigen. Wählen Sie als Nächstes **[!UICONTROL Warnhinweise abonnieren]** aus, um die Warnhinweiseinstellungen Ihres Ziel-Datenflusses zu ändern.

![UI-Bild mit den Zieloptionen](../assets/ui/alerts/destination-alerts-subscribe.png)

Es wird ein Popup-Fenster mit einer Liste von Zielwarnungen angezeigt. Wählen Sie alle Warnhinweise aus, die Sie abonnieren möchten, oder heben Sie die Auswahl für Warnhinweise auf, von denen Sie sich abmelden möchten. Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![UI-Bild, das die Seite mit den Zielwarnhinweisen zu Abonnements anzeigt](../assets/ui/alerts/destination-alerts-list.png)

## Nächste Schritte {#next-steps}

Dieses Dokument enthält eine schrittweise Anleitung zum Abonnieren von kontextbezogenen Warnhinweisen für Ihre Ziel-Datenflüsse. Weitere Informationen finden Sie im Leitfaden zur Benutzeroberfläche von [Warnhinweisen](../../observability/alerts/ui.md).
