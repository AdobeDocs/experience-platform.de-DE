---
keywords: Experience Platform;Startseite;beliebte Themen;Warnhinweise;Ziele
description: Sie können beim Erstellen eines Datenflusses Warnhinweise abonnieren, um Benachrichtigungen zum Status, Erfolg oder Misserfolg Ihres Datenflusses zu erhalten.
title: Abonnieren von kontextbezogenen Zielwarnhinweisen
exl-id: 134144a0-cdfe-49a8-bd8b-e36a4f053de5
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 17%

---

# Abonnieren von kontextbezogenen Zielwarnhinweisen

Mit Adobe Experience Platform können Sie ereignisbasierte Warnhinweise zu Adobe Experience Platform-Aktivitäten abonnieren. Warnhinweise verringern oder beseitigen die Notwendigkeit, die [[!DNL Observability Insights] API](../../observability/api/overview.md) abzufragen, um zu überprüfen, ob ein Auftrag abgeschlossen wurde, ob ein bestimmter Meilenstein innerhalb eines Arbeitsablaufs erreicht wurde oder ob Fehler aufgetreten sind.

Sie können beim Erstellen eines Datenflusses Warnhinweise abonnieren, um Benachrichtigungen zum Status, Erfolg oder Misserfolg Ihres Datenflusses zu erhalten.

In diesem Dokument wird beschrieben, wie Sie Warnhinweise für Ihre Ziel-Datenflüsse abonnieren und empfangen können.

## Erste Schritte

Dieses Dokument setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Ziele](../home.md): Vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.
* [Observability](../../observability/home.md): [!DNL Observability Insights] ermöglicht Ihnen die Überwachung von Platform-Aktivitäten mithilfe von statistischen Metriken und Ereignisbenachrichtigungen.
   * [Warnhinweise](../../observability/alerts/overview.md): Wenn bestimmte Bedingungen in Ihren Platform-Vorgängen erfüllt sind (z. B. ein potenzielles Problem, wenn das System einen Schwellenwert überschreitet), kann Platform allen Benutzern in Ihrer Organisation, die sich dafür angemeldet haben, Warnhinweise senden.

## Abonnieren von Warnhinweisen in der Benutzeroberfläche {#subscribe-destination-alerts}

>[!CONTEXTUALHELP]
>id="platform_destination_alerts_subscribe"
>title="Abonnieren von Warnhinweisen für Ziele"
>abstract="Mit Warnhinweisen erhalten Sie Benachrichtigungen zum Status Ihrer Ziel-Datenflüsse. Sie können die Warnhinweise so einrichten, dass Sie Aktualisierungen erhalten, wenn Ihr Datenfluss gestartet wurde, erfolgreich war, fehlgeschlagen ist oder keine Daten an Ihr Ziel gesendet hat."
>text="Learn more in documentation"

>[!IMPORTANT]
>
>Sie müssen sofortige E-Mail-Benachrichtigungen für Ihr Platform-Konto aktivieren, um E-Mail-basierte Warnhinweise für Ihre Datenflüsse zu erhalten.

Sie können Warnhinweise für Ihre Datenflüsse während des [!UICONTROL Neues Ziel konfigurieren] des Workflows [Zielverbindung](connect-destination.md) aktivieren.

![UI-Bild, das den Abschnitt „Ziel-Warnhinweise“ anzeigt.](../assets/ui/alerts/destination-alerts.png)

Wählen Sie die Warnhinweise aus, die Sie abonnieren möchten, und wählen Sie dann **[!UICONTROL Weiter]**, um Ihren Datenfluss zu überprüfen und abzuschließen.

Die für Ziel-Datenflüsse verfügbaren Warnhinweise werden in der folgenden Tabelle beschrieben.

* Für Streaming-Ziele ist nur der [!DNL Activation Skipped Rate Exceeded] Warnhinweis verfügbar.
* Für dateibasierte Ziele sind alle Warnhinweise verfügbar.

| Warnhinweise | Beschreibung |
| --- | --- |
| Verzögerung bei der Ausführung des Zielflusses | Dieser Warnhinweis benachrichtigt Sie, wenn die Aktivierung einer Zielgruppe für die Ausführung eines Zielflusses länger als 150 Minuten dauert. |
| Fehler beim Ausführen des Zielflusses | Dieser Warnhinweis benachrichtigt Sie, wenn beim Aktivieren einer Zielgruppe für ein Ziel ein Fehler auftritt. |
| Erfolgreiche Ausführung des Zielflusses | Dieser Warnhinweis benachrichtigt Sie, wenn eine Zielgruppe erfolgreich für ein Ziel aktiviert wurde. |
| Start der Ausführung des Zielflusses | Dieser Warnhinweis informiert Sie, wenn ein Zielfluss mit der Aktivierung einer Zielgruppe beginnt. |
| Aktivierung der Überspringungsrate überschritten | Dieser Warnhinweis informiert Sie, wenn die Aktivierungsüberspringungsrate 1 % der gesamten Aktivierungen überschritten hat. Identitäten werden während der Aktivierung übersprungen, wenn sie fehlende Attribute oder eine Einverständnisverletzung aufweisen. |

## Warnungen erhalten {#receiving-alerts}

Sobald Ihr Ziel-Datenfluss ausgeführt wird, können Sie Warnhinweise über die Benutzeroberfläche oder per E-Mail erhalten.

