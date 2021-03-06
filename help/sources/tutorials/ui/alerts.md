---
keywords: Experience Platform; Homepage; beliebte Themen Warnungen
description: Sie können Warnhinweise abonnieren, wenn Sie einen Datenfluss erstellen, um Warnhinweise zum Status, Erfolg oder Misserfolg Ihres Datenflusses zu erhalten.
title: In-Context-Warnhinweise in der Benutzeroberfläche abonnieren
exl-id: 5d51edaa-ecba-4ac0-8d3c-49010466b9a5
source-git-commit: 2acb58d21952699c60471cb4f4347af89621f045
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 10%

---

# Warnhinweise für Datenflüsse zu Quellen in der Benutzeroberfläche abonnieren

Mit Adobe Experience Platform können Sie ereignisbasierte Warnhinweise zu Adobe Experience Platform-Aktivitäten abonnieren. Warnhinweise verringern oder beseitigen die Notwendigkeit, die [[!DNL Observability Insights] API](../../../observability/api/overview.md) abzufragen, um zu überprüfen, ob ein Auftrag abgeschlossen wurde, ob ein bestimmter Meilenstein innerhalb eines Arbeitsablaufs erreicht wurde oder ob Fehler aufgetreten sind.

Sie können Warnhinweise abonnieren, wenn Sie einen Datenfluss erstellen, um Warnhinweise zum Status, Erfolg oder Misserfolg Ihres Datenflusses zu erhalten.

In diesem Dokument erfahren Sie, wie Sie Warnhinweise für Ihren Datenfluss zu Quellen abonnieren.

## Erste Schritte

Dieses Dokument setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu beschriften und zu erweitern, indem Sie [!DNL Platform] Dienste.
* [Mit Observability können Sie Platform-Aktivitäten mithilfe von statistischen Metriken und Ereignisbenachrichtigungen überwachen.](../../../observability/home.md)[!DNL Observability Insights]
   * [Warnhinweise](../../../observability/alerts/overview.md): Wenn bestimmte Bedingungen in Ihren Platform-Vorgängen erreicht sind (z. B. ein potenzielles Problem, wenn das System einen Schwellenwert überschreitet), kann Platform allen Benutzern in Ihrer Organisation, die sich für diese Bedingungen angemeldet haben, Warnhinweise bereitstellen.

## Warnhinweise über die Benutzeroberfläche abonnieren {#subscribe-sources-alerts}

>[!CONTEXTUALHELP]
>id="platform_sources_alerts_subscribe"
>title="Warnhinweise für Quellen abonnieren"
>abstract="Warnhinweise ermöglichen den Empfang von Benachrichtigungen basierend auf dem Status Ihrer Datenflüsse aus Quellen. Sie können Warnhinweise so einrichten, dass Aktualisierungen abgerufen werden, wenn Ihr Datenfluss gestartet wurde, erfolgreich war, fehlgeschlagen ist oder keine Daten erfasst hat."
>text="Learn more in documentation"

>[!IMPORTANT]
>
>Sie müssen sofortige Benachrichtigungen von E-Mails für Ihr Platform-Konto aktivieren, um E-Mail-basierte Warnhinweise für Ihre Datenflüsse zu erhalten.

Sie können Warnhinweise für Ihre Datenflüsse während der [!UICONTROL Datenflussdetails] Schritt des Ursprungs-Workflows im Arbeitsbereich &quot;Quellen&quot;.

![dataflow-detail](../../images/tutorials/alerts/dataflow-detail.png)

Die verfügbaren Warnhinweise für Datenflüsse zu Quellen sind:

| Warnhinweise | Beschreibung |
| --- | --- |
| Start des Datenflusses für Quellen | Dieser Warnhinweis sendet Ihnen eine Nachricht, wenn Ihr Quelldatensatz gestartet wurde. |
| Quellen-Datenfluss erfolgreich ausgeführt | Dieser Warnhinweis sendet Ihnen eine Nachricht, wenn Daten aus Ihrer Quelle erfolgreich in Platform erfasst wurden. |
| Fehler beim Ausführen des Datenflusses für Quellen | Dieser Warnhinweis sendet Ihnen eine Nachricht, wenn in Ihrem Datenfluss ein Fehler auftritt. |
| Datenfluss-unzureichende Aufnahme von Quellen | Dieser Warnhinweis sendet Ihnen eine Nachricht, wenn die Aufnahme um mehr als sieben Stunden verzögert ist und keine Daten an Platform erfasst werden. |

Wählen Sie die Warnhinweise aus, die Sie abonnieren möchten, und wählen Sie dann **[!UICONTROL Nächste]** , um Ihren Datenfluss zu überprüfen und abzuschließen.

![select-alerts](../../images/tutorials/alerts/select-alerts.png)

Detaillierte Schritte zum Erstellen eines Datenflusses für Quellen in der Benutzeroberfläche finden Sie in den folgenden Handbüchern:

