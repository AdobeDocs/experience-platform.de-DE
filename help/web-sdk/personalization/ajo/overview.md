---
title: Verwenden von Adobe Journey Optimizer mit dem Platform Web SDK
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK mit Adobe Journey Optimizer rendern
keywords: ajo; ajo web; adobe Journey optimizer; renderDecisions; Oberflächen; Entscheidungen; Vorschläge; Umfang; Schema
exl-id: 3f28e2bc-2c4b-4400-8f69-c7316449ff4f
source-git-commit: ae6c6d21b1eea900d01be3287827296071429d30
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 1%

---

# Verwenden von [!DNL Adobe Journey Optimizer] mit dem [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] kann personalisierte Erlebnisse, die in [!DNL Adobe Journey Optimizer] verwaltet werden, für den Webkanal bereitstellen und rendern. Sie können einen WYSIWYG-Editor, [!DNL Adobe Journey Optimizer] [Webkanal](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) oder eine nicht visuelle Schnittstelle, den [code-basierten Experience-Kanal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based), verwenden, um Ihre [!DNL Journey Optimizer Web]-Kampagnen und Personalisierungserlebnisse zu erstellen, zu aktivieren und bereitzustellen.

>[!IMPORTANT]
>
>Informationen zu den ersten Schritten mit dem [!DNL Journey Optimizer Web] -Erlebnis-Authoring und -Reporting finden Sie in der Dokumentation zu Adobe Journey Optimizer-Webkanälen](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html?lang=de) .[

## Terminologie {#terminology}

**[!UICONTROL Oberfläche]**: Eine Weboberfläche ist eine Webseite oder Position auf einer Seite, die durch einen URI identifiziert wird, auf der der Erlebnisinhalt [!DNL Adobe Journey Optimizer] bereitgestellt wird.

**[!UICONTROL Vorschläge]**: In [!DNL Adobe Journey Optimizer] korrelieren Vorschläge mit dem Erlebnis, das aus einem [!DNL Journey Optimizer Campaign] ausgewählt wurde.

## Aktivieren von [!DNL Adobe Journey Optimizer] {#enable-ajo}

Gehen Sie wie folgt vor, um mit der Verwendung von [!DNL Adobe Journey Optimizer] zu beginnen.

1. Gehen Sie im [!DNL Adobe Journey Optimizer] [Web Experience Guide](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) durch die [Voraussetzungen](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#prerequesites), insbesondere:
   * Einrichten von [!DNL Adobe Experience Cloud Visual Editing Helper].
   * Aktivieren Sie [!DNL Adobe Journey Optimizer] in Ihrem [Datastream](../../../datastreams/overview.md).
   * Aktivieren Sie die Option [!UICONTROL Richtlinie zum Zusammenführen von aktiven Elementen in Edge] .

2. Fügen Sie Ihren Ereignissen die Option `renderDecisions` hinzu. Setzen Sie `renderDecisions` auf `true` , um die bereitgestellten Journey Optimizer-Inhaltsvorschläge auf den Oberflächen Ihrer Webseite automatisch zu rendern.

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. Optional können Sie in Ihren Ereignissen zusätzliche Oberflächen angeben. Standardmäßig generiert das Web SDK automatisch die Weboberfläche für die aktuelle Webseite und fügt sie in die Anforderung an das Edge Network ein. Falls erforderlich, können zusätzliche Oberflächen in die Anfrage aufgenommen werden, indem Sie diese in der Option `personalization.surfaces` des Befehls `sendEvent` oder in der entsprechenden Konfiguration **[!UICONTROL Oberflächen]** [[!UICONTROL Ereignis senden] Aktion](../../../tags/extensions/client/web-sdk/action-types.md#send-event) der Web SDK-Erweiterung angeben.

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
           "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![extension-add-interface](./assets/extension-add-surface.png)

   Ereignisflächen sind im Anforderungsfeld `query.personalization.surfaces` enthalten:

   ```json
   {
   "events": [
       {
           "query": {
               "personalization": {
               "schemas": [
                   ...
               ],
               "decisionScopes": [
                   "__view__"
               ],
               "surfaces": [
                   "web://ajostage.weebly.com/"
               ]
               }
           },
           ...
       }
   ]
   }
   ```

4. Ähnlich wie bei anderen Personalisierungsfunktionen können Sie einen **[Codeausschnitt zur Vorab-Ausblendung](../manage-flicker.md)** hinzufügen, um beim Abrufen von Erlebnissen nur bestimmte Teile der Seite auszublenden.

## Erstellen von Adobe Journey Optimizer-Web-Erlebnissen {#create-ajo-web-experiences}

Befolgen Sie die Anweisungen zum [Erstellen von Web-Kampagnen](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#create-web-campaign) im [!DNL Adobe Journey Optimizer] [Web-Erlebnisse-Handbuch](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) , um [!DNL Journey Optimizer Web] Kampagnen und Erlebnisse zu erstellen.

## Rendern von personalisiertem Inhalt {#rendering-personalized-content}

Weitere Informationen finden Sie in der Dokumentation zu [Rendern von Personalisierungsinhalten](../rendering-personalization-content.md) .

Adobe Journey Optimizer-Vorschläge für Weboberflächen werden auf ähnliche Weise verarbeitet wie die Vorschläge für den Entscheidungsbereich von `__view__`. Wenn die Option `renderDecisions` im Befehl `sendEvent` auf `true` gesetzt ist, werden diese vom Web SDK automatisch gerendert.

Beispiel für Journey Optimizer-Inhaltsvorschlag:

```json
{
    "scope": "web://ajostage.weebly.com/",
    "scopeDetails": {
        "correlationID": "ccfaf19c-6360-4aea-b464-0cf924db5da7",
        "characteristics": {
            "eventToken": "eyJtZXNzYWdlRXhlY3V0aW9uIjp7Im1lc3NhZ2VFeGVjdXRpb25JRCI6ImEzNDYxYTMzLTc5MjktNGQyNS1hNmMxLTVkYzM2YWY1NzRmMyIsIm1lc3NhZ2VJRCI6ImNjZmFmMTljLTYzNjAtNGFlYS1iNDY0LTBjZjkyNGRiNWRhNyIsIm1lc3NhZ2VUeXBlIjoibWFya2V0aW5nIiwiY2FtcGFpZ25JRCI6IjEzN2JmMzllLWM1ODgtNGI1My1iODQxLTJiMWZiZDYxM2JkYiIsImNhbXBhaWduVmVyc2lvbklEIjoiMTA1NzY1MmEtZWYwNS00YjE3LWExMmUtY2FlOTQyOTFhMWFjIiwiY2FtcGFpZ25BY3Rpb25JRCI6ImViNTlmODQ4LTk5ZDYtNGE1OC05YmU4LTk4MjIxODU0NmYzNiIsIm1lc3NhZ2VQdWJsaWNhdGlvbklEIjoiYzg2NzFjZmItNDdjYS00YTVjLTg4Y2YtNzYwZDFlZjU1MzQyIn0sIm1lc3NhZ2VQcm9maWxlIjp7ImNoYW5uZWwiOnsiX2lkIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWxzL3dlYiIsIl90eXBlIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWwtdHlwZXMvd2ViIn0sIm1lc3NhZ2VQcm9maWxlSUQiOiI2YTViY2I3ZC02MmYxLTQ5NDItODRkMC02MzE5ZjM5Zjk1ZGUifX0="
        },
        "decisionProvider": "AJO",
        "activity": {
            "id": "137bf39e-c588-4b53-b841-2b1fbd613bdb#eb59f848-99d6-4a58-9be8-982218546f36"
        }
    },
    "id": "002321c0-dff5-4153-b171-a9dfb70b9750",
    "items": [
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": "Welcome AJO!",
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setHtml",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "0a522f66-9e6a-4ded-b1d0-e9167f103290"
        },
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": {
                    "font-weight": "bold"
                },
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setStyle",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "66216ca5-5d0f-4239-a8c8-6bc4a5a7cbdb"
        }
    ]
}
```

## Debugging {#debugging}

Verwenden Sie zum Debuggen von Adobe Journey Optimizer-Personalisierungsimplementierungen das [Debugging des Web SDK](/help/web-sdk/use-cases/debugging.md). [!DNL Adobe Journey Optimizer] Debug-Traces sind verfügbar, wenn Sie eine Fehlerbehebung mit [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/) durchführen. Suchen Sie nach Ereignissen mit dem Präfix `AJO:` .

![assurance-ajo-trace](./assets/assurance-ajo-trace.png)
