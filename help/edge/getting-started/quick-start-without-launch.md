---
title: Schneller Beginn mit einfachem Javascript
seo-title: 'Adobe Experience Platform Web SDK - SchnellBeginn '
description: Kurzanleitung zum Verwenden des Experience Platform Web SDK zum Erfassen von Daten
seo-description: Kurzanleitung zum Verwenden des Experience Platform Web SDK zum Erfassen von Daten
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 13%

---


# Willkommen

Dieser Leitfaden führt Sie durch die verschiedenen Möglichkeiten, die Adobe Experience Platform einzurichten [!DNL Web SDK]. Um diese Funktion nutzen zu können, müssen Sie auf der Zulassungsliste sein. Wenn Sie auf die wartende Liste kommen möchten, wenden Sie sich bitte an Ihren CSM.

- Sie benötigen eine aktivierte [Erstanbieter-Domäne (CNAME)](https://docs.adobe.com/content/help/de-DE/core-services/interface/ec-cookies/cookies-first-party.html). If you already have a CNAME for [!DNL Analytics], you should use that one. Tests in der Entwicklung funktionieren ohne CNAME, Sie benötigen jedoch einen, bevor Sie zur Produktion gehen
- Berechtigung für Adobe Experience Platform [!DNL Data Platform].  Wenn Sie keine Plattform gekauft haben, stellen wir Ihnen eine begrenzte Verwendung mit dem SDK ohne Aufpreis [!DNL Experience Platform Data Services Foundation] zur Verfügung.
- Verwenden Sie die neueste Version des Besucher-ID-Diensts

## Erstellen einer Konfigurations-ID

Sie können eine Konfigurations-ID mit dem [Edge-Konfigurationstool](../fundamentals/edge-configuration.md) in Adobe Launch erstellen, auch wenn Sie die Tag-Management-Funktionen nicht verwenden. Auf diese Weise können Sie das Senden von Daten [!DNL Edge Network] an die verschiedenen Lösungen aktivieren. Einzelheiten zu den einzelnen Optionen finden Sie auf der Seite [Edge Configuration Tool](../fundamentals/edge-configuration.md) .

>[!NOTE]
>
>Ihr Unternehmen muss für diese Funktion auf der Zulassungsliste stehen. Wenden Sie sich an Ihren CSM, um die Zulassungsliste zu erhalten.

## Schemas vorbereiten

Die [!DNL Experience Platform Edge Network] Daten werden als XDM verwendet. XDM ist ein Datenformat, mit dem Sie Schema definieren können. Das Schema definiert, wie die Daten formatiert werden [!DNL Edge Network] sollen. Um Daten zu senden, müssen Sie Ihr Schema definieren.

- [Erstellen eines Schemas](../../xdm/tutorials/create-schema-ui.md)
- Add the Adobe Experience Platform [!DNL Web SDK] mixin to the schema you created

Das folgende Video soll Sie beim Erstellen eines Schema-, Datasets- und Streaming-Quell-Connectors für Ihre [!DNL Web SDK] Daten unterstützen.

>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

## SDK installieren

Um das SDK zu installieren, kopieren Sie den folgenden &quot;Basiscode&quot;so hoch wie möglich im `<head>` -Tag Ihres HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

Weitere Informationen zu verschiedenen Optionen finden Sie unter [Installieren des SDK](../fundamentals/installing-the-sdk.md).

## SDK konfigurieren

Als Nächstes stellen Sie Ihre Konfiguration für das SDK bereit. Dies geschieht mithilfe des `configure` Befehls. Dies sollte der erste Befehl sein, der auf jeder Seite aufgerufen wird.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93:dev",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Hier geben Sie die oben erstellte Konfigurations-ID sowie Ihre Organisations-ID ein. Dies sind die einzigen zwei erforderlichen Felder. Es gibt jedoch noch viele andere [Konfigurationsoptionen](../fundamentals/configuring-the-sdk.md).

## Ereignis senden

Nachdem Sie den Befehl &quot;configure&quot;aufgerufen haben, können Sie Ereignis zur Beginn-Verfolgung aufrufen.

```javascript
alloy("sendEvent", {});
```

Normalerweise senden Sie Ereignisse mit einigen Daten. Sie können XDM-Daten wie folgt senden. Die gesendeten Daten müssen sich in dem Schema befinden, das Sie in XDM erstellt haben.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web":{
      "webPageDetails":{
        "name":"Home Page"
      }
    }
  }
});
```

Weitere Informationen zur Verfolgung von Ereignissen finden Sie unter [Verfolgen von Ereignissen](../fundamentals/tracking-events.md).

## Nächste Schritte

Nachdem die Daten gesendet wurden, haben Sie folgende Möglichkeiten:

- [Erstellen Sie Ihr Schema](https://docs.adobe.com/content/help/de-DE/experience-platform/xdm/schema/composition.html)
- [Informationen zum Debugging](../fundamentals/debugging.md)
- Erfahren Sie, wie Sie das Erlebnis [personalisieren.](../fundamentals/rendering-personalization-content.md)
- Informationen zum Senden von Daten an mehrere Lösungen
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
