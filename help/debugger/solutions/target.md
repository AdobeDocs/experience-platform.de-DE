---
title: Testen einer Adobe Target-Implementierung mit Adobe Experience Platform Debugger
description: Erfahren Sie, wie Sie mit Adobe Experience Platform Debugger eine Website testen und debuggen können, die für Adobe Target aktiviert ist.
source-git-commit: 1ce7ac78936040d76faa3a58b92333a737fbeb66
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 6%

---

# Testen einer Adobe Target-Implementierung mit Adobe Experience Platform Debugger

Adobe Experience Platform Debugger bietet eine Suite nützlicher Tools zum Testen und Debuggen einer Website, die mit einer Adobe Target-Implementierung ausgestattet wurde. In diesem Handbuch werden einige gängige Workflows und Best Practices für die Verwendung von Platform Debugger auf einer Target-fähigen Website behandelt.

## Voraussetzungen

Um Platform Debugger für Target zu verwenden, muss die Website die [at.js-Bibliothek](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/) Version 1.x oder höher. Frühere Versionen werden nicht unterstützt.

## Platform Debugger initialisieren

Öffnen Sie die Website, die Sie testen möchten, in einem Browser und öffnen Sie dann die Platform Debugger-Erweiterung.

Wählen Sie **[!DNL Target]** in der linken Navigation aus. Wenn Platform Debugger erkennt, dass eine kompatible Version von at.js auf der Site ausgeführt wird, werden Adobe Target-Implementierungsdetails angezeigt.

![Die im Platform Debugger ausgewählte Target-Ansicht gibt an, dass Adobe Target auf der aktuell angezeigten Browserseite aktiv ist.](../images/solutions/target/target-initialized.png)

## Globale Konfigurationsinformationen

Informationen zur globalen Konfiguration der Implementierung werden oben in der Target-Ansicht in Platform Debugger angezeigt.

![Globale Konfigurationsinformationen für Target im Platform Debugger hervorgehoben](../images/solutions/target/global-config.png)

