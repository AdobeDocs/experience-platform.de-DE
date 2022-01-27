---
keywords: Aktivieren von Profilanforderungszielen; Aktivieren von Daten; Profilanforderungsziele
title: Aktivieren von Zielgruppendaten für Profilanforderungsziele (Beta)
type: Tutorial
seo-title: Activate audience data to profile request destinations
description: Erfahren Sie, wie Sie die Zielgruppendaten aktivieren, die Sie in Adobe Experience Platform haben, indem Sie Segmente Profilanfragezielen zuordnen.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to profile request destinations.
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: dd9493077706b102467493e90b363ac202550eee
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 9%

---

# Aktivieren von Zielgruppendaten für Profilanforderungsziele

## Übersicht {#overview}

In diesem Artikel wird der Workflow erläutert, der zum Aktivieren von Zielgruppendaten in Adobe Experience Platform-Profilanforderungszielen erforderlich ist. Beispiele für Profilanforderungsziele sind die [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) und [Benutzerdefinierte Personalisierung](../../destinations/catalog/personalization/custom-personalization.md) Verbindungen.

## Voraussetzungen {#prerequisites}

Um Daten für Ziele aktivieren zu können, müssen Sie erfolgreich [mit Ziel verbunden](./connect-destination.md). Wenn Sie das noch nicht getan haben, gehen Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

### Segmentzusammenführungsrichtlinie {#merge-policy}

Derzeit unterstützen Profilanforderungsziele nur die Aktivierung von Segmenten, die die [standardmäßige Zusammenführungsrichtlinie](../../segmentation/ui/segment-builder.md#merge-policies).

## Ziel auswählen {#select-destination}

1. Navigieren Sie zu **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die **[!UICONTROL Katalog]** Registerkarte.

   ![Registerkarte &quot;Zielkatalog&quot;](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Auswählen **[!UICONTROL Segmente aktivieren]** auf der Karte, die dem Ziel entspricht, an dem Sie Ihre Segmente aktivieren möchten, wie in der Abbildung unten dargestellt.

   ![Schaltflächen aktivieren](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. Wählen Sie die Zielverbindung aus, die Sie zum Aktivieren Ihrer Segmente verwenden möchten, und wählen Sie dann **[!UICONTROL Nächste]**.

   ![Ziel auswählen](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. Zum nächsten Abschnitt wechseln, um [Segmente auswählen](#select-segments).

## Segmente auswählen {#select-segments}

Aktivieren Sie die Kontrollkästchen links neben den Segmentnamen, um die Segmente auszuwählen, die Sie für das Ziel aktivieren möchten, und wählen Sie dann **[!UICONTROL Nächste]**.

![Segmente auswählen](../assets/ui/activate-profile-request-destinations/select-segments.png)

## Segmentexport planen {#scheduling}

Standardmäßig wird die [!UICONTROL Segmentplan] zeigt nur die neu ausgewählten Segmente an, die Sie im aktuellen Aktivierungsfluss ausgewählt haben.

![Neue Segmente](../assets/ui/activate-profile-request-destinations/new-segments.png)

Um alle für Ihr Ziel aktivierten Segmente anzuzeigen, verwenden Sie die Filteroption und deaktivieren Sie die **[!UICONTROL Nur neue Segmente anzeigen]** Filter.

![Alle Segmente](../assets/ui/activate-profile-request-destinations/all-segments.png)

Im **[!UICONTROL Segmentplan]** Seite, wählen Sie jedes Segment aus und verwenden Sie dann die **[!UICONTROL Startdatum]** und **[!UICONTROL Enddatum]** Selektoren zum Konfigurieren des Zeitintervalls für das Senden von Daten an Ihr Ziel.

![Segmentplan](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

Auswählen **[!UICONTROL Nächste]** , um [!UICONTROL Überprüfen] Seite.

## Überprüfung {#review}

Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

>[!IMPORTANT]
>
>In diesem Schritt prüft Adobe Experience Platform, ob Verstöße gegen Datennutzungsrichtlinien vorliegen. Im Folgenden finden Sie ein Beispiel, bei dem eine Richtlinie verletzt wird. Sie können den Workflow zur Segmentaktivierung erst abschließen, nachdem Sie den Verstoß behoben haben. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Durchsetzung von Richtlinien](../../rtcdp/privacy/data-governance-overview.md#enforcement) im Abschnitt Data Governance-Dokumentation .

![Verletzung von Datenrichtlinien](../assets/common/data-policy-violation.png)

Wenn keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Beenden]** , um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

![Überprüfung](../assets/ui/activate-profile-request-destinations/review.png)

## Segmentaktivierung überprüfen {#verify}

Überprüfen Sie die [Zielüberwachungsdokumentation](../../dataflows/ui/monitor-destinations.md) für detaillierte Informationen zur Überwachung des Datenflusses zu Ihren Zielen.
