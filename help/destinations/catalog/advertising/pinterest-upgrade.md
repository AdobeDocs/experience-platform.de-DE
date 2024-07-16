---
title: Migration der pinterest-Ziele auf die neue API. Kundenaktion erforderlich.
description: Pinterest stellt die v4-Advertiser-API ein, die derzeit vom Pinterest-Ziel in Real-Time CDP verwendet wird. Machen Sie sich mit Ihren Aktionselementen vertraut, um ohne Unterbrechung Ihrer Pinterest-Kampagnen nahtlos zur neuen API zu wechseln.
hide: true
hidefromtoc: true
exl-id: c965235c-4208-4c28-9ac5-eb4c0061515d
source-git-commit: e3341ec6f62844858ecda7dd4db70d085f0bf217
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Pinterest-Ziel-Upgrade auf neue API. Kundenaktion erforderlich bis zum 18. Januar 2024.

>[!IMPORTANT]
>
>Die Kundenaktionselemente auf dieser Seite gelten für Sie, wenn Ihr Unternehmen Datenflüsse eingerichtet hat, um Daten vor dem 16. November 2023 nach Pinterest zu exportieren. Dies ist das Datum, an dem das neue **[!UICONTROL Pinterest]** -Ziel mithilfe der neuesten Pinterest-API zum Zielkatalog hinzugefügt wurde.

## Was geschieht?

Pinterest hat die v4-Advertiser-API, die vom [Pinterest-Ziel](/help/destinations/catalog/advertising/pinterest.md) in Real-Time CDP verwendet wurde, eingestellt. Adobe hat das Ziel aktualisiert, um die [v5 Advertiser-API](https://developers.pinterest.com/docs/getting-started/migration/) zu verwenden. Lesen Sie diese Seite, um Ihre Aktionselemente zu verstehen, damit Sie ohne Unterbrechung Ihrer Pinterest-Kampagnen nahtlos zur neuen API wechseln können.

## Warum wird ich benachrichtigt?

Wir haben festgestellt, dass Ihr Unternehmen über aktive Datenflüsse verfügt, um Zielgruppen für Pinterest zu aktivieren.

## Was ist der Plan?

Adobe hat eine neue Pinterest-Zielkarte veröffentlicht, die die Pinterest API v5 nutzt und Ihre vorhandenen Datenflüsse in der neuen Verbindung behält.

## Muss ich irgendetwas tun, um meine aktivierten Zielgruppen funktionsfähig zu halten?

Ja, vor dem 18. Januar 2024 müssen Sie sich mit Ihrem Pinterest-Advertiser-Konto in Real-Time CDP beim neuen Pinterest-Ziel authentifizieren. Weitere Informationen finden Sie unten.

### Erneutes Authentifizieren bei Pinterest {#reauthenticate}

1. Wechseln Sie zu **[!UICONTROL Ziele > Konten]** und verwenden Sie den Filter auf dem Bildschirm, um nur das Pinterest-Ziel zu filtern.
   ![Nur Pinterest-Konten filtern](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. Wählen Sie im Ziel **Pinterest** das Drei-Punkte-Symbol ... und dann **[!UICONTROL Details bearbeiten]** aus.
   ![Klicken Sie auf Details bearbeiten](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. Wählen Sie **[!UICONTROL OAuth erneut anschließen]** und melden Sie sich bei Ihrem Pinterest-Konto an.
   ![Wählen Sie &quot;OAuth erneut verbinden&quot;](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Zum Aktionselement im folgenden Abschnitt wechseln

### Fluss zum neuen Ziel aktivieren {#disable-old-enable-new-flows}

Anschließend müssen Sie die Datenflüsse auf die neue Karte **[!UICONTROL Pinterest]** aktivieren.

1. Navigieren Sie zu **[!UICONTROL Ziele > Durchsuchen]** und verwenden Sie den Filter auf dem Bildschirm, um nur das Ziel **[!UICONTROL Pinterest]** zu filtern.
   ![Filtern von Pinterest-Datenflüssen nur auf der Registerkarte &quot;Durchsuchen&quot;](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Wählen Sie den Hyperlink-Verbindungsnamen (Treuekampagne im obigen Screenshot) zum Ziel **[!UICONTROL Pinterest]** aus und wechseln Sie zwischen dem Umschalter **[!UICONTROL Aktivieren]** und dem Umschalter **auf**.
   ![Ein- und Ausschalten für neue Verbindungen und aus alten Verbindungen](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)

<!--

While no disruption to your campaigns is expected, remember to check in the Pinterest UI that everything works as expected.

-->

## Können Sie einige Zeitpläne auf hoher Ebene freigeben?

Ja, siehe unten:

**Bis zum 16. November 2023**: Das neue Ziel ist fertig und Sie sollten zwei Pinterest-Karten nebeneinander im Katalog sehen, bis Pinterest aufhört, die alte v4-API zu unterstützen. Alle vorhandenen Datenflüsse auf die aktuelle Pinterest-Karte werden in das neue Ziel kopiert.

![Altes und neues Pinterest-Ziel nebeneinander](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

<!--

>[!IMPORTANT]
>
>After November 16th, 2023 the legacy Pinterest destination is marked **[!UICONTROL Deprecating]**. <span class="preview">Any changes that you make to dataflows to the (Deprecating) Pinterest destination after November 16th will *not* be automatically carried over to the new Pinterest destination. </span>
>For example, we *do not recommend* that you activate new audiences to the old destination after November 16th. If you do that, you will then have to follow the [regular activation steps](/help/destinations/ui/activate-segment-streaming-destinations.md) to add the audience to the new destination once the customer actions are taken.

-->

**Bis zum 15. Dezember 2023**: <span class="preview">Kundenaktion 1</span>. Sie müssen sich erneut bei Pinterest authentifizieren, damit die neue Karte mit Pinterest verbunden ist. Zeigen Sie vollständige Anweisungen in [diesem Abschnitt](#reauthenticate) an.

<span class="preview">Kundenaktion 2</span>. Anschließend müssen Sie die Datenflüsse in der neuen Karte aktivieren. Zeigen Sie vollständige Anweisungen in [diesem Abschnitt](#disable-old-enable-new-flows) an.

<!--

>[!IMPORTANT]
>
>After December 15th, 2023, Adobe does not guarantee the integrity of dataflows to the old **[!UICONTROL (Deprecating) Pinterest]** destination.

-->

**Nach dem 18. Januar 2024**: <span class="preview">Pinterest hat den Zugriff auf die V4-Advertiser-API deaktiviert. Kunden von Real-Time CDP, die noch kein Upgrade auf das neue Ziel durchgeführt haben, werden nun feststellen, dass ihre Datenflüsse zum Pinterest-Ziel fehlschlagen. [Authentifizieren Sie sich erneut bei Pinterest](#reauthenticate) und [aktivieren Sie die Datenflüsse](#disable-old-enable-new-flows) für das aktualisierte Ziel, um Ihre Kampagnen in Pinterest wiederaufzunehmen.</span>

<!--

## Other items to note

After you enable the dataflows on the new destination card and disable the dataflows on the old destination cards, you should see no disruption in your campaigns or in the numbers of qualified profiles in the audiences coming in from Adobe Real-Time CDP.

-->