| Name | Beschreibung |
| --- | --- |
| Clientcode | Eine eindeutige ID, die Ihre Organisation identifiziert. |
| Version | Die aktuell auf der Website installierte Version der Adobe Target-Bibliothek. |
| Globaler Anforderungsname | Der Name der [globale Mbox](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/?) für die Target-Implementierung der Standardname ist `target-global-mbox`. |
| Ereignis zum Laden der Seite | Ein boolescher Wert, der angibt, ob ein [Seitenladeereignis](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/how-atjs-works/#atjs-2x-diagrams) hat stattgefunden. Seitenladeereignisse werden nur für at.js 2.x unterstützt. Bei nicht kompatiblen Versionen wird dieser Wert standardmäßig auf `None`. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Network Requests] {#network}

Auswählen **[!DNL Network Requests]** um zusammenfassende Informationen zu den einzelnen Netzwerkanfragen anzuzeigen, die auf der Seite durchgeführt wurden.

![Die [!DNL Network Requests] für Target, das im Platform Debugger ausgewählt wurde](../images/solutions/target/network-requests.png)

Wenn Sie Aktionen auf der Seite ausführen (einschließlich des Neuladens der Seite), werden der Tabelle automatisch neue Spalten hinzugefügt, sodass Sie die Aktionssequenz und die Art und Weise, wie Werte zwischen den einzelnen Anforderungen verändert werden, anzeigen können.

![Die [!DNL Network Requests] für Target, das im Platform Debugger ausgewählt wurde](../images/solutions/target/new-request.png)

Die folgenden Werte werden erfasst:

| Name | Beschreibung |
| --- | --- |
| [!DNL Page Title] | Der Titel der Seite, die diese Anfrage initiiert hat. |
| [!DNL Page URL] | Die URL der Seite, die die Anfrage initiiert hat. |
| [!DNL URL] | Die unformatierte URL der Anfrage. |
| [!DNL Method] | Die HTTP-Methode für die Anfrage. |
| [!DNL Query String] | Die Abfragezeichenfolge der Anfrage, die aus der URL stammt. |
| [!DNL POST Body] | Der Text der Anfrage (nur für POST-Anforderungen festgelegt). |
| [!DNL Pathname] | Der Pfadname der Anfrage-URL. |
| [!DNL Hostname] | Der Hostname der Anfrage-URL. |
| [!DNL Domain] | Die Domäne der Anfrage-URL. |
| [!DNL Timestamp] | Ein Zeitstempel, der angibt, wann die Anfrage (oder das Ereignis) innerhalb der Zeitzone des Browsers stattgefunden hat. |
| [!DNL Time Since Page Load] | Die seit dem ersten Laden der Seite zum Zeitpunkt der Anforderung verstrichene Zeit. |
| [!DNL Initiator] | Der Initiator der Anfrage. Mit anderen Worten, wer hat die Bitte gestellt? |
| [!DNL clientCode] | Die Kennung für das Konto Ihres Unternehmens, die von Target erkannt wurde. |
| [!DNL requestType] | Die für die Anfrage verwendete API. Bei Verwendung von at.js 1.x lautet der Wert `/json`. Bei Verwendung von at.js 2.x lautet der Wert `delivery`. |
| [!DNL Audience Manager Blob] | Stellt Informationen zu verschlüsselten Audience Manager-Metadaten bereit, die als &quot;Blob&quot;bezeichnet werden. |
| [!DNL Audience Location Hint] | Die Regions-ID für die Datenerfassung. Dies ist eine numerische ID für den geografischen Standort eines bestimmten ID-Dienst-Rechenzentrums. Weitere Informationen finden Sie in der Audience Manager-Dokumentation unter [DCS-Regions-IDs, Standorte und Hostnamen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html?lang=de) und das Handbuch zum Experience Cloud Identity Service [`getLocationHint`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/getlocationhint.html?lang=en#reference-a761030ff06c4439946bb56febf42d4c). |
| [!DNL Browser Height] | Die Browser-Höhe in Pixel. |
| [!DNL Browser Time Offset] | Der mit der Zeitzone des Browsers verknüpfte Zeitversatz. |
| [!DNL Browser Width] | Die Browser-Breite in Pixel. |
| [!DNL Color Depth] | Die Farbtiefe des Bildschirms. |
| [!DNL context] | Ein Objekt, das Kontextinformationen über den Browser enthält, der für die Anforderung verwendet wird, einschließlich Bildschirmmaßen und Client-Plattform. |
| [!DNL prefetch] | Die Parameter, die in während `prefetch` Verarbeitung. |
| [!DNL execute] | Die Parameter, die während `execute` Verarbeitung. |
| [!DNL Experience Cloud Visitor ID] | Wenn eine erkannt wird, enthält Informationen zum [Experience Cloud-ID (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de) , das dem aktuellen Site-Besucher zugewiesen ist. |
| [!DNL experienceCloud] | Enthält die Experience Cloud-IDs für diese spezifische Benutzersitzung: A4T [Zusatzdaten-ID](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html?#section_2C1F745A2B7D41FE9E30915539226E3A)und [Besucher-ID (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html). |
| [!DNL id] | Die [Target-ID](https://developers.adobetarget.com/api/delivery-api/#section/Identifying-Visitors/Target-ID) für den Besucher. |
| [!DNL Mbox Host] | Die [Host](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=de) dass die Target-Anfrage an gesendet wurde. |
| [!DNL Mbox PC] | Eine Zeichenfolge, die die [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) Sitzungs-ID und [Adobe Target Edge](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934) Standorthinweis. Dieser Wert wird von at.js verwendet, um sicherzustellen, dass die Sitzung und der Edge-Standort persistent bleiben. |
| [!DNL Mbox Referrer] | Die URL-Referenz für die spezifische [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) -Anfrage. |
| [!DNL Mbox URL] | Die URL für die [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) Server. |
| [!DNL Mbox Version] | Die Version von [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) verwendet werden. |
| [!DNL mbox3rdPartyId] | Die [`mbox3rdPartyId`](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) dem aktuellen Besucher zugewiesen. |
| [!DNL mboxRid] | Die [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) Anfrage-ID. |
| [!DNL requestId] | Eine eindeutige ID für die Anfrage. |
| [!DNL Screen Height] | Die Höhe des Bildschirms in Pixel. |
| [!DNL Screen Width] | Die Breite des Bildschirms in Pixel. |
| [!DNL Supplemental Data ID] | Eine systemgenerierte ID, mit der Besucher mit entsprechenden Adobe Target- und Adobe Analytics-Aufrufen abgeglichen werden. Siehe [Handbuch zur Fehlerbehebung bei A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/troubleshoot-a4t/a4t-troubleshooting.html?#section_75002584FA63456D8D9086172925DD8D) für weitere Informationen. |
| [!DNL vst] | Die [Experience Cloud Identity Service-API-Konfiguration](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/function-vars.html). |
| [!DNL webGLRenderer] | Enthält Informationen zum auf der Seite verwendeten WebGL-Renderer, falls zutreffend. |

{style=&quot;table-layout:auto&quot;}

Um die Details eines Parameters für ein bestimmtes Netzwerkereignis anzuzeigen, wählen Sie die betreffende Tabellenzelle aus. Es wird ein Popover mit weiteren Informationen zum Parameter angezeigt, einschließlich einer Beschreibung und dessen Wert. Wenn der Wert ein JSON-Objekt ist, enthält das Dialogfeld eine vollständig navigierbare Ansicht der Objektstruktur.

![Die [!DNL Network Requests] für Target, das im Platform Debugger ausgewählt wurde](../images/solutions/target/request-param-details.png)

## [!DNL Configuration]

Auswählen **[!DNL Configuration]** um eine Auswahl zusätzlicher Debuggingwerkzeuge für Target zu aktivieren oder zu deaktivieren.

![Die [!DNL Configuration Requests] für Target, das im Platform Debugger ausgewählt wurde](../images/solutions/target/configuration.png)

| Debugging-Tool | Beschreibung |
| --- | --- |
| [!DNL Target Console Logging] | Wenn diese Option aktiviert ist, können Sie auf die at.js-Protokolle auf der Registerkarte &quot;Konsole&quot;des Browsers zugreifen. Diese Funktion kann auch durch Hinzufügen eines `mboxDebug` Abfrageparameter (mit beliebigem Wert) zur Browser-URL. |
| [!DNL Target Diable] | Wenn diese Option aktiviert ist, sind alle Target-Funktionen auf der Seite deaktiviert. Auf diese Weise können Sie bestimmen, ob ein Target-spezifisches Angebot das Problem auf der Seite verursacht. |
| [!DNL Target Trace] | **Hinweis**: Sie müssen angemeldet sein, um diese Funktion zu aktivieren.<br><br>Wenn diese Option aktiviert ist, werden bei jeder Abfrage Trackingtokens gesendet und in jeder Antwort wird ein Trace-Objekt zurückgegeben. `at.js` analysiert die Antwort `window.__targetTraces`. Jedes Trace-Objekt enthält dieselben Informationen wie das [[!DNL Network Requests] Registerkarte] mit den folgenden Ergänzungen:<ul><li>Eine Momentaufnahme des Profils, in der Attribute vor und nach Anforderungen angezeigt werden.</li><li>Übereinstimmende und nicht übereinstimmende [activities](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html), was zeigt, warum das aktuelle Profil für bestimmte Aktivitäten qualifiziert war oder nicht.<ul><li>Dies kann dabei helfen zu ermitteln, für welche Zielgruppen ein Profil zu einem bestimmten Zeitpunkt qualifiziert ist und warum.</li><li>Zieldokumente enthalten mehr Informationen zu verschiedenen Aktivitätstypen</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
