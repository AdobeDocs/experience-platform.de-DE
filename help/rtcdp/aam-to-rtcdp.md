---
title: Wechsel von Audience Manager zu Real-Time CDP
description: Machen Sie sich damit vertraut, was vor der Migration von Audience Manager nach Real-Time CDP alles zu beachten ist.
source-git-commit: 147e95cce203933d591fc807d9d20bcbc06e68e3
workflow-type: ht
source-wordcount: '538'
ht-degree: 100%

---


# Wechsel von Audience Manager zu Real-Time CDP

Wenn sich Ihr Unternehmen entschließt, Adobe Real-Time CDP zu verwenden, sollten Sie sich diese Hinweise ansehen, um Ihre Daten vorzubereiten und um sich über die wichtigen Unterschiede zwischen den beiden Technologien zu informieren. Dieser Artikel richtet sich an Praktikerinnen und Praktiker.

![Abbildung zum Wechsel von Audience Manager zu Real-Time CDP](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. Berücksichtigen der Datenarchitektur in Audience Manager

Wenn Sie über den Wechsel von Audience Manager zu Real-Time CDP nachdenken, ist nun ein kritischer Zeitpunkt gekommen, um Ihre [Audience Manager-Segmente](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=de) zu analysieren und zu bestimmen, welche [Kennzeichen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=de), [Eigenschaften](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=de) und [Regeln](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=de#segment-builder-section) diese Segmente ausmachen.

Stellen Sie außerdem Überlegungen über die aktuell in Audience Manager verwendeten Datenquellen an.

Adobe empfiehlt, Ihre Segmente wie folgt zu kategorisieren:

* Segmente, die über den [[!UICONTROL Audience Manager-Quell-Connector]](/help/sources/connectors/adobe-applications/audience-manager.md) an Experience Platform gesendet werden können, da sie keine Datenabhängigkeiten, keine Ziel- oder Aktivierungsprobleme haben, und deren Segmentierungsregeln später über den Real-time CDP [Segment Builder](/help/segmentation/ui/segment-builder.md) erstellt werden können.
* Segmente mit Regeln, die unterstützt werden können, aber möglicherweise Daten enthalten, die in Real-Time CDP nicht verfügbar sind.
* Segmente, die nicht in Real-Time CDP erstellt werden können und denen Funktionen fehlen.

>[!TIP]
>
>Adobe Real-Time CDP bietet [drei Arten der Segmentauswertung](/help/segmentation/home.md#evaluate-segments): [!UICONTROL Batch], [!UICONTROL Streaming] und [!UICONTROL Edge]. Kundinnen und Kunden, die Echtzeit-Segmente in Audience Manager verwenden, können durch die aktuelle Grenze von 500 Streaming-Segmenten in Real-Time CDP eingeschränkt sein. Weitere Informationen dazu finden Sie in den [Leitlinien für die Segmentierung](/help/profile/guardrails.md).

## 2. Welche Segmente müssen unbedingt über den [!UICONTROL Audience Manager-Quell-Connector] gesendet werden?

Auf Grundlage ihrer Auswertungskriterien sollten Segmente ohne Datenabhängigkeiten, Ziel- oder Aktivierungsprobleme über den Audience Manager-Quell-Connector gesendet werden. Ihre Segmentierungsregeln können dabei zu einem späteren Zeitpunkt mittels Real-Time CDP-Datenerfassung (z. B. über [Adobe Experience Platform Web SDK](/help/edge/web-sdk-faq.md)) erstellt werden.

## 3. Werden Sie Daten mithilfe der Zielkarte [!UICONTROL Experience Cloud-Zielgruppen] nach Audience Manager zurückholen?

Segmente mit Regeln, die in Real-Time CDP unterstützt werden können, aber Aktivierungsabhängigkeiten gegenüber Audience Manager aufweisen, könnten über die Zielkarte [Experience Cloud-Zielgruppen](/help/destinations/catalog/adobe/experience-cloud-audiences.md) gesendet werden.

## 4. Welche Ziele haben Sie derzeit in Audience Manager eingerichtet, die Sie nach Real-Time CDP umziehen lassen können?

Adobe empfiehlt ausdrücklich, dass in Audience Manager für [benutzerbasierte Ziele](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=de) aktivierte Segmente über den [!UICONTROL Audience Manager-Quell-Connector] nach Real-Time CDP per Push übertragen werden, um dann eine Aktivierung über Real-Time CDP durchzusetzen.

Alle benutzerbasierten Ziele, die in Audience Manager verfügbar sind – [Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Google Customer Match]](/help/destinations/catalog/advertising/google-customer-match.md), [LinkedIn](/help/destinations/catalog/social/linkedin.md) – sind auch in Real-Time CDP verfügbar.

Zusätzliche Erstanbieter-Daten- und -Medienstrategiepartner wie [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) und [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md) sind verfügbar.

Real-Time CDP unterstützt derzeit über 60 Ziele nativ im [Katalog](/help/destinations/catalog/overview.md), darunter mehr als 20 Werbe- oder Social-Ziele, die das Audience Matching von Erstanbietern unterstützen.

## Nächste Schritte

Nachdem Sie diese Seite gelesen haben, können Sie nun erste Überlegungen für Ihren Wechsel von Audience Manager zu Real-Time CDP anstellen.
