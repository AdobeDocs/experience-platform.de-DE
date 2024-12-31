---
title: Pinterest-Zielmigration zur neuen API. Kundenaktion erforderlich.
description: Pinterest stellt die v4-Advertiser-API ein, die derzeit vom Pinterest-Ziel in Real-Time CDP verwendet wird. Verstehen Sie Ihre Aktionselemente, um nahtlos auf die neue API umzusteigen, ohne Ihre Pinterest-Kampagnen zu unterbrechen.
hide: true
hidefromtoc: true
exl-id: c965235c-4208-4c28-9ac5-eb4c0061515d
source-git-commit: e3341ec6f62844858ecda7dd4db70d085f0bf217
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Pinterest-Ziel-Upgrade auf neue API. Bis zum 18. Januar 2024 erforderliche Kundenaktion.

>[!IMPORTANT]
>
>Die Kundenaktionselemente auf dieser Seite gelten für Sie, wenn Ihr Unternehmen vor dem 16. November 2023, dem Datum, an dem das neue **[!UICONTROL Pinterest]**-Ziel mit der neuesten Pinterest-API zum Zielkatalog hinzugefügt wurde, Datenflüsse zum Exportieren von Daten in Pinterest eingerichtet hat.

## Was geschieht?

Pinterest hat die v4-Advertiser-API veraltet, die vom [Pinterest-Ziel](/help/destinations/catalog/advertising/pinterest.md) in Real-Time CDP verwendet wurde. Adobe aktualisierte das Ziel für die Verwendung der [v5 Advertiser-API](https://developers.pinterest.com/docs/getting-started/migration/). Lesen Sie diese Seite, um Ihre Aktionselemente zu verstehen, damit Sie nahtlos zur neuen API wechseln können, ohne Ihre Pinterest-Kampagnen zu unterbrechen.

## Warum werde ich benachrichtigt?

Wir haben festgestellt, dass Ihr Unternehmen über aktive Datenflüsse zur Aktivierung von Zielgruppen in Pinterest verfügt.

## Was ist der Plan?

Adobe hat eine neue Pinterest-Zielkarte veröffentlicht, die die Pinterest-API v5 nutzt und Ihre vorhandenen Datenflüsse in der neuen Verbindung beibehält.

## Muss ich etwas tun, damit meine aktivierten Zielgruppen weiterhin funktionieren?

Ja, vor dem 18. Januar 2024 müssen Sie sich mit Ihrem Pinterest Advertiser-Konto in Real-Time CDP beim neuen Pinterest-Ziel authentifizieren. Detaillierte Anweisungen finden Sie unten.

### Erneutes Authentifizieren bei Pinterest {#reauthenticate}

1. Navigieren Sie **[!UICONTROL Ziele > Konten]** und verwenden Sie den Filter auf dem Bildschirm, um nur das Pinterest-Ziel zu filtern.
   ![Nur Pinterest-Konten filtern](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. Wählen Sie am Ziel **Pinterest** das Drei-Punkte-Symbol … und anschließend **[!UICONTROL Details bearbeiten]**.
   ![Details bearbeiten auswählen](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. Wählen Sie **[!UICONTROL OAuth erneut]** und melden Sie sich bei Ihrem Pinterest-Konto an.
   ![Wählen Sie OAuth erneut verbinden aus](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Wechseln Sie zum Aktionselement im folgenden Abschnitt

### Aktivieren von Flüssen zu einem neuen Ziel {#disable-old-enable-new-flows}

Anschließend müssen Sie die Datenflüsse zur neuen **[!UICONTROL Pinterest]**-Karte aktivieren.

1. Navigieren Sie zu **[!UICONTROL Ziele > Durchsuchen]** und verwenden Sie den Filter auf dem Bildschirm, um nur das **[!UICONTROL Pinterest]**-Ziel zu filtern.
   ![Filtern Sie Pinterest-Datenflüsse nur auf der Registerkarte Durchsuchen](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Wählen Sie den Hyperlink-Verbindungsnamen (im obigen Screenshot-Beispiel die Treuekampagne) zum Ziel **[!UICONTROL Pinterest]** aus und schalten Sie den Umschalter **[!UICONTROL Aktivieren]** auf **Ein** um.
   ![Ein-/Ausschalten für neue Verbindungen und Aus für alte Verbindungen](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)

<!--

While no disruption to your campaigns is expected, remember to check in the Pinterest UI that everything works as expected.

-->

## Können Sie einige allgemeine Timelines freigeben?

Ja, siehe unten:

**Bis zum 16. November 2023**: Das neue Ziel ist bereit, und Sie sollten im Katalog zwei Pinterest-Karten nebeneinander sehen, bis Pinterest die alte v4-API nicht mehr unterstützt. Alle Ihre vorhandenen Datenflüsse zur aktuellen Pinterest-Karte werden in das neue Ziel kopiert.

![Altes und neues Pinterest-Ziel nebeneinander](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

<!--

>[!IMPORTANT]
>
>After November 16th, 2023 the legacy Pinterest destination is marked **[!UICONTROL Deprecating]**. <span class="preview">Any changes that you make to dataflows to the (Deprecating) Pinterest destination after November 16th will *not* be automatically carried over to the new Pinterest destination. </span>
>For example, we *do not recommend* that you activate new audiences to the old destination after November 16th. If you do that, you will then have to follow the [regular activation steps](/help/destinations/ui/activate-segment-streaming-destinations.md) to add the audience to the new destination once the customer actions are taken.

-->

**Bis zum 15. Dezember 2023**: <span class="preview">Kundenaktion 1</span>. Sie müssen sich erneut bei Pinterest authentifizieren, damit die neue Karte mit Pinterest verbunden ist. Vollständige Anweisungen finden Sie [ (diesem Abschnitt](#reauthenticate).

<span class="preview">Kundenaktion 2</span>.Dann müssen Sie die Datenflüsse in der neuen Karte aktivieren. Vollständige Anweisungen finden Sie [ (diesem Abschnitt](#disable-old-enable-new-flows).

<!--

>[!IMPORTANT]
>
>After December 15th, 2023, Adobe does not guarantee the integrity of dataflows to the old **[!UICONTROL (Deprecating) Pinterest]** destination.

-->

**Nach dem 18. Januar 2024**: <span class="preview">Pinterest hat den Zugriff auf die V4 Advertiser-API deaktiviert. Real-Time CDP-Kunden, die noch kein Upgrade auf das neue Ziel durchgeführt haben, stellen nun fest, dass ihre Datenflüsse zum Pinterest-Ziel fehlschlagen. [Erneute Authentifizierung bei Pinterest](#reauthenticate) und [Aktivieren der Datenflüsse](#disable-old-enable-new-flows) zum aktualisierten Ziel, um Ihre Kampagnen für Pinterest fortzusetzen.</span>

<!--

## Other items to note

After you enable the dataflows on the new destination card and disable the dataflows on the old destination cards, you should see no disruption in your campaigns or in the numbers of qualified profiles in the audiences coming in from Adobe Real-Time CDP.

-->