### Empfangen von Warnhinweisen über die Benutzeroberfläche {#receiving-alerts-in-ui}

Warnhinweise werden in der Benutzeroberfläche durch ein Benachrichtigungssymbol in der oberen Kopfzeile der Platform-Benutzeroberfläche dargestellt. Wählen Sie das Benachrichtigungssymbol aus, um spezifische Warnmeldungen zu Ihren Datenflüssen anzuzeigen.

![UI-Bild, das das Benachrichtigungssymbol auf Experience Platform anzeigt](../assets/ui/alerts/notification.png)

Das Benachrichtigungsfenster wird mit einer Liste von Statusaktualisierungen zu dem von Ihnen erstellten Datenfluss angezeigt.

![UI-Bild mit dem Benachrichtigungsbereich](../assets/ui/alerts/alert-window.png)

Sie können den Mauszeiger über eine Warnmeldung bewegen, um sie als gelesen zu markieren, oder auf das Uhrensymbol klicken, um zukünftige Erinnerungen an den Status Ihres Datenflusses festzulegen.

![UI-Bild mit den Erinnerungsoptionen für Benachrichtigungen](../assets/ui/alerts/remind-me.png)

Wählen Sie die Warnmeldung aus, um spezifische Informationen zu Ihrem Datenfluss anzuzeigen.

![UI-Bild, das zeigt, wie eine Benachrichtigung ausgewählt wird](../assets/ui/alerts/select-alert-message.png)

Die [!UICONTROL Datenflussausführungs-Details] wird angezeigt. In der oberen Hälfte des Bildschirms wird ein Überblick über Ihren Datenfluss angezeigt, einschließlich Informationen zu den Attributen, der entsprechenden Datenflussausführungs-ID und der allgemeinen Fehlerzusammenfassung.

![UI-Bild, das die Seite mit den Datenflussausführungs-Details anzeigt.](../assets/ui/alerts/dataflow-overview.png)

In der unteren Hälfte der Seite werden alle [!UICONTROL Datenflussausführungsfehler) angezeigt] die während der Datenflussausführungsstufe aufgetreten sind. Von hier aus können Sie eine Vorschau der Fehlerdiagnose anzeigen oder die [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) verwenden, um Fehlerdiagnosen oder das Dateimanifest herunterzuladen, das Ihrem Datenfluss entspricht.

![UI-Bild, das die Seite mit den Datenflussausführungs-Details zeigt, mit einer Hervorhebung des Abschnitts „Fehler“.](../assets/ui/alerts/dataflow-run-error.png)

Weitere Informationen zum Umgang mit Datenflussfehlern finden Sie im Handbuch [Überwachen von Zieldatenflüssen in der Benutzeroberfläche](../../dataflows/ui/monitor-destinations.md).

### Benachrichtigungen per E-Mail erhalten {#receiving-alerts-by-email}

Warnhinweise für Ihre Datenflüsse werden Ihnen auch per E-Mail zugestellt. Wählen Sie den Namen des Datenflusses im E-Mail-Textkörper aus, um weitere Informationen zu Ihrem Datenfluss anzuzeigen.

![Screenshot einer Benachrichtigungs-E-Mail](../assets/ui/alerts/email.png)

Ähnlich wie beim Warnhinweis in der Benutzeroberfläche wird die Seite [!UICONTROL Übersicht über die Datenflussausführung] angezeigt, auf der Sie eine Oberfläche zur Untersuchung von Fehlern erhalten, die mit Ihrem Datenfluss verbunden sind.

![Datenfluss-Übersicht](../assets/ui/alerts/dataflow-overview.png)

## Warnungen abonnieren und abmelden {#subscribe-and-unsubscribe}

Sie können weitere Warnhinweise abonnieren oder sich von eingerichteten Warnhinweisen für einen vorhandenen Ziel-Datenfluss auf der Seite Ziele [!UICONTROL Durchsuchen] abmelden.

![UI-Bild, das die Seite zum Durchsuchen von Zielen zeigt](../assets/ui/alerts/destination-list.png)

Suchen Sie die Zielverbindung, für die Sie Warnhinweise erhalten möchten, und wählen Sie die Auslassungszeichen (`...`) aus, um ein Dropdown-Menü mit Optionen anzuzeigen. Wählen Sie als Nächstes **[!UICONTROL Warnhinweise abonnieren]**, um die Warnhinweiseinstellungen Ihres Ziel-Datenflusses zu ändern.

![UI-Bild, das die Zieloptionen zeigt](../assets/ui/alerts/destination-alerts-subscribe.png)

Ein Popup-Fenster wird angezeigt, das eine Liste der Ziel-Warnhinweise enthält. Wählen Sie alle Warnhinweise aus, die Sie abonnieren möchten, oder heben Sie die Auswahl der Warnhinweise auf, die Sie kündigen möchten. Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![UI-Bild, das die Ziel-Warnhinweis-Abonnementseite anzeigt](../assets/ui/alerts/destination-alerts-list.png)

## Nächste Schritte {#next-steps}

Dieses Dokument enthält eine schrittweise Anleitung zum Abonnieren von kontextbezogenen Warnhinweisen für Ihre Ziel-Datenflüsse. Weitere Informationen finden Sie im [Handbuch zur Warnhinweis-Benutzeroberfläche](../../observability/alerts/ui.md).
