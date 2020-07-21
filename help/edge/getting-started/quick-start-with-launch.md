---
title: Schnellstart mit Launch
seo-title: Adobe Experience Platform Web SDK – Schnellstart mit Launch
description: Kurzanleitung zum Einsatz der Experience Platform Web SDK-Erweiterung zur Datenerfassung
seo-description: Kurzanleitung zum Einsatz der Experience Platform Web SDK-Erweiterung zur Datenerfassung
translation-type: tm+mt
source-git-commit: 8574a2d54c00f1bd3c41780fb12ff739a7d98fc3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 28%

---


# Willkommen

Dieser Leitfaden führt Sie durch die verschiedenen Möglichkeiten, das Web SDK für Adobe Experience Platformen in Launch einzurichten. Um diese Funktion nutzen zu können, müssen Sie in der Positivliste eingetragen sein. Wenn Sie auf die wartende Liste kommen möchten, wenden Sie sich bitte an Ihren CSM.

- Sie benötigen eine aktivierte [Erstanbieter-Domäne (CNAME)](https://docs.adobe.com/content/help/de-DE/core-services/interface/ec-cookies/cookies-first-party.html). Wenn Sie bereits über eine CNAME für Analytics verfügen, sollten Sie diese verwenden. Tests in der Entwicklung funktionieren ohne CNAME, Sie benötigen jedoch einen, bevor Sie zur Produktion gehen.
- Berechtigung für Adobe Experience Platform. Wenn Sie Platform nicht erworben haben, stellt Adobe Ihnen die Experience Platform Data Services Foundation zur begrenzten Verwendung mit dem SDK ohne Aufpreis zur Verfügung.
- Verwenden Sie die neueste Version des Besucher-ID-Diensts.

## Erstellen einer Konfigurations-ID

Sie können eine Konfigurations-ID mit dem [Edge-Konfigurationstool](../fundamentals/edge-configuration.md) in Launch erstellen. Dadurch können Sie das Edge-Netzwerk aktivieren, um Daten an die verschiedenen Lösungen zu senden. Einzelheiten zu den einzelnen Optionen finden Sie auf der Seite [Edge Configuration Tool](../fundamentals/edge-configuration.md) .

>[!NOTE]
>
>Ihre Organisation muss für diese Funktion auf die Positivliste gesetzt werden. Wenden Sie sich an Ihren CSM, um die Liste für eine eventuelle Whitelist zu erhalten.

## Schemas vorbereiten

Das Experience Platform Edge Network nimmt Daten als XDM. XDM ist ein Datenformat, mit dem Sie Schema definieren können. Das Schema definiert, wie das Edge-Netzwerk erwartet, dass die Daten formatiert werden. Um Daten zu senden, müssen Sie Ihr Schema definieren.

1. [Erstellen eines Schemas](../../xdm/tutorials/create-schema-ui.md)
2. Hinzufügen Sie das AEP [!DNL Web SDK ExperienceEvent] Mixin mit dem von Ihnen erstellten Schema.
3. Erstellen Sie einen Datensatz aus dem erstellten Schema.

Das folgende Video soll Sie beim Erstellen eines Schema-, Datasets- und Streaming-Quell-Connectors für Ihre [!DNL Web SDK] Daten unterstützen.

Melden Sie sich bei Launch an und installieren Sie die `AEP Web SDK`-Erweiterung. Wenn Sie das SDK installieren, werden Sie aufgefordert, die Erweiterung zu konfigurieren. Geben Sie die oben angeforderte Konfigurations-ID ein. Die Erweiterung füllt Ihre Organisations-ID automatisch aus.


Weitere Informationen zu den verschiedenen Konfigurationsoptionen finden Sie unter [Konfigurieren des SDK](../fundamentals/configuring-the-sdk.md).

## Datenelement basierend auf Ihrem Schema erstellen

Erstellen Sie in Launch ein Datenelement, das auf das Schema verweist, indem Sie die Erweiterung auf AEP Web SDK ändern und den Typ auf `XDM Object`. Dadurch wird Ihr Schema geladen und Sie können Datenelemente verschiedenen Teilen des Schemas zuordnen.

![Datumselement beim Start](../../assets/edge_data_element.png)

## Ereignis senden

After the extension is installed, start sending events by adding a `sendEvent` action from the AEP Web SDK extension to a rule. Hinzufügen Sie das soeben erstellte Datenelement als XDM-Daten an das Ereignis. Adobe empfiehlt, dass Sie jedes Mal, wenn eine Seite geladen wird, mindestens ein Ereignis senden.

Weitere Informationen zur Verfolgung von Ereignissen finden Sie unter [Verfolgen von Ereignissen](../fundamentals/tracking-events.md).

## Nächste Schritte

Nachdem die Daten gesendet wurden, können Sie Folgendes tun.

- [Erstellen Sie Ihr Schema](https://docs.adobe.com/content/help/de-DE/experience-platform/xdm/schema/composition.html)
- [Informationen zum Debugging](../fundamentals/debugging.md)
- Erfahren Sie, wie Sie das Erlebnis [personalisieren.](../fundamentals/rendering-personalization-content.md)
- Informationen zum Senden von Daten an mehrere Lösungen
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
