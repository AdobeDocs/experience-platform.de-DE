---
title: Zielgruppen-Lebenszyklus in Experience Platform und Streaming-Ziele
description: Erfahren Sie, wie Zielgruppennamen und -zuordnungen aus Experience Platform in Streaming-Zielplattformen dargestellt werden.
source-git-commit: 6b4dfa714e078fb5b97900811aade081ffef0d78
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 3%

---


# Zielgruppen-Lebenszyklus in Streaming-Zielen

Auf dieser Seite wird beschrieben, wie Aktualisierungen und Zuordnungen von Zielgruppennamen in Experience Platform mit Streaming-Zielplattformen synchronisiert werden. Wenn Sie in Experience Platform Zielgruppennamen ändern oder Zielgruppenzuordnungen entfernen, variiert das Verhalten je nach den Funktionen der Zielplattform.

Das Verständnis dieser Unterschiede ist für die Verwaltung von Zielgruppen-Lebenszyklusvorgängen wichtig und stellt sicher, dass Ihre Zielplattformen den aktuellen Status Ihrer Zielgruppen in Experience Platform widerspiegeln.

## Verhalten bei der Verbreitung von Zielgruppennamen {#audience-name-propagation}

Wenn Sie eine Zielgruppe für ein Streaming-Ziel aktivieren, wird der Zielgruppenname bei der ersten Aktivierung an das Ziel gesendet. Das Verhalten bei der Aktualisierung des Zielgruppennamen variiert jedoch je nach Ziel:

* **[Ziele, die Namensaktualisierungen für Zielgruppen unterstützen](#name-update-supported)**: Wenn Sie einen Zielgruppennamen in Experience Platform ändern, wird der aktualisierte Name automatisch auf diese Ziele übertragen.
* **[Ziele, die keine Aktualisierungen des Zielgruppennamen unterstützen](#name-update-not-supported)**: Wenn Sie einen Zielgruppennamen in Experience Platform ändern, verwendet das Ziel weiterhin den Originalnamen aus der ersten Aktivierung.

### Ziele, die die Aktualisierung von Zielgruppennamen unterstützen {#name-update-supported}

Die folgenden Streaming-Ziele unterstützen automatische Namensaktualisierungen für Zielgruppen, wenn Sie Zielgruppennamen in Experience Platform ändern:

* [Verbindung mit Acxiom-Zielgruppe](../catalog/advertising/acxiom-audience-connection.md)
* [Adobe Campaign Managed Cloud](../catalog/email-marketing/adobe-campaign-managed-services.md)
* [Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [Bombora](../catalog/advertising/bombora.md)
* [Criteo](../catalog/advertising/criteo.md)
* [Demandbase](../catalog/advertising/demandbase.md)
* [Demandbase People](../catalog/advertising/demandbase-people.md)
* [Experience Cloud-Zielgruppen](../catalog/adobe/experience-cloud-audiences.md)
* [Benutzerdefinierte Facebook-Zielgruppe](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [LINE](../catalog/mobile-engagement/line.md)
* [(Firmen) LinkedIn Matched Audience](../catalog/social/linkedin-b2b.md)
* [Zugeordnete LinkedIn-Zielgruppe](../catalog/social/linkedin.md)
* [(Legacy) (v2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [SendGrid](../catalog/email-marketing/sendgrid.md)
* [SNAP erh](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Benutzerdefinierte Twitter-Zielgruppen](../catalog/social/twitter.md)
* [Yahoo DataX](../catalog/advertising/datax.md)

### Ziele, die keine Aktualisierungen des Zielgruppennamen unterstützen {#name-update-not-supported}

Bei Zielen, die oben nicht aufgeführt sind, bleiben Zielgruppennamen nach der ersten Aktivierung statisch. Wenn Sie einen Zielgruppennamen für diese Ziele aktualisieren müssen, müssen Sie:

1. Erstellen Sie in Experience Platform eine neue Zielgruppe mit dem gewünschten Namen
2. Aktivieren der neuen Zielgruppe für das Ziel

>[!TIP]
>
>Um Verwirrung zu vermeiden, verwenden Sie beschreibende Zielgruppennamen von der ersten Aktivierung, insbesondere bei der Aktivierung für Ziele, die keine Aktualisierungen des Zielgruppennamen unterstützen.

## Ziele, die das Entfernen von Zielgruppen unterstützen {#support-removal}

Wenn Sie eine Zielgruppe aus einem Streaming-Ziel entfernen (deren Zuordnung aufheben), versucht Experience Platform, die entsprechende Zielgruppe aus der Zielplattform zu entfernen. Nicht alle Ziele unterstützen diese Funktion.

Die folgenden Streaming-Ziele unterstützen das automatische Entfernen von Zielgruppen, wenn Sie die Zuordnung einer Zielgruppe zum Ziel aufheben:

* [(API) Oracle Eloqua](../catalog/email-marketing/oracle-eloqua-api.md)
* [(Firmen) LinkedIn Matched Audience](../catalog/social/linkedin-b2b.md)
* [(Legacy) (v2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [Adobe Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [Zielgruppen des Bombora-Kontos](../catalog/advertising/bombora.md)
* [Criteo](../catalog/advertising/criteo.md)
* [Experience Cloud-Zielgruppen](../catalog/adobe/experience-cloud-audiences.md)
* [Facebook](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [HubSpot](../catalog/crm/hubspot.md)
* [LINE](../catalog/mobile-engagement/line.md)
* [Abgestimmte LinkedIn-Zielgruppen](../catalog/social/linkedin.md)
* [LiveRamp - Verteilung](../catalog/advertising/liveramp-distribution.md)
* [Mailchimp-Interessenkategorien](../catalog/email-marketing/mailchimp-interest-categories.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [Salesforce Marketing Cloud-Kundeninteraktion](../catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)
* [SendGrid](../catalog/email-marketing/sendgrid.md)
* [SNAP erh](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Benutzerdefinierte Twitter-Zielgruppen](../catalog/social/twitter.md)
* [Yahoo DataX](../catalog/advertising/datax.md)

### Ziele, die das Entfernen von Zielgruppen nicht unterstützen

Wenn Sie bei Zielen, die oben nicht aufgeführt sind, die Zuordnung einer Zielgruppe zum Ziel aufheben, entfernt Experience Platform nur die Zuordnung. Die Zielgruppe in der Zielplattform bleibt aktiv, bis Sie sie manuell in der Partnerplattform löschen.