* [Adobe Advertising](./dataflow/advertising.md)
* [Cloud-Speicher](./dataflow/batch/cloud-storage.md)
* [CRM](./dataflow/crm.md)
* [Datenbank](./dataflow/databases.md)
* [E-Commerce](./dataflow/ecommerce.md)
* [Lokale Dateien](./create/local-system/local-file-upload.md)
* [Marketing-Automatisierung](./dataflow/marketing-automation.md)
* [Zahlungen](./dataflow/payments.md)
* [Protokolle](./dataflow/protocols.md)

## Warnungen empfangen

Sobald Ihr Datenfluss ausgeführt wird, können Sie Warnhinweise über die Benutzeroberfläche oder per E-Mail erhalten.

### In der Benutzeroberfläche

Warnhinweise werden in der Benutzeroberfläche durch ein Benachrichtigungssymbol in der oberen Kopfzeile der Platform-Benutzeroberfläche dargestellt. Wählen Sie das Benachrichtigungssymbol aus, um Warnhinweise zu Ihren Datenflüssen anzuzeigen.

![Benachrichtigung](../../images/tutorials/alerts/notification.png)

Das Fenster &quot;Benachrichtigungen&quot;wird mit einer Liste von Statusaktualisierungen für den von Ihnen erstellten Datenfluss angezeigt.

![alert-window](../../images/tutorials/alerts/alert-window.png)

Sie können den Mauszeiger auf eine Warnmeldung bewegen, um sie als gelesen zu kennzeichnen, oder Sie können das Uhrensymbol auswählen, um zukünftige Erinnerungen zum Status Ihres Datenflusses festzulegen.

![ERINNERUNGEN](../../images/tutorials/alerts/remind-me.png)

Wählen Sie die Warnmeldung aus, um spezifische Informationen zu Ihrem Datenfluss anzuzeigen.

![select-alert-message](../../images/tutorials/alerts/select-alert-message.png)

Die [!UICONTROL Übersicht über Datenfluss] angezeigt. In der oberen Hälfte des Bildschirms wird ein Überblick über Ihren Datenfluss angezeigt, einschließlich Informationen zu seinen Attributen, der zugehörigen Datenfluss-Ausführungskennung und einer allgemeinen Fehlerzusammenfassung.

![dataflow-overview](../../images/tutorials/alerts/dataflow-overview.png)

In der unteren Hälfte der Seite werden alle [!UICONTROL Fehler bei Datenfluss-Ausführung] , die während der Datenfluss-Ausführungsphase aufgetreten sind. Hier können Sie eine Vorschau der Fehlerdiagnose anzeigen oder die [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) um die Fehlerdiagnose oder das Dateimanifest herunterzuladen, das Ihrem Datenfluss entspricht.

![dataflow-run-errors](../../images/tutorials/alerts/dataflow-run-error.png)

Weitere Informationen zur Verarbeitung von Datenflug-Fehlern finden Sie im Handbuch unter [Überwachen von Datenflüssen aus Quellen in der Benutzeroberfläche](../../../dataflows/ui/monitor-sources.md).

### Nach E-Mail

Warnhinweise für Ihre Datenflüsse werden Ihnen auch per E-Mail zugestellt. Wählen Sie den Namen des Datenflusses im E-Mail-Textkörper aus, um weitere Informationen zu Ihrem Datenfluss anzuzeigen.

![email](../../images/tutorials/alerts/email.png)

Ähnlich wie bei der UI-Warnung wird die [!UICONTROL Übersicht über Datenfluss] angezeigt werden. Sie erhalten eine Oberfläche, über die Sie alle mit Ihrem Datenfluss verbundenen Fehler untersuchen können.

![dataflow-overview](../../images/tutorials/alerts/dataflow-overview.png)

## Warnungen abonnieren und abmelden

Sie können weitere Warnhinweise abonnieren oder sich von etablierten Warnhinweisen für einen vorhandenen Datenfluss im [!UICONTROL Datenflüsse] Seite. Suchen Sie den erstellten Datenfluss aus der Liste und wählen Sie dann die Auslassungspunkte (`...`), um ein Dropdown-Menü mit Optionen anzuzeigen. Wählen Sie als Nächstes **[!UICONTROL Warnhinweise abonnieren]** , um die Warnhinweiseinstellungen Ihres Datenflusses zu ändern.

![options](../../images/tutorials/alerts/options.png)

Es wird ein Popup-Fenster mit einer Liste von Warnungen zu Quellen angezeigt. Wählen Sie alle Warnhinweise aus, die Sie abonnieren möchten, oder heben Sie die Auswahl für Warnhinweise auf, von denen Sie sich abmelden möchten. Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![Speichern](../../images/tutorials/alerts/save.png)

## Nächste Schritte

Dieses Dokument enthält eine schrittweise Anleitung zum Abonnieren von kontextbezogenen Warnhinweisen für Ihre Datenflüsse für Quellen. Weitere Informationen finden Sie unter [Warnhinweis-UI-Handbuch](../../../observability/alerts/ui.md).