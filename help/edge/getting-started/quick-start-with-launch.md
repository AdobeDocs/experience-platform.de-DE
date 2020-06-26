---
title: Schnellstart mit Launch
seo-title: Adobe Experience Platform Web SDK – Schnellstart mit Launch
description: Kurzanleitung zum Einsatz der Experience Platform Web SDK-Erweiterung zur Datenerfassung
seo-description: Kurzanleitung zum Einsatz der Experience Platform Web SDK-Erweiterung zur Datenerfassung
translation-type: tm+mt
source-git-commit: 3f52def8318f57cfc6534e15415d172e768a8614
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 27%

---


# Willkommen

In diesem Handbuch werden die verschiedenen Schritte zum Einrichten des Adobe Experience Platform Web SDK in Adobe Launch beschrieben. Sie müssen über Berechtigungen verfügen und auf der zulassungsliste sein, um diese Funktion zu verwenden. Wenn Sie auf die wartende Liste kommen möchten, wenden Sie sich bitte an Ihren CSM. Um diese Funktion nutzen zu können, müssen Sie außerdem:

- Sie benötigen eine aktivierte [Erstanbieter-Domäne (CNAME)](https://docs.adobe.com/content/help/de-DE/core-services/interface/ec-cookies/cookies-first-party.html). Wenn Sie bereits über einen CNAME für Adobe Analytics verfügen, sollten Sie diesen verwenden. Tests in der Entwicklung funktionieren ohne CNAME, Sie benötigen jedoch einen, bevor Sie zur Produktion gehen
- Verwenden Sie die neueste Version des Besucher-ID-Diensts

## Erstellen einer Konfigurations-ID

Sie können eine Konfigurations-ID mit dem [Edge-Konfigurationstool](../fundamentals/edge-configuration.md) in Adobe Launch erstellen. Dadurch können Sie das Edge-Netzwerk aktivieren, um Daten an die verschiedenen Lösungen zu senden. Auf der Seite &quot; [Edge Configuration Tool](../fundamentals/edge-configuration.md) &quot;finden Sie Informationen zum Auffinden der einzelnen Optionen.

>[!NOTE]
>
>Ihre Organisation muss für die Funktion auf der zulassungsliste sein. Wenden Sie sich an Ihren CSM, um zur zulassungsliste hinzugefügt zu werden.

## Schemas vorbereiten

Das Experience Platform Edge Network nimmt Daten als XDM. XDM ist ein Datenformat, mit dem Sie Schema definieren können. Das Schema definiert, wie das Edge-Netzwerk erwartet, dass die Daten formatiert werden. Um Daten zu senden, müssen Sie Ihr Schema definieren. Vergewissern Sie sich, dass Sie Folgendes abgeschlossen haben:

- [Schema erstellen](../../xdm/tutorials/create-schema-ui.md)
- Fügen Sie dem erstellten Schema das Adobe Experience Platform Web SDK-Mixin hinzu

## SDK in Adobe Launch installieren

Log in to Adobe Launch and install the `AEP Web SDK` extension. Während der Installation des SDK werden Sie aufgefordert, die Erweiterung zu konfigurieren. Geben Sie die oben angeforderte Konfigurations-ID ein. Die Erweiterung füllt Ihre Organisations-ID automatisch aus.

Weitere Informationen zu den verschiedenen Konfigurationsoptionen finden Sie unter [Konfigurieren des SDK](../fundamentals/configuring-the-sdk.md).

## Datenelementbasis auf Ihrem Schema erstellen

Erstellen Sie in Adobe Launch ein Datenelement, das auf das Schema verweist, indem Sie die Erweiterung auf AEP Web SDK ändern und den Typ auf XDM-Objekt festlegen. Dadurch wird Ihr Schema hochgeladen und Sie können Datenelemente verschiedenen Teilen des Schemas zuordnen.

![Datumselement beim Start](../../assets/edge_data_element.png)

## Ereignis senden

Nachdem die Erweiterung installiert wurde, sendet Beginn Ereignis, indem eine &quot;sendEvent&quot;-Aktion aus der AEP Web SDK-Erweiterung zu einer Regel hinzugefügt wird. Fügen Sie dem Ereignis unbedingt das soeben erstellte Datenelement als XDM-Daten hinzu. Es wird empfohlen, jedes Mal, wenn eine Seite geladen wird, mindestens ein Ereignis zu senden.

Weitere Informationen zur Verfolgung von Ereignissen finden Sie unter [Verfolgen von Ereignissen](../fundamentals/tracking-events.md).

## Nächste Schritte

Sobald Daten gesendet wurden, können Sie Folgendes tun:

- [Erstellen Sie Ihr Schema](https://docs.adobe.com/content/help/de-DE/experience-platform/xdm/schema/composition.html)
- [Informationen zum Debugging](../fundamentals/debugging.md)
- Erfahren Sie, wie Sie das Erlebnis [personalisieren.](../fundamentals/rendering-personalization-content.md)
- Informationen zum Senden von Daten an mehrere Lösungen
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
