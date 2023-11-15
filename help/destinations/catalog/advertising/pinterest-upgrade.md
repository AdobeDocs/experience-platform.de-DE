---
title: Migration der pinterest-Ziele auf die neue API. Kundenaktion erforderlich.
description: Pinterest stellt die v4-Advertiser-API ein, die derzeit vom Pinterest-Ziel in Real-Time CDP verwendet wird. Machen Sie sich mit Ihren Aktionselementen vertraut, um ohne Unterbrechung Ihrer Pinterest-Kampagnen nahtlos zur neuen API zu wechseln.
hide: true
hidefromtoc: true
source-git-commit: 10bf63677c66366c226d647b1174093c1704a8b9
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 0%

---

# Pinterest-Ziel-Upgrade auf neue API. Vom 15. Dezember 2023 angeforderte Kundenaktion

## Was geschieht?

Pinterest stellt die v4-Advertiser-API ein, die derzeit von der [Pinterest-Ziel](/help/destinations/catalog/advertising/pinterest.md) in Real-Time CDP. Adobe arbeitet mit Pinterest und aktualisiert das Ziel, um die [v5 Advertiser-API](https://developers.pinterest.com/docs/getting-started/migration/). Lesen Sie diese Seite, um Ihre Aktionselemente zu verstehen, damit Sie ohne Unterbrechung Ihrer Pinterest-Kampagnen nahtlos zur neuen API wechseln können.

## Warum wird ich benachrichtigt?

Wir haben festgestellt, dass Ihr Unternehmen über aktive Datenflüsse verfügt, um Zielgruppen für Pinterest zu aktivieren.

## Was ist der Plan?

Adobe veröffentlicht eine neue Pinterest-Zielkarte, die die Pinterest API v5 nutzt und Ihre vorhandenen Datenflüsse in der neuen Verbindung erhält.

## Muss ich irgendetwas tun, um meine aktivierten Zielgruppen funktionsfähig zu halten?

Ja, nach Abschluss des Adobe-Upgrades (Targeting am 16. November) müssen Sie sich mit Ihrem Pinterest-Advertiser-Konto in Adobe Experience Platform erneut bei Pinterest authentifizieren. Weitere Informationen finden Sie unten.

### Erneutes Authentifizieren bei Pinterest {#reauthenticate}

1. Navigieren Sie zu **[!UICONTROL Ziele > Konten]** und verwenden Sie den Filter auf dem Bildschirm, um nur das Pinterest-Ziel zu filtern.
   ![Nur Pinterest-Konten filtern](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. Im **(Neu) Pinterest** Ziel, wählen Sie das Drei-Punkte-Symbol ... und wählen Sie **[!UICONTROL Details bearbeiten]**.
   ![Details bearbeiten](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. Auswählen **[!UICONTROL OAuth erneut anschließen]** und melden Sie sich bei Ihrem Pinterest-Konto an.
   ![Wählen Sie &quot;OAuth erneut verbinden&quot;aus.](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Teilen Sie Adobe mit, dass Sie sich erneut bei der **[!UICONTROL (Neu) Pinterest]** Ziel.

### Vorhandene Flüsse zum alten Ziel deaktivieren und Flüsse zum neuen Ziel aktivieren {#disable-old-enable-new-flows}

Dann müssen Sie vorhandene Flüsse auf die alte Karte manuell deaktivieren und Flüsse auf die neue Karte aktivieren.

>[!IMPORTANT]
>
>Nach der erneuten Authentifizierung können Sie sich an die Adobe wenden und wir führen diesen zweiten Schritt für Sie durch. Wenn Sie diesen Schritt lieber manuell ausführen möchten, führen Sie die folgenden Schritte aus:

1. Navigieren Sie zu **[!UICONTROL Ziele > Durchsuchen]** und den Filter auf dem Bildschirm verwenden, um die **[!UICONTROL (Neu) Pinterest]** und **[!UICONTROL (Veraltet) Pinterest]** nur Ziele.
   ![Filtern von Pinterest-Datenflüssen nur auf der Registerkarte Durchsuchen](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Wählen Sie den Namen der Hyperlink-Verbindung aus (Kampagne &quot;Treueprogramm&quot;im obigen Screenshot) und wechseln Sie zwischen **[!UICONTROL Aktivieren]** Umschalten auf **off** für die alte Verbindung und **on** für die neue Verbindung.
   ![Aktivieren für neue Verbindungen und Deaktivieren für alte Verbindungen](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle.png)
3. Vergleichen Sie die Liste der aktivierten Zielgruppe im alten und neuen Datenfluss und stellen Sie sicher, dass in den alten Flüssen keine neuen Zielgruppen vorhanden sind, die in den neuen Flüssen fehlen.

Beachten Sie, dass keine Unterbrechung Ihrer Kampagnen erwartet wird. Stellen Sie jedoch in der Pinterest-Benutzeroberfläche sicher, dass alles erwartungsgemäß funktioniert.

## Können Sie einige Zeitpläne auf hoher Ebene freigeben?

Ja, siehe unten:

**Bis zum 16. November**: Das neue Ziel ist fertig. Im Katalog sollten Sie zwei Pinterest-Karten nebeneinander sehen, und alle vorhandenen Datenflüsse auf die aktuelle Pinterest-Karte werden in das neue Ziel kopiert.

![Altes und neues Pinterest-Ziel nebeneinander](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

>[!IMPORTANT]
>
>Nach dem 16. November wird das alte Pinterest-Ziel als **[!UICONTROL Veraltet]**. <span class="preview">Änderungen, die Sie nach dem 16. November an den Datenflüssen an dem Pinterest-Ziel (veraltet) vornehmen, werden *not* automatisch an das neue Pinterest-Ziel übertragen werden. </span>
>Beispiel: Wir *nicht empfehlen* dass Sie nach dem 16. November neue Zielgruppen für das alte Ziel aktivieren. Wenn Sie dies tun, müssen Sie dann dem [regelmäßige Aktivierungsschritte](/help/destinations/ui/activate-segment-streaming-destinations.md) , um die Zielgruppe zum neuen Ziel hinzuzufügen, sobald die Kundenaktionen ausgeführt wurden.

**Bis zum 15. Dezember**: <span class="preview">Kundenaktion</span>. Sie müssen sich erneut bei Pinterest authentifizieren, damit die neue Karte mit Pinterest verbunden ist (Anweisungen weiter oben). Sobald Sie dies getan haben, wenden Sie sich an uns.

Die Datenflüsse zu Pinterest auf der alten Karte müssen deaktiviert und die Datenflüsse auf der neuen Karte müssen aktiviert werden. Sie können dies manuell in der Benutzeroberfläche tun, oder Sie können sich an Adobe wenden und wir werden dies für Sie tun.

## Sonstige zu beachtende Punkte

Nachdem Sie die Datenflüsse auf der neuen Zielkarte aktiviert und die Datenflüsse auf den alten Zielkarten deaktiviert haben, sollten Sie keine Unterbrechung Ihrer Kampagnen oder der Anzahl der qualifizierten Profile in den Zielgruppen sehen, die aus Adobe Real-Time CDP eingehen.
