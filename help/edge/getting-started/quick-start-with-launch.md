---
title: Schnellstart mit Launch
seo-title: Adobe Experience Platform Web SDK – Schnellstart mit Launch
description: Kurzanleitung zum Einsatz der Experience Platform Web SDK-Erweiterung zur Datenerfassung
seo-description: Kurzanleitung zum Einsatz der Experience Platform Web SDK-Erweiterung zur Datenerfassung
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 31%

---


# Willkommen

In diesem Handbuch erfahren Sie, wie Sie das Adobe Experience Platform Web SDK in Launch einrichten. Um diese Funktion nutzen zu können, müssen Sie auf die Positivliste gesetzt werden. Wenn Sie auf die wartende Liste kommen möchten, wenden Sie sich bitte an Ihren CSM.

- Sie benötigen eine aktivierte [Erstanbieter-Domäne (CNAME)](https://docs.adobe.com/content/help/de-DE/core-services/interface/ec-cookies/cookies-first-party.html). Wenn Sie bereits über eine CNAME für Analytics verfügen, sollten Sie diese verwenden. Tests in der Entwicklung funktionieren ohne CNAME, Sie benötigen jedoch einen, bevor Sie zur Produktion gehen
- Sie haben die Berechtigung zur Adobe Experience Platform-Datenplattform. Wenn Sie keine Plattform gekauft haben, stellen wir Ihnen Experience Platform Data Services Foundation zur Verwendung mit dem SDK zur Verfügung.
- Verwenden Sie die neueste Version des Besucher-ID-Diensts

## Erstellen einer Konfigurations-ID

Sie können beim Start eine Konfigurations-ID mit dem [Edge-Konfigurationstool](../fundamentals/edge-configuration.md) erstellen. Dadurch können Sie das Edge-Netzwerk aktivieren, um Daten an die verschiedenen Lösungen zu senden. Einzelheiten zu den einzelnen Optionen finden Sie auf der Seite [Edge Configuration Tool](../fundamentals/edge-configuration.md) .

>Hinweis: Ihre Organisation muss für die Funktion auf die Positivliste gesetzt werden. Wenden Sie sich an Ihren CSM, um die Liste für eine eventuelle Whitelist zu erhalten.

## Schemas vorbereiten

Das Experience Platform Edge Network verwendet Daten als XDM. XDM ist ein Datenformat, mit dem Sie Schema definieren können. Das Schema definiert, wie das Edge-Netzwerk erwartet, dass die Daten formatiert werden. Um Daten zu senden, müssen Sie Ihr Schema definieren.

- [Schema erstellen](../../xdm/tutorials/create-schema-ui.md)
- Fügen Sie dem erstellten Schema das Adobe Experience Platform Web SDK-Mixin hinzu

## SDK in Launch installieren

Melden Sie sich bei Launch an und installieren Sie die `AEP Web SDK`-Erweiterung. Während der Installation des SDK werden Sie aufgefordert, die Erweiterung zu konfigurieren. Geben Sie die oben angeforderte Konfigurations-ID ein. Die Erweiterung füllt Ihre Organisations-ID automatisch aus.

Weitere Informationen zu den verschiedenen Konfigurationsoptionen finden Sie unter [Konfigurieren des SDK](../fundamentals/configuring-the-sdk.md).

## Datenelementbasis auf Ihrem Schema erstellen

Erstellen Sie beim Start ein Datenelement, das auf das Schema verweist, indem Sie die Erweiterung auf AEP Web SDK ändern und den Typ auf XDM-Objekt festlegen. Dadurch wird Ihr Schema hochgeladen und Sie können Datenelemente verschiedenen Teilen des Schemas zuordnen.

![Datumselement beim Start](../../assets/edge_data_element.png)

## Ereignis senden

Nachdem die Erweiterung installiert wurde, sendet Beginn Ereignis, indem eine &quot;sendEvent&quot;-Aktion aus der AEP Web SDK-Erweiterung zu einer Regel hinzugefügt wird. Fügen Sie dem Ereignis unbedingt das soeben erstellte Datenelement als XDM-Daten hinzu. Es wird empfohlen, jedes Mal, wenn eine Seite geladen wird, mindestens ein Ereignis zu senden.

Weitere Informationen zur Verfolgung von Ereignissen finden Sie unter [Verfolgen von Ereignissen](../fundamentals/tracking-events.md).

## Nächste Schritte

Sobald Daten gesendet wurden, können Sie Folgendes tun.

- [Erstellen Sie Ihr Schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
- Erfahren Sie, wie Sie das Erlebnis [personalisieren.](../fundamentals/rendering-personalization-content.md)
- Informationen zum Senden von Daten an mehrere Lösungen
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
