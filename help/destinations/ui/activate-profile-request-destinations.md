---
keywords: Aktivieren von Profilanforderungszielen; Aktivieren von Daten; Profilanforderungsziele
title: Aktivieren von Zielgruppendaten für Profilanforderungsziele
type: Tutorial
seo-title: Activate audience data to profile request destinations
description: Erfahren Sie, wie Sie die Zielgruppendaten aktivieren, die Sie in Adobe Experience Platform haben, indem Sie Segmente Profilanfragezielen zuordnen.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to profile request destinations.
source-git-commit: caccd096c9165139d9b966bbfcb311456276192a
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 10%

---

# Aktivieren von Zielgruppendaten für Profilanforderungsziele (Beta)

## Übersicht {#overview}

>[!IMPORTANT]
>
>Profilanforderungsziele in Adobe Experience Platform sind derzeit als Betaversion verfügbar. Dokumentation und Funktionalität können sich ändern.

In diesem Artikel wird der Workflow erläutert, der zum Aktivieren von Zielgruppendaten in Adobe Experience Platform-Profilanforderungszielen erforderlich ist. Beispiele für Profilanforderungsziele sind die Verbindungen [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) und [Benutzerdefinierte Personalisierung](../../destinations/catalog/personalization/custom-personalization.md).

## Voraussetzungen {#prerequisites}

Um Daten für Ziele aktivieren zu können, müssen Sie über eine erfolgreiche [Verbindung zu einem Ziel](./connect-destination.md) verfügen. Wenn Sie dies noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

### Segmentzusammenführungsrichtlinie {#merge-policy}

Profilanforderungsziele unterstützen derzeit nur die Aktivierung von Segmenten, die die standardmäßige Zusammenführungsrichtlinie verwenden. Der Versuch, Segmente mit einer anderen Zusammenführungsrichtlinie zu aktivieren, führt zu einem Fehler auf der Seite [[!UICONTROL Überprüfen]](#review).

## Ziel auswählen {#select-destination}

1. Gehen Sie zu **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]** aus.

   ![Registerkarte &quot;Zielkatalog&quot;](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Wählen Sie **[!UICONTROL Segmente aktivieren]** auf der Karte aus, die dem Ziel entspricht, an dem Sie Ihre Segmente aktivieren möchten, wie in der Abbildung unten dargestellt.

   ![Schaltflächen aktivieren](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. Wählen Sie die Zielverbindung aus, die Sie zum Aktivieren Ihrer Segmente verwenden möchten, und wählen Sie dann **[!UICONTROL Weiter]** aus.

   ![Ziel auswählen](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. Navigieren Sie zum nächsten Abschnitt [wählen Sie Ihre Segmente](#select-segments) aus.

## Segmente auswählen {#select-segments}

Verwenden Sie die Kontrollkästchen links neben den Segmentnamen, um die Segmente auszuwählen, die Sie für das Ziel aktivieren möchten, und wählen Sie dann **[!UICONTROL Weiter]** aus.

![Segmente auswählen](../assets/ui/activate-profile-request-destinations/select-segments.png)

## Segmentexport planen {#scheduling}

Standardmäßig zeigt die Seite [!UICONTROL Segmentzeitplan] nur die neu ausgewählten Segmente an, die Sie im aktuellen Aktivierungsfluss ausgewählt haben.

![Neue Segmente](../assets/ui/activate-profile-request-destinations/new-segments.png)

Um alle für Ihr Ziel aktivierten Segmente anzuzeigen, verwenden Sie die Filteroption und deaktivieren Sie den Filter **[!UICONTROL Nur neue Segmente anzeigen]** .

![Alle Segmente](../assets/ui/activate-profile-request-destinations/all-segments.png)

Wählen Sie auf der Seite **[!UICONTROL Segment schedule]** jedes Segment aus und konfigurieren Sie dann mithilfe der Selektoren **[!UICONTROL Startdatum]** und **[!UICONTROL Enddatum]** das Zeitintervall für das Senden von Daten an Ihr Ziel.

![Segmentplan](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

Wählen Sie **[!UICONTROL Next]** aus, um zur Seite [!UICONTROL Review] zu wechseln.

## Überprüfung {#review}

Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

>[!IMPORTANT]
>
>In diesem Schritt prüft Adobe Experience Platform, ob Verstöße gegen Datennutzungsrichtlinien vorliegen. Im Folgenden finden Sie ein Beispiel, bei dem eine Richtlinie verletzt wird. Sie können den Workflow zur Segmentaktivierung erst abschließen, nachdem Sie den Verstoß behoben haben. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Richtliniendurchsetzung](../../rtcdp/privacy/data-governance-overview.md#enforcement) im Abschnitt zur Data Governance-Dokumentation.

![Verletzung von Datenrichtlinien](../assets/common/data-policy-violation.png)

Wenn keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Beenden]** aus, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

![Überprüfung](../assets/ui/activate-profile-request-destinations/review.png)

## Segmentaktivierung überprüfen {#verify}

Detaillierte Informationen zur Überwachung des Datenflusses zu Ihren Zielen finden Sie in der [Dokumentation zur Zielüberwachung](../../dataflows/ui/monitor-destinations.md) .