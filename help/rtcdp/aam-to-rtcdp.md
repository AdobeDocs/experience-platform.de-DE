---
title: Wechsel von Audience Manager zu Real-Time CDP
description: Machen Sie sich mit den Überlegungen vertraut, bevor Sie Ihre Migration von Audience Manager zu Adobe Real-Time CDP planen.
exl-id: 83ab9a5d-9abc-4072-b449-e2a9ecd48639
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 67%

---

# Wechsel von Audience Manager zu Real-Time CDP

Wenn sich Ihr Unternehmen entschließt, Adobe Real-Time CDP zu verwenden, sollten Sie sich diese Hinweise ansehen, um Ihre Daten vorzubereiten und um sich über die wichtigen Unterschiede zwischen den beiden Technologien zu informieren. Dieser Artikel richtet sich an Praktikerinnen und Praktiker.

![Abbildung zum Wechsel von Audience Manager zu Real-Time CDP](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## &#x200B;1. Berücksichtigen der Datenarchitektur in Audience Manager

Wenn Sie über den Wechsel von Audience Manager zu Real-Time CDP nachdenken, ist nun ein kritischer Zeitpunkt gekommen, um Ihre [Audience Manager-Segmente](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=de) zu analysieren und zu bestimmen, welche [Kennzeichen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=de), [Merkmale](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=de) und [Regeln](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=de#segment-builder-section) diese Segmente ausmachen.

Stellen Sie außerdem Überlegungen über die aktuell in Audience Manager verwendeten Datenquellen an.

Adobe empfiehlt, Ihre Segmente wie folgt zu kategorisieren:

* Segmente, die über die [[!UICONTROL Audience Manager Source Connector]](/help/sources/connectors/adobe-applications/audience-manager.md) an Experience Platform gesendet werden können, da sie keine Datenabhängigkeiten, keine Zielgruppen- oder Aktivierungsprobleme aufweisen und ihre Segmentierungsregeln später über den Real-Time CDP [Segment Builder](/help/segmentation/ui/segment-builder.md) erstellt werden können.
* Segmente mit Regeln, die unterstützt werden können, aber möglicherweise Daten enthalten, die in Real-Time CDP nicht verfügbar sind.
* Segmente, die in Real-Time CDP nicht erstellt werden können und denen eine Funktion fehlt.

>[!TIP]
>
>Adobe Real-Time CDP bietet [drei Arten der Segmentauswertung](/help/segmentation/home.md#evaluate-segments): [!UICONTROL Batch], [!UICONTROL Streaming] und [!UICONTROL Edge]. Kundinnen und Kunden, die Echtzeit-Segmente in Audience Manager verwenden, können durch die aktuelle Grenze von 500 Streaming-Segmenten in Real-Time CDP eingeschränkt sein. Weitere Informationen dazu finden Sie in den [Leitlinien für die Segmentierung](/help/profile/guardrails.md).

## &#x200B;2. Welche Segmente müssen unbedingt über [!UICONTROL Audience Manager Source Connector] gesendet werden?

Auf Grundlage ihrer Auswertungskriterien sollten Segmente ohne Datenabhängigkeiten, Ziel- oder Aktivierungsprobleme über den Audience Manager-Quell-Connector gesendet werden. Ihre Segmentierungsregeln können dabei zu einem späteren Zeitpunkt mittels Real-Time CDP-Datenerfassung (z. B. über [Adobe Experience Platform Web SDK](/help/collection/js/faq.md)) erstellt werden.

## &#x200B;3. Verwenden Sie das [!UICONTROL Experience Cloud Audiences]-Ziel, um Daten zurück an Audience Manager zu senden?

Segmente mit Regeln, die in Real-Time CDP unterstützt werden können, aber Aktivierungsabhängigkeiten gegenüber Audience Manager aufweisen, könnten über die Zielkarte [Experience Cloud-Zielgruppen](/help/destinations/catalog/adobe/experience-cloud-audiences.md) gesendet werden.

## &#x200B;4. Welche Ziele haben Sie derzeit in Audience Manager eingerichtet, die Sie nach Real-Time CDP umziehen lassen können?

Adobe empfiehlt dringend, Segmente, die in Audience Manager für [personenbasierte Ziele“ aktiviert &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=de), über die [!UICONTROL Audience Manager Source Connector] an Real-Time CDP zu pushen, um sie dann über Real-Time CDP zu aktivieren.

Alle in Audience Manager verfügbaren personenbasierten Ziele - [Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Google Customer Match]](/help/destinations/catalog/advertising/google-customer-match.md), [LinkedIn](/help/destinations/catalog/social/linkedin.md) - sind auch in Real-Time CDP verfügbar.

Weitere First-Party-Daten- und Medienstrategiepartner wie [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) und [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md) sind verfügbar.

Real-Time CDP unterstützt derzeit über 60 Ziele nativ im [Katalog](/help/destinations/catalog/overview.md), darunter mehr als 20 Werbe- oder Social-Ziele, die die Zielgruppen-Zuordnung von Erstanbietern unterstützen.

## Nächste Schritte

Nachdem Sie diese Seite gelesen haben, können Sie nun erste Überlegungen für Ihren Wechsel von Audience Manager zu Real-Time CDP anstellen.
