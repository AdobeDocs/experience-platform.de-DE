---
title: Verwenden von Adobe Journey Optimizer mit dem Platform Web SDK
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK mit Adobe Journey Optimizer rendern
keywords: ajo; ajo web; adobe Journey optimizer; renderDecisions; Oberflächen; Entscheidungen; Vorschläge; Umfang; Schema
exl-id: 3f28e2bc-2c4b-4400-8f69-c7316449ff4f
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 2%

---

# Verwenden [!DNL Adobe Journey Optimizer] mit dem [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] kann personalisierte Erlebnisse bereitstellen und rendern, die in verwaltet werden [!DNL Adobe Journey Optimizer] zum Webkanal hinzu. Sie können einen WYSIWYG-Editor verwenden, [!DNL Adobe Journey Optimizer] [Web-Campaign-Benutzeroberfläche](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), um Ihre [!DNL Journey Optimizer Web] Kampagnen und Personalisierungserlebnisse.

>[!IMPORTANT]
>
>Lesen Sie die [Adobe Journey Optimizer-Webkanal-Dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html) Informationen zu den ersten Schritten mit [!DNL Journey Optimizer Web] Erlebnis-Authoring und -Berichterstellung.

## Terminologie {#terminology}

**[!UICONTROL Oberfläche]**: Eine Weboberfläche ist eine Webeigenschaft, die durch eine URL identifiziert wird, wobei die Variable [!DNL Adobe Journey Optimizer] Erlebnisinhalte werden bereitgestellt.

**[!UICONTROL Vorschläge]**: In [!DNL Adobe Journey Optimizer], korrelieren Vorschläge mit dem aus einem [!DNL Journey Optimizer Campaign].

## Aktivieren [!DNL Adobe Journey Optimizer] {#enable-ajo}

Zu Beginn der Verwendung von [!DNL Adobe Journey Optimizer]führen Sie die folgenden Schritte aus.

1. Durchsuchen Sie die [Voraussetzungen](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#prerequesites) von [!DNL Adobe Journey Optimizer] [Handbuch für Web-Erlebnisse](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), insbesondere:
   * Einrichten [!DNL Adobe Experience Cloud Visual Editing Helper].
   * Aktivieren [!DNL Adobe Journey Optimizer] in [datastream](../../datastreams/overview.md).
   * Aktivieren Sie die [!UICONTROL Richtlinie zur aktiven Zusammenführung auf Edge] -Option.

2. Fügen Sie die `renderDecisions` -Option zu Ihren Ereignissen hinzufügen. Satz `renderDecisions` nach `true` für die automatische Darstellung von bereitgestellten Journey Optimizer-Inhaltsvorschlägen auf Webseiten.

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. Optional können Sie in Ihren Ereignissen zusätzliche Oberflächen angeben. Standardmäßig generiert das Web SDK automatisch die Weboberfläche für die aktuelle Webseite und fügt sie in die Anforderung an das Edge-Netzwerk ein. Bei Bedarf können zusätzliche Oberflächen in die Anforderung eingeschlossen werden, indem Sie diese in der `personalization.surfaces` der `sendEvent` -Befehl oder im entsprechenden **[!UICONTROL Oberflächen]** [[!UICONTROL Ereignis senden] action](../../extension/action-types.md#send-event) Konfiguration der Web SDK-Erweiterung.

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
       "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![extension-add-interface](./assets/extension-add-surface.png)

   Ereignisflächen sind im `query.personalization.surfaces` Anforderungsfeld:

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

4. Ähnlich wie bei anderen Personalisierungsfunktionen können Sie auch eine **[Codeausschnitt vorab ausblenden](../manage-flicker.md)** , um beim Abrufen von Erlebnissen nur bestimmte Teile der Seite auszublenden.

## Erstellen von Adobe Journey Optimizer-Web-Erlebnissen {#create-ajo-web-experiences}

Befolgen Sie die [Erstellung von Web-Kampagnen](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#create-web-campaign) Anweisungen aus [!DNL Adobe Journey Optimizer] [Handbuch für Web-Erlebnisse](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) erstellen [!DNL Journey Optimizer Web] Kampagnen und Erlebnisse.

## Rendern von personalisiertem Inhalt {#rendering-personalized-content}

Weitere Informationen finden Sie in der Dokumentation unter [Rendern von Personalisierungsinhalten](../rendering-personalization-content.md) für weitere Informationen.

Adobe Journey Optimizer-Vorschläge für Weboberflächen werden auf ähnliche Weise wie die `__view__` Vorschläge für den Entscheidungsbereich. Insbesondere wann `renderDecisions` ist auf `true` im `sendEvent` verwenden, werden diese automatisch vom Web SDK gerendert.

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

Zum Debuggen von Adobe Journey Optimizer-Personalisierungsimplementierungen verwenden Sie [[!DNL Web SDK] Debugging](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html). [!DNL Adobe Journey Optimizer] Debug-Traces sind verfügbar, wenn Sie die Fehlerbehebung mit [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). Suchen Sie nach Ereignissen mit dem `AJO:` -Präfix.

![assurance-ajo-trace](./assets/assurance-ajo-trace.png)
